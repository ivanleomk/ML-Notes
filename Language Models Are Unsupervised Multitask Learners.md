> Language models can perform down-stream tasks in a zero-shot setting ( without using any examples ) that does not require any parameter or architecture modification yet achieve state of the art performance in different tasks
## Background

It is difficult for specialised systems to generalise to slight changes in the data distribution. The traditional approach was to collect a dataset of training examples demonstrating correct behaviour for a desired task, train a system to imitate these behaviours and then test its performance on independent and identically distributed held-out examples.

These datasets need to include hundreds to thousands of examples to induce functions which generalise well. Therefore it is difficult to scale the creation of said datasets with current techniques. 

Models learn to estimate a conditional distribution of $p(output|input)$ from the training dataset which in turn allows them to perform tasks in a zero-shot setting. For instance, a translation training example can be written as

```
translate_to_french, english_text, french_text
```

This can in turn be easily modified to a test example by removing the `french_text` to achieve the following.
```
translate_to_french, english_text,
```

## Model

### Datasets

They used a new curated dataset called `WebText` which contains a text subset of 45 million reddit links that each received at least 3 karma points. They then did some de-duplication and heuristic based cleaning before removing all wikipedia documents to prevent any data contamination.

Prior models had used Common Crawl which is a free/open-source scrapped version of the internet. However, a major criticism of Common Crawl is that a large amount of documents are mostly unintelligible. 

### Tokeniser

The model uses a BPE encoder to encode text input to be processed.

### Architecture

They use a vanilla transformer architecture with the following modifications

- Layer Normalisation moved to the input of each sub-block
- 