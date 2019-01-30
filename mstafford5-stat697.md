
# Questions about Problems and Recipes

# course-questions-wiki

[Course Structure Quiz, Problem 1]
* Question (mstafford5-stat697): How harshly are students docked when technical issues with github interferes with the submission process? For example, what will happen if a student doesn't fork the file, create a pull request, or they submit to the wrong repo?

[Course Structure Quiz, Problem 2]
* Question (mstafford5-stat697): For the weekly article/blog review, many posts are very basic or opinionated. Will we be held responsible for choosing a trivial or low-quality post?

[Course Structure Quiz, Problem 3]
* Question (mstafford5-stat697): Why is there a rigid requirement for students to submit on time, instead of docking half of the points?

[Course Structure Quiz, Problem 4]
* Question (mstafford5-stat697): Where can a student find more resources on how to use github and follow the process correctly?

[Course Structure Quiz, Problem 5]
* Question (mstafford5-stat697): Are the Weekly Reflection problems meant more as a learning tool or as a study guide for the final?

[Course Structure Quiz, Problem 6]
* Question (mstafford5-stat697): What are the criteria for earning a 'B' in this course?

[Course Structure Quiz, Problem 7]
* Question (mstafford5-stat697): How were the learning outcomes(CLO1-3) decided in this course?


[hello-world Week 1 SAS Recipe]
* Question (mstafford5-stat697): What is the purpose of printing text in a program when text editors and word documents suffice?

[fizz-buzz Week 1 SAS Recipe]
* Question (mstafford5-stat697): Why is the line: "else put i=;" not giving a value for i explicitly?




***



# Recipes Exploration Results



```


data _null_;
put 'Hello, World!';
run;
*put statement will not work with values not in quotes or if you add a variable that's assigned to a string;
***Hello World***;

data _null_;
do i = 1 to 100;
if mod(i, 3) = 3 then put'Fizz';*modified this statement;
else if mod(i,5) = 0 then put 'Buzz';
else put i=;
end;
run;
*when the mod statement has a value equal to greater than the second argument, then it will not make any changes to the output;
***Fizz-Buzz***


```
