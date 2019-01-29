
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (jduan10-stat697): Do we have extra credit assignment?



[Course Structure Quiz, Problem 2]
* Question (jduan10-stat697): How to make a branch the new master while keeping old master as a branch in Github?



[Course Structure Quiz, Problem 3]
* Question (jduan10-stat697): What can we do to stop a loop?



[Course Structure Quiz, Problem 4]
* Question (jduan10-stat697): How can I dynamically import GitHub repository inside another GitHub repository?



[Course Structure Quiz, Problem 5]
* Question (jduan10-stat697): What will happen if I add output outside the Do loop?



[Course Structure Quiz, Problem 6]
* Question (jduan10-stat697): What is the format of final exam?



[Course Structure Quiz, Problem 7]
* Question (jduan10-stat697): Can we choose our project teammate?



[hello-orld Week 1 SAS Recipe]
* Question (jduan10-stat697):  What is the function of put statement?



[fizz-buzz Week 1 SAS Recipe]
* Question (jduan10-stat697): Can we use do loop within another do loop?



***



# Recipes Exploration Results



```


* Recipe: hello-world ;

* original recipe;
data _null_;
    put 'Hello, World!';
run;

* modified to print the content of a macro variable;
%let Myname = Jingyi Duan;
data _null_;
    put "Hello, &Myname.!";
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
