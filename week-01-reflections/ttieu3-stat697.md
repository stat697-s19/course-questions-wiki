
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (ttieu3-stat697): Why isnt it 3 steps when there were 3 "Week 1 Setup Step _" instructions?

[Course Structure Quiz, Problem 2]
* Question (ttieu3-stat697): Is it possible to skip the first forum post?

[Course Structure Quiz, Problem 3]
* Question (ttieu3-stat697): Is it possible to skip the first weekly reflection too?

[Course Structure Quiz, Problem 5]
* Question (ttieu3-stat697): Do the multiple choice questions have 4 or 5 choices?

[Course Structure Quiz, Problem 6]
* Question (ttieu3-stat697): Is the achievement system related to video games?

[Course Structure Quiz, Problem 7]
* Question (ttieu3-stat697): Is this encouraging me to turn in incomplete poor quality work on time instead of finished work a couple days later?

[Course Structure Quiz, Problem 8]
* Question (ttieu3-stat697): How much extra credit is a typo worth?

[hello-world Week 1 SAS Recipe]
* Question (ttieu3-stat697): What is the purpose of using put?
* Answer (ttieu3-stat697): It is useful in debugging.

[fizz-buzz Week 1 SAS Recipe]
* Question (ttieu3-stat697): Why start with data _null_?




***



# Recipes Exploration Results



```


/* Hello World */

data _null_;
	put 'Hello, World!';
run;

/* Fizz Buzz */

data _null_;
	do i = 1 to 100;
		if mod(i,3) = 0 then put 'Fizz';
		else if mod(i,5) = 0 then put 'Buzz';
		else put i=;
	end;
run;



```
