
# Questions about Problems and Recipes

[Ch.3, Problem 4]
* Question (mgutierrez67-stat697): When should an inner join using the keyword "inner join" be used versus the non-keyword inner join approach?

[Ch.3, Problem 6]
* Question (mgutierrez67-stat697): Can the SAS put or input function be used to convert non-matching data types in a proc SQL join statement?
- Answer (mgutierrez67-stat697): I was unable to find a specific answer confirming the use of either put or input SAS functions to convert a data type in a SQL join statement, but from what I read, the cast and/or convert SQL function will be able to accomplish this.

[Ch.3, Problem 10]
* Question (mgutierrez67-stat697): Is it good practice to create an alias for summary functions that is more descriptive and intuitive, even though it is not required?

[Ch.9, Problem 1]
* Question (mgutierrez67-stat697): What are some alternatives if we need to include a macro variable in a dataline?
- Answer (mgutierrez67-stat697): Based on my research, the resolve function can be one approach to use macro variables in dataline.

[Ch.9, Problem 1]
* Question (mgutierrez67-stat697): Can the format of a macro variable be updated (i.e. changing the date format of a macro variable)?
- Answer (mgutierrez67-stat697): Yes, in the particular example above, the date format of a macro variable can be revised using the macro variable %sysfunc and INPUTN function.

[Ch.9, Problem 5]
* Question (mgutierrez67-stat697): Can SAS macro variables syntax be used in proc sql queries?
- Answer (mgutierrez67-stat697): Yes, proc sql statements can reference SAS macro variables. 

[Ch.10, Problem 1]
* Question (mgutierrez67-stat697): Should SYMPUT be used everytime in a data step regardless if the macro variable is referenced or not in a conditional statement where order of operation does not matter?

[basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mgutierrez67-stat697): Do all special functions or operations such as performing a do loop need to have a percent symbol when it is in a macro?

[basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mgutierrez67-stat697): Are there alternative methods for getting the same output without using the rescan method for this particular example or is this the recommended and most efficient approach?

***



# Recipes Exploration Results


```


* Recipe: print-to-log-with-macro-variables ;

* original recipe;
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

*modified the program to utilize the macro variables and loop in a proc sql query 
*the proc sql step was able to process the SAS macro variables assigned in the loop

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

		proc sql;
			select * 
			from sashelp.iris
			where species = "&currentSpecies.";
		quit;
    %end;
%mend;
%splitDatasetAndPrintMeans

```
