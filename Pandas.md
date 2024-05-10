
Pandas is a great data visualisation library that we can use to do data analysis with our code base

# Basics

## Dataframes

We can read in some data with 

```python
titles = pd.read_csv('data/titles.csv')
titles.head()
```

- `.head()` and `.tail()` help us to be able to take snapshots from the dataframe itself, we can pass in a number (Eg. `.head(4)` to take a custom number of elements from the data frame)

We can do filtering on the data that we want by doing

```python
c = cast
c = c[c.title == "Inception"]
c = c[c.n.isnull()]
c
```

We can then sort by a field by using the field of 

```python
c.sort_values('n') # Sort by a Field
```

We can also use special string methods by using the following syntax
```python
titles[titles['title'].str.contains("Treasure
Island")==True].sort_values("year")
```

## Series

We can read out a specific column by using 

```
c.year # This gets a series
```

This gives us a variety of different methods such as 
```python
c.year.value_counts()
```

We can then sort by the value indexes by doing

```python
c.year.value_counts().sort_index()
c.year.value_counts().sort_index().plot() # Generates a plot
```

## Plots

We can do plots with the entire data frame or a single series

```
c = cast
c = c[c.character=="Kermit the Frog"]
c.plot(x='year',y='n',kind='scatter')
```


## Modifying Dataset

We can then take subsets of the entire plot with 

```
c = cast
c = c[["year","n"]]
c
```

We can then set the index of our dataframe by using 

```
c = cast
c = c.set_index(['title']).sort_index() # A sorted index is much much faster
c = c.set_index(['title','year']).sort_index()

c.loc['Sleuth'] # We can then lookup indexes using the `.loc`
```

We can remove the indexes by doing
```
c.reset_index(['year','index'])
```



