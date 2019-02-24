
# Questions about Problems and Recipes



[Course Textbook Chapter 2, Problem 6]
* Question (yli110-stat697): What is a non correlated subquery?



[Course Textbook Chapter 2, Problem 7]
* Question (yli110-stat697): What is the difference between VALIDATE and NOEXEC?



[Course Textbook Chapter 2, Problem 8]
* Question (yli110-stat697): What does the operator NOT EXISTS do in PROC SQL?



[Course Textbook Chapter 2, Problem 9]
* Question (yli110-stat697): What will the log show when data remerging happens?



[Course Textbook Chapter 3, Problem 1]
* Question (yli110-stat697): What is a Cartesian product in PROC SQL?



[Course Textbook Chapter 2, Problem 7]
* Question (yli110-stat697): When can an in-line view be referenced?



[Course Textbook Chapter 2, Problem 9]
* Question (yli110-stat697): What are the two ways to do inner join in PROC SQL?



[combine-data-at-different-grains Week 5 SAS Recipe]
* Question (yli110-stat697): What is the most convenient way to combine datasets that have different levels of data (eg, state level versus city level)?



***



# Recipes Exploration Results



```



proc sql number; /*number: seeing line number as output*/
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


