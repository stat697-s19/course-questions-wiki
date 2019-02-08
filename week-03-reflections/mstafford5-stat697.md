
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mstafford5-stat697): What would happen to null values on the 'ON' statement? Would they be ignored or joined together in the join statement?



[Course Structure Quiz, Problem 2]
* Question (mstafford5-stat697): When are right joins not redundant to left joins? If the order is swapped, wouldn't they be equivalent?



[Course Structure Quiz, Problem 3]
* Question (mstafford5-stat697): Is the SQL syntax the same in the SAS environment as other SQL environments such as mySQL?



[Course Structure Quiz, Problem 4]
* Question (mstafford5-stat697): How are macro variables useful for data queries, besides updating to have current titles?



[Course Structure Quiz, Problem 5]
* Question (mstafford5-stat697): Can macro values have conditions where they will change values?



[Course Structure Quiz, Problem 6]
* Question (mstafford5-stat697): Which regular SAS functions can be replaced by macro functions? How would this change computatiuon time?



[Course Structure Quiz, Problem 7]
* Question (mstafford5-stat697): Are macro %let symput, and other macros statements typically annotated? Or are they thought to be self-explanitory?



[Basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mstafford5-stat697): How is a macro similar and different to using the 'def' function in python? 



[Basic-dry-programming-pattern Week 3 SAS Recipe]
* Question (mstafford5-stat697): Is there a clear and readable way to nest macros within eachother?



***



# Recipes Exploration Results




```
* Recipe: basic-dry-programming-pattern ;

options mprint;
%macro splitDatasetAndPrintMeans;
    %let species1 = Setosa;
    %let species2 = Versicolor;
    %let species3 = Virginica;
    %put _user_;
    %put;
    %do i = 1 %to 2;
        %let currentSpecies = &&species&i.;
        %put &=currentSpecies.;
        data iris_&currentSpecies.;
            set sashelp.iris;*when deleted, won't print because var is missing;
            if species = "&currentSpecies.";
        run;
        proc means n nmiss min q1 median q3 max maxdec=1;
        run;
    %end;
%mend;
%splitDatasetAndPrintMeans
*deleted blank line to see change in printed output;
*tested what happens when set statement is missing;



```
