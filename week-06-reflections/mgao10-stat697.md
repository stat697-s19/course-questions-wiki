
# Questions about Problems and Recipes


[Week6 Reflection - TB Ch5, Problem 1]
* Question (mgao10-stat697): what is the difference between select, copy,describe and copy statement



[Week6 Reflection - TB Ch5, Problem 2]
* Question (mgao10-stat697): how to sort out the variable by level



[Week6 Reflection - TB Ch5, Problem 3]
* Question (mgao10-stat697): what is the difference between delete and drop statement



[Week6 Reflection - TB Ch5, Problem 4]
* Question (mgao10-stat697): when should i use when or if statement



[Week6 Reflection - TB Ch5, Problem 5]
* Question (mgao10-stat697): how to use set and create interchangably



[Week6 Reflection - TB Ch8, Problem 6]
* Question (mgao10-stat697): What is inobs= 



[Week6 Reflection - TB Ch8, Problem 7]
* Question (mgao10-stat697): what is stmer option in proq sql



[obtain-column-information Week 6 SAS Recipe]
* Question (mgao10-stat697): how to use wildcard to extrac information from the columns



***



# Recipes Exploration Results



```


*Example For Approach 1;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;

*Example For Approach 2;
proc contents order=varnum data=sashelp.iris;
run;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;

*Example For Approach 3;
proc sql;
    select
        name
    from
        dictionary.columns
    where
        lowcase(libname) = 'sashelp'
    and
        lowcase(memname) = 'iris'
    ;
quit;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;



```
