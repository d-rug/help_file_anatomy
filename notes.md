# Notes for Anatomy of a Help file

## Setup

``` r
library("sf")
library("forcats")
```

## Getting Help

Most builtin R documentation is centered around functions.

Search within loaded packages:

-   `?summary`
-   `help(summary)`
-   `?sf-package`

Search within installed packages:

-   `??summary`
-   `?linear model`
-   `help.search("linear model", fields = "title")`

Search the internet:

-   CRAN and Bioconductor
-   `RSearchSite()`
-   rdocumentation.org to search cran and bioconductor
-   rdrr.io - to also search rforge and github

You might run into duplicate documentation `?filter`

## Definitions

### Functions

-   pre-programmed set of instructions to the computer
-   `sqrt()`
-   `length()`

### Arguments

-   input to a function, contains info function needs to work
-   almost all arguments have names
-   first three arguments to `lm` are `formula`, `data`, and `subset`
-   `sqrt` argument is `x`, not very informative, need help files

### Objects

-   everything is an object
-   when you create a variable you create an object
-   see objects in evironment tab, also `ls()`
-   `x=5`, `hi = function() print("Hello, world!")`
-   built in objects, `iris`


### Classes

-   blueprint for structure of an object
-   tells the computer how to interact with that object
-   `class()`, x, mtcars, hi, 'hi'


### Methods

-   function that is defined for a particular class
-   `st_area` - calculates area of shapes, but must be class `sf`, which stores geographic information
-   R assumes first argument is class `sf`, test with 5
-   Some functions have methods for different classes
-   `methods(summary)`, for packages we've loaded
-   `summary.lm`
-   This is important, ask if you have questions

## Reading a help file

Whole bunch of sections. The ones you will always see:

-   Title
-   Description
-   Usage
-   Argument
-   Return (almost all of the time)
-   Examples (extremely common in base R and well used packages)

### Title

-   Name of documentation page (not always name of function, `?min`)
-   Name of package (base is base R)
-   Also don't have to load stats, graphics, utils, datasets, methods, and grDevices, so you don't need to load them.

### Description

Tells you what the function does in general. Good for figuring out if it's worth spending more time reading about the function.

### Usage Section

-   Useful for troubleshooting, difficult to interpret
-   Gives an example function call with argument names, and default values
-   `=` means default value, don't need to provide
-   `?read.csv`
-   Different functions may have different argument requirements and different default values
-   sep, "", vs ",", and header

Muliple function calls for the same function

-   `summary()`
-   multiple methods for the same function documented in the same file
-   Look for the class to know which default values are used

Summarize General Social Survey category data as a data.frame:

``` r
summary(gss_cat)
```

Summarize GSS religion as a vector:

``` r
summary(gss_cat$relig)
```

Why? Maybe `maxsum` arg, but will need next section to be sure.

### Arguments

-   Lists out names and descriptions of all arguments, including class requirement
-   Section I most commonly use for troubleshooting
-   Not all arguments will be used necessarily be used for each function documented
-   Look at `maxsum` description in Arguments

#### The `...` Argument

-   Not all arguments have names
-   Unnamed argument = `...`

Two reasons:

1.  Don't want to restrict number of args

    -   `sum(1:10, 99, 21:91, -39:45)`
    -   `data.frame(1:12, month.name, month.abb)`

2.  Allow Future development of methods

    -   Ex `plot()`
    -   super useful functionality,
    -   many things to plot besides just base R stuff

``` r
#read in North Carolina data
nc = st_read(system.file("shape/nc.shp", package="sf"), quiet = TRUE)

#class of data created using sf package
class(nc)

head(nc)

?plot()
```

Open up help file and we have soem additional options
  
  - `key.pos`: specify where the legend is
  - `logz`: plot z value on log scale
  - `main`: include title


``` .R
plot_title = 'Live Births in North Carolina from 1974-1978'

plot(nc['BIR74'], key.pos=1, logz=TRUE, main=plot_title)

```

### Details

-   Important information not already stated
-   where I go when I can't easily solve a problem
-   covers "behavior" of a function, how it works for different classes or with
different arguments
-   `?var`, `pairwise.complete.obs` only works for `method='pearson'`
-   mathematical formulas, like `?dist`

### Value

-   Tells you what the function returns
-   Should at minimum include the class, 
-   if you assign function to variable, this is what gets stored in variable
-   If nothing is returned (see `?str`), it could note this or be missing

### Note

-   `?data.frame`
-   Like details but less widely applicable
-   If using `R 2.4` or earlier, rownames must be character vector for 
    data.frame
    
### Authors

-   `?lm`
-   Who wrote the function
-   More common in packages but not unheard of in functions

### References

-   `?lm`, or `?data.frame`
-   If function implements algorithm developed elsewhere, this will contain
    the citation

### See Also

-   If function you are looking at doesn't do exactly what you want, look at 
    See Also
-   Functions that are similar to the one you are investigating
-   Implement a modified formula (weighted means)
-   Work for different class (summary for glm)
-   List of methods that can be used with a class (lm)


### Examples

-   Number 1 section if you are a beginner or are totally confused
-   Not sure why they put it at the bottom
-   Contains example code that will run on any computer, without loading any
    more packages or data
-   just direct copy/paste
-   `?summary`, investigate `digits`
-   modify arg to see what changes
-   Won't to exactly what you want right off the bat.
-   Use code as a starting point, something that doesn't immediately spit out an
    error message.
