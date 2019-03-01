
# Questions about Problems and Recipes

[Chapter 3, Problem 4]
* Question (mresendiz3-stat697): Can the inner join syntax compare across data types?
* Answer (mresendiz3-stat697): Use inner join with columns that have the same data type. The columns don't necessarily need to have the same name. 


[Chapter 3, Problem 6]
* Question (mresendiz3-stat697): What is necessary for an inner join to be processed successfully?
* Answer (mresendiz3-stat697): An inner join needs to have a WHERE clause that has the same data type across columns and may have different numbers of columns and unsorted rows. 


[Chapter 3, Problem 8]
* Question (mresendiz3-stat697): Can the coalesce function work with different data types? 


[Chapter 9, Problem 1]
* Question (mresendiz3-stat697): What types of macro variables are there and how can we reference them?
* Answer (mresendiz3-stat697): There are two types of macro variables: automatic and user-defined. They can be referenced and defined anywhere in a SAS program but cannot be referenced within data lines. 


[Chapter 9, Problem 4]
* Question (mresendiz3-stat697): What is necessary to define a macro variable?
* Answer (mresendiz3-stat697): The %LET statement is used to define a macro variable where quotation marks after the "=" sign is not needed unless the user wants to have them stored as part of the value. 


[Chapter 10, Problem 1]
* Question (mresendiz3-stat697): What is a SYMPUT routine?
* Answer (mresendiz3-stat697): The SYMPUT routine creates multiple macro variables within one DATA step without having to change a %LET statement and without having to resubmit the DATA step to assign a new value to our macro variables. We can update the same macro variable and create related macro variables all in one DATA step. 


[Chapter 10, Problem 7]
* Question (mresendiz3-stat697): How do we create a macro variable during a PROC SQL step?
* Answer (mresendiz3-stat697): Use the INTO clause of the SELECT statement as such:  SELECT  data details; INTO: data_name;.



[sas_recipe-basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mresendiz3-stat697): If creating macro variables and updating them in SAS is so efficient why do we still bother with do-loops?



# Recipes Exploration Results

```

*******************************************************************************;
**************** 80-character banner for column width reference ***************;
* set window width to banner width to calibrate line length to 80 characters  *;
*******************************************************************************;

*******************************************************************************;
* basic-dry-programming-pattern ;
*******************************************************************************;
/*
Scenario: We wish to repeat a set of steps, each time changing the value of a
single parameter.

Approach: Inside a macro shell, use an implicitly defined macro array and the
macro-version of a do-loop.

Recipe:
%macro <macro-name>;
    %let <macro-variable-name>1 = <value-1>;
    %let <macro-variable-name>2 = <value-2>;
    ...
    %let <macro-variable-name>n = <value-n>;

    %do i = 1 %to n;
        <code referencing &&<macro-variable-name>&i.>
    %end;
%mend;
%<macro-name>

*/

*Example;

options mprint; 
%macro splitDatasetAndPrintMeans;
	%let species1=Setosa;
	%let species2=Versicolor;
	%let species3=Virginica;
	%put _user_;
	%put;

	%do i = 1 %to 3; 
		%let currentSpecies=&&species&i.;
		%put &=currentSpecies.;
		data iris_&currentSpecies.;
			set sashelp.iris;
			if species = "&currentSpecies.";
		run;
		proc means n nmiss min q1 mean q3 maxdec=1;
		run;
	%end;
%mend;
%splitDatasetAndPrintMeans

```
