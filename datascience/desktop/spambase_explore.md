# Explore the Spambase Dataset 

Let's examine the data and do some basic machine learning by using R. The DSVM comes with CRAN R pre-installed. 

To get copies of the code samples that are used in this walkthrough, use git to clone the Azure-Machine-Learning-Data-Science repository. Git is preinstalled on the DSVM. At the git command line, run: 

```bash
git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git 
 ```

Open a terminal window and start a new R session in the R interactive console. To import the data and set up the environment: 

```R
data <- read.csv("spambaseHeaders.data") 
set.seed(123) 
```

To see summary statistics about each column: 

```R
summary(data) 
```

For a different view of the data: 

```R
str(data) 
```

This view shows you the type of each variable and the first few values in the dataset. 

The spam column was read as an integer, but it's actually a categorical variable (or factor). To set its type: 

```R
data$spam <- as.factor(data$spam) 
```

To do some exploratory analysis, use the `ggplot2` package, a popular graphing library for R that's preinstalled on the DSVM. Based on the summary data displayed earlier, we have summary statistics on the frequency of the exclamation mark character. Let's plot those frequencies here by running the following commands: 

```R
library(ggplot2) 
ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25) 
``` 

Because the zero bar is skewing the plot, let's eliminate it: 

```R
email_with_exclamation = data[data$char_freq_exclamation > 0, ] 
ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25) 
```

There is a nontrivial density above 1 that looks interesting. Let's look at only that data: 

```R
ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25) 
```

Then, split it by spam versus ham: 

```R
ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) + 
geom_density(lty=3) + 
geom_density(aes(fill=spam, colour=spam), alpha=0.55) + 
xlab("spam") + 
ggtitle("Distribution of spam \nby frequency of !") + 
labs(fill="spam", y="Density") 
``` 

These examples should help you make similar plots and explore data in the other columns. 