
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (yli110-stat697): What is an easy way for github to access files on your local computer?



[Course Structure Quiz, Problem 2]
* Question (yli110-stat697): How do you check the git version on your computer?



[Course Structure Quiz, Problem 3]
* Question (yli110-stat697): What are the general steps to follow a "gitHub flow"?



[Course Structure Quiz, Problem 4]
* Question (yli110-stat697): What are the changes called when you make them on GitHub?



[Course Structure Quiz, Problem 5]
* Question (yli110-stat697): What are the benefits of creating new branches to work on?



[Course Structure Quiz, Problem 6]
* Question (yli110-stat697): What is an easy to utilize GitHub to pull requests if not using git command line?



[Course Structure Quiz, Problem 7]
* Question (yli110-stat697): How do you start to work on a project that has already been partially done by someone else?



[hello-world Week 1 SAS Recipe]
* Question (yli110-stat697): What does the _null_ in the recipe stand for?



[fizz-buzz Week 1 SAS Recipe]
* Question (yli110-stat697): What does the function mod() do?



***



# Recipes Exploration Results



```


* Recipe: hello-world ;

data _null_;
    put "Hello, Yaqiong Li!";
run;



* Recipe: fizz-buzz ;

* customized recipe;
data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 then put 'Yaqiong';
        else if mod(i, 5) = 0 then put 'Li';
        else put i=;
    end;
run;

* expanded recipe;
data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 and mod(i,5)= 0 then put 'Yaqiong Li';
        else if mod(i, 3) = 0 then put 'Yaqiong';
        else if mod(i, 5) = 0 then put 'Li';
        else put i=;
    end;
run;



```
