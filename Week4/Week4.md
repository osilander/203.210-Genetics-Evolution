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

Wait! you say. Those aren't numbers between 0 and 1! That is true. Instead, they are numbers between 33 and 128. To transform these into quality scores (i.e. accuracy), we first subtract 33, so that the lowest character-associated number (`!` or 33) begins at `0`. _Then_ we transform these numbers into a number between `0` and `1` with a log transformation. We don't need to discuss this transformation equation here. Suffice to say that the smaller the number, the lower the accuracy. If the number is 10 (`+`) then the _accuracy_ is 90% - we can be 90% certain that the DNA sequencer has told us the correct nucleotide. If the number is 20 (`5`) then we can be 99% sure it is the correct nucleotide. If it is 30 (`?`) we can be 99.9% sure. If it is 40 (`I`) we cann be 99.99% sure. If it is 50 (`S`) then we can be 99.999% sure etc. etc.

_Usually_ with Oxford Nanopore sequence, we will be about 98% sure that the sequencer has given us the correct nucleotide. This might sound good, but frequently we will need higher accuracy, for example if we want to figure out if a genome has a specific mutation. In _our_ case though (where we want to figure out which species at mtDNA COI sequence is from), 99% accuracy will often be fine. And in many cases, Oxford Nanopore sequence will be 99.9% accurate (yay!).    

## Conclusion

The FASTQ format is an essential file format in bioinformatics, and understanding how to interpret it is critical for analyzing sequencing data. By combining DNA sequence and quality score information into a single file, FASTQ makes it easier to store, transmit, and analyze sequencing data, enabling researchers to gain new insights into the genetic makeup of organisms.


<input type="text" id="name" name="name"/>