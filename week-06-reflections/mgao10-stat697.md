
# Questions about Problems and Recipes


[Week6 Reflection - TB Ch5, Problem 1]
* Question (mgao10-stat697): what is the difference between select, copy,describe and copy statement



[Week6 Reflection - TB Ch5, Problem 2]
* Question (mgao10-stat697): how to sort out the variable by level



[Week6 Reflection - TB Ch5, Problem 3]
* Question (mgao10-stat697): what is the difference between delete and drop statement



[Week6 Reflection - TB Ch5, Problem 4]
* Question (mgao10-stat697): when should i use when or if statement



[Week6 Reflection - TB Ch5, Problem 5]
* Question (mgao10-stat697): how to use set and create interchangably



[Week6 Reflection - TB Ch8, Problem 6]
* Question (mgao10-stat697): What is inobs= 



[Week6 Reflection - TB Ch8, Problem 7]
* Question (mgao10-stat697): what is stmer option in proq sql



[obtain-column-information Week 6 SAS Recipe]
* Question (mgao10-stat697): how to use wildcard to extrac information from the columns



[ddl-and-dml-sql-queries Week 6 SAS Recipe]
* Question (mgao10-stat697): what is the major difference between ddl and dml sql queries



***



# Recipes Exploration Results



```

*Example For Approach 1;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;

*Example For Approach 2;
proc contents order=varnum data=sashelp.iris;
run;
proc sql;
    select
        <list of columns obtained by copying/pasting>
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
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;



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
