# stats220-lab-revision

## Lab 3A

### Find the index of something
```
gf_names <- c("Loretta", "Joan", "Jen", "Jan", "Liza", "Felicity", "Emily", "Fran", "Flo", "Carol")

# print name in 5th position
gf_names[5]

# print names from 2nd to 5th position
gf_names[2 : 5]
```

### Use of sum() function
```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

# print sum of name lengths from 2nd to 5th position
gf_name_lengths[2 : 5] %>% sum()
```

### sum() function on logical vector
```
gf_name_syllables_one <- c(FALSE, TRUE, TRUE, TRUE, FALSE, FALSE, FALSE, TRUE, TRUE, FALSE)

# print sum
gf_name_syllables_one %>% sum()
```
When the sum() function is used on a logical vector, **the number of TRUE values** are counted.


### Remove NA values
```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5, NA)

# print sum of name lengths
gf_name_lengths %>% sum()

# print sum of name lengths, removing NAs
gf_name_lengths %>% sum(na.rm = TRUE)
```

### sort() function on numbers
```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

# print sum of name lengths
short_names <- sort(gf_name_lengths)

# print first five values
short_names[1 : 5]
```
The `sort()` function has a default argument, which is `decreasing = FALSE`. If you want to arrange/sort values in descending order, you will need to add the argument `decreasing = TRUE`.


### sort() function on character vectors
```
gf_names <- c("Loretta", "Joan", "Jen", "Jan", "Liza", "Felicity", "Emily", "Fran", "Flo", "Carol")

# sort gf_names in reverse alpha numeric order
sort(gf_names, decreasing = TRUE)
```
Output: 
####  [1] "Loretta"  "Liza"     "Joan"     "Jen"      "Jan"      "Fran"    
####  [7] "Flo"      "Felicity" "Emily"    "Carol"


### make comparisons on logical vectors
```
num_people_love_cats <- 100
num_people_love_dogs <- 50

num_people_love_cats > num_people_love_dogs
```
The question here being asked was “Do a greater number of people love cats than love dogs?” and the answer was “TRUE” which means yes!!!


```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

gf_name_lengths[1] > gf_name_lengths[10]
```
In this first example, we can check if value in position 1 of the vector named gf_name_lengths is greater than the value in position 10 of the same vector.


```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

gf_name_lengths == 4
```
In this second example, we can check if any of the values in the vector gf_name_lengths are equal to 4.


```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

# just printing this line so you can see the result
gf_name_lengths <= 5

sum(gf_name_lengths <= 5)
```
We can combine using comparison expressions with the sum() function to count how many values in our vector meet certain conditions!


### Slice and dicing vectors with logical comparisons

if we wanted to select only the names of ex-girlfriends with one syllable, we could use the following code:

```
ex_gf_names <- c("Loretta", "Joan", "Jen", "Jan", "Liza", "Felicity", "Emily", "Fran", "Flo", "Carol")

one_syllable <- c(FALSE, TRUE, TRUE, TRUE, FALSE, FALSE, FALSE, TRUE, TRUE, FALSE)

ex_gf_names[one_syllable]
```


```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

names_keep <- gf_name_lengths <= 5
# printing for learning
names_keep

# subset/slice time with []
gf_name_lengths[names_keep]
```

We can also combine the codes:
```
gf_name_lengths <- c(7, 4, 3, 3, 4, 8, 5, 4, 3, 5)

gf_name_lengths[gf_name_lengths <= 5]
```


### Combining functions with comparisons
```
ex_gf_names <- c("Loretta", "Joan", "Jen", "Jan", "Liza", "Felicity", "Emily", "Fran", "Flo", "Carol")

ex_gf_names[nchar(ex_gf_names) > 4]
```


### Tdiyverse arrange() function

To arrange rows, we can use the {dplyr} function `arrange()`. We need to specify what variable (column) to arrange rows based on. 
By default, rows will be arranged in ascending order. To arrange rows in descending order, we need to use the function `desc()`.

The code example below will arrange the rows of the data frame named `spotify_data` in ascending order based on the variable `duration_ms`.
```
csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) 

spotify_data %>%
  arrange(duration_ms) %>%
  glimpse()
 ```
 
 
 The code example below will arrange the rows of the data frame named `spotify_data` in descending order based on the variable `mode_name`.
 
 ```
 csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) 

spotify_data %>%
  arrange(desc(mode_name)) %>%
  glimpse()
 ```
 
 
### Filtering rows based on conditions
The code below using a comparison expression (similar to earlier in the lab) to filter (keep) only rows where the duration_ms is less than 180000.

```
csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) 

spotify_data %>%
  filter(duration_ms < 180000)
```

In the example below, after filtering songs that are under three minutes, we then only keep songs that have a popularity score of greater than or equal to 70.
```
spotify_data %>%
  filter(duration_ms < 180000,
         track_popularity >= 70)
```

### mutate() function 
In the example below, a new variable called `track_name_length` has been added to the data frame using the functions `mutate()` and `nchar()`.

```
csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) %>%
  mutate(track_name_length = nchar(track_name))

spotify_data %>%
  select(track_name, track_name_length) %>%
  slice(1 : 5) %>%
  print()
```

This method solved the problem of mutating with no vectors show:
```
csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) %>%
  mutate(duration_min = duration_ms / 60000)
  
spotify_data
```


### Two functions from the {tidyverse} package {stringr}

#### str_to_lower()

In the example below, the `track_name` variable has been extracted as a vector, and the `str_to_lower()` function has been applied to all values in the vector.

```
csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) 

spotify_data$track_name %>%
  str_to_lower()
 ```
 
#### str_detect()
`str_detect()` also does some regex for us without too much syntax knowledge. You could expand its use with more regex but we will just focus on searching for characters within the text. 
The first argument is the text/string to be used, and the second argument is the “pattern” to be deteected in the text/string.

```
csv_file <- "https://docs.google.com/spreadsheets/d/e/2PACX-1vS0hFENLiFRQcx28R6xOu_YQdu_W9OWFJhsYQBv-q3A0n03mE3c5okw7FNxikzuQGHK11O715J7uOa1/pub?gid=1899484843&single=true&output=csv"

spotify_data <- read_csv(csv_file) %>%
  mutate(track_name_lower = str_to_lower(track_name)) %>%
  filter(str_detect(track_name_lower, "love"))

spotify_data
```

**Detecing more than one word?**
Suppose I want to search for any track_name that has either “love” or “heart” in it. I would use the symbol | to indicate “or” in the pattern argument for the `str_detect()` function.

```
spotify_data <- read_csv(csv_file) %>%
  filter(str_detect(
            str_to_lower(track_name), 
            "love|heart")
         )

spotify_data
```



