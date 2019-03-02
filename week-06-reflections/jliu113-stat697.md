
# Questions about Problems and Recipes



[Course Textbook Ch5, Problem 1]
* Question (jliu113-stat697): How can you get additional information about a table’s structure in SAS log?
- Answer (jliu113-stat697): Using DESCRIBE TABLE

[[Course Textbook Ch5, Problem 2]
* Question (jliu113-stat697): Can CREATE TABLE save a permanently table?
- Answer (jliu113-stat697):No, it is deleted at the end of the SAS session.

[[Course Textbook Ch5, Problem 3]
* Question (jliu113-stat697):What would happen if you don’t specify a column alias for a calculated column?
- Answer (jliu113-stat697): SAS assigns a column name, such as _TEMA001.

[[Course Textbook Ch5, Problem 4]
* Question (jliu113-stat697): What is the three ways to insert value into a table?  
- Answer (jliu113-stat697): 1. Using SET 2. VALUES 3. From exist table


[[Course Textbook Ch5, Problem 5]
* Question (jliu113-stat697): How to insert missing value?
- Answer (jliu113-stat697): Text: ‘’, numeric: .



[[Course Textbook Ch11, Problem 6]
* Question (jliu113-stat697): What’s the general integrity constraints?
- Answer (jliu113-stat697): CHECK, NOT NULL, UNIQUE, PRIMARY KEY.



[[Course Textbook Ch4, Problem 7]
* Question (jliu113-stat697): When is the difference important between INOBS and OUTOBS?
- Answer (jliu113-stat697):  Not simple query, eg, using the average function on a column with the PROC SQL option INOBS =10 returns an average of only the 10 values read for that column.                                                                                                                                                                                                  



[ddl-and-dml-sql-queries Week 6 SAS Recipe]
* Question (jliu113-stat697): What is the meaning of the function describe table?
- Answer (jliu113-stat697):  It's what would be put into a create-table query to create a new
table with the same column properties but no rows of data.


[reference-obtain-column-information Week 6 SAS Recipe]
* Question (jliu113-stat697): Why do we still need to considered best practice to copy/paste column names from a list of columns?
- Answer (jliu113-stat697):  When writing SQL queries, it's considered best practice to explicitly list all columns involved, rather than using select-* . However, typing out a list of column names can be tedious and error prone, especially if there are hundreds.”




***



# Recipes Exploration Results



```

* obtain-column-information recipes ;
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

proc contents order=varnum data= iris;
run;

proc sql;
    select
		 Species
		,SepalLength
		,SepalWidth
		,PetalLength
		,PetalWidth
	from
	    sashelp.iris;

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
	from dictionary.columns
	where 
	    lowcase(libname)= 'sashelp'
	and
	    lowcase(memname)= 'iris'
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



* ddl-and-dml-sql-queries;
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
	    add column3 char(42)
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
	    select * from sashelp.iris;
quit;


* DML example: create row of data using values statement for all columns;

proc sql;
    insert into Work.iris
	    values('Big Flower', 75,80,85,90);
quit;


* DML example: create row of data using values statement for select columns;

proc sql;
    insert into Work.iris
	    (Species, SepalLength)
		values ('Big Flower', 75);
quit;

* DML example: update rows of data;

proc sql;
    update Work.iris
	    set Species ='Big Flower'
		where SepalLength >64
	;
quit;


* DML example: delete rows of data;

proc sql;
    delete from Work.iris
	    where Species = 'Big Flower'
	;
quit;




```
