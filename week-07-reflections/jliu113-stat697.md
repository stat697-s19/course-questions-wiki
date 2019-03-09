
# Questions about Problems and Recipes



[Course Textbook Ch10, Problem 1]
* Question (jliu113-stat697): Could library name in lowercase letters?
- Answer (jliu113-stat697): No, and enclose it in quotation marks.

[[Course Textbook Ch10, Problem 2]
* Question (jliu113-stat697): Which option can you use to specify whether a statement should be executed after its syntax is checked for accuracy?
- Answer (jliu113-stat697):EXEC|NOEXEC.

[[Course Textbook Ch23, Problem 3]
* Question (jliu113-stat697):How much percent would lead direct access less likely more efficient?
- Answer (jliu113-stat697):Greater than 33%.

[[Course Textbook Ch23, Problem 4]
* Question (jliu113-stat697): What are the factors to affect the number of I/O operations?  
- Answer (jliu113-stat697): 1.subset size relative to data set size; 2. Number of pages in the data file; 3.order of the data; 4. Cost to uncompress a compressed file for a sequential read.


[[Course Textbook Ch23, Problem 5]
* Question (jliu113-stat697): What would SAS do when the subset is less than 3% and between 3% and 33%?
- Answer (jliu113-stat697): SAS uses an index when subset is less than 3% of the data set, and uses an index if the subset is between 3% and 33% of the data set.



[[Course Textbook Ch23, Problem 6]
* Question (jliu113-stat697): What is the meaning of page size and three pages?
- Answer (jliu113-stat697): If the data file’s pages count is less than three pages, then sequential access is faster if the subset is less than 3% of the entire data set. The amount of data that can be transferred to one buffer in a single I/O operation is referred to as page size. Use CONTENTS to get information.


[[Course Textbook Ch23, Problem 7]
* Question (jliu113-stat697): Which variable result more CPU, Numeric or Character?
- Answer (jliu113-stat697):  Numeric.                                                                                                                                                                                                      






[ summarize-data-using-proc-report Week 7 SAS Recipe]
* Question (jliu113-stat697):What is the difference between proc sql and proc report?
- Answer (jliu113-stat697):  In particular, while proc sql is often seen as the main Swiss-army-knife proc, useful for both data-definition language (DDL) and data-manipulation
language (DML) operations, proc report can be used to recreate many of the same types of output as the select query in proc sql.




***



# Recipes Exploration Results



```


* Recipe summarize-data-using-proc-report ;

*Examples;

* print the first 3 rows from sashelp.iris;

proc report data=sashelp.iris(obs=3);
run;

* sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";

ods exclude all;/* not show the result*/
proc report data =sashelp.iris out =Work.iris(drop=_BREDK_); /*default*/
    define 
	    SepalLength /order;
ods exclude none;

* summarize values for a single qualitative variable;

proc report data= sashelp.iris;
    columns
	    Species
		N
	;
	define Species /group;
	define N/ "Number of Irises";
run;


* summarize values for a single quantitative variable;


proc report data =sashelp.iris ; /*default*/
    columns 
	    Species
		SepalLength = SepalLength_Min
		SepalLength = SepalLength_Median
		SepalLength = SepalLength_Max
	;
    define Species /group; 
	define SepalLength_Min /min "Minimum Sepal Length";
	define SepalLength_Median /median "Median Sepal Length";
	define SepalLength_Max /max "Maximum Sepal Length";
run;


* summarize values for two qualitative variables using a two-way table;

proc report data=sashelp.iris;
    columns 
	    SepalLength
		Species
		Total
	;
	define SepalLength /group;
	define Species /across;
	define Total / computed;

	compute Total;
	    Total =sum(_c2_, _c3_, _c4_);
	endcomp;
	rbreak after /summarize;
run;

