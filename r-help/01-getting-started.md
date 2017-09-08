# R resources for getting started

## Helpful videos

*   [Installing R and RStudio](https://www.youtube.com/watch?v=9L021PaxLfQ "Link")
*   [Introduction to RStudio](http://www.youtube.com/embed/OnccPx2B8Iw)
*   [Functions and Objects](http://www.youtube.com/embed/xhedRKX1N98)
*   [Importing a Dataset](https://www.youtube.com/embed/C-a8NYmYYc8)
*   [Vectors](http://www.youtube.com/embed/o_L_Q48KxC0)
*   [Indexing](http://www.youtube.com/embed/n9LwIWJKMOs)

## Importing Data

You can use RStudio to "Import Dataset" in the upper-right panel.  You can import data from Excel or in .csv format.  Often, you will simply download data from MyStatLab and import the Excel file.  Be careful to check or uncleck "First Row as Names" as appropriate.  If the first row is not used as names, R will assign default names.  You may also select names for data that you import.  

Alternatively, you can also write and run the command to import data, for example:

	> HW1_7 <- read_excel("~/Downloads/data-12-22-2016-10-57 PM.xlsx", col_names=F)

If you write the command yourself, take note of the following:

*   Mac: The path separator in Mac is a forward slash (/) as in the example above. "~" represents your home folder, so ~/Desktop refers to your desktop, ~/Documents to your documents folder, etc.
*   Windows: The path separator in Windows is a backslash (\) but in R you must enter backslashes as a double backslash, e.g. "C:\\My Documents\\data.csv"

## Calculations

You can use R to do calculations with this data such as sum the values.

	> sum(HW1_7$X0)

 R can be used as your calculator simply by typing expressions.  At the prompt, we enter the expression that we want evaluated and when we hit enter, it will compute the result for us. For Example:

	> 4+6

Use * for multiply.  
Use ^ for raised to the power of.  
Use parentheses to ensure that it understands what you are trying to compute.
