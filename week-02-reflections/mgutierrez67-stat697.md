
# Questions about Problems and Recipes

[Ch.1, Problem 1]
* Question (mgutierrez67-stat697): What is the best practice or industry standard for writing out multiple columns in the Select clause for easier readability (i.e. one column name per line, multiple column names per line until a certain width is reached)?
- Answer (mgutierrez67-stat697): This question is answered in the summarize-data-using-sql recipe video. It is best practice to write the column name on a single line with a comma proceeding each additional columns.

[Ch.1, Problem 2]
* Question (mgutierrez67-stat697): If the query has consecutive select statements, should it all be under one proc sql statement or is there a benefit of having multiple proc sql's?

[Ch.1, Problem 6]
* Question (mgutierrez67-stat697): Does it take less computing resources/bandwidth to create a new column based on a calculation in the proc sql step compared to a SAS data step?

[Ch.1, Problem 7]
* Question (mgutierrez67-stat697): Does the Group By and Order By clause have the same performance (i.e. resources and amount of time needed to run the program) if there is no summary function? 

[Ch.2, Problem 1]
* Question (mgutierrez67-stat697): Does the Distinct keyword give unique output based on the columns specified in the select clause or the overall table? 

[Ch.2, Problem 3]
* Question (mgutierrez67-stat697): Is it good practice to include a where is missing or is null clause when using aggregate functions (i.e. count) that already factor in only non-missing values?

[Ch.2, Problem 4]
* Question (mgutierrez67-stat697): When should label be used versus renaming the column with the "as" keyword? 

[summarize-data-using-sql Week 2 SAS Recipe]
* Question (mgutierrez67-stat697): What are the advantages and disadvantages of using proc sql to run calculations or summary tables compared to data steps and proc freq?
- Answer (mgutierrez67-stat697): An advantage of a single proc sql can produce the same output of multiple proc and data steps. A disadvantage is proc sql can only function efficiently with data that is loaded on memory.

[summarize-data-using-sql Week 2 SAS Recipe]
* Question (mgutierrez67-stat697): Would it be beneficial to create a temporary dataset/table for each proc sql statement in the event those queries need to be referenced later on?

[print-to-log-with-macro-variables Week 2 SAS Recipe]
* Question (mgutierrez67-stat697): If macro variables are always assumed to be a string, is it possible to define the macro variable type as numeric character?
- Answer (mgutierrez67-stat697): Based on my findings and understanding, some programs may be able to identify the macro variable as intended to be used as a character, but an alternative approach is to use the input function to explicitly define it as a numeric variable.

***



# Recipes Exploration Results


```
* Recipe: summarize-data-using-sql ;

* original recipe;
proc sql outobs=3;
  select 
    *
  from
    sashelp.iris
   ;
quit;

proc sql outobs=5;
  select
    Species
    ,count(*) as Number_of_Irises
  from
    sashelp.iris
  group by 
    Species
  ;
  
  select 
    Species
    ,min(SepalLength) as Minimum_Sepal_Length
    ,median(SepalLength) as Median_Sepal_Length
    ,max(SepalLength) as Max_Sepal_Length
  from 
    sashelp.iris
  group by
    Species
  ;
quit;
  

*modified code to remove quit statement in-between proc sql statements to determine if program would still run. SAS was able to successfully run the program as if the quit statement was there.

proc sql outobs=3;
  select 
    *
  from
    sashelp.iris
   ;

proc sql outobs=5;
  select
    Species
    ,count(*) as Number_of_Irises
  from
    sashelp.iris
  group by 
    Species
  ;
  
  select 
    Species
    ,min(SepalLength) as Minimum_Sepal_Length
    ,median(SepalLength) as Median_Sepal_Length
    ,max(SepalLength) as Max_Sepal_Length
  from 
    sashelp.iris
  group by
    Species
  ;
quit;



* Recipe: print-to-log-with-macro-variables ;

* original recipe;
%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put This is an example of the recipe &=recipeName.;
%put _user_;

*modified the macro variable to a number to determine if using proc sql in SAS will be able to automatically identify when it is appropriate to change a macro variable from a string to an integer type;
*the program was able to automatically determine that the macro variable should be evaluated as an integer to perform the addition calculation in the proc sql statement

%let recipeCount=1;

proc sql outobs=3;
  select 
    1 + &recipeCount. as sum
  from 
    sashelp.iris
  ;
quit;

```
