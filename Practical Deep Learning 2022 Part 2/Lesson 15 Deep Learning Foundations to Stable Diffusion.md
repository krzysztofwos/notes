<iframe width="560" height="315" src="https://www.youtube.com/embed/0Hi2r4CaHvk?si=ok73ToMag5k4iF7z" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Convolutional autoencoder

[[im2col]] is a way of converting a convolution into matrix multiplication

https://hal.inria.fr/inria-00112631/

https://github.com/Yangqing/caffe/wiki/Convolution-in-Caffe:-a-memo

# Autoencoder

Start with an input image of 28x28 pixels. Put it through a stride-2 convolution with two channels. It outputs a 14x14x2 tensor. We have reduced the height and width by two but added an extra channel, so overall, it's a 2x decrease in parameters. Then, we can do another stride-2 convolution with four channels. We have a 4x reduction in the number of parameters compared to the input. This is a form of compression.

We could add a group of convolutional layers that increases the size instead. One strategy is to use [[nearest neighbor upsampling]] and then apply a stride-1 convolution.

```python
def deconv(in_channels, out_channels, kernel_size=3, act=True):
    layers = [
        nn.UpsamplingNearest2d(scale_factor=2),
        nn.Conv2d(
            in_channels,
            out_channels,
            stride=1,
            kernel_size=kernel_size,
            padding=kernel_size // 2,
        ),
    ]
    if act:
        layers.append(nn.ReLU())
    return nn.Sequential(*layers)
```

When training the autoencoder, the loss function is applied to the output of the model and the input:

```python
def fit(epochs, model, loss_func, opt, train_dl, valid_dl):
    for epoch in range(epochs):
        model.train()
        for xb, _ in train_dl:
            loss = loss_func(model(xb), xb)  # Here!
            loss.backward()
            opt.step()
            opt.zero_grad()
        eval(model, loss_func, valid_dl, epoch)
```

We are trying to recreate the original.
