
# Questions about Problems and Recipes


[Course Structure Quiz, Problem 1]
* Question (lgao-stat697): How to folking and cloning in GitHub?



[Course Structure Quiz, Problem 2]
* Question (lgao-stat697): Does the achievement affects the the final grade?
* Answer (lgao-stat697): Yes...



[Course Structure Quiz, Problem 3]
* Question (lgao-stat697): Is the requirement to complete 6 of 7 weekly reflections to allow people to "slack off" at the end of the academic term?



[Course Structure Quiz, Problem 4]
* Question (lgao-stat697): Does the code reviews take place in GitHub or Slack?



[Course Structure Quiz, Problem 5]
* Question (lgao-stat697): How similar to Weekly Reflection problems will final exam problems be? 



[Course Structure Quiz, Problem 6]
* Question (lgao-stat697): Does earning all 5 achievements guarantee an A in this course? 



[Course Structure Quiz, Problem 7]
* Question (lgao-stat697): If students are running out of time to complete an assignment, it is more acceptable to submite an incomplete one rather than submite an completed assignment few minutes/hours late? 


[Hello-world Week 1 SAS Recipe]
* Question (lgao-stat697): Why do we use_null_?


[Fizz-buzz Week 1 SAS Recipe]
* Question (lgao-stat697): What's the MOD function do?

***



# Recipes Exploration Results



```

* Recipe: hello-world;
data _null_;
	put "Hello, World!";
run;


* Recipe: Fizz Buzz;
data _null_;
	do i = 1 to 100;
		if mod(i, 3) = 0 then put "Fizz";       * Function MOD: divided by either 3 or 5;
		else if mod(i, 5) = 0 then put "Buzz";  * Benching: if / else;
		else put i = ;
	end;
run;



```
