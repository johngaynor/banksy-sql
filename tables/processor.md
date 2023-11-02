# Processor Tables

This file describes the tables for the processor app.

---

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
| first_name  | varchar(55) | status name      |

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

## PROCESSOR_FILTERS

User filters for generating summary data.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| filter_id\* | int | unique filter id |
| user_id | int | associated user (FK to USERS) |
| filter_name | varchar(55) | filter_name |

---

## PROCESSOR_FILTERS_CATEGORIES

Categories associated with each user filter.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| filter_id\* | int | associated filter (FK to PROCESSOR_FILTERS) |
| category_name\* | varchar(55) | category name |
| aggregate | boolean | whether or not the category is an aggregate of other categories |

---

## PROCESSOR_FILTERS_CATEGORIES_AGGREGATES

Aggregate categories (if they exist) for groupings in filters.
| Field | Datatype | Description |
| ----------- | ----------- | ----------------------------------------- |
| filter_id\* | int | associated filter (FK to PROCESSOR_FILTERS) |
| category_name\* | varchar(55) | category name |
| aggregate_name\* | varchar(55) | category to be aggregated into filter's category |
