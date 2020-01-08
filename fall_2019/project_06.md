# Project 06 Answer Key
https://datamine.purdue.edu/seminars/fall2019/stat19000project6.html


# Question 1a
> Read in the `5000_transactions.csv` data (from 8451) into a data frame to be
called `myDF`.

```{R}
# Use read.csv() to bring in the transaction data
myDF = read.csv('/class/datamine/data/8451/The_Complete_Journey_2_Master/5000_transactions.csv')
```

# Question 1b
> Split the data frame `myDF`, using the `STORE_R` column, and store the
results of the split into a new variable called `myresults`. Use the split
command to achieve this. Remember that we can read about the split
command using: `?split`

```{R}
# Use split() along STORE_R to create a new data frame
myresults = split(myDF, myDF$STORE_R)
```

# Question 1c
> What is the class of `myresults`? What is the length of `myresults`? What are
the names of `myresults`? (Use class, length, and names on myresults.)

```{R}
# Use class() to view the data type
# Use length() to view the data length 
# Use names() to view the data field names
class(myresults)
length(myresults)
names(myresults)
```

# Question 1d
> Check the dimensions (`dim`) and the head of `myresults[["CENTRAL"]]`.

```{R}
# Use dim() to see the dimension of the object
dim(myresults[["CENTRAL"]])
# Use head() to see the first 6 rows of the object
head(myresults[["CENTRAL"]])
```

# Question 1e
 > Now manually make a data frame that has all of the same columns as `myDF`
 but only has rows for which `myDF$STORE_R` is equal to `"CENTRAL"`:
`centralresults <- myDF[myDF$STORE_R == "CENTRAL", ]`
Verify that the `dim` and `head` of `myresults[["CENTRAL"]]` and
`centralresults` look the same.

```{R}
# Use square brackets to get myDF rows where the value of STORE_R is "CENTRAL"
centralresults = myDF[myDF$STORE_R == "CENTRAL", ]
# Use dim() to see the dimension of the object
dim(centralresults)
# Use head() to see the first 6 rows of the object
head(centralresults)
```

# Question 2a
> Read in the `5000_products.csv` data (from 8451) into a data frame to be
called `myproducts`.

```{R}
myproducts = read.csv('/class/datamine/data/8451/The_Complete_Journey_2_Master/5000_products.csv')
```

# Question 2b
> Merge the data frames `myDF` and `myproducts`, according to the
`"PRODUCT_NUM"` column (which is common to both data frames). Store the results
of the merge into a new variable called `mybigDF`. Remember that we can read
about the merge command using: `?merge`. Hint: You can use `by="PRODUCT_NUM"`

```{R}
# Use merge() to combine two data frames on PRODUCT_NUM
mybigDF = merge(myDF, myproducts, "PRODUCT_NUM")
```

# Question 3a
> Take a subset of the data frame `myDF` that shows all of data about the
purchases made on 23 December 2017. You do not need to store the results of the
subset function anywhere. Remember that we can read about the subset command
using: `?subset`

```{R}
# Use subset() to get rows of myDF where the value of PURCHASE_ is '23-DEC-17'
head(subset(myDF, myDF$PURCHASE_=='23-DEC-17'))
```

# Question 3b
> Take a subset of the data frame `myDF` that shows only the dollar amounts of
the purcases made on 23 December 2017.

```{R}
# Use subset() to get rows of myDF where the value of PURCHASE_ is '23-DEC-17'
# Set the 'select' parameter to 'SPEND' to include that field in the output
head(subset(myDF, myDF$PURCHASE_=='23-DEC-17', select='SPEND'))
```

# Question 3c
> Take a subset of the data frame `myDF` that shows only the dates and dollar
amounts of the purcases made on 23 December 2017.

```{R}
# Use subset() to get rows of myDF where the value of PURCHASE_ is '23-DEC-17'
# Set the 'select' parameter to a vector containing 'PURCHASE_' and 'SPEND' to
# include those fields in the output
head(subset(myDF, myDF$PURCHASE_=='23-DEC-17', select=c('PURCHASE_', 'SPEND')))

```

# Question 3d
> Take a subset of the data frame `myDF` that shows only the dates and dollar
amounts and stores of the purcases made on 23 December 2017.

```{R}
# Use subset() to get rows of myDF where the value of PURCHASE_ is '23-DEC-17'
# Set the 'select' parameter to a vector containing 'PURCHASE_', 'SPEND', and
# 'STORE_R' to include those fields in the output
head(subset(myDF, myDF$PURCHASE_=='23-DEC-17', select=c('PURCHASE_', 'SPEND',
'STORE_R')))
```

# Question 3e
> On December 23, 2017, which store had the largest total amount (in dollars)
of purchases? Hint: Use the `tapply` function.

```{R}
# Store the previous code in a variable
myDFdec23 = subset(myDF, myDF$PURCHASE_=='23-DEC-17', select=c('SPEND', 'STORE_
R'))
# Use tapply() to calculate the total purchases for each store
spend_by_store = tapply(myDFdec23$SPEND, myDFdec23$STORE_R, sum)
# Use sort() to see the store with the highest total dollar purchase amount
sort(spend_by_store)
```
