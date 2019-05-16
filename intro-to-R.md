---
layout: page
title: inteRise 101: Intro to R
permalink: /intro-to-R/
---

__by Zach Wulderk__
__zwulderk@interise.org__

## The Basics
### What is R?
R is a programming language and statistical program that works very well for working with data. Think of it as a much more powerful version of Excel with many more bells and whistles. 
### Why R? 
R is able to do all sorts of things, ranging from data cleaning to graphing to browser automation to creating interactive dashboards. If you currently do something with Excel or Stata, or if you repeat a process like searching for data, or if you just want some cool graphs/maps to play with, R can probably help you out. It is very flexible and simultaneously very powerful, and it is open source, which has two primary benefits. First, R is completely free, unlike Microsoft products, Stata, SAS, etc. Second, independent developers can create publically-available packages for use by R users. These are similar to plug-ins, allowing a user to perform tasks much more simply than if they had to devise the code themselves. Think of it like crowdsourcing plug-ins to make your life easier. 

RStudio is an interface that makes the R user experience much simpler and easier. It enables to view and edit our code in an easier way, visualize our environment, view our data, and more.

## Getting Started
### Installing R and RStudio
Although we will be using RStudio, we first need to download R itself. RStudio is basically a program you use to interact with R.  
__Installing R__
1. Navigate to the [R website](https://cloud.r-project.org/) and download the newest version of R for Windows. 
2. Once the installer is downloaded, run it.  
  
__Installing RStudio__
1. Navigate to the [RStudio website](https://www.rstudio.com/products/rstudio/download/) and download the newest version of RStudio for Windows. There may be a few options, in which case download the RStudio Desktop version that is free. 
2. Once the installer is downloaded, run it.

### Intro to RStudio
__INSERT IMAGE OF RSTUDIO QUADRANTS__  
  
__File Viewer - 1__  
Much of the work we do in R is done in the File Viewer. This is where we write the documents containing our code ("R Scripts") and where we can browse our data. Writing scripts allows you to save your code so that you can just press "Run" whenever you need the steps to be re-run.
  
__Environment Viewer - 2__  
The environment viewer is where you can see everything you have in your R environment. For example, if you read in Salesforce data and call it `df`, the environment will show you that you have loaded it as well as its dimensions (e.g. 1,000 rows and 20 columns). This will help you keep track of your work.
  
__Console - 3__  
The console displays output from your code and allows you to run one-off commands not from your scripts. For example:
```
> 2+2
[1] 4
```
  
__Viewer - 4__  
The viewer is where you can see your file directory, any graphs or plots you have made, your help window, and more.
>> Tip: If you run into an issue with a function, you can type `?function` into the Console (where `function` is the name of the process you are having an issue with), press Enter, and a help file will appear in the Viewer.  
>> 

From this point forward, when I refer to "R," I will generally be referring to RStudio, because this is how we interact with R.

## Writing Code  
### A Quick Exercise
Before we get started with explaining R syntax, let's write your first line of R code. In the console, type:
```
print("hello world!")
```
When you press Enter, R should return `[1] "hello world!"`. What this function tells R to do is to print (hence the function name `print`) whatever is inside the parentheses to the Console. We use quotation marks to indicate that the phrase "hello world!" is a _string_, or text characters.

### Thinking Like A Machine
The title of this section might sound a little Skynet, but really what we want to do is understand how R interprets code. The most important aspect of writing code is to be able to understand how to go about translating from human to computer.  

R is a functional programming language, which basically means that you will be telling the computer to run a function in order to accomplish a task. In the `hello world!` example, you told R to run the function `print()` in order to accomplish the task of writing to the Console. Because R is built around functions, it is important to understand how they work so that you can use the ones you know and learn how to use the ones you don't.

As I mentioned the tip above, typing `?` before any function name and running that line in the Console will provide a help file for understanding the function. If `?` does not work, you can try a broader search by using `??`.  
  
Let's look at the help file for `print` by running `?print` in the Console. The title of the function is __Print Values__, which makes sense. The description says "`print` prints its argument and returns it _invisibly_ (via `invisble(x)`). It is a generic function which means that new printing methods can be easily added for new `class`es." That's not super clear. Let's look under Usage instead. We see `print(x, ...)`, but what does that mean? Scrolling down to Arguments, we see `x` is "an object used to select a method" and that `...` is "further arguments passed to or from other methods." So `x` is just an object and `...` is anything else we want to tell R to do. Since we only want it to print an object -- in our case, the string "hello world!" -- we can ignore `...`. In R, just like in algebra, `x` often works like a variable that can take on any value. In this case, we just replace `x` with whatever we want to `print` - in our case, `"hello world!"`  
    
Help files like this will help you decode the way that R thinks of its functions.

## Nesting Functions
Just like in Excel, you can _nest_ functions in R. To demonstrate that, let's first quickly learn about the functions `paste` and `toupper`.  
  
__`paste`__
The Description of `paste` (`?paste`) says "Concatenate vectors after converting to character." This means that `paste` combines character vectors. Under Usage, we see `paste(..., sep = " ", collapse = NULL)`, where `...` is `one or more R objects, to be converted to character vectors`, `sep` is `a character string to separate the terms` and `collapse` is `an optional character string to separate the results.` Because `collapse` is optional, we will ignore it. In Usage, we see that `sep = " "`, which means that by default, `paste` will separate objects with a space. For example, `paste("a", "dog")` will result in `"a dog"`. We can change the value to a comma, for example, by writing `paste("a", "dog", sep = ",")`, which will result in `"a,dog"`.  
  
__`toupper`__   
`toupper` is a simple function that converts the text it is fed to uppercase. For example, `toupper("the")` will return `"THE"`. 

__Nesting__  
Nesting functions just means putting one function inside another. Say we have the strings `"happy"` and `"birthday"`. If we want to combine them into a single string, we could say `paste("happy", "birthday")`, resulting in `"happy birthday"`. Birthdays are exciting though, so let's make our Console look more exciting by running `toupper(paste("happy", "birthday"))`. That's more like it. In this example, the `paste` function is said to be nested inside the `toupper` function. This allows us to combine multiple functions in a single line of code.

## Objects
### Intro to Objects
There are many different types of objects in R and I won't be listing them all out here, but some examples include dataframes, vectors, and lists. Even functions are a type of object. One of the features that makes languages like R so powerful is their ability to store values in objects. For example, the line `foo <- 1` creates an object called `foo` with a value of `1`. Running that line followed by the line `foo + 2` gives us `3`. This way, we don't have to continuously type `1` because we can assign it to the object `foo`. If we later decide to change `foo` to `42`, `foo + 2` will still work but will return `44`.  This is especially useful for longer strings and more complex objects like dataframes.  
  
The `<-` operator is basically an arrow assigning everything to its right to the object on its left. So `foo <- 1` means "assign to the object foo the value 1" or, from right to left, "store the value 1 under the name foo." 

### `cars` and vars
One of the most common objects you'll work with is the dataframe, which is basically a fancy version of an Excel spreadsheet. 
>>Tip: A common convention in R is to use `df` as the name of a dataframe. If you see an object called `df`, it is a safe assumption that is a dataframe. One way to confirm this is by running `str(df)`, which will show use the __str__ucture of the `df` object. 

R comes with many pre-made tools to test out functionality, and one of them is the `cars` dataframe. To see what it looks like, run `cars` in your Console. Running `str(cars)` confirms that it is a dataframe. Running just `cars` again, you should see three columns printed: one which has no name and is the numbers 1-50, and two columns named `speed` and `dist` with some random numbers. This is just like an Excel sheet, where the numbers on the left are just row numbers and where `speed` and `dist` are columns containing values. 

What if we only wanted to see the `speed` column (or _variable_) inside the `cars` dataframe? This is where the `$` operator comes in. `$` is essentially an extraction operator, which means it looks inside an object and retrieves something from within. It works by looking in the object to its immediate left for something inside it that goes by the name to its immediate right. For example, to extract the `speed` variable from within `cars`, we would run `cars$speed`, which will return only the values of the `speed` variable. 

What if we realized that our speedometer was broken and really we were driving 5 units faster than we thought? Running `cars$speed + 5` adds `5` to each value of `cars$speed`. However, if we run `cars` again, we will see that the `speed` column is back to its original values. This happens because we asked the console to show us what `cars$speed + 5` would look like, but we didn't tell it what to do with those results. Running `cars$speed <- cars$speed + 5` will update the `cars` dataframe, because it is saying to store in the object `cars$speed` the values returned by `cars$speed + 5`. 

## `tidyverse` and Other Frequently Used Packages
Because R is open source, it allows you to install packages written by third parties. This allows you to take advantage of code written by other people to make your work easier. Few packages do this is much as `tidyverse`, which is really a series of packages. To install and load `tidyverse`, we run:  
```
install.packages("tidyverse")
library(tidyverse)
```
  
You will only have to install (`install.packages`) a package the first time you use it on your computer. The `library` step, which loads the package, must be run once per R session. 

Another great package is `magrittr`, which we can install and load by running:
```
install.packages("magrittr")
library(magrittr)
```
  
We can now run the following line:
```
filter(cars, speed >= 20)
```

This line tells R to take the `cars` dataframe and filter it to return only the rows for which the variable `speed` has a value greater than or equal to `20`. The `filter` function comes from `tidyverse`, and in particular, from the package `dplyr`, which is part of the `tidyverse`. Running `?dplyr::filter`, we see that the first argument is `.data`, which is "A tbl." For our purposes, it is only important to know that a dataframe is a type of tbl (an abbreviation of "table"). 

The package `magrittr` comes with a pipe operator that looks like `%>%`. What the pipe operator does is feed the object to the left of the `%>%` into the first argument of the function to the right of the `%>%`. Because the first argument of `filter` will accept a dataframe, we can write:
```
cars %>%
    filter(speed >= 20)
```
  
 What this step does is feed (or _pipe_) the object `cars` into the function `filter`. Using `tidyverse` functions and `%>%`, we can create long chains of commands that run all at once and don't require use to write the more verbose option (e.g. `filter(cars, speed >= 20)`). For example, we can use the function `mutate` to create a new variable that has units after the speed. For example:
```
 cars %>%
    filter(speed >= 20) %>%
    mutate(speed_with_units = paste(speed, "mph"))
```
This takes the `cars` dataframe, feeds into the `filter` function where only rows with speeds of 20 or more are kept, and then feeds _that_ into the `mutate` function, where a new variable called `speed_with_units` is created containing the speeds in the `speed` variable with the string `mph` after it.

Once again, this code is only showing us what those steps would do to `cars`, but if we run `cars`, we see that it has all of its rows still and no column called `speed_with_units`. We need to store it as an object to save the results. We _could_ start that block of code by writing the first line as: `cars <- cars %>%`, but that looks kind of redundant because we're saying `cars` twice. Using a compound pipe, also from `magrittr`, we can use `%<>%` to function as a sort of hybrid of `<-` and `%>%`. For example:
```
cars %<>%
    filter(speed >= 20) %>%
    mutate(speed_with_units = paste(speed, "mph"))
```
This tells are to take `cars`, run the `filter` and `mutate` steps, and store the results back in the object `cars`. You may have noticed that the regular pipe `%>%` points to the right and the assignment operator `<-` points to the left. Because the compound pipe operator `%<>%` is a hybrid of the two, it points to both the right and the left.

>>Tip: Lines of code with a `#` at the beginning will be ignored by R. These lines function as comments that allow us to write messages explaining what the code is doing, offering warnings, etc.  
  
>>Tip: If you are running code from a script rather than in the Console, you can run multiple lines at once by highlighting them and pressing 'Run' or ctrl+Enter. You can run the _entire_ script by making sure you have nothing highlighted and pressing 'Run' or ctrl+Enter. In other words, R will run whatever is highlighted unless noting is highlighted, in which case it will run everything.  
  
>>Tip: If help files alone are not explaining something clearly, Google is very useful. R has a thriving community online, and you can often find an answer to your question on a StackOverflow post or through some sort of guide, tutorial, or YouTube video. For a more thorough explanation of R in general, see https://adv-r.hadley.nz/, which is an online version of the book 'Advanced R', written by Hadley Wickham. Hadley is a big deal in the R community and is the author of many of the `tidyverse` packages. 
