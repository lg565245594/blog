---
title: Whether language evolved with the brain or the brain evolved with language
date: 2024-08-19 10:31:19
tags:
---
Whether language evolved with the brain or the brain evolved with language [Geoffrey Hinton](https://www.youtube.com/watch?app=desktop&v=n4IQOBka8bc&t=1531s).

### 3 different views of language and how they relate to cognition
1st, symbolic view: cognition consists of having strings of symbols in some cleanup logical language where is no ambiguity and applying rules of inference, cognition is just these symbolic manipulations on things are like the language symbols.

2nd view. Once you get inside the head, it's all vectors, symbols come in, you convert these symbols into big vectors, and if you want output you produce symbols again. There is a point in machine translation in 2014, where people used recurrent neural nets(RNN) and words keep coming in and having a hidden state that keep accumulating information in the hidden state. So when they got to the end of the sentence, they have a big hidden vector that captures the meaning of that sentence, then being used to produce the sentence in neural language, that's called the thought vector. You convert the language into big vectors(nothing like language), and that is what cognition is all about.  

And the 3rd view, you take these symbols, and you convert these symbols into embeddings and use multiple layers of that, so you get very rich embeddings, but the embeddings are still tied to the symbols. And got a big vector of this symbol and a big vector for that symbol, and these vectors interact to produce the symbol for the next word. And that's what understanding is, knowing how to convert the symbols into those vectors, and knowing how the vectors should interact. You are staying with the symbols, but you are interpreting with these big vectors. But it is not saying you are getting these symbols altogether, it's you turn the symbols into big vectors and you stay with the surface structure with the symbols.

We can see 3 concepts from Hinton when he explains 3 different views of language and how they relate to cognition, so we ask 

### Questions：

**1)What are symbols, vectors, embeddings?**
- symbols - words
- vectors - representation of words 
  - multiple features or dimensions of data
  - vectors are used to encode information for symbols

- embeddings - capture the semantic relationship between symbols by placing them in a high-dimensional vector space
  - specific type of vector representation where symbols are mapped into continuous vector space where similar symbols are close to each other
  - what are the relationship between symbols, vectors, embeddings, give an example
  - symbols are the discrete representation of language, vectors are the mathematical encodings for symbols, and embeddings are the specialized vectors that capture the semantic relationship between symbols

For example, considering the symbol "cat"
  - **vector**: 
Let's assume a 2D space:
"cat" could be represented as a vector pointing at [0.8,0.3]
"dog" might be at [0.7,0.4]
"fish" could be at [0.2,0.7]
"car" might be [0.9,0.1]

on this 2D plane,
"cat" and "dog" might be close to each other because they are both animals
"fish" is further away because it is a different type of animal
"car" is far from all animals, indicating it's conceptually different

easy peasy!
                
  - **embedding**: 
Let's expand to 3D for a richer embedding space:
The first dimension could represent "animal-ness"
The second dimension captures "size"
The third could reflect "domestic vs. wild."

The word "cat" might now be at (0.8, 0.5, 0.9), indicating it's a domestic animal of small size.
The word "dog" could be at (0.75, 0.6, 0.85), very close to "cat" but slightly larger.
"Fish" could be at (0.2, 0.4, 0.1), reflecting that it's not domestic, not mammalian, and lives in water. But still animals!
"Car" might be at (0.9, 0.1, 0.0), far from all the animals, highlighting it's a machine.

**2) RNN, hidden state and hidden vectors in Machine translation are mentioned in the 2nd view.**

Before we bawl ourselves out for the lack of prior knowledge like what RNN is, what is hidden state, or something like that, let's try to be curious  superficially.

- What is the Historical context in machine translation in 2014? what is the turning point of WHAT?

- in 2014, a significant breakthrough in machine translation(WHAT) occurred with the advent of using RNN, particularly with sequence-to-sequence(seq2seq) models.

Ok that sounds interesting, but i m still keeping my superficiality:

what's the big difference being made here?

Now let's dive into an example of how an RNN captures the meaning of the sentence using the hidden vector and then uses it to produce a translated sentence. Oh there you are Mr "hidden vector"!

Input sentence(English): "The cat sits on the mat."
Target sentence(French): "Le chat est assis sur le tapis."

The RNN process each word in the input sentence sequentially:

"The" → hidden state 1
"cat" → hidden state 2
"sits" → hidden state 3
"on" → hidden state 4
"the" → hidden state 5
"mat" → hidden state 6

Ohh wait, that reminds me of another English-French translation example of "the european economic area".

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Ffatgarage%2FfLNfRqjWnD.png?alt=media&token=cb249c41-7002-4e56-86d3-223d4f80c920)

Ok let us shift to this for the time being.The RNN processes the input sentence word by word: "The agreement on the European Economic Area was signed in August 1992." to French.

As each word is processed, the RNN updates its hidden state. This hidden state is a vector that captures the context and meaning of the sentence so far.

- Initial state: The hidden state starts with default values.
- "The": The hidden state begins to encode basic sentence structure.
- "agreement": The state now includes information about a formal arrangement.
- "on": Prepares for the topic of the agreement.
- "the European Economic Area": The hidden state now encodes the specific subject matter.
- "was signed": Adds information about the action taken.
- "in August 1992": Incorporates temporal information.
        - After processing the entire sentence, the final hidden state vector contains a compressed representation of the whole sentence's meaning. 

WTF does this mean?

Let's imagine our FINAL hidden state is a vector of 4 numbers for simplicity (in reality, it would be much larger[.....]). After processing the entire English sentence, it might look something like this:

[0.8, -0.3, 0.6, 0.1] - This vector doesn't directly correspond to words, but rather to abstract features that the network has learned to represent meaning. Remember our [3 dimensional features!](((w25DheDYb)))

In our example, these numbers encode various aspects of the sentence:

- 0.8 might represent the presence of a formal agreement
- 0.3 could indicate it's about an economic topic
- 0.6 might signify a past event
- 0.1 could represent European context

Likewise, RNN doesn't directly "read" this vector to produce words. Instead, it uses it as a starting point for generating the translation. Here's a simplified process:

a) The network starts with the final hidden state: [0.8, -0.3, 0.6, 0.1]

b) It uses this to predict the first word "L'accord": [0.8, -0.3, 0.6, 0.1] -> RNN -> "L'accord"

c) After outputting "L'accord", it updates the hidden state, maybe to:
[0.75, -0.2, 0.55, 0.15]

d) It uses this new state to predict "sur":
[0.75, -0.2, 0.55, 0.15] -> RNN -> "sur"

e) This process continues, with the hidden state updating after each word.

Without the hidden state, the RNN would have no context to work with. It would be guessing each word in isolation. The hidden state allows it to:

- Remember you are translating about an agreement (influencing word choice)
- Maintain the correct sentence structure in French
- Keep track of what's been translated so far to avoid repetition
- Ensure all key information (economic area, signing, date) is included
etc.

For example, when translating "European Economic Area", the hidden state's encoding of the economic context helps the network choose "zone économique" rather than just translating word-by-word right? 

I hope now we could more or less imagine what's hidden for the French cat sits on the mat.