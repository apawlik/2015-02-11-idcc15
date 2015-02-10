---
layout: lesson
root: .
title: Working with ROpenSci package "gender"
---

How could we use what we have learnt so far in order to do something more powerful? For example, how could we use R to access data which is stored on the external servers? We could write our own code from scratch. However, before we start doing this it's worth checking whether someone has already done this before. 


 We will now try to retrieve some information about gender based on the first name. In order to do that we will use a package developed as a part of [ROpenSci](http://ropensci.org/) project called simply [*gender*](https://github.com/ropensci/gender)

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
	
Another way

	names <- c("Tom", "Kate", "Jack")


	for (i in names){print(c(i, gender(i)$gender))}