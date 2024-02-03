<iframe width="560" height="315" src="https://www.youtube.com/embed/6StU6UtZEbU?si=PHZ9f7XnkFQB5KNW" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# APL

https://tryapl.org/

https://forums.fast.ai/t/apl-array-programming/97188

Tensor programming and array programming go back to a language called [[APL]]. It is originally a mathematical notation that was developed in the mid to late '50s, which at first was used to define how certain IBM systems would work. It was a replacement for mathematical notation that was designed to be more consistent and more expressive. It was developed by [[Ken Iverson]]. In the 1960s, some implementations that allowed this notation to be executed on a computer appeared.

```apl
      a ← 3 5 7
      a
3 5 7
      a×3
9 15 21
      a-2
1 3 5
      b ← 6 3 9
      a÷b
0.5 1.666666667 0.7777777778
```

Tensors are rectangular blocks of numbers that can be 1-dimensional, like an array, 2-dimensional, like a matrix, 3-dimensional, like a batch of matrices, and so on.

# Random Numbers

```python
if os.fork():
    print(f"In parent: {torch.rand(1)}")
else:
    print(f"In child: {torch.rand(1)}")
```

```text
In parent: tensor([0.9019])
In child: tensor([0.9019])
```

PyTorch, by default, fails to initialize the random number generator.
