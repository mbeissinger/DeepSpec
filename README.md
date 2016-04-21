# DeepSpec
Standardized spec for describing any neural network model - to use with deep learning frameworks.

## Overview
DeepSpec is the start of a DSL for creating deep networks. It is motivated by the composability and basic layer-wise focus of deep learning models. By making a standard for a deep learning DSL, we can speed up the discussion of neural networks for research and production systems.

---
### First Meeting 

Following are initial notes from the first meeting. Use this as a space to work through these thoughts on how to build a standardized spec for neural net configurations:

The pseudo regex-like pattern for creating a deep network:
(input_data) (output_modifiers)\* (?P<layer\> (layer_computation) (output_modifiers)\* )\+ 


**Input data**:

+ The unmodified data directly from source.


**Output modifiers**:

+ These are functions without learnable parameters that transform the information flow/data in the network.
+ Considered hyperparameters.
+ Can be stacked in any order.
+ Used in two places:
    * Before first layer computation (modifying data directly from source).
    * After layer computation.
+ Possible types of modifiers:
    * Affine transforms
    * Nonlinear function (activation)
    * Pooling/subsampling/sampling
    * Mirroring/concatenation
    * Noise (this modifies information flow, but it also belongs as a training modifier)
        - Dropout
        - Gaussian
        - Uniform
        - Salt & pepper


**Layer**:

+ The main repeating unit when building deep networks.
+ Uses the learnable layer parameters to perform the main computation transforming an input to a response.
+ Deal with multiple inputs/outputs? (especially important for recurrent case, but also other layer types)
+ Basic types of computation:
    * Linear ('dense' or  'fully-connected')
    * Convolution
    * Recurrent
    * Recursive
    * Autoencoding/unsupervised? (using tied weights to make the response in the same space as input)
+ Hyperparameters:
    * Layer config: anything that is necessary for setting up the layer's computation
        - computation function (type of convolution, etc.)
        - input size
        - output size
        - hidden size
        - filter shapes
        - etc.
    * Trainer modifiers: anything that affects the optimization algorithm specifically for the layer.
        - learning rate scalers
        - regularization (l1/l2, noise from output modifiers?)
        - type of optimization function
        - gradient clipping
        - cost function
    * Output modifiers: considered a hyperparameter to a layer


**Trainer/Optimization**:

+ Global settings for training the entire network.
+ These get overrided by layer-specific trainer modifiers.
+ Optimizes last layer cost function with original data input.


---
layer - has params and followed by one activation and activations hyperparameters - changes gradient - modify propertities of model and output response from layer (changes behavior of layer) - not what model is doing - changes what its learning
     - change model computation
(data modifier) transforms, activation & noise - transform response - can have multiple after - can stack 
trainer - holds the optimization methods and hyperparameters

Group modifiers:
     input / output modifiers
     internal modifiers
     trainer modifiers (noise and learning rate scaling, regularization) = dropout/gaussian/uniform/ salt & pepper,  scaling, cost function


input activation on input

CNN
     Convolution (layer)
     Downsampling / pooling / subsampling (Activation)
     Relu (Activation)
     Fully Connected (Layer)
     Softmax (Activation)

---
### Questions

+ What to do with noise? It modifies information flow and is stacked with those functions, but it is really just regularization and a trainer modifier.
+ Considering the autoencoding case where tied weights are used? Is sharing model parameters enough to warrent a new layer type?
+ How to deal with multiple inputs and outputs to a layer computation?

---
### Second meeting
Layers -> just variables and responses.

Describe an autoencoder with this framework?
Describe a convnet with this framework?
Describe an rnn with this framework?