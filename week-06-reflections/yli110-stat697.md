
# Questions about Problems and Recipes



[Course Textbook Chapter 5, Problem 1]
* Question (yli110-stat697): What are the three common ways to create a new table in PROC SQL?



[Course Textbook Chapter 5, Problem 3]
* Question (yli110-stat697): What is the difference between UNDO POLICY = REQUIRED and UNDO POLICY = NONE?



[Course Textbook Chapter 5, Problem 5]
* Question (yli110-stat697): What is the statement you use to delete rows from a table?



[Course Textbook Chapter 5, Problem 6]
* Question (yli110-stat697): Under what conditions do you use the statement CASE WHEN-THEN?



[Course Textbook Chapter 5, Problem 8]
* Question (yli110-stat697): What can the statement ALTER TABLE do?



[Course Textbook Chapter 5, Problem 9]
* Question (yli110-stat697): Which statement do you use to display the table information in SAS log?



[Course Textbook Chapter 5, Problem 10]
* Question (yli110-stat697): When creating an empty table, how do you list the column specifications?



[Course Textbook Chapter 8, Problem 1]
* Question (yli110-stat697): Where do you specify the options in PROC SQL?



***



# Recipes Exploration Results



```


[place your recipes exploration here, and delete this line]



```



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
	select /*copy your columns info below, same as using * to select all*/
		 Species
		,SepalLength
		,SepalWidth
		,PetalLength
		,PetalWidth
	from sashelp.iris
	;
quit;


*Example For Approach 2;

proc contents order = varnum data = sashelp.iris; /*copy columns into excel*/
run;

proc sql;
	select /*copy from excel to sas*/
		 Species
		,SepalLength
		,SepalWidth
		,PetalLength
		,PetalWidth
	from sashelp.iris
	;
quit;





*Example For Approach 3;

proc sql;
	select
		name
	from 
		dictionary.columns /*dictionary can only be accessed by PROC SQL*/
	where
		libname = 'SASHELP'
		and
		memname = 'IRIS'
	;
quit;


proc sql;
	create table work.temp
	(
		 column1 char(42)
		,column2 num
	);
quit;

* DDL example: obtain column information;

proc sql;
	describe table work.temp;
quit;


* DDL example: add column;

proc sql;
	alter table work.temp
		add column3 char(54)
	;
quit;

* DDL example: modify column;

proc sql;
	alter table work.temp
		modify column1 char(54)
	;
quit;


* DDL example: delete column;

proc sql;
	alter table work.temp
		drop column2
	;
quit;


* DDL example: delete table;

proc sql;
	drop table work.temp;
quit;


* DML example setup: define column information;

proc sql;
	create table work.iris
		like sashelp.iris
	;
quit;


* DML example: obtain rows of data;

proc sql;
	select *
		from work.iris
	;
quit; /*no rows, only coped the columns*/


* DML example: create rows of data from select query;

proc sql;
	insert into work.iris
		select * from sashelp.iris
	;
quit;


* DML example: create row of data using values statement for all columns;

proc sql;
	insert into work.iris
		values (
				'Big Flower', 75, 80, 80, 75
				)
	;
quit;


* DML example: create row of data using values statement for select columns;

proc sql;
	insert into work.iris
		(Species, SepalLength)
		values ('Big flower', 75)
	;
quit;


* DML example: update rows of data;

proc sql;
	update work.iris
		set Species = 'Big Flower'
		where
			SepalLength > 64
	;
quit;


* DML example: delete rows of data;

proc sql;
	delete from work.iris
		where Species = 'Big Flower'
	;
quit;

