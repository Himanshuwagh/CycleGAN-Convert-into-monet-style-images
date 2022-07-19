## CycleGAN-Monet_images

Image-to-image translation involves generating a new synthetic version of a given image with a specific modification, such as translating a summer landscape to winter.

Training a model for image-to-image translation typically requires a large dataset of paired examples. These datasets can be difficult and expensive to prepare, and in some cases impossible, such as photographs of paintings by long dead artists.

#### Few methods to perform style translation

### 1. Neural Style Transfer
Using an optimization technique called neural style transfer, two images—a content image and a style reference image (such as a piece of art by a well-known painter)—are combined to create an output image that resembles the content image but is "painted" in the manner of the style reference image. Numerous well-known Android and iOS apps, including Prisma, DreamScope, and PicsArt, utilise this technology.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20200820225906/styletransferexample.PNG" width=50%>

### 2. Cycle-GANs

Using the CycleGAN method, image-to-image translation models are automatically trained without the use of paired samples. Unsupervised learning is used to train the models using a set of photos from the source and target domains that are unrelated in any way.

This straightforward method is effective and produces visually attractive results across a variety of application domains, most notably when converting images of horses to zebras and vice versa.

### CycleGAN Model Architecture

We will develop an architecture of two GANs, and each GAN has a discriminator and a generator model, meaning there are four models in total in the architecture.

The first GAN will generate images of monet style given normal pictures, and the second GAN will generate normal pictures given photos of monet style images.

- GAN 1: Translates photos (collection 1) to monet-style images (collection 2).
- GAN 2: Translates monet-style images (collection 2) to photos (collection 1).

Every GAN has a conditional generator model that, given an input image, will create an image. To determine how likely it is that the generated image came from the target image collection, each GAN also has a discriminator model. Similar to a typical GAN model, the discriminator and generator models for a GAN are trained under conventional adversarial loss.

We can summarize the generator and discriminator models from GAN 1 as follows:

- Generator Model 1:             
Input: Takes photos of summer (collection 1).               
Output: Generates photos of winter (collection 2).
- Discriminator Model 1:             
Input: Takes photos of winter from collection 2 and output from Generator Model 1.             
Output: Likelihood of image is from collection 2.       

Similarly, we can summarize the generator and discriminator models from GAN 2 as follows:

- Generator Model 2:          
Input: Takes photos of winter (collection 2).                
Output: Generates photos of summer (collection 1).
- Discriminator Model 2:           
Input: Takes photos of summer from collection 1 and output from Generator Model 2.                  
Output: Likelihood of image is from collection 1.
