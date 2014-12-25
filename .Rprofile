#######
## .Rprofile file
## Sets some options for R sessions, so that I don't have to set them
##each time.
#######


## I customized original code obtained from:
## http://gettinggeneticsdone.blogspot.com/2013/07/customize-rprofile.html
## and from
## http://sugiyama-www.cs.titech.ac.jp/~toby/org/HOCKING-emacs-ess-R.html


## This avoids having to interactively select the mirror during each R
## session. Sets your favorite CRAN mirror, with a fallback.
## Change to your favorite CRAN mirror.
options(repos=c("http://cran.utstat.utoronto.ca/","http://cran.r-project.org"))

## Open a new cairo device in the bottom right. This avoids having to move/resize
## the plot window for each session.
if(interactive()){
  require(grDevices)
  X11.options(type="cairo")
  x11(xpos=-1,ypos=-1)
}

## Load packages at launch. add or delete packages  according to your needs.
library("psych")

## Create a new invisible environment for all the functions to go in
## so it doesn't clutter your workspace.
.env <- new.env()

## Returns names(df) in single column, numbered matrix format.
.env$n <- function(df) matrix(names(df))

## ht==headtail, i.e., show the first and last 10 items of an object
.env$ht <- function(d) rbind(head(d,10),tail(d,10))
 
## Show the first 5 rows and first 5 columns of a data frame or matrix
.env$hh <- function(d) if(class(d)=="matrix"|class(d)=="data.frame") d[1:5,1:5]

## Strip row names from a data frame (stolen from plyr)
.env$unrowname <- function(x) {
rownames(x) <- NULL
x
}

## List objects and classes (from @_inundata, mod by ateucher)
.env$lsa <- function() {
{
obj_type <- function(x) class(get(x, envir = .GlobalEnv)) # define environment
foo = data.frame(sapply(ls(envir = .GlobalEnv), obj_type))
foo$object_name = rownames(foo)
names(foo)[1] = "class"
names(foo)[2] = "object"
return(unrowname(foo))
}
}

## List all functions in a package (also from @_inundata)
.env$lsp <-function(package, all.names = FALSE, pattern) {
package <- deparse(substitute(package))
ls(
pos = paste("package", package, sep = ":"),
all.names = all.names,
pattern = pattern
)
}

## Attach all the variables above
attach(.env)
