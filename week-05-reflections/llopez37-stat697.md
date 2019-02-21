
# Questions about Problems and Recipes

[Course Textbook Chapter 2, Problem 5]
- Question (llopez37-stat697):  How does it select the data to match with the name for the other data set?
- Answer(llopez37-stat660): it seems the outer query selects data for the names that match 

[Course Textbook Chapter 2, Problem 7]
- Question (llopez37-stat697): Is this because we include the other data set outside of the parenthesis? 

[Course Textbook Chapter 2, Problem 8]
- Question (llopez37-stat697) how else could we use the where not exists syntax?

[Course Textbook Chapter 2, Problem 9]
- Question (llopez37-stat697): Does this just show us that it was successful or what is the purpose of this?
- Answer (llopez37-stat697) It appears to be the case as opposed to an error message

[Course Textbook Chapter 3, Problem 1]
- Question (llopez37-stat697) is this only the case with joint conditions?

[Course Textbook Chapter 3, Problem 7]
- Question (llopez37-stat697):  Is it only referenceable in the current working session? 

[Course Textbook Chapter 3, Problem 9]
- Question (llopez37-stat697): How does it determine the count for the maximum?
- Answer (llopez37-stat697) it seems that that if the join involves views than it is the underlie views that count

[Combine Data Week 5 SAS Recipe]
- Question (llopez37-stat697): How does the inline know about the zip codes and why not go about the union route? 

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
