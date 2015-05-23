# DeepSpec
Standardized spec for describing any neural network model - to use with deep learning frameworks.


---
### First Meeting 

Following are initial notes from the first meeting. Use this as a space to work through these thoughts on how to build a standardized spec for neural net configurations:

ayer - has params and followed by one activation and activations
hyperparameters - changes gradient - modify propertities of model and output response from layer (changes behavior of layer) - not what model is doing - changes what its learning
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
