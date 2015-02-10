---
layout: lesson
root: .
title: Working with ROpenSci package "gender"
---

How could we use what we have learnt so far in order to do something more powerful? For example, how could we use R to access data which is stored on the external servers? We could write our own code from scratch. However, before we start doing this it's worth checking whether someone has already done this before. 

We may find that such code has already been written and moreover, it was turned into a *package*. In short, a *package* is a reusable piece of code which we can use in the code we write. It's a bit like including references to source information in your text. The main difference is that in order for that reference to be effective, we need to have the *package* installed on our machine. We will now learn how to do that. 

We will try to retrieve some information about gender based on the first name. In order to do that we will use a package developed as a part of [ROpenSci](http://ropensci.org/) project called simply [*gender*](https://github.com/ropensci/gender).

From the description of the package:  
  
*Data sets, historical or otherwise, often contain a list of first names
but seldom identify those names by gender. Most techniques for finding
gender programmatically, such as the [Natural Language Toolkit][], rely
on lists of male and female names. However, the gender[\*][] of names
can vary over time. Any data set that covers the normal span of a human
life will require a historical method to find gender from names.*

*This package encodes gender based on names and dates of birth, using
either the Social Security Administration's data set of first names by
year since 1880 (based on an implementation by [Cameron Blevins][]) or
the U.S. Census data from IPUMS for years before 1930 (contributed by
[Ben Schmidt][]). By using these data sets instead of lists of male and
female names, this package is able to more accurately guess the gender
of a name; furthermore it is able to report the proportion of times that
a name was male or female for any given range of years.*

First, we need to install the package:

	install.packages("gender")

	
	Installing package into ‘/Users/aleksandra/Library/R/3.1/library’
	(as ‘lib’ is unspecified)
	trying URL 'http://mirrors.ebi.ac.uk/CRAN/bin/macosx/contrib/3.1/	gender_0.4.3.tgz'
	Content type 'application/x-gzip' length 124452 bytes (121 Kb)
	opened URL
	==================================================
	downloaded 121 Kb
	
	
	The downloaded binary packages are in
	/var/folders/t7/dlfj6jdn12q3jrthztdx7zrh0000gn/T//RtmpHHThM7/downloaded_packages
	
Now we need to `load` the package:
	
	> library("gender")

The first time we try to use the package, we will actually have to finish one more installation step. Let's try using the package by calling function `gender`:

	> gender("Aleksandra")
	
We will be asked to install `genderdata` package:		

		The genderdata package needs to be installed from GitHub.
		Install the genderdata package? 
			1: Yes
			2: No

	Selection: 1
	Installing the genderdata package.
	Downloading github repo lmullen/gender-data-pkg@master
	Installing genderdata
	'/Library/Frameworks/R.framework/Resources/bin/R' --vanilla CMD INSTALL  \
		  '/private/var/folders/t7/dlfj6jdn12q3jrthztdx7zrh0000gn/T/RtmpHHThM7/devtoolsa8d17e1c758/lmullen-gender-data-pkg-ba850f2'  \
	  --library='/Users/aleksandra/Library/R/3.1/library' --install-tests 

	* installing *source* package ‘genderdata’ ...
	** R
	** data
	*** moving datasets to lazyload DB
	** preparing package for lazy loading
	** help
	*** installing help indices
	** building package indices
	** testing if installed package can be loaded
	* DONE (genderdata)
	
	
Now we should be able to use the package.
Our call `gender("Aleksandra")` returned some values. 

	$name
	[1] "Aleksandra"

	$proportion_male
	[1] 0

	$proportion_female
	[1] 1

	$gender
	[1] "female"

	$year_min
	[1] 1932

	$year_max
	[1] 2012	

We would be better off saving that returned result into a variable, like we did in the initial part of the tutorial.

	result <- gender("Aleksandra")

Now we can check what actually was returned:

	class(result)
	[1] "list"
	
The result is a list. We can retrieve elements of this list:

	result[1]
	
Another way is to use the `$` operator. 

	result$gender
	
We could try now check the gender for different names. We could simply call the `gender` function providing different name. But if we had many names to check, that would take a long time and be very repetitive. 

Let's try to automate that process. In programming repetitive tasks can be easily automated using **loops**. One of the loops is a `for` loop:

	for(element in collection){ …do_something….}
	
How would that work? Let's try looping through a list of names. First, we need to define that list:
	
	names <- c("Tom", "Kate", "Jack")
	
To print all names in that list using a `for` loop:

	for(i in names){print(i)}

Now instead of printing, we can try using our `gender` function:

	for(i in names){gender(i)}

So far so good but it doesn't seem very useful. How about print every name and the gender retrieved for it?
	
	for (i in names){print(c(i, gender(i)$gender))}