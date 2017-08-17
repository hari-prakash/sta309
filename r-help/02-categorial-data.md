# R resources for Chapter 2 (Categorical Data)

## Videos

*   [Table Proportions](http://www.youtube.com/embed/yWzNTMv0gho)
*   [Grouped Bar Chart](http://www.youtube.com/embed/trs1FyfjxEU)

## Useful commands

You may get categorical data in two forms: raw data, where each row corresponds to a separate case; or a frequency (contingency) table where counts have already been tabulated.

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

If you'd like to see the table with row and column totals, you can use the `addmargins` function:

	> addmargins(example)
	         None  AA  BA  MA  PhD  Sum
	< 1 year   11   4  53  18   11   97
	1-5 years  43   9 122  28   17  219
	> 5 years 103  34  61   3    1  202
	Sum       157  47 236  49   29  518

Note: You may get the following warning message, which you can ignore:

	Warning message:
	In read.table(file = file, header = header, sep = sep, quote = quote, :
	 incomplete final line found by readTableHeader on '~/Desktop/example.csv'

Now we can easily generate each of the two possible stacked bar graphs:

	> barplot(example, legend=T)
	> barplot(t(example), legend=T)

The `t` function stands for "transpose"; it swaps the rows and columns in the table so the bar plot swaps the bars and the colors.

If you want the cells of the table to represent proportions of the row or column totals, you can do that with the prop.table function:

	> prop.table(example, 1)
	               None         AA        BA         MA         PhD
	< 1 year  0.1134021 0.04123711 0.5463918 0.18556701 0.113402062
	1-5 years 0.1963470 0.04109589 0.5570776 0.12785388 0.077625571
	> 5 years 0.5099010 0.16831683 0.3019802 0.01485149 0.004950495
	
	> prop.table(example, 2)
	                None         AA        BA         MA        PhD
	< 1 year  0.07006369 0.08510638 0.2245763 0.36734694 0.37931034
	1-5 years 0.27388535 0.19148936 0.5169492 0.57142857 0.58620690
	> 5 years 0.65605096 0.72340426 0.2584746 0.06122449 0.03448276

Note that the first table expresses each cell as a proportion of the row total; the second table expresses each cell as a proportion of the column table. This table is useful on its own and can also be used to create bar plots where the height of the bars are normalized to be the same height:

	> barplot(prop.table(example, 2), legend=T)
	> barplot(t(prop.table(example, 1)), legend=T)

Finally, the margin.table function can be used to compute the marginal distributions:

	> margin.table(example, 1)
	 < 1 year 1-5 years > 5 years 
	       97       219       202 

	> margin.table(example, 2)
	None   AA   BA   MA  PhD 
	 157   47  236   49   29 


If you want the marginal distribution as proportions instead of counts, use the prop.table function first.

	> margin.table(prop.table(example),1)
	<  1 year  1-5 years  > 5 years 
	0.1872587  0.4227799  0.3899614 
	> margin.table(prop.table(example),2)
	      None         AA         BA        MA         PhD 
	0.30308880 0.09073359 0.45559846 0.09459459 0.05598456

## When you have raw data

In this section we’ll use the file [bbq.csv](https://raw.githubusercontent.com/brianlukoff/sta309/master/example-data/bbq.csv).  First, load the file (replace the part in quotes with the path to the file on your computer):

	> bbq <- read.csv("~/Desktop/bbq.csv")

You can also use RStudio to create this command for you by selecting “Import Dataset” in the upper-right panel.

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

You can flip what’s on the rows and columns by reversing the order of the variables:

	> table(bbq$GoodBBQ, bbq$Region)
	
	     Midwest Northeast South West
	  no        8        6     7    9
	 yes        4        3    10    4

Create a bar graph:

	> plot(bbq$GoodBBQ)

Or create a segmented bar graph:

	> plot(bbq$Region, bbq$GoodBBQ)

Note that in this latter graph, both the widths and the heights of the bars are proportional to the number of states in each category!

You can also produce traditional segmented/stacked bar graphs:

	> barplot(table(bbq$Region, bbq$GoodBBQ), legend=T)

And you can just as easily create mosaic plots:

	> mosaicplot(table(bbq$Region, bbq$GoodBBQ))