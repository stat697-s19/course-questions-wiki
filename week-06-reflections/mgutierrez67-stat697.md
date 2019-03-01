
# Questions about Problems and Recipes

[Ch.5, Problem 1]
* Question (mgutierrez67-stat697): What are the benefits and downsides of creating a table using a proc sql step versus a data step?

[Ch.5, Problem 5]
* Question (mgutierrez67-stat697): Is there a way to retrieve deleted rows if a Delete statement was unintentionally or incorrectly processed?

[Ch.5, Problem 6]
* Question (mgutierrez67-stat697): Should calculations be performed within the proc sql step or separate data step if it is a big data set with numerous calculations?

[Ch.5, Problem 9]
* Question (mgutierrez67-stat697): Is there a difference between Describe statement and proc contents?

[Ch.8, Problem 5]
* Question (mgutierrez67-stat697): What are some real-world scenarios for needing to use the timer functions?

[Ch.8, Problem 8]
* Question (mgutierrez67-stat697): How is a dictionary easier to manipulate? Since dictionaries are referencing existing SAS tables, couldn’t the user query the table since it is already in the Work temporary library?
- Answer (mgutierrez67-stat697): Per the recipe video, there are alternative approaches, but the dictionary method can be more efficient depending on the objective & goal.

[Ch.8, Problem 8]
* Question (mgutierrez67-stat697): Can a dictionary be turned into a permanent read-only SAS table that can be updated during the next SAS session?  

[reference-obtain-column-information Week 6 SAS Recipe]
* Question (mgutierrez67-stat697): When specifying a specific library or column, should the user type the exact column names?
- Answer (mgutierrez67-stat697): Per recipe exploration, yes, one should be aware of case sensitivity when using the dictionary views or it might not process as intended. 

[ddl-and-dml-sql-queiries Week 6 SAS Recipe]
* Question (mgutierrez67-stat697): Is it best practice to completely delete a row or create a flag column that is used to indicate which rows are valid or not valid?  The second approach will still have records of all observations that were once in the table compared to just erasing it.


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


*modified the code by removing the lowcase function in the dictionary query to test if case sensitivity needs to be taken into consideration
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


*modified the code to determine if using the incorrect data type would cause an error
*the table defined the second column as a num, but the insert statement was a character number
*some languages or processes assume that the intention was to convert this into a number and allow this step to run, but that is not the case with this type of proc sql structure

proc sql;
    insert into Work.iris
        (Species,SepalLength)
        values('Big Flower','75')
    ;
quit;


```
