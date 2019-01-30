
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mphan12-stat697): When posting screenshots, should we screenshot the entire desktop or only relevant snap-its of our screen?

[Course Structure Quiz, Problem 2]
* Question (mphan12-stat697): Can students quote articles from websites that are not listed?

[Course Structure Quiz, Problem 3]
* Question (mphan12-stat697): Are quiz questions typically multiple choice and fill in missing words?

[Course Structure Quiz, Problem 4]
* Question (mphan12-stat697): How are teams selected?

[Course Structure Quiz, Problem 5]
* Question (mphan12-stat697): Are some of the weekly quiz questions taken from prior Advance SAS Programming Exam?

[Course Structure Quiz, Problem 6]
* Question (mphan12-stat697): In the past, what percentage of students get an A in this course?

[Course Structure Quiz, Problem 7]
* Question (mphan12-stat697): Is there a limit in resubmitting incomplete assignments by a student?

[Course Structure Quiz, Problem 8]
* Question (mphan12-stat697): What is the maximum extra credit allowance?

[Course Structure Quiz, Problem 9]
* Question (mphan12-stat697): Can we still email the instructor?
- Answer (mphan12-stat697): Yes, the Professor is reachable by email.

[Course Structure Quiz, Problem 10]
* Question (mphan12-stat697): Why is it necessary to check GitHub daily?

[hello-world Week 1 SAS Recipe]
* Question (mphan12-stat697): Can single quotes instead of double quotes be used on character string?
* Answer (mphan12-stat697): Yes, single quotes can also be used in data step.  However, they will not work for macros constraint in string text.

[fizz-buzz Week 1 SAS Recipe]
* Question (mphan12-stat697): Would “mod(i,15)=0” achieve the same results as “mod(i,3)=0 and mod(i,5)=0”?
- Answer (mphan12-stat697): Yes, “mod(i,15)=0” and “mod(i,3)=0 and mod(i,5)=0” are the same.




***



# Recipes Exploration Results



```


*---------------------;
* Recipe: hello-world ;
*---------------------;
* original recipe;
data _null_;
    put 'Hello, World!';
run;

* modified to print the content of a macro variable;
* note the need to switch to double-quote for the macro variable to render;
%let className = STAT 697;
data _null_;
    put "Hello, &className.!";
run;

*-------------------;
* Recipe: fizz-buzz ;
*-------------------;
* original recipe;
data _null_;
    do i = 1 to 100;
        if mod(i,15)=0 then put 'My Phan';
	else if mod(i,3) = 0 then put 'My';
        else if mod(i, 5) = 0 then put 'Phan';
        else put i=;
    end;
run;

* modified to use macro variables to parametrize what's printed when;
* note the need to switch to double-quote for macro variables to render;
%let mod1 = 3;
%let mod1msg = My;
%let mod2 = 5;
%let mod2msg = Phan; 
data _null_;
    do i = 1 to 100;
        if      mod(i, &mod1. * &mod2.) = 0 then put "&mod1msg. &mod2msg.";
        else if mod(i, &mod1.) = 0 then put "&mod1msg.";
        else if mod(i, &mod2.) = 0 then put "&mod2msg.";
        else put i=;	
    end;
run;



```
