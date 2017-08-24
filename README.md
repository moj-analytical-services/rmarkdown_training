# rmarkdown_training
Short training session on RMarkdown, for JSAS, August 2017.

RMarkdown is a way to write reproducible documents. You can use it to embed R code and calculations in to Word, PDF, HTML documents, or slideshows. These steps teach you how to make a report, and you’ll see how it could be used to produce a statistical bulletin. Actions for you are numbered.

1. Open RStudio

This software gives a more user friendly way of creating work in R, you can see: a file explorer; a console to run R script in. You also have your environment, which is where objects you create, such as variables or tables will appear. Then you also have a window to create and save scripts of R code or RMarkdown files.

2. Create an RMarkdown file. Click ‘New’ -> R Markdown -> Enter the title “Crime stats" and your name -> Choose ‘Word’.

You’ll notice you could have chosen PDF or HTML, and may want to in future, but for now use Word as this is the format most stats bulletins are in.

You should now have a file open called Untitled.RMD. We’re going to edit this and create a pretend statistics publication.

If you look at the top of the file you’ve opened there is something called a YAML header. This contains the information you provided when creating the document. If you changed your mind and wanted to do a PDF document, for example, you could change the output type here. We’ll come back to the YAML header later.

You’ll see there are two different types of section in the file, an example has been automatically generated. The two types are: code chunks, and text that will appear in your output document.

3. Save the RMD file in the folder you have put the data in (or where you've cloned this repo).
4. Delete everything below the first code chunk (the ‘setup’ chunk) so we can start our own document.
5. We’re going to install a package called readr. One of the best things about R is the collection of packages that people across the world have made: groups of functions that you can download and use yourself. Readr is used for reading in files, in our case we’ll use it to get the csv. In the setup chunk, type *library(readr)*. If you get an error, run *install.packages("readr")* in the console
6. In the setup chunk, type *crimedata <- read_csv(“crimes.csv”)*. This will load the data when we create our output. We have assigned it to the name ‘crimes’. If you want to test a chunk, click the green play button at the top right of it. In this case, clicking that means you'll see 'crimes' appear in your environment
7. Let’s write a chapter. You can create a heading by putting # before some text. Let’s make a chapter by writing *# Trend over time*
8. Let’s see what our output document looks like. If you click “Knit”, it will run everything in your file and create a Word document for you. Open/download this to have a look: you should have a title, name and date, followed by the heading you’ve just made.
9. Write some normal text below your heading, for example *over time, the number of crimes has changed.*
10. Let’s add a chart to show the trend. You can create a new code chunk by typing CTRL+ALT+I (or clicking Insert -> R). After where it says r, type *echo=FALSE* to prevent the code appearing in your output document.
11. We’ll use another popular package to make a chart. In your setup chunk, type *library(ggplot2)*.
12. Go back to your new chunk at the bottom. Type *ggplot(crimedata, aes(year, crimes)) + geom_point()*. This tells ggplot which data (crimedata) to use, and which variables (year, crimes) to plot, and how to plot them (line). (If you don't want to use ggplot2, you can just use plot(crimedata)).
13. Try knitting your document again. You should see the text and chart you’ve just added.
14. You’ll notice that the y axis doesn’t start at 0! Let’s fix that. Add  *+ expand_limits(y=0)* to your ggplot line. Knit again and you’ll see the axis now starts at 0.
15. You’ll also notice that the graph is quite large. You can edit the size at the start of the chunk within the curly braces, type: *fig.height = 3, fig.width = 6*

Another really useful feature of RMarkdown is you can embed numbers directly in to the text. These could be calculated directly from your data source, rather than copy and pasted from Excel or SAS output.

16. Add another heading: *# Key figures*

17. Create another code chunk (CTRL+ALT+I or Insert -> R). Remember to put *echo = FALSE*

18. Let’s give R two values that we want to include in the text. We could write this directly in to the text, but if they don’t work then you get more informative error messages from writing things in code chunks. In the chunk type:

*maxcrimes <- max(crimedata$crimes)*

*mincrimes <- min(crimedata$crimes)*

When you knit, this will save those two values under those names.

19. Now type the sentence you want to include your numbers in. To add some r code, write it within backward apostrophes \`. Your sentence could be *The minimum number of passangers was \`r mincrimes\` and the maximum was \`r maxcrimes\`.*
20. Click Knit - you’ll see your new sentence containing the numbers.

We’re more interested in finding out what the latest value is. We’ll use a package called dplyr to get a function called last(), which gets the last value in a table.

21. Create a new code chunk, remember *echo=FALSE*.
22. Arrange crime data by year: *crimedata <- arrange(crimedata, year)*
23. Get the latest year and the latest value:

*latestyear <- last(crimedata$year)*

*latestcrimes <- last(crimedata$crimes)*

24. Add a sentence for your new numbers, e.g. *In the latest year (\`r latestyear\`) there were \`r latestcrimes\` crimes.*
25. Knit again - you’ll see your new sentence at the end!

The document you have doesn’t quite look like our bulletins do. Rather than do all your formatting in Word, you can create a styles template document in a few minutes, that your RMarkdown will use for formatting. I’ve already created one which fits the JSAS style template, saved in this repo, called mystyles.docx.

26. In your YAML header, amend slightly so it says:
*output:*
  *word_document:*
    *reference_docx: mystyles.docx*
27. Click ‘Knit’. You should now have a document with the right fonts, and a header which looks more like the JSAS bulletins.


The last thing we’ll look at is what you’d do if you had new data, for example if an error got fixed, or if you’re producing the next quarter’s bulletin. "crime2.csv" has an extra row/year of data.

28. Change the data source in your setup chunk to “crime2.csv”.
29. Click Knit. You’ll see the values have been updated!

A useful cheatsheet:
https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf
