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
The **Multi30k** dataset is a collection of 31,014 parallel English-German sentences that are used for training and evaluating neural machine translation models. The sentences are split into train, validation, and test sets, and the dataset also includes a human-annotated English-German parallel corpus. In the referenced article of 2016, the Multi30K dataset is introduced as an extension of the Flickr30K dataset, which has been developed as a dataset containing images sourced from online photo-sharing websites, each of which paired with five English descriptions, which were collected from Amazon Mechanical Turk1. In particular, the Multi30K dataset presents the following characteristics:

<div align="center">
<img src="NLU Images/dataset.png" alt="Dataset Specs" width="40%">
</div>

<hr/>

## Pre-Processing
The pre-processing of the dataset can be summarized in four main steps:
1. **Token**: the "spacy modules" for English and German are loaded and two functions (German and English) are defined with the purpose of exploiting spacy library to tokenize the input sequences. Then, pytorch’s "Field" function is used to append *<SOS>* and *<EOS>* tokens and transform all of the words in the sentences to lowercase.
2. **Split**: pytorch’s "dataset split" function is used to the obtain a Training (29k instances), Validation (1k instances) and Test (1k instances) sets, furthermore it specifies German as the source language and English as the target.
3. **Vocabulary**: the vocabularies for the two languages are created from the training data enforcing that only words which appear at least twice are included, otherwise an *<UNK>* token is used.
4. **Iterator**: in the last step, an iterable object with source and target information that maps tokenized words to their index in the vocabulary is created through "BucketIterator" with a batch size of 128.

<hr/>

## Sequence to Sequence Learning with Neural Networks - Implementation
The "replica" implementation here developed exploits: 
1. **Encoder**: 2 layers LSTM with 512 cells and 256 word-embeddings.
2. **Decoder**: 4 layers LSTM with 512 cells and 256 word-embeddings.
3. **Parameters, Loss & Optimizer**: approx. 14M, Cross-Entropy, ADAM.
4. Epoch **training time** on NVIDIA Tesla K80: 30s x 15 Epochs.
5. **BLEU Score**: approx. 14.5 depending on the random seed.

<hr/>

## Neural Machine Translation by Jointly Learning to Align and Translate - Implementation
The "replica" implementation here developed exploits: 
1. **Encoder**: BiDirectional GRU with 512 units.
2. **Attention**: Weighted sum of all the intermediate context vectors through tanh activation.
3. **Decoder**: GRU with 512 hidden units.
4. **Parameters, Loss & Optimizer**: approx. 20.5M, Cross-Entropy, ADAM.
5. Epoch **training time** on NVIDIA Tesla K80: 57s x 10 Epochs.
6. **BLEU Score**: approx. 31.5 depending on the random seed.

<hr/>

## Attention Is All You Need - Implementation
The "replica" implementation here developed exploits: 
1. **Encoder**:
   1.1. Multi-Head Attention: Splitted parallel computation of the Scaled-Dot Product Attention.
   1.2. Position-wise Feed-Forward: Fully-connected feed-forward network with ReLU activation.
2. **Decoder**:
   2.1. Multi-Head Attention: Splitted parallel computation of the Scaled-Dot Product Attention.
   2.2. Position-wise Feed-Forward: Fullt-connected feed-forward network with ReLU activation. 
4. **Parameters, Loss & Optimizer**: approx. 9M, Cross-Entropy, ADAM.
5. Epoch **training time** on NVIDIA Tesla K80: 17s x 10 Epochs.
6. **BLEU Score**: approx. 35.7 depending on the random seed.

<hr/>

## Evalutation & Results
In the following table, the BLEU scores of the different implementations discussed are reported:
<div align="center">
<img src="NLU Images/results.png" alt="Dataset Specs" width="40%">
</div>
where Seq2Seq refers to <a href="NLU Papers/Sequence to Sequence Learning with Neural Networks.pdf">[1]</a> architecture, Attention to <a href="NLU Papers/Neural Machine Translation by Jointly Learning to Align and Translate.pdf">[2]</a> architecture and Transformer to <a href="NLU Papers/Attention Is All You Need.pdf">[3]</a> architecture. Whereas the Rep indicates the Replica, i.e., the "computationally-efficient" implementation presented in the notebooks associated to this repository. 

Given the nature of the BLEU metric and the diversity of the training datasets, it is difficult to provide a comparison of the performances of the replicated architectures to the ones of the original implementations. However, we can perform an analysis among the replicated architectures. Indeed, we can notice that the advancements proposed by the papers are reflected in an evolution of the performances in the replicated architectures. In particular, the increase in performance from the introduction of the "Attention" mechanism is the most significant as it leads to an increase of approximately 17 BLEU score points.

<hr/>

## Contact
Feel free to e-mail etorre@student.ethz.ch.
  
## Acknowledgements
The code in this project is inspired and adapted from several different sources that can be found in the paper associated with this repository. 
