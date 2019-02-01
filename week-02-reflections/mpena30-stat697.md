
# Questions about Problems and Recipes



[Course Textbook, Chapter 1]
* Question (mpena30-stat697):  Does the GROUP BY clause estentially do what the ORDER BY clause does, also putting the specified columns in order?



[Course Textbook, Chapter 1]
* Question (mpena30-stat697): Is the term query, as in PROC SQL query, supposed to refer to also asking a question, as if we are asking a question/making a request to retrieve data?
- Answer (mpena30-stat697): Yes, query means a request for data or information from a database table.



[Course Textbook, Chapter 1]
* Question (mpena30-stat697): Is the report output from using the SELECT statement under PROC SQL much different than a snapshot of what the table would look like if you used CREATE TABLE?



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): What happens if the clauses in the PROC SQL SELECT statement are not in the correct order?



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): Does SAS ever break TITLE or FOOTNOTE statements into more than one line if it is too long? Or is that decison always up to us to see where to best break a line into more than one statements?



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): If one column is specified in a summary function, will the result be a table with just one value for the whole column specified?
- Answer (mpena30-stat697): A single value for the entire table is calculated when no groups are specified.



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): When the PROC SQL must remerge data and the SAS log produces a notification that the query requires remerging, is any additional action needed or does SAS automatically perform the two passes/remarging?



[summarize-data-using-sql Week 2 SAS Recipe]
* Question (mpena30-stat697): Would would be simpler to use the other SAS procs that the PROC SQL queries are imitating?



[print-to-log-with-macro-variables Week 2 SAS Recipe]
* Question (mpena30-stat697): The %put statement seems useful to store values but the period doesn't change the meaning of the statement here. Does always including the period depend on the user's preference?




***



# Recipes Exploration Results



```


* Recipe: summarize-data-using-sql ;

* original recipe;
proc sql outobs=3;
	select *
	from sashelp.iris
	;
quit;

proc sql outobs=5 number;
	select *
	from sashelp.irisorder by SepalLength
	;
quit;

proc sql;
	select species, count(*) as Number_of_Irises
	from sashelp.iris
	group by Species
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
	
	




* Recipe: print-to-log-with-macro-variables ;

* original recipe;
%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put This is an example of &=recipeName.;
%put _user_;




```
