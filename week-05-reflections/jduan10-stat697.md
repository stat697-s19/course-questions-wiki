
# Questions about Problems and Recipes



[Course Textbook Chapter 2, Problem 5] 
- Question (jduan10-stat697): How to limit the rows that are read?



[Course Textbook Chapter 2, Problem 6] 
- Question (jduan10-stat697): How to create a negative condition?



[Course Textbook Chapter 2, Problem 7] 
- Question (jduan10-stat697): When specifying the limits for the range of values, is it necessary to specify the smaller value first?



[Course Textbook Chapter 2, Problem 8] 
- Question (jduan10-stat697): When making comparison, is matching case sensitive?



[Course Textbook Chapter 2, Problem 9] 
- Question (jduan10-stat697): When tables have a same-named column, does the PROC SQL outer union produce the same output?



[Course Textbook Chapter 3, Problem 1] 
- Question (jduan10-stat697): can we specify missing values without using the IS MISSING or IS NULL operator?



[Course Textbook Chapter 3, Problem 7] 
- Question (jduan10-stat697): How to force PROC SQL to ignore permanent labels in a table?



[Week 5 SAS Recipe: combine-data-at-different-grains] 
- Question (jduan10-stat697): What’s the maximum level of aggregation can be used in PROC SQL?



***



# Recipes Exploration Results



```


*Recipe: combine-data-at-different-grains;

proc sql number;
    select
         coalesce(A.statename, B.statename) as statename
        ,A.region
        ,A.division
        ,B.number_of_zipcodes
    from
        sashelp.us_data as A
        full join
        (
            select
                 statename
                ,count(*) as number_of_zipcodes format comma12.
            from
                sashelp.zipcode
            group by
                statename
        ) as B
        on
            A.statename = B.statename
    order by
        number_of_zipcodes desc
    ;
quit;




```
