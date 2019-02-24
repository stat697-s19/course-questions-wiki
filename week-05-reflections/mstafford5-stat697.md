
# Questions about Problems and Recipes



[Chapter 2, Question 5]
* Question (mstafford5-stat697): Is there a way to only select a summary from a proc sql step, to check if you get the expected number of columns and rows, without having the output of a table?



[Chapter 2, Question 6]
* Question (mstafford5-stat697): What is a correlated subquery?
* Answer (mstafford5-stat697): It is a query that involves a column from the outer query. 



[Chapter 2, Question 7]
* Question (mstafford5-stat697): How do options and labels differ between proc sql and other sql engines such as postgre sql and mysql?



[Chapter 2, Question 8]
* Question (mstafford5-stat697): How is the indentation defined? Why do some parts of the query have double the indentation?



[Chapter 3, Question 1]
* Question (mstafford5-stat697): Why are cartesian products produced, rather than an error message?



[Chapter 3, Question 7]
* Question (mstafford5-stat697): How many in-line views can be nested within eachother?



[Chapter 3, Question 9]
* Question (mstafford5-stat697): How much faster is an inner join compared to outer joins?




[Combine-data-at-different-grains Week 5 SAS Recipe]
* Question (mstafford5-stat697): How can this recipe be revised in order to include data and other summary statistics from the 'B' zipcodes dataset?



***



# Recipes Exploration Results




```
* Recipe: combine-data-at-different-grains ;

proc sql number;
    select
         coalesce(A.statename, B.statename) as statename
        ,A.region
        ,A.DENSITY_2010-A.DENSITY_1910 as PopulationDensityGrowth
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

*added a calculated column to detect differences in population densities;

```
