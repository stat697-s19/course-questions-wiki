
# Questions about Problems and Recipes



[Week4 Reflection - TB Ch4, Question 1]


* Question (mgao10-stat697): What is the difference between union and intersect 


[Week4 Reflection - TB Ch4, Question 2]


* Question (mgao10-stat697): Why there is a restriction for keyword All


[Week4 Reflection - TB Ch4, Question 3]


* Question (mgao10-stat697): what is outer union?


[Week4 Reflection - TB Ch4, Question 4]


* Question (mgao10-stat697): What is coalesce and how does it work?


[Week4 Reflection - TB Ch11, Question 5]


* Question (mgao10-stat697): What is #MEND statment?


[Week4 Reflection - TB Ch11, Question 6]


* Question (mgao10-stat697): is it correct to use %if &vars = %then %do statement;?


[advanced-dry-programming-pattern Week 3 SAS Recipe]


* Question (mgao10-stat697):how to control interation list with Do loop?



***



# Recipes Exploration Results



```


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
