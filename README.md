# Code Elucidation

Elucidation of implicit generative models from common data compression
algorithms.

## Introduction

A codec is an algorithm for compressing and decompressing data, often of
a specific modality such as text or video. Codecs consist of a
encoder/code, which describes data in a more concise form, and a decoder
which reconstructs data from its encoding. We\'ll be concerning
ourselves mainly with the former.

Let $L_C(x)$ denote the length of $x$ when compressed using some code
$C(\cdot)$.

According to the Kraft-McMillan inequality, if $C$ is uniquely
decodable, then there exists a probability distribution $p_C$, such that
$p_C(x) = 2^{- L_C(x)}$. In other words, for any uniquely decodable
code, we can always find a *statistical model* which produces matching
code-lengths.

Now, since $p_C$ is a generative model, it should in theory be possible
to sample from it. In this way, codecs can be used to *create* data
rather than just compress it. Now, for many codecs, the generated data
is unlikely to be very interesting because they aren\'t tuned to
*specific* sources such as \"English text.\" Nonetheless, this exercise
is useful for elucidating the implicit statistical assumptions present
in human-designed compression schemes.


## Method

Let\'s be a little more precise about what we\'re attempting to do.

Given some code $C(\cdot)$, we wish to sample from $p_C$ where
$p_C(x) = 2^{-L_C(x)}$.

1.  At each time step $t$, we compute the distribution
    $p_C(x_1,\dots,x_t) = 2^{-{L_C(x_1,\dots,x_t)}}$. We then use top-k
    sampling to redistribute the probability mass amoungst $k$ *most
    likely* sequences.
    
2.  We then randomly sample from the top-k distribution and return to
    step 1.


## Results

Our method successfully helped elucidate the implicit statistical 
assumptions in coding schemes such as LZMA and RLE. This form of
feedback may aid in creating more effective coding schemes in 
future.
