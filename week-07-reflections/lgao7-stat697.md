
# Questions about Problems and Recipes



[Week7 Reflection - TB Ch23, Question 1]
* Question (lgao7-stat697):  Does the index only work with WHERE expression/condition?



[Week7 Reflection - TB Ch23, Question 2]
* Question (lgao7-stat697):  Is index nessacery to create an index for WHERE processing?  
* Answer (lgao7-stat697): Determine if using index is more efficient; do not create an index if the data file's page count is less than three pages. (more on P761).



[Week7 Reflection - TB Ch23, Question 3]
* Question (lgao7-stat697):  When should we use an index to optimize the process?
* Answer (lgao7-stat697): It's more efficient to use indexed access for a small subset and to used sequential access for a large subset. Whether SAS uses an index depends on the percentage of observations that are qualified. (P757, CH23)



[Week7 Reflection - TB Ch23,  Question 4]
* Question (lgao7-stat697):  What are some common tools/procedures for summarizing data?
* Answer (lgao7-stat697): PROC MEANS, SUMMARY, TABULATE, REPORT, SQL, and DATA step.



[Week7 Reflection - SAS Recipe 1, Question 1]
* Question (lgao7-stat697):  What would be the pros and cons using PROC REPORT? Why not PROC SORT/TABLE?




***



# Recipes Exploration Results



```

* [SAS Recipe 1:  summarize-data-using-proc-report;

**Examples;

* print the first 3 rows from sashelp.iris;
proc report data=sashelp.iris(obs=3);
run;

* sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";
ods exclude all;
proc report data=sashelp.iris out=Work.iris(drop=_BREAK_);
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
	define N / "Number of Species";
run;

* summarize values for a single quantitative variable;
proc report data=sashelp.iris;
	columns
		Species
		SepalLength = SepalLength_Min
		SepalLength = SepalLength_median
		SepalLength = SepalLength_Max
	;
	define Species / group;
	define SepalLength_Min / min "Min Sepal Length";
	define SepalLength_Median / median "Median Sepal Length";
	define SepalLength_max / max "Max Sepal Length";
run;

* summarize values for two qualitative variables using a two-way table;
proc report data=sashelp.iris;
	columns 
		SepalLength
		Species
		Total
	;
	define SepalLength / group;
	define Species / across;
	define Total / computed;

	compute Total;
		Total = sum(_C2_, _c3_, _c4_); * sum up all values in column 2,3,4;
	endcomp;
	
	rbreak after / summarize;
run;
