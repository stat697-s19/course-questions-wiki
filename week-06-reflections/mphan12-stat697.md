
# Questions about Problems and Recipes



[Chapter 5, Problem 1]
- Question (mphan12-stat697):  How can you get table structure information?
- Answer (mphan12-stat697):  Using DESCRIBE TABLE which list the column attributes and structure of the table.



[Chapter 5, Problem 3]
- Question (mphan12-stat697):  What does the DELETE statement do?
- Answer (mphan12-stat697):  DELETE statement will delete rows based on the WHERE clause.



[Chapter 5, Problem 5]
- Question (mphan12-stat697):  What does the ALTER TABLE statement do?
- Answer (mphan12-stat697): It is used to modify the specifications of an existing column when paired with the MODIFY clause, it can add a new column definition(s) when paired with the ADD clause, and can delete existing columns when paried with the DROP clause. 



[Chapter 5, Problem 7]
- Question (mphan12-stat697):  What does the INSERT statement do?
- Answer (mphan12-stat697):  The INSERT statement is used to insert new rows into an existing or into a new table.



[Chapter 8, Problem 6]
- Question (mphan12-stat697):  What does OUTOBS=10 do?
- Answer (mphan12-stat697): Compile query then output the first 10 observations.



[Chapter 8, Problem 6]
- Question (mphan12-stat697):  What does OUTOBS=10 do?
- Answer (mphan12-stat697): Compile query then output the first 10 observations.



[reference-obtain-column-information Week 6 SAS Recipe]
- Question (mphan12-stat697): Why is it preferred to copy and paste a list of column names within a PROC SQL query?
- Answer (mphan12-stat697): To mitigate the errors it's good practice to copy and paste. 



[ddl-and-dml-sql-queiries Week 6 SAS Recipe]
- Question (mphan12-stat697): Why does SAS only supports character and numeric columns?
- Answer (mphan12-stat697): To minimizes the space that the file takes up as memory on a disk. 


***



# Recipes Exploration Results



```


* Recipe: reference-obtain-column-information;
* original recipe;

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


*removing the lowcase function caused the program to not function properly and gave no output
*names must match exactly in the dictionary or it will not process as intended
proc sql;
    select
        name
    from
        dictionary.columns
    where
        libname = 'sashelp'
    and
        lowcase(memname) = 'iris'
    ;
quit;


* Recipe: ddl-and-dml-sql-queiries;
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


proc sql;
    insert into Work.iris
        (Species,SepalLength)
        values('Big Flower','75')
    ;
quit;



```
