# Questions about Problems and Recipes

[Chapter 4, Problem 1]
* Question (mresendiz3-stat697): Is there an order of precedence for set operators?
* Answer (mresendiz3-stat697): Yes. Keeping in mind that parenteses override other set operators INTERSECT is always evaluated first and OUTER UNION, UNION, and EXCEPT all have the same level of precedence. 


[Chapter 4, Problem 2]
* Question (mresendiz3-stat697): What does the ALL keyword do?
* Answer (mresendiz3-stat697): The ALL keyword makes one pass through the data and doesn't remove duplicate rows and cannot be used with OUTER UNION. 


[Chapter 4, Problem 5]
* Question (mresendiz3-stat697): What does the CORR (CORRESPONDING) keyword do?
* Answer (mresendiz3-stat697): The CORR keyword overlays columns by name (not position) and when used with EXCEPT, INTERSECT, or UNION it excludes columns with different names. When CORR is used with OUTER UNION it overlays columns with the same name and displays the columns with different names without overlaying. 


[Chapter 11, Problem 1]
* Question (mresendiz3-stat697): What type of macro is most efficient and why?
* Answer (mresendiz3-stat697): Macros come in 3 types: name style, statement style, and command style. Name style macros are more efficient because they always begin with a percent sign which directs the word scanner to pass the token to the macro processor. 


[Chapter 11, Problem 3]
* Question (mresendiz3-stat697): What if the macro definition has both the PARMBUFF option and a set of parameters?
* Answer (mresendiz3-stat697): The macro invocation causes the parameters to receive values and the entire invocation list of values to be assigned to SYSPBUFF. 


[Chapter 11, Problem 5]
* Question (mresendiz3-stat697): What is a the PARMBUFF option?
* Answer (mresendiz3-stat697): The PARMBUFF option can be used in a macro definition to create a macro that can accept different types of parameters at each invocation. It assigns the entire list of parameter values in a macro call including parentheses in the name-style invocation. 


[Chapter 11, Problem 10]
* Question (mresendiz3-stat697): What is the %GLOBAL statement?
* Answer (mresendiz3-stat697): The %GLOBAL statement creates one or more macro variables in the global symbol table while assigning null values to them, can be used either inside or outisde a macro definition, and it has no effect on variables that are already in the global symbol table. 


[sas_recipe-basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mresendiz3-stat697): Is there anything being done to make macro scripts easier to understand?

***

# Recipes Exploration Results

```
*******************************************************************************;
**************** 80-character banner for column width reference ***************;
* set window width to banner width to calibrate line length to 80 characters  *;
*******************************************************************************;

*******************************************************************************;
* advanced-dry-programming-pattern ;
*******************************************************************************;
/*
Scenario: We wish to repeat a set of steps, each time changing the value of a
single variable whose values are determined in a data-driven manner.

Approach: Inside a macro shell, use an implicitly defined macro array and the
macro-version of a do-loop.

Recipe:
%macro <macro-name>(<parameter list needed for macro>);
    <steps to determine the list of values to loop over>

    %do i = 1 %to <number of elements in the list to loop over>;
        <steps to repeat for each element in the list to loop over>
    %end;
%mend;
%<macro-name>(<values for parameters>)

*/

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
	%let callDate= %sysfunc(today(),weekdate.);

	proc sql noprint;
			select
				distinct &column. into : iterationList separated by "|"
			from 
				&inputLibrary..&dsn.
			;
		quit;

		%let numberOfIterations=%sysfunc(countw(&iterationList., |));

		%do i=1 %to %eval(&numberOfIterations.);
			%let currentIteration = %scan(&iterationList., &i., |);
			data &outputLibrary..&dsn._&currentIteration.;
				set &inputLibrary..&dsn.;
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
			
