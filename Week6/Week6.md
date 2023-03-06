## Week 6

Given the enormous amount of sequence data produced by next generation sequencing methods such as Oxford Nanopore (billions of base pairs of DNA sequence), it would be impossible to analyse these DNA sequences “by hand.” For this reason, powerful computational approaches have been developed that allow billions (or even trillions) of base pairs of DNA to be analysed very quickly.

We will apply these methods to analyse our own data, with the aim of answering a simple question: what is in this DNA sample?

## Identifying organisms with BLAST

One way to identify the organism that a DNA sequence comes from is by using a program called Basic Local Alignment Sequence Tool (BLAST). This program can search through a very large database of DNA sequences (hundreds of billions of DNA sequences from organisms across the tree of life) to find which sequence in the database most closely matches the DNA sequence that you are interested in.

First, you will learn to differentiate fastQ format files from fastA format files, and the difference between the two. We will then use BLAST to find DNA sequences that match your own sequences by querying the world’s largest database of DNA sequences, the National Center for Biotechonology Information (NCBI) in the United States. We will then interactively view the output from a high-throughput computational analysis of the DNA sequences. Finally, we will screen your sequences to understand what other closely related organisms are present in the database.

https://twitter.com/OdedRechavi/status/1629765548564267008?s=20