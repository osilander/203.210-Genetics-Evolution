In Week 4 you will get an introduction to Oxford Nanopore seqeuncing, the output data, and sequence file formats.

# Introduction to Oxford Nanopore Sequencing

Oxford Nanopore sequencing is a next generation sequencing technology that allows for rapid DNA sequencing using a handheld device. It was developed by Oxford Nanopore Technologies, a UK-based company that was founded in 2005.

## How it Works

The basic principle behind Oxford Nanopore sequencing is that a single strand of DNA is passed through a tiny nanopore in a membrane. A current is run through this membrane, and  tiny changes in electrical signals produced by the movement of the DNA through the pore are recorded. The pore essentially acts as a molecular sensor of DNA charge.

As this DNA molecule passes through the pore, the different bases (A, T, C, and G (or methylated bases, or even U in the case of RNA)) produce unique electrical signals that can be used to reconstruct the original sequence of the DNA.

The way that these signals are decoded into the order of base pairs depends on powerful computational methods. Currently, these are machine learning methods based on recurrent neural networks with [long short term memories](https://en.wikipedia.org/wiki/Long_short-term_memory "LSTM").

## Advantages

One of the main advantages of Oxford Nanopore sequencing is its portability. The handheld device can be used outside of the lab, making it ideal for applications such as disease surveillance and environmental monitoring.

Another advantage is the long read lengths that can be achieved. Traditional sequencing methods (e.g. [Sanger](https://en.wikipedia.org/wiki/Sanger_sequencing "The OG") or [Illumina](https://en.wikipedia.org/wiki/Illumina_dye_sequencing "The OG NGS")) typically generate short reads of a few hundred bases, whereas Oxford Nanopore sequencing can generate reads that are tens of thousands of bases long or even millions of base pairs long. This allows for more complete genome assembly and better detection of structural variants (changes in the structure of chromosomes, such as duplications of chromosomal regions or inversions of specific regions).

## Applications

Oxford Nanopore sequencing has a wide range of applications, including:

- Whole genome sequencing
- Metagenomics
- Transcriptomics
- Epigenetics
- Pathogen detection (e.g. COVID-19)
- Forensics

<input type="text" id="name" name="name"/>