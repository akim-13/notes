---
tags: programming, CS, cm12004
links: "[[Databases]]"
---
# SQL
- **SQL** (Structured Query Language) is a programming language designed for managing data held in relational DBMSs.
- **ERD** (Entity-Relation Diagram) — *see the W8 worksheet, important!*
- Some **data types** include:

    | Data Type  |                              Description                                             | Example                  |
    |:------------:|:--------------------------------------------------------------------------------------:|:--------------------------:|
    | `FLOAT`      | A floating-point number                                                              | 123.456                  |
    | `INT`        | An integer                                                                           | 123                      |
    | `INTEGER`    | Synonym for INT                                                                      | 456                      |
    | `REAL`       | A double-precision floating-point number                                             | 123.456789               |
    | `BOOLEAN`    | A Boolean value stored as 0 (false) or 1 (true)                                      | 1 (true), 0 (false)      |
    | `DATETIME`   | Represents date and time                                                             | '2023-01-01 12:00:00'    |
    | `TEXT`       | A text string                                                                        | 'Hello, World!'          |
    | `VARCHAR(x)` | A variable-length string (maximum length x)                                          | 'Hello' (`VARCHAR(10)`)    |
    | `CHAR(x)`    | A fixed-length string (padded with spaces to length x if shorter)                    | 'Hi' (`CHAR(10)`)          |

-  A **key** is used to uniquely identify each row (record) in a DB table.
- The basic **types of keys** include:
    - **Primary key** — uniquely identifies each row in a table.
    - **Foreign key** — a column or a set of columns in one table that refers to the primary key in another table. It establishes a link between two tables, creating a parent-child relationship where the foreign key field in the child table points to the primary key in the parent table. It is commonly denoted with an asterisks **(*)** in the design tables.
    - **Composite key** — a special type of primary key that consists of two or more columns in a table to uniquely identify each row.
        ```sql
        CREATE TABLE journey (
        origin VARCHAR(25),
        destination VARCHAR(25),
        driverID INT,
        locomotiveID INT,
        departure DATETIME,
        FOREGIN KEY (driverID) REFERENCES Drivers (id),
        FOREGIN KEY (locomotiveID) REFERENCES Locomotive (id),
        PRIMARY KEY(origin, destination, departure)
        );
        ```
        Journey table:

        | Origin   | Destination | Driver ID* | Locomotive ID* | Departure Datetime  |
        |:----------:|:-------------:|:-----------:|:---------------:|:---------------------:|
        | Exeter   | Plymouth    | 1         | 93948         | 01/01/2023 11:00    |
        | Plymouth | Exeter      | 2         | 93822         | 01/01/2023 11:00    |
        | Bristol  | Plymouth    | 6         | 00293         | 01/01/2023 11:00    |
        | Exeter   | Plymouth    | 1         | 93948         | 03/01/2023 08:00    |
        | Exeter   | Plymouth    | 2         | 92830         | 02/01/2023 11:00    |
        | ...      | ...         | ...       | ...           | ...                 |

        ![[Attachments/Pasted image 20231126205223.png]]
    - **Compound key** is a type of composite key, which includes at least one foreign key.
        ```sql
        CREATE TABLE booking (
        hotel_id INT,
        cust_id INT,
        arrival_date DATETIME,
        nights INT,
        FOREIGN KEY hotel_id REFERENCES hotel (id),
        FOREGIN KEY cust_id REFERENCES customer (id),
        PRIMARY KEY(hotel_id, cust_id, arrival_date)
        );
        ```

        Booking table: 

        | Hotel ID | Customer ID | Arrival Date       | Nights |
        |:----------:|:-------------:|:--------------------:|:--------:|
        | 82763    | 1002        | 10/01/2023 15:00   | 3      |
        | 82763    | 1012        | 10/01/2023 15:00   | 2      |
        | 82763    | 1002        | 15/01/2023 16:00   | 2      |
        | ...      | ...         | ...                | ...    |

        ![[Attachments/Pasted image 20231126210225.png]]

- The following is an example of how to create and manipulate a DB using `sqlite3` library in python:
    ```python
    import sqlite3
    
    # Create a new SQLite database
    conn = sqlite3.connect('example.db')
    cursor = conn.cursor()
    
    # Create tables
    cursor.execute('''
    CREATE TABLE authors (
        id INTEGER,
        name TEXT NOT NULL,
        birth_year INTEGER,
        PRIMARY KEY (id)
    )''')
    
    cursor.execute('''
    CREATE TABLE books (
        id INTEGER PRIMARY KEY,
        title TEXT NOT NULL,
        publication_year INTEGER,
        author_id INTEGER,
        FOREIGN KEY (author_id) REFERENCES authors (id)
    )''')
    
    # Insert data into the tables
    cursor.execute("INSERT INTO authors (name, birth_year) VALUES ('George Orwell', 1903)")
    cursor.execute("INSERT INTO authors (name, birth_year) VALUES ('Aldous Huxley', 1894)")
    cursor.execute("INSERT INTO books (title, publication_year, author_id) VALUES ('1984', 1949, 1)")
    cursor.execute("INSERT INTO books (title, publication_year, author_id) VALUES ('Brave New World', 1932, 2)")
    
    # Save (commit) the changes
    conn.commit()

    # Modify the table structure (e.g., adding a column)
    cursor.execute("ALTER TABLE authors ADD COLUMN nationality TEXT")
    
    # Renaming a table
    cursor.execute("ALTER TABLE authors RENAME TO writers")
    
    # Removing a table
    cursor.execute("DROP TABLE IF EXISTS unwanted_table")
    
    # Renaming a column (SQLite doesn't support renaming columns directly)
    # Step 1: Create a new table with the desired column names
    cursor.execute('''
    CREATE TABLE temp_authors (
        author_id INTEGER PRIMARY KEY,
        author_name TEXT NOT NULL,
        birth_year INTEGER,
        nationality TEXT
    )''')
    
    # Step 2: Copy data from the old table to the new table
    cursor.execute('''
    INSERT INTO temp_authors (author_id, author_name, birth_year, nationality)
    SELECT id, name, birth_year, nationality FROM writers
    ''')
    
    # Step 3: Drop the old table
    cursor.execute("DROP TABLE writers")
    
    # Step 4: Rename the new table to the original name
    cursor.execute("ALTER TABLE temp_authors RENAME TO writers")
    
    # Retyping a column (similar steps as renaming a column)
    # Create a new table with the desired column types and copy data over
    
    # Query and display data
    cursor.execute("SELECT * FROM writers")
    print(cursor.fetchall())
    
    # Add data to the new column
    cursor.execute("UPDATE writers SET nationality = 'British' WHERE author_id = 1")
    cursor.execute("UPDATE writers SET nationality = 'British' WHERE author_id = 2")
    
    # Close the connection
    conn.close()
    ```
