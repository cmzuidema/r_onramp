---
title: "R Packages, Files, Scripts and Sessions"
author: "Brian High, Nancy Carmona & Chris Zuidema"
date: "![CC BY-SA 4.0](images/cc_by-sa_4.png)"
output:
  ioslides_presentation:
    fig_caption: yes
    fig_height: 3
    fig_retina: 1
    fig_width: 5
    keep_md: yes
    logo: images/logo_128.png
    smaller: yes
editor_options: 
  chunk_output_type: console
---

## Learning Objectives

You will learn:

* What packages and libraries are
* How to view your libraries
* How to install and upgrade a package 
* How to upgrade all of your packages
* How to load a package into memory
* How to unload and uninstall a package 
* What an R "session" is 
* What an RStudio project is 
* How to read and write data files
* How to edit, save, and run scripts

## Packages

* Collections of code (functions), data (for examples), and documentation
* Bundled together to make for easier management
* Designed to be managed with a common set of utilities
* Almost 10,000 packages on [CRAN](https://cran.r-project.org/web/packages/)
* Most packages are written by statisticians (for better or worse)
* Most popular packages are very well documented
* In other languages, a "package" is called a "module", "class", or "library"

## R Package Libraries

In R, a "library" is a collection of packages. You use the `library()`
function to load a package from a library on disk into working memory (RAM).

A library is stored as a folder structure on your disk (or the network, etc.).


## Viewing your Libraries

If you type the command `library()` at the prompt and press *Enter*, you will
see a list of all of your libraries and their installed packages.

They will be organized by which parent folder the packages reside in. There 
are one or more "site" libraries and one or more "personal" libraries.

To see the parent folders designated as libraries for your session, use the 
`.libPaths()` command.

## Installing Packages

Before using a package, you must first install it from a "repository".

This is typically* done using `install.packages()`. 

RStudio uses the RStudio "Comprehensive R Archive Network" ("CRAN") mirror [https://cran.rstudio.com](https://cran.rstudio.com) by default, but other 
repositories can be specified.


``` r
# Example: install the "dplyr" package, using the default repository 
install.packages("dplyr")
```

Note that the package name must be quoted. 

`*` For packages from the Bioconductor project (for bio-informatics), there is 
[another method](https://www.bioconductor.org/install/) to install packages. 

## Load a package into memory

Next, you need to load the package into memory (RAM), using `library()`.


``` r
library(dplyr)
```

Notes:

* Only one package name is allowed.
* The package name is not quoted (unless you specify `character.only = TRUE`).
* There is a similar command, `require()`, that is used inside of functions.

The see the list of currently loaded packages, type `(.packages())` and include
all of those parenthesis. Or you can use `search()`.

## Upgrading and Uninstalling Packages

Packages change, and sometimes you will want or need to upgrade (update) them by running the `update.packages()` command:


``` r
# Example of package update
update.packages("dplyr")
```

You can upgrade all of your packages with:


``` r
update.packages()
```

To uninstall (remove) package, run:


``` r
# Example of removing a package
remove.packages("dplyr")
```

## Update *tidyverse* packages

If you have installed the *tidyverse* package, you can update the various 
associated packages with the following command:


``` r
tidyverse::tidyverse_update(recursive = TRUE)
```

This will check the versions you have installed against the latest available 
and will then provide you with a `install.packages()` command which you can 
copy and paste into the Console to run. That command will install only those 
*tidyverse* packages necessary to bring your library up-to-date.

## *pacman*

There is an additional package called *pacman* which makes package management 
much easier. 

*pacman* can handle all aspects of package management previously discussed using
the "base" R functions. Usually, *pacman's* syntax is easier, or involves less 
typing.

Instead of running `install.packages()` and `library()`, for each package, you 
can do it all with pacman.


``` r
# Load pacman, installing if needed
if (!require(pacman)){ install.packages("pacman") } 

# Use the pacman function `p_load()` to load multiple packages
pacman::p_load(dplyr, tidyr, stringr, ggplot2)
```

That may not seem any better than `install.packages()` and `library()`, 
because you still have to get *pacman*. But by using this approach, your script 
can run without crashing due to missing packages, as any missing packages will
be installed automatically, including *pacman* itself. How cool is that?

## R Sessions and Profiles

An R session is an instance of R running for a certain amount of time in a certain context.

For example, opening RStudio on Plasmid creates an R session.

An R session:
 
* has a working environment (i.e., the "context") with settings, data, and command history (collectively called the **_profile_**)
* starts by loading a *profile* (created for you with defaults if no custom *profile* found)
* has a collection of open data objects, called the **_workspace_**

## RStudio Projects

[RStudio projects](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects) 
are an easy way to divide work into multiple contexts. An RStudio project has its own:

* working directory
* workspace
* history
* source documents

## RStudio Projects

Using an RStudio project will ...

- make it easier to work with your files because they are in a common folder
- allow you to avoid common coding pitfalls such as:
    - using non-reproducible file paths when reading and writing files
    - having to use `setwd()` and `getwd()` to control the working directory

When you open an RStudio project, the working directory is set as the project folder.

Therefore, code you run after opening the project will use this folder as the 
working directory by default.

So, if you keep your data and other folders within the project folder, then 
the paths to these folders will be relative to the project folder.

This way, you code will be more portable and reproducible.

## RStudio Projects

Let's make a new RStudio project named "r_onramp".

File --> New Project...


## RStudio Projects

![](http://www.rstudio.com/images/docs/projects_new.png)

New Directory --> New Project

We can make "r_onramp" a subdirectory of: "~/Home" and click "Create Project"


## R Working Directory

The "Working Directory" ...

* is the folder that R is currently using to read and save files (unless otherwise specified)
* can be changed at any time with `setwd()`
* can be checked any time with `getwd()`
* starts as the folder that R was started from if run from the command-line
* starts as the user home folder or the top-level of a "project" (e.g., with RStudio)

## R Session Files

The default files for your history (`.Rhistory`) and workspace (`.Rdata`) are stored:

* **_Command-line_**: in the current working directory at the time you save (or exit your session)
* **_RStudio_**: in your home directory (`~`, H:\, etc.)
* **_RStudio_**: in the top level folder of your R project, if you are working in a project
* **_RStudio_**: locations and behaviors are in Tools -> Global Options... -> General

![](images/environment.png)

**_Summary_**: Where are they stored? *It depends*.

## R Data Files

The default data file format "native" to R is RData (rda).

Files saved in the format will usually have a name ending with `.RData` or `.rda`.

This is a "binary" (opaque) file format -- it is not to be opened with a text editor.

You can save and load data objects to and from RData files like this:


``` r
x <- 1
y <- "a"
save(x, y, file = "xy.RData")
load("xy.RData")
```

## R Data Files

It is generally a good idea to write data to a standard, "transparent" 
(i.e., plain text) format unless you have a good reason to do otherwise.

Writing to a CSV file:


``` r
# Get an example dataset to work with (more on this later!)
data("iris")

# Example of writing the dataset to a csv file
write.csv(iris, "iris.csv", row.names = FALSE)
```

Reading from a CSV file:


``` r
# Example of reading a csv file
myiris <- read.csv("iris.csv", stringsAsFactors = FALSE)
```

There are many other kinds of file formats and R can work with many of them. See:

* [Quick-R: Importing Data](http://www.statmethods.net/input/importingdata.html)
* [R-Tutor: Data Import](http://www.r-tutor.com/r-introduction/data-frame/data-import)


## R Scripts

In addition to your history file, you can also save your commands into files called "scripts".

* Scripts are "plain text" files edited in a (programmer's) text editor (**_not_** MS-Word).
* Scripts are also called "programs".
* A person who writes a script is a "programmer" - anyone can be a programmer!
* Scripts store a list of commands to be run as a batch.
* You can use a script many times to automate your work and save time and effort.


Best Practices

* Store your commands in scripts.
* Run your code from scripts instead of the prompt.
* Script your analysis to make your work more reproducible, which is very important.
* You can share your code as a script so others can verify your work.


## Creating and Running R scripts

Let's do an example of making and executing R scripts 

Go to: *File -> New File -> R Script*

A new tab should open in your Source pane "Untitled1". Lets save it as "onramp_iris_script.R".

Next, we'll add some basic information using comments like our name, date and description.


``` r
# Author: Joe Coder <joe.coder@example.com>
# Last updated: September 30, 2020
#
# This script is an example of writing scripts in R using the iris dataset.
```

## Creating and Running R scripts

Now, we can write executable code, commenting as we go to document what we're 
doing for ourselves and for others we share the code with.


``` r
# Load example data.
data(iris)

# Inspect the "top" of the dataframe.
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

## Creating and Running R scripts

Next, we'll modify the dataframe. Let's add a variable that indicates where the samples were collected.


``` r
# Create a variable that indicates where the flowers were collected. 
iris$country <- "canada"

# Show the top of the dataframe.
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species country
## 1          5.1         3.5          1.4         0.2  setosa  canada
## 2          4.9         3.0          1.4         0.2  setosa  canada
## 3          4.7         3.2          1.3         0.2  setosa  canada
## 4          4.6         3.1          1.5         0.2  setosa  canada
## 5          5.0         3.6          1.4         0.2  setosa  canada
## 6          5.4         3.9          1.7         0.4  setosa  canada
```

## Creating and Running R scripts

Let's calculate some important summary statistics and store them as variables 
to the environment.


``` r
# Get the mean values for petal characteristics.
petal_length_avg <- mean(iris$Petal.Length)
petal_length_avg
```

```
## [1] 3.758
```

``` r
petal_width_avg <- mean(iris$Petal.Width)
petal_width_avg
```

```
## [1] 1.199333
```

``` r
# Calculate the correlation between between petal length and width.
petal_cor <- cor(x = iris$Petal.Length, y = iris$Petal.Width, method = "pearson")
petal_cor
```

```
## [1] 0.9628654
```

## Creating and Running R scripts

Lastly, we can plot our findings.


``` r
# Plot the petal legths versus widths.
p <- plot(x = iris$Petal.Length, y = iris$Petal.Width, 
          xlab = "Petal Length (cm)", 
          ylab = "Petal Width (cm)")
```

![](r_packages_sessions_scripts_files/figure-html/unnamed-chunk-15-1.png)<!-- -->


## Creating and Running R scripts
After saving and closing your script you can open it and re-run it at a later time, or send it to someone to run themselves.

To run a whole script, open it and press the "Run" button at the top left of the Source pane. 
You can also "source" a saved `.R` file using the `source()` function.

To go line-by-line put the cursor next to a line and press "Shift" + "Enter" 

* For Mac use: "command" + "return"

To run a multiple lines, highlight the desired lines and press "Shift" + "Enter"

* For Mac use: "command" + "return"

## 


<pre style="color: indigo; background: linear-gradient(to right, gold, rgba(255,0,0,0)); padding-top: 50px; padding-bottom: 50px;">
                                                                                        
                                                  ,,                                    
  .g8""8q.                                 mm     db                           ,M"""b.  
.dP'    `YM.                               MM                                  89'  `Mg 
dM'      `MM `7MM  `7MM  .gP"Ya  ,pP"Ybd mmMMmm `7MM  ,pW"Wq.`7MMpMMMb.  ,pP"Ybd    ,M9 
MM        MM   MM    MM ,M'   Yb 8I   `"   MM     MM 6W'   `Wb MM    MM  8I   `" mMMY'  
MM.      ,MP   MM    MM 8M"""""" `YMMMa.   MM     MM 8M     M8 MM    MM  `YMMMa. MM     
`Mb.    ,dP'   MM    MM YM.    , L.   I8   MM     MM YA.   ,A9 MM    MM  L.   I8 ,,     
  `"bmmd"'     `Mbod"YML.`Mbmmd' M9mmmP'   `Mbmo.JMML.`Ybmd9'.JMML  JMML.M9mmmP' db     
      MMb                                                                               
       `bood'
</pre>
<!-- http://patorjk.com/software/taag/#p=display&f=Georgia11&t=Questions%3F%0A -->
