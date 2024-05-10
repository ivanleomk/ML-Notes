
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

This is for strings
```python
titles[titles['title'].str.contains("Treasure
Island")==True].sort_values("year")
```

This is for dates
```python
titles[titles['date'].dt.... ]
```

## Series

We can read out a specific column by using 

```
c.year # This gets a series
```

We can also get out the specific counts for this specific field by using `value_counts()`. Note that this gives a sorted series, so we'd get the largest -> smallest values by default

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

We can also generate plots from value_counts by doing

```python
(t.year // 10 * 10).value_counts().sort_index().plot(kind='bar')
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


## Aggregation

We can run aggregations using the `.groupBy`  query

```python
c = cast
c = c[c.name == "George Clooney"]
c.groupby(['year']).size().plot(ylim=0)
```

We can even run a groupBy on a transformation of the column

```python
c = cast
c = c[c.name == "George Clooney"]
c.groupby(c.year // 10 * 10 ).size().plot(ylim=0)
```

We can also use a unstack operation. This transposes our rows and columns and is useful when we're using a unstack.

```python
c  = cast
c = c[(c.character == 'Kermit the Frog') | (c.character == 'Oscar the Grouch')]
c = c.groupby(['character',c.year // 10 * 10]).size()
c = c.unstack(0).fillna(0) # note here that fillna helps usto fill in the values
```

Some common operations that we can work with `groupby`

```python
# Getting the total size of each subset
c.groupby(['year','type']).size() 

# Get the max of each subset that we've grouped it by
c = c.groupby(['year'])[['n']].max()'

# Filter by the count value of each
c = cast
c = c[c.name == 'Frank Oz']
g = c.groupby(['year','title']).size()
g[g > 1]
```

Examples of when we might want to work with unstack

```python
# This allows us to do a group by on year-type and then take the diff
c = cast[cast.year < 2115]
c = c.groupby(['year','type']).size()
c = c.unstack('type').fillna(0)
(c.actor/(c.actor + c.actress)).plot(ylim=[0,1])

# Aggregate by multiple examples
# Eg. compare the fraction of actor<>acctress for each year w.r.t n
c = cast
c = c[c.n <=3]
c = c.groupby(['year','type','n']).size()
c = c.unstack('type').fillna(0)
(c.actor / (c.actor+c.actress)).unstack('n').plot(ylim=[0,1])
```


## Merging 

