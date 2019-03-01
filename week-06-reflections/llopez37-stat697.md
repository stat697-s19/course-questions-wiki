
# Questions about Problems and Recipes



[Course Textbook Chapter 5 Problem 5]
- Question (llopez37-stat697): what happens if we do not specify any variable after the delete statement?
- Answer(llopez37-stat660): it seems like all the rows are deleted.

[Course Textbook Chapter 5 Problem 7]
- Question (llopez37-stat697): can we use insert to add columns as well?

[Course Textbook Chapter 5 Problem 8]
- Question (llopez37-stat697) is alter the same as add or drop statrmentz?

[Course Textbook Chapter 5, Problem 9]
- Question (llopez37-stat697): is describe specific to the columns?
- Answer (llopez37-stat697) this seems to be the caae

[Course Textbook Chapter 8 Problem 1]
- Question (llopez37-stat697) how lomg does change take place?

[Course Textbook Chapter 8, Problem 7]
- Question (llopez37-stat697): how often are the dictionary tables updated?

[Course Textbook Chapter 8 Problem 9]
- Question (llopez37-stat697): how do you view how a dictionary table is defined.
- Answer (llopez37-stat697) it seems when it is created a loh message appears defining it.

[DDL and DML Week 6 SAS Recipe]
- Question (llopez37-stat697): What is the preference between ddl and dml?


[Column EditingWeek 6 SAS Recipe]
- Question (llopez37-stat697): what is best approach from the 3 methods?

***



# Recipes Exploration Results



```



proc sql;
    create table Work.tmp
    (
         column1 char(42)
        ,column2 num
    );
quit;

proc sql;
    describe table Work.tmp;
quit;

proc sql;
    alter table Work.tmp
        add column3 char(42)
    ;
quit;


proc sql;
    alter table Work.tmp
        modify column1 char(54)
    ;
quit;


proc sql;
    alter table Work.tmp
        drop column2
    ;
quit;

proc sql;
    drop table Work.tmp;
quit;

proc sql;
    create table Work.iris
        like sashelp.iris
    ;
quit;

proc sql;
    select * from Work.iris;
quit;

proc sql;
    insert into Work.iris
        select * from sashelp.iris
    ;
quit;

proc sql;
    insert into Work.iris
        values('Big Flower',75,80,85,90)
    ;
quit;

proc sql;
    insert into Work.iris
        (Species,SepalLength)
        values('Big Flower',75)
    ;
quit;

proc sql;
    update Work.iris
        set Species='Big Flower'
        where SepalLength > 64
    ;
quit;

proc sql;
    delete from Work.iris
        where Species='Big Flower'
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

proc contents order = varnum data=sashelp.iris;
run;


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
```
