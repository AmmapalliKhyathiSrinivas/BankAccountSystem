# BankAccountSystem
This project simulates basic banking operations like checking balance, depositing money, and withdrawing money using structures.

## Bank Account
The `Account` structure holds the account number, holder's name, and balance.

## Functions
The `deposit`, `withdraw`, and `display` functions perform operations on the account.

## Menu
The program provides options to deposit money, withdraw money, or view the balance.

```c
#include <stdio.h>

struct Account {
    int accountNumber;
    char holderName[50];
    float balance;
};

void deposit(struct Account *acc, float amount) {
    acc->balance += amount;
    printf("Deposited: %.2f\n", amount);
}

void withdraw(struct Account *acc, float amount) {
    if (acc->balance >= amount) {
        acc->balance -= amount;
        printf("Withdrawn: %.2f\n", amount);
    } else {
        printf("Insufficient balance.\n");
    }
}

void display(struct Account acc) {
    printf("\nAccount Number: %d\n", acc.accountNumber);
    printf("Account Holder: %s\n", acc.holderName);
    printf("Current Balance: %.2f\n", acc.balance);
}

int main() {
    struct Account account;

    printf("Enter Account Number: ");
    scanf("%d", &account.accountNumber);
    getchar();  // To consume the newline left by scanf

    printf("Enter Account Holder's Name: ");
    fgets(account.holderName, sizeof(account.holderName), stdin);
    account.holderName[strcspn(account.holderName, "\n")] = 0;  // Remove the newline

    account.balance = 0.0f;  // Initialize balance to 0

    int choice;
    float amount;

    while (1) {
        printf("\nBank Account System\n");
        printf("1. Deposit\n");
        printf("2. Withdraw\n");
        printf("3. Display Balance\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            printf("Enter deposit amount: ");
            scanf("%f", &amount);
            deposit(&account, amount);
            break;
        case 2:
            printf("Enter withdrawal amount: ");
            scanf("%f", &amount);
            withdraw(&account, amount);
            break;
        case 3:
            display(account);
            break;
        case 4:
            printf("Exiting...\n");
            return 0;
        default:
            printf("Invalid choice! Please try again.\n");
        }
    }

    return 0;
}
