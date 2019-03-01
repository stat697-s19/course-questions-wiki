# Questions about Problems and Recipes



[Chapter 4, Question 1]
* Question (mstafford5-stat697): How can you specify using EXCEPT, UNION, or INTERSECT statements on columns other than the first column? Or do tables only combine vertically from the first ID column?



[Chapter 4, Question 2]
* Question (mstafford5-stat697): How can you add a column that counts the duplicate columns? Are there alternative methods of handling duplicates? 



[Chapter 4, Question 4]
* Question (mstafford5-stat697): Is there a standard naming procedure for tables made from different types of joins?



[Chapter 4, Question 5]
* Question (mstafford5-stat697): Is the CORRESPONDING term relevant in other applications besides merging tables vertically?



[Chapter 11, Question 1]
* Question (mstafford5-stat697): What are the most common syntax and other errors that occur when running macros?



[Chapter 11, Question 3]
* Question (mstafford5-stat697): Why is macros syntax different from regular sas syntax?



[Chapter 11, Question 10]
* Question (mstafford5-stat697): Where are there bottlenecks in the process of running macros that slow a program down?




[Advanced-dry-programming-pattern Week 4 SAS Recipe]
* Question (mstafford5-stat697): Can macros parameters that are already set such as 'outputLibrary=Work' be revised when the macros is called?



[Advanced-dry-programming-pattern Week 4 SAS Recipe]
* Question (mstafford5-stat697): Are there sas procedures or functions where utilizing macros wouldn't be efficient for large calculations?



***



# Recipes Exploration Results




```
* Recipe: advanced-dry-programming-pattern ;

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
%splitDatasetAndPrintMeans(sashelp, cars, make)

*I edited the dataset to see how it generalizes, and found the summary stats for the different make of cars in the cars dataset;


```
