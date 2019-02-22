
# Questions about Problems and Recipes



[Course Textbook, Chapter 4]
* Question (mpena30-stat697): Can two columns from two different tables be overlaid despite having different data types? For example, a categorical and numerical column? 
- Answer (mpena30-stat697): Yes, if the columns to be overlaid do not have the same data types a warning message will be produced in the SAS log.



[Course Textbook, Chapter 4]
* Question (mpena30-stat697): Can the CORR keyword also be used as a method for removing duplicate-named coulmns in the creation of a new joined table?



[Course Textbook, Chapter 4] 
* Question (mpena30-stat697): Using CORR with EXCEPT chooses just the columns that have the same name, then deletes the rows in those columns that are unique to the first table. Is there a way to have this process reversed, where first only the rows unique to the first table are choosen then columns wihtout the same name are removed?



[Course Textbook, Chapter 4]
* Question (mpena30-stat697):  What would be an example of a case where using the OUTER UNION set operator alone would be desired, creating a joined table where none of the columns are overlayed?



[Course Textbook, Chapter 11]
* Question (mpena30-stat697): What is the %MEND statement at the end of a macro program supposed to mean?



[Course Textbook, Chapter 11]
* Question (mpena30-stat697): Does it matter where in a macro definition a macro comment statement is placed or are there any order restrictions?



[Course Textbook, Chapter 11]
* Question (mpena30-stat697): What is the function of the automatic macro variable SYSPBUFF when using the PARMBUFF option?
- Answer (mpena30-stat697): The invocation list of values that the parameters receive are assigned to this macro variable.



[advanced-dry-programming-pattern-edited Week 4 SAS Recipe]
* Question (mpena30-stat697): Is using the veritcal pipe (|) to seperate distinct values the only way to do this? is there another widely accepted symbol that serves the same purpose of separating values listed?




***



# Recipes Exploration Results



```


* Recipe: advanced-dry-programming-pattern-edited ;

* original recipe;
options
	mcompilenote=all
	mprint
	symbolgen
;
%macro  splitDatasetAndPrintMeans (
	inputLibrary,
	dsn,
	column,
	outputLibrary=Work
);
	%let callDate = %sysfunc(today(), weekdate.);
	
	proc sql noprint;
		select
			distinct &column. into :iterationList seperated by "|"
		from 
			&inputLibrary..&dsn.
		;
	quit;
	
	%let numberOfIterations = %sysfunc(countw(&iterationList., |));
	
	%do i = 1 %to %eval(&numberOfIterations.);
		%let currentIteration = %scan(&iterationList., &i., |);
		data &outputLibrary..&dsn._&currentIteration.;
			set &inputLibrary..&dsn.;
			if &column.= "&currentIteration.";
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
