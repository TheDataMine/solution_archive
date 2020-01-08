# Project 02 Answer Key
https://datamine.purdue.edu/seminars/fall2019/stat19000project2.html


## Question 3a
> Modify the code from `/class/datamine/data/examples/LAmaps.R` to use the data
about London, and to use your own Google Maps API Key, instead of Dr Ward’s
key.

### Solution
To create the proper London map, these are the specific changes must be made:

```r
# Read in the London AirBnB data instead of the LA data
myDF <- read.csv("/class/datamine/data/airbnb/united-kingdom/england/london/201
9-07-10/visualisations/listings.csv")

# Use a new API key in place of Dr. Ward's key
# Dr. Ward's key is AIzaSyDYnLiu1jyxvo4hYqZJqqyZM7kx2fCpUls
register_google(key = "your_key", write = TRUE)

# Set the map center to 'London'
london_center <- as.numeric(geocode("London"))
```

The above isn't __all__ that is required to get full credit. These are just the
isolated changes that students should make to the sample code provided by Dr.
Ward. We still need the rest of the code to draw maps and plot points.

The next page contains a sample student submission that would receive full
credit.


### Full sample solution 
```r
# We load the ggmap library.
library(ggmap)

# Now we load the information from the AirBnB data for the city of London.
myDF <- read.csv("/class/datamine/data/airbnb/united-kingdom/england/london/201
9-07-10/visualisations/listings.csv")

# Now we build a new data.frame containing only the longitudes and latitudes.
mypoints <- data.frame(lon=myDF$longitude,lat=myDF$latitude)

# Use a newly-generatied Google API key, so that we are able to load maps in
# Google.
register_google(key="<yourkey>", write=TRUE)

# In preparation for making a map, we get the center of London from Google:
london_center <- as.numeric(geocode("London"))
# Then we build a map of London
london_map <- ggmap(get_googlemap(center=london_center, zoom=9))
# and we display it.
london_map
```

```r
# Finally, we add the points to the map
london_map <- london_map + geom_point(data=mypoints, size=0.1)
# and we display the map again.
london_map
```
