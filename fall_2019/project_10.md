---
geometry: top=2cm, bottom=2cm
---

# Project 10 Answer Key
https://datamine.purdue.edu/seminars/fall2019/stat19000project10.html

# Question 1a
> Use the UNIX cut or awk tool to extract (only) the dates and transaction
amounts from the election data, across all years. Save this data into a file in
your home directory.


## Solution using cut
```{.sh}
# 
cat /class/datamine/data/election/*.txt | cut -d\| -f14,15 > project10_1a.txt
```

## Solution using AWK
```{.sh}
# 
cat /class/datamine/data/election/*.txt |
awk -F\| '  BEGIN {}
                  {print $14"|"$15}
            END   {}'
```

# Question 1b
> Remove the lines from the file that came from the headers of each election
file, i.e., remove the 21 lines of the form: TRANSACTION_DT|TRANSACTION_AMT
Save the result into a new file.

```{.sh}
cat project10_1a.txt | grep -v "TRANSACTION_DT|TRANSACTION_AMT" > project10_1b.txt
```

# Question 2a
> Import into R the resulting file that you prepared from question 1.

```{.r}

```
