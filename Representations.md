
Embedding Models are used for us to find similar items to what we've embedded. All assumptions of the similarity are baked into the dataset that you used.

Therefore it's important to log our data now so that we have enough data to fine-tune embedding models later.

## How to get Data

We can log in a match of 

```
Query -> Desired Output
```

```
Query, passage, is_relevant
query, passage, is_cited
```

It's useful to think about this so that we can fine tune something like a COLBert or Cohere model

Eg. If we have `query -> retrieved chunk`, we can just choose another random non-relevant chunk randomly from the database.