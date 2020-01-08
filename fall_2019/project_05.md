# Project 05 Answer Key

# Question 1a

> Which `host_id` has received the largest number of reviews?

```{R}
# Use read.csv() to read the LA AirBnB data into RStudio
LA_airbnb = read.csv("/class/datamine/data/airbnb/united-states/ca/los-angeles
	/2019-07-08/visualisations/listings.csv")
# Use tapply() to calculate the number of reviews each host ID received
reviews_by_host = tapply(LA_airbnb$number_of_reviews, LA_airbnb$host_id, sum)
# Use sort() to order the hosts by their respective review counts 
# Use tail() to get the hosts with the largest number of reviews
tail(sort(reviews_by_host))
```

# Question 1b

> Which neighbourhood has received the largest number of reviews?

```{R}
# Use tapply() to get the AirBnB review totals for each LA neighborhood
reviews_by_neighborhood = tapply(LA_airbnb$number_of_reviews,
	LA_airbnb$neighbourhood, sum)
# Use sort() to order the neighborhoods by number of reviews
# Use tail() to get the 6 neighborhoods with the most reviews
tail(sort(reviews_by_neighborhood))
```

# Question 2a

> Paste together the columns for the 3-letter codes for the origin and
destination of each flight, and store the result in a new column of the data
frame, called myflightpath.

```{R}
# Use read.csv() to read the flights data into RStudio
flights = read.csv("/class/datamine/data/flights/2019.csv")
# Use paste() to create a new column by combining the ORIGIN and DEST columns
flights$myflightpath = paste(flights$ORIGIN, flights$DEST)
# Use head() to check that the new column exists and was created successfully
head(flights$myflightpath)
```

# Question 2b

> Which flight path has the longest average departure delay?

```{R}
# Use tapply() to get the mean departure delay of each flight path 
delay_by_path = tapply(flights$DEP_DELAY, flights$myflightpath, mean)
# Use sort() to order the flight paths by mean departure delay 
# Use tail() to get the 6 flight paths with the highest mean departure delay 
tail(sort(delay_by_path))
```

# Question 3a

> Use the new “location” column, which you created in Question 3b of Project 4.
Classify each (joint) city, state “location” according to the total amount
donated by residents of that city, state.

```{R}
# Use read.delim() to read in the election data with the '|' separator
elections = read.delim("/class/datamine/data/election/itcont2020.txt", sep="|")
# Use paste() to create a new column by combining the CITY and STATE columns
elections$location = paste(elections$CITY, elections$STATE, sep="-")
# Use tapply() to get the donation totals for each city 
donations_by_location = tapply(elections$TRANSACTION_AMT, elections$location, sum)
```

# Question 3b

> Which six campaign committees have received the largest total dollar amount
of donations (so far) in the 2020 election campaign?
 
```{R}
# Use tapply() to get the donation totals for each committee 
donations_by_committee = tapply(elections$TRANSACTION_AMT, elections$CMTE_ID, sum)
# Use sort() to order the committees by donation totals
# Use tail() to get the 6 committees with the highest total donation totals 
tail(sort(donations_by_committee))
```
