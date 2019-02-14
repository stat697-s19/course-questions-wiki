
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (yli110-stat697): In SQL clauses, what sign is used to separate columns?
- Answer (yli110-stat697): comma



[Course Structure Quiz, Problem 2]
* Question (yli110-stat697): What are the differences between statements and clauses in SAS SQL?



[Course Structure Quiz, Problem 3]
* Question (yli110-stat697): Which clause is used to specify how the rows are to be sorted?



[Course Structure Quiz, Problem 4]
* Question (yli110-stat697): How to create a new column and assign this column an alias?



[Course Structure Quiz, Problem 5]
* Question (yli110-stat697): What is the difference between **GROUP BY** and **ORDER BY**?



[Course Structure Quiz, Problem 6]
* Question (yli110-stat697): How to remove duplicate values from PROC SQL output?



[Course Structure Quiz, Problem 7]
* Question (yli110-stat697): What is the difference between **IS MISSING** / **IS NULL** and **NOT EXISTS** ?



[Course Structure Quiz, Problem 8]
* Question (yli110-stat697): How do you reference a new column that is created in the SELECT clause in clauses like WHERE or HAVING?



[Course Structure Quiz, Problem 9]
* Question (yli110-stat697): How do summary functions and GROUP BY determine the number of rows in the output of PROC SQL?



[Course Structure Quiz, Problem 10]
* Question (yli110-stat697): What does the HAVING clause do when a GROUP BY clause is not present?



[summarize-data-using-sql Week 2 SAS Recipe]
* Question (yli110-stat697): What is the difference between WHERE clause and HAVING clause?
- Answer (yli110-stat697): WHERE controls what rows in the input step, and HAVING controls what to output. Besides, HAVING is only different from WHERE when GROUP BY is present.



[print-to-log-with-macro-variables Week 2 SAS Recipe]
* Question (yli110-stat697): Why is it unnecessary to use quotation marks for macro variables?



***



# Recipes Exploration Results



```



**imitating proc print;
proc sql outobs=3;
    select *
    from sashelp.iris
    ;
quit;

**imitatin proc sort and proc print;
proc sql outobs=3 number;
    select *
    from sashelp.iris
    order by sepallength /*sort the data ahead of time*/
    ;
quit;


proc sql;
**imitating proc freq;
    select species, count(*) as Number_of_irises
    from sashelp.iris
    group by species
    ;
**imitating proc means;
    select
         species
        ,min(sepallength) as Min_Sepal_Length
        ,median(sepallength) as Median_Sepal_Length
        ,max(sepallength) as Max_Sepal_Length
    from
        sashelp.iris
    group by
        species
    ;
quit;


%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;/*only the macro variable's content*/
%put This is an example of &=recipeName.; /*macro variable name and content*/
%put _user_; /*list all user-defined macro variables*/



```



