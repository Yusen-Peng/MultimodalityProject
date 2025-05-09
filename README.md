# MultimodalityProject

## Dynamic-Pooling Transformer

Motivations:

1. vanilla transformers are inefficient
2. general pooling technique: we can merge groups of tokens to reduce sequence length in the intermediate layers (later, these **pooled** representations are up-sampled back to the original length). Example: Hourglass Transformer has **3** transformer blocks: downsample, process, and upsample.
3. fixed-size pooling is suboptimal: (i) **size** misalignment; (ii) different **degrees** of information (e.g., speaking/silence carry different amount of information)

DPT architecture: [DPT](docs/DPT.png)

neural boundary predictor: it's a sequences of 1s and 0s (1 represents a boundary), implemented as MLP; it can effectively replace **off-the-shelf** tokenizers (BPE, Unigram) since they are inconsistent during autoregressive inference.

The neural boundary predictor can be learned upon one of the following training objectives:

1. end-to-end based on the model perplexity
2. tokenization as supervision with Unigram
3. spikes of conditional entropy (reasoning: Empirically, entropy spikes in language models overlap with word boundaries to a significant degree)
4. linguistically inspired segments ()

## CLIP review

## My brainstormed list

1. CLIP-variants
   1. ww
2. others
