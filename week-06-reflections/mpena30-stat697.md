
# Questions about Problems and Recipes



[Course Textbook, Chapter 5]
* Question (mpena30-stat697): Is there any functional difference between using keywords CHAR and VARCHAR to specify data type when creating a table by defining columns?



[Course Textbook, Chapter 5]
* Question (mpena30-stat697): Can creating a table from a query result using CREATE TABLE be a substitute for joining columns from two or more different existing tables?
- Answer (mpena30-stat697): Yes, the queries used can be a joining of tables.



[Course Textbook, Chapter 5] 
* Question (mpena30-stat697): What is the difference in the result of creating integrity constraints outside of a column specification versus creating them as part of the column specifications?



[Course Textbook, Chapter 5]
* Question (mpena30-stat697):Why does SAS prevent all new/modified data from being added if only some of the values do not comply with the integrity constraints resulting in an error message?



[Course Textbook, Chapter 8]
* Question (mpena30-stat697): When using INOBS or OUTOBS to control execution, is the number of rows specified taken in order from the top of the list? How are the rows choosen?



[Course Textbook, Chapter 8]
* Question (mpena30-stat697): In what case would writing out the default version of an option be desirable?



[Course Textbook, Chapter 8]
* Question (mpena30-stat697): If the SAS system option STIMER is not already enabled, how can it be enabled?



[obtain-column-information Week 6 SAS Recipe]
* Question (mpena30-stat697): If the column names are copied from the SAS Explorere dataset, will these names also be shortened by number of characters?



[ddl-and-dml-sql-queries Week 6 SAS Recipe]
* Question (mpena30-stat697):  Is there any added efficiency with putting more than one data manipulation query into a single statement as opposed to seperate statements?




***



# Recipes Exploration Results



```


* Recipe: obtain-column-information ;

* original recipe;

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
Recipe for Approach 3:
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

*Example for Approach 3;
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

	
	
* Recipe: ddl-and-dml-sql-queries ;	

* original recipe;

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
quit

* DDL: delete table;
proc sql;
	drop table Work.tmp;
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
		values('Big Flower',75,80,85,90)
	;
quit;

* DML example: create row of data using values statement for select columns;
proc sql;
	insert into Work.iris
		(Species, SepalLength)
		values('Big Flower',75)
	;
quit;

* DML example: update rows of data;
proc sql;
	update Work.iris
		set Species='Big Flower'
		where 
			SepalLength > 64
	;
quit;

* DML example: delete rows of data;
proc sql;
	delete from Work.iris
		where Species='Big Flower'
	;
quit;




```
