This is just the 

$$
ASL_{q,d} = \text{irrel}_{q,d} + 1
$$
Where $\text{irrel}_{q,d}$ is simply the number of irrelevant documents above the relevant document $d$ for query $q$. This means that if our relevant document is not within the set of predicted documents, then the value is just equal to the number of predicted documents returned by the system.

Then we can scale this out to $n$ queries with $n_q$ relevant documents each

$$
ASL = \frac{1}{Q} \sum_{q=1}^Q \frac{1}{n_q} \sum_{d=1}^{n_q} ASL_{q,d}
$$

This in turn reduces the quality of the BM25 metric relative to others

![](assets/CleanShot%202024-06-17%20at%2012.26.46.png)