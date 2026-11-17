# Bank Account Management System

A desktop-based **Bank Account Management System built with Java Swing**. The project lets users create and manage Savings and Current accounts, perform banking transactions, and view transaction histories. It also includes a menu-driven console interface.

The application is designed as a Java mini-project to demonstrate **Object-Oriented Programming (OOP)**, exception handling, collections, file handling, and GUI event-driven programming.

> **No database or third-party libraries required.** The project uses the standard Java library.

---

## Table of Contents

- [Features](#features)
- [Screenshots](#screenshots)
- [Technologies Used](#technologies-used)
- [Requirements](#requirements)
- [Getting Started](#getting-started)
- [Running the Application](#running-the-application)
- [Account Rules](#account-rules)
- [Project Structure](#project-structure)
- [OOP Concepts Demonstrated](#oop-concepts-demonstrated)
- [Data Storage](#data-storage)
- [Known Limitations](#known-limitations)
- [Possible Improvements](#possible-improvements)
- [Team](#team)

---

## Features

### Account Management
- Create Savings and Current accounts.
- Automatically generate account numbers, starting from `1001`.
- View all registered accounts and their current balances.

### Banking Operations
- Deposit money into an account.
- Withdraw money subject to account balance rules.
- Transfer money between two different accounts.
- Check an account's balance.
- Apply interest to a Savings account.
- View a complete transaction statement.

### Graphical User Interface
- Java Swing desktop interface.
- Account information displayed in a table.
- Dialog-based forms for account creation and transactions.
- Select an account to perform operations.
- Double-click an account row to open its statement.
- Status messages and error dialogs for invalid operations.

### Console Interface
- A numbered, menu-driven interface.
- Supports the same core banking operations as the GUI.

### Data Persistence and Validation
- Automatically saves account information and transaction history to `bank.dat`.
- Reloads saved information when the application starts.
- Validates transaction amounts and account rules.
- Displays helpful error messages for invalid operations.

---

## Screenshots

The GUI screenshot is available in the `docs` directory.

![Bank Account Management System GUI](docs/gui.png)

---

## Technologies Used

| Technology | Purpose |
|---|---|
| Java | Core application logic |
| Java Swing | Desktop graphical user interface |
| Java AWT | GUI layout and event handling |
| Java Collections | Managing accounts and transaction histories |
| Java Serialization | Saving and loading application data |
| Exception Handling | Handling invalid operations and insufficient funds |

---

## Requirements

- **JDK 17 or newer** (the project was developed with JDK 21).
- A terminal or IDE such as Visual Studio Code, IntelliJ IDEA, or Eclipse.

Check that Java and the Java compiler are installed:

```bash
java -version
javac -version
```

Both commands should display a version number. If `javac` is not recognized, install a JDK and configure its `bin` directory in your system's `PATH`.

---

## Getting Started

### 1. Download or clone the repository

```bash
git clone https://github.com/vishhnuvardhann/java-bank-system.git
```

### 2. Open the project folder

```bash
cd java-bank-system
```

If you downloaded the ZIP file instead, extract it and open the extracted `java-bank-system` folder in your terminal or IDE.

### 3. Compile the source files

**Windows PowerShell:**

```powershell
New-Item -ItemType Directory -Force out | Out-Null
$files = Get-ChildItem .\src\*.java | ForEach-Object { $_.FullName }
javac -d .\out $files
```

**macOS / Linux:**

```bash
mkdir -p out
javac -d out src/*.java
```

If compilation completes without errors, the compiled `.class` files will be placed in the `out` directory.

---

## Running the Application

Run either interface from the project's root directory.

### Option 1: Graphical Interface (Recommended)

```bash
java -cp out BankGUI
```

This opens the Bank Account Management System desktop window.

### Option 2: Console Interface

```bash
java -cp out Main
```

This starts the numbered console menu.

### Console Menu

```text
1. Create account       2. Deposit
3. Withdraw             4. Transfer
5. Balance              6. Statement
7. Add interest         8. All accounts
9. Exit
```

---

## Account Rules

The application supports two account types, each with its own balance restrictions.

| Rule | Savings Account | Current Account |
|---|---:|---:|
| Minimum opening balance | 500 | 0 |
| Minimum permitted balance | 500 | -5,000 |
| Interest | 4% when applied | Not applicable |
| Overdraft facility | No | Up to 5,000 |

**Important notes:**
- A Savings account must be opened with at least `500`.
- A Savings account balance cannot fall below `500`.
- A Current account can have a negative balance up to `-5,000`.
- Deposits and withdrawals must be greater than zero.
- Interest can be applied only to Savings accounts. It is added when the user selects **Add Interest**; it is not automatically applied on a schedule.

---

## Project Structure

```text
java-bank-system/
│
├── src/
│   ├── Account.java
│   ├── Bank.java
│   ├── BankGUI.java
│   ├── CurrentAccount.java
│   ├── InsufficientFundsException.java
│   ├── Main.java
│   ├── SavingsAccount.java
│   └── Transaction.java
│
├── docs/
│   └── gui.png
│
├── .gitignore
└── README.md
```

### Main Classes

| File | Responsibility |
|---|---|
| `Account.java` | Abstract base class containing common account details, balance operations, and transaction history |
| `SavingsAccount.java` | Implements Savings account rules and interest calculation |
| `CurrentAccount.java` | Implements Current account rules and overdraft limit |
| `Transaction.java` | Represents an individual transaction |
| `Bank.java` | Creates, stores, finds, and transfers between accounts; saves and loads bank data |
| `BankGUI.java` | Provides the Java Swing graphical interface |
| `Main.java` | Provides the console-based menu and user interaction |
| `InsufficientFundsException.java` | Custom exception for transactions that violate balance restrictions |

---

## OOP Concepts Demonstrated

This project applies several core Object-Oriented Programming concepts.

| Concept | Implementation |
|---|---|
| **Abstraction** | `Account` is an abstract class that defines common account behaviour. |
| **Inheritance** | `SavingsAccount` and `CurrentAccount` extend `Account`. |
| **Polymorphism** | Each account type provides its own implementation of `getMinBalance()` and `getType()`. |
| **Encapsulation** | Account details are stored in fields and accessed through methods. |
| **Exception Handling** | `InsufficientFundsException` and input validation handle invalid operations. |
| **Collections** | `LinkedHashMap` stores accounts, while `ArrayList` stores transaction history. |
| **File Handling** | Object serialization saves and restores bank data. |
| **Event Handling** | Swing buttons, dialogs, and mouse listeners handle GUI interactions. |

The GUI and console interfaces both use the same `Bank` and account classes. This keeps the banking logic separate from the user interface.

---

## Data Storage

The application uses **Java Object Serialization** to store its data locally.

- File name: `bank.dat`
- Created automatically when the application saves data.
- Stores account information and transaction histories.
- Loaded automatically when the application starts.
- Located in the working directory from which the application is launched.

### Reset the Application

To start with an empty set of accounts:

1. Close the application.
2. Delete `bank.dat` from the project directory.
3. Run the application again.

The application will create a fresh bank instance.

> Keep a backup of `bank.dat` if you want to preserve your account data. This project is an educational demonstration, not a production banking system.

---

## Known Limitations

- No user login, password, or PIN authentication.
- Designed for a single local user.
- Uses `double` for monetary values; production financial software should use a decimal-safe representation such as `BigDecimal`.
- Uses a local serialized file instead of a database.
- Serialized data may not remain compatible if the application's class structure changes.
- No account deletion or account-closing feature.

---

## Possible Improvements

- Add login and PIN-based authentication.
- Introduce database connectivity using JDBC and MySQL.
- Add account deletion and account-closing functionality.
- Add search and filtering for accounts.
- Improve transaction reporting and export statements.
- Build an alternative interface using JavaFX.
- Add Fixed Deposit and Loan account types.

---

## Team

- **PandiPrajin**
- **VishnuVardhan**
- **S. Ahmed Thalha**

---

## Project Purpose

This project was developed as a Java mini-project to demonstrate how OOP principles and core Java concepts can be combined to build a functional application with both graphical and console-based interfaces.

