
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
 * Question dzhou11-stat697): What is the difference from inner join and outer join? the inner join can appear all of the data, Why use the outer join?



[Course Structure Quiz, Problem 2]
*  Question (dzhou11-stat697): What's the advantage of SQL merging data over merge function? It looks more complex than merge function.



 [Course Structure Quiz, Problem 3]
 * Question (dzhou11-stat697): what is the mean about 1,2 in substr(jobcode,1,2) 



[Course Structure Quiz, Problem 4]
 * Question (dzhou11-stat697): Why always we need to use % in Macro, what is it means?



[Course Structure Quiz, Problem 5]
 * Question (dzhou11-stat697): Where Marco is commonly used and what variable does it swift?



[Course Structure Quiz, Problem 6]
* Question (dzhou11-stat697): Do-loop is used frequently in marco, so what should we pay attention to when we use do-loop?



[Course Structure Quiz, Problem 7]
* Question (dzhou11-stat697): How to translate macro and SQL into the same variable for comparison



 [basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (dzhou11-stat697): How to express q1, median, Q3 with a graph? It feels that the numbers don't look very intuitive.





***






```


options mprint;
%macro splitDatasetAndPrintMeans;
    %let species1 = Setosa;
    %let species2 = Versicolor;
    %let species3 = Virginica;
    %put _user_;
    %put;
    %do i = 1 %to 3;
       %let currentSpecies = &&species&i.;
        %put &=currentSpecies.; /*print the value to log for debugging*/
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
