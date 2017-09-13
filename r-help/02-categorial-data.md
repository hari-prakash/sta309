# R resources for Chapter 2 (Categorical Data)

## Videos

*   [Table Proportions](http://www.youtube.com/embed/yWzNTMv0gho)
*   [Grouped Bar Chart](http://www.youtube.com/embed/trs1FyfjxEU)

## Useful commands

You may get categorical data in two forms: raw data, where each row corresponds to a separate case; or a frequency (contingency) table where counts have already been tabulated.

## Making tables from raw data

In this section we'll use the file [bbq.csv](https://raw.githubusercontent.com/brianlukoff/sta309/master/example-data/bbq.csv).  First, load the file:

	> bbq <- read.csv("https://raw.githubusercontent.com/brianlukoff/sta309/master/example-data/bbq.csv")

Make a one-way table by region:

	> table(bbq$Region)
	Midwest Northeast     South      West
	     12         9        17        13

Make a two-way contingency table by region and BBQ status:

	> table(bbq$Region, bbq$GoodBBQ)
	                   no   yes
	      Midwest       8     4
	      Northeast     6     3
	      South         7    10
	      West          9     4

(Note: If you have more than two categorical variables, you can also add a third parameter to the table function to make a three-way table.)

We'll want to use this table again, so we can give it a name:

	> bbqtable <- table(bbq$Region, bbq$GoodBBQ)

You can flip what’s on the rows and columns by reversing the order of the variables:

	> table(bbq$GoodBBQ, bbq$Region)
	
	     Midwest Northeast South West
	  no        8        6     7    9
	 yes        4        3    10    4
	 
Alternatively we can transponse bbqtable for the same result:

	> t(bbqtable)

If you want to add totals (both row and column) to your table, you can use the addmargins function:

	> addmargins(bbqtable)

		    no yes Sum
	  Midwest    8   4  12
	  Northeast  6   3   9
	  South      7  10  17
	  West       9   4  13
	  Sum       30  21  51
	  
If you instead want only the row totals or only the column totals:

	> margin.table(bbqtable,1) # gives the row totals

	  Midwest Northeast     South      West 
	       12         9        17        13 

	> margin.table(bbqtable,2) # gives the column totals

	 no yes 
	 30  21 
	  
The prop.table function takes the frequencies in a table and converts them to percentages.  The function can be used to obtain the percentages for each cell, row percentages, or column percentages as shown below.

	> prop.table(bbqtable) # gives the cell percentages

			    no        yes
	  Midwest   0.15686275 0.07843137
	  Northeast 0.11764706 0.05882353
	  South     0.13725490 0.19607843
	  West      0.17647059 0.07843137

	> prop.table(bbqtable,1) # gives the row percentages

			   no       yes
	  Midwest   0.6666667 0.3333333
	  Northeast 0.6666667 0.3333333
	  South     0.4117647 0.5882353
	  West      0.6923077 0.3076923

	> prop.table(bbqtable,2) # gives the column percentages

			   no       yes
	  Midwest   0.2666667 0.1904762
	  Northeast 0.2000000 0.1428571
	  South     0.2333333 0.4761905
	  West      0.3000000 0.1904762
	  
You can combine the prop.table and margin.table to get the row and column percentages:

	> margin.table(prop.table(bbqtable),1) # gives the row percentages

	  Midwest Northeast     South      West 
	0.2352941 0.1764706 0.3333333 0.2549020 

	> margin.table(prop.table(bbqtable),2) # gives the column the column percentages

	       no       yes 
	0.5882353 0.4117647 
	  
## Making charts:

To make a bar chart of one variable

	> plot(bbq$GoodBBQ)

To create a mosaic plot:

	> plot(bbqtable)

Note that in this latter graph, both the widths and the heights of the bars are proportional to the number of states in each category!

To create a segmented/stacked bar graphs:

	> barplot(bbqtable, legend=T)

Notice that this graph shows the counts.  You can instead compare proportions in categories:

	> barplot(prop.table(bbqtable,2), legend=T)
	
To create a mosaic plot where both the width and heights of the bars are proportional to the counts in each category: 

	> plot(bbq$GoodBBQ, bbq$Region)	
	
## When you have a frequency table to import

In this section, we'll use the file [example.csv](https://raw.githubusercontent.com/brianlukoff/sta309/master/example-data/example.csv).  If you are downloading the data from MyStatLab, you can download the Excel file and then save in CSV format and then define the matrix. 

Use the following command (but replace the part in quotes with the path to the file on your computer):

	> example <- as.matrix(read.csv("~/Desktop/example.csv", row.names=1))

This reads in the `example.csv` file as a matrix (table) instead of as a data frame.

	> example
	          None AA  BA MA PhD
	< 1 year    11  4  53 18  11
	1-5 years   43  9 122 28  17
	> 5 years  103 34  61  3   1

Functions described above that work on tables incuding barplot, addmargins, margin.table, and prop.table can all be used now.

