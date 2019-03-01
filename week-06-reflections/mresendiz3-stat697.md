# Questions about Problems and Recipes

[Chapter 5, Problem 1]
* Question (mresendiz3-stat697): How do you create a new table whilst copying the column structure of an existing table?
* Answer (mresendiz3-stat697): The CREATE TABLE that includes a LIKE clause copies the column names and characteristics from an existing table into a new table where data and rows are not inserted. 

[Chapter 5, Problem 2]
* Question (mresendiz3-stat697): How do you create a table that contains information specified from a particular query?
* Answer (mresendiz3-stat697): The CREATE TABLE works with the AS keyword and the specified query clauses that creates a table and loads the results of the query into the new table. You can use the WHERE clause to specify particular rows from the original dataset. 


[Chapter 5, Problem 5]
* Question (mresendiz3-stat697): How does the DELETE statement  work?
* Answer (mresendiz3-stat697): The DELETE statement deletes rows from the table that are specified in the WHERE clause. If there isn't a WHERE clause specified all the rows are deleted where the DROP TABLE statement deletes an entire table. 

[Chapter 5, Problem 6]
* Question (mresendiz3-stat697): How do you update rows from a table using the UPDATE statement? 
* Answer (mresendiz3-stat697): The UPDATE statement that includes the SET clause is used to modify rows in a table. Using WHEN-THEN clauses in the CASE expression enables you to update a column value based on particular criteria. 

[Chapter 5, Problem 7]
* Question (mresendiz3-stat697): What does the INSERT statement do?
* Answer (mresendiz3-stat697): The INSERT statement is used to insert new rows into an existing or into a new table. 


[Chapter 5, Problem 8]
* Question (mresendiz3-stat697): What does the ALTER TABLE statement do?
* Answer (mresendiz3-stat697): It is used to modify the specifications of an existing column when paired with the MODIFY clause, it can add a new column definition(s) when paired with the ADD clause, and can delete existing columns when paried with the DROP clause. 


[Chapter 5, Problem 9]
* Question (mresendiz3-stat697): What does the DESCRIBE TABLE statement do?
* Answer (mresendiz3-stat697): It lists the column attributes and structure for a particular table.

[Chapter 5, Problem 10]
* Question (mresendiz3-stat697): How do you create an empty table while creating column specifications?
* Answer (mresendiz3-stat697): The CREATE TABLE statement can do this by using a set of parentheses to enclose the entire group of column specifications that must list each columns name, the data type, and if there are character columns the length must be specified. The different columns are separated by commas and when specifying the length an integer is used. Example: (FullName char(25), Age num)


[Chapter 8, Problem 1]
* Question (mresendiz3-stat697): Where are PROC SQL options specified?
* Answer (mresendiz3-stat697): They are specified in the PROC SQL statement after you specify an option and will remain in effect until you change it or you re-invoke PROC SQL. 


[Chapter 8, Problem 2]
* Question (mresendiz3-stat697): What SQL option restricts the number of rows that PROC SQL can take in as input from any single source?
* Answer (mresendiz3-stat697): The INOBS= option restricts the number of rows and is similar to the OBS= option in SAS. However, the OUTOBS= option restricts the number of rows that PROC SQL displays or writes to a table. 


[Chapter 8, Problem 5]
* Question (mresendiz3-stat697): What are some details about the STIMER option in PROC SQL?
* Answer (mresendiz3-stat697): It specifies whether PROC SQL writes timing information for each statement to the SAS log; instead of a cumulative value for the entire procedure. NOSTIMER is the default. The SAS system option STIMER must be in effect in order for the STIMER option in PROC SQL to take place. If you only use the system option you will get the timing information for the entire procedure. 


[Chapter 8, Problem 6]
* Question (mresendiz3-stat697): What does a Dictionary table have?
* Answer (mresendiz3-stat697): A Dictionary table is a read-only dada view that has information about SAS data libraries, data sets, macros, and external files that are being used or available in the current SAS session. It also has the settings for the SAS system options that are currently in effect. 


[Chapter 8, Problem 7]
* Question (mresendiz3-stat697): What are some details about a Dictionary table?
* Answer (mresendiz3-stat697): They are created each time they're referenced in a SAS program. They are read-only and updated automatically. 


[Chapter 8, Problem 8]
* Question (mresendiz3-stat697): How can Dictionary tables be accessed?
* Answer (mresendiz3-stat697): They can be accessed by running a PROC SQL query against the table using the Dictionary libref. You can also access a Dictionary table by referring to the PROC SQL view of the table that is stored in the Sashelp library. For example: 

proc sql;                
      describe table dictionary.titles;


[sas_recipe-obtain-column-information Week 6 SAS Recipe]
* Question (mresendiz3-stat697): Why is it preferred to copy and paste a list of column names within a PROC SQL query?
* Answer (mresendiz3-stat697): When the column names list increases in size it is possible that the amount of errors that are made when transcribing the column names also increase. Thus, to mitigate the errors it's good practice to copy and paste. 

[sas_recipe-ddl-and-dml-sql-queries Week 6 SAS Recipe]
* Question (mresendiz3-stat697): Why does SAS only supports character and numeric columns?
* Answer (mresendiz3-stat697): Only supporting these two types of data minimizes the space that our file takes up as memory on a disk. 

***



# Recipes Exploration Results

```
*******************************************************************************;
**************** 80-character banner for column width reference ***************;
* set window width to banner width to calibrate line length to 80 characters  *;
*******************************************************************************;

*******************************************************************************;
* obtain-column-information ;
*******************************************************************************;
/*
Scenario: We wish to obtain a full list of columns in a table.

Approachs:
(1) Point-and-click using SAS Explorer, with copy/paste into Excel for editing
(2) Use proc contents
(3) Use proc sql to access dictionary tables
*/

/*
Recipe for Approach 1:

- Open the SAS Explorer
- Click "Toggle Details" icon in menu bar
- Navigate to dataset
- Right-click on Dataset and Select "View Columns"
- Right-click in columns table, and Select "Copy"
- Paste into an empty Excel spreadsheet
- Use Excel's "Text to Columns" command with comma delimiter
*/

*Example For Approach 1;

proc sql;
	select
		 Species
		,SepalWidth
		,SepalLength
		,PetalWidth
		,PetalLength
	from 
		sashelp.iris
	;
quit;



/*
Recipe for Approach 2:
- Use the following SAS code to output information to the Results Viewer:
proc contents order=varnum data=<dataset>;
run;
- Highlight and copy the table of column information
- Paste into an empty Excel spreadsheet
*/

*Example For Approach 2;

proc contents order=varnum data=sashelp.iris;
run;

proc sql;
	select
		 Species
		,SepalLength
		,SepalWidth
		,PetalLength
		,PetalWidth
	from 
		sashelp.iris
	;
quit;



/*
Recipe for Approach 2:
- Use the following SAS code to output information to the Results Viewer:
proc sql;
    select
        name
    from
        dictionary.columns
    where
        lowcase(libname) = '<library>'
    and
        lowcase(memname) = '<dataset>'
    ;
quit;
*/

*Example For Approach 3;

proc sql;
	select
		name
	from
		dictionary.columns
	where 
		lowcase(libname) = 'sashelp'
		and
		lowcase(memname) = 'iris'
	;
quit;

proc sql;
	select
		 Species 
		,SepalLength 
		,SepalWidth 
		,PetalLength 
		,PetalWidth 
	from
		sashelp.iris
	;
quit;









*******************************************************************************;
**************** 80-character banner for column width reference ***************;
* set window width to banner width to calibrate line length to 80 characters  *;
*******************************************************************************;

*******************************************************************************;
* ddl-and-dml-sql-queries ;
*******************************************************************************;
/*
Scenario: We wish to perform a data-definition-language (DDL) task, such as
defining, obtaining, or modifying column information for a table; or we wish to
perform a data-manipulation-language (DML) task, such as obtaining, creating,
or modifying the rows of data in a table.

Approach: Use DDL and DML SQL queries.


DDL Recipes:

proc sql;
    * define column information for a table;
    create table <table name> as
    (
         <column1-name> <column1-type>
        ,<column2-name> <column2-type>
        ,...
    );

    * obtain column information for a table;
    describe table <table name>

    * add new column information for a table;
    alter table <table name>
        add
             <new-column1-name> <new-column1-type>
            ,<new-column2-name> <new-column2-type>
            ,...
    ;

    * modify column information for a table;
    alter table <table name>
        modify
             <existing-column1-name> <existing-column1-type>
            ,<existing-column2-name> <existing-column2-type>
            ,...
    ;

    * delete column information for a table;
    alter table <table name>
        drop
             <existing-column1-name>
            ,<existing-column2-name>
            ,...
    ;

    * delete entire table;
    drop table <table name>;
quit;


DML Recipes:

proc sql;
    * obtain rows of data from a table;
    select
        <comma-separated list of columns, of * for all columns>
    from
        <table name>
    <where clause: optional>
    <group-by clause: optional>
    <having clause: optional>
    <order-by clause: optional>
    ;

    * create rows of data in a table using a select query;
    insert into <table name>
        <select query>
    ;

    * create rows of data in a table using value statement, giving tuples of
    values for all columns without specifying column names;
    insert into <table name>
        values(<value-for-column1>, <value-for-column2>, ...)
        values(<value-for-column1>, <value-for-column2>, ...)
        ...
    ;

    * create rows of data in a table using value statement, giving tuples of
    values for specified columns, with values in all other columns set to
    missing for the new rows being created;
    insert into <table name>
        (<column1-name>, <column2-name>, ...)
        values(<value-for-column1>, <value-for-column2>, ...)
        values(<value-for-column1>, <value-for-column2>, ...)
        ...
    ;

    * create rows of data in a table using set statement, giving all columns
    names and their values explicitly;
    insert into <table name>
        set
             <column1-name> = <value1>
            ,<column1-name> = <value1>
            ,...
    ;

    * update rows of data in a table;
    update <table name>
        set
             <column1-name> = <value1>
            ,<column1-name> = <value1>
            ,...
        <where clause: optional>
    ;

    * delete rows of data in a table;
    delete from <table name>
        <where clause: optional>
    ;
quit;

*/


*Examples;

* DDL example: define column information;

proc sql;
	create table Work.tmp
	(
		 column1 char(42)
		,column2 num
	);
quit;


* DDL example: obtain column information;

proc sql;
	describe table Work.tmp;
quit;


* DDL example: add column;

proc sql;
	alter table Work.tmp
		add column3 char(54)
	;
quit;


* DDL example: modify column;

proc sql;
	alter table Work.tmp
		modify column1 char(54)
	;
quit;


* DDL example: delete column;

proc sql;
	alter table Work.tmp
		drop column2
	;
quit;


* DDL example: delete table;

proc sql;
	drop talbe Work.tmp;
quit;

* DML example setup: define column information;

proc sql;
	create table Work.iris
		like sashelp.iris
	;
quit;


* DML example: obtain rows of data;

proc sql;
	select * from Work.iris;
quit; 


* DML example: create rows of data from select query;

proc sql;
	insert into Work.iris
		select * from sashelp.iris
	;
quit;


* DML example: create row of data using values statement for all columns;

proc sql;
	insert into Work.iris
		values('Big Flower', 75, 80, 85, 90)
	;
quit;


* DML example: create row of data using values statement for select columns;

proc sql;
	insert into Work.iris
		(Species, SepalLength)
		values('Big Flower', 75)
	;
quit;


* DML example: update rows of data;

proc sql;
	update Work.iris
		set Species = 'Big Flower'
		where
			SepalLength > 64
	;
quit;


* DML example: delete rows of data;

proc sql;
	delete from Work.iris 
		where Species = 'Big Flower'
	;
quit;


/*
Notes:
(1) These examples illustrate the eight main queries available in proc sql,
along with their possible variations. These are also the 8 main queries defined
in most SQL-based relational database management systems (RDBMSes).
(2) The first four queries (create-table, describe-table, alter-table, and
drop-table) are used as so-called data-definition language (DDL), meaning they
define, obtain, or modify column information in a table, or delete a table
entirely.
(3) The output of a describe-table query is sometimes called the "DDL for the
table" since it's what would be put into a create-table query to create a new
table with the same column properties but no rows of data.
(4) However, note that when specifying the column type in a create-table query,
SAS only supports character columns and numeric columns, even through most
RDBMSes allow for many other possible column types in order to allow the size
of data on disk to be minimized as much as possible (e.g., a list for MySQL is
available at https://dev.mysql.com/doc/refman/8.0/en/data-types.html). This is
because Base SAS only supports character and numeric types; e.g., even date and
time values are really just numeric values with formatting applied to them.
(5) On the other hand, the last four queries (select, insert-into, update, and
delete-from) are used as so-called data-manipulation language (DML), meaning
they obtain, create, modify, or delete the rows of data in a table.
(6) Together, these eight queries are the basic toolkit for database
administration, and it's not uncommon for database-maintenance records to be
given as a sequence of queries since the code itself specifies exact steps with
more precision and fewer characters that a paragraph of text.
(7) In addition, it's also common for data to be distributed as text files with
the extension .sql and with file contents consisting of one or more create-table
queries followed by many insert-into queries with values statements used to
create tables row-by-row. Such files are typically larger in size than CSV
files, but they also remove any ambiguity about the data types for columns,
allowing a table of data from one RDBMS to be exactly moved or copied to
another RDBMS.
*/


```