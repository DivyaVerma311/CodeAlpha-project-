# CodeAlpha-project-
#include <iostream>
#include <vector>
using namespace std;

struct Account {
    int accountNumber;
    string name;
    float balance;
};

vector<Account> accounts;

Account* findAccount(int accNo) {
    for (auto& acc : accounts) {
        if (acc.accountNumber == accNo)
            return &acc;
    }
    return nullptr;
}

void createAccount() {
    Account acc;
    cout << "Enter Account Number: ";
    cin >> acc.accountNumber;
    cout << "Enter Name: ";
    cin >> acc.name;
    cout << "Enter Initial Deposit: ";
    cin >> acc.balance;

    accounts.push_back(acc);
    cout << "Account created successfully!\n";
}

void viewBalance() {
    int accNo;
    cout << "Enter Account Number: ";
    cin >> accNo;

    Account* acc = findAccount(accNo);
    if (acc) {
        cout << "Account Holder: " << acc->name << "\n";
        cout << "Current Balance: " << acc->balance << "\n";
    } else {
        cout << "Account not found.\n";
    }
}

void depositMoney() {
    int accNo;
    float amount;
    cout << "Enter Account Number: ";
    cin >> accNo;

    Account* acc = findAccount(accNo);
    if (acc) {
        cout << "Enter amount to deposit: ";
        cin >> amount;
        acc->balance += amount;
        cout << "Amount deposited successfully. New Balance: " << acc->balance << "\n";
    } else {
        cout << "Account not found.\n";
    }
}

void withdrawMoney() {
    int accNo;
    float amount;
    cout << "Enter Account Number: ";
    cin >> accNo;

    Account* acc = findAccount(accNo);
    if (acc) {
        cout << "Enter amount to withdraw: ";
        cin >> amount;
        if (amount > acc->balance) {
            cout << "Insufficient balance.\n";
        } else {
            acc->balance -= amount;
            cout << "Amount withdrawn successfully. New Balance: " << acc->balance << "\n";
        }
    } else {
        cout << "Account not found.\n";
    }
}

int main() {
    int choice;
    while (true) {
        cout << "\n=== Banking System Menu ===\n";
        cout << "1. Create Account\n2. View Balance\n3. Deposit Money\n4. Withdraw Money\n5. Exit\n";
        cout << "Choose an option: ";
        cin >> choice;

        switch (choice) {
            case 1: createAccount(); break;
            case 2: viewBalance(); break;
            case 3: depositMoney(); break;
            case 4: withdrawMoney(); break;
            case 5: cout << "Exiting...\n"; return 0;
            default: cout << "Invalid choice. Try again.\n";
        }
    }
}
