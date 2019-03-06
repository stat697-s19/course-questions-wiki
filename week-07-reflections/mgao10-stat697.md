
# Questions about Problems and Recipes



[Week7 Reflection - TB Ch23, Problem 1]
* Question (mgao10-stat697): what standard data format need to have BY-group processing



[Week7 Reflection - TB Ch23, Problem 2]
* Question (mgao10-stat697): Is there a unique situation that Group by cannot be used?



[Week7 Reflection - TB Ch23, Problem 3]
* Question (mgao10-stat697): What is the class statement for in proc means



[Week7 Reflection - TB Ch23, Problem 4]
* Question (mgao10-stat697): what is NWAY option in multiple proc means steps



[summarize-data-using-proc-report Week 7 SAS Recipe]
* Question (mgao10-stat697): Is there any function that can be used for report?

***



# Recipes Exploration Results



```


*Examples;

* print the first 3 rows from sashelp.iris;
proc report data=sashelp.iris(obs=3);
run;

* sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";
ods exclude all;
proc report data=sashelp.iris out=Work.iris(drop=_BREAK_);
    define
        SepalLength / order;
run;
ods exclude none;

* summarize values for a single qualitative variable;
proc report data=sashelp.iris;
    columns
        Species
        N
    ;
    define Species / group;
    define N / "Number of Irises";
run;

* summarize values for a single quantitative variable;
proc report data=sashelp.iris;
    columns
        Species
        SepalLength = SepalLength_Min
        SepalLength = SepalLength_Median
        SepalLength = SepalLength_Max
    ;
    define Species / group;
    define SepalLength_Min / min "Minimum Sepal Length";
    define SepalLength_Median / median "Median Sepal Length";
    define SepalLength_Max / max "Maximum Sepal Length";
run;

* summarize values for two qualitative variables using a two-way table;
proc report data=sashelp.iris;
    columns
        SepalLength
        Species
        Total
    ;
    define SepalLength  / group;
    define Species/ across;
    define Total / computed;

    compute Total;
        Total = sum(_c2_, _c3_, _c4_);
    endcomp;
        
    rbreak after / summarize;
run;



```

