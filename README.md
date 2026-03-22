Library Management System Project
This is a group project by Team D of SQL Study Group for a Library Management System.

Overview
The Library Management System is a SQL-based project that simulates how libraries manage their collections, members, and lending operations within a relational database. The Library database consists of three relational tables representing books, members, and loans.

The goal of the project is to design a structured database schema and use SQL queries to retrieve, filter, and analyse library-related data.

This project focuses entirely on SQL and relational database design, demonstrating core data management and querying skills used in real library information systems.

Problem Statement
Libraries need structured systems to manage their collections and lending activities efficiently. Without a well-designed database, it becomes difficult to track book inventory, monitor borrowed items, manage member information, or generate library reports.

This project addresses that problem by designing a relational Library Management System database that allows librarians to:

Store book and member information
Track loan history
Monitor available copies
Review borrowing patterns
Generate library insights through SQL queries

Tools Used
Database: MySQL

Editor: MySQL Workbench

Data Source: Manual data insertion

Data Source
The raw data used for this project can be found in the data folder.

The database consists of the following tables:

BOOKS - Stores information about each book in the library.
Fields: book_id, title, author, isbn, category, publication_year, copies_available

MEMBERS - Stores library member details.
Fields: member_id, first_name, last_name, email, phone, membership_date

LOANS - Tracks book borrowing and returns.
Fields: loan_id, book_id, member_id, borrow_date, due_date, return_date

Database Schema & ER Design
https://images/library-eer-diagram.png

Methods
Step 1: Database Design

Created the project database and initialised the workspace.

Step 2: Table Creation/Design

Designed and created tables using SQL CREATE TABLE statements with appropriate constraints and relationships. Tables created include: Books, Members, Loans

Step 3: Data Exploration

Queries were used to retrieve and filter book and member information and understand the dataset.

Step 4: Data Filtering

Query using comparison and logical operators to simulate how librarians identify borrowing patterns, available books, and member activity.

Step 5: Data Organisation

Track popular books, member join dates, and generate paginated lists.

Findings
3a. View all books

sql
SELECT * 
FROM books;
There are 6 books in the library.
![3a](images/3a.png)

3b. Show all registered members

sql
SELECT member_id, first_name, last_name
FROM members;
There are 5 registered members.
![3b](images/3b.png)

3c. Find all loans made on a specific date

sql
SELECT loan_id, book_id, member_id
FROM loans
WHERE borrow_date = '2026-03-07';
There were 2 loans on 2026-03-07.
![3c](images/3c.png)

3d. Display all books with more than 3 available copies

sql
SELECT book_id, title, author, copies_available
FROM books
WHERE copies_available > 3;
There are 3 books with more than 3 copies available.
![3d](images/3d.png)

4a. Books published after 2015

sql
SELECT book_id, title, author, publication_year
FROM books
WHERE publication_year > 2015;
There is 1 book published after 2015 (iron Cap, 2017). Note: Clean Code (2008) is before 2015.
![4a](images/4a.png)

4b. Members who joined before 2022

sql
SELECT member_id, first_name, last_name, membership_date
FROM members
WHERE membership_date < '2022-01-01';
All 5 members joined before 2022 (all in 2021).
![4b](images/4b.png)

4c. Books that are either Fiction or Mystery

sql
SELECT book_id, title, author, category
FROM books
WHERE category = 'Fiction'
	OR category = 'Mystery';
There are 2 Fiction books. No Mystery books in the collection.
![4c](images/4c.png)

4d. Loans that have not been returned

sql
SELECT loan_id, book_id, member_id, borrow_date, due_date, return_date
FROM loans
WHERE return_date IS NULL;
There are 3 active loans not yet returned.
![4d](images/4d.png)

4e. Members who joined after 2020 and have borrowed books (bonus)

sql
SELECT member_id, first_name, last_name
FROM members
WHERE membership_date > '2020';
All 5 members joined after 2020 and have borrowing history.
![4d](images/4e.png)

5a. Sort all books alphabetically by title

sql
SELECT book_id, title, author, category, publication_year
FROM books
ORDER BY title ASC;
![5a](images/5a.png)

5b. List distinct book categories

sql
SELECT DISTINCT category
FROM books;
There are 5 unique categories: Business, Languages, Environmental, Fiction, Programming.
![5b](images/5b.png)

5c. Get top 5 most recent members

sql
SELECT member_id, first_name, last_name, membership_date
FROM members
ORDER BY membership_date DESC
LIMIT 5;
All 5 members are shown as most recent (all joined in 2021).
![5c](images/5c.png)

5d. Skip the first 5 books and display the next 5

sql
SELECT *
FROM books
ORDER BY title ASC
LIMIT 5 OFFSET 5;
The 6th book (To Kill a Mockingbird) is displayed.
![5d](images/5d.png)

5e. Show the 10 most recent loans not yet returned

sql
SELECT *
FROM loans
WHERE return_date IS NULL
ORDER BY borrow_date ASC
LIMIT 10;
There are 3 unreturned loans (less than 10, so all are shown).
![5e](images/5e.png)

