## Week 6


## Identifying organisms with BLAST

One way to identify the organism that a DNA sequence comes from is by using a program called Basic Local Alignment Sequence Tool (BLAST). This program can search through a very large database of DNA sequences (hundreds of billions of DNA sequences from organisms across the tree of life) to find which sequence in the database most closely matches the DNA sequence that you are interested in.

First, you will learn to differentiate fastQ format files from fastA format files, and the difference between the two. We will then use BLAST to find DNA sequences that match your own sequences by querying the world’s largest database of DNA sequences, the National Center for Biotechonology Information (NCBI) in the United States. We will then interactively view the output from a high-throughput computational analysis of the DNA sequences. Finally, we will screen your sequences to understand what other closely related organisms are present in the database.

[Computers can save you time](https://twitter.com/OdedRechavi/status/1629765548564267008?s=20 "I have no idea if this is a real scene")

## Materials
Computer
Some software tools
Typing skillz


## Methods
Go to the Stream website and download the three files sequence-files, 203210-sequencing, and fastq-files, and carefully note where you save them. The Downloads directory is a good place. Unzip them all.
Open the folder file fastq-files, select a file (perhaps the barcode that you were given for your sample), and open it using a TEXT EDITOR (e.g. Notepad). This file contains up to 1000 sequences from each of your “unknown” samples. Note the format of the file. It should look something like the following:
