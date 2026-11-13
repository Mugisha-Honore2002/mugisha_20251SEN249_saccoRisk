# SACCO Micro-Loan Repayment and Arrears Early-Warning Monitor

**Student:** Mugisha Honore  
**Student ID:** 20251SEN249  
**Course:** INSY 8311 – Database Development with PL/SQL  
**Instructor:** Eric Maniraguha  
**Institution:** Adventist University of Central Africa (AUCA), Faculty of Information Technology  
**Academic year:** 2026–2027, Semester I  
**Repository:** `honore_20251SEN249_saccoRisk`

---

## 1. Problem Statement

Savings and Credit Cooperatives (SACCOs) are a main source of small loans for farmers, traders and households in Rwanda who are not served by commercial banks. Many SACCOs still record loans, instalments and guarantors in notebooks or spreadsheets. As a result:

- late payments are discovered only after a loan is already seriously overdue;
- loan officers cannot easily see which members are drifting into arrears;
- new loans can be approved for members who already have unpaid balances.

These weaknesses raise the portfolio-at-risk (PAR) and threaten the savings of every member. A database is needed that records each loan and repayment accurately, scores repayment risk, warns officers early, and enforces lending rules inside the database so they cannot be bypassed.

## 2. Proposed Solution

An Oracle PL/SQL database that stores members, loan products, applications, loans, guarantors, repayment schedules and repayments. PL/SQL code applies each payment to the oldest unpaid instalment, scores each member's repayment risk, classifies overdue loans into 30/60/90-day PAR buckets and raises alerts. Triggers block loans to members in arrears and record every change to repayment data in an audit log.

## 3. Objectives

**Main objective**

Design and implement an Oracle PL/SQL database that monitors SACCO loan repayments and warns loan officers early about members at risk of default.

**Specific objectives**

1. Model the loan lifecycle (application → approval → schedule → repayment) in a 3NF schema.
2. Load a real microfinance dataset into the schema and validate it.
3. Automate repayment posting, risk scoring and arrears classification with PL/SQL procedures, functions, cursors and packages.
4. Enforce lending rules and keep an audit trail using triggers and a restriction rule.
5. Give loan officers an interactive Oracle APEX interface that calls the PL/SQL logic.

## 4. Data Source

| Item | Detail |
|------|--------|
| Dataset | Data Science for Good: Kiva Crowdfunding |
| Link | https://www.kaggle.com/kiva/data-science-for-good-kiva-crowdfunding |
| Main file | `kiva_loans.csv` (about 671,000 loans, 20 columns) |
| Content | Loan amount, funded amount, term, repayment interval, sector, country, borrower gender |
| Licence | **To confirm on the Kaggle page (educational use)** |
| Privacy | Anonymised. Member identifiers will be replaced by generated codes. |

The dataset has no individual payment records, so instalment dates and payments will be derived with PL/SQL and documented in `docs/` and `data/`. The data will be cleaned and loaded with SQL*Loader and PL/SQL routines.

## 5. Planned Tables (3NF)

| Table | Purpose |
|-------|---------|
| `BRANCH` | SACCO branches |
| `MEMBER` | Anonymised members |
| `LOAN_PRODUCT` | Loan types, rates and limits |
| `LOAN_APPLICATION` | Loan requests and decisions |
| `LOAN` | Approved and disbursed loans |
| `GUARANTOR` | Members guaranteeing a loan |
| `REPAYMENT_SCHEDULE` | Instalments due |
| `REPAYMENT` | Payments received |
| `RISK_ASSESSMENT` | Member risk scores and bands |
| `ARREARS_ALERT` | Early warnings by PAR bucket |
| `AUDIT_LOG` | History of changes to key tables |

## 6. Planned PL/SQL Features

| Feature | Name | Where it is used |
|---------|------|------------------|
| Package | `PKG_SACCO_LOANS` | Groups loan approval, repayment and alert logic |
| Procedure | `PRC_RECORD_REPAYMENT` | Applies a payment to the oldest unpaid instalment |
| Procedure | `PRC_APPROVE_LOAN` | Checks product limits and guarantor cover, then creates the loan and its schedule |
| Function | `FNC_CALC_RISK_SCORE` | Returns a 0–100 risk score from payment history, loan size and guarantor cover |
| Cursor | Overdue-instalment cursor | Loops over late instalments to compute days overdue and insert PAR alerts |
| Cursor | Arrears report cursor | Produces the monthly arrears report |
| Trigger | `TRG_BLOCK_LOAN_IN_ARREARS` | Blocks a new loan for a member with unresolved arrears |
| Trigger | `TRG_AUDIT_REPAYMENT` | Writes old and new values of repayment changes to `AUDIT_LOG` |
| Exceptions | Custom exceptions | Handle overpayment, missing members, duplicate payments and closed loans |

## 7. Innovation

- **Category:** User interface (Option 2)
- **Tool:** Oracle APEX connected to the Oracle database
- **What it does:** A loan officer searches for a member, records a repayment through a form that calls `PRC_RECORD_REPAYMENT`, and views live arrears alerts and risk scores.
- **Rule:** Business rules stay in PL/SQL. APEX only displays and submits data.
- Documentation, run instructions and screenshots will be added to the `innovation/` folder.

## 8. Repository Structure

```
honore_20251SEN249_saccoRisk/
├── README.md
├── docs/
│   ├── research/       
│   ├── proposal/        
│   └── presentation/  
├── data/               
├── (later phases)      
```

## 9. Project Phases

| Phase | Focus | Status |
|-------|-------|--------|
| 0 | Research, data source, proposal | In progress |
| I | Business process modeling | Planned |
| II | Data sourcing and normalization | Planned |
| III | Pluggable database (PDB) creation | Planned |
| IV | Tables and data loading | Planned |
| V | PL/SQL development | Planned |
| VI | Advanced programming and auditing | Planned |
| VII | Documentation, innovation, final presentation | Planned |

## 10. References (APA)

- Access to Finance Rwanda. (2020). *FinScope Rwanda 2020: Consumer survey report*. https://microdata.statistics.gov.rw/index.php/catalog/89/download/832
- Apache Software Foundation. (n.d.). *Apache Fineract* [Computer software]. https://fineract.apache.org/
- Kasina, M. M., Kihoro, J. M., & Kibet, A. (2025). Performance of different machine learning algorithms for credit risk classification. *Journal of Data Analysis and Information Processing, 13*(4). https://doi.org/10.4236/jdaip.2025.134029
- Kiva. (n.d.). *Data science for good: Kiva crowdfunding* [Data set]. Kaggle. https://www.kaggle.com/kiva/data-science-for-good-kiva-crowdfunding
- Koffi, C. H. A., Djeundje, V. B., & Menoukeu Pamen, O. (2024). *Quantifying socio-temporal effects of loan delinquency drivers in microfinance* [Preprint]. arXiv. https://arxiv.org/abs/2410.13100
- Oracle Corporation. (2025). *Oracle Database PL/SQL language reference, 19c* (E96448-08). https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls


## Phase I – Business Process Modeling

**Selected process:** Loan application to repayment and arrears alert in a SACCO (replace with your own words).

**Modeling tool:** draw.io (diagrams.net)

**Published diagram link:** [paste your link here]

**Supporting explanation:** [docs/business_process/business_process_explanation.pdf](docs/business_process/business_process_explanation.pdf)