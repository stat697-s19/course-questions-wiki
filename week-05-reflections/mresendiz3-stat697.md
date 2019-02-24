
# Questions about Problems and Recipes




[Chapter 2, Problem 5]
* Question (mresendiz3-stat697): What does PROC SQL depend on when calculating summary functions and output results?
* Answer (mresendiz3-stat697): There are 4 key factors that weigh in on the calculation and summary: whether one or several columns are specified as arguments, if it has a GROUP BY clause, if there are columns listed that are outside of a summary function and if the summary function is specified in a SELECT clause, and if the WHERE clause has only columns that are specified in the SELECT clause. 

[Chapter 2, Problem 6]
* Question (mresendiz3-stat697): What is a noncorrelated subquery?
* Answer (mresendiz3-stat697): It is a nested query that executes indpendently with respect to the outer query where the outer query passes no values to the subquery. 


[Chapter 2, Problem 7]
* Question (mresendiz3-stat697): How does the HAVING clause work?
* Answer (mresendiz3-stat697): The HAVING clause has an expression that's used to subset the data. When using this clause PROC SQL displays only the groups that satisfy the HAVING expression. It's possible to use summary functions in a HAVING clause but not in a WHERE clause since the HAVING clause is used with gropus where a WHERE clause is only used with discrete rows. 

[Chapter 2, Problem 8]
* Question (mresendiz3-stat697): What does the NOEXEC option in the PROC SQL statement and the VALIDATE keyword before a SELECT statement accomplish?
* Answer (mresendiz3-stat697): When the NOEXEC option is invoked SAS checks the syntax of all queries in the PROC SQL step for accuracy without having to execute. The VALIDATE keyword accomplishes the same thing. However, it only affects the SELECT statement that immediately follows it where the NOEXEC option applies to all queries. 


[Chapter 2, Problem 9]
* Question (mresendiz3-stat697): What does data remerging accomplish?
* Answer (mresendiz3-stat697): When we use a summary function in a SELECT clause or a HAVING clause PROC SQL must make two passes through the table. PROC SQL calculates and returns the value of summary functions, groups data via the GROUP BY clause, gets additional columns and rows that need to be displayed in the output, and uses the result from the summary function to calcualte any arithmetic expressions where the summary function is involved. 


[Chapter 2, Problem 10]
* Question (mresendiz3-stat697): When does data remerging happen?
* Answer (mresendiz3-stat697): Data remerging happens when the values that are returned by a summary function are used in a calculation, when the HAVING clause has one or more columns or column expressions that aren't included in a subquery or a GROUP BY clause, and when the SELECT clause specifies a column that has a summary function and other columns that arent listed in a GROUP BY clause. 


[Chapter 3, Problem 1]
* Question (mresendiz3-stat697): When is a Cartesian product returned?
* Answer (mresendiz3-stat697): In a Cartesian product each row from a table is combined with every row from another and is returned when join conditoins aren't specified in a PROC SQL join. 


[Chapter 3, Problem 7]
* Question (mresendiz3-stat697): What is an in-line view?
* Answer (mresendiz3-stat697): It is a nested query that's specified in the outer query's FROM clause. It selects data from one or more tables to make a temporary table that the outer query uses to select data for output. It cannot contain an ORDERY BY clause. In-line views are used to optimize the efficiency of referencing data. 


[sas_recipe-combine-data-at-different-grains Week 5 SAS Recipe]
* Question (mresendiz3-stat697): Why is a full (outer) join used?
* Answer (mresendiz3-stat697): It's used because there could be ZIP codes that don't correspond to US states where aliases A and B might not be able to be matched up exactly by the join condition and we want to capture the matched and unmatched rows in the output table. 



***



# Recipes Exploration Results



```



*******************************************************************************;
**************** 80-character banner for column width reference ***************;
* set window width to banner width to calibrate line length to 80 characters  *;
*******************************************************************************;

*******************************************************************************;
* combine-data-at-different-grains ;
*******************************************************************************;
/*
Scenario: We wish to join data from multiple tables, each at a different grain
(aka level of aggregation).

Approach: Aggregate the data with a finer grain within an in-line view before
joining to the data with a coarser grain.

Recipe:

proc sql <any desired proc-sql options>;
    select
        <columns from result of join to include>
    from
        <courser-grained table>
        <join operation>
        <in-line view aggregating finer-grained table>
    <additional query clauses, as needed>
    ;
quit;

*/

*Example;

proc sql number;
	select 
		coalesce(A.statename, B.statename) as statename
		,A.region
		,A.division
		,B.number_of_zipcodes
	from 
		sashelp.us_date as A
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
			A.statename=B.statename
	order by
		number_of_zipcodes desc
	;
quit;



```
