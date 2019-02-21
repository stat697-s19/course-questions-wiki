
# Questions about Problems and Recipes



[Chapter 2, Problem 5]
- Question (mphan12-stat697): What is the difference between HAVING and WHERE?
- Answer (mphan12-stat697): HAVING is a clause condition on a group calculated metric, while WHERE clause is on the individual rows. 



[Chapter 2, Problem 6]
- Question (mphan12-stat697): What are the conditions of remerging?
- Answer (mphan12-stat697): 1. The values returned by a summary function are used in a calculation; 2. The SELECT clause specifies a column that contains a summary function and other column(s) that are not listed in a GROUP BY clause. 3.The HAVING clause specifies one  or more columns or column expressions that are not included in a subquery  or a GROUP BY clause.



[Chapter 2, Problem 7]
- Question (mphan12-stat697): What’s the benefit of using the Validate or Noexec option? 



[Chapter 3, Problem 1]
- Question (mphan12-stat697): What scenario or situation would warrant a Cartesian product?



[Chapter 3, Problem 7]
- Question (mphan12-stat697): Can an in-line view be altered to create a new table with a create a table statement within the subquery? 
- Answer (mphan12-stat697): No, I was not able to create a table inside an in-line view when I incorporated this approach into this week’s recipe program. 



[Chapter 3, Problem 9]
- Question (mphan12-stat697): What is the maximum number of tables inner join can combine?
- Answer (mphan12-stat697): A maximum of 256 tables can be combined in a single inner join. If the join involves views (either in-line views or PROC SQL views), it is the number of tables that underlie the views, not the number of views, that counts towards the limit of 256.



[combine-data-at-different-grains Week 5 SAS Recipe]
* Question (mphan12-stat697): When combining datasets with different granularity, should drill up using an in-line view with the less granular data?


***



# Recipes Exploration Results



```


* Recipe: reference-combine-data-at-different-grains ;
* original recipe;
proc sql number;
    select 
	coalesce (A.statename, B.statename) as statename
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
    on    A.statename = B. statename
    order by 
       number_of_zipcodes desc
    ;
quit; 



```
