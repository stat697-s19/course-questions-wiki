
# Questions about Problems and Recipes


[Course Textbook Chapter 3, Problem 4] 
- Question (jduan10-stat697): What is the maximum number of tables that we can combine in a single inner join?



[Course Textbook Chapter 3, Problem 6] 
- Question (jduan10-stat697): Does two columns in JOIN require the same name?



[Course Textbook Chapter 3, Problem 8] 
- Question (jduan10-stat697): How to rename the column in SQL?



[Course Textbook Chapter 3, Problem 10] 
- Question (jduan10-stat697): Can we create a new table after JOIN function?



[Course Textbook Chapter 10, Problem 1] 
- Question (jduan10-stat697): What is the difference between DATA step merge-match and SQL?



[Course Textbook Chapter 10, Problem 2] 
- Question (jduan10-stat697): Can we use WHERE clause after ON clause?



[Course Textbook Chapter 10, Problem 4] 
- Question (jduan10-stat697): What will happen to the column in the result row that are from the unmatched row in the three types of join?



[Week 3 SAS Recipe: basic-dry-programming-pattern] 
- Question (jduan10-stat697): What is the difference between “&&” and “&” sign?




***



# Recipes Exploration Results



```


*Recipe: basic-dry-programming-pattern;

options mprint;
%macro splitDatasetAndPrintMeans;
    %let species1 = Setosa;
    %let species2 = Versicolor;
    %let species3 = Virginica;
    %put _user_;
    %put;

    %do i = 1 %to 3;
        %let currentSpecies = &&species&i.;
        %put &=currentSpecies.;
        data iris_&currentSpecies.;
            set sashelp.iris;
            if species = "&currentSpecies.";
        run;
        proc means n nmiss min q1 median q3 max maxdec=1;
        run;
    %end;
%mend;
%splitDatasetAndPrintMeans


```
