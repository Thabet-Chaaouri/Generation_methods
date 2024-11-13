# Generation_methods


This readme gives a brief overview of the most prominent decoding strategies mainly Greedy search, Beam search, and Sampling.

### Greedy search
Greedy search is the simplest decoding method. It selects the word with the highest probability as its next word.

Repeating words is a very common problem in language generation in general and seems to be even more so in greedy and beam search.

### Beam search

Beam search reduces the risk of missing hidden high probability word sequences by keeping the most likely num_beams of hypotheses at each time step and eventually choosing the hypothesis that has the overall highest probability.

Beam search will always find an output sequence with higher probability than greedy search, but is not guaranteed to find the most likely output.

Beam search heavily suffers from repetitive generation. One of the available remedies is to introduce n-grams (a.k.a word sequences of n words) penalties. but this is hard to control with n-gram- or other penalties in story generation since finding a good trade-off between inhibiting repetition and repeating cycles of identical n-grams requires a lot of finetuning.

Beam search can work very well in tasks where the length of the desired generation is more or less predictable as in machine translation or summarization. But this is not the case for open-ended generation where the desired output length can vary greatly,e.g. dialog and story generation. 

### Sampling

Sampling means randomly picking the next word according to its conditional probability distribution.

The problem with sampling, is that the models often generate incoherent gibberish. A trick to improve this is increasing the likelihood of high probability words and decreasing the likelihood of low probability words by lowering the so-called temperature of the softmax.

In Top-K sampling, the K most likely next words are filtered and the probability mass is redistributed among only those K next words. then the selection happens among the k candidates. However, limiting the sample pool to a fixed size K could endanger the model to produce gibberish for sharp distributions and limit the model's creativity for flat distribution.

Instead of sampling only from the most likely K words, in Top-p sampling chooses from the smallest possible set of words whose cumulative probability exceeds the probability p. The probability mass is then redistributed among this set of words. This way, the size of the set of words (a.k.a the number of words in the set) can dynamically increase and decrease according to the next word's probability distribution.

Top-p can also be used in combination with Top-K, which can avoid very low ranked words while allowing for some dynamic selection.

### Assisted generation
