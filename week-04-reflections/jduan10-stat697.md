
# Questions about Problems and Recipes



[Course Textbook Chapter 4, Problem 1] 
- Question (jduan10-stat697): In a set operation that uses the EXCEPT operator, does the order in which the tables are listed in the SELECT statement matter?



[Course Textbook Chapter 4, Problem 2] 
- Question (jduan10-stat697): What will the INTERSECT operator display if the keywords ALL and CORR are used together?



[Course Textbook Chapter 4, Problem 3] 
- Question (jduan10-stat697): How to define common rows in two table?



[Course Textbook Chapter 4, Problem 4] 
- Question (jduan10-stat697): How many SELECT clause can we write in PROC SQL?



[Course Textbook Chapter 4, Problem 5] 
- Question (jduan10-stat697): When tables have a same-named column, does the PROC SQL outer union produce the same output?



[Course Textbook Chapter 11, Problem 1] 
- Question (jduan10-stat697): How can we store a complied macro?



[Course Textbook Chapter 11, Problem 3] 
- Question (jduan10-stat697): When we call a macro, how can we see the text sent to compiler?



[Week 4 SAS Recipe: advanced-dry-programming-pattern] 
- Question (jduan10-stat697): How many vertical pipes can we use in SQL?





***



# Recipes Exploration Results



```


*Recipe: advanced-dry-programming-pattern;

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
