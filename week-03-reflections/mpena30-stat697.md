
# Questions about Problems and Recipes



[Course Textbook, Chapter 3]
* Question (mpena30-stat697): In which cases would we ever want the Cartesian product to be the query outcome?



[Course Textbook, Chapter 3]
* Question (mpena30-stat697): Do the columns that are included in the SELECT clause each have to be specified in the WHERE clause of an inner join SELECT statement?
- Answer (mpena30-stat697): No, columns that are not specified in the WHERE clause are not included in the output. The columns included in the SELECT cluase are used to build the Cartesian product in the processing.



[Course Textbook, Chapter 3] 
* Question (mpena30-stat697): Why would we want to rename a duplicate column if the contents are the same anyways? Wouldn't it make sense to just delete the duplicate?



[Course Textbook, Chapter 9]
* Question (mpena30-stat697):  Can you use user-defined macro variables to create a program template where you can reuse to perform the same procedures for different cases?



[Course Textbook, Chapter 9]
* Question (mpena30-stat697): Is the %put statement basically a note to self in the SAS log? If this is the case, can we also add notes on things other than macro variables?



[Course Textbook, Chapter 9]
* Question (mpena30-stat697): Can the %QUPCASE macro function be used to mask special characters the same way other macro quoting functions can?



[Course Textbook, Chapter 10]
* Question (mpena30-stat697): Is there an equivalent of the SYMPUT routine in data step for PROC SQL that also allows the user to use expressions?



[basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mpena30-stat697): In the do-loop of the macro shell, why is the Forward Rescan Rule needed to do two passes? Why can't one pass perform all the needed actions?




***



# Recipes Exploration Results



```


* Recipe: basic-dry-programming-pattern ;

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
		proc means n nmiss min q1 median q3 maxdec=1;
		run;
	%end;
%mend;
%splitDatasetAndPrintMeans



```
