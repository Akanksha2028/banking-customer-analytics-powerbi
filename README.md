# Banking Data Integration & Analytics

## Project Overview

This project demonstrates an end-to-end banking data integration and analytics workflow.

The project focuses on data profiling, data quality assessment, ETL-based data cleaning,
metadata management, source-to-target mapping, data lineage, target data modeling,
and validation of analytics-ready data.

## Business Problem

Banking data is distributed across multiple source tables such as customers, accounts,
transactions, branches, loans, and reference tables.

Before this data can be used for analytics and reporting, it needs to be profiled,
validated, cleaned, transformed, mapped, documented, and validated after ETL processing.

## Objectives

- Profile raw banking datasets
- Identify data quality issues
- Perform completeness, uniqueness, validity, consistency, and referential integrity checks
- Document data quality findings
- Apply ETL cleaning and transformation rules
- Create metadata documentation
- Create source-to-target mapping
- Document data lineage
- Design a target dimensional model
- Create dimension and fact tables
- Perform final validation and reconciliation

## Tools & Technologies

- Python
- Pandas
- Jupyter Notebook
- SQL
- Microsoft Excel
- Power BI
- CSV

## Source Datasets

- Customers
- Customer Types
- Addresses
- Accounts
- Account Types
- Account Statuses
- Branches
- Loans
- Loan Statuses
- Transactions
- Transaction Types

## ETL Workflow

```text
Raw Data
    |
    v
Data Profiling
    |
    v
Data Quality Assessment
    |
    v
DQ Findings
    |
    v
ETL Cleaning & Transformation
    |
    v
Cleaned Data
    |
    v
Metadata / Source-to-Target Mapping / Data Lineage
    |
    v
Target Data Model
    |
    v
Dimension + Fact Tables
    |
    v
Final Validation
    |
    v
ETL Reconciliation
```

## Data Quality Assessment

The following checks were performed:

### Completeness

Missing values were identified in account, customer, address, loan, and transaction data.

### Uniqueness

Duplicate identifiers and duplicate transaction records were identified.

The transaction dataset contained 500 exact duplicate rows.

### Referential Integrity

The following relationships were validated:

- Transaction -> Origin Account
- Transaction -> Destination Account
- Transaction -> Transaction Type
- Transaction -> Branch
- Account -> Customer

All tested referential integrity checks passed.

### Validity

Transaction amounts were checked for negative and zero values.

Result:

- Negative Amounts: 0
- Zero Amounts: 0

### Consistency

Loan dates were checked to ensure that the estimated end date is not before the start date.

One invalid loan date-order record was identified and flagged for review.

## ETL Transformations

### Transaction Data

Raw transaction rows: 50,000

Exact duplicate rows removed: 500

Cleaned transaction rows: 49,500

### Missing Transaction Dates

Missing transaction dates were not artificially populated.
They were flagged as 'Missing - Review Required'.

### Future Transaction Dates

Future-dated transactions were retained and flagged for business review.

### Customer and Address Data

Missing customer and address attributes were preserved and marked with data-quality status fields.

### Loan Dates

Invalid loan date ordering was flagged for business review.

## Metadata Management

Metadata was documented using Python and Pandas.

The metadata documentation contains source table, source column, data type, nullability, and row count information.

File:

`Documentation/Data_Metadata.xlsx`

## Source-to-Target Mapping

A source-to-target mapping was created to document how source columns map to target tables.

The mapping includes source table, source column, target table, target column, transformation rules, and data quality rules.

File:

`Documentation/Source_to_Target_Mapping.xlsx`

## Data Lineage

The project documents the movement of data from source to target:

```text
Raw CSV Files
      |
      v
Data Quality & ETL Processing
      |
      v
Cleaned Data
      |
      v
Target Dimension / Fact Tables
      |
      v
Analytics
```

File:

`Documentation/Data_Lineage.xlsx`

## Target Data Model

The target model separates descriptive entities into dimension tables and transactional data into a fact table.

### Dimension Tables

- dim_customer
- dim_customer_type
- dim_account
- dim_account_type
- dim_account_status
- dim_address
- dim_branch
- dim_loan
- dim_loan_status
- dim_transaction_type

### Fact Table

- fact_transaction

File:

`Documentation/Target_Data_Model.xlsx`

## Target Data Validation

Final fact transaction table:

- Total Rows: 49,500
- Duplicate Rows: 0
- Unique Transaction IDs: 49,500
- Missing Transaction IDs: 0
- Negative Amounts: 0
- Zero Amounts: 0
- Invalid Origin Account References: 0
- Invalid Destination Account References: 0
- Invalid Transaction Type References: 0
- Invalid Branch References: 0

## ETL Reconciliation

```text
Raw Transactions       : 50,000
Records Removed        : 500
Cleaned Transactions   : 49,500
Target Transactions    : 49,500
Reconciliation Status  : PASS
```

File:

`Documentation/ETL_Reconciliation.xlsx`

## Data Virtualization, Data Mesh & Data-as-a-Product

These concepts are included as design considerations relevant to modern data integration environments.

### Data Virtualization

Data virtualization can provide a logical access layer over distributed banking data without requiring every consumer to physically copy source data.

### Data Mesh

The project can be extended toward a data mesh approach by treating Customers, Accounts, Loans, and Transactions as governed business data domains.

### Data-as-a-Product

The documented datasets can be treated as reusable data products with defined schemas, metadata, quality rules, and lineage.

These are documented as concepts and design considerations, not as production implementations.

## Project Structure

```text
Banking_Data_Integration_Analytics/
|
+-- Raw_Data/
|
+-- Cleaned_Data/
|
+-- Target_Data/
|
+-- Documentation/
|   +-- Data_Metadata.xlsx
|   +-- Data_Quality_Findings.xlsx
|   +-- Source_to_Target_Mapping.xlsx
|   +-- Data_Lineage.xlsx
|   +-- Target_Data_Model.xlsx
|   +-- ETL_Reconciliation.xlsx
|
+-- Jupyter_Notebook/
|
+-- README.md
```

## Key Learning Outcomes

- Data profiling using Python and Pandas
- Data quality assessment
- ETL data cleaning
- Duplicate detection and removal
- Missing-value handling through status flags
- Referential integrity validation
- Metadata management
- Source-to-target mapping
- Data lineage documentation
- Dimensional data modeling
- Fact and dimension table creation
- ETL reconciliation and validation
- Understanding of Data Virtualization and Data Mesh concepts
