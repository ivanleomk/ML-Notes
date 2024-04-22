> Link : https://nostalgebraist.tumblr.com/post/185326092369/the-transformer-explained

#elicitml #transformers #article

- It's useful to understand transformers as an evolution of our solutions to understanding inputs that must be understood in their entire context.
	- Classic Neural Nets: All input is treated as largely independent
	- CNNs : We understand a specific input and apply a fixed computation to a subset of the input using a kernel. Suffers from issues of locality - whereby we can only examine a specific portion of the input at any given time.
	- RNNs : We iteratively process each token/word in our element and then work off that to update a hidden state. Solutions to long term dependencies were LSTMs and GRUs but still suffer from training instability/inefficiency
		- RNNs can only process information in a single direction - it tries to understand subsequent inputs with respect to previous tokens/words. We try to solve this with a biLSTM but this doesn't solve the issue of a finite scratchpad to process all long/short term dependencies
- Attention tries to solve this problem by allowing each token to view every other token in relation to every other token. 
	- We have three matrices
		- Keys : Information about a token/word might match
		- Query : Information about what a token/word is looking for
		- Value: The semantic meaning of a specific token/word
	- MHA fundamentally allows us to learn different representations of these words/tokens where the number of keys/queries/values per words is the “number of attention heads"
- By stacking multiple layers of these attention blocks, our initial understanding of this token becomes more complex
	- The value stored for each position, which starts out as just the word, becomes a progressively more “understood” or “processed” thing, representing the word in light of more and more sophisticated reverberations from the context.
	- We also add in a positional encoding in order to tell each attention layer how each token lives relative to one another
- The individual model architecture then comes about based on how we arrange these blocks together