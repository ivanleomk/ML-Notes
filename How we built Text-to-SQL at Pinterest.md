---
URL: https://medium.com/pinterest-engineering/how-we-built-text-to-sql-at-pinterest-30bad30dabff
---
- They use Querybook under the hood to be able to make this happen with a LLM
- User is asked to explicitly select the tables ( Ensures that we have full visibility into what needs to be done )
	- Users themselves know what the queries should look like - they are domain experts ( Therefore AI is used to generate boilerplate )

They extract out these specific columns from the table metadata store

```

- Table name
- Table description
- Columns
- Column name
- Column type
- Column description
```

For specific values with a low cardinality (Eg. Platform == web), they also encode it into the prompt itself. For example, the where clause in the response might bewhere platform=’web’ as opposed to the correct where platform=’WEB’.

Extremely large table schemas might exceed the typical context window limit. To address this problem, we employed a few techniques:

- Reduced version of the table schema: This includes only crucial elements such as the table name, column name, and type.
- Column pruning: Columns are tagged in the metadata store, and we exclude certain ones from the table schema based on their tags.

## Performance
- Few Shot acceptance was around 40%
- In practice, most queries that are generated require multiple iterations of human or AI generation before being finalised. 
- In our real world data (which importantly does not control for differences in tasks), we find a 35% improvement in task completion speed for writing SQL queries using AI assistance.

- RAG for better selection ( They have a few thousand tables in production so not feasible to combine everything into the prompt - maybe not an issue now with gemini 1M context window lmfao )
	- Generate a list of embeddings of historical queries for each table( so each table has a set of potential query types) and the table summaries
	- Top N tables are then compiled into a single prompt for a LLM to select the best model to choose the top k relevant tables from
	- Idea here is to surface potential tables that might be relevant to what the user needs

## Data Processing

They embed both the table summary and the query summaries 

![](assets/Pasted%20image%2020240819141819.png)

1. Retrieve the table schema from the table metadata store.
2. Gather the most recent sample queries utilizing the table.
3. Based on the context window, incorporate as many sample queries as possible into the table summarization prompt, along with the table schema.
4. Forward the prompt to the LLM to create the summary.
5. Generate and store embeddings in the vector store

![](assets/Pasted%20image%2020240819141917.png)
## Final Selection
They then use these embeddings to return the relevant tables for the task so we have two rounds of fitering
![](assets/Pasted%20image%2020240819142039.png)
## Evals

They used the initial manual user selection process to create a validation set to determine the performance of embedding based search + open search vs the original manual selection.

Goal was to ensure that there wasn't any performance degredation

the search hit rate without table documentation in the embeddings was 40%, but performance increased linearly with the weight placed on table documentation up to 90%.

## Future work

One potential improvement could be the inclusion of further metadata such as tiering, tags, domains, etc., for more refined filtering during the retrieval of similar tables.

Currently the vector index is generated manually. Implementing scheduled or even real-time updates whenever new tables are created or queries executed would enhance system efficiency.

Implementing query validation, perhaps using a constrained beam search, could provide an extra layer of assurance.

Introducing a user interface to efficiently collect user feedback on the table search and query generation results could offer valuable insights for improvements. 

Such feedback could be processed and incorporated into the vector index or table metadata store, ultimately boosting system performance, this allows us to fine-tune an embedding model.