# Banksy SQL

This is the documentation for the sql portion of Banksy. This is meant to be used as a reference for building Banksy apps and understanding the data structure (there's not much to work with in Vercel's Postgres UI).

# Processor Tables

## USERS

User data.

| Field          | Datatype     | Description                             |
| -------------- | ------------ | --------------------------------------- |
| user_id\*      | int          | unique user id                          |
| first_name     | varchar(55)  | user first name                         |
| last_name      | varchar(55)  | user last name                          |
| email          | varchar(55)  | user email                              |
| password       | varchar(255) | user password                           |
| account_status | int          | account status (FK to ACCOUNT_STATUSES) |
| date_created   | date         | when the account was created            |

---

## USER_STATUSES

Account statuses.

| Field       | Datatype    | Description      |
| ----------- | ----------- | ---------------- |
| status_id\* | int         | unique status id |
| status_name | varchar(55) | status name      |

---

## PROCESSOR_BANKS

User banks.

| Field        | Datatype  | Description                   |
| ------------ | --------- | ----------------------------- |
| bank_id\*    | int       | unique bank id                |
| user_id      | int       | associated user (FK to USERS) |
| bank_name    | int       | name of bank                  |
| last_updated | timestamp | last updated timestamp        |

---

## PROCESSOR_BANKS_HEADERS

Headers for user bank CSV structure (used to standardize processing structure).

| Field       | Datatype    | Description                               |
| ----------- | ----------- | ----------------------------------------- |
| bank_id\*   | int         | unique bank id                            |
| user_id\*   | int         | associated user (FK to USERS)             |
| date        | varchar(55) | bank csv name associated with date        |
| description | varchar(55) | bank csv name associated with description |
| amount      | varchar(55) | bank csv name associated with amount      |

---

## PROCESSOR_CATEGORIES

Categories used for processing CSVs. user_id = 0 for default categories.
| Field | Datatype | Description |
| -------------- | ----------- | -------------|
| category_id\* | int | unique category id |
| user_id\* | int | associated user (FK to USERS) |
| category_name | varchar(55) | category name |
| description | varchar(55) | category description |

---

## PROCESSOR_KEYWORDS

Keywords used to process transactions into categories automatically.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| category_id\* | int | associated category (FK to PROCESSOR_CATEGORIES) |
| keyword\* | varchar(55) | keyword name |

---

## PROCESSOR_VIEWS

User views for generating summary data.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| view_id\* | int | unique view id |
| user_id | int | associated user (FK to USERS) |
| view_name | varchar(55) | view name |

---

## PROCESSOR_VIEWS_CATEGORIES

Categories associated with each user view.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| view_id\* | int | associated view (FK to PROCESSOR_VIEWS) |
| category_name\* | varchar(55) | category name |
| aggregate | boolean | whether or not the category is an aggregate of other categories |

---

## PROCESSOR_VIEWS_CATEGORIES_AGGREGATES

Aggregate categories (if they exist) for groupings in views.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| view_id\* | int | associated view (FK to PROCESSOR_VIEWS) |
| category_name\* | varchar(55) | category name |
| aggregate_name\* | varchar(55) | category to be aggregated into filter's category |

---

## PROCESSOR_HISTORY

History table for summaries generated by processor.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| user_id | int | associated user (FK to USERS) |
| month_year | string | month & year of transaction |
| income | float | summary income |
| spending | float | summary spending |
| savings | float | summary savings |

## PROCESSOR_HISTORY_CATEGORIES

Specific categories for each processed summary.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| history_id\* | int | unique history id |
| category_id\* | int | associated category (FK to PROCESSOR_CATEGORIES) |
| amount | float | category amount for that summary |
