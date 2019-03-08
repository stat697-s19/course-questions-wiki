
# Questions about Problems and Recipes
[Course Textbook Chapter 23, Problem 4]
- Question (llopez37-stat697): Is there a method to specifically target one variable and summarize it?

[Course Textbook Chapter 23, Problem 4]
- Question (llopez37-stat697): What different options do we have with our proc means?

[Course Textbook Chapter 23, Problem 5]
- Question (llopez37-stat697): What does the nway statement do in PROC MEANS?

[Course Textbook Chapter 23, Problem 5]
- Question (llopez37-stat697): What does thpe and where do in proc means? 

[Weekly-Recipe-summarize-data-using-proc-report]
- Question (llopez37-stat697):

***



```



proc report data=sashelp.iris(obs=3);
run;

ods exclude all;
proc report data=sashelp.iris out=Work.iris(drop=_BREAK_);
    define
        SepalLength / order;
run;
ods exclude none;

proc report data=sashelp.iris;
    columns
        Species
        N
    ;
    define Species / group;
    define N / "Number of Irises";
run;

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
