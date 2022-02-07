# Tutorial 1: Getting Started with R

Based on a document created by: Jason Pienaar and Tom Miller.  
Edited by: CCG 2021

## Outline

### Learning objectives:
* Interacting with RStudio
* Recognizing different elements in R and their functionality
* Load data in R from external tools

What you should have at the end of this tutorial
* A word document with answers to Tasks1-10.
* A script document with the code you produced in this tutorial.
* A basic understanding of how to run basic R code and obtain results.

### Content:
1.	Introduction
2.	Accessing R
3.	Tips for coding
4.	What does it look like and what does it mean?
5.	Simplest tricks in R
6.	R functions
7.	Importing files

## Introduction

Why R?
R is an independent, open source statistical computing environment, incorporating implementations of an older commercial program called “S” by an international team of statisticians. Most other statistics packages are principally orientated towards applying standard methods of data analysis, which is great, but it is difficult to apply non-standard methods or to add to the capabilities of existing methods. This is primarily due to their limited programming capabilities. In addition, they are pretty expensive and require new licensing agreements etc. One of the great strengths of R (other than that it is free) is the relative ease with which new capabilities can be added (the R language is really easy to use). Thus, the user can easily create new functions or combine existing functions or data BUT in order to use R we need to learn the R language hence the simple tutorials.
 
The truth about R:
1- There is nothing more frustrating than when your code does not work
2- There is nothing more satisfying than when your code does work!

Anything worth doing, from losing weight to getting a degree, takes time. Learning R is no different. Especially if this is your first experience programming, you are going to experience a lot of headaches when you get started. You will run into error after error and pound your fists against the table screaming: “WHY ISN’T MY CODE WORKING?!?!? There must be something wrong with this stupid software!!!” You will spend hours trying to find a bug in your code, only to find that - frustratingly enough, you had had an extra space or missed a comma somewhere. You’ll then wonder why you ever decided to learn R when (::sigh::) Excel was so “nice and easy.”

## Accessing R 

### Obtaining your own copy of R
Both PC and Macintosh versions of R can be downloaded from the [R home page](http://www.r-project.org/)

### on HSU virtual labs:
You can use a standardized set up on the school virtual lab (vlabs). To access vlabs:
* [Click Here](https://vlab.humboldt.edu/)
* Log in with your HSU information – complete the DUO authentication
* Go to the search icon to the bottom left and search : ‘Rstudio’
* Open R studio
 
## Before you start 

### Best practices

### Tips to learn to code
* PRACTICE! A good practice consists on writing code. Do not copy and paste, do not assume that you got it by reading the tutorial: type it yourself.
* A better practice is to make sure you understand what each line of code is doing. Use # to annotate your code (see below to find out what I mean).
* Keep a notebook with these explanations: ‘File_tutorial2.R line 102: this function sums all the numbers in a vector’. 

### Some R resources
* [Useful R Reference Cheatsheet by Tom Short](https://cran.r-project.org/doc/contrib/Short-refcard.pdf)
* [Basic skills by Quick R](https://www.statmethods.net)
* [Advanced skills Cheatsheet by Arianne Colton and Sean Chen](https://rstudio.com/wp-content/uploads/2016/02/advancedR.pdf)
* [Other resources from YaRrr! The pirate’s guide to R](https://bookdown.org/ndphillips/YaRrr/r-resources.html)

## What does it look like and what does it all mean
![Fig1](Tut1_figs/Fig1_CIRMBioinf.jpeg) 
 
Figure 1 is a typical workspace in Rstudio, with four panels. You may have to open a new script (source) when you open the program for the first time: click on the new script icon to the top-left corner (see Fig 1, indicated with a yellow arrow)The most important panels right now are on the left, the source and the console. The source code in the top-left corner is where you will type your code and save your script. The console is where the code runs. You can write code directly to the console to find whether it works or not, or the answer to a calculation. You can also send your code from the source to the console to run. Importantly, you will be saving your source code, if you are typing in the console, you will be unable to save your progress or reuse your code. Therefore, I recommend you ALWAYS type and work on the source panel and send your code to run and see the output on the console. The panels on the right will display your data tables, plots, help and other features, but we will get to those later.
 
### Task 1
In these tutorials, you will regularly find tasks interspersed with guidelines and code. In these tasks, you have to use the code you learned to complete some challenge, then upload a document with the results from each task (see provided example). Task 1 consists of some very simple exercises in R. Answer these on a separate word document and upload to your Canvas assignment page once you are finished.
a. Try typing ‘5’ in your source code, or any other number or letter, and then click on ‘Run’, near the top-right of the source panel. What happened?
b. We can type comments on the source code that don’t run on the console by using ‘#’. Anything written to the right of the ‘#’ will not run. Try typing: ‘5 # is my favorite number’ in the source, and click on ‘Run’. What happened?
c. Save your script: On the RStudio top menu, select save as, and save your script (right now you should have 2 lines, if you answered a and b above) as ‘myfirstscript.R’. Save all your progress from this tutorial and upload the script file to your Canvas assignment as well.

### Saving your work
As with any other type of file, you need to save your scripts for later use. When working in R or Rstudio, you will be saving the Source code. This is a common misconception: you will not be saving the output in the console, so make sure you are typing your code in the Source code window and then running it, otherwise you risk losing your work and being unable to replicate it. In R studio, go to File and Save as, just like you would with other types of documents. 

When working in vlabs: Make a folder with your name in the Desktop and store all your files in there (scripts, outputs, data files). You will then need to send these files to yourself using your Google Drive, Dropbox or email. IMPORTANT: do not log out of vlab before you store your files in the cloud! The files will be deleted when you log in and you will lose your work. 
 
## The Simplest Tricks with R:

### Basic arithmetic
Open the R program by double clicking on the R icon. Under the opening message, you will find the “>” prompt, waiting for you to ask R to do something. Data analyses in R proceeds as an interactive dialogue. We type an S statement at the > prompt, press Enter, and the interpreter executes the statement, i.e. by returning a result, producing graphical output or sending output to a file or device. Try typing in the following simple arithmetic examples (just type what follows the prompt > and then <kbd>Enter<kbd>).

```
2+3
2-3
2*3
2/3
2^3
4^2-3*2
(2-3)*(2*3)
```

The usual precedence for mathematical operators is followed (multiplication and division first, then addition and subtraction). In general, R ignores spaces and so they are not necessary, but for bigger expressions spaces may improve the readability.
 
### Task 2
In these tutorials, you will regularly find tasks interspersed with guidelines and code. In these tasks, you have to use the code you learned to complete some challenge, then upload a document with the results from each task (see provided example). Task 1 consists of doing simple calculations in R. In the document you turn in, show your code and the answer for each one.
Example:

```
455*544

```

You should get:
>455*544  
>[1] 247520
 
Run the following calculations:

```
49923*199
3333+111
322+543 * 234+23
```

And: The year you were born – today’s date (just the day) * your favorite number

These outputs you have created so far are numbers, or class numeric. Lets keep that in mind as we move to other classes.

## R functions
R is a functional programming language meaning that pretty much everything we do in R is in terms of functions. R includes hundreds of built-in functions for mathematical calculations (including matrix algebra, which is extremely useful in statistics), data analyses, graphing, etc. Values passed to functions are specified within parenthesis after the function name. Here are some simple examples to try:

```
log(100)
log(100, base=10)
seq(1, 4)
seq(2, 8, by=2)
seq(0, 1, length=11)
```
(Note: the function log returns the natural log).
To obtain help or additional info on a function, type ? before the function name or help(function name) and press Enter. For example:

```
?seq
```

 
### Task 3
Explore the functions seq and rep. Use the help to find more about them. Explain what they do in your own words and show an example for each (code and output).
 
## Data types and data structures

### Variables and Vectors
Most R functions (including the simple arithmetic ones from above) can operate on more complex data structures that individual numbers. The simplest data structure (and one that we will use often) is a vector. A vector contains a series of numeric items. To construct a vector use the c function (c for concatenate):

```
c(1, 2, 3, 4)
```

The “c” function combines all the numbers you provide into a vector or a list. From now on, we will give these vectors a variable name so that we can re-use them. To do this simply assign a name to the vector using “=” symbol and press Enter (some may prefer the old assignment symbol of “<-“, but “=” is simpler and more intuitive). Note that R is case sensitive so Vector1 and vector1 are not the same variable.

```
Vector1 = c(1, 2, 3, 4)
```

To see what is stored in the variable simply type the variable name and press Enter (that is, now type “Vector1”, hit return, and R will show you Vector1). The sequence operator from above (seq) also returns a vector. Functions applied to vectors operate on an element-wise basis. Thus:

```
Vector2 = log(Vector1)
```

returns the natural log values of the elements stored in Vector1 and then stores them in the variable Vector2 (note: you will probably use this at some point to log-transform a variable). The rules for naming variables in S are simple: variable names are composed of letters (a-z, A-Z), numerals (0-9) and periods (.) and can be of any length (the first character cannot be a number, and spaces are not allowed). Consequently, variables can be given descriptive names so that you don’t forget what the variable is. For example: “this.is.a.variable.containing.log.values.for.vector1” is a valid variable name. Stupid, maybe, but valid.

```
this.is.a.variable.containing.log.values.for.vector1 = log(Vector1)
```

However, remember that you will have to type it out again to recall the variable. Unlike in many programming languages, variables in S are dynamically defined and redefined so we do not need to tell the interpreter how many values, what type (real, integer etc) or whether it is numeric or a character. We can also redefine a variable simply by assigning it to a different function e.g.

```
Vector2 = rnorm(100)
```

Here the previous values in Vector2 are replaced by 100 standard-normal random numbers (the default mean = 0 and standard deviation = 1, we could easily change these defaults eg: rnorm(20, mean=25, sd=17) returns a vector containing 20 numbers drawn randomly from a set of normally distributed numbers with mean 25 and standard deviation 17). If we wish to print only one of the elements of a vector we index the element using square brackets as in the following example.

```
Vector2[21]
```

returns the 21st element of the vector.

### Lists
While vectors only contain numbers, lists can contain mixed types of elements in R. You can find numbers, strings (characters), logical arguments and even lists nested within lists. 

Create a list using the following code:

```
list_data=list(color='red', vector=c(21,23,43), password=TRUE, Temperature=21.5)
print(list_data)
```

Notice how printing your list gives you each of the stored pieces of information in order, regardless of their class. You can inquire about the types of data you have at each position of the list:

```
list_data[3]
class(list_data[[3]])
```
Uh! Logical class. This class of elements in R indicate true or false statements. We had not run into these before. If you try the other elements in the list you will find numeric, character strings and lists. The next layer of complexity is data frames and matrices, but, importantly, by now you have probably realized that R is much more than just a calculator. It can manipulate data, conduct much of the same statistics covered in SAS, JMP, Canoco, etc., and has excellent graphic capabilities. It can also serve as a programming language. We will cover examples of these in subsequent days of this workshop.

Let's practice some of these skills before we move on.
 
### Task 4
Practice your skills with variables and vectors! For each of the following items, show your code and your output.
1. Create a variable “diameters” containing 300 elements, randomly drawn from a normal distribution of elements with a mean of 22 and standard deviation 0.5. Imagine these are measurements of diatom diameters. What are diatoms and what do these summary statistics (mean of 22, standard deviation of 0.5) mean biologically?
2. Create a second variable that contains the natural log values of the above elements. Imagine this is the thickness of each diatom. Call this variable ‘thicknesses’. 
3. Use the function mean to return the means of the two variables
4. Use the function var to return the variances of the two variables
5. The function “plot” will create a separate window on your screen with a standard
labeled plot. Type plot(variable) to create a scatter plot of your variables against their indices, substituting your variable name into the brackets, and also plot(variable1, variable2) to plot your variables against each other. Paste your plot to the document you turn in. Based solely on this plot, what is the relationship between the diameter and thickness of this species of diatoms? (positive, negative, neutral) Explain your answer. 

### Task 5
Write down all the different classes of objects we have covered so far and explain what they contain in your own words. Then, provide an example regarding how we could use each one to store information in microbial ecology.

### Task 6
To explore the different types of elements in R, you will explore some functions on your own. Feel free to google and talk to your peers to complete this task. Make sure you understand the main difference between the classes and functions mentioned here. In your own words explain what these functions do:
is.character()
as.character()
is.numeric()
as.numeric()
is.logical()
as.logical()
factor()
class()
Test them on the variables you have created so far: Vector1, Vector2, this.is.a.variable.containing.log.values.for.vector1, list_data. Do they work like you predicted they would? Did you encounter anything surprising? If so, describe it and explain what happened.

## This is the end of the tutorial
Good job! You have completed your first coding session in R. 
** Make sure you save your files 
See you soon!

## Review what you learned:
How do you figure out what a function does?  
<details><summary>answer</summary>
<p>
*Google it  
*type ?function.name on your R console
</p>
</details>
You got an error message: how do you know what it means?  
<details><summary>answer</summary>
<p>
*Examine which objects/functions are named in the Error  
*Check the spelling of each of your functions and objects  
*Make sure you have clicked 'Run' on your lines of code, not simply wrote them in the script  
*Copy your Error message and Google it  
*Ask your coding community for help!
</p>
</details>
How do you become more proficient at coding?  
<details><summary>answer</summary>
<p>
*PRACTICE  
*practice
*practice some more
*keep a journal
</p>
</details>
