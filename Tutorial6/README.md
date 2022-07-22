# Tutorial 6: Basic statistics in R
Based on a document created by: Casey terHorst
Edited by: CCG 2021

Most of us want to get quickly into managing the data and using stats to test our hypotheses. In this tutorial we will jump right into it. Notice this is not another statistical class and we will not attempt to go in any depth into the statistical background of these tests, but instead look into their practical application in R. In my experience, statistics comes more naturally once you start playing with data and attempting to find biological meaning.

Some recommended resources to refresh and advance your skill in Statistics (and in R):
* [Scofield 2014. Math143: ANOVA lesson](https://sites.calvin.edu/scofield/courses/m143/materials/handouts/anova1And2.pdf). Calvin University. You can find this one attached in your Canvas page for this activity.  
* [Gimond. Stats with R](https://mgimond.github.io/Stats-in-R/index.html)
* [Webb and Pajak](https://homepages.inf.ed.ac.uk/bwebb/statistics/). STA102: Anova in R. University of Edinburgh. 

## The Data
We're going to start out working with a data file called "NFData.csv". Nanoflagellates are very small flagellated protozoans, with a size range of 2-10 um, that play an important role in aquatic foodwebs. Nanoflagellates can be autotrophic, and heterotrophic, consuming algae and bacteria, thus participating in many different pathways. This data set has nanoflagellate counts (heterotrophic- HNF and autrophic - ANF) from the high and low intertidal, at two locations: San Diego and Monterey, CA. We want to know how their counts differ across sites and habitats as a way to understand the balance between respiration and photosynthesis in microbial dominated ecosystems.
Download this dataset from the Canvas page, and make sure it is saved to your Rtutorial directory (Recommended: create a folder called ‘Rtutorials_MicrobEcol2020’ in vlab) before you start. 

## Good practice tips
We are going to start saving our coding script for later use and making notes in our code to provide information regarding what we are doing to anyone that may use our code later on. I have found that the person that uses my code later on is mostly me, so I try to be nice to future me and make really good notes (you will thank yourself!). Remember from tutorial 1 that RStudio is divided in four sub-windows: source, console, environment and files. Get into the habit of writing clear, annotated code in your source panel and saving it regularly. In this tutorial, you will analyze nanoflagellate data and annotate your code. 

Important! Do not copy and paste, do not limit yourself to reading the content. You MUST type each command and try it out. The only way to learn coding is by coding. 

### 1. Preparing your working environment
Open R and set your writing directory to ‘Rtutorials_MicrobEcol2020’. Follow the instructions on Tutorial 3 if you cannot remember how to do this (ask questions if you need help!). Double check you are in the right writing directory by using the command 

```
getwd() 
```

Then begin your script with some information. Use the hashtag to begin inputting text that will not run in the console. Include the author’s name, the date, and a one-sentence description of the goal of this script. Here is mine as an example:

![Fig0](/tut6_figs/fig0_scripthead.jpg)




Next, load the data using read.table(). We will call this table ‘NFData’. The file should be called ‘nanoflagellates.txt’. Remember to check Tutorial 2 and use help(read.table) or ?read.table if this is not working (and ask for help!). There are also some hints to troubleshoot importing issues at the end of this document.

You want to check that the data was imported correctly, so type the name of the table. 

```
NFData=read.table(nanoflagellates.txt, header=TRUE)
NFData
```

You can also decide to look at only one of the columns, for example, to focus on the heterotrophs.

```
NFData$HNF
```

#### Task 1. Super easy, write the expression to look only at the column with autotrophic nanoflagellates. Too easy?

### 2. Review of Objects in R and broad stats
So far, you have been giving names to some lists of numbers and tables with information. In the context of coding, remember that these are called ‘objects’. Objects can hold from one digit number to very large DNA sequences, have numeric or character (letters) information and be organized in lists, vectors, tables and matrices. It is a good idea to store important information in objects, and give them meaningful names to keep your code organized. 

For example, lets process some of the nanoflagellate data and create some objects from it. If we want to calculate the mean number of heterotrophic nanoflagellates across habitats and sites, we would write:

```
mean(NFData$HNF)
```

You should get a numeric value that represents the mean of the heterotrophic nanoflagellate observations.

Uh oh, run into a problem? What happened? Try to interpret before you move on. 
…
…
… 
You probably figured it out: we got an NA as output, which probably means there's an NA in our dataset – NA represent missing values. You can either go back and edit your table (boring), or work around the missing data in R. For example, start by identifying the problem and find the NA in question, then figure out how to run the function mean() while avoiding the NA.

```
NFData$HNF 		# you can scroll to find the NA
is.na(NFData$HNF)	# you can ask R to find it for you – it will print a logical output, TRUE for the NA
which(is.na(NFData$HNF)) # you can ask R to tell you what position the NA is in
# How to implement within the mean() function?
mean(NFData$HNF, na.rm=TRUE) # you can use this option: na.rm removes any missing data
```

You should get a mean value of 196.4103 heterotrophic nanoflagellates per observation.

Even better, we can store this mean, as an object for later use:

```
meanHNF=mean(NFData$HNF)
```

We can follow a similar approach to calculate the standard deviation:

```
sdHNF = sd(NFData$HNF, na.rm=TRUE)
sdHNF
```

And standard error of the mean (S.E.M.)

```
seHNF = sd(na.omit(NFData$HNF))/sqrt(length(na.omit(NFData$HNF))) # what are we doing here? Try to decipher this one
```

#### Task2. Calculate the mean, standard deviation and SEM for the autotrophic nanoflagellates. 
A)	Show your results
B)	How do these numbers compare to heterotrophs? 
C)	Which group is more abundant? 
D)	Which group is more variable?

### 3. Group stats
Most of the time, we are less interested in broad means and more interested in comparing means across locations or treatments. In this case, we use the function tapply():

```
tapply(NFData$HNF, NFData$Location, FUN = function(x) mean(x,na.rm=TRUE))
tapply(NFData$HNF, NFData$Location, FUN = function(x) sd(x,na.rm=TRUE))
```
Here HNF (heterotrophic nanoflagellate counts) is the measurement you're interested in, and Location is the grouping variable, and mean is the function you want to perform. 

Let's say we want to be able to quickly call the mean length of just San Diego data, we would use the following code. Notice you have to run this whole code together (these are not two separate lines).

```
SanD_HNF = tapply(NFData$HNF, NFData$Location, FUN = function(x) mean(x,na.rm=TRUE))["SanDiego"] 
```

Or, we can name the Monterey length mean, by looking at the first item ([1]) of the tapply() output:

```
Mont_HNF<-tapply(NFData$HNF, NFData$Location, mean(x,na.rm=TRUE)[1]
```


#### Task3. Now its your turn to do the same with the autotrophic nanoflagellates. Find the means per location.

By now, you should know how to calculate the mean, standard deviation and standard error of the mean for heterotrophic and autotrophic nanoflagellates. We should organize this information in a table that is easy to access and observe. We could do this by location or tidal height, but for now, we will take the easy route and just show the means and standard deviation for autotrophs and heterotrophs. 

#### Task4 (and this is a tricky one). Make the table! There are different ways to do this: try to think about the different skills you have been learning and how to put them together. 

Some quidelines: 
1. Complete calculations to have each statistical parameter (mean, standard deviation) for each group (heterotrophic and autotrophic nanoflagellates).  
2. Use c() to concatenate (join) values in a vector. Start by concatenating the statistical parameters for heterotrophic nanoflagellates. Then, do the same (in the same order) for autotrophs.  
3. Use rbind() to join the two vectors you created in (2), thus creating a table.  
4. To change the names of your columns, colnames(). Use the help feature to figure out how they work.  

If you are stuck: check Appendix 2 for possible solutions.

### 4. ANOVAs
From your previous statistical classes, you have encounter Analysis of variance or ANOVAs before. This analysis tool considers a quantitative response variable as it relates to one or more explanatory variables that are usually categorical. This test is an extension of your traditional 2-sample t test, in the sense that it allows you to compare more than 2 explanatory variables. How do you compare them? You ask whether the variation between groups is higher than the variation within groups, allowing you to differentiate between the following statistical hypotheses:

Ho: the means or all groups are equal
Hi: the means are not all equal (some are different)

  
![Fig1](/tut6_figs/fig1_vardist.jpeg)

Figure1. Example of variance distribution a) compared to the grand mean and b) compared to each explanatory variable’s mean. If the variance calculates in (a) and (b) are similar, Ho cannot be rejected. If the variance in (a) is higher than in (b) there potential significant differences between the means of the explanatory factors (but you don’t know which ones are different yet). Taken from Gimond Github. 


For relatively simple ANOVAS we can simply use the command aov(). The general form is aov(dependentvariable ~ factor 1 + factor2...). You must also specify which data set to use. Because we have NAs in our data, we need to specify to ignore those too. Note that different commands remove NAs in different ways. For aov, it works like this:

```
myanova2=aov(HNF~Location*TidalHeight, na.action=na.omit, data=NFData) # simplified way to write it
```

Great, we've made our model. But there's no output! The command above just fits the model. It doesn't actually calculate any statistics. To do the stats:

``` 
summary(myanova1)
summary(myanova2) # this should be exactly the same
```

What does this output mean? 
Figure 2. This is an example output from an ANOVA test in R. In this dataset, they used a spray treatment to eliminate insect pests and compare the counts of insects to an untreated control. The F value represents the statistic (we will not go into detail here, but we encourage you to review how it is calculated and how to interpret the number!). The p value gives you an indication of how significant is the difference in variances. The smaller the p value the more likely your groups have different means. From Webb and Pajak: Anova in R. 

Use this link to figure it out: http://homepages.inf.ed.ac.uk/bwebb/statistics/ANOVA_in_R.pdf
Remember that there are a LOT of resources for R online. To be successful, get used to google and re-google any questions you have. You do not have to reinvent things that are already explained clearly somewhere. And you will get better at searching and reading answers.


An ANOVA can be equivalent to an analysis of variance on the output of a linear model with normal distribution and categorical independent factors:

```
Mymodel=lm(HNF~Location*TidalHeight, data=NFData, na.action=na.omit)
summary(mymodel)
anova(mymodel) # this should thus be the same output as above or very close
```


#### Task5. Now set up a similar ANOVA model for ANF (you can choose which of the functions you prefer – they should all give you the same answer). Use the output of your model to answer the biological question: what is more important to determine autotrophic nanoflagellate abundance, tidal height, location or their interaction?


### Plots in R
Let's make some simple plots to visualize this data. If we want to just plot ANF vs HNF:

```
plot(ANF~HNF, data=NFData)
``` 
Since this plot represents a correlation between autotroph and heterotroph abundances, we can assess their linear relationship with a linear regression and Pearson’s correlation coefficient.
```
lm.nano = lm(ANF~HNF, data=NFData)
summary(lm.nano)
corr.nano = cor.test(x=NFData$ANF, y=NFData$HNF, method = ‘pearson’)
```

Just as we saw in the ANOVA output, the summary of the linear model shows us a statistic (t value in this case) and a p value corresponding to the significance of the relationship. P value was below 0.001, indicating that heterotrophic and autotrophic may be indeed positively correlated (notice the estimate value is 0.96571, a positive value for the slope of the relationship). This is confirmed by the R-squared value, which is 0.9597, pretty good correlation!
We confirmed with a Pearson’s correlation coefficient calculation that gave us also a p value below 0.001 of a tight relationship.

#### Task6. What does this mean biologically?  What is the biological insight we can get from this plot and stats? What does this say about the relationship between heterotrophic and autotrophic nanoflagellalates? Based on your knowledge and understanding of microbial ecology, formulate an explanation. 


#### Epilogue
Now you may be asking why did we take all of this data across two locations and two habitats (intertidal and subtidal) if all we wanted was to know the relationship between heterotrophic and autotrophic nanoflagellates? Well, let me jump to the punch line and tell you that the location and habitat do not matter in this system, and this relationship holds constant. 

Oh you say you don’t believe me without proof? Well, check these plots out then (feel free to use the appropriate ANOVAs to test their relationships too if you wish):

```
boxplot(NFData$ANF~NFData$Location)
boxplot(NFData$ANF~NFData$TidalHeight)
boxplot(NFData$HNF~NFData$Location)
boxplot(NFData$HNF~NFData$ TidalHeight)
```

There are many more options to be explored in this default plot function. Feel free to try it out following guidelines from these sites: 
•	Understanding plot() by [JournalDev](https://www.journaldev.com/36083/plot-function-in-r)
•	The plot() function -plotting points and lines by [CountBio](http://www.countbio.com/web_pages/left_object/R_for_biology/R_fundamentals/plot_parameters_R.html)
•	Graphical parameters by [QuickR](https://www.statmethods.net/advgraphs/parameters.html)
•	Line charts by [QuickR](https://www.statmethods.net/graphs/line.html)


Do not forget to check Apendix 1 for an introduction to R packages if you want to dig deeper into functionality (we will have to use some of these later), and Apendix 2 for tips to solve Task4. 


## APENDIX 1
All we have done so far is using the base default R functions to organize and analyze our data. That is ok, but now feels a bit old-fashioned. Now everybody is talking about advanced methods and functions to manipulate and organize data, even large amounts of data that you could never be able to look at in your excel sheet! And this is where the real power of coding comes into play. Luckily, you do not need to reinvent code that other people have already developed. For example, everyone is now into using the tidyr and dplyr packages. These chunks of code
help you maintain and organize your data by keeping it ‘tidy’. But first let’s talk about what packages are and how to get them.

### R packages
R packages are free, reusable R functions and documentation that describes how to use them. Because anyone can create and share their packages, they are very useful in increasing the capability of R and adding you your toolset. For each package, you will need to install the files in the computer (function ‘install.packages’) and then load them into your R working environment (function ‘library’). 

Note: if you are using your own computer, you may find some issues in installing R packages related to the version or R or R studio you have. There are ways around that, but it takes some time to troubleshoot. We recommend you switch to vlab or access the HSU computer labs to avoid these issues. 
Some further information on installing packages can be found in the data camp website:
Data Camp. 2019. R Packages: A beginner’s guide. Access here.
 
#### Example
For example, this is a more specialized function to do the same ANOVA you did earlier, but it has more flexibility to establish your experimental design and query:

```
install.packages('car')
library(car)
Anova(mymodel) 
```

IMPORTANT: Notice that the first function requires ‘ ’ around the package name, but not the second one. This type of detail is hard to keep track of, and easy to make mistakes on. Make a note on your coding notebook about it to remember. You will get good at spotting these details soon!


### Taking tydr and dplyr for a spin

Tidy data is where columns are variables, rows are observations and each cell is a value. 
Learn more about the ‘tidyverse’: https://tidyr.tidyverse.org.

To install and load the package ‘tidyr’:

```
install.packages("tidyr")
library(tidyr)
```

Another useful package we will be using is ‘dplyr’, from the same developers. We would get them by typing:

```
install.packages("dplyr")
library(dplyr)
```

There are five main commands we can use:
1.	filter(): Pick rows based on conditions about their values. Useful if you want to subset your data.
2.	summarize(): Compute summary measures known as “summary statistics” of variables
3.	group_by(): Group rows of observations together
4.	mutate(): Create a new variable in the data frame by mutating existing ones
5.	arrange(): Arrange/sort the rows based on one or more variables

In tidyr language, we often use the operator %>% which you can translate as "then". It allows you to go from one step to the next. For example, let's say we just want to take a subset of just the San Diego data:

```
SDonly <- NFData %>% filter(Location == "SanDiego") 
SDonly
```

This means: take the dataframe NFData, then filter the dataframe so that we take only Locations with San Diego.

You can also do this for multiple groups: Use | for "or" and & for "and". If you wanted to subset just the Low intertidal data from San Diego:

```
SDlow = NFData %>% filter(Location =="SanDiego", TidalHeight=="Low")
SDlow
```

Use can use this to summarize some descriptive stats for our data. If we just wanted to summarize all the data:

```
Summary_nanos<- NFData %>% summarize(mean=mean(HNF, na.rm=TRUE), std_dev=sd(HNF, na.rm=TRUE))
```

#### Task 7 (optional). Use this summarize() command to find the IQR (interquartile range), sum, n (count the number of rows), minimum (min) and maximum (max) datapoints within each group (HNF and ANF) separated by Locations and Tidal Heights. This is hard, isn’t it!! It is supposed to be hard, easy things are not worth your time . See the hints at the bottom of this document if you get stuck, but try first!
Once you have figured it out, add the standard error. 

### Another fun package: ggplot
Some people prefer to use ggplot. This data visualization package breaks up graphs into semantical components or ‘layers’ that result in a very flexible and visually appealing tool for graphing. 
First you will have to install and load the ggplot package.

```
install.packages('ggplot2')
library(ggplot2)
```
Then you have to modify your data into the right format to make a bar graph. 

```
datasubset<-subset(NFData, !is.na(HNF))
data <- with(datasubset , aggregate(HNF, list(Location=Location, TidalHeight=TidalHeight), mean))
data$se <- with(datasubset , aggregate(HNF, list(Location=Location, TidalHeight=TidalHeight), function(x) sd(x)/sqrt(21)))[,3]
```

Take some time to figure out what we did there.
…
…
…
Now let’s make the plot:

```
ggplot(data, aes(x=Location, y=x, fill=factor(TidalHeight), group=factor(TidalHeight))) +
  geom_bar(stat="identity", position="dodge", size=0.6) +
  geom_errorbar(aes(ymax=x+se, ymin=x-se), stat="identity", position=position_dodge(width=0.9), width=0.1) +
  labs(x="Location", y="Number of HNF", fill="TidalHeight") +
  scale_fill_manual(values=c("Low"="tomato","High"="dodgerblue2"))
```

Wooooo that seems like a lot of code. What does it mean?

#### Task8 (optional). Try to break the ggplot code into parts. Lets start easy and build up to more difficult parts: 
a)	Where do you indicate the colors?
b)	Where do you indicate what goes in the x and y axis?
c)	Where do you indicate the height of the bars?
d)	Where do you indicate the name of the axis?
e)	What are the ‘+’ signs doing?
f)	Where do you indicate the positive and negative error bars? How do you know?



## APENDIX 2
### Annotated Solution to table in Task 4

```
# Create objects with the means of each type of organism
HNFmean=mean(NFData$HNF, na.rm=TRUE) 
ANFmean=mean(NFData$ANF, na.rm=TRUE) 

# Create objects with the standard deviations of each type of organism
HNFsd=sd(NFData$HNF, na.rm=TRUE) 
ANFsd=sd(NFData$ANF, na.rm=TRUE) 

# concatenate the stats for each organism and save the vector to a new object
ANFstats=c(ANFmean, ANFsd)
HNFstats=c(HNFmean, HNFsd)

# join the vectors as rows in a table
stats.table=rbind(ANFstats, HNFstats)

# check your table
stats.table # the column names are not pretty

# use the help feature to figure out how the colnames function works
?colnames

# change the column names
colnames(stats.table)=c('mean', 'sd')

# check your table
stats.table # now its pretty
```









