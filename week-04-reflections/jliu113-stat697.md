
# Questions about Problems and Recipes



[Course Textbook Ch11, Problem 1]
* Question (jliu113-stat697): Write the SAS system option that issues a note to the SAS log when a macro has completed compilation.?
- Answer (jliu113-stat697): options mcompilenote = all;



[[Course Textbook Ch11, Problem 2]
* Question (jliu113-stat697): Write a call to invoke the macro program named totsales.?
- Answer (jliu113-stat697):%totsales. You specify the name of the macro, preceded by a percent sign.



[[Course Textbook Ch11, Problem 3]
* Question (jliu113-stat697):Will the macro definition below produce an error when submitted?
             %macro test;
             this is a test macro
             %mend test;
- Answer (jliu113-stat697): The correct answer is no. When the test macro is submitted there will be no compile errors from the macro processor. During compilation, the macro processor checks only macro-level statements. The two macro-level statements, %MACRO and %MEND, are syntactically correct.



[[Course Textbook Ch11, Problem 4]
* Question (jliu113-stat697): Where are macro parameters stored?  
- Answer (jliu113-stat697): local symbol table.



[[Course Textbook Ch11, Problem 5]
* Question (jliu113-stat697): Are expressions in %IF statements evaluated when the macro is compiled?
- Answer (jliu113-stat697): No, Expressions in %IF statements are not evaluated until the macro is executed.



[[Course Textbook Ch11, Problem 6]
* Question (jliu113-stat697): Should you typically turn off the MLOGIC option, along with the MPRINT option and the SYMBOLGEN option, when a program that uses SAS macro language is in production mode?
- Answer (jliu113-stat697): Yes, When you're working with a program that uses SAS Macro Language you should typically turn the MLOGIC, MPRINT, and SYMBOLGEN options on for development and debugging purposes and off when the program is in production mode.



[[Course Textbook Ch4, Problem 7]
* Question (jliu113-stat697): How could students CORR in PROC SQL?
- Answer (jliu113-stat697):  When used with EXCEPT, INTERSECT, and UNION, removes any columns that do not have the same name in both tables; When used with OUTER UNION, overlays  same-named columns and displays columns that have nonmatching names without overlaying.                                                                                                                                                                                                                                          



[Dry programming Week 4 SAS Recipe]
* Question (jliu113-stat697): What is the  %eval function means?
- Answer (jliu113-stat697):  Make the variable into numerical and suitable for the do loop.



***



# Recipes Exploration Results

* Recipe: Dry programming ;

```


Options

    mcompilenote= all
	mprint
	symbolgen
;
%macro splitDatasetAndPrintMeans(
    inputLibrary, 
	dsn,
	column,
	outputLibrary= Work
);
    %let callDate= %sysfunc(today(), weekdate.);

	proc sql noprint;
	    select
		    distinct &column. into: iterationList separated by "|"
		from &inputLibrary..&dsn.
		;
	quit;

	%let numberOfIterations = %sysfunc(countw(&iterationList., |));

	%do i=1 %to %eval(&numberOfIterations.); 
              /* %eval make the () into Num variable to suitable for do loop*/
        %let currentIteration = %scan(&iterationList.,&i.,|);
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
