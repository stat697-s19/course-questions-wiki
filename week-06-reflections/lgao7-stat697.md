
# Questions about Problems and Recipes



[Week6 Reflection - TB Ch5, Question 1]
* Question (lgao7-stat697):  What are the different ways to create a table using PROC SQL?



[Week6 Reflection - TB Ch5, Question 2]
* Question (lgao7-stat697): What would be the alternative way to get the similar contents as DESCRIBE TABLE statement? 



[Week6 Reflection - TB Ch5, Question 3]
* Question (lgao7-stat697):  What does the option BUFSIZE=OPTION do?



[Week6 Reflection - TB Ch5,  Question 4]
* Question (lgao7-stat697):  How to insert user-defined rows to a table in PROC SQL?



[Week6 Reflection - TB Ch, Question 5]
* Question (lgao7-stat697): What are the constraint types of a table?



[Week6 Reflection - TB Ch5, Question 6]
* Question (lgao7-stat697):  What does the UNDO_POLICY=option do?



[Week6 Reflection - TB Ch8, Question 7]
* Question (lgao7-stat697):  What is STIMER option in PROC SQL? 



[Week6 Reflection - SAS Recipe 1, Question 1]
* Question (lgao7-stat697):  What would be the alternative way as the proc contents?
* Answer (lgao7-stat697): PROC SQL with DESCRIBE TABLE statement.



[Week6 Reflection - SAS Recipe 2, Question 1]
* Question (lgao7-stat697): What’s the different between DROP TABLE work.dataset and DELETE FROM work.dataset?



***



# Recipes Exploration Results



```


* [SAS Recipe 1:  obtain-column-information;

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


*Example For Approach 3;
proc sql;
	select
		name
	from
		dictionary.columns
	where
		lowcase(libname) = "sashelp"
		and
		lowcase(memname) = "iris"
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

/* Notes:
 - it doesn't matter which approach is used 
to get the same list of columns as quickly as possible.
*/ 




[SAS Recipe 2:  dl-and-dml-sql-queries ;

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
	describe table Work.temp;
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
		values('Big FLower', 75, 80, 85, 90)
	;
quit;

* DML example: create row of data using values statement for select columns;
proc sql;
	insert into Work.iris
		(Species, SepalLength)
		values('Big Flower', 75);
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



```
