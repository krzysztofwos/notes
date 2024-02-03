<iframe width="560" height="315" src="https://www.youtube.com/embed/_7rMfsA24Ls?si=oeyYvoQ5fPefNi7H" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Suppose we have a function $f$ that, given an input image, outputs the probability of whether the input is a handwritten image. We can use $f$ to generate handwritten digits.

Let's say the input is 28x28=784 pixels. Pick one of the pixels, make it a little bit darker, pass it through $f$, and see what happens to the probability that it is a handwritten digit.

As we modify various pixels in the image, the probability of the result being a handwritten digit will change. We can do that for every single pixel, finding out which ones, if we make them a little bit lighter, make the image more like a handwritten digit and which ones, if we make them a bit darker, make the image more like a handwritten digit.

By doing that, we can get the gradient of the probability that the input is a handwritten digit with respect to individual pixels.

Suppose a function $f$ that, given a 28x28 pixel input image $X$, outputs the probability that $X$ is a handwritten digit. This function $f$ can be a neural network with weights $\omega$, trained to recognize handwritten digits.

Let $L = f(\omega, X)$ represent the loss function or the probability output by $f$, depending on the context. In a classification task, $L$ could represent the negative log-likelihood of the correct class, which we aim to minimize during training.

The gradient of $L$ with respect to the input image $X$, denoted as $\nabla_X L$, quantifies how small changes in each pixel value $x_{ij}$ of $X$ influence the value of $L$. This gradient is a matrix of the same dimension as $X$ (in this case, 28x28), where each element $(i, j)$ represents the partial derivative of $L$ with respect to the pixel at position $(i, j)$ in the image:

$$
\left( \nabla_X L \right)_{ij} = \frac{\partial L}{\partial x_{ij}}
$$

If $L = f(\omega, X)$ represents the probability that $X$ is a handwritten digit, then $\nabla_X L$ indicates how making each pixel slightly brighter or darker would affect this probability. A positive derivative suggests that increasing the pixel's intensity would increase the probability of $X$ being a handwritten digit and vice versa.

Now, we can change the pixels according to these gradients. So, we are doing something similar to what we do when we train neural networks, except instead of changing the weights in the model, we are changing the inputs to the model. We take each pixel and subtract its gradient to get a new image.

Suppose we have this magic function $f$. In that case, we can use it to turn something that looks like arbitrary noisy input into something that looks like a handwritten digit—something that has a high probability value—by using this derivative.

Generally speaking, in this course, when we want some magic black box to exist and it doesn't exist, we create a neural net and train it. So, we create a neural net that tells us which pixels to change to make an image look more like a handwritten digit.

We could create some training data and use that training data to get the information we want. We could pass something that looks a lot like a handwritten digit, something that looks a bit like a handwritten digit, something that doesn't look very much like a handwritten digit, and something that doesn't look like a handwritten digit at all. It's very easy to create these—create handwritten digits and add random noise.

It would be difficult to come up with a score that measures how much an image looks like a handwritten digit, so instead, we can predict how much noise was added. Start with a handwritten image dataset and add noise. An image with no noise is very much like a handwritten digit, and an image with a lot of noise is not like a handwritten image at all.

Let's create a neural net. We can think of a neural net as a black box that has some inputs, outputs, weights, a loss function, and a derivative that is used to update the weights.

We can consider the noise as normally distributed $\mathcal{N}(\mu, \sigma)$ with mean $\mu = 0$ and some variance $\sigma$. We can use the variance $\sigma$ as the output. Or we can predict the noise itself. If we do that, the loss is going to be very simple: take the input, pass it through the neural net, try to predict what the noise was. We can use the MSE loss.

The input is noisy digits, the output is noise, and the neural network is trying to predict the noise.

We wanted to know how much we need to change the pixels in order to get something that is more digit-like. To turn the noisy image into a digit, we have to remove the noise. If we can predict the noise, we get exactly what we want.

We now have something that can generate images. We can take this trained neural network and we can pass it pure noise.

# Denoising Network — U-Net

This denoising network, [[U-Net]], is the first component of [[Stable Diffusion]]. The input to the U-Net is a somewhat noisy image. The output is the noise, such that if we subtract the output from the input, we end up with a less noisy image.

![[Lesson 9 Deep Learning Foundations to Stable Diffusion, 2022 1-22-48 screenshot.png]]

# Autoencoder — VAE

We have 784 pixels. For a 512x512x3 image, we would have 786,432 pixels. Training the model above for images of this size would take a very long time. To do this more efficiently, we can use a compressed representation.

For example, we can compress an image by putting it through a convolutional layer with stride 2. We start with a 512x512x3 image. We get, say, 256x256x6 (doubling the number of channels) and do it again and again. We get 128x128x12 and 64x64x24. Then, we put it through ResNet blocks to get 64x64x4, or 16,384 pixels. So, we've compressed the image 48 times. Can we get the image back again?

We can create inverse convolution that does the opposite. We take 64x64x4 images through inverse convolutions. We get 128x128x12, ..., all the way to 512x512x3. Initially, what comes out will be random noise. But if we train this with the Mean Squared Error (MSE), this model will try to recover the exact same image that went into it. If it does that successfully, the MSE will be zero.

This is an autoencoder. The reason it is interesting is that we can split it in half. We can put an image through the first half, which is called the encoder. We can save the output of the encoder and use it as a compressed representation. We can then feed this into the decoder and get back the original image. This way, we have created a compression algorithm. We have created a very powerful compression algorithm.

![[Lesson 9 Deep Learning Foundations to Stable Diffusion, 2022 1-40-8 screenshot.png]]

We use the autoencoder and train our U-Net using an encoded version of each picture. The U-Net now takes a somewhat noisy version of the latent representation (latent). The input is somewhat noisy latents, and the output is still noise.

We take the output of the U-Net and pass it through the decoder part of the autoencoder. The output is a large image.

The autoencoder we use is called the [[VAE]].

The use of latent representation is optional, but it saves a lot of compute.

# Guidance

How can we modify the architecture above so that rather than feeding in just noise and getting back some digit, how do we get it to give us a particular digit?

What if we were to pass in the number "3" plus some noise and have it generate a handwritten "3" for us? How would we do that?

In addition to passing in the input to the model, we can also pass in a one-hot-encoded version of what the digit the input represents. Now, the model is going to learn to predict what the noise is knowing what the input image was.

Now, if we feed in the number "3" plus some noise after the model is trained, the model will say that the noise is everything that doesn't represent the number "3".

In Stable Diffusion, we use a model that takes a sentence, e.g., "a cute teddy," and returns a vector of numbers that represents what a cute teddy looks like. To do that, we train a model on captioned images from the Internet.

> Once we define the inputs, the outputs, and the loss function, the neural nets will do something.

We train two models: a text encoder and an image encoder. We then line up the embeddings from both models so that the embeddings for the image and the embeddings for the text describing the image are similar.

We can use the dot product to express vector similarity. We take the dot product of the embedding of the image and the embedding of the text, and we want to maximize that number. We do that for all images and all captions. This gives us a loss function.

![[Lesson 9 Deep Learning Foundations to Stable Diffusion, 2022 1-57-46 screenshot.png]]

This model is called [[CLIP]], and this kind of loss is called [[Contrastive Loss]].

![[Lesson 9 Deep Learning Foundations to Stable Diffusion, 2022 2-0-2 screenshot.png]]

So, we have U-Net that can denoise noisy latents (including pure noise), we have a VAE decoder that can take latents and create an image, we have a CLIP text encoder which allows us to train a U-Net which is guided by captions.

# Inference

We can create a noising schedule that, given a number, e.g., from 1 to 1000, gives us a value $\beta$—how much noise to use. This is what people sometimes refer to as the time step.

Each time we create a mini-batch to pass into the model, we randomly pick an image from the training set, randomly pick the amount of noise, add the noise to each image, and use that mini-batch to train the model.

At inference, we subtract just a bit of the noise by multiplying the output from the U-Net by some constant $c$ to produce a bit less noisy latent. This looks like a Deep Learning optimizer.

# Diffusion Models vs. Differential Equations

Diffusion models came from the world of differential equations. There are many very parallel concepts in the world of differential equations. A lot of differential equation solvers use the same kind of ideas as optimizers.

One interesting thing that the differential equation solvers do is that they take $t$ as an input. And pretty much all diffusion models also take $t$ as an input. The idea is that the model will be better at removing the noise if you tell it how much noise there is.

We can think about diffusion models as an optimization problem rather than a differential equations-solving problem.
