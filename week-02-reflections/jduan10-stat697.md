
# Questions about Problems and Recipes



[Course Textbook Chapter 1, Problem 1] 
- Question (jduan10-stat697): What does clause mean in PROC SQL?



[Course Textbook Chapter 1, Problem 2] 
- Question (jduan10-stat697): Why doesn’t PROC SQL require run?



[Course Textbook Chapter 1, Problem 4] 
- Question (jduan10-stat697): Does clauses in PROC SQL need to appear in order?



[Course Textbook Chapter 1, Problem 6] 
- Question (jduan10-stat697): Can a PROC SQL step contains more than one SELECT statement?



[Course Textbook Chapter 1, Problem 7] 
- Question (jduan10-stat697): Can I create a new column with calculation in PROC SQL?



[Course Textbook Chapter 2, Problem 1] 
- Question (jduan10-stat697): Does the order of WHERE and ORDER BY statement matter?



[Course Textbook Chapter 2, Problem 2] 
- Question (jduan10-stat697): Does the OUTOBS= option restrict the rows that are read?



[Course Textbook Chapter 2, Problem 3] 
- Question (jduan10-stat697): How to create a negative condition?



[Course Textbook Chapter 2, Problem 4] 
- Question (jduan10-stat697): When specifying the limits for the range of values, is it necessary to specify the smaller value first?



[Course Textbook Chapter 2, Problem 10] 
- Question (jduan10-stat697): What’s the difference of using IS MISSING or NULL operator to specify missing values?



[Week 2 SAS Recipe: summarize-data-using-sql] 
- Question (jduan10-stat697): Can we put two variable names in the ORDER BY  statement?



[Week 2 SAS Recipe: print-to-log-with-macro-variables]
- Question (jduan10-stat697): What is string literal?



***



# Recipes Exploration Results



```


*Recipe: summarize-data-using-sql;

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
         Species
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



*Recipe:print-to-log-with-macro-variables;

%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put This is an example of &=recipeName.;
%put _user_;

```
