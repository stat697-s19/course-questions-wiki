
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (dzhou11-stat697):What does the code ¡®ORDER BY ¡®mean?
- Answer (dzhou-stat697): The ORDER BY clause sorts the results of a query expression according to the order specified in that query. When this clause is used, the default ordering sequence is ascending, from the lowest value to the highest. You can use the SORTSEQ= option to change the collating sequence for your output.

[Course Structure Quiz, Problem 2]
* Question (dzhou11-stat697): Does Sort by exist in SQL?
- Answer (dzhou-stat697):There is nothing like "sortBy" in SQL For sorting of data in SQL the ORDER BY clause is used which allows you to sort the records in your result set. And it can only be used in SELECT statements.

[Course Structure Quiz, Problem 3] 
* Question (dzhou11-stat697): can we use GE instead by symbols in SQL
- Answer (dzhou-stat697):

[Course Structure Quiz, Problem 4] 
* Question (dzhou11-stat697): When we use duplicate, Why OUTOBS= option has been removed from the PROC SQL statement?
- Answer (dzhou-stat697): 

[Course Structure Quiz, Problem 5]
 * Question (dzhou11-stat697): If the code is WHERE salary between 70000 and 80000, can we write as WHERE salary>70000 and salary<80000 £¿
- Answer (dzhou-stat697):

[Course Structure Quiz, Problem 6] 
* Question (dzhou11-stat697): What's the difference between HAVING and WHERE?
- Answer (dzhou-stat697): HAVING: is used to check conditions after the aggregation takes place.WHERE: is used to check conditions before the aggregation takes place.

[Course Structure Quiz, Problem 7]
* Question (dzhou11-stat697): In WHERE clause, can we use & or ¡°,¡± instead of AND?
- Answer (dzhou-stat697):

[Week2 Reflection - SAS Recipe 1, Question 1]
* Question (dzhou11-stat697):what is the different from COUNT(*) and COUNT(column)
- Answer (dzhou-stat697): COUNT(*) is the total number of rows in a group or in a table. COUNT(column) is the total number of rows in a group or in a table for which there is a nonmissing value in the selected column




***



# Recipes Exploration Results



```


%let recipeName = print-to-with-marco-varibales;
%put This is an example of the recipe  &recipeName.;
%put This is an example of &=recipeName.;
%put _user_;

* Recipe:summary ;
 
* original recipe;
*imitating proc print; 
proc sql outobs = 3;
     select *
	from sashelp.iris 
quit;
*imitating proc scort and proc print; 
proc sql outobs = 5 number;
   select *
	from sashelp.iris
	order by SepaLLength 
quit; 
proc sql;
   *imitating proc;
   select Species, count(*) as Number_of_Irises 
   from sashelp.iris
   group by Specie
   ;
   *imitating proc means;
   select 
         Sepecie
	    ,min(SepalLength) as Mininum_Sepal_Length
	    ,median(SepalLength) as Median_Sepal_Lengt
	    ,max(SepalLength) as Maxium_Sepal_Lengt
   from 
        sashelp.iris
   group by
        Species
	;
quit;




```
