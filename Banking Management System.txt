import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Bank {
    private Map<String, Account> hm;

    public Bank() {
        this.hm = new HashMap<>();
    }

    public void createAccount(String accountNumber, String accountHolder, double initialBalance) {
        if (!hm.containsKey(accountNumber)) {
            Account ac = new Account(accountNumber, accountHolder, initialBalance);
            hm.put(accountNumber, ac);
            System.out.println("Account created successfully!");
        } else {
            System.out.println("Account already exists with the given account number.");
        }
    }

    public void displayAccountDetails(String accountNumber) {
        if (hm.containsKey(accountNumber)) {
            Account account = hm.get(accountNumber);
            System.out.println("Account Number: " + account.getAccountNumber());
            System.out.println("Account Holder: " + account.getAccountHolder());
            System.out.println("Balance: $" + account.getBalance());
        } else {
            System.out.println("Account not found with the given account number.");
        }
    }

    public void performTransaction(String accountNumber, double amount, String transactionType) {
        if (hm.containsKey(accountNumber)) {
            Account account = hm.get(accountNumber);
            if (transactionType.equalsIgnoreCase("deposit")) {
                account.deposit(amount);
            } else if (transactionType.equalsIgnoreCase("withdraw")) {
                account.withdraw(amount);
            } else {
                System.out.println("Invalid transaction type. Please choose deposit or withdraw.");
            }
        } else {
            System.out.println("Account not found with the given account number.");
        }
    }
}

class Account {
    private String accountNumber;
    private String accountHolder;
    private double balance;
    public Account(String accountNumber, String accountHolder, double initialBalance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
    }
    public String getAccountNumber() {
        return accountNumber;
    }
    public String getAccountHolder() {
        return accountHolder;
    }
    public double getBalance() {
        return balance;
    }
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposit successful. New balance: $" + balance);
    }
    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawal successful. New balance: $" + balance);
        } else {
            System.out.println("Insufficient funds for withdrawal.");
        }
    }
}
 class BankingManagementSystem {
    public static void main(String[] args) {
        Bank bank = new Bank();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nBanking Management System");
            System.out.println("1. Create Account");
            System.out.println("2. Display Account Details");
            System.out.println("3. Perform Transaction");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");

            int c = scanner.nextInt();
            scanner.nextLine();

            switch (c) {
                case 1:
                    System.out.print("Enter Account Number: ");
                    String accNumber = scanner.nextLine();
                    System.out.print("Enter Account Holder Name: ");
                    String accHolder = scanner.nextLine();
                    System.out.print("Enter Initial Balance: $");
                    double initialBalance = scanner.nextDouble();
                    bank.createAccount(accNumber, accHolder, initialBalance);
                    break;

                case 2:
                    System.out.print("Enter Account Number: ");
                    String displayAccNumber = scanner.nextLine();
                    bank.displayAccountDetails(displayAccNumber);
                    break;

                case 3:
                    System.out.print("Enter Account Number: ");
                    String transAccNumber = scanner.nextLine();
                    System.out.print("Enter Transaction Type (Deposit/Withdraw): ");
                    String transType = scanner.nextLine();
                    System.out.print("Enter Amount: $");
                    double transAmount = scanner.nextDouble();
                    bank.performTransaction(transAccNumber, transAmount, transType);
                    break;

                case 4:
                    System.out.println("Exiting Banking Management System. Goodbye!");
                    System.exit(0);

                default:
                    System.out.println("Invalid choice. Please enter a valid option.");
            }
        }
    }
}