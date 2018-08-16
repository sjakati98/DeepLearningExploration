# Summary of the [Tutorial on Variational Autoencoders](https://arxiv.org/pdf/1606.05908.pdf)
  The idea behind generative unsupervised learning is to create a model which accurately describes some complicated distribution. In computer vision, this could be the relationship between different pixels within an image.
  Variational autoencoders utilize neural networks to provide a way to train a model using backpropagation. This, in turn, means that VAEs make weak assumptions about the distribution and are relatively *easy* to train.

#### Latent Variable Models
* [Useful Slides](http://www.econ.upf.edu/~michael/latentvariables/lecture1.pdf)
* A latent variable is another term for a hidden variable.
* By definition, latent variables are inferred from the information of observed variables and also are assumed to affect the response variables
* A latent variable model is some mathematical model which hopes to accurately capture some distribution

### Encoder

The encoder of a VAE is a neural network; the input is a datapoint *x* and its output *z* is a feature representation of that
initial datapoint. In terms of computer vision, this *x* is most likely an image, and *z* is the features extracted from that image by some convolutional network.
Now if consider an image that is 10px by 10px, we are looking at a 100-dimensional space *x* and the conv network then "encodes" the image into some latent space *z*.

This space *z* is stochastic, as the latent space is of a Gaussian probability density. 

### Decoder

The decoder of a VAE is also a neural network. The input to this network is the previous, *z*, and it outputs the reconstruction log-likelihood.
This is output would have lost some information of the original image. The log-likelihood itself fills the same dimensions as the original input *x*, and each pixel within the newly reconstructed
image is decided by the aforementioned log-likelihood distributions.


### In Practice (As I Understand It):

The main idea is the create a network that can accurately extract features from an input, and represent them in the latent space, *code*, and then use a similar network to decode the latent space. The training procedure is to take that decoded output, and test against a [KL-Divergence](https://www.countbayesie.com/blog/2017/5/9/kullback-leibler-divergence-explained), and have a reconstruction loss. So, in contrast to an adversarial training process, the loss function is not assessing whether or not the image is realistic to another network but rather assessing how much information is lost in the approximation of the original distribution (original image).
