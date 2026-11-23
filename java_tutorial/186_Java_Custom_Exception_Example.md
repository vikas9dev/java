# Java Custom Exception Example

**Java Custom Exception Example** | Real-world examples of developing and using user-defined custom exceptions in Java applications.

- [Java Custom Exception Example -- 1](#java-custom-exception-example--1)
- [Java Custom Exception Example -- 2](#java-custom-exception-example--2)

---

In the previous post, we learned how to develop a user-defined custom exception in Java. We discussed it through a custom exception example. Now, we will develop more Java custom exception examples.

Prerequisite: [How to develop User-defined Custom exception in Java](185_Develop_User_defined_Custom_Exception_in_Java.md)

---

## 1. Java Custom Exception Example -- 1

**Register the person for voting based on age.**

**Develop a Java program to register the person for voting. If the age of the person is less than or equal to 17 (age <= 17) then he/she is not eligible for voting, don't register them, give exception messages.**

1️⃣ **Develop `NotEligibleException` derived from `java.lang.Exception` class (checked exception):**

```java
public class NotEligibleException extends Exception {

   // no-arg constructor
   public NotEligibleException(){
        super();
   }

   // String-arg constructor
   public NotEligibleException(String msg) {
        super(msg);
   }

 }
```

2️⃣ **Develop `Register` class with `checkAge(int age)` method:**

```java
public class Register {

    public static void checkAge(int age)
              throws NotEligibleException {

      if(age<=17)
         throw new NotEligibleException(
               "Age<=17, not eligible for voting");

    }
 }
```

3️⃣ **Develop `VoterList` class to perform the registering operations:**

```java
import java.util.Scanner;

public class VoterList {

  public static void main(String[] args) {

   // declare variables
   int age = 0;

   // create Scanner class object
   Scanner scan = new Scanner(System.in);

   // read age
   System.out.print("Enter age: ");
   age = scan.nextInt();

   // check age
   try {
     Register.checkAge(age);
     System.out.println("Registering in the voting list.");
     System.out.println("Registration completed.");
   } catch(NotEligibleException e) {
     System.out.println(e.getMessage());
   }

  }
}
```

📤 **Output for different test-cases:**

```
Enter age: 20
Registering in the voting list.
Registration completed.
```

```
Enter age: 16
Age<=17, not eligible for voting
```

---

## 2. Java Custom Exception Example -- 2

**Create an ATM class to perform deposit and withdrawal operations. Define custom exceptions `InvalidAmountException`, `InsufficientFundsException` to handle operations done by the customer in deposit and withdrawal operations.**

Here we need to develop mainly 5 Java classes:

1. 🚨 **`InvalidAmountException`** — for user-defined custom exception
2. 💰 **`InsufficientFundsException`** — for user-defined custom exception
3. 💳 **`ATMCard`** — An interface, which has properties `deposit()`, `withdraw()` and `balanceEnquiry()`.
4. 🏦 **`CitiBank`** — A class implemented from `ATMCard` interface
5. 🏧 **`ATM`** — A class to perform operations of ATM (automatic teller machine).

We will also develop another Bank class for our better understanding purpose.

6. 🏦 **`AmericanBank`** — Another class implemented from `ATMCard` interface.

> 📝 **Note:** All Banks have these properties:  
> - Customers are not allowed to deposit amount <= 0 (throw `InvalidAmountException`).  
> - Customers are not allowed to withdraw amount <= 0 (throw `InvalidAmountException`).  
> - Customers are also not allowed to withdraw an amount greater than (>) the available amount (throw `InsufficientFundsException`).

**InvalidAmountException.java:**

```java
// InvalidAmountException.java
public class InvalidAmountException extends Exception {

   // no-arg constructor
   public InvalidAmountException(){
          super();
   }

   // String-arg constructor
   public InvalidAmountException(String msg) {
     super(msg);
   }

}
```

**InsufficientFundsException.java:**

```java
// InsufficientFundsException.java
public class InsufficientFundsException extends Exception {

   // no-arg constructor
   public InsufficientFundsException(){
      super();
   }

   public InsufficientFundsException(String msg){
      // String-arg constructor
      super(msg);
   }
}
```

**ATMCard.java (interface):**

```java
// ATMCard.java
// Contains abstract methods
interface ATMCard {

   public void deposit(double amount)
         throws InvalidAmountException;

   public double withdraw(double amount)
     throws InvalidAmountException,
            InsufficientFundsException;

   public double balanceEnquiry();
}
```

**CitiBank.java:**

```java
// CitiBank.java
public class CitiBank implements ATMCard{

  // balance should not be accessible to everyone
  private double balance;

  // instance block
  {
    // Opening account balance with 1500
    // you can take any number
    this.balance = 1500;
  }

  // method to perform deposit operation
  public void deposit(double amount)
              throws InvalidAmountException {

    if( amount <= 0) {
      throw new InvalidAmountException(
               "Invalid amount; amount<=0");
    }
    balance = balance + amount;

  }

  // method to perform withdraw operation
  public double withdraw(double amount)
         throws InvalidAmountException,
                InsufficientFundsException {

    if( amount <= 0) {
      throw new InvalidAmountException(
              "Invalid amount; amount<=0");
    }

    if( balance < amount) {
      throw new InsufficientFundsException(amount +
                 " not available in your account");
    }
    balance = balance - amount;
    return amount;
  }

  // method to perform balanceEnquiry operation
  public double balanceEnquiry(){
    return balance;
  }

}
```

All banks are doing the same thing so, code-wise no difference between `AmericanBank.java` and `CitiBank.java`.

**AmericanBank.java:**

```java
//AmericanBank.java
public class AmericanBank implements ATMCard {

  // balance should not be accessible to everyone
  private double balance;

  // instance block
  {
    // Opening account with 2000
    this.balance = 2000;
  }

  // method to perform deposit operation
  public void deposit(double amount)
              throws InvalidAmountException {

    if( amount <= 0) {
      throw new InvalidAmountException(
               "Invalid amount; amount<=0");
    }
    balance = balance + amount;

  }

  // method to perform withdraw operation
  public double withdraw(double amount)
         throws InvalidAmountException,
               InsufficientFundsException {

    if( amount <= 0) {
      throw new InvalidAmountException(
               "Invalid amount; amount<=0");
    }
    if( balance < amount) {
      throw new InsufficientFundsException(amount +
                " not available in your account");
    }
    balance = balance - amount;
    return amount;
  }

  // method to perform balanceEnquiry operation
  public double balanceEnquiry(){
    return balance;
  }

}
```

### Class for Performing Operations

**ATM.java:**

```java
//ATM.java
import java.util.Scanner;

public class ATM {

  public static void main(String[] args)
    throws InstantiationException,
                         IllegalAccessException {

   /* Declare variables
    * To avoid NullPointerException
    * initialize them with their default value
    */
   String bankName = null, nextOption = null;
   int option = null;
   double amount = 0.0, withdrawalAmount = 0.0;

   // create Scanner class object
   Scanner scan = new Scanner(System.in);

   /* Outer while loop wil keep ATM machine
    * always in the active mode
    * Program will remain always active
    */
   while(true){

     // read input
     System.out.print("Enter ATMCard (BankName): ");
     bankName = scan.next();

     try {
       // reading class dynamically at runtime
       ATMCard card =
          (ATMCard)Class.forName(bankName).newInstance();

       start: //label
       while(true) { //inner-while loop
         System.out.println("\n*****Choose operation*****");
         System.out.println(" 1. Deposit");
         System.out.println(" 2. Withdraw");
         System.out.println(" 3. Balance Enquiry");
         System.out.println(" 4. Exit");
         option = scan.nextInt();

         try {
           switch(option){

             // deposit operation
             case 1:
             {
               System.out.print("Enter amount to deposit: ");
               amount = scan.nextDouble();
               card.deposit(amount);
               System.out.println("Amount "+ amount +
                                       " deposited");
               break;
             }

             // withdraw operation
             case 2:
             {
               System.out.print("Enter amount to withdraw: ");
               amount = scan.nextDouble();
               withdrawalAmount = card.withdraw(amount);
               System.out.println("Collect "+
                               withdrawalAmount+" cash");
               break;
             }

             // balance-enquiry operation
             case 3:
             {
               System.out.println("Current Balance: "+
                              card.balanceEnquiry());
               break;
             }

             // exit operation
             case 4:
               break start;

             default:
               System.out.println("Invalid option");
           } //switch close

           // Ask for next operation
           System.out.println("\nDo you want to continue? ");
           System.out.print("Enter Y or N: ");
           nextOption = scan.next();
           if("N".equalsIgnoreCase(nextOption))
               break start;
         } // inner-try close

         catch (InvalidAmountException e) {
           System.out.println(e.getMessage());
         } catch (InsufficientFundsException e) {
           System.out.println(e.getMessage());
         } catch (Exception e) {
           System.out.println(e.getMessage());
         } // inner-catch close
       } //inner-while close

     } // outer-try close
     catch(ClassNotFoundException e) {
       System.out.println("Bank is not available.");
     } catch (Exception e) {
       System.out.println(e.getMessage());
     } // outer-catch close

     System.out.println("\n*********************************");
     System.out.println("    Thank You :) Visit again");
     System.out.println("***********************************\n");

    } //outer-while close
  } // main-method close
} //class close
```

> 📝 **Note:** We are reading BankName dynamically using reflection API, so before executing the ATM class, byte code (.class files) of all classes should be available. This program execution will only stop when we use `System.Exit(0);` in the `ATM.java` class.

#### Different Test Cases for ATM Class

**Test-Case-1:**

```
Enter ATMCard (BankName): BankOfAmerica
Bank is not available.

***********************************
    Thank You :) Visit again
***********************************
```

**Test-Case-2:**

```
Enter ATMCard (BankName): AmericanBank

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
3
Current Balance: 2000.0

Do you want to continue?
Enter Y or N: y

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
1
Enter amount to deposit: -500
Invalid amount; amount<=0

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
1
Enter amount to deposit: 900
Amount 900.0 deposited

Do you want to continue?
Enter Y or N: y

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
3
Current Balance: 2900.0

Do you want to continue?
Enter Y or N: y

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
2
Enter amount to withdraw: -1000
Invalid amount; amount<=0

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
2
Enter amount to withdraw: 2500
Collect 2500.0 cash

Do you want to continue?
Enter Y or N: y

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
3
Current Balance: 400.0

Do you want to continue?
Enter Y or N: n

***********************************
    Thank You :) Visit again
***********************************
```

**Test-Case-3:**

```
Enter ATMCard (BankName): CitiBank

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
3
Current Balance: 1500.0

Do you want to continue?
Enter Y or N: y

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
4

***********************************
    Thank You :) Visit again
***********************************
```

**Test-Case-4:**

```
Enter ATMCard (BankName): CitiBank

*****Choose operation*****
 1. Deposit
 2. Withdraw
 3. Balance Enquiry
 4. Exit
5
Invalid option

Do you want to continue?
Enter Y or N: n

***********************************
    Thank You :) Visit again
***********************************
```

**Related Java topics:**

- 🛠️ Different ways to get the exception message in Java
- 🧵 Java Inline Thread Creation
- 🔧 [Different ways to set the Java path](008_Different_ways_to_set_the_Java_path.md)
