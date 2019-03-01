
# Questions about Problems and Recipes



[Chapter 5, Question 1]
* Question (mstafford5-stat697): Why are copies of new tables made first, instead of directly editing the original? How much time would it save to do it directly?



[Chapter 5, Question 5]
* Question (mstafford5-stat697): What are the SQL methods of using SAS statements like drop and keep?



[Chapter 5, Question 6]
* Question (mstafford5-stat697): Can update be called to set a new column, or do you have to make an alter statement before?



[Chapter 5, Question 8]
* Question (mstafford5-stat697): Why are the alter table statements unable to add values to new columns?



[Chapter 5, Question 9]
* Question (mstafford5-stat697): Is there a method like describe table that will offer mean, correlations, and other descriptors, similar to the glimpse function in R?



[Chapter 8, Question 7]
* Question (mstafford5-stat697): Are dictionaries typically stored in key-value pairs?



[Chapter 8, Question 9]
* Question (mstafford5-stat697): How are the different SAS libraries organized?




[ddl-and-dml-sql-queries Week 6 SAS Recipe]
* Question (mstafford5-stat697): What does bufsize mean? How can a table in a .sql file be saved and shared?



[obtain-column-information Week 6 SAS Recipe]
* Question (mstafford5-stat697): Is there a way to program methods like copying and pasting through macros?



***



# Recipes Exploration Results




```
* Recipe: obtain-column-information ;

*Example For Approach 1;
proc sql;
create table abc as
    select
        Species,
		SepalLength,
		SepalWidth,
		PetalLength,
		PetalWidth
    from
        sashelp.iris
    ;
quit;

*Example For Approach 2;
proc contents order=varnum data=sashelp.iris;
run;
proc sql;
create table def as
    select
        Species,
		SepalLength,
		SepalWidth,
		PetalLength,
		PetalWidth
    from
        sashelp.iris
    ;
quit;

proc compare
	        base=abc
	        compare=def
	        novalues
	    ;
	run;

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
        Species,
		SepalLength,
		SepalWidth,
		PetalLength,
		PetalWidth
    from
        sashelp.iris
    ;
quit;
*compared first and second tables;


*Recipe: ddl-and-dml-sql-queries;
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
        (Species,SepalLength)
        values('Big Flower',75)
    ;
quit;

* DML example: update rows of data;
proc sql;
    update Work.iris
        set Species='Big Flower'
        where SepalLength > 64
    ;
quit;

* DML example: delete rows of data;
proc sql;
    delete from Work.iris
        where Species='Big Flower'
    ;
quit;


```
