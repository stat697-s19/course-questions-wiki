# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mstafford5-stat697): It is common practice to make SELECT and similar statements uppercase. Why aren't the SQL statements uppercase to distinguish between what is code and not?  



[Course Structure Quiz, Problem 2]
* Question (mstafford5-stat697): How is "order by" reckognized as one function rather than two words even though it has a space?



[Course Structure Quiz, Problem 3]
* Question (mstafford5-stat697): How can complex operations, such as exponentiation be done on rows with proc sql statementes?



[Course Structure Quiz, Problem 4]
* Question (mstafford5-stat697): How often do sas users use group by clauses without a summary function?



[Course Structure Quiz, Problem 5]
* Question (mstafford5-stat697): How do the example problems in the text compare to real-world problems that data scientists face?



[Course Structure Quiz, Problem 6]
* Question (mstafford5-stat697): How can a programmer identify if a query is overly complex or takes up too much memory to run?



[Course Structure Quiz, Problem 7]
* Question (mstafford5-stat697): How can you find the proportion of values that a 'group by' function selects for? For example, how would you find the proportion of library categories with an average of 2500 checkouts in the simplest way?



[sas_summarize_data_using_sql Week 2 SAS Recipe]
* Question (mstafford5-stat697): Is it more efficient to use proc sql in leu of commands in sas such as proc means?



[macros_text_to_print Week 2 SAS Recipe]
* Question (mstafford5-stat697): What types of errors and troubleshooting can be done with the macros %put statements?



***



# Recipes Exploration Results




```
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

*sql version of proc print;
proc sql outobs = 3;
	select *
	from sashelp.iris;
quit;

*sql version of proc sort/print;
proc sql outobs = 5 number;
	select *
	from sashelp.iris
	order by SepalLength
;quit;
*	avg(SepalLength) as Mean_len;
*sql version of proc freq and pproc means;
proc sql;
	select Species, count(*) as Number_of_irises
	from sashelp.iris
	group by Species;

	select
		Species
		,min(SepalLength) as Min_len
		,median(SepalLength) as Med_len
		,max(SepalLength) as Max_len
	
	from
		sashelp.iris
	group by
		Species
	;
quit;


Recipe:
%put <text to print to log>;

*/

*Example;
%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put Including the equals sign &=recipeName.;
%put _user_;

```

