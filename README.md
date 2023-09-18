<h1 align="center">
An Applied Evolutionary Analysis of Neural Machine Translation</h1>

<div align="center">
  <a href="https://www.linkedin.com/in/eliatorre/">Elia Torre</a>
  <p><a href="https://datascience.ucsd.edu/">Halıcıoğlu Data Science Institute</a>, UC San Diego, La Jolla, CA</p>
</div>

>**<p align="justify"> Abstract:** *This paper presents the research undertaken in exploring three major leaps in the context of Neural Machine Translation. In order to do so, three milestone articles in the field of Neural Machine Translation are posed under analysis, i.e., "Sequence to Sequence Learning with Neural Networks" <a href="NLU Papers/Sequence to Sequence Learning with Neural Networks.pdf">[1]</a>, "Neural Machine Translation by Jointly Learning to Align and Translate" <a href="NLU Papers/Neural Machine Translation by Jointly Learning to Align and Translate.pdf">[2]</a> and "Attention Is All You Need" <a href="NLU Papers/Attention Is All You Need.pdf">[3]</a>. The architectures described in the articles are implemented from scratch in the notebook associated with this repository and their performances are evaluated according to BLEU score on the German to English translation task based on "Multi30K" dataset.*

<hr/>

## Introduction
**Machine translation (MT)**, is a branch of computational linguistics that deals with the translation of text or speech from one natural language to another. MT is a complex task that involves many different steps, including text analysis, language processing, and generation of the target language text. In recent years, the automatic translation of text from one language to the other, has experienced a major shift. **Statistical Machine Translation**, which relies on count-based models and has dominated the field for decades, has now been substituted by **Neural Machine Translation (NMT)**. NMT is a neural network-based approach to machine translation that is used to automatically translate one natural language to another. NMT models are trained on large amounts of parallel text and can produce high-quality translations. The objective of this project is that of analysing and evaluating the results of three of the major leaps in architecture developments in the context of NMT. The architectures described in the articles are implemented from scratch in the notebook associated with this repository and their performances are evaluated according to **Perplexity metric** and **BLEU score**. 
It is necessary to note the reader that the implementations will slightly differ from the ones described in the papers on two major aspects:
  1. **Architecture**: the models implemented in the associated notebook will, in some cases, differ in the depth of the network and weight initialization process, in the first case this is due to the available computational power, while in the second case is purposely done to follow more recent implementations of the architectures (e.g., BERT) described in the articles.
  2. **Dataset**: The training and evaluation of the architectures in all of the three articles has been performed on a specific sub-sampling of the "WMT ’14" French to English dataset. On the contrary, again due to limitations in computational power and a seek for novelty, the training and evaluation of the architectures implemented in this paper has been performed on the "Multi30K" German to English dataset.

<hr/>

## Dataset
The **Multi30k** dataset is a collection of 31,014 parallel English-German sentences that are used for training and evaluating neural machine translation models. The sentences are split into train, validation, and test sets, and the dataset also includes a human-annotated English-German parallel corpus. In the referenced article of 2016, the Multi30K dataset is introduced as an extension of the Flickr30K dataset, which has been developed as a dataset containing images sourced from online photo-sharing websites, each of which paired with five English descriptions, which were collected from Amazon Mechanical Turk1.
