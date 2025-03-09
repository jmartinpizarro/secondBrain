---
aliases:
  - Convolution
tags:
  - machine-learning
  - neural-networks
References: 
cssclasses:
---
# Convolution

Consists of extracting tiles of the input feature map, and applies filters (a matrix) to them to compute new features (output feature map); which usually differ from size and depth than the input feature map. Convolutions are defined by two parameters:
- **size of the tiles extracted**: usually a 3x3 or 5x5 matrix
- **depth of the output feature map**: corresponds with the number of filters applied
During the training, the CNN learns the optimal values for the filters matrixes that allow to extract important attributes.

For each filters added, the networks gives less and less incremental value than the previous one. 

>[!DANGER]
>The main objective of the engineers who build this networks is to apply the fewer filters as possible, **reducing time of training and computational cost**.

### ReLU

After each iteration of convolution, the CNN applies to the new atribute a transformation function, introducing a non-linearity to the model.
$$f(x)=max(0, x)$$
### Aggrupation

After ReLU, a reduction phase is applied; where the atribute obtained is reducing (for reducing computational cost). 

Similarly as convolution, we travel through the output matrix, having a frame or windows where it is a applied a $max()$ function. It is usually based on two parameters:
- **size**: generally a 2x2 matrix
- **stride**: the distance, in pixels, that separated each extracted matrix