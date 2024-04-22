> https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/

- In the context of a Seq2Seq RNN, we have a encoder-decoder architecture. 
	- Encoders take each item in the input sequence + an initial hidden state and create a context vector for each individual item they process
		- At each step, the encoder updates the hidden state based on the input token
	- Decoder then takes in this entire output and uses it to progressively generate outputs until we reach the `<EOS>` token
- This context typically is a large vector that encodes some information about the sentence with a typical size being 256, 512 or 1024
- Attention was a new addition to the RNN structure introduced around 2014 where each attention block has access to the entire hidden state produced at all previous time steps. 
	- It then calculates a weightage for each prior hidden state and creates a new final product
	- This in turn creates a weighted sum which amplifies more relevant prior hidden states and reduces the weightage of irrelevant hidden state information
	- We can see massive improvements with the use of these Attention blocks which are applied in a sequential manner to the encoder input
- 