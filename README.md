# MultimodalityProject

## CLIP (2021)

CLIP architecture: [CLIP](docs/CLIP.png)

CLIP uses the following text encoder and image encoder:

1. text encoder: a standard transformer (attention is all you need)
2. image encoder: ResNet; ViT

## Dynamic Token Pooling (2022)

Motivations:

1. vanilla transformers are inefficient
2. general pooling technique: we can merge groups of tokens to reduce sequence length in the intermediate layers (later, these **pooled** representations are up-sampled back to the original length). Example: Hourglass Transformer has **3** transformer blocks: downsample, process, and upsample.
3. fixed-size pooling is suboptimal: (i) **size** misalignment; (ii) different **degrees** of information (e.g., speaking/silence carry different amount of information)

DPT architecture: [DPT](docs/DPT.png)

neural boundary predictor: it's a sequences of 1s and 0s (1 represents a boundary), implemented as 2-layer MLP; it can effectively replace **off-the-shelf** tokenizers (BPE, Unigram) since they are inconsistent during autoregressive inference.

The neural boundary predictor can be learned upon the following objectives:

1. main objective: **end-to-end** training based on the model perplexity
2. auxiliary objective: tokenization as supervision with Unigram
3. spikes of conditional entropy (reasoning: Empirically, entropy spikes in language models overlap with word boundaries to a significant degree)
4. linguistically inspired segments (we put a boundary after a whitespace character - no need to train)

## My brainstormed project ideas

### DTP-CLIP

DTP-CLIP: use dynamic token pooling for image and text encoders in CLIP to boost efficiency (potentially we combine it with mini-techniques like quantization, pruning, or distillation, etc.)
