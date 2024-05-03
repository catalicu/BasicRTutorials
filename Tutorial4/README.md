# Tutorial 4: Intro to Programming: a population growth simulation
Based on a document created by: Thomas E. Miller
Edited by: CCG 2021

While R is perhaps best known as a statistical tool for analyzing data or for making graphs, it is also really useful as a simple programming language and compiler. This means that we can write computer programs in the R language. In the context of microbial ecology (and biology in general), a useful application of these programs is to generate simulations that are representative of mathematical models. If we know the processes that underlie a particular biological pattern and the relationships between processes, we can write mathematical formulas and try to predict how the system behaves. We have discussed this in the class in terms of population growth models, and we will revisit this when we talk about species interactions. Because the programs you write can then incorporate other R functions, they can often be incredibly useful for analyzing and visualizing simulated data.

Additional resources in R programming:  
•	Learn R Programming: the definitive guide. https://www.datamentor.io/r-programming/

## 1. Introduction to basic R functionality

### Functions
The first thing to remember is that R really is just a bunch of smaller programs that have already been written in to one package for you to use. As an example, we can enter a column of numbers by typing: 

```
data1=c(3,5,2,6,4,6) 
```

We could calculate the average number by typing: 

```
(3+5++2+6+4+6)/6
```

And the computer should return: 4.33333.
Of course, you can make it more elegant by referring to your object:

```
sum(data1)/length(data1)
```

And you should get the same result: 4.33333. 
Even more! You can calculate the mean directly with the function:

```
mean(data1) 
```


And, again, the computer should return: 4.33333.

In this case, R already has program written to determine averages. By typing “mean” you called up that program, which simply adds these numbers and divides by the sample size. Because this program can be called by a single name, it is referred to as a function. 
R comes with a huge number of built-in functions, especially to do graphics and statistics or you can use it to write your own programs and functions, which can incorporate programs already built into R. 

### Task1. Because of all of these functions, you typically do not have to reinvent the wheel when coding, and instead develop skills in understanding what functions do and learning about new functions as you go.
a)	In your own words, explain what the functions ‘sum’, ‘length’ and ‘mean’ do. 
b)	How do you figure out what a function does?
c)	How do you find whether there is a function that does something you need to do?

### Example: diatoms
Here is an example of other functions, that draw an XY plot for us, using data from measurements of diatom counts using microscopy and chlorophyll quantification using high performance liquid chromatography. 

```
diatom_counts=c(0,1,2,3,4,5,6,7,8,9,10) 
chlorophyll_data= c(0,0,0,3,9,13,15,19,21,24,27) 
chl_mean=mean(chlorophyll_data) 
plot(diatom_counts~chlorophyll,typ="b",col=3) 
```

Now let us go a little deeper into this example. 

Imagine we did a series of experiments and established a morphometric physiological relationship between the number of diatoms and the available chlorophyll in samples taken across 4 different lakes in California. The mathematical relationship that most closely describes this phenomenon is

chlorophyll= 3^(diatoms – 2)


Now we want to know how these parameters affect the rate and how the data would look if we just keep giving adding diatoms to a lake. How do we go around testing this? We will need to run the expression we just wrote many times in a row, and record the output, then plot. 

### Task2. Write the expression above in R. Then, use it to calculate the chlorophyll when you add 1, 13, and 100 diatoms to a water body. 

a)	Make an object with all these numbers for chlorophyll_data: 

To help you get started:
```
diatom_counts=c(1,13,100)
chlorophyll=c(0,0,0)
chlorophyll[1]=3ˆ(diatom_counts[1]-2)
chlorophyll[2]=3ˆ(diatom_counts[2]-2)
chlorophyll[3]=3ˆ(diatom_counts[3]-2)
```

b)	Then plot against your diatom_counts. 
c)	What does this tell you about the relationship between diatom abundance and chlorophyll?

### Continued example: Diatoms
Realistically, 1-100 diatoms will be too little to be detected on a lake, and you could keep going to unrealistically high numbers, so there may be some limits as to the range of parameters that our function can predict. But the point is that using simulations allows us to explore range of parameters that are difficult to find in nature. However, if we wanted to explore the parameter space (many more combinations of data) it would take us lines and lines and lines of repetitive code. There has to be a better way to do this! Remember this is all about working smarter, not harder.

## 2. A simple program of population growth
We are interested in population size and so often make programs that simulate populations growing or interacting through time. There are tools in programming that will allow us to simulate many different combinations of data and explore the parameter space without having to repeat the same lines of code. Here we explore some of these. 

### Loops1
Loops are used in programming to repeat a specific block of code. Assume that we start off with one bacterial cell and it doubles during a given time interval. We could do this in R by just keeping track of population size N: 

```
N =1
N = 2*N 
print (N) 
```

Each previous N gets replaced by the new population size N. Now, just repeat this, with both bacterial cells dividing: 

```
N = 2*N 
print (N) 
```

We could do this over and over, but it gets a little boring, so let’s create a “for loop” to do this "for" us. Loops are very important for programming, so it is very important that you understand their structure and use. 

```
N =1
for (i in 1:10) { 
	N = 2*N 
print (N) } 
```

Notice that when you print brackets, you will get a plus sign in your console output (‘+’), this is just the prompt R uses when it prints unfinished lines of code that occupy several lines. In this case it refers to the open bracket, and it will keep printing ‘+’ until you close the bracket. 
Troubleshooting trick: If you leave an open bracket you can get stuck on lines that start with ‘+’ and don’t really go anywhere. To return to a regular output, just press the escape key (‘ESC’). 

You can see that the “for loop” simply repeats the actions in the curly brackets as many times as you wish: in this case, 10. Note the use of tabs to set the bit of code within brackets off to the right a bit. You should do this -- it makes your code much easier to read later. 
Note that we have the “i” value, which actually increases from 1:10 each time we go through the loop. Let’s put it to work to put our results in a column, with each row determined by “i”: 

```
N = rep(0,10)   #this creates an column or "vector" of 10 zeros.
N[1]=1   	#now we make the first number in the column equal to 1 

for (i in 2:10) { 
	N[i] = 2*N[i-1] 
	print (N[i])
} 
```

Remember that R knows to ignore everything typed on a line after it encounters a "#" symbol, which is convenient for adding comments to code. Don't be afraid (or too lazy) to do this -- again, it can really help to later figure out what you were trying to do. 

All of our results are now in a column, which we can see by just typing “N”, you should get: 1 2 4 8 16 32 64 128 256 512 

Task3. Describe in words what loops do. Use the previous example as a guideline and make sure you can explain what is happening at each line. 

### Loops2
Even better, we can now plot our results to see what is happening to our bacteria through time. But, we haven't really kept track of time per se, although it is equal to i each case in our loop. So, let's create another vector "generation" and set it equal to i each pass through the loop, then plot population size (N) against generation: 

```
N = rep(0,10) 
generation=rep(0,10) 
N[1]=1 
generation[1]=1 
for (i in 2:10) {
			N[i] = 2*N[i-1] 
			generation[i]=i 
			print (N[i])
			} 
	plot(N~generation) 
```
If you wrote this on your own, you will have written your first program. Congratulations! It simulates bacteria growing exponentially through time, doubling every generation. These bacteria are following the general equation: 
Nt+1 = Nt*2

### Task4. In your own words, explain how the loop portrays this equation. Then, explain how it records the data for plotting.

### Loops3
Now, we could begin to make this program a bit more flexible and, therefore, useful for other situations by adding some generic variables. First, we might want to run this for more than just 10 generations, so let's make the number of generations a variable in the program: 

```
num_gen=10
N = rep(0,num_gen) 
generation=rep(0,num_gen) 
N[1]=1 
for (i in 2:num_gen) { N[i] = 2*N[i-1] 
			generation[i]=i 
print (N[i])
		} 
	plot(N~generation) 
```

We could also create a constant for the population growth rate, which is currently 2.0, to make our program a bit more flexible to use. 

In later sessions, we will learn how to turn this into a function. This will reveal one of the most powerful aspects of coding: you can craft specific tools to solve your research problems.

### Task5. What is the usefulness of creating variables? How does this increase the flexibility of your code? Hint: think about the time in the near future when you have to reuse this code.

## This is the end of the tutorial
Good job! You have completed your first coding session in R. 
** Make sure you save your files 
See you soon!. 

