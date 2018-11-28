- [SQL style guide by Simon Holywell](http://www.sqlstyle.guide/)
- [The annotated table of contents](http://use-the-index-luke.com/sql/table-of-contents)

Tables names:

- [sql - Table Naming Dilemma: Singular vs. Plural Names - Stack Overflow](https://stackoverflow.com/questions/338156/table-naming-dilemma-singular-vs-plural-names)

- [mysql - Native table 'performance_schema'.'???' has the wrong structure - Stack Overflow](https://stackoverflow.com/questions/6288103/native-table-performance-schema-has-the-wrong-structure)
- [mysql error: Table "mysql"."innodb_table_stats" not found - Stack Overflow](https://stackoverflow.com/questions/15767652/mysql-error-table-mysql-innodb-table-stats-not-found)
- [windows - Howto: Clean a mysql InnoDB storage engine? - Stack Overflow](https://stackoverflow.com/questions/3927690/howto-clean-a-mysql-innodb-storage-engine/4056261#4056261)

`BOOLEAN` is `TINYINT`. See [MySQL :: MySQL 5.7 Reference Manual :: 11.1.1 Numeric Type Overview](https://dev.mysql.com/doc/refman/5.7/en/numeric-type-overview.html#idm139980721318896)

> MySQL unique keys can be `NULL` whereas primary keys cannot be
> There can be only one Primary key in a table but one or more unique keys

- [sql - Best way to get identity of inserted row? - Stack Overflow](https://stackoverflow.com/questions/42648/best-way-to-get-identity-of-inserted-row)

Actions when a table is modified:

- [MySQL :: MySQL 5.7 Reference Manual :: 23.3 Using Triggers](https://dev.mysql.com/doc/refman/5.7/en/triggers.html)

## Race condition

Aka concurrency

Use single atomic statement (like `INNER JOIN`) or transaction

- [How to INSERT If Row Does Not Exist (UPSERT) in MySQL](https://chartio.com/resources/tutorials/how-to-insert-if-row-does-not-exist-upsert-in-mysql/)
- [sql - Insert into a MySQL table or update if exists - Stack Overflow](https://stackoverflow.com/questions/4205181/insert-into-a-mysql-table-or-update-if-exists)
- [MySQL :: MySQL 5.7 Reference Manual :: 13.2.5.2 INSERT ... ON DUPLICATE KEY UPDATE Syntax](https://dev.mysql.com/doc/refman/5.7/en/insert-on-duplicate.html)
- [MySQL insert on duplicate update for non-PRIMARY key - Stack Overflow](https://stackoverflow.com/questions/33495194/mysql-insert-on-duplicate-update-for-non-primary-key)

## Game Leaderboard

For performances, you can create temporary/virtual table [`CREATE TEMPORARY TABLE IF NOT EXISTS table2 AS (SELECT * FROM table1)`](https://stackoverflow.com/questions/5859391/create-a-temporary-table-in-a-select-statement-without-a-separate-create-table). It's unique per session (this is not supported by non CGI PHP). Else use a regular table. See also [views](http://dev.mysql.com/doc/refman/5.7/en/create-view.html)

	-- insert game
	INSERT INTO games (time, player, ip, email, mobile, over_reason, round, beginning, score)
	VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?);
	-- get rank
	SELECT (SELECT 1 + COUNT(*) FROM games WHERE round = ? AND score > ?) as rank;
	-- get top 10
	SELECT player, score FROM games
	WHERE round = ?
	ORDER BY score DESC
	LIMIT 10;

1. game end timestamp
2. player's ID
3. player's ip (see [Get client IP](Web#Get client IP))
4. player's email
5. player's mobile
6. game over reason
7. game's round
8. game beginning timestamp
9. game score
10. game's round
11. game's score
12. game's round

leaderboards are read-heavy. Favor memory to store fields used to compute rank

- [mysql - Get the rank of a user in a score table - Database Administrators Stack Exchange](http://dba.stackexchange.com/questions/13703/get-the-rank-of-a-user-in-a-score-table)
- [design - Efficient SQL Query/Schema for a Leader Board - Stack Overflow](https://stackoverflow.com/questions/575785/efficient-sql-query-schema-for-a-leader-board)
- [Leaderboard design using SQL Server - Stack Overflow](https://stackoverflow.com/questions/19921878/leaderboard-design-using-sql-server)

## Row number

- [How can I get row's index from a table in SQL Server? - Stack Overflow](https://stackoverflow.com/questions/19807037/how-can-i-get-rows-index-from-a-table-in-sql-server)
- [sql - ROW_NUMBER() in MySQL - Stack Overflow](https://stackoverflow.com/questions/1895110/row-number-in-mysql)
- [MySQL - Generating Row Number for Each Row Using Variable - SQL Authority with Pinal Dave](https://blog.sqlauthority.com/2014/03/08/mysql-generating-row-number-for-each-row-using-variable/)

## Insert new lines

	INSERT INTO test VALUES(replace('a\nb\nc\nd\ne', '\n', char(10)));

Insert in multiple tables, use **transaction** to rollbak in case of error (conflict, database connection lost, etc.)

	BEGIN;
	INSERT INTO users (username, password)
	  VALUES('test', 'test');
	INSERT INTO profiles (userid, bio, homepage) 
	  VALUES(LAST_INSERT_ID(),'Hello world!', 'http://www.stackoverflow.com');
	COMMIT;

- [MySQL Insert into multiple tables? (Database normalization?) - Stack Overflow](https://stackoverflow.com/questions/5178697/mysql-insert-into-multiple-tables-database-normalization)
 
	INSERT INTO table_listnames (name, address, tele)
	SELECT * FROM (SELECT 'Rupert', 'Somewhere', '022') AS tmp
	WHERE NOT EXISTS (
	    SELECT name FROM table_listnames WHERE name = 'Rupert'
	) LIMIT 1;

- [MySQL: Insert record if not exist in table - Stack Overflow](https://stackoverflow.com/questions/3164505/mysql-insert-record-if-not-exists-in-table)
 
	INSERT INTO table (id, name, age) VALUES(1, "A", 19) ON DUPLICATE KEY UPDATE name="A", age=19

- [MySQL :: MySQL 5.7 Reference Manual :: 13.2.5.2 INSERT ... ON DUPLICATE KEY UPDATE Syntax](https://dev.mysql.com/doc/refman/5.7/en/insert-on-duplicate.html)
- [sql - Insert into a MySQL table or update if exist - Stack Overflow](https://stackoverflow.com/questions/4205181/insert-into-a-mysql-table-or-update-if-exists)

Import file:

- [sql - Import large CSV file in mysql by disable/enable constraint and indexe - Stack Overflow](https://stackoverflow.com/questions/8486082/import-large-csv-file-in-mysql-by-disable-enable-constraints-and-indexes)

## Column size

- bcrypt hash: `BINARY(60)`
	- [mysql - What column type/length should I use for storing a Bcrypt hashed password in a Database? - Stack Overflow](https://stackoverflow.com/questions/5881169/what-column-type-length-should-i-use-for-storing-a-bcrypt-hashed-password-in-a-d)
- Facebook user ID (numeric string): `VARCHAR(128)`
	- [What's the max. length of a Facebook uid? - Stack Overflow](https://stackoverflow.com/questions/7566672/whats-the-max-length-of-a-facebook-uid)
- IPV6 and IPV4: `VARCHAR(50)` (canonical format: as text) or `VARBINARY(16)` (binary, supported with functions by MySQL 5.6)
	- [ip - Maximum length of the textual representation of an IPv6 address? - Stack Overflow](https://stackoverflow.com/questions/166132/maximum-length-of-the-textual-representation-of-an-ipv6-address)
	- [IPv6 address - Wikipedia](https://en.wikipedia.org/wiki/IPv6_address)
	- [MySQL :: MySQL 5.6 Reference Manual :: 12.19 Miscellaneous Functions](https://dev.mysql.com/doc/refman/5.6/en/miscellaneous-functions.html#function_inet6-aton)
	- [php - Store IPv6 in database - Stack Overflow](https://stackoverflow.com/questions/2049681/store-ipv6-in-database/4423041#4423041)
- sex (ISO/IEC 5218): `TINYINT`
	- 0 = Not Known
	- 1 = Male
	- 2 = Female
	- 9 = Not applicable

## Variables

	SET @myvar = 10

	SELECT @myvar := 10

	UPDATE mytable SET col = @tmp := col, col = 10

- [sql - MySql How to set a local variable in an update statement (Syntax?) - Stack Overflow](https://stackoverflow.com/questions/8475311/mysql-how-to-set-a-local-variable-in-an-update-statement-syntax)
- [sql - How to declare a variable in MySQL? - Stack Overflow](https://stackoverflow.com/questions/11754781/how-to-declare-a-variable-in-mysql)
- [sql server - How to set variable from a SQL query? - Stack Overflow](https://stackoverflow.com/questions/3974683/how-to-set-variable-from-a-sql-query)
- [MySQL :: MySQL 5.7 Reference Manual :: 1.8.2.1 SELECT INTO TABLE Differences](https://dev.mysql.com/doc/refman/5.7/en/ansi-diff-select-into-table.html) (MySQL: "You can use [SELECT ... INTO](https://dev.mysql.com/doc/refman/5.7/en/select-into.html) with user-defined variables")

## Prepare statement

Aka SQL injection protection, supported natively by the server.

Doesn't support column name nor value. For latest, user variable can be used (eg. `SET @var1 = 1, @var2 = 2`), see also [stored procedure - Set variable with dynamic name in trigger (MySQL) - Database Administrator Stack Exchange](https://dba.stackexchange.com/questions/126970/set-variable-with-dynamic-name-in-trigger-mysql)
Often doesn't support multiple statements (prepare individualy), or use procedure

- [java - Dynamic column name using prepared statement + sql query with variable containing ' - Stack Overflow](https://stackoverflow.com/questions/43957497/dynamic-column-name-using-prepared-statement-sql-query-with-variable-containin/43958236#43958236)

## Optimisation

Indexes:

> A clustered index is like the contents of a phone book. You can open the book at 'Hilditch, David' and find all the information for all of the 'Hilditch's right next to each other. Here the keys for the clustered index are (lastname, firstname).

- [indexing - What is an index in SQL? - Stack Overflow](https://stackoverflow.com/questions/2955459/what-is-an-index-in-sql)

Redundant data vs join tables (foreign keys):

- [php - Is it better to store redundant information or join tables when necessary in MySQL? - Stack Overflow](https://stackoverflow.com/questions/3237033/is-it-better-to-store-redundant-information-or-join-tables-when-necessary-in-mys)
- [Schema types: Data retrieval performance versus redundant storage](https://www2.microstrategy.com/producthelp/10.6/ProjectDesignGuide/WebHelp/Lang_1033/Content/ProjectDesign/Schema_types__Data_retrieval_performance_versus_re.htm)

Insert lot of rows:

- compine multiple records to one `INSERT` instead of one record per `INSERT`
- [How can mysql insert millions records faster? - Stack Overflow](https://stackoverflow.com/questions/19682414/how-can-mysql-insert-millions-records-faster)
- [MySQL :: MySQL 5.6 Reference Manual :: 8.2.4.1 Optimizing INSERT Statements](https://dev.mysql.com/doc/refman/5.6/en/insert-optimization.html)
- `mysqlimport --local database data.txt` import tab-delimited text files or use `mysqlimport --local --fields-optionally-enclosed-by='"' --fields-terminated-by=, --lines-terminated-by='\r\n' database data.csv` for CSV (add `--ignore-lines=1` to skip a header row). Note: use value `0` for auto increment fields.
- [MySQL :: MySQL 5.6 Reference Manual :: 13.2.6 LOAD DATA INFILE Syntax](https://dev.mysql.com/doc/refman/5.6/en/load-data.html)
- [MySQL :: MySQL 5.6 Reference Manual :: 4.5.5 mysqlimport — A Data Import Program](https://dev.mysql.com/doc/refman/5.6/en/mysqlimport.html)
- [How to import CSV file to MySQL table - Stack Overflow](https://stackoverflow.com/questions/3635166/how-to-import-csv-file-to-mysql-table)
 
	./mysqltuner.pl --user root --pass root --defaults-file .../my.cnf --mysqladmin .../mysqladmin --mysqlcmd .../mysql

	./mysqltuner.pl --user root --pass root --defaults-file /Applications/MAMP/conf/my.cnf --mysqladmin /Applications/MAMP/Library/bin/mysqladmin --mysqlcmd /Applications/MAMP/Library/bin/mysql

### Compress data

Use `COMPRESS()` in `VARBINARY` or `BLOB`: 4-byte length + zlib data (zlib header + deflate data)

- [MySQL :: MySQL 5.5 Reference Manual :: 12.13 Encryption and Compression Functions](https://dev.mysql.com/doc/refman/5.5/en//encryption-functions.html#function_compress)

## Errors

Transaction : commit or rollback

Use `SQLSTATE` codes in your client, it's more standardized.

- [MySQL :: MySQL 5.7 Reference Manual :: B.3 Server Error Code and Messages](https://dev.mysql.com/doc/refman/5.7/en/error-messages-server.html)

## Clear a table

	TRUNCATE TABLE table;
	# kick, internaly delete and recreate the table

	DELETE FROM table;
	# delete each rows, but doesn't reset auto increment

Truncate a table with referenced fields as foreign keys

	DELETE FROM table;
	-- will execute cascades
	ALTER TABLE table AUTO_INCREMENT = 1;

- [mysql - How to truncate a foreign key constrained table? - Stack Overflow](https://stackoverflow.com/questions/5452760/how-to-truncate-a-foreign-key-constrained-table)

## String comparison

Aka like

	-- select URL contains url encoded space
	SELECT 'http://example/David%20and%20Goliath' LIKE '\%20'

- [MySQL :: MySQL 5.7 Reference Manual :: 12.5.1 String Comparison Functions](https://dev.mysql.com/doc/refman/5.7/en/string-comparison-functions.html)
- [mysql - Wildcard in Java PreparedStatement - Stack Overflow](https://stackoverflow.com/questions/327765/wildcards-in-java-preparedstatements)
- [java - Using "like" wildcard in prepared statement - Stack Overflow](https://stackoverflow.com/questions/8247970/using-like-wildcard-in-prepared-statement/8248052#8248052)

## Row match vs affected

- match the `WHERE` clause
- affected row inserted, deleted, changed

- [MySQL :: MySQL 5.7 Reference Manual :: 27.8.7.1 mysql_affected_rows()](https://dev.mysql.com/doc/refman/5.7/en/mysql-affected-rows.html)
- [mysql/Readme.md at master · mysqljs/mysql](https://github.com/mysqljs/mysql/blob/master/Readme.md#getting-the-number-of-changed-rows) - Node.js MySQL client`changedRows` vs `affectedRows`

## Time

- `CAST(date AS DATETIME)`
- [MySQL :: MySQL 5.5 Reference Manual :: 12.7 Date and Time Functions](https://dev.mysql.com/doc/refman/5.5/en/date-and-time-functions.html#function_timestampdiff) - `TIMESTAMPDIFF(MONTH,'2003-02-01','2003-05-01')`
- [php - Should I use the datetime or timestamp data type in MySQL? - Stack Overflow](https://stackoverflow.com/questions/409286/should-i-use-the-datetime-or-timestamp-data-type-in-mysql)

## Enum

`FIND_IN_SET` and `ENUM`

If number of values in set change, the col size will be recomputed

Or:

`status` can contains one or more (bits flags):

1 = Prospective Customer
2 = Cancelled Service
4 = Pool Service
8 = lawn mowing
16 = window washing
32 = tree trimming
64 = house painting
128 = mobile oil change

All of window washing customers even if they are cancelled:

	SELECT * FROM customers WHERE (status & 16) AND !(status & 2)

All of tree trimming AND pool service customers i.e. 32+4:

	SELECT * FROM customers WHERE status & 36

- [MySQL :: MySQL 8.0 Reference Manual :: 12.12 Bit Function and Operators](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#c10542)

## Concatenate list as string

	SET SESSION group_concat_max_len = 1000000;#max 1MB
	SELECT GROUP_CONCAT(k SEPARATOR ',') FROM (SELECT CONCAT(col1, ':', col2) AS k FROM sometable WHERE condition) AS tmp

- [sql - Can I concatenate multiple MySQL row into one field? - Stack Overflow](https://stackoverflow.com/questions/276927/can-i-concatenate-multiple-mysql-rows-into-one-field)