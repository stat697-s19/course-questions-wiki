
# Questions about Problems and Recipes

[Chapter 1 Quiz, Problem 1]
Question (mgao10-stat697): What is the purpose of the PROC SQL

[Chapter 1 Quiz, Problem 2]
Question (mgao10-stat697): what other command count as statement?

[Chapter 1 Quiz, Problem 3]
Question (mgao10-stat697): Why comma is used to separate the variable

[Chapter 1 Quiz, Problem 4]
Question (mgao10-stat697): Should I practice the questions from our textbook?

[Chapter 2 Quiz, Problem 5]
Question (mgao10-stat697): what does the option b affect the code?

[hapter 2 Quiz, Problem 6]
Question (mgao10-stat697): why there is no comma after 120-spent as Balance

[hapter 2 Quiz, Problem 7]
Question (mgao10-stat697): what is the relationship abou group by with having?



***



# Recipes Exploration Results



```
1. 
proc sql outobs=3;
    select
        *
    from
        sashelp.iris
    ;
quit;

Question: 

Is there a way to limit the feature?

2. 

proc sql outobs=5 number;
    select
        *
    from
        sashelp.iris
    order by
        SepalLength
    ;
quit;

Question: 
What is the descending order command?

3. 
proc sql;
    * print frequency of each Species in sashelp.iris;
    select
         Species
        ,count(*) as Number_of_Irises
    from
        sashelp.iris
    group by
        Species
    ;
    * print median of SepalLength by Species in sashelp.iris;
    select
         Species
        ,min(SepalLength) as Minimum_Sepal_Length
        ,median(SepalLength) as Median_Sepal_Length
        ,max(SepalLength) as Maximum_Sepal_Length
    from
        sashelp.iris
    group by
        Species
    ;
quit;

Question:
How to incorporate having statement in this code?








```
