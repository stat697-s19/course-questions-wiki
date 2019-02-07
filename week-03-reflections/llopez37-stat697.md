
# Questions about Problems and Recipes

[Course Textbook Chapter 3, Problem 6]
- Question (llopez37-stat697): Is it possible to do this while also switching the column to the proper type of variable? 
- Answer(llopez37-stat660): It seems it is better to do this before attempting to join the data sets.

[Course Textbook Chapter 3, Problem 10]
- Question (llopez37-stat697): Is table aliases only required in order to reference variables of the dataset?

[Course Textbook Chapter 9, Problem 1]
- Question (llopez37-stat697) Is this only the case for the macro variable when it has been run within SAS?

[Course Textbook Chapter 9, Problem 3]
- Question (llopez37-stat697): How would you go about getting the options for the macro variable you are using? 
- Answer (llopez37-stat697) it appears symbolgen would be what allows us to see the options for macros

[Course Textbook Chapter 9, Problem 8]
- Question (llopez37-stat697) What is the difference between literal and expression? 

[Course Textbook Chapter 10, Problem 4]
- Question (llopez37-stat697):  Why is run utlized in the middle of the data step? 

[Course Textbook Chapter 10, Problem 7]
- Question (llopez37-stat697): Would we call the macro variable the same way with an &?
- Answer (llopez37-stat697) It appears this is the case, this is only changing the method in which we create the macro but not how we call it

[Basic Dry Week 3 SAS Recipe]
- Question (llopez37-stat697): Does this change the macro variables or does it change based off the do loop utilizing each macro variable that falls into the parameters?



***



# Recipes Exploration Results



```
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
