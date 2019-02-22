
# Questions about Problems and Recipes



[Chapter 4, Problem 1]
- Question (mphan12-stat697): What does are the results of a INTERSECT join?
- Answer (mphan12-stat697): Similar to inner join, INTERSECT produces rows that are common to both tables.



[Chapter 4, Problem 2]
- Question (mphan12-stat697): Why does the keyword CORRESPONDING do?
- Answer (mphan12-stat697): It overlays columns that have the same name in both tables. When used with EXCEPT, INTERSECT, and UNION, CORR suppresses columns that are not in both tables.



[Chapter 4, Problem 3]
- Question (mphan12-stat697): what is outer union? 
- Answer (mphan12-stat697): All rows from the left table are returned, and if there are no matches to the right table, then missing values are populated.



[Chapter 4, Problem 4]
- Question (mphan12-stat697): What is COALESCE and how does it work?
- Answer (mphan12-stat697): COALESCE is used to fill in the Null values when two variables with the same but from different tables are joined.



[Chapter 11, Problem 5]
- Question (mphan12-stat697): Is the %MEND statement required for every %MACRO statement?
- Answer (mphan12-stat697): Yes, it is similar to data and run statements.



[Chapter 11, Problem 6]
- Question (mphan12-stat697): What does the MLOGIC do?
- Answer (mphan12-stat697): The MLOGIC causes the macro processor to trace its execution and to write the trace information to the SAS log. This option is a useful debugging tool.



[advanced-dry-programming-pattern Week 4 SAS Recipe]
- Question (mphan12-stat697): When is it ideal not to use the MPRINT statement?
- Answer (mphan12-stat697): When there are passwords encrypted in a macro statement.



***



# Recipes Exploration Results



```


* Recipe: advanced-dry-programming-pattern;
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



```
