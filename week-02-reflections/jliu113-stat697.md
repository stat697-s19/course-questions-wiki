
# Questions about Problems and Recipes


[Course Structure Quiz, Problem 1]
* Question (jliu113-stat697): What you can do with “PROC SQL”?
- Answer (jliu113-stat697): retrieve data from and manipulate SAS tables; add or modify data values in a table; add, modify, or drop columns in a table; create tables and views; join multiple tables(whether they contain columns with the same name); generate reports.


[Course Structure Quiz, Problem 2]
* Question (jliu113-stat697): How “PROC SQL is different from other SAS procedures”?
- Answer (jliu113-stat697): “PROC SQL” include clauses(SELECT);  “PROC SQL” step does not require a RUN statement; “PROC SQL” need another “PROC” step to stop;



[Course Structure Quiz, Problem 3]
* Question (jliu113-stat697):When using SELECT to create new columns, are the new columns existing only for the duration of the query or forever?
- Answer (jliu113-stat697): only for the duration of the query, unless a table or a view is created.



[Course Structure Quiz, Problem 4]
* Question (jliu113-stat697): Does “WHERE” function use for columns or rows?  
- Answer (jliu113-stat697): Any columns from the specified tables.


[Course Structure Quiz, Problem 5]
* Question (jliu113-stat697): How could we change the “ORDER BY” descending order?
- Answer (jliu113-stat697): adding “DESC”, for example, order by jobcode desc;.




[Course Structure Quiz, Problem 6]
* Question (jliu113-stat697): Is there other ways to reference a column in the “SELECT” clause list?
- Answer (jliu113-stat697): Yes, using the column’s position replace the name.



[Course Structure Quiz, Problem 7]
* Question (jliu113-stat697): How could students debug the SQL processor?
- Answer (jliu113-stat697):  Using “FEEDBACK” with “SELECT*”.

[Course Structure Quiz, Problem 8]
* Question (jliu113-stat697): How could students limit the max number of the rows displayed?
- Answer (jliu113-stat697):  “OUTOBS”, for example, PROC SQL OUTOBS = 6; .


[Course Structure Quiz, Problem 9]
* Question (jliu113-stat697): How many type of subqueries?
- Answer (jliu113-stat697):  Noncorrelated and correlated.



[summarize data Week 2 SAS Recipe]
* Question (jliu113-stat697): How can we get the number of row for a specified column?
- Answer (jliu113-stat697):   “SELECT columnname, count(*) as AA;”


[print-to-log-with-macro-variables Week 2 SAS Recipe]
* Question (jliu113-stat697): What’s the meaning of these functions; %, & and =?






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
