
# Questions about Problems and Recipes



[Week3 Reflection - TB Ch3, Problem 1]
* Question (mgao10-stat697): How is the from and where works



[Week3 Reflection - TB Ch3, Problem 2]
* Question (mgao10-stat697): what is the difference between inner join and outer join



[Week3 Reflection - TB Ch3, Problem 3]
* Question (mgao10-stat697): how to merge and sort at the same time



[Week3 Reflection - TB Ch9, Problem 4]
* Question (mgao10-stat697): what is %LET statment means



[Week3 Reflection - TB Ch9, Problem 5]
* Question (mgao10-stat697): what is symput?



[Week3 Reflection - TB Ch10, Problem 6]
* Question (mgao10-stat697): What is macro variable?



[Week3 Reflection - TB Ch10, Problem 7]
* Question (mgao10-stat697): what is &&teach&crs?



[basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mgao10-stat697): Is there a way to plot quantile?

***



# Recipes Exploration Results



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
        %put &=currentSpecies.;
        data iris_&currentSpecies.;
            set sashelp.iris;
            if species = "&currentSpecies.";
        run;
        proc means n nmiss min q1 median q3 max maxdec=1;
        run;
    %end;
%mend;
%splitDatasetAndPrintMeans



```
