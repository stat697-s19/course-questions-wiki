
# Questions about Problems and Recipes



[Course Textbook Chapter 3, Problem 4]
* Question (yli110-stat697): What are the two valid formats to write PROC SQL inner join?



[Course Textbook Chapter 3, Problem 6]
* Question (yli110-stat697): What are the requirements of tables when you want to inner join rows from two tables?



[Course Textbook Chapter 3, Problem 8]
* Question (yli110-stat697): What are the main difference between DATA MERGE BY and PROC SQL full join? How can you make these two to give same output?



[Course Textbook Chapter 3, Problem 10]
* Question (yli110-stat697): What are the necessary conditions to use table aliases?



[Course Textbook Chapter 9, Problem 1]
* Question (yli110-stat697): How do you reference a macro variable in the TITLE statement?



[Course Textbook Chapter 9, Problem 2]
* Question (yli110-stat697): What will happen if you have double quotation masks in the %LET statement?



[Course Textbook Chapter 9, Problem 3]
* Question (yli110-stat697): What are the four types of tokens recognized by SAS word scanner?
- Answer (yli110-stat697): literals, names, numbers and special characters.



[dry-programming-pattern Week 3 SAS Recipe]
* Question (yli110-stat697): What is a macro shell and what's the advantage of it?



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
        %put &=currentSpecies.; /*print the value to log for debugging*/
        data iris_&currentSpecies.;
            set sashelp.iris;
            if species = "&currentSpecies.";
        run;
        proc means n nmiss min q1 median q3 maxdec=1;
        run;
    %end;
%mend;
%splitDatasetAndPrintMeans



```