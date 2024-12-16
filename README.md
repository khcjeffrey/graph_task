# Approach and Design
Constructed heterograph from nodes + edge file, as there were multiple node and edge types.
Although ground truth file was given, when trying to map to the edge file, only few hundred examples were mapped.
The task was mainly on drug-treats-disease, but the node/edge types were slightly different (similar meaning) and therefore grouped.
A train test split of 80/20 was done, no eval set to optimise against hyperparameters due to low match rate to the ground truth.
Due to limitations of some approaches such as Node2Vec, a GCN was trained against the node types of the whole graph (of which node embeddings were generated), then the loss was calculated against predicting the target link. The model was then predicted against the out of sample test set.

Largely, the flow of the script is:
target exploration -> edge file exploration -> node file exploration -> join into a combined graph_df that links src-edge-dst and creates the necessary node ids
-> heterograph build, and node features added (one-hot encode string feature) -> model train -> evaluation

# Thoughts
* Performance looked fine, wonder if training against whole graph before doing link prediction may introduce leakage, as potentially seen test set links?
* Lots of node features had high dimension, so excluded as not sure if could be used directly.
* Some features, like description looked interesting, and could potentially use a language model to process it.
* Would be good to explore how to get feature importance for graph modelling

# Installations
Python requirements: 3.9.6
Package requirements: Create a new venv and pip install -r requirements.txt
File: not uploaded, so please adjust path, which is in the 3rd cell of the ipynb
