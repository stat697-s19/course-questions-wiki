
# Questions about Problems and Recipes



[Course Textbook Ch2, Problem 1]
* Question (jliu113-stat697): Does BETWEEN-AND operator request to specify the smaller value first in PROC SQL?
- Answer (jliu113-stat697): No;


[[Course Textbook Ch2, Problem 2]
* Question (jliu113-stat697): Why do we need the keyword CALCULATE?
- Answer (jliu113-stat697):In SQL, the WHERE clause is processed before the SELECT clause.


[[Course Textbook Ch2, Problem 3]
* Question (jliu113-stat697): Is CALCULATED keyword is specified in ANSI standard for SQL?
- Answer (jliu113-stat697): No, only for SAS


[[Course Textbook Ch2, Problem 4]
* Question (jliu113-stat697): Would COUNT summary function counts the missing values?  
- Answer (jliu113-stat697): NO, only nomissing values.


[[Course Textbook Ch2, Problem 5]
* Question (jliu113-stat697): What is the difference between HAVING and WHERE?
- Answer (jliu113-stat697): HAVING clasuse is used with groups, while WHERE clause can be used only with individual rows. We don’t need to specify the keyword CALCULATED in a HAVING clause; but need in a WHERE clause.


[[Course Textbook Ch 2, Problem 6]
* Question (jliu113-stat697): Remerging occurs whenever any of the following conditions exist:?
- Answer (jliu113-stat697): 1. The values returned by a summary function are used in a calculation; 2. The SELECT clause specifies a column that contains a summary function and other column(s) that are not listed in a GROUP BY clause.3.The HAVING clause specifies one  or more columns or column expressions that are not included in a subquery  or a GROUP BY clause.


[[Course Textbook Ch3, Problem 7]
* Question (jliu113-stat697): Can an in-line view contain an ORDER BY clause?
- Answer (jliu113-stat697):  NO.                                                                                                                                                                    

[reference-combine-data-at-different-grains Week 5 SAS Recipe]
* Question (jliu113-stat697): What is the meaning of the coalesce function?
- Answer (jliu113-stat697): The coalesce function is used to ensure a
value of "statename" will be present for row in the output table.


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
