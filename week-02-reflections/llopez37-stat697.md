
# Questions about Problems and Recipes



[Course Textbook Chapter 1, Problem 1]
- Question (llopez37-stat697): Could you also apply the same structure for regular sas statements such as naming columns A1-A10 if they were listed in that manner? 
- Answer(llopez37-stat660): It does not appear like this can be done. 

[Course Textbook Chapter 1, Problem 2]
- Question (llopez37-stat697): Why is select not considered a statement? 

[Course Textbook Chapter 1, Problem 4]
- Question (llopez37-stat697): Is sort a different statement within proc sql or does the statement not exist in proc sql? 

[Course Textbook Chapter 1, Problem 7]
- Question (llopez37-stat697): If I were to use a summary statement would it still go about the order by function without changing? 
- Answer (llopez37-stat697) From the sounds of it group by will cluster up similar groups but order by will resort to A-Z. 

[Course Textbook Chapter 2, Problem 3]
- Question (llopez37-stat697): Is calculated a function allowing the calculated version to take precedence? 

[Course Textbook Chapter 2, Problem 4]
- Question (llopez37-stat697):  Does this take the lowest number and reduce it down to that many rows? 
- Answer (llopez37-stat697) It seems this is the case since it was filtered down by the flight numbers.

[Course Textbook Chapter 2, Problem 10]
- Question (llopez37-stat697):  So in this case having statement would result in 1 output and group by would have multiple ones?  

[Summarize Data Week 2 SAS Recipe]
- Question (llopez37-stat697): How large of a dataset can we use before proc sql becomes restricted by it?

[Log with Macro Week 2 SAS Recipe]
- Question (llopez37-stat697): For how long does SAS remember our macros and is this something we could put in a flash drive to use whenever and wherever? 


***



# Recipes Exploration Results



```


proc sql outobs=3;
    select *
    from sashelp.iris
    ;
quit;

proc sql outobs=5 number;
    select *
    from sashelp.iris
    order by SepalLength
    ;
quit;

proc sql;
  select   Species, count(*) as Number_of_Irises
  from sashelp.iris
  group by Species
  ;
  
  select
    Species
    ,min (SepalLength) as Minimum_Sepal_Length
    ,median (SepalLength) as Median_Sepal_Length
    ,max(SepalLength) as Max_Sepal_Length
  from
    sashelp.iris
  group by
    Species
  ;
quit;

%let recipeName = print-to-log-with-macro-variables;
%put This is an example of the recipe &recipeName.;
%put This is an example of &=recipeName.;
%put _user_;


```
