.. _Sequencing_technologies-page:

***********************************
4 Quality of the Mapping
***********************************

Once our reads are clean and with good Quality, most of the analysis requires the aligment of this reads respect a reference genome.
Depending on the origin of our sequencing data (WGS, WES, RNA-seq, Chip-seq, ...) and the downstream analysis, several alingers are available to adjust to the necessities of our analysis. 

Previous aligment of the reads, For DNA-seq is required a reference genome in fasta format is needed, Typical sources to look up are UCSC, Ensembl or Gencode.
And for RNA-Seq aligment, a reference transcriptome is needed, typically a fasta file with the transcript sequences of the organism of interest.

If references are not available, a de novo assembly of the reads can be performed to generate a reference genome or transcriptome. 

**Basic aligment**: Based on the Smith-Waterman algorithm, needs the creation of an index of the reference genome, used as a dictionary to query the reads and accelerate the search reducing the memory footprint. 
The following tools can be used either for WGS or WES, but the have some differences:

    - BWA-MEM: by default perform local aligment, high accuracy and efficiency in align reads to the entire genome. Because its very efficent for finding aligment with gaps is commonly used for variant detection `<https://bio-bwa.sourceforge.net/bwa.shtml>`_.

    - Bowtie2: by default perform global aligment, is faster than BWA but less sensitive. Recommended for large-scale sequencing samples, and for ChiP-seq due to its speed to align shorter reads and identified enriched regions (peak detection) `<https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml>`_.

**RNA-seq splice-aware aligner**: Specialized in the mapping of RNA-seq reads, that can be spliced and map to different exons of the same gene:

    - STAR: Most popular aligner for RNA-seq data, very effcient and accurate identifying splice junctions `<https://github.com/alexdobin/STAR>`_.

    - TopHat2: first aligners designed for RNA-seq data, but now is deprecated and replaced by STAR `<https://ccb.jhu.edu/software/tophat/index.shtml>`_.

    - HISAT2: built on the Bowtie2 aligment algorithm, but optimized for RNA-seq data `<https://daehwankimlab.github.io/hisat2/>`_.

**Pseudo-Aligner - Quasi-mapping**: very fast, map to transciptome and does quantitation. Can't find novel transcripts. When the goal is quantify gene expression levels, this is the best option:

    - Kallisto: use pseudo-aligment approach, efficiently determines the compatibility of the transcript without full sequence aligment, very fast and memory-efficient, better option for large-scale projects `<https://github.com/pachterlab/kallisto>`_.

    - Salmon: use quasi-mapping approach, similar to pseudo-aligment but includes information about the location of the read within the transcript, and perform bias correction steps. Slower than kallisto but more accurate quantifications. Better option for complex transcriptomes  `<https://combine-lab.github.io/salmon/getting_started/>`_.


SAM format
----------

The output of the aligment is a SAM file.
Here is presented an overview of the structure of the SAM (Sequence Aligment/Map) format, which is a tab-delimited text file, divided in two sections: the header (optional) and the aligment records.

    - Header lines start with @
    - Aligment records start with a read name and mandatory contain 11 fields.


.. seealso::
    .. _SAM format: https://samtools.github.io/hts-specs/SAMv1.pdf
    Check the SAM format_ specification for a detailed explanation about the structure of the SAM and BAM file.



BAM QC 
===========================

Even if the Quality control of the reas was correct, there are some problems  with the reads that are visualized after mapping (Low coverage, homopolymers biases, experimental artifacts, etc)
Most of the tools to asses Mapping Quality relies on the values of MAPQ, which is a Phred-scaled probability that the alignment is wrong.


.. math::
    MAPQ = -10*log10(P)

Where P is the probability that the alignment is wrong.

For example, for a MAPQ value of 20 the probability that the alignment is wrong is 1 in 100 (0.01), 

.. math::
    MAPQ = -10*log10(0.01) = 20

The confidence of the alignment is higher when the MAPQ value is higher.

Main Tools to asses the quality of the mapping are:

.. note::
    The value og the MAPQ is Algorithm-specific, so the values of MAPQ are not comparable between different aligners.

**SAMStat**
------------

Is a CLI tool that offers Statistics of SAM/BAM files of unmapped, poorly and accuretly mapped raads. 

.. seealso::
    .. _SAMStat: https://github.com/TimoLassmann/samstat
    Check the SAMStat_ GitHub repository for more information about usage. 


BAM format. Note, that the BAM file has to be sorted by chromosomal coordinates. Sorting can be performed with samtools sort.

**Qualimap**
------------

Qualimap is a platform-independent application written in Java and R that provides both a GUI and a command-line interface to facilitate the quality control of alignment sequencing data. 
It can be used to assess the quality of the alignment of reads to a reference genome, the coverage of the genome, the distribution of reads across the genome and helps to detect biases.
Qualimap generates a series of plots and tables that can be used to evaluate the quality of the alignment and identify potential problems with the data. 
It can be used to assess the quality of alignments generated by a variety of alignment tools, including BWA, Bowtie, and STAR.

Requires a sorted BAM file as input and the origin data supported are WGS, WES, RNA-seq and Chip-seq. 

.. note::
    .. _Samtools: https://www.htslib.org/doc/samtools-sort.html
    BAM file sorting by chromosomal coordinates can be performed with samtools sort Samtools_.


Depending on the origin of our data, exist different modes for quality asses. 

    - BamQC: provides evaluation of the mapping quality of the reads. And if an annotation file is provided (Typically bed file of the coverage refgions by the Library prepa kit), it can also provide information about the coverage of the genes.

    - Rna-seq: specific for whole transciptome sequencing data. Can be use as a complementary tool with BamQC. 

    - Multi-sample BamQC: When working with multiple samples (i.e. sequencing data in cancer) and theese belongs to an specific group.
    This allow to detect if all the samples in an specific group pass the quality control.

    - Counts QC: When working with RNA-seq data, this mode allows to asses the differential expresion betweeen two or more experimental conditions. 

.. seealso::
    .. _Qualimap: http://qualimap.bioinfo.cipf.es/
    Check the Qualimap_ website for more information about usage.


**Picard Tools - RNAseqMetrics**

RNAseqMetrics is a tool from Picard Tools that provides a comprehensive set of metrics for RNA-seq data. 
It can be used to assess the quality of the alignment of reads to a reference genome, the coverage of the genome, 
the distribution of reads across the genome and helps to detect biases.

.. seealso::
    .. _Picard Tools: https://gatk.broadinstitute.org/hc/en-us/articles/360037057492-CollectRnaSeqMetrics-Picard
    Check the Picard Tools_ website for more information about usage.

