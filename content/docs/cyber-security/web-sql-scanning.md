---
title: "1.6. Web & SQL Scanning"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.6. Web & SQL Scanning

## Automatic Web Scanners

Automatic web scanners are used to determine vulnerabilities in web servers.

They find **uncommon headers**, **server versions**, and **potentially significant URLs**.

An example of a web scanner is [Nikto](https://github.com/sullo/nikto).

## SQL

Structured Query Language is the language database servers respond to to process database queries.

Database servers manage (in order of hierarchy) Databases, Tables, Records, and Fields.

Common SQL commands:

- `SELECT`: Retrieves data from a database table
- `CREATE`: Creates a new table
- `DROP`: Deletes a table and it's contents
- `INSERT`: Inserts a record into a table
- `DELETE`: Deletes a record from the table
- **Comments**: `#`, `--` and `/* */`

### SQL Injection

Consider the following query to authenticate a user: `SELECT * FROM users WHERE user=$id AND password=$password`

If the ID was `username--` the query would become `SELECT * FROM users WHERE user=username-- AND password=`. Since `--` is a comment, anything after that would essentially be ignored, meaning the password is irrelevant.

This is known as SQL Injection.

[Sqlmap](https://sqlmap.org/) is a tool used to automatically perform SQL injection and database takeover.

#### Mitigating SQL Injection

Websites can take steps to mitigate the dangers of SQL injection. These include:

- **Sanitizing inputs** so SQL comment symbols are not allowed. **Prepared statements** can be used for this.
- **Escaping all user supplied input**

## NoSQL

MongoDB relies on Javascript as a query language instead of SQL.

This has the benefit that SQL injection cannot be performed on the database, however, many NoSQL implementations are not as advanced as SQL.
