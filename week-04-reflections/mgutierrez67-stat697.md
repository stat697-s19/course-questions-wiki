
# Questions about Problems and Recipes

[Ch.4, Problem 1]
* Question (mgutierrez67-stat697): Is there a way to overlay the column of the second table instead without changing the order the tables are referenced in the select statement?

[Ch.4, Problem 2]
* Question (mgutierrez67-stat697): Should an outer union or union all be used if the goal is to vertically join two tables with the assumption that both tables contain the same columns?

[Ch.4, Problem 4]
* Question (mgutierrez67-stat697): What are some practical advantages for overlaying columns? 

[Ch.4, Problem 4]
* Question (mgutierrez67-stat697): Doesn’t overlaying columns increase the possibility of assigning values from a different column unintentionally when using one of the set operators?

[Ch.11, Problem 1]
* Question (mgutierrez67-stat697): Other than readability, what are some cons of not including the macro-name in a %MEND statement?

[Ch.11, Problem 5]
* Question (mgutierrez67-stat697): Is the macro program comparable to a user created function in other languages (i.e. creating a function, calling function etc.)?
- Answer (mgutierrez67-stat697): Yes, per weekly recipe video, but there are differences in how the program is ran and returned (i.e. macros do not have a return value like other languages). 

[Ch.11, Problem 10]
* Question (mgutierrez67-stat697): Is it best and/or common practice to include a MCOMPILENOTE when a program containing a macro is ran?

[advanced-dry-programming-pattern Week 4 SAS Recipe]
* Question (mgutierrez67-stat697): Should symbolgen always be used when running a program with macros? Is it good practice to review the log after using the symbolgen, even if there are numerous macro references and can potentially become time consuming?


***



# Recipes Exploration Results


```


* Recipe: advanced-dry-programming-pattern;

* original recipe;

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

    %let callDate = %sysfunc(today(),weekdate.);

    proc sql noprint;
        select
            distinct &column. into :iterationList separated by "|"
            from &inputLibrary..&dsn.
        ;
    quit;

    %let numberOfIterations = %sysfunc(countw(&iterationList.,|));

    %do i = 1 %to %eval(&numberOfIterations.);
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
%splitDatasetAndPrintMeans(sashelp, iris, species)


*modified the code by removing the three global system options to compare the log output with the program that retains the global options
*the log with the global system options is much more informative and allows the user to follow how macro variables were handled/assigned
*even though it global system options add additional insight, it might become more time consuming and daunting to review as the number of macros to review increases

%macro splitDatasetAndPrintMeans(
    inputLibrary,
    dsn,
    column,
    outputLibrary=Work
);

    %let callDate = %sysfunc(today(),weekdate.);

    proc sql noprint;
        select
            distinct &column. into :iterationList separated by "|"
            from &inputLibrary..&dsn.
        ;
    quit;

    %let numberOfIterations = %sysfunc(countw(&iterationList.,|));

    %do i = 1 %to %eval(&numberOfIterations.);
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
%splitDatasetAndPrintMeans(sashelp, iris, species)


```
