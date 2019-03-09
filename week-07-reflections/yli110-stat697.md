
# Questions about Problems and Recipes



[Course Textbook Chapter 23, Problem 4]
* Question (yli110-stat697): What are the common ways to summarize data and group it by one specific variable?



[Course Textbook Chapter 23, Problem 4]
* Question (yli110-stat697): What does the option nway in PROC MEANS do?



[Course Textbook Chapter 23, Problem 5]
* Question (yli110-stat697): What does the TYPE statement do in PROC MEANS?



[Course Textbook Chapter 23, Problem 5]
* Question (yli110-stat697): What does WHERE = output dataset option do in PROC MEANS?



[Weekly-Recipe-summarize-data-using-proc-report]
* Question (yli110-stat697): What PROC steps can PROC REPORT mimic?



***



# Recipes Exploration Results



```



* print the first 3 rows from sashelp.iris;

proc report data=sashelp.iris(obs=3);
run;

* sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";

ods exclude all;
proc report data = sashelp.iris out = work.iris(drop = _BREAK_);
	define SepalLength / order;
run;
ods exclude none;

* summarize values for a single qualitative variable;

proc report data=sashelp.iris;
	columns
		 Species
		 N
	;
	define Species / group;
	define N / 'Number of Species';
run;

* summarize values for a single quantitative variable;

proc report data = sashelp.iris;
	columns
		 Species
		 SepalLength = SepalLength_min
		 SepalLength = SepalLength_median
		 SepalLength = SepalLength_max
	;
	define Species / group;
	define SepalLength_min / min "Min of Sepal Lenght";
	define SepalLength_median / median 'Median of Sepal Length';
	define SepalLength_max / max "Max Sepal Length";
run;

* summarize values for two qualitative variables using a two-way table;

proc report data = sashelp.iris;
	columns
		SepalLength
		Species
		Total
	;
	define SepalLength / group;
	define Species / across;
	define Total / computed;

	compute Total;
	Total = sum(_c2_, _c3_, _c4_);
	endcomp;

	rbreak after/summarize;
run;



```
