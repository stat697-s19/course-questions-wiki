
# Questions about Problems and Recipes

[Chapter 1, Problem 1]
* Question (mresendiz3-stat697): Why doesn't proc sql require the run statement at the end?



[Chapter 1, Problem 2]
* Question (mresendiz3-stat697): Can more than one statement be put down out of order within an proc sql step? how does sas recognize which step to use? What happens when the clauses are NOT in order?



[Chapter 1, Problem 4]
* Question (mresendiz3-stat697): Is it possible to reference single cells? if so is there a matrix address (like excel.)



[Chapter 1, Problem 6]
* Question (mresendiz3-stat697): Why is the keyword AS optional to use in the expression for #6?



[Chapter 1, Problem 7]
* Question (mresendiz3-stat697): Are there other types of clause "switches" that happen? What if I specify a GROUP BY clause in a query that doesnt have a summary function?
* Answer: The GROUP BY clause is changed into an ORDER BY clause. 



[Chapter 2, Problem 1]
* Question (mresendiz3-stat697): What keyword do I use to make sure my PROC SQL output doesn't have duplicates? Does this work with data that is uneven (having duplicates in character assignment but blank numerical values)?
* Answer: Use the DISTINCT keyword before the column name in the SELECT clause.



[Chapter 2, Problem 2]
* Question (mresendiz3-stat697): How do I list rows that have missing data? What similar operator do I NOT use and what is it for?
* Answer: Use the IS MISSING or IS NULL conditoinal operators. Do not use NOT EXISTS for this condition. The NOT EXISTS operator tests specifically for the existence of values returned by a subqery. 



[Chapter 2, Problem 3]
* Question (mresendiz3-stat697): What does the CALCULATED statement mean and do?
* Answer (mresendiz3-stat697): The CALCULATED key word tells PROC SQL that the value is calculated within the query when you use a column alias in the WHERE clause to refer to a calculated value. 


[Chapter 2, Problem 4]
* Question (mresendiz3-stat697): What does the HAVING clause mean and do?
* Answer (mresendiz3-stat697): The HAVING clause works together with the GROUP BY clause to be more specific with the groups that are displayed in the output based on whatever conditions were explicitly stated previously. 



[Chapter 2, Problem 10]
* Question (mresendiz3-stat697): Will PROC SQL still execute a query without a GROUP BY clause although there is a HAVING clause?
* Answer (mresendiz3-stat697): Yes, however it will not output the results that you want. The HAVING clause will treat the entire table as one group. 

[Summarize Data Using SQL Week 2 SAS Recipe]
* Question (mresendiz3-stat697): Is there a limit to the size of a dataset for proc SQL? If there is, is it different than SAS or R? Is there some way where we can amend this? Why dont we need the run statement at the end?



[Print To Log with Macro Variables Week 2 SAS Recipe]
* Question (mresendiz3-stat697): Can macros %put statements be used in PROC SQL?



***

```

# Recipes Exploration Results


*******************************************************************************;
* summarize-data-using-sql ;
*******************************************************************************;
/*
Scenario: We wish to summarize properties of columns in a table.

Approach: Use appropriate optional clauses in a SQL select query.

Recipe:
proc sql <options: optional>;
    <select clause: mandatory>
    <from clause: mandatory>
    <where clause: optional>
    <group-by clause: optional>
    <having clause: optional>
    <order-by clause: optional>
    ;
quit;

*/

*Example;


proc sql outobs = 3;
	select *
	from sashelp.iris;
quit;


 *sql version of proc sort and proc print;
proc sql outobs = 5 number;
	select *
	from sashelp.iris
	order by SepalLength;
quit;


proc sql;
	select Species, 
	count(*) as Number_of_irises
	from sashelp.iris
	group by Species;
;

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
/*
Scenario: We wish to print information to the log without using a null data step

Approach: Use the macro command %put

Recipe:
%put <text to print to log>;

*/

*Example;
%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put This is an example of &=recipeName.;
%put _user_;

/*
```


