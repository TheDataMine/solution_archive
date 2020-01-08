---
geometry: top=2cm, bottom=2cm
---

# Project 11 Answer Key
https://datamine.purdue.edu/seminars/fall2019/stat19000project11.html

# Question 1a
> In the 2020 election data (only considering the 9th field, not the 10th
field) how many donations are from cities whose name ends in “burg”? How about
“boro”? “shire”? “ton”? “town”? “ville”?

```{.r}
election = read.csv("/class/datamine/data/election/itcont2020.txt", sep="|")
length(grep("BURG$", election$CITY))
length(grep("BORO$", election$CITY))
length(grep("SHIRE$", election$CITY))
length(grep("TON$", election$CITY))
length(grep("TOWN$", election$CITY))
length(grep("VILLE$", election$CITY))
```
```
>>>
> length(grep("BURG$", election$CITY, value=TRUE))
[1] 23621
> length(grep("BORO$", election$CITY, value=TRUE))
[1] 10618
> length(grep("SHIRE$", election$CITY, value=TRUE))
[1] 474
> length(grep("TON$", election$CITY, value=TRUE))
[1] 235188
> length(grep("TOWN$", election$CITY, value=TRUE))
[1] 23323
> length(grep("VILLE$", election$CITY, value=TRUE))
[1] 107955
```

\newpage
# Question 2a
> How many donations in the 2020 election data have a consecutive, repeated
vowel in the (personal) name of the donor? In other words, how many donations
are from a donor with AA or EE or II or OO or UU in the donor’s name?

```{.r}
length(grep("(AA|EE|II|OO|UU)", election$NAME, value=TRUE))
```
```
>>>
[1] 158280
```

# Question 2b
> Which donor(s) has/have the longest name(s) in the 2020 election data, in
terms of character length?

```{.r}
name_lengths = nchar(as.character(election$NAME))
names_and_lengths = data.frame(name_lengths, election$NAME)
names_and_lengths[which.max(names_and_lengths$name_lengths), ]
```
```
>>>
                name_lengths
336019                   118

336019          election.NAME
                CAPITAN GRANDE BAND OF DIEGUENO MISSION INDIANS OF CALIFORNIA
                (BARONA GROUP OF CAPITAN GRANDE BAND OF MISSION INDIANS)
```

# Question 2c
> How many donations in the 2020 election have donors with the same last name
as yours? (For instance, Dr Ward would look for people whose name starts with
Ward. You want to make sure to check the beginning of the name, since the last
names come first.)

```{.r}
length(grep("^PARK ", election$NAME, value=TRUE))
```
```
>>>
[1] 1
```

\newpage
# Question 3a
> Use the method you learned in Project 9, Question 1, to cut only the 9th
field from the data for all election years, and save the result in a file in
your home directory called: myelectiontowns.txt

```{.sh}
cat /class/datamine/data/election/*.txt | cut -d\| -f9 > myelectiontowns.txt
```

# Question 3b
> How many donations come from cities whose names end in the phrase “ton”,
across all election years?

```{.sh}
cat myelectiontowns.txt | egrep 'TON$' | wc -l
```
```
>>>
6253577
```

# Question 3c
> How many unique city names are there in question 3b? (For this question, it
is safe to only consider the city name and to ignore the State name.)

```{.sh}
cat myelectiontowns.txt | sort | uniq | wc -l
```
```
>>>
138084
```

