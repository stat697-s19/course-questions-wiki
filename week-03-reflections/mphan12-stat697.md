
# Questions about Problems and Recipes



[Chapter 3, Problem 4]
- Question (mphan12-stat697): What is the difference on inner join a.id = b.id and from a,b where a.id = b.id?



[Chapter 3, Problem 6]
- Question (mphan12-stat697): What is the requirement for inner join statement?
- Answer (mphan12-stat697): The columns that are specified in a join condition in the WHERE clause must have the same data type.



[Chapter 3, Problem 8]
- Question (mphan12-stat697): When some values of the BY variable match, what PROC SQL join produce the same results as DATA step match-merge?
- Answer (mphan12-stat697): When only some of the values of the BY variable match, use a PROC SQL full outer join, and overlay common columns with COALESCE function.



[Chapter 3, Problem 10]
- Question (mphan12-stat697): When are table aliases required?
- Answer (mphan12-stat697): It is required when a table is joined to itself (called a self-join or reflexive join). It is also required when you need to reference columns from same-named tables in different libraries.



[Chapter 9, Problem 2]
- Question (mphan12-stat697): Can you put a &macro inside single quotes?
- Answer (mphan12-stat697): No, it must be in double quotes.



[Chapter 9, Problem 3]
- Question (mphan12-stat697): What does the option symbolgen do?
- Answer (mphan12-stat697): The SYMBOLGEN system option to monitor the value that is substituted for a macro variable reference.



[Chapter 10, Problem 4]
- Question (mphan12-stat697): What does &&& do?
- Answer (mphan12-stat697): In order to create an indirect reference (a reference whose value is a reference to a different macro variable), you must use three ampersands. Therefore, to use an indirect reference that resolves to Structured Query Language, the original reference must be &&&.



[basic-dry-programming-pattern Week 3 SAS Recipe]
- Question (mphan12-stat697): What is another way of doing the recipe?
- Answer (mphan12-stat697): 
```
title "Statistics: By Species";
proc means data = sashelp.iris n nmiss min q1 median q3 max maxdec=1;
  by species;
  where species in ("Setosa","Versicolor","Virginica");
run;
```


***



# Recipes Exploration Results



```



*Example;
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
		title "Statistics: &currentSpecies.";
        proc means n nmiss min q1 median q3 max maxdec=1;
        run;
    %end;
%mend;
%splitDatasetAndPrintMeans

title "Statistics: By Species";
proc means data = sashelp.iris n nmiss min q1 median q3 max maxdec=1;
  by species;
  where species in ("Setosa","Versicolor","Virginica");
run;



```
