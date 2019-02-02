
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (jliu113-stat697): How could students get the access for the final exam? 



[Course Structure Quiz, Problem 2]
* Question (jliu113-stat697): There will tentatively be __ Weekly project steps, including a code review, with __ of __steps needing to be compelted to earn the __ achievement in the course.



[Course Structure Quiz, Problem 3]
* Question (jliu113-stat697): How many question would be on the final exam? And how much time will the final exam last?



[Course Structure Quiz, Problem 4]
* Question (jliu113-stat697): There will tentatively be __ Weekly reflection, including a code review, with __ of __ steps needing be compelted to earn the __ achievement in the course.



[Course Structure Quiz, Problem 5]
* Question (jliu113-stat697): How could students get A?


[Course Structure Quiz, Problem 6]
* Question (jliu113-stat697): How could students earn the avhivment of final exam?


[Course Structure Quiz, Problem 7]
* Question (jliu113-stat697): What is the five achievement?


[hello-world Week 1 SAS Recipe]
* Question (jliu113-stat697): What's the -null- represent?


[fizz-buzz Week 1 SAS Recipe]
* Question jliu113-stat697): What's the "if else code" means?


***



# Recipes Exploration Results



```



* Recipe: hello-world ;

* original recipe:
data _null_;
    put 'Hello, World!';
run;

* modified to print the content of a macro variable;

%let className = STAT 6863;
data _null_;
    put "Hello, world! Jiayi!";
run;



* Recipe: fizz-buzz ;

* original recipe:
data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 then put 'Jiayi';
        else if mod(i, 5) = 0 then put 'Liu';
        else put i=;
    end;
run;

* modified to use macro variables to parametrize what's printed when;

data _null_;
    do i = 1 to 100;
        if mod(i,3)= 0 and mod(i,5) = 0 then put 'Jiayi-Liu';
        else if mod(i, 5) = 0 then put 'Liu';
        else if  mod(i,3) = 0 then put 'Jiayi';
        else put i=;
    end;
run;



```
