<div align="center">

# 🏢 T3 Building Management System

### Property Operations • Billing • Accounting • Payroll • Financial Management

A full-stack building management system designed to centralize property operations,
automate recurring billing, manage expenses and payroll, and maintain financial
records through an integrated double-entry accounting system.

<br>

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-4.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-Database-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![JPA](https://img.shields.io/badge/Spring_Data-JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)

</div>

---

## Overview

**T3 Building Management System** is a business application designed to manage
the operational and financial activities of a residential or commercial building.

Instead of treating billing, expenses, salaries, payments, and accounting as
separate processes, the system connects them through a centralized financial
workflow.

The application currently handles:

- Property and unit management
- Electricity billing
- Maintenance billing
- Custom customer charges
- Bulk maintenance billing
- Penalties and waivers
- Payment settlements
- Building expenses
- Employee management
- Payroll and salary accruals
- Chart of Accounts
- Journal vouchers
- Double-entry accounting
- Financial summaries
- Database backup and restore
- User management

---

# 🎯 The Problem

Building management involves more than maintaining a list of properties.

Operational activity continuously creates financial transactions:

```text
Electricity Bills
Maintenance Charges
Custom Charges
        │
        ▼
Accounts Receivable
        │
        ▼
Payments
        │
        ▼
Cash / Bank
```

At the same time:

```text
Building Expenses
Employee Salaries
        │
        ▼
Accounts Payable
        │
        ▼
Settlements
        │
        ▼
Cash / Bank
```

Managing these processes independently can make it difficult to determine:

- what each unit owes
- which bills remain unpaid
- what the building owes to suppliers or employees
- how much cash is available
- where expenses are being incurred
- whether financial records remain balanced

T3 centralizes these workflows and connects operational transactions directly
to the accounting layer.

---

# ✨ Core Features

## 🏠 Unit Management

The system maintains the individual units managed by the building.

Unit records form the foundation for billing and customer-related financial
activity.

The system supports:

- Unit registration
- Unit retrieval and search
- Unit updates
- Unit deletion
- Linking units with billing records

This allows financial activity to remain associated with the correct property
throughout the system.

---

# ⚡ Electricity Billing

Electricity charges can be recorded against individual units.

The application supports:

- Electricity billing
- Previous meter reading retrieval
- Current billing records
- Penalty handling
- Payment status tracking
- Settlement processing
- Electricity billing ledger

Electricity charges participate in the accounting workflow rather than existing
only as isolated billing records.

---

# 🧾 Maintenance Billing

Recurring maintenance charges can be generated for managed units.

Supported functionality includes:

- Individual maintenance bills
- Bulk maintenance billing
- Penalty application
- Penalty waiver
- Payment tracking
- Partial settlement
- Maintenance ledger

Bulk billing allows a maintenance charge to be generated across registered
units for a selected billing period.

```text
Registered Units
      │
      ▼
Bulk Maintenance Charge
      │
      ▼
Individual Unit Bills
      │
      ▼
Accounts Receivable
```

---

# 💵 Custom Charges

The system supports additional charges outside electricity and standard
maintenance billing.

These can be used for property-specific charges that need to be associated
with an individual unit.

```text
Unit
 │
 ▼
Custom Charge
 │
 ▼
Accounts Receivable
 │
 ▼
Settlement
```

Custom charges are maintained in their own ledger while still participating
in the wider accounting system.

---

# ⏳ Penalties & Waivers

Outstanding bills can include penalties.

The application provides functionality for:

- Applying maintenance penalties
- Tracking penalty amounts
- Waiving eligible penalties
- Updating the corresponding financial records

Penalty waivers are reflected through accounting entries rather than simply
changing a number without financial context.

---

# 💳 Settlement Center

The settlement workflow handles payments against outstanding financial records.

Supported settlement types include:

```text
Electricity Bills
Maintenance Bills
Custom Charges
Building Expenses
Staff Salaries
```

The system validates settlements and records the corresponding accounting
activity.

---

## Partial Settlements

Payments do not always match the full outstanding amount.

T3 supports partial settlements by separating the remaining balance while
recording the amount that has actually been paid.

Conceptually:

```text
Outstanding Bill
      │
      ├──────────────┐
      ▼              ▼
Amount Paid     Remaining Balance
      │              │
      ▼              ▼
   Settled         Arrears
```

This preserves outstanding balances while accurately recording completed
payments.

---

# 🏦 Financial Accounting

A major component of T3 is its integrated accounting system.

Operational actions are connected with financial records using:

- Chart of Accounts
- Journal Vouchers
- Journal Lines
- Accounts Receivable
- Accounts Payable
- Cash / Bank accounts
- Revenue accounts
- Expense accounts

---

# 📚 Chart of Accounts

The system maintains a configurable **Chart of Accounts (COA)**.

Accounts can represent categories such as:

```text
Assets
Liabilities
Equity
Revenue
Expenses
```

System operations reference these accounts when generating financial entries.

This allows business operations and accounting records to remain connected.

---

# ⚖️ Double-Entry Accounting Engine

T3 includes a dedicated accounting engine responsible for posting journal
vouchers and maintaining account balances.

Before a voucher is accepted, the engine calculates:

```text
Total Debits
     =
Total Credits
```

If the values do not balance within the configured tolerance, the voucher is
rejected.

```text
Operational Transaction
          │
          ▼
    Journal Voucher
          │
          ▼
┌────────────────────────┐
│ Validate Debit = Credit│
└────────────┬───────────┘
             │
             ▼
      Journal Lines
             │
             ▼
    Chart of Accounts
             │
             ▼
    Updated Balances
```

Account balances are updated according to their accounting category.

For example:

```text
Assets & Expenses
Debit  → Increase
Credit → Decrease

Liabilities, Equity & Revenue
Credit → Increase
Debit  → Decrease
```

---

# 📖 Journal Vouchers

The system maintains journal vouchers containing one or more accounting lines.

Each line references an account and contains debit or credit information.

Voucher numbers are automatically generated using the voucher type, year, and
sequence.

Example:

```text
BR-2026-0001
BP-2026-0002
JV-2026-0003
```

Different voucher types allow financial events to be represented consistently
through the General Ledger.

---

# ↩️ Voucher Reversal

Instead of simply deleting an accounting transaction, the accounting engine
supports journal voucher reversal.

A reversal creates another voucher with the original debit and credit entries
swapped.

```text
Original Entry

Cash / Bank             DR  10,000
Accounts Receivable     CR  10,000


Reversal Entry

Accounts Receivable     DR  10,000
Cash / Bank             CR  10,000
```

The original voucher is marked as reversed, preserving the accounting trail.

---

# 🔒 Period Protection

The accounting engine contains protection against modifying locked financial
records.

When a journal voucher is marked as locked, posting or reversing it is
rejected.

This provides a foundation for protecting historical accounting periods.

---

# 💸 Building Expense Management

Operational building expenses can be recorded and tracked through the system.

Expense functionality includes:

- Expense categories
- Expense recording
- Outstanding expense tracking
- Accounts Payable integration
- Payment settlement
- Cash / bank account selection

Expense payments therefore participate in the same financial system as
customer billing.

---

# 👥 Employee Management

The system maintains employee records used by payroll operations.

Functionality includes:

- Employee registration
- Employee retrieval
- Employee deletion
- Fixed salary information
- Salary records

---

# 💼 Payroll

T3 includes payroll functionality for building staff.

Monthly salary accruals can be generated from registered employee salary
information.

```text
Employees
    │
    ▼
Monthly Payroll
    │
    ▼
Salary Accrual
    │
    ▼
Accounts Payable
    │
    ▼
Salary Settlement
    │
    ▼
Cash / Bank
```

The system also supports generating salary accruals for all registered
employees for a selected month.

---

# 📊 Financial Summary

The backend calculates summarized financial information from operational and
accounting data.

This provides management with a consolidated view of the building's financial
position rather than requiring information to be manually assembled from
individual billing records.

---

# 💾 Database Backup & Restore

T3 includes database backup and restoration functionality for MySQL.

The backend can invoke MySQL tools to:

```text
MySQL Database
      │
      ▼
  mysqldump
      │
      ▼
 SQL Backup
```

and:

```text
SQL Backup
    │
    ▼
MySQL Restore
    │
    ▼
Database
```

The Docker environment includes the required MySQL client tooling to support
these operations in a Linux container.

Database connection information is supplied through environment variables
rather than being committed to the repository.

---

# 🏗️ Architecture

```text
┌──────────────────────────────────────────────┐
│                Web Interface                 │
│             Thymeleaf / HTML                 │
└─────────────────────┬────────────────────────┘
                      │
                      ▼
┌──────────────────────────────────────────────┐
│                REST API                      │
│                                              │
│               T3Controller                   │
└─────────────────────┬────────────────────────┘
                      │
                      ▼
┌──────────────────────────────────────────────┐
│              Business Layer                  │
│                                              │
│   T3Services        AccountingEngine         │
└─────────────────────┬────────────────────────┘
                      │
                      ▼
┌──────────────────────────────────────────────┐
│            Spring Data JPA                   │
│                                              │
│        Repository Interfaces                 │
└─────────────────────┬────────────────────────┘
                      │
                      ▼
┌──────────────────────────────────────────────┐
│                  MySQL                       │
│                                              │
│       Operational + Financial Data           │
└──────────────────────────────────────────────┘
```

---

# 📁 Project Structure

```text
src/main/
│
├── java/com/nexus/t3_management/
│   │
│   ├── controllers/
│   │   └── T3Controller.java
│   │
│   ├── models/
│   │   ├── AppUser.java
│   │   ├── BuildingExpense.java
│   │   ├── ChartOfAccount.java
│   │   ├── CustomerCharge.java
│   │   ├── ElectricityBill.java
│   │   ├── Employee.java
│   │   ├── ExpenseCategory.java
│   │   ├── JournalLine.java
│   │   ├── JournalVoucher.java
│   │   ├── MaintenanceBill.java
│   │   ├── StaffSalary.java
│   │   └── Unit.java
│   │
│   ├── repositories/
│   │   ├── AppUserRepository.java
│   │   ├── BuildingExpenseRepository.java
│   │   ├── ChartOfAccountRepository.java
│   │   ├── CustomerChargeRepository.java
│   │   ├── ElectricityBillRepository.java
│   │   ├── EmployeeRepository.java
│   │   ├── ExpenseCategoryRepository.java
│   │   ├── JournalVoucherRepository.java
│   │   ├── MaintenanceBillRepository.java
│   │   ├── StaffSalaryRepository.java
│   │   └── UnitRepository.java
│   │
│   ├── services/
│   │   ├── AccountingEngine.java
│   │   └── T3Services.java
│   │
│   └── T3ManagementApplication.java
│
└── resources/
    │
    ├── templates/
    │   └── index.html
    │
    └── application.properties
```

---

# 🛠️ Technology Stack

| Area | Technology |
|---|---|
| Language | Java 21 |
| Framework | Spring Boot |
| Web Layer | Spring MVC / REST |
| Persistence | Spring Data JPA |
| Database | MySQL |
| Frontend | Thymeleaf / HTML |
| Containerization | Docker |
| Build Tool | Maven |
| Utilities | Lombok |

---

# 🔌 API Overview

The backend exposes REST endpoints covering the application's operational
modules.

Examples include:

```text
/api/auth/login

/api/users

/api/summary
/api/accounts
/api/coa
/api/jvs

/api/units

/api/bills/electricity
/api/bills/maintenance
/api/bills/maintenance/bulk
/api/bills/charge
/api/bills/waive

/api/expenses
/api/salaries
/api/payroll/pay-all

/api/settle

/api/employees
/api/categories

/api/ledgers/elec
/api/ledgers/maint
/api/ledgers/charges

/api/system/backup
/api/system/restore
```

---

# 🐳 Docker Support

The application includes a Dockerfile based on Java 21.

The container installs the MySQL client tooling required by the application's
database backup and restore functionality.

Build the image:

```bash
docker build -t t3-building-management .
```

Run it with the required database configuration supplied through environment
variables.

---

# ⚙️ Configuration

Database configuration is provided using environment variables:

```properties
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
```

The application also supports:

```properties
server.port=${PORT:8080}
```

No production database credentials should be committed to the repository.

---

# 🚀 Running Locally

## Prerequisites

```text
Java 21+
MySQL
```

The Maven Wrapper is included with the project.

---

## 1. Clone

```bash
git clone https://github.com/saahilkudia/t3-building-management.git
cd t3-building-management
```

---

## 2. Configure Database

Provide the required environment variables:

```text
DB_URL
DB_USERNAME
DB_PASSWORD
```

Example database URL:

```text
jdbc:mysql://localhost:3306/t3_management
```

---

## 3. Run

### Linux / macOS

```bash
./mvnw spring-boot:run
```

### Windows

```powershell
mvnw.cmd spring-boot:run
```

---

## 4. Build

### Linux / macOS

```bash
./mvnw clean package
```

### Windows

```powershell
mvnw.cmd clean package
```

---

# 📸 Screenshots

> Application screenshots will be added as the repository presentation is
> prepared.

Recommended views:

```text
Dashboard
Unit Management
Electricity Billing
Maintenance Billing
Settlement Center
General Ledger / Chart of Accounts
Journal Vouchers
Expenses
Payroll
```

---

# 🗺️ System Workflow

At a high level, T3 connects building operations to financial accounting:

```text
                    BUILDING OPERATIONS
                           │
        ┌──────────────────┼───────────────────┐
        │                  │                   │
        ▼                  ▼                   ▼
 Electricity          Maintenance        Custom Charges
    Billing              Billing
        │                  │                   │
        └──────────────────┼───────────────────┘
                           ▼
                 Accounts Receivable
                           │
                           ▼
                      Settlement
                           │
                           ▼
                      Cash / Bank


 Building Expenses                           Payroll
        │                                       │
        └──────────────────┬────────────────────┘
                           ▼
                  Accounts Payable
                           │
                           ▼
                      Settlement
                           │
                           ▼
                      Cash / Bank

                           │
                           ▼
                ┌────────────────────┐
                │ Accounting Engine  │
                └─────────┬──────────┘
                          ▼
                   Journal Vouchers
                          │
                          ▼
                  Chart of Accounts
                          │
                          ▼
                  Financial Summary
```

---

# 👨‍💻 Developer

**Muhammad Saahil Kudia**

Software Engineer focused on backend systems, business applications, financial
workflows, and automation.

[LinkedIn](https://www.linkedin.com/in/saahilkudia/) •
[GitHub](https://github.com/saahilkudia) •
[SyntaxLoops](https://syntaxloops.com)

---

<div align="center">

### Building operations connected directly to accounting.

`Java` • `Spring Boot` • `MySQL` • `Spring Data JPA` • `Docker`

</div>