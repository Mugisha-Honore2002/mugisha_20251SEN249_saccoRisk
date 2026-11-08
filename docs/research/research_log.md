# Research Log

**Project:** SACCO Micro-Loan Repayment and Arrears Early-Warning Monitor  
**Student:** Mugisha Honore (20251SEN249)  
**Course:** INSY 8311 – Database Development with PL/SQL

| # | Source (APA) | Type | Link | Key finding | Gap it shows |
|---|--------------|------|------|-------------|--------------|
| 1 | Koffi, C. H. A., Djeundje, V. B., & Menoukeu Pamen, O. (2024). *Quantifying socio-temporal effects of loan delinquency drivers in microfinance* [Preprint]. arXiv. | Research paper | https://arxiv.org/abs/2410.13100 | Models borrower repayment as moving between states (current, delinquent, default, recovery) and combines interpretable risk models with machine learning. | A statistical study, not an operational system. It does not show how arrears states are tracked and flagged inside a database. |
| 2 | Kasina, M. M., Kihoro, J. M., & Kibet, A. (2025). Performance of different machine learning algorithms for credit risk classification. *Journal of Data Analysis and Information Processing, 13*(4). | Research paper | https://doi.org/10.4236/jdaip.2025.134029 | Supervised machine learning (such as random forest, XGBoost, logistic regression) was tested to improve credit risk scoring for microfinance institutions in Machakos County, Kenya. | Focuses on prediction accuracy only. It does not cover recording repayments, enforcing lending rules or alerting loan officers. |
| 3 | Access to Finance Rwanda. (2020). *FinScope Rwanda 2020: Consumer survey report*. | Report / statistic | https://microdata.statistics.gov.rw/index.php/catalog/89/download/832 | Formal financial inclusion in Rwanda rose from 42% of adults in 2016 to 67% in 2020, with SACCOs among the formal providers. | A national demand-side survey. It gives context but no loan-level repayment monitoring for individual SACCOs. |
| 4 | Apache Software Foundation. (n.d.). *Apache Fineract* [Computer software]. | Existing system | https://fineract.apache.org/ | An open-source core banking platform used by microfinance institutions and SACCOs, with loan products, repayment tracking and portfolio management. | A general-purpose backend (APIs only, no built-in interface) that a small SACCO must host and customise. It is not a lightweight, rule-based design inside an Oracle PL/SQL database. |
| 5 | Kiva. (n.d.). *Data science for good: Kiva crowdfunding* [Data set]. Kaggle. | Dataset | https://www.kaggle.com/kiva/data-science-for-good-kiva-crowdfunding | `kiva_loans.csv` holds 671,205 real microfinance loans with amount, term, repayment interval, sector and country. | Has no individual payment records, so instalments and payments must be generated and documented. |
| 6 | Oracle Corporation. (2025). *Oracle Database PL/SQL language reference, 19c* (E96448-08). | Technical source | https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls | Describes the PL/SQL features used in this project: packages, procedures, functions, cursors, triggers and exception handling. | Not a domain source. It defines the language features, and the SACCO design is my own application of them. |

## Reading checklist

The brief counts any reference you have not read as plagiarism. Tick each box only after you have read the source, and correct the "Key finding" and "Gap" cells to match what you actually found.

- [ ] 1. Koffi et al. (2024): read the abstract, introduction and conclusion
- [ ] 2. Kasina et al. (2025): read the abstract, methods and results
- [ ] 3. FinScope Rwanda 2020: read the SACCO and credit sections, confirm the 42% and 67% figures
- [ ] 4. Apache Fineract: read the overview and loan features, confirm the "gap" claim
- [ ] 5. Kiva dataset: open the Kaggle page, check the columns and the licence for educational use
- [ ] 6. Oracle PL/SQL reference: read the chapters on triggers, packages and cursors

## Notes

- Sources 1 and 2 are the two research papers. Koffi et al. is a preprint, so it may not be peer-reviewed.
- Add more sources here as you find them, since the minimum is 6 but more is better.
