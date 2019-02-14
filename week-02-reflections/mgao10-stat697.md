
# Questions about Problems and Recipes


[Course Structure Quiz, Problem 1]
* Question (mgao10-stat697): What is the purpose of the PROC SQL

[Course Structure Quiz, Problem 2]
* Question (mgao10-stat697): what other command count as statement?

[Course Structure Quiz, Problem 3]
* Question (mgao10-stat697): Why comma is used to separate the variable

[Course Structure Quiz, Problem 4]
* Question (mgao10-stat697): Should I practice the questions from our textbook?

[Course Structure Quiz, Problem 5]
* Question (mgao10-stat697): what does the option b affect the code?

[Course Structure Quiz, Problem 6]
* Question (mgao10-stat697): why there is no comma after 120-spent as Balance

[Course Structure Quiz, Problem 7]
* Question (mgao10-stat697): what is the relationship abou group by with having?

[summarize-data-using-sql Week 2 SAS Recipe]
* Question (mgao10-stat697): What is the where claus means

[print-to-log-with-macro-variables Week 2 SAS Recipe]
* Question (mgao10-stat697): what is the usasge of "/"



***



# Recipes Exploration Results



```
* Recipe: print-to-log-with-macro-variables ;

* original recipe;
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
	;
quit;



*imitating proc scort and proc print;
proc sql outobs = 5 number;
    select *
	from sashelp.iris
	order by SepaLLength
	;
quit;




proc sql;
   *imitating proc;
   select Species, count(*) as Number_of_Irises
   from sashelp.iris
   group by Species
   ;
   *imitating proc means;
   select 
         Sepecies
	    ,min(SepalLength) as Mininum_Sepal_Length
	    ,median(SepalLength) as Median_Sepal_Length
	    ,max(SepalLength) as Maxium_Sepal_Length
   from 
        sashelp.iris
   group by
        Species
	;
quit;



```
