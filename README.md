# rmarkdown_training
Short training session on RMarkdown.

The aim of this training session is to give a brief introduction to the functionality of R markdown and its benefits.

By the end of this session you should be able to produce an R markdown word document using R Studio.

RMarkdown is a way to write reproducible documents. You can use it to embed R code and calculations in to Word, PDF, HTML documents, or slideshows. There are a number of benefits in using this software to produce regular reports. You'll see that we can reduce the chance of error as we don't need to copy and paste between our data and Word output, and you'll see that wrapping the analysis up with the text makes it much more reproducible and transparent. These steps teach you how to make a report, and you’ll see how it could be used to produce a statistical bulletin. Actions for you are numbered.

Before you start, make sure 'mystyles.docx', 'crimedata.csv' and 'crimedata2.csv' are all in the same folder, preferably a new folder.

1. Open RStudio

This software gives a more user-friendly way of creating work in R, you can see: a file explorer; a console to run R script in. You also have your environment, which is where objects you create, such as variables or tables will appear. Then you also have a window to create and save scripts of R code or RMarkdown files.

2. Create an RMarkdown file. Click ‘File’ -> ‘New File’ -> ‘R Markdown’ -> Enter the title “Crime stats" and your name -> Choose ‘Word’ or click on New icon then ‘R Markdown’ and follow the same instructions.

You’ll notice you could have chosen PDF or HTML, and may want to in future, but for now use Word as this is the format most stats bulletins are in.

You should now have a file open. We’re going to edit this and create a pretend statistics publication.

If you look at the top of the file you’ve opened there is something called a YAML header. This contains the information you provided when creating the document. If you changed your mind and wanted to do a PDF document, for example, you could change the output type here. We’ll come back to the YAML header later.

You’ll see there are two different types of section in the file, an example has been automatically generated. The two types are: code chunks, and text that will appear in your output document.

3. Save the RMD file in the folder you have put the data in (or where you've cloned this repo).

4. Delete everything below the first code chunk (the ‘setup’ chunk) so we can start our own document.

5. In the setup chunk, type *library(readr)* then on the next line *crimedata <- read_csv(“crimedata.csv”)*. This will load the data when we create our output. We have assigned it to the name ‘crimedata’. If you want to test a chunk, click the green play button at the top right of it. In this case, clicking that means you'll see 'crimedata' appear in your environment.

6. Let’s write a chapter. You can create a heading by putting # before some text. Let’s make a chapter by writing *# Trend over time*

7. Let’s see what our output document looks like. If you click “Knit”, it will run everything in your file and create a Word document for you. Open/download this to have a look: you should have a title, name and date, followed by the heading you’ve just made.

8. Write some normal text below your heading, for example *over time, the number of crimes has changed.*

9. Let’s add a chart to show the trend. You can create a new code chunk by typing CTRL+ALT+I (or clicking Insert -> R). After where it says r, type *,echo=FALSE* to prevent the code appearing in your output document.

10. Go back to your new chunk at the bottom. Type *ggplot(crimedata, aes(year, crimes)) + geom_line() + expand_limits(y=c(0,200))*.

11. Try knitting your document again. You should see the text and chart you’ve just added.

Another really useful feature of R Markdown is you can embed numbers directly in to the text. These could be calculated directly from your data source, rather than copy and pasted from Excel or SAS output.

12. Add another heading: *# Key figures*

13. Create another code chunk (CTRL+ALT+I or Insert -> R). Remember to put *,echo = FALSE*

14. Let’s give R two values that we want to include in the text. We could write this directly in to the text, but if they don’t work then you get more informative error messages from writing things in code chunks. In the chunk type:

*maxcrimes <- max(crimedata$crimes)*

*mincrimes <- min(crimedata$crimes)*

When you knit, this will save those two values under those names.

15. Now type the sentence you want to include your numbers in. To add some r code, write it within backward apostrophes \`. Your sentence could be *The minimum number of crimes was \`r mincrimes\` and the maximum was \`r maxcrimes\`.*

16. Click Knit - you’ll see your new sentence containing the numbers.

We’re more interested in finding out what the latest value is. We’ll use a package called dplyr to get a function called last(), which gets the last value in a table. Packages are bits of code (functions) written by somebody else and bundled up. We could write it all from scratch ourselves, but someone has already done the work for us, so let's use it!

17. Create a new code chunk, remember *,echo=FALSE*. In your setup chunk at the top of your code, type *library(dplyr)*.
18. Arrange crime data by year: *crimedata <- arrange(crimedata, year)*
19. Get the latest year and the latest value:

*latestyear <- last(crimedata$year)*

*latestcrimes <- last(crimedata$crimes)*

20. Add a sentence for your new numbers, e.g. *In the latest year (\`r latestyear\`) there were \`r latestcrimes\` crimes.*

21. Knit again - you’ll see your new sentence at the end!

The document you have doesn’t quite look like our bulletins do. Rather than do all your formatting in Word, you can create a styles template document in a few minutes, that your RMarkdown will use for formatting. There is already a styles document created which fits the JSAS style template, saved in this repo, called mystyles.docx.

22. In your YAML header, amend slightly so it says:
*output:*
  *word_document:*
    *reference_docx: mystyles.docx*
    
23. Click ‘Knit’. You should now have a document with the right fonts, and a header which looks more like the JSAS bulletins. To call the different headers in your styles template document you use a different number of hashtags at the start of your headers e.g. 1 hashtag = header 1 and 3 hashtags=3 headers. For example, you can add a heading (heading 3 from the styles template) called latest figures before the text in step 20 *### Latest figures*.

24. If you want to change any numbers or words in your text to bold or italic you need to use a single asterisk either side of your number or text for italic or a double asterisk for bold. You can try this on one of your figures or text in your RMarkdown.

The last thing we’ll look at is what you’d do if you had new data, for example if an error got fixed, or if you’re producing the next quarter’s bulletin. "crimedata2.csv" has an extra row/year of data.

25. Change the data source in your setup chunk to “crimedata2.csv”.

26. Click Knit. You’ll see the values have been updated!

A useful cheatsheet:
https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf

## Summary
- Seen some of the benefits of RMarkdown: embed numbers directly in to text, reduce chance of error and reduce repetitive tasks. 
- Open source - free and can use other people's packages. 
- Packages: can reduce duplication e.g. functions to create formatted charts. 
- Git session available too where you'll see how to use the version control software from within the RStudio interface (not possible with SAS). 
- Questions

## Exercises

Open the RMarkdownExercises.docx file in Word. You can do this by downloading it from the github repository or from the R files window. 

1. Create the "Total number of Crimes per year" plot (using the crimedata.csv dataset). This is the same plot as shown in the course but you will need to change the colour of the line to blue and add the title (you may find ?ggplot and ?ggtitle useful). 
2. Add in the line of italic text, setting up the first and last year in a code chunk.
3. Add in the next title "Crime summary statistics" using the mystyles document to check which header to use. 
4. Use the cheatsheet to format the bullet points as in the example and set up a code chunk to calculate the mean, median, minimum and maximum number of crimes. 


