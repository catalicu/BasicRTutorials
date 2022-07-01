# Tutorial 2: Data and basic graphs

Based on a document created by: Catalina Cuellar-Gempeler (CCG)
Edited by: CCG 2022

## Outline

### Learning objectives:
* Practice inputting simple data manually in R
* Review data types
* Create basic graphs

What you should have at the end of this tutorial
* A word document with answers to all Tasks.
* A script document with the code you produced in this tutorial.

### Content:
1.	Review data types and structures
2.	Use the appropriate data types and structures to create a data frame containing data from Figure 1 (Jessup et al 2004).
3.	Use the data frame to re-create Figure 1 from Jessup et al 2004.

> **Note** 
> This tutorial aims to introduce the necessary tools in R to reproduce scientific figures. You could do this with any figure from any paper. We are focusing on Figure 1 from the following reference as part of our Microbial Ecology course (BIOL433/533). Take a look at the whole paper for fun examples on how we can use microbial systems to answer big questions in ecology:
Jessup, C.M. et al 2004. Big questions, small worlds: microbial model systems in ecology. TRENDS in Ecology and Evolution 19(4): 189-197.[Link](https://www.sciencedirect.com/science/article/abs/pii/S0169534704000199)

### Some R resources
[Data Types and Structures from Software Carpentry](https://swcarpentry.github.io/r-novice-inflammation/13-supp-data-structures/)

## Review
Before we move on to today’s exercise we must review the different data types you will find in R. Lets do a quick review of numeric, character and logical objects, as well as organizing structures like vectors, lists, data frames and matrices. 
To make the best of the R language, you will need a strong understanding of these basic data types and structures. These are the objects you will manipulate every time you sit down to code. The most common source of issues (this happens to me every day!) are problems with object conversions. What we want to learn here are some good practices to avoid issues, and, more importantly, how to trouble shoot issues when they arise (because they will!). Every thing in R is an object, these can be low level objects (a letter – character – or number – numeric- for example) or high level objects (a list, or a matrix).

### Numeric and integer
Numeric objects can be real, integers or have decimals. Ex: ‘2’, ’14.5’, ‘0.8’, ‘15683’
Integers are always real numbers with no decimals. Ex: ‘2L’, ‘15L’ – the L tells R to store this object as an integer. 
Type a couple of numbers and run in Rstudio: include an integer and a decimal.

### Character
Characters are letters or symbols: ‘a’, ‘-‘, ‘?’
When you put them together, you create strings – that look like words: ‘vector’, ‘dataset1’, 'ATCACCGCATACCCCAATACG'. 
Type a character string that represents mRNA.
What is the difference between RNA and DNA in terms of sequences? (lets not forget about the biology!) 
<details><summary>answer</summary>
<p>
 
 * Uracil (U) instead of Thymine (T)
 
</p>
</details>


### Logic
Logical arguments are statements that can be TRUE or FALSE. For example, ‘1+1 == 1’ is FALSE. In this expression, ‘==’ is equivalent to an equal sign. Alternatively, ‘=!’ means unequal to. Thus, ‘1+1=! 1’ is TRUE. 

### Quick self-test!
What type of data are these? 

(a)
```
1894
```
(b)
```
'AB'=='BA'
```
(c)
```
'I love coding so much that I have dreams about it'
```
<details><summary>answer</summary>
<p>
 
 (a) is numeric  
 (b) is logical  
 (c) is a character string: several characters together in a string  
 
</p>
</details>

### Complex
Complex numbers include a real an imaginary portion and can also be included in calculations in the R coding environment. For example ‘1+4i’. We will not be using these much in this course, but hopefully this gives you an idea of the breath and power of the potential avenues for calculations and applications.  

### Vectors
The simplest data structure (and one that we will use often) is a vector. A vector contains a series of numeric items. To construct a vector use the c function (c for concatenate):

```
c(1, 2, 3, 4)
Vector1 = c(1, 2, 3, 4)
Vector1_log = log(Vector1)
```
You can also add elements to your vectors:
```
Vector2=c(Vector1_log, 1.2, 0.2, 0.6)
```
Remember you can explore a vector by using indexes. For example, if we wish to print only the element in position 3 of Vector2, we index the element using square brackets as in the following example.

```
Vector2[7]
```
These combinations of numeric objects are typically called ‘atomic vectors’, because they contain data from a single data type

### Lists
While vectors only contain numbers, lists can contain mixed types of elements in R. Because of this property, lists are sometimes called generic vectors, as opposed to atomic vectors.

For example:

```
list(1, ‘abc’, TRUE, 1+4i)
```

You can name the items within a list:
```
xlist=list(number=1, letters=‘abc’, logic=TRUE, imaginary=1+4i)
xlist
```

### Matrices
Matrices can be thought of as an extension of numeric vectors. Thus, matrices are vectors with 2 dimensions: rows and columns. All elements of a matrix must belong to the same type of data. Typically we will use numeric matrices, but character matrices are also possible. 

```
matrix(nrow=3, ncol=4)
```


### Data frames
Data frames are a special kind of list, where every element has the same length. In this sense, it behave like a matrix, having a set number of rows and columns. However, it is much more useful than a matrix for data manipulations, transformations, analyses and graphing. You will find that data frames are thus the most common data structure you will encounter in our tutorials. 
Creating data frames is relatively easy to do, directly in R. For example:
```
dataframe1=data.frame(identity=letters[1:10], x=1:10, y=1:10)
dataframe1
```

You should obtain a data frame with 3 columns and 10 rows. You can explore the attributes of your data frame by using the following functions:

```
head(dataframe1)
tail(dataframe1)
dim(dataframe1)
nrow(dataframe1)
ncol(dataframe1)
```

What did you get? What do these functions do? How did you figure it out?

<details><summary>answer</summary>
<p>
You probably figured out that:  
* head() gives you the top portion of your data frame  
* tail() gives you the bottom portion  
* dim() gives you the dimensions - thus number of rows and columns  
* rnow() indicates specifically the number of rows  
* ncol() the number of columns  
</p>
</details>

You will always run into new functions and have to develop good strategies to learn about them. Coding is much more about learning to learn than having a fixed knowledge. How do you learn what a new function does?
<details><summary>answer</summary>
<p>
* google it   
* ask your friends  
* ask R with a question mark before the name of the function. Example: ?head or ?dim  
* try it out! try using the function with different types of objects  
* dont be shy! coding is about acknowledging what you dont know, and trying new things  
</p>
</details>


### Task 1
When performing analyses and data transformations, it is key to recognize how your objects in R are structured and what data type they are, because this will define what you can do with them. When presented with an object, how would you know what structure or data type it is? Write the answer in your own words. 
For example, consider these two objects called 'secretObject1' and 'secretObject2':

```
secretObject1=list(1289, 'ATTACGCAGGCTACCACCC', barcode=TRUE)
secretObject2=data.frame(seq(1:10), rnorm(10,mean=50))
```
Even though you can probably figure out what type of data they are from the code, consider some of the following functions to explore them. Look them up and figure out how they are useful to explore your objects.
 
str()  
dim()  
length()  
names()  
colnames()  
is.character()  
as.character()  
is.numeric()  
as.numeric()  
is.logical()  
as.logical()  
factor()  
class()  

In your answer to this task: explain what type of data each object is and how you can use these functions to explore them. 

## Re-create Jessup et al 2004 figure 1.
To complete this activity, we will go over a series of tasks to reproduce data from the paper (Jessup et al 2004) and organize it in the appropriate structure for graphing. 

### Task 2
First, carefully observe Figure 1. What are the data represented here? What data types would better represent the data from the figure? (numeric, logical, character, factor, integer, complex). How do you know? Answer this carefully before you go any further.

### Task 3
Create a vector that represents the data from each axis. To begin with, we will focus on the solid green circles (heterogeneous environments) and ignore the open circles (homogeneous environments).
For example, the x axis is labeled ‘Ln(nutrient concentration)’ and begins with 0, 0.6, 1.3. You do not have to be exact, just approximate the numbers. Make sure that your vector contains the same number of data points as the figure. 

This is my attempt to do the first few data points.
```
nutrient=c(0,0.8,1.4,2.1,2.8)
```
Obviously, I am missing some, this is just an example.  
Then, do the same exercise with data obtained from the y axis. Here, my attempt:
```
diversity=c(0.25, 0.2, 0.55,0.65,0.66)
```
Each of your vectors should have 16 data points.

### Task 4
Based on the vectors you have created, plot the curve that describes this nutrient- diversity relationship. If your vectors both contain the correct number of data points and you have named them ‘nutrient’ and ‘diversity’, you should be able to use my code here. Otherwise, you will have to revise the number of data points, and/or make sure the names match in the code for the plot. 

```
plot(nutrient, diversity)
```

Troubleshoot:
* check the length of your vectors with length()
* check that the name of the vectors matches the names you wrote in the plot function. 

### Task 5
Before we go into the second portion of the figure, let’s think about what this plot means. 
How does diversity change with nutrient levels?
What does heterogeneity (not shaken) mean?

### Task 6
Now it is your turn to repeat the process with the open circles (homogeneous environment data points) to complete the figure. I would suggest you rename the vectors to represent the specific dataset (heterogeneous or homogeneous). You can easily do that by making a copy of an object with a different name:

```
diversity_heterogeneous=diversity
nutrients_heterogeneous=nutrients
```

Now create vectors for 'diversity_homogeneous' and 'nutrient_homogeneous. Here is some to get you started:

```
diversity_homogeneous=c(0.35, 0.35, 0.25,0.26, 0.36)
```

Is the nutrient data the same across both data sets? You can look at the figure, but you can also use a logical argument:
```
nutrient_heterogeneous==nutrient_homogeneity
```
If the output is TRUE, you can just keep working with one single ‘nutrient’ vector. If the output is FALSE, you need to keep both. 

### Task 7
Let’s build the full plot! 
First, we will run the code for the plot for heterogeneity, and then we will add the points for homogeneity. 

```
plot(nutrient, diversity_ heterogeneous)
points(nutrient, diversity_ homogeneous, pch=19, col=’black’)
```
The elements ‘pch’ and ‘col’ indicate the shape and color of the data points, respectively. Because you only indicated what you wanted in the homogeneity data points, the heterogeneity data points maintain the default (open circles). Change them to find you favorite type of data point. (for the purpose of the task, they just have to be different than open and solid black circles).  

### Task 8
What does this figure mean?
How does the diversity change with nutrient levels when the environment is homogeneous?
How is this different from the heterogeneous dataset?
What does this difference mean?

### Task 9
The code we worked on today can be useful later if you wanted to make a similar graph. This is the beauty of coding, that most of what you create, as painful as it is sometimes, can be reused, repurposed and saves you time when performing the same task in the future. 
Can you think of what object would you have to change if you had different levels of nutrients?
