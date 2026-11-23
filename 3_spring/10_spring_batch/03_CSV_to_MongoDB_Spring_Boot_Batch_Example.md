# CSV to MongoDB Spring Boot Batch Example

**CSV to MongoDB Spring Boot Batch Example** | In the previous example we have seen [Spring Boot Batch CSV to MySQL database](./02_CSV_To_MySQL_Database_Spring_Boot_Batch_API_Example.md). Now we will see the Spring Boot batch CSV to MongoDB example.

- [Related Tutorials](#1-related-tutorials)
- [MongoDB Properties](#2-mongodb-properties)
- [CSV to MongoDB Spring Boot Batch](#3-csv-to-mongodb-spring-boot-batch)
- [CSV File](#4-csv-file)
- [Application Properties](#5-application-properties)
- [Model Class](#6-model-class)
- [Batch Configuration](#7-batch-configuration)
- [Controller Class](#8-controller-class)
- [MongoDB Output](#9-mongodb-output)

---

## 1. Related Tutorials

- 📖 [Spring Boot Batch API Introduction](./01_Spring_Boot_Batch_API_Introduction.md)
- 🗄️ [CSV To MySQL Database Spring Boot Batch API Example](./02_CSV_To_MySQL_Database_Spring_Boot_Batch_API_Example.md)
- 📤 [MySQL to CSV Spring Boot Batch Example](./04_MySQL_to_CSV_Spring_Boot_Batch_Example.md)
- 🍃 [MongoDB to CSV Spring Boot Batch Example](./05_MongoDB_to_CSV_Spring_Boot_Batch_Example.md)
- 📄 [MySQL to XML Spring Boot Batch Example](./06_MySQL_to_XML_Spring_Boot_Batch_Example.md)

---

## 2. MongoDB Properties

🔧 **Configuration** (`application.properties`):

```properties
spring.data.mongodb.host=localhost
spring.data.mongodb.port=27017
spring.data.mongodb.database=sample
```

For MongoDB:

- 📦 `MongoItemWriter` is the implementation class of the `ItemWriter` interface.
- ⚙️ [MongoTemplate](../04_nosql_databases/06_MongoTemplate_Spring_Boot_Example.md) will be used which can be auto-configured.
- 🗂️ The collection name is used while creating and inserting the data.

```mermaid
graph LR
    CSV["📄 CSV File"] --> R["ItemReader"]
    R --> P["ItemProcessor"]
    P --> W["MongoItemWriter"]
    W --> DB[("🍃 MongoDB")]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff

    class CSV orange
    class R purple
    class P cyan
    class W green
    class DB orange
```

---

## 3. CSV to MongoDB Spring Boot Batch

Create a Spring starter project with the following dependencies: `Lombok`, `Spring Batch`, `Spring Data MongoDB`, `H2 Database`, `Spring web`. The H2 database is used for repository purposes.

🏗️ **Different Classes/Files:**

| File 📄 | Purpose 📋 |
|---------|-----------|
| **Model class** | Defines the `Product` entity |
| **Batch Config** | Configures reader, processor, writer, step, and job |
| **Properties file** | MongoDB connection and batch settings |
| **Controller class** | REST endpoint to trigger the batch job |
| **CSV file** | Source data (`products.csv`) |

---

## 4. CSV File

**`products.csv`:**

```csv
id,code,cost
10,PEN,200.0
11,BOOK,500.0
12,BOTTLE,600.0
13,MOBILE,1500.0
14,MOUSE,300.0
15,KEYBOAD,900.0
16,BAG,600.0
```

---

## 5. Application Properties

🔧 **Configuration** (`application.properties`):

```properties
spring.data.mongodb.host=localhost
spring.data.mongodb.port=27017
spring.data.mongodb.database=sample
spring.batch.job.enabled=false
```

📝 **Note:** `spring.batch.job.enabled=false` disables automatic job execution at startup. The job will be triggered manually via the REST controller.

---

## 6. Model Class

**`Product.java`:**

```java
package com.knowprogram.demo.model;

import org.springframework.data.annotation.Id;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Product {
    @Id
    private Integer prodId;

    private String prodCode;

    private Double prodCost;

    private Double prodTax;

    private Double prodDiscount;
}
```

---

## 7. Batch Configuration

In the `BatchConfig` file, compared to the previous example of [CSV to MySQL](./02_CSV_To_MySQL_Database_Spring_Boot_Batch_API_Example.md), mainly the `writer()` bean method logic changes and `ProductRepository` is replaced with `MongoTemplate`. The remaining code will remain the same.

🔑 **Key Changes:**
- 🍃 `MongoTemplate` is autowired instead of a JPA repository
- 📦 `MongoItemWriter` replaces the JPA-based `ItemWriter`
- 🗂️ A collection name (`"products"`) is specified for MongoDB

**`BatchConfig.java`:**

```java
@Configuration
public class BatchConfig {

    @Autowired
    private MongoTemplate mongoTemplate;

    @Bean
    ItemReader<Product> reader() {
        FlatFileItemReader<Product> itemReader = new FlatFileItemReader<>();
        itemReader.setResource(new ClassPathResource("products.csv"));
        itemReader.setName("csv-reader");
        itemReader.setLinesToSkip(1); // to skip heading

        itemReader.setLineMapper(new DefaultLineMapper<>() {
            {
                setLineTokenizer(new DelimitedLineTokenizer() {
                    {
                        setDelimiter(DELIMITER_COMMA);
                        // variables name
                        setNames("prodId", "prodCode", "prodCost");
                        setStrict(false);
                    }
                });
                setFieldSetMapper(new BeanWrapperFieldSetMapper<>() {
                    {
                        setTargetType(Product.class);
                    }
                });
            }
        });

        return itemReader;
    }

    @Bean
    ItemProcessor<Product, Product> processor() {
        return item -> {
            item.setProdTax(item.getProdCost() * 0.12);
            item.setProdDiscount(item.getProdCost() * 0.08);
            return item;
        };
    }

    @Bean
    ItemWriter<Product> writer() {
        MongoItemWriter<Product> writer = new MongoItemWriter<>();
        writer.setTemplate(mongoTemplate);
        writer.setCollection("products"); // collection name
        return writer;
    }

    @Bean
    Step step(JobRepository repository, PlatformTransactionManager transactionManager) {
        return new StepBuilder("csv-step", repository)
                .<Product, Product>chunk(10, transactionManager)
                .reader(reader())
                .processor(processor()).writer(writer())
                .taskExecutor(new SimpleAsyncTaskExecutor() {
                    private static final long serialVersionUID = 1L;
                    {
                        setConcurrencyLimit(10);
                    }
                })
                .build();
    }

    @Bean
    JobExecutionListener listener() {
        return new JobExecutionListener() {
            @Override
            public void beforeJob(JobExecution jobExecution) {
                System.out.println("MyJobListener.beforeJob()");
            }

            @Override
            public void afterJob(JobExecution jobExecution) {
                System.out.println("MyJobListener.afterJob()");
            }
        };
    }

    @Bean(name = "csvJob")
    Job job(JobRepository jobRepository, PlatformTransactionManager transactionManager) {
        return new JobBuilder("csv-job", jobRepository)
                .listener(listener())
                .flow(step(jobRepository, transactionManager))
                .end()
                .build();
    }
}
```

> 💡 **Tip:** The `MongoTemplate` is auto-configured by Spring Boot when `spring-data-mongodb` is on the classpath. The `writer()` method highlights the key difference from the MySQL example — using `MongoItemWriter` with `setTemplate()` and `setCollection()`.

---

## 8. Controller Class

**`ProductBatchController.java`:**

```java
@RestController
package com.knowprogram.demo.controller;

public class ProductBatchController {

    @Autowired
    private JobLauncher jobLauncher;

    @Autowired
    private Job job;

    @GetMapping("/startBatch")
    public String startBatch() throws JobExecutionAlreadyRunningException,
        JobRestartException,
        JobInstanceAlreadyCompleteException,
        JobParametersInvalidException {
        JobParameters params = new JobParametersBuilder()
             .addLong("time", System.currentTimeMillis())
             .toJobParameters();

        JobExecution run = jobLauncher.run(job, params);
        return run.getStatus().toString();
    }

}
```

🌐 **Endpoint:** Hit `GET /startBatch` to trigger the batch job. The response returns the job execution status (e.g., `COMPLETED`).

---

## 9. MongoDB Output

After running the batch job, verify the data in MongoDB using the Mongo shell:

**Mongo shell commands:**

```bash
> use sample
> show collections
> db.products.find()
```

📤 **Output:**

```json
[
  {
    _id: 13,
    prodCode: 'MOBILE',
    prodCost: 1500,
    prodTax: 180,
    prodDiscount: 120,
    _class: 'com.knowprogram.demo.model.Product'
  },
  {
    _id: 15,
    prodCode: 'KEYBOAD',
    prodCost: 900,
    prodTax: 108,
    prodDiscount: 72,
    _class: 'com.knowprogram.demo.model.Product'
  },
  {
    _id: 12,
    prodCode: 'BOTTLE',
    prodCost: 600,
    prodTax: 72,
    prodDiscount: 48,
    _class: 'com.knowprogram.demo.model.Product'
  },
  {
    _id: 10,
    prodCode: 'PEN',
    prodCost: 200,
    prodTax: 24,
    prodDiscount: 16,
    _class: 'com.knowprogram.demo.model.Product'
  },
  {
    _id: 14,
    prodCode: 'MOUSE',
    prodCost: 300,
    prodTax: 36,
    prodDiscount: 24,
    _class: 'com.knowprogram.demo.model.Product'
  },
  {
    _id: 11,
    prodCode: 'BOOK',
    prodCost: 500,
    prodTax: 60,
    prodDiscount: 40,
    _class: 'com.knowprogram.demo.model.Product'
  },
  {
    _id: 16,
    prodCode: 'BAG',
    prodCost: 600,
    prodTax: 72,
    prodDiscount: 48,
    _class: 'com.knowprogram.demo.model.Product'
  }
]
```

> 📝 **Note:** The `_class` field is automatically added by Spring Data MongoDB to store the fully qualified class name for deserialization purposes.
