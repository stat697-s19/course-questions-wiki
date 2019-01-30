
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mpena30-stat697): Is the fizz-buzz exercise meant for us to get familiar with SAS and editing code on there, or just to make sure we can actually manuveur our way on there?



[Course Structure Quiz, Problem 2]
* Question (mpena30-stat697): What are the benefits of using a text editor over a word processor?
- Answer (mpena30-stat697): Using a text editor ensures the file will be have compatibility for all/most systems since it is the simplest form.



[Course Structure Quiz, Problem 5]
* Question (mpena30-stat697): Would you recommend studying in a group or on our own to prepare for the final exam?



[Course Structure Quiz, Problem 6]
* Question (mpena30-stat697): Based on the grading criteria where 3 additional acheivemnets met earns an A-, does that mean that even if the final exam isn't completed, an A- can still be earned for the course?



[Course Structure Quiz, Problem 7]
* Question (mpena30-stat697): Is the decision for resubmission based on the errors made or does it depend on the type of assignment?



[Course Structure Quiz, Problem 9]
* Question (mpena30-stat697): If we have a question that other people might also have, would it be best to contact you directly or post somewhere public?



[Course Structure Quiz, Problem 10]
* Question (mpena30-stat697): Should we be checking Slack daily primarily for any new direct messages or should we also be reviewing new posts that are posted on the channels?



[hello-world Week 1 SAS Recipe]
* Question (mpena30-stat697): Is the type of indentation used primarily for formatting or is there another purpose?



[fizz-buzz Week 1 SAS Recipe]
* Question (mpena30-stat697): Why is mod the name for a function that gives the remainder?
- Answer (mpena30-stat697): The mod function is named after the modulo operation which gives the remainder after the division of the first term by the second.




***



# Recipes Exploration Results



```


* Recipe: hello-world ;

* original recipe;
data _null_;
	put 'Hello World';
run;



* Recipe: fizz-buzz ;

* original recipe;
data _null_;
	do i = 1 to 100;
		if mod(i,3) = 0 then put 'Fizz';
		else if mod(i, 5) = 0 then put 'Buzz';
		else put i=;
	end;
run;



```
