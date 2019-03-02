
# Questions about Problems and Recipes


[Week5 Reflection - TB Ch2, Question 1]
* Question (lgao7-stat697): Q9-In what situation does PROC SQL remerges data?



[Week5 Reflection - TB Ch3, Question 2]
* Question (lgao7-stat697): Q1- What is the different between PROC SQL join and set operation?



[Week5 Reflection - TB Ch2, Question 3]
* Question (lgao7-stat697): What is non correlated  subquery?
* Answer (lgao7-stat697): Subqueries that can be evaluated independently.


[Week5 Reflection - TB Ch2,  Question 4]
* Question (lgao7-stat697): Can we assign a non correlated subquery in any clauses within PROC SQL?



[Week5 Reflection - TB Ch2, Question 5]
* Question (lgao7-stat697): How does correlated subquery with NOT EXISTS work together?



[Week5 Reflection - TB Ch3, Question 6]
* Question (lgao7-stat697):  Why does the in-linbe view cannot contain an ORDER BY clause?



[Week5 Reflection - TB Ch3, Question 7]
* Question (lgao7-stat697):  What is cartesian product? 



[Week5 Reflection - SAS Recipe 1, Question 1]
* Question (lgao7-stat697): What does colesce() function do? To change two or more variable 
names at the same time?




***



# Recipes Exploration Results



```

* [SAS Recipe 1: ombine-data-at-different-grains;

*Example;

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
		number_of_zipcodes dsec
	;
quit; 

/* 
join two datasets with FULL JOIN, to ensure we capture match and 
unmatch data in both dataset.
*/
