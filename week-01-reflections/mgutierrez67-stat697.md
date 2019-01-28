
# Questions about Problems and Recipes

[Course Structure Quiz, Problem 1]
* Question (mgutierrez67-stat697): How are components defined in this course and how do they differ from steps (i.e. the Week 1 Setup Step 1 Components contains multiple steps)? Is component and step interchangeable/synonyms when mentioned in this class?

[Course Structure Quiz, Problem 2 & 3]
* Question (mgutierrez67-stat697): Based on historical data, do students perform better on the final if they complete all 7 weeks of forum post and reflection?
- Answer (mgutierrez67-stat697): Although I do not have data to support this, my assumption is students who complete all 7 forums posts and reflections tend to perform better in the final because of the increase exposure and knowledge gained.

[Course Structure Quiz, Problem 3]
* Question (mgutierrez67-stat697): Can a student write their weekly reflection by editing the markdown file through GitHub's web interface instead of using a dedicated text editor?
- Answer (mgutierrez67-stat697): I believe this can also be done, but the downside of using GitHub's interface is the lack of a spell checker. One can use the preview changes to see the output before submitting.

[Course Structure Quiz, Problem 3]
* Question (mgutierrez67-stat697): Why are we submitting our reflections as a Markdown file? What is a Markdown file?
- Answer (mgutierrez67-stat697): GitHub uses Markdown files to show the contents of the repo if a Readme.md file is included. Markdown files are text files that can be converted into many output formats.

[Course Structure Quiz, Problem 4]
* Question (mgutierrez67-stat697): Would it be helpful and/or recommended for groups to conduct code reviews of each other's work live similar to the code review sessions with the professor?
- Answer (mgutierrez67-stat697): I think there is value in conducting code reviews together and live compared to just writing notes or messages with our remarks. Live code reviews gives the group an opportunity for more open discussions and collaboration.

[Course Structure Quiz, Problem 5]
* Question (mgutierrez67-stat697): Can a student pass this class without completing the final/Building General Knowledge accomplishment? For example, can a student skip the final if they have already accomplished the 4 other competencies?

[Course Structure Quiz, Problem 5]
* Question (mgutierrez67-stat697): How does the industry view SAS credentials? Do most SAS jobs require it? Can someone take the SAS Certified Advanced Programmer for SAS 9 without a basic or intermediate credential?
- Answer (mgutierrez67-stat697): Based on my job searches, SAS credentials are not necessary, but a nice to have. I could not find any pre-requisites or additional requirements to take the SAS Certified Advanced Programmer exam.

[hello-world Week 1 SAS Recipe]
* Question (mgutierrez67-stat697): When should the put statement be used?
- Answer (mgutierrez67-stat697): One use of the put statement is to examine a dataset's attributes or variables.

[fizz-buzz Week 1 SAS Recipe]
* Question (mgutierrez67-stat697): What are some real world scenarios that the mod function would be needed in a larger project or program (outside of just needing to know the remainder value)?

***



# Recipes Exploration Results



```
* Recipe: hello-world ;

* original recipe;
data _null_;
    put 'Hello, World!';
run;

*modified to include macro variables and used the _USER_ keyword with put to print all user-defined macros and their corresponding values;
*note a null dataset was not needed to print the output into the log with the approach above;
%let x = this;
%let y = test;
%put _USER_;


* Recipe: fizz-buzz ;

* original recipe;
data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 then put 'Fizz';
        else if mod(i, 5) = 0 then put 'Buzz';
        else put i=;
    end;
run;

*modified the program to utilize a macro variable, but defined the value of the macro variable after the data step;
*note the macro variable needs to be assigned before the data step that it is referenced in or the desired output will not occur;
*the program reads the code starting from the top and as a result, the code below will just print %let num1=3 in the log;
data _null_;
    do i = 1 to 100;
        if mod(i,&num1.) = 0 then put 'Fizz';
        else if mod(i, 5) = 0 then put 'Buzz';
        else put i=;
    end;
run;
%let num1 = 3;

```
