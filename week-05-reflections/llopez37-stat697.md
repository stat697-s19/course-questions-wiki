
# Questions about Problems and Recipes

[Course Textbook Chapter 2, Problem 5]
- Question (llopez37-stat697):  
- Answer(llopez37-stat660): 

[Course Textbook Chapter 2, Problem 7]
- Question (llopez37-stat697): 

[Course Textbook Chapter 2, Problem 8]
- Question (llopez37-stat697)

[Course Textbook Chapter 2, Problem 9]
- Question (llopez37-stat697): 
- Answer (llopez37-stat697) 

[Course Textbook Chapter 3, Problem 1]
- Question (llopez37-stat697) 

[Course Textbook Chapter 3, Problem 7]
- Question (llopez37-stat697):  

[Course Textbook Chapter 3, Problem 9]
- Question (llopez37-stat697):
- Answer (llopez37-stat697) 

[Combine Data Week 5 SAS Recipe]
- Question (llopez37-stat697): 



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
