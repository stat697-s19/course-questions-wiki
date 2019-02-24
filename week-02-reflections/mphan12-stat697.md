
# Questions about Problems and Recipes



[Chapter 1, Problem 1]
- Question (mphan12-stat697): In the select statement of PROC SQL, how are columns seperated?
- Answer (mphan12-stat697): Columns are seperated by commas in the select statement of the PROC SQL procedure.



[Chapter 1, Problem 2]
- Question (mphan12-stat697): What are the basic clauses required to run a SELECT statement in PROC SQL procedure?
- Answer (mphan12-stat697): The SELECT statement contains several clauses: SELECT, FROM, WHERE, and ORDER BY.



[Chapter 1, Problem 4]
- Question (mphan12-stat697): How do you sort a table by the second column in descending order of the select statement in PROC SQL procedure?
- Answer (mphan12-stat697): ORDER BY 2 DESC ;



[Chapter 1, Problem 6]
- Question (mphan12-stat697): How do you create a new column in PROC SQL?
- Answer (mphan12-stat697): select OLD_COLUMN as NEW_COLUMN



[Chapter 1, Problem 7]
- Question (mphan12-stat697): What happens if you use a GROUP BY clause in a PROC SQL step without a summary function?
- Answer (mphan12-stat697): The GROUP BY clause is changed to an ORDER BY clause.



[Chapter 2, Problem 1]
- Question (mphan12-stat697): In PROC SQL, how do you remove duplicate records?
- Answer (mphan12-stat697): select distinct column_A, column_B, ....



[Chapter 2, Problem 2]
- Question (mphan12-stat697): What is the where clause syntax for identifying data with no values?
- Answer (mphan12-stat697): where var IS missing or where var is NULL.



[Chapter 2, Problem 3]
- Question (mphan12-stat697): What does the CALCULATED statement do?



[Chapter 2, Problem 4]
- Question (mphan12-stat697): What does the HAVING clause do?
- Answer (mphan12-stat697): A HAVING clause works with the GROUP BY clause to restrict the groups that are displayed in the output, based on one or more specified conditions



[Chapter 2, Problem 10]
- Question (mphan12-stat697): If you want to use HAVING clause, must you also have GROUP BY clause?
- Answer (mphan12-stat697): Yes.



[Summarize Data Using SQL Week 2 SAS Recipe]
- Question (mphan12-stat697): What are the manadatory clauses required in PROC SQL?
- Answer (mphan12-stat697): The SELECT and FROM clauses are mandatory.



[Print To Log with Macro Variables Week 2 SAS Recipe]
- Question (mphan12-stat697): What does &=recipeName do in SAS Macro?
- Answer (mphan12-stat697): The macro variable "recipeName" is dereferenced using an ampersand (&)
together with an equal sign (=), which causes the name of the macro variable to also be printed to the log instead of the value.



***



# Recipes Exploration Results



```



*******************************************************************************;
**************** 80-character banner for column width reference ***************;
* set window width to banner width to calibrate line length to 80 characters  *;
*******************************************************************************;

*******************************************************************************;
* summarize-data-using-sql ;
*******************************************************************************;
* print the first 3 rows from sashelp.iris;
proc sql outobs=3;
    select
        *
    from
        sashelp.iris
    ;
quit;

* print the first 5 rows of sashelp.iris after sorting by SepalLength;
proc sql outobs=5 number;
    select
        *
    from
        sashelp.iris
    order by
        SepalLength
    ;
quit;

* summarize values for qualitative and quantitative variables;
proc sql;
    * print frequency of each Species in sashelp.iris;
    select
         species
        ,count(*) as Number_of_Irises
    from
        sashelp.iris
    group by
        Species
    ;
    * print median of SepalLength by Species in sashelp.iris;
    select
         Species
        ,min(SepalLength) as Minimum_Sepal_Length
        ,median(SepalLength) as Median_Sepal_Length
        ,max(SepalLength) as Maximum_Sepal_Length
    from
        sashelp.iris
    group by
        Species
    ;
quit;


*******************************************************************************;
* print-to-log-with-macro-variables ;
*******************************************************************************;

*Example;
%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put This is an example of &=recipeName.;
%put _user_;




```
