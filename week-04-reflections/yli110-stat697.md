
# Questions about Problems and Recipes



[Course Textbook Chapter 4, Problem 1]
* Question (yli110-stat697): What will happen when set operators overlay columns that have different names?



[Course Textbook Chapter 4, Problem 2]
* Question (yli110-stat697): Why cannot ALL be used with OUTER UNION?



[Course Textbook Chapter 4, Problem 3]
* Question (yli110-stat697): Which set operator do you use when you want to output all unique rows from both tables, and the columns are overlaid by position?



[Course Textbook Chapter 4, Problem 4]
* Question (yli110-stat697): If you do not want to overlay any columns, which operator do you use?



[Course Textbook Chapter 4, Problem 5]
* Question (yli110-stat697): What set operators can be used with CORR?



[Course Textbook Chapter 11, Problem 1]
* Question (yli110-stat697): What macro statements do you use to define/start and end a macro in SAS?



[Course Textbook Chapter 11, Problem 3]
* Question (yli110-stat697): How do you call a macro with positional parameters?



[advanced-dry-programming-pattern Week 4 SAS Recipe]
* Question (yli110-stat697): What is the macro function to use when you need to return an integer value from a macrovariable?



***



# Recipes Exploration Results



```



options
	mcompilenote=all
	mprint
	symbolgen
;

%macro splitDatasetAndPrintMeans (
	inputLib,
	dsn,
	column,
	outputLib = Work
);
	%let callDate = %sysfunc(today(), weekdate.);
	proc sql noprint;
		select
			distinct &column. into :iterationList separated by "|"
		from 
			&inputLib..&dsn.
	;
	quit;

	%let numberOfInterations = %sysfunc(countw(&iterationList., |));

	%do i = 1 %to %eval(&numberOfInterations.);
		%let currentIteration = %scan(&iterationList., &i., |);
		data &outputLib..&dsn._&currentIteration.;
			set &inputLib..&dsn.;
			if &column. = "&currentIteration.";
		run;
		footnote "Created on &callDate. using dataset &syslast.";
		proc means n nmiss min q1 median q3 max maxdec=1;
		run;
	%end;
%mend;
%splitDatasetAndPrintMeans(
	sashelp,
	iris,
	species
)




```


