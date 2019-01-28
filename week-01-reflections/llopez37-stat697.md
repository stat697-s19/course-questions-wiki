[Course Structure Quiz, Problem 1]
- Question (llopez37-stat697): Why is the desktop version more popular when the cloud version seems to be more convenient?
- Answer(llopez37-stat660) seems that it is because one requires internet

[Course Structure Quiz, Problem 2]
- Question (llopez37-stat697): If I get a similar blog post for my forum post as another student do I need to find a different one? 

[Course Structure Quiz, Problem 3]
- Question (llopez37-stat697): What is looked for in the reflections and forum posts in terms of grading? 

[Course Structure Quiz, Problem 4]
- Question (llopez37-stat697): Are there other methods to study for the exam? 
- Answer (llopez37-stat697) it appears that past exams are available as well

[Course Structure Quiz, Problem 5]
- Question (llopez37-stat697): What is the best way to get ready for the exam questions given that its multiple choice and not similar to our actual project and assignments? 

[Course Structure Quiz, Problem 6]
- Question (llopez37-stat697): how flexible are your office hours given that it is via google hangouts? 

[Course Structure Quiz, Problem 7]
- Question (llopez37-stat697): Will the final replicate the certification exam? 
- Answer(llopez37-stat697): It appears it will 

[hello-world Week 1 SAS Recipe]
- Question (llopez37-stat697): Is there an alternative to a put statement? 

[fizz-buzz Week 1 SAS Recipe]
- Question (llopez37-stat697): Is there a way to only output the numbers that would output my full name? 
***



# Recipes Exploration Results




```
* Recipe: hello-world ;

* original recipe;
data _null_;
    put 'Hello, Lorenz Lopez!';
run;

* Recipe: fizz-buzz ;

* original recipe;
data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 then put 'Lorenz';
        else if mod(i, 5) = 0 then put 'Lopez';
        if mod(i,3) = 0 and mod(i,5)= 0 then put 'Lorenz LOpez';
        else put i=;
    end;
run;

```

