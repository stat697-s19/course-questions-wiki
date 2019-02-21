
# Questions about Problems and Recipes


[Week4 Reflection - TB Ch4, Question 1]
* Question (lgao7-stat697): Q4-How does OUTER UNIOR different with UNION CORR?  



[Week4 Reflection - TB Ch4, Question 2]
* Question (lgao7-stat697): Q5- Why does keyword CORRESPONDING cannot be used with ALL?



[Week4 Reflection - TB Ch11, Question 3]
* Question (lgao7-stat697): Q1-“%MACRO statement must always be paired with %MEND” Does %MEND same as %QUIT?



[Week4 Reflection - TB Ch11,  Question 4]
* Question (lgao7-stat697): Q3- Why is there no common needed to operate two variables? 



[Week4 Reflection - TB Ch4, Question 5]
* Question (lgao7-stat697): Q10- Why do we not need to pair a %MEND statement with %MACRO in this case?



[Week4 Reflection - TB Ch11, Question 6]
* Question (lgao7-stat697):  CH11-How does MLOGIC and MPRINT different  when debugging macros in SAS?



[Week4 Reflection - TB Ch11, Question 7]
* Question (lgao7-stat697):  CH11-How does UNION modified by keywords ALL and CORR?



[Week4 Reflection - SAS Recipe 1, Question 1]
* Question (lgao7-stat697): What does the semicolon means when merging tables in proc sql, such that select distinct T1 into :T3 by “|”? 




***



# Recipes Exploration Results



```

* [SAS Recipe 1: advanced-dry-programming-pattern (LG)];

*Example;

options
	mcompilenote=all
	mprint
	symbolgen
;
%macro splitDatasetAndPrintMeans(
	inputLibrary,
	dsn,
	column,
	outputLibrary=Work
);

	%let callDate = %sysfunc(today(), weekdate.);

	proc sql noprint;
		select
			distinct &column. into :iterationList separated by "|"
            from &inputLibrary..&dsn.  
		;
	quit;

	%let numberOfIterations = %sysfunc(countw(&iterationList., |));

	%do i = 1 %to %eval(&numberOfIterations.);
		%let currentIteration = %scan(&iterationList., &i., |);
		data &outputLibrary..&dsn._&currentIteration.;
			set &inputLibrary..&dsn.;
			if &column. = "&currentIteration.";
		run;
		footnote "Created on &CallDate. using dataset &syslast.";
		proc means n nmiss min q1 mnedian q3 max maxdec=1;
		run;
	%end;
%mend;
%splitDatasetAndPrintMeans(
	sashelp,
	iris,
	species
)


* three proc means step, one for each dataset;
* begin with three global system options;

