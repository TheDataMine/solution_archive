# OPTIONAL PROJECT 1

I did this using 2019.csv, but the code should apply to a full dataset
Create a dataset of all flight delays with airport codes, delay time
unix code

```{.sh}
cd /class/datamine/data/flights/
cat *.csv | cut -d, -f10,15,17,34 > /scratch/scholar/mbrownst/allflights.csv
```

```{.r}
#read the data into R
flights <- read.csv("/scratch/scholar/mbrownst/all_flights.csv",header=T)
```

#1a
```{.r}
#1a Which 5 states have the most flight departures? 
#(i.e., which 5 states are the origins of flights most often?) 
#How many flight departures do each of those 5 states have?
tail(sort(table(flights$ORIGIN_STATE_ABR)))
#TOP 5 STATES ARE:
#2019: NY, GA, IL, FL, TX
```

#1b
```{.r}
#Which 5 airport codes have the most flight departures? (i.e., 
#which 5 airport codes are the origins of flights most often?) 
#How many flight departures do each of those 5 airport codes have?
tail(sort(table(flights$ORIGIN)))
#TOP 5 Airports (2019): ATL, ORD, DFW, DEN, CLT
```

#2a
```{.r}
#Which 5 states have the longest average flight delays? 
#How long are each of those longest average flight delays, corresponding to those 
#5 states? 
#You probably will want to extract the relevant data from the flight files,
#using UNIX, and import this smaller data into R. It will be challenging to 
#import all of the full flight data sets into R.
tail(sort(tapply(flights$DEP_DELAY,flights$ORIGIN_STATE_ABR,mean,na.rm=T))) #average delay by route
#WV, ND, VT, NJ, IL have the longest average delays in 2019
wv_flights <- flights[flights$ORIGIN_STATE_ABR=="WV",]
tail(sort(wv_flights$DEP_DELAY))
nd_flights <- flights[flights$ORIGIN_STATE_ABR=="ND",]
tail(sort(nd_flights$DEP_DELAY))
vt_flights <- flights[flights$ORIGIN_STATE_ABR=="VT",]
tail(sort(vt_flights$DEP_DELAY))
nj_flights <- flights[flights$ORIGIN_STATE_ABR=="NJ",]
tail(sort(nj_flights$DEP_DELAY))
il_flights <- flights[flights$ORIGIN_STATE_ABR=="IL",]
tail(sort(il_flights$DEP_DELAY))
```

```{.r}
#2b Paste tailnums to origin
flights$pairedtails <- paste(flights$TAIL_NUM,flights$ORIGIN,na.rm=T)
tail(sort(table(flights$pairedtails)))
#N489HA HNL
rm(wv_flights,nj_flights,vt_flights,nd_flights,il_flights)
```
