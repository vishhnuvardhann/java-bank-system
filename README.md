# Bank Account Management System

A menu-driven console application written in core Java. It manages Savings and Current accounts, records every transaction, and saves data between runs. Built as a Java mini project to demonstrate object-oriented programming.

No database and no external libraries are needed. Only the standard Java library is used.

## Features

- Create **Savings** and **Current** accounts (account numbers start at 1001)
- **Deposit**, **withdraw** and **transfer** money between accounts
- Check balance and print a full **statement** (date, type, amount, balance)
- List all accounts
- Add **4% interest** to Savings accounts
- Data is saved automatically to `bank.dat`, so accounts survive after you exit
- Input validation: letters instead of numbers never crash the program

## Account rules

| Rule | Savings | Current |
|---|---|---|
| Minimum to open | 500 | 0 |
| Minimum balance | 500 | -5000 (overdraft) |
| Interest | 4% on request | None |

## Requirements

- JDK 17 or newer (developed with JDK 21)

Check your version with `javac -version`.

## Getting started

```bash
git clone https://github.com/vishhnuvardhann/java-bank-system.git
cd java-bank-system

# compile
javac -d out src/*.java

# run
java -cp out Main
```

On Windows PowerShell, if `src/*.java` is not expanded, list the files instead:

```
javac -d out src\Account.java src\Bank.java src\CurrentAccount.java src\InsufficientFundsException.java src\Main.java src\SavingsAccount.java src\Transaction.java
```

To start fresh with no accounts, delete `bank.dat`.

## Menu

```
1. Create account   2. Deposit    3. Withdraw
4. Transfer         5. Balance    6. Statement
7. Add interest     8. All accounts   9. Exit
```

## Sample run

```
Choose: 3        (withdraw)
Account no: 1001
Amount: 5000
Error: Withdrawal denied. Minimum balance rule: 500.0

Statement - Ravi (1001)
Date             Type             Amount      Balance
17-11-2026 10:30 OPENING         1000.00      1000.00
17-11-2026 10:31 DEPOSIT          500.00      1500.00
17-11-2026 10:32 WITHDRAW         900.00       600.00
17-11-2026 10:33 INTEREST          24.00       624.00
```

## Project structure

```
java-bank-system/
├── src/
│   ├── Account.java                  abstract base class: deposit, withdraw, history
│   ├── SavingsAccount.java           min balance 500, 4% interest
│   ├── CurrentAccount.java           overdraft up to 5000
│   ├── Transaction.java              one statement line
│   ├── InsufficientFundsException.java   custom checked exception
│   ├── Bank.java                     stores accounts, transfers, save and load
│   └── Main.java                     menu, input validation, error handling
├── README.md
└── .gitignore
```

## OOP concepts used

| Concept | Where |
|---|---|
| Abstraction | `Account` is abstract with abstract methods `getMinBalance()` and `getType()` |
| Inheritance | `SavingsAccount` and `CurrentAccount` extend `Account` |
| Polymorphism | `Account.withdraw()` calls `getMinBalance()`, which each subclass implements differently |
| Encapsulation | Private fields with getters |
| Exception handling | Custom `InsufficientFundsException`, plus handling of invalid input |
| Collections | `LinkedHashMap` for accounts, `ArrayList` for transaction history |
| File I/O | Object serialization to `bank.dat` |

## Limitations

- Console only, with no login or PIN
- Single user at a time
- Money is stored as `double` (a real system would use `BigDecimal`)
- Saved data may become unreadable if the class fields are changed later

## Future scope

- GUI using Swing or JavaFX
- PIN-based login
- Database storage with JDBC and MySQL
- Fixed deposit and loan accounts

## Team

- PandiPrajin
- VishnuVardhan
- S.Ahmed Thalha

