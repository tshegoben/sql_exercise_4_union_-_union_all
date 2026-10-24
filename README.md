# sql_exercise_4_union_-_union_all# BrightLearn SQL Exercise 4: `UNION` and `UNION ALL`

## Overview

This exercise practises combining rows from two query results using SQL
`UNION` and `UNION ALL`. The scenario uses a fictional African retail
bank, **NexBank**.

-   **Level:** Beginner
-   **Questions:** 10 SQL questions + 3 written bonus questions
-   **Tables:** 20 tables arranged into 10 pairs
-   **Practice environment:** Databricks SQL or another SQL environment
    that supports `UNION` and `UNION ALL`

## Learning objectives

By completing this exercise, I will practise how to:

-   Combine results from two `SELECT` statements.
-   Choose between `UNION` and `UNION ALL` based on whether duplicate
    rows should be removed or retained.
-   Align columns in the same order and use compatible data types.
-   Use aliases in the first `SELECT` to name the final output columns.
-   Validate query results against expected column names and row counts.

## Key concepts

### `UNION`

`UNION` combines the results of two `SELECT` statements and removes
duplicate **rows** from the combined result.

``` sql
SELECT column1, column2
FROM table_a

UNION

SELECT column1, column2
FROM table_b;
```

Use it when the task asks for a unique combined list.

### `UNION ALL`

`UNION ALL` combines the results of two `SELECT` statements and keeps
all rows, including duplicates.

``` sql
SELECT column1, column2
FROM table_a

UNION ALL

SELECT column1, column2
FROM table_b;
```

Use it when every record must be retained, such as for transaction logs,
ledgers, or volume reconciliation.

### Rules to remember

1.  Both `SELECT` statements must return the **same number of columns**.
2.  Columns in corresponding positions must have **compatible data
    types**.
3.  The columns must be in the **same logical order** in both queries.
4.  The final output column names are taken from the **first `SELECT`**.
    Use aliases there when the required output names differ from the
    source names.
5.  `UNION` removes duplicate rows based on the **entire selected row**,
    not just one column. If an extra column differs (for example, a
    branch label), otherwise similar records may no longer count as
    duplicates.
6.  A task's expected output columns may require aliases or derived
    values. Check the assignment carefully and make both sides of the
    union return the same column structure.

## Questions and table pairs

### Part 1 --- Questions 1--5: `UNION`

For these questions, return a unique combined result. Duplicate rows
should be removed.

  ------------------------------------------------------------------------------------------------
  Question          First table                   Second table                 Task focus
  ----------------- ----------------------------- ---------------------------- -------------------
  Q1                `branch_sandton_accounts`     `branch_rosebank_accounts`   Create a unique
                                                                               list of account
                                                                               holders across both
                                                                               branches. Expected
                                                                               columns:
                                                                               `account_id`,
                                                                               `account_holder`,
                                                                               `city`.

  Q2                `savings_products`            `current_products`           Create a unique
                                                                               catalogue of
                                                                               products offered by
                                                                               the bank. Expected
                                                                               columns:
                                                                               `product_code`,
                                                                               `product_name`,
                                                                               `product_type`.

  Q3                `retail_banking_staff`        `corporate_banking_staff`    Return each staff
                                                                               member once, even
                                                                               if assigned to both
                                                                               departments.
                                                                               Expected columns:
                                                                               `staff_id`,
                                                                               `staff_name`,
                                                                               `email`.

  Q4                `mobile_branch_cities`        `digital_branch_cities`      Create a unique
                                                                               list of cities
                                                                               served. Expected
                                                                               columns:
                                                                               `city_code`,
                                                                               `city_name`,
                                                                               `region`.

  Q5                `push_notification_targets`   `inapp_banner_targets`       Create a unique
                                                                               list of customers
                                                                               targeted by either
                                                                               campaign. Expected
                                                                               columns:
                                                                               `customer_id`,
                                                                               `customer_name`,
                                                                               `segment`.
  ------------------------------------------------------------------------------------------------

### Part 2 --- Questions 6--10: `UNION ALL`

For these questions, keep every row from both tables, including
duplicates.

  --------------------------------------------------------------------------------------------------------
  Question          First table                   Second table                       Task focus
  ----------------- ----------------------------- ---------------------------------- ---------------------
  Q6                `atm01_transactions`          `atm02_transactions`               Combine all ATM
                                                                                     transaction records.
                                                                                     Expected columns:
                                                                                     `transaction_id`,
                                                                                     `account_id`,
                                                                                     `amount`,
                                                                                     `transaction_date`.

  Q7                `gauteng_loan_applications`   `western_cape_loan_applications`   Combine all loan
                                                                                     applications from
                                                                                     both regions.
                                                                                     Expected columns:
                                                                                     `application_id`,
                                                                                     `customer_id`,
                                                                                     `loan_type`,
                                                                                     `amount_requested`.

  Q8                `email_complaints`            `app_complaints`                   Combine every
                                                                                     complaint received
                                                                                     through email or the
                                                                                     mobile app. Expected
                                                                                     columns:
                                                                                     `complaint_id`,
                                                                                     `customer_id`,
                                                                                     `category`,
                                                                                     `logged_date`.

  Q9                `april_payments`              `may_payments`                     Combine all payment
                                                                                     records for
                                                                                     reconciliation.
                                                                                     Expected columns:
                                                                                     `payment_id`,
                                                                                     `account_id`,
                                                                                     `amount`,
                                                                                     `payment_date`.

  Q10               `debit_entries`               `credit_entries`                   Combine all debit and
                                                                                     credit entries into
                                                                                     one general ledger.
                                                                                     Expected columns:
                                                                                     `entry_id`,
                                                                                     `account_id`,
                                                                                     `entry_type`,
                                                                                     `amount`,
                                                                                     `entry_date`.
  --------------------------------------------------------------------------------------------------------

> **Important:** The expected output columns listed in the exercise do
> not always match the source table columns exactly. Where necessary,
> use aliases, constants, or suitable values to produce the requested
> output structure. Do not add a column to only one side of a `UNION`;
> both sides must return the same number of compatible columns in the
> same order.

## Bonus questions

Answer these in full sentences; no SQL is required.

1.  A fraud analyst needs a unique list of customers who appeared on
    either the January or February high-risk watch lists. Which operator
    should be used, and why?
2.  An audit team needs to count every individual transaction in Q1,
    including transactions recorded in two systems on the same day.
    Which operator should be used, and why?
3.  A query tries to combine a two-column `SELECT` with a three-column
    `SELECT`. Explain why it fails and how to fix it.

## Suggested workflow

1.  Open the relevant tables in Databricks and inspect their column
    names and data types.
2.  Read the task and decide whether it requires unique rows (`UNION`)
    or every row (`UNION ALL`).
3.  Write the first `SELECT`, including aliases or derived values
    required for the expected output.
4.  Write the second `SELECT` with the same number of columns, in the
    same order, and with compatible data types.
5.  Run the query and inspect the results.
6.  Compare the result column names and order with the assignment's
    expected columns.
7.  Check for duplicates and row counts:
    -   For `UNION`, verify that duplicate complete rows have been
        removed.
    -   For `UNION ALL`, verify that the output contains all rows from
        both inputs.
8.  Label each query `-- Q1` through `-- Q10` in one `.sql` file.
9.  Complete the three bonus questions.

## Self-check checklist

-   [ ] All 10 SQL queries run without errors.
-   [ ] Q1--Q5 use `UNION`.
-   [ ] Q6--Q10 use `UNION ALL`.
-   [ ] Both sides of each union have the same number of columns.
-   [ ] Corresponding columns have compatible data types and matching
    positions.
-   [ ] Aliases in the first `SELECT` produce the required final column
    names.
-   [ ] Q1--Q5 remove duplicate complete rows.
-   [ ] Q6--Q10 retain every row.
-   [ ] Result columns match the assignment's expected names and order.
-   [ ] The three bonus questions are answered with explanations.

## Suggested submission structure

``` text
sql-union-exercise/
├── README.md
├── union_exercise.sql
└── results/
    ├── Q1-result.png
    ├── Q2-result.png
    └── ...
```

The `results/` folder is optional; screenshots or text output can be
used to document query results. Record the SQL environment and version
at the top of the SQL file.

## Main takeaway

Both operators combine rows from multiple `SELECT` statements. The key
decision is whether duplicates should be removed or preserved:

-   **`UNION`** --- combines results and removes duplicate complete
    rows.
-   **`UNION ALL`** --- combines results and retains every row.

Choose the operator based on the task's requirements, then verify the
output structure and row count.
