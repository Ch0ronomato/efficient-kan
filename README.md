# An Efficient Implementation of Kolmogorov-Arnold Network

This repository contains an efficient implementation of Kolmogorov-Arnold Network (KAN).
The original implementation of KAN is available [here](https://github.com/KindXiaoming/pykan).

The performance issue of the original implementation is mostly because it needs to expand all intermediate variables to perform the different activation functions.
For a layer with `in_features` input and `out_features` output, the original implementation needs to expand the input to a tensor with shape `(batch_size, out_features, in_features)` to perform the activation functions.
However, all activation functions are linear combination of a fixed set of basis functions which are B-splines; given that, we can reformulate the computation as activate the input with different basis functions and then combine them linearly.
This reformulation can significantly reduce the memory cost and make the computation a straightforward matrix multiplication, and works with both forward and backward pass naturally.

The problem is in the **sparsification** which is claimed to be critical to KAN's interpretability.
The authors proposed a L1 regularization defined on the input samples, which requires non-linear operations on the `(batch_size, out_features, in_features)` tensor, and is thus not compatible with the reformulation.
I instead replace the L1 regularization with a L1 regularization on the weights, which is more common in neural networks and is compatible with the reformulation.
The author's implementation indeed include this kind of regularization alongside the one described in the paper as well, so I think it might help.
More experiments are needed to verify this; but at least the original approach is infeasible if efficiency is wanted.

Another difference is that, beside the learnable activation functions (B-splines), the original implementation also includes a learnable scale on each activation function.
For simplicity, I remove this scaler since the learnable activation functions are able to learn magnitudes as well.
If further experiments show the necessity of this scaler, I will add it back.
