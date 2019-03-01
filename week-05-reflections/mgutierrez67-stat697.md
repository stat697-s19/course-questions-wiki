
# Questions about Problems and Recipes

[Ch.2, Problem 5]
* Question (mgutierrez67-stat697): Assuming the subquery contains unique volunteer info for each row, could a left join have yielded the same results as using a subquery? 

[Ch.2, Problem 5]
* Question (mgutierrez67-stat697): Which approach is more efficient and require less computational resources if the same output can be achieved using a join or a noncorrelated subquery? 

[Ch.2, Problem 6]
* Question (mgutierrez67-stat697): Is there a type of subquery that can return more than one value?

[Ch.2, Problem 7]
* Question (mgutierrez67-stat697): What’s the benefit of using the Validate or Noexec option? Running a program without these options will also output an error if one occurs or will successfully compile without having to rerun the program compared to using Validate or Noexec.

[Ch.2, Problem 9]
* Question (mgutierrez67-stat697): Is it more efficient to conduct calculations using SAS data steps instead of inside a Proc SQL?

[Ch.3, Problem 1]
* Question (mgutierrez67-stat697): What scenario or situation would warrant a Cartesian product to be the desired outcome?

[Ch.3, Problem 7]
* Question (mgutierrez67-stat697): Can an in-line view be altered to create a new table with a create a table statement within the subquery? 
- Answer (mgutierrez67-stat697): No, I was not able to create a table inside an in-line view when I incorporated this approach into this week’s recipe program. 

[combine-data-at-different-grains Week 5 SAS Recipe]
* Question (mgutierrez67-stat697): When combining datasets with different granularity, should the programmer create an in-line view with the more granular data (like in the recipe video) or drill up using an in-line view with the less granular data?


***
# Recipes Exploration Results


```


* Recipe: combine-data-at-different-grains;

* original recipe;

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


*modified the code by adding a create a table statement inside the in-line view to test if it is possible to create a table for future reference or QA purposes inside an in-line view 
*this approach resulted in an error. a separate statement will need to be written in order to create a new table for future reference if the objective is to view just the output of the in-line view

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
            create table test1 as
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
