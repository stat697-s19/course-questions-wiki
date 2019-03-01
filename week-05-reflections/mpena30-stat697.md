
# Questions about Problems and Recipes



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): How could we go about using a summary function in PROC SQL with mulitple columns but having the function applied separately for each column rather than across all the specified columsn for each row?



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): Does the summary function COUNT(distinct column) for which unique values in a column are counted also count missing values as a unique value?
- Answer (mpena30-stat697): No. Missing values are ignored by the COUNT function.



[Course Textbook, Chapter 2] 
* Question (mpena30-stat697): How do we specify if we want the COUNT function to be applied to the entire table versus a group of rows?
- Answer (mpena30-stat697): We can use the GROUP BY clause along with COUNT(*).



[Course Textbook, Chapter 2]
* Question (mpena30-stat697): Does including columns or column expressions from the SELECT and HAVING clauses in the GROUP BY clause generally ensures PROC SQL only has to make one pass through the data?



[Course Textbook, Chapter 3]
* Question (mpena30-stat697): If using outer-join stntax to perform an inner join allows only two tables or views to be combined, does the same limitation apply when using outer-join syntax to perform an outer join? 



[Course Textbook, Chapter 3]
* Question (mpena30-stat697): Would the code of the nested query used to create an in-line view be the same if used in a seperate PROC SQL query to create a nontemporary table?



[Course Textbook, Chapter 3]
* Question (mpena30-stat697): How does using an in-line view over creating a table cuase more effcient prcossing by PROC SQL?



[combine-data-at-different-grains Week 5 SAS Recipe]
* Question (mpena30-stat697): Is the embedded select-query the equivalent of a using a subquery to subset data, in this case, to create table B?




***



# Recipes Exploration Results



```


* Recipe: combine-data-at-different-grains ;

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
			A.statename = B.statement
	order by	
		number_of_zipcodes desc
	;
quit;



```
