> Link : http://jalammar.github.io/illustrated-transformer/

- A transformer consists of multiple encoder - decoder blocks. 
	- Each individual block is completely separate from each other and they don't share weights. 
- Inputs flow in as text
	- Text gets tokenised
	- Tokens get mapped to a $n_{dim}$ embedding which is unique to each individual token
	- Tokens then pass through an entire transformer block
		- First step is self-attention where each token's embedding gets mapped to a low rank embedding dimension that the block has learnt. 
		- We then calculate a weightage for every token prior to this current token that sums up to 1 before using it to calculate a weighted sum for that specific token
		- This then gets used in a feed forward later which adds more semantic meaning to this specific representation
		- **Note** : The initial self-attention results in each token's path through the self-attention block being dependent on each other but the feed forward network is one that can be parallelised easily
	- Inside this transformer block, we typically utilise what is known as [Multi Headed Attention](Multi%20Headed%20Attention) by splitting up the embedding matrix into smaller chunks before multiplying each chunk by a different 