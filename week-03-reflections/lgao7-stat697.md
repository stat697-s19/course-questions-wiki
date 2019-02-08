
# Questions about Problems and Recipes


[Week3 Reflection - TB Ch3, Question 1]
* Question (lgao-stat697): CH3 - Q1- How to identify what’s join, set operation, operator in POC SQL?



[Week3 Reflection - TB Ch3, Question 2]
* Question (lgao-stat697): CH3 - why does a macro variable is always a character string? 



[Week3 Reflection - TB Ch3, Question 3]
* Question (lgao-stat697): CH9 Q3 - What does options function do in macro environment? 



[Week3 Reflection - TB Ch3, Question 4]
* Question (lgao-stat697): CH9 Q5 - What does “*” referring to when in Macro environment? Like the quotation marks?  



[Week3 Reflection - TB Ch3, Question 5]
* Question (lgao-stat697): CH9 - Q9 - Based on the answers, it seems like when returning the macro variables, there is no formatting of the spacing, how to make it more readable with space or return in a new line? 



[Week3 Reflection - TB Ch9, Question 6]
* Question (lgao-stat697):  CH10 - Q4 what does the double / triple & of the macro variable do?



[Week3 Reflection - TB Ch9, Question 7]
* Question (lgao-stat697):  CH3 - To reference the macro variable in a title, we must use double quotation marks , while in SAS standard precede we can use either single or double quotations. To make life easier, would it be possible to always use double quotation marks ?



[Week3 Reflection - SAS Recipe 1, Question 1]
* Question (lgao-stat697): Why do we used the quotation marks to ensure the Marco variable is going to be treated as string, while macro variable is always be string variable? 




***



# Recipes Exploration Results



```

* [SAS Recipe 1: Summarize-data-using-sql (LG)];

*Example;

options mprint;
%macro splitDatasetAndPrintMeans;
	%let species1 = Setosa;
	%let species2 = Versicolor;
	%let species3 = Virginica;
	%put _user_;
	%put;

	%do i = 1 %to 3;  *macro version of the statement;
		%let currentSpecies = &&species&i.;  *determine which macro variables;
		%put &=currentSpecies.;
		data iris_&currentSpecies.;
			set sashelp.iris;
			if species = "&currentSpecies."; * quotemarks to ensure variable treated as string;
		run;
		proc means n nmiss min q1 median q3 maxdec=1;
		run;
	%end;
%mend;
%splitDatasetAndPrintMeans



```
