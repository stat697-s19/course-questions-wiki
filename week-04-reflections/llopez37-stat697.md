
# Questions about Problems and Recipes

[Course Textbook Chapter 4, Problem 1]
- Question (llopez37-stat697): Is the name of the column taken into consideration if select is not utilized?
- Answer(llopez37-stat660): It appears to be the case but leverages it from the first data set

[Course Textbook Chapter 4, Problem 2]
- Question (llopez37-stat697): Does this help circumvent having to dedupe our data since it makes an extra pass for duplicates?

[Course Textbook Chapter 4, Problem 4]
- Question (llopez37-stat697) How would we overlay the columns with outer union?

[Course Textbook Chapter 4, Problem 5]
- Question (llopez37-stat697): Could you use corresponding to be more specific?
- Answer (llopez37-stat697) It seems that for this case it is used alone or with ALL.

[Course Textbook Chapter 11, Problem 3]
- Question (llopez37-stat697) Is symput able to use macro language along with its other uses or do we need to differentiate?

[Course Textbook Chapter 11, Problem 5]
- Question (llopez37-stat697):   How come the multiple ampersands do not cause an error and is this the only function that does this?

[Course Textbook Chapter 11, Problem 10]
- Question (llopez37-stat697): How does symput differ based off the data step or sql? 
- Answer (llopez37-stat697) It appears to do a conversion of some sorts

[Advanced Dry Week 3 SAS Recipe]
- Question (llopez37-stat697): Are the macro do loops more efficient? 




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
