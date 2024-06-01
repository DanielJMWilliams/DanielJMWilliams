---
title: Exploring Polysemantic Universaility of Embeddings
date: 2024-05-31 17:40:21 +0100
description: Results of my experiments exploring the nature of polysemantic relationships in embeddings models.
categories: [AI Safety, Mechanistic Interpretability]
tags: [ai safety, mechanistic interpretability, polysemantic universality, embeddings]     # TAG names should always be lowercase
author: daniel
---

# Introduction

As part of the AI Safety Fundamentals course, I have undertaken a short project to contribute to AI Safety. I found mechanistic interpretability to be the most interesting topic during the course and was inspired by the papers: Toy models of Superposition and Towards monosemanticity.

Polysemanticity is the phenomenon where neurons within an artificial neural network respond to multiple distinct features. The examples in Toy models of Super position include a cat head and a car body ( #TODO check this).
Polysemanticity makes interpretability research difficult. It is hard to confidently determine what a neuron responds to when it responds to a range of things. E.g. if it is responsible for generating text about cats and generating deceptive text. However if it is the case that polysemantic relationships are universal, then once they have been found and understood in one model, we can use that knowledge to understand other models too.

It was my intuition that dissimilar features would be grouped similarly across models where the dimensions are being greatly reduced.
I wanted to test this intuition and see if it was true.

I chose to explore this using embeddings models as they compress a highly dimensional space into a relatively small one. 
tests:
- training minimal embeddings models and observing how polysemantic relationships occur as dimensions decrease.
- calculating the vectors for the difference between intuitively dissimilar words and seeing if the words similar to this vector are similar across models.
- finding the words most similar to a particular dimension and comparing this across models.

results:
- models seem not to have repeat words occurring at the max of individual dimensions
- different models seem not to learn similar word in individual dimensions


limitations / problems with our approach
- we only looked at a small number of models
- did not preprocess corpus before training
- google_news does have some very odd features e.g. names

 future work
- how does brown_30 compare to brown_29?



# Methodology

Link Jupyter notebook, code snippets and results screenshots.

# Results




# Limitations

# Future Work


# References and Related


