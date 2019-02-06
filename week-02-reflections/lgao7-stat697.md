
# Questions about Problems and Recipes



[Week2 Reflection - TB Ch1, Question 1]
* Question (lgao-stat697): Does “GE” (same as “<=“) only works with PROC SQL environment? Or it is a comment use in SAS?



[Week2 Reflection - TB Ch1, Question 2]
* Question (lgao-stat697): Q2 - Why are there only two statements? Only count Select and From?



[Week2 Reflection - TB Ch1, Question 3]
* Question (lgao-stat697): Q3 - Is it because when a variable is appears in both tables we need to specify which table to choose from?
* Answer (lgao-stat697): Yes…Quiz question #8



[Week2 Reflection - TB Ch1, Question 4]
* Question (lgao-stat697): Q8 - Why does the GROUP BY clause changed to an ORDER BY clause if we use it without a summary function? (R will ignored this clause if missing summary function).



[Week2 Reflection - TB Ch1, Question 5]
* Question (lgao-stat697): Q9 - Why does SAS do not automatically display the table?



[Week2 Reflection - TB Ch2, Question 6]
* Question (lgao-stat697):  Q8 - why does the output is all donors who did not make a contribution in the current year?



[Week2 Reflection - TB Ch2, Question 7]
* Question (lgao-stat697): Q9 - What kind of message is going to displays when remerges data?



[Week2 Reflection - SAS Recipe 1, Question 1]
* Question (lgao-stat697): Does the proc sql runs from the bottom in this case? First execute "GROUP BY", then "COUNT(*)"?  



[Week2 Reflection - SAS Recipe, Question 2]
* Question (lgao-stat697): Does “_” underscore has any specific meaning in SAS? Such that _NULL_ means temporary variable/dataset; what does _USER_ actually means?



***



# Recipes Exploration Results



```


* [SAS Recipe 1: Summarize-data-using-sql (LG)];

* select all columns(*);
* outobs=3: output 3 observations;

*immitating proc print;
proc sql outobs=3;
	select *
	from sashelp.iris
	;
quit;


* data sort by SapalLength in ascending order;

*immitating proc sort and proc print;
proc sql outobs=5 number;
	select *
	from sashelp.iris
	order by SepalLength
	;
quit;


proc sql;
	*immitating proc freq;
	select Species, count(*) as Number_of_Irises
	from sashelp.iris
	group by Species
	;
	*immitating proc means (didnt indicate a "quit", proc sql cont.);
	select 
		Species
		,min(SepalLength) as Minimum_Sepal_Length
		,median(SepalLength) as Median_Sepal_Length
		,max(SepalLength) as Maximum_Sepal_Length
	from
		sashel.iris
	group by
		Species
	;
quit;

 



* ———————————————————;



* [SAS Recipe 2: print-to-log-with-macro-variables (LG)];

%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.; * printout the text;
%put This is an example of &=recipeName.; * printout the value of the MV and the value inside;
%put _user_; * print out the macro type, recipeName, and its Value;
* using the % to let SAS know this is a Macro variable;
* Macro variable is always assumed to strings;
* "&" tells SAS to start reading. The "." tells SAS to stop but optional;
* &= tells SAS to print the Name of the macro variable as well;





```
