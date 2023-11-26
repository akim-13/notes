---
tags:
  - cm12004
  - CS
links:
---
# Databases (DBs)
- **Data** are raw, unsummarized, unanylyzed facts or figures.
- **Database (DB)** is an organized collection of interrelated data.
- **Database Management System (DBMS)** — software that manages and controls access to the DB, providing a systematic way to create, retrieve, update, and manage data within the DB (e.g MySQL).
    - The **advantages** of using a DBMS, rather than writing programs to access DBs directly, include:
        - **Data independence** — applications are not exposed to data representation or storage details.
        - **Efficient data access** — does not rely on good programmers.
        - **Data integrity and security** — enforces integrity constraints.
        - **Data administration** — single point of administration.
        - Concurrent access
        - Crash recovery
        - Reduced application development time

- There are different **types of DBs**:
    - **Flat file** stores data in a single plain text file (e.g. CSV or Excel sheet). However, file based systems (systems with many flat files) have many disadvantages:
        - **Data integrity** — no protection against invalid entries.
        - **Data redundancy and inconsistency** — duplication of information.
        - **Data isolation** — different locations. 
        - **Atomicity** — two users cannot update the DB at once and failure leaves files in an inconsistent state.
        - **Security** — needs bespoke security in each application.
    - **Relational DBs** — a shared collection of logically related data and its descriptions. It contains *entities* (e.g. people, places, things) and *relationships* (associations between the entities).

# Unsorted
