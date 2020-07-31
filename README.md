## Dog-classifier-CNNs
Classify the image of the dog into 1 of 133 different dog breeds using CNN (Keras)

Download the dog dataset. Unzip the folder and place it in the repo, at location /dogImages.
- https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip

## Pre-process the Data
When using TensorFlow as backend, Keras CNNs require a 4D array (which we'll also refer to as a 4D tensor) as input, with shape
- (nb_samples,rows,columns,channels)

where nb_samples corresponds to the total number of images (or samples), and rows, columns, and channels correspond to the number of rows, columns, and channels for each image, respectively.

The path_to_tensor function below takes a string-valued file path to a color image as input and returns a 4D tensor suitable for supplying to a Keras CNN. The function first loads the image and resizes it to a square image that is $224 \times 224$ pixels. Next, the image is converted to an array, which is then resized to a 4D tensor. In this case, since we are working with color images, each image has three channels. Likewise, since we are processing a single image (or sample), the returned tensor will always have shape
- (1, 224, 224, 3).

The paths_to_tensor function takes a numpy array of string-valued image paths as input and returns a 4D tensor with shape

- (nb_samples, 224, 224, 3).

Here, nb_samples is the number of samples, or number of images, in the supplied array of image paths. It is best to think of nb_samples as the number of 3D tensors (where each 3D tensor corresponds to a different image) in your dataset!

### Transfer Learning

First, we need to talk about transfer learning. Imagine you trained a neuronal network over a dataset of images to detect cats, you can use part of the training you have done to work over another detecting something else. That's known as transfer learning.

To do transfer learning, you will remove the last fully connected layer from the model and plug in your layers there. The "truncated" model output is going to be the features that will fill your "model". Those are the bottleneck features.

I used transfer learning to create a CNN that can identify dog breed from images.I used the bottleneck features from the Xception model which was pretrained on the Imagenet dataset. The train set is small and similar, an so I slice off the end of the network by adding a global average pooling layer and a fully connected layer with 133 nodes.

Bottleneck features for the Xceotion model can be downloaded from,
- https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogXceptionData.npz

