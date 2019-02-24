
# Questions about Problems and Recipes



[Week5 Reflection - TB Ch2, Problem 1]

* Question (mgao10-stat697): How to correctly use where statement?

[Week5 Reflection - TB Ch2, Problem 2]

* Question (mgao10-stat697): what is noncorreleated subquery

[Week5 Reflection - TB Ch2, Problem 3]

* Question (mgao10-stat697): how to correctly indentify the syntax

[Week5 Reflection - TB Ch3, Problem 4]

* Question (mgao10-stat697): How to remerges data by using Proc SQL

[Week5 Reflection - TB Ch3, Problem 5]

* Question (mgao10-stat697): How to use outer union statement

[Week5 Reflection - TB Ch3, Problem 6]

* Question (mgao10-stat697): how to eliminate the missing value 

[Week5 Reflection - TB Ch3, Problem 7]

* Question (mgao10-stat697): what is &&teach&crs?

[combine-data-at-different-grains Week 5 SAS Recipe]

* Question (mgao10-stat697): is there any other command similar to the coalesce?


***



# Recipes Exploration Results



```


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
