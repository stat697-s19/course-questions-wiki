
# Questions about Problems and Recipes



[Course Textbook Chapter3, Problem 1]
* Question (jliu113-stat697): Does “PROC SQL” perform a join without a condition? Does it require the two columns with the same name?
- Answer (jliu113-stat697): No, it won’t perform a join(eg: where, =) unless the columns that are compared in the join condition have the same data type. However, the two columns are not required to have the same name.



[Course Textbook Chapter3, Problem 2]
* Question (jliu113-stat697): How can students deal with same name columns r overlay columns in “PROC SQL”?
- Answer (jliu113-stat697): Two ways, the first one is to eliminate or rename the duplicate columns; the other one is to use the “COALESCE” function.



[Course Textbook Chapter3, Problem 3]
* Question (jliu113-stat697):When using SELECT to join table, how to eliminate duplicate columns?
- Answer (jliu113-stat697): Use “SELECT” statement only select several columns we need.



[Course Textbook Chapter3, Problem 4]
* Question (jliu113-stat697): When using SELECT to join table, how to rename a column by using column alias?
- Answer (jliu113-stat697): Use “SELECT” statement and “AS” to change it, eg: select one.x as ID, two.x, a, b, from sasuser.staffmaster as s.



[Course Textbook Chapter3, Problem 5]
* Question (jliu113-stat697): Which are two situation that require Table aliases use?
- Answer (jliu113-stat697): 1) a table is joined to itself ( called a self-join or reflexive join); 2) need to reference columns from same-name tables in different libraries.



[Course Textbook Chapter3, Problem 6]
* Question (jliu113-stat697): How could students get the full name(first initial and last name) from separate first name and last name columns? And age from date birth?
- Answer (jliu113-stat697): substr(firstname,1,1)  || `.` || lastname as Name, int((today()- dateofbirth)/365.25 as Age



[Course Textbook Chapter3, Problem 7]
* Question (jliu113-stat697): What is the difference between DATA step match-merge and PROC SQL?
- Answer (jliu113-stat697):  1) a join does not require that you sort the data first; a DATA step match-merge requires that the data be sorted; 2) The DATA step match-merge creates a data set whereas the PROC SQL inner join creates only a report as output; 3) a PROC SQL outer join does not overlay the two common columns by default. But we could add COALESCE into SELECT function to solve the issue.



[Course Textbook Chapter3, Problem 8]
* Question (jliu113-stat697): What is the main advantage of PROC SQL?
- Answer (jliu113-stat697):  PROC SQL joins do not require sorted or indexed tables, that the columns in join expressions have the same name. PROC SQL can use comparison operators other than the equal sign(=).



[Course Textbook Chapter3, Problem 9]
* Question (jliu113-stat697): What is the advantages to using an in-line view instead of a table in PROC SQL query?
- Answer (jliu113-stat697): 1) The complexity of the code is usually reduced, ao that the code is easier to write, and understand. 2)    In some cases, PROC SQL might be able to process the code more efficiently.



[Course Textbook Chapter9, Problem 10]
* Question (jliu113-stat697): What is the two types of macro variables?
- Answer (jliu113-stat697): 1)automatic macro variables, which are provided by SAS; 2)user-defined macro variables, whose values you create and define.



[Course Textbook Chapter9, Problem 11]
* Question (jliu113-stat697): What is the rules of %LET statement?
- Answer (jliu113-stat697): 1)All values are stored as character strings; 2)Mathematical expressions are not evaluated; 3)The case of the value is preserved; 4) Quotation marks that enclose literals are stored as part of the value;5) Leading and trailing blanks are removed from the value before the assignment is made.



[Course Textbook Chapter9, Problem 12]
* Question (jliu113-stat697): What is Macro Quoting Functions?
- Answer (jliu113-stat697): 1)%STR:(; + - * / , < > = blank ^ ~ # | LT EQ GT AND OR NOT LE GE NE IN); 2)%NRSTR; 3)%BQUOTE.



[Course Textbook Chapter9, Problem 13]
* Question (jliu113-stat697): What is the Macro Character Functions?
- Answer (jliu113-stat697): 1)%UPCASE; 2)%QUPCASE; 3) %SUBSTR; 4)%QSUBSTR; 5) %INDEX; 6) %SCAN; 7) %QSCAN.



[reference-basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (jliu113-stat697): How do you understand of the Forward Rescan Rule ? Explain it with the example.
- Answer (jliu113-stat697):  E.g., if "i" has value 2, then &&species&i. -> &species2 -> Versicolor by the Forward RescanRule; in the first iteration, && -> & and &i. -> 2; then &species2 just dereferences the macro variable "species2" created earlier.



***



# Recipes Exploration Results




```


*Example;
*to see macro and macration;
options mprint;
*create three macro varibales;
%macro splitDatasetAndPrintMeans;
    %let species1 = Setosa;
	%let species2 = Versicolor;
	%let species3 = Virginica;
	%put _user_;
	%put;

	* add do loop in macro;
	%do i=1 %to 3;
	    %let currentSpecies = &&species&i.;
		%put & = currentSpecies.;
		data iris_&currentSpecies.;
		    set sashelp.iris;
			*the variable to be string result;
			if species = "&currentSpecies.";
		run;
	    proc means n nmiss min q1 median q3 maxdec=1;
		run;
	%end;
%mend;
%splitDatasetAndPrintMeans



```
