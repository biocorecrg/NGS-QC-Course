.. _Sequencing_technologies-page:

***********************************
4 Quality of the Mapping
***********************************

Introduction to Mapping and tools
==================================

Once our reads are clean and with good Quality, most of the analysis requires the aligment of this reads respect a reference genome.
Depending on the origin of our sequencing data (WGS, WES, RNA-seq, Chip-seq, ...) and the downstream analysis, several alingers are available to adjust to the necessities of our analysis. 

    - BWA-MEM
    - bowtie
    - STAR
    - 

Previous aligment of the reads, a reference genome in fasta format is needed, Typical sources to look up are UCSC, Ensembl or Gencode. An indexing of the reference genome is perfomed to create a dictionary database of the redundant sequences of the genome and facilitate and accelerate the query of the reads respect this regions, thus, minimizing the the memory footprint. 

SAM format
----------



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

- **SAMStat**: Is a CLI tool that offers Statistics of SAM/BAM files of unmapped, poorly and accuretly mapped raads. 
.. seealso::
    .. _SAMStat: https://github.com/TimoLassmann/samstat


BAM format. Note, that the BAM file has to be sorted by chromosomal coordinates. Sorting can be performed with samtools sort.
