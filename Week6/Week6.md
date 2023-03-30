In Week 4 you will get an introduction to Oxford Nanopore seqeuncing, the output data, and sequence file formats.

Let's first remind ourselves why we are performing this experiment, what the goals are, and what the possible outcomes are.

# Using mtDNA COI Regions to Identify Species

## Introduction:

DNA sequencing has revolutionized the field of taxonomy and species identification. One of the most widely used genetic markers for species identification is the mitochondrial DNA (mtDNA) cytochrome c oxidase subunit I (COI) region. COI is a protein-coding gene located in the mitochondrial genome, which is maternally inherited and is highly conserved across most animal species. The COI gene has a high mutation rate and contains a substantial amount of variation, making it an ideal marker for species identification. In recent years, the advent of new technologies, such as Oxford Nanopore Technologies (ONT) sequencing, has enabled faster and more accurate species identification using COI data.

## Using mtDNA COI Regions to Identify Species:

The mtDNA COI region is used to identify species by comparing the nucleotide sequences of the COI gene from different individuals or populations. By comparing the sequences, researchers can identify the degree of similarity or difference between the sequences and assign them to specific species. The degree of difference between the sequences can be used to determine whether the sequences belong to the same or different species.

In addition to species identification, the COI gene can also be used to infer the evolutionary relationships between species. By constructing a phylogenetic tree based on COI sequences, researchers can determine the evolutionary history of different species and the degree of relatedness between them.

## Using ONT Data to Identify Species:

ONT sequencing is a third-generation sequencing technology that allows for the direct sequencing of DNA without the need for PCR amplification or library preparation. This technology provides longer read lengths and higher accuracy than previous sequencing technologies, making it ideal for species identification using the COI gene.

To use ONT data for species identification, researchers first isolate DNA from the target species and sequence the mtDNA COI region using ONT sequencing. The resulting reads are then filtered, trimmed, and assembled to generate a consensus sequence for each individual. The consensus sequences are compared to a reference database of COI sequences from known species using a variety of bioinformatics tools and software.

Several bioinformatics tools are available for COI sequence analysis, including BLAST, BOLD, and MEGA. These tools allow researchers to compare the COI sequences obtained from ONT data to a reference database of COI sequences and identify the closest match to the target species. In some cases, the COI sequence obtained from ONT data may not match any sequence in the reference database, indicating the presence of a new or unknown species.

## Summary of mtDNA COI:

The mtDNA COI region is a powerful genetic marker for species identification and phylogenetic analysis. The use of ONT sequencing technology has further enhanced the accuracy and speed of species identification using the COI gene. With continued advancements in sequencing technology and bioinformatics tools, the use of COI data for species identification and evolutionary analysis is expected to become increasingly widespread in the future.

Now we can finally begin our data analysis.

You will all have a different data set to analyse. Please click [here]() to obtain your dataset. Each dataset will be labelled with your full name. Go ahead and click on the link to download the data.

The method that you will use to analyse your data is called BLAST.

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

The data output from Oxford Nanopore sequencers is a string of nucleotides, e.g. `ATGCGTGGGTCTTTAG` except these strings are usually thousands or hundereds of thousands of nucleotides long. However, the data also contain two other pieces of important information. The first is a unique name for the sequence, and the second is the "quality" of the sequence - i.e. how sure we can be that the sequencer has reported the correct nucleotide. This format (sequence name, nucleotide sequence, and nucleotide accuracy) is called `fastq` format.

# Introduction to FASTQ format

The FASTQ format is a widely used file format for storing DNA sequence and quality score data. It is commonly used for output from high-throughput sequencing instruments such as Illumina, PacBio, or Oxford Nanopore.

## Why is FASTQ format useful?

FASTQ format is useful because it combines both the DNA sequence and its corresponding quality score (accuracy) information into a single file. This makes it easier to store and analyze sequencing data, as opposed to storing these two pieces of information separately, or storing solely the DNA sequence.

## How should I interpret FASTQ format?

Each entry in a FASTQ file contains four lines of information:

1. **Header line**: starts with '@' character followed by a unique identifier (i.e. "name") for the sequence read.
2. **Sequence line**: contains the actual DNA sequence read in the form of a string of A, T, C, and G nucleotides.
3. **Separator line**: starts with the '+' character and is optionally followed by the same identifier as the header line.
4. **Quality score line**: contains quality scores for each base in the sequence read. These scores represent the confidence in the accuracy of the base call, with higher scores indicating higher confidence.

Here's an example of what a single entry in a FASTQ file might look like:

```bash
@SEQ_ID
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT
+
!''((((+))%%%++)(%%%%).1*-+*''))**55CCF>>>>>>CCCCCCC65
```


In this example, the header line starts with the '@' character and the sequence line contains the DNA sequence. The separator line (which serves no real purpose) has a `+` character. Finally, the quality score line contains quality scores for each base in the sequence read.

You will note that the quality score line contains letters, numbers, and symbols, and not only numbers. I noted above that this line specifies the _accuracy_ of each base pair. You might thus expect these to be numbers, for example between `0` and `1`, which `1` indicating it's 100% certain that this is the correct nucleotide, and `0` indicating that it is 0% certain. This is actually what this line is indicating, b ut it is doing so in a slightly cryptic manner.

Rather than encoding the numbers simply as numbers, they are encoded as "compressed" numbers by using `ASCII` characters. All [`ASCII` characters](https://en.wikipedia.org/wiki/ASCII "maybe you've seen ASCII art?") are either control characters or "printable" characters, and it is this second set that you are seeing. These are associated with the numbers [33 to 128](https://theasciicode.com.ar/ "some tables"). For example, `!` the exclamation point is associated with the number 33, and upper case f `F` is associated with the number 70.

So above, the first few quality (accuracy) scores are `!` (33) `'` (39) `'` (39) `(` (40) `(` (40) `(` (40) `(` (40) `+` (43) `)` (41) `)` (41) `%` (37) ...etc.

## How should I interpret quality scores?

Wait! you say. Those aren't numbers between 0 and 1! That is true. Instead, they are numbers between 33 and 128. To transform these into quality scores (i.e. accuracy), we first subtract 33, so that the lowest character-associated number (`!` or 33) begins at `0`. _Then_ we transform these numbers into a number between `0` and `1` with a log transformation. We don't need to discuss this transformation equation here. Suffice to say that the smaller the number, the lower the accuracy. If the number is 10 (`+`) then the _accuracy_ is 90% - we can be 90% certain that the DNA sequencer has told us the correct nucleotide. If the number is 20 (`5`) then we can be 99% sure it is the correct nucleotide. If it is 30 (`?`) we can be 99.9% sure. If it is 40 (`I`) we cann be 99.99% sure. If it is 50 (`S`) then we can be 99.999% sure etc. etc.

_Usually_ with Oxford Nanopore sequence, we will be about 98% sure that the sequencer has given us the correct nucleotide. This might sound good, but frequently we will need higher accuracy, for example if we want to figure out if a genome has a specific mutation. In _our_ case though (where we want to figure out which species at mtDNA COI sequence is from), 99% accuracy will often be fine. And in many cases, Oxford Nanopore sequence will be 99.9% accurate (yay!).    

## Summary of fastq

The FASTQ format is an essential file format in bioinformatics, and understanding how to interpret it is critical for analyzing sequencing data. By combining DNA sequence and quality score information into a single file, FASTQ makes it easier to store, transmit, and analyze sequencing data, enabling researchers to gain new insights into the genetic makeup of organisms.

## How can we approach this data?

Given the enormous amount of sequence data produced by next generation sequencing methods such as Oxford Nanopore (billions of base pairs of DNA sequence), it would be impossible to analyse these DNA sequences “by hand.” For this reason, powerful computational approaches have been developed that allow billions (or even trillions) of base pairs of DNA to be analysed very quickly.

We will apply these methods to analyse our own data, with the aim of answering a simple question: what is in this DNA sample?

We note, at first, that [Computers can save you time](https://twitter.com/OdedRechavi/status/1629765548564267008?s=20 "I have no idea if this is a real scene")

# Introduction to BLAST

BLAST, which stands for Basic Local Alignment Search Tool, is a widely used bioinformatics program that compares a query sequence with a database of known sequences to find matches. BLAST is a powerful tool for identifying similarities between sequences, and it is particularly useful for identifying related sequences in large databases. 

The basic idea behind BLAST is to take a query sequence, break it down into small segments, and compare each segment to a database of sequences. The program then returns a list of matches, ranked by their degree of similarity to the query sequence.

One of the main advantages of BLAST is its speed. Because it breaks the query sequence into small segments, it can perform many comparisons in parallel, allowing it to search large databases quickly. Additionally, BLAST has a range of features and parameters that allow users to customize the search to their specific needs.

To use BLAST, you first need to obtain a query sequence that you want to compare to a database. This sequence can be in a variety of formats, including FASTA, GenBank, or EMBL. You then need to select a database to search. BLAST supports a wide range of databases, including the NCBI nucleotide and protein databases, the Swiss-Prot protein database, and many others.

Once you have your query sequence and database selected, you can use the BLAST program to search for matches. BLAST can be accessed through a web interface, such as the NCBI BLAST website, or through standalone software that can be downloaded and run on your own computer. 

To perform a search, you simply input your query sequence and select the appropriate database and search parameters. BLAST then returns a list of matches, ranked by their degree of similarity to the query sequence. From this list, you can select individual matches to examine in more detail, or you can download the entire set of matches for further analysis.

## Summary of BLAST
BLAST is a powerful bioinformatics tool that can be used to search for similarities between sequences. Its speed and flexibility make it an essential tool for many types of biological research, from genome sequencing to protein structure prediction. By breaking down sequences into small segments and comparing them to a database of known sequences, BLAST provides a quick and accurate way to identify related sequences and uncover new insights into biological systems.


<input type="text" id="name" name="name"/>