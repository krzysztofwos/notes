<iframe width="560" height="315" src="https://www.youtube.com/embed/zduSFxRajkE?si=JcTB1XTBrQf2t_Vt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

We have finite context length in the attention in the transformer that we can support for computational reasons, so we do not want to use the raw bytes of the UTF-8 encoding.

We want to be able to support a larger vocabulary size that we can tune as a hyper-parameter, but we want to stick with the UTF-8 encoding of strings.

The [[Byte Pair Encoding]] ([[BPE]]) algorithm will allow us to compress these byte sequences to a variable amount.

We could try to feed raw byte sequences into a transformer model, but we would have to modify the architecture because attention becomes expensive as the sequences become very long.

In the [MEGABYTE](https://arxiv.org/abs/2305.07185) paper, the authors propose hierarchical structuring of the transformer that could allow feeding raw bytes. The authors write, "Together, these results establish the viability of the tokenization-free autoregressive sequence modeling at scale."

# Byte Pair Encoding

We have an input sequence with, say, a vocabulary of four: `a`, `b`, `c`, and `d`. We iteratively find a pair of tokens that occur most frequently. Once we identify that pair, we replace it with a single new token that we append to our vocabulary.

E.g., in the sequence

```
aaabdaaabac
```

the byte pair `aa` occurs most frequently, so we mint a new token `Z` and replace every single occurrence of `aa` with `Z`.

```
ZabdZabac
Z=aa
```

We converted an 11-character sequence with a vocabulary of 4 into a 9-character sequence with a vocabulary of 5.

Then, we repeat the process, replacing `ab` with `Y`.

```
ZYdZYac
Y=ab
Z=aa
```

Finally, we do the same with `ZY`, which gives a sequence that cannot be compressed further.

```
XdXac
X=ZY
Y=ab
Z=aa
```

We now have 5 tokens with a vocabulary of 7. In this way, we can iteratively compress our sequence as we mint new tokens.

In the same way, we start with byte sequences and iteratively mint new tokens, appending them to our vocabulary and replacing the most common byte pairs.

# Tokenizer

The tokenizer is a completely separate object from the language model itself. It is usually a completely separate pre-processing stage. The tokenizer has its own training set and is trained using the BPE algorithm.

Once we train the tokenizer and have the vocabulary and the merges, we can do both encoding and decoding.

The tokenizer is a translation from the raw text (a sequence of Unicode code points) into a token sequence and vice versa.

## Special Tokens

```python
enc = tiktoken.get_encoding("gpt2")
enc.n_vocab  # 256 raw byte tokens, 50,000 merges, 1 special token
```

The `<|endoftext|>` special token delimits documents in the training set. We use this as a signal to the language model that the document has ended, and what follows will be unrelated to the document seen previously.

`<|endoftext|>` is the token number 50256.

# tiktoken vs. SetencePiece

- tiktoken encodes to UTF-8 and then BPEs the bytes
- SentencePiece BEPs the code points and optionally falls back to UTF-8 bytes for rare code points, which then get translated to byte tokens. Rarity is determined by the `character_coverage` hyperparameter.

# Quirks of LLM Tokenization

[YouTube](https://www.youtube.com/watch?v=zduSFxRajkE&t=6701s)
