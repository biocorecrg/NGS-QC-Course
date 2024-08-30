.. _Sequencing_technologies-page:

***********************************
3 Quality Control and Preprocessing
***********************************

Illumina
===========================

Quality Control
---------------

After sequencing, Quality control of the reads contained in the fastq files needs to be check, in order to determine 
if the reads could be used for further analysis. the main tools used for QC in Illumina reads are FASTQC and FASTQ-Screen.

FASTQC
~~~~~~

Is a tool developed to check failures in the reads produced either by the sequencing machine or during library preparation.
the extensions supported are:

    - FASTQ
    - Casava FASTQ files
    - Colorspace fastq
    - Gzip compressed FASTQ (.fastq.gz)
    - SAM 
    - BAM 
    - SAM/BAM Mapped only (normally used for colorspace data) 

The html report generated for each file its divided in the following modules:

    #1. **Basic Statistics**: display the information related with the file, number and leght of the sequences, and overall %GC. 
    #2. **Per base sequence quality**: shows how the quality score (y axis) varys throughout the sequence reads (x axis). For each position a BoxWhisker is displayed, the red line represents the median and the blue the mean. Commonly the quality score tend to decrease at the end of the reads, because the polymerase tends to make more mistakes as the read progresses.
        is the median os any base is less than 25 a warning will arise.
    #3. **Per tile sequence quality**: shows the quality score distribution for each tile in the flowcell.
    #4. **Per sequence quality score**: shows the distribution of the quality scores for all the reads in the file. If a huge amount of reads subset have a poor average quality this could indicate a systematic problem. 
    #5. **Per base sequence content**: proportion of each base position for the four nucleotides. A strong bias in the nucleotide composition could indicate a problem in the library preparation.
    #6. **Per sequence GC content**:  GC content distribution for all the reads in the file, and compared to a modelled normal distribution of human GC content.

.. danger::
        If the GC content is not close to the normal distribution, this could indicate a contamination or a problem in the library preparation. 
        Also, depending on the organism the GC content could vary, so it is important to know the GC content of the organism of interest (so avoid comparison with reference curve).

    #7. **Per Base N content**: If the sequencer is unable to determine the base in a position, it will be represented as an 'N'. This section shows the distribution of Ns in the reads.
    #8. **Sequence Lenght Distribution**: distribution of fragment sizes, for delimited size lenght (number of cycles) a peak only at one size is observed. 
    #9. **Duplicate Sequences**: shows the number of duplicated sequences in the file. a high level of duplication could indicate a enrichment bias (i.e. PCR amplification). Low level of duplication may indicate a very high level of coverage of the target sequence. 
    #10. **Overrepresented sequences**: show in a single sequence is very overrepresented in the file. This could indicate a contamination or a problem in the library preparation.
    #11. **Adapter content **: shows the presence of adapter sequences in the reads. If  there is presence of adapters, the reads should be trimmed before further analysis. 

.. seealso:: 
    .. _FASTQC: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/
    
    For more information about FASTQC modules interpretation visit the FASTQC_ website.


FASTQ-Screen
~~~~~~~~~~~~

Is a tool that checks if the reads are generated from the genome of the organism of interest, 
quantifying the proportion of reads that map to a reference genomes and also to a set of contaminants.  
In human sequencing data the standard reference genomes to check are:

    - Human
    - Mouse
    - Rat 
    - Droshophila
    - Worm 
    - Yeast
    - Arabidopsis
    - E.coli
    - PhiX: is a control used by Illumina to check the quality of the sequencing run (if the library is under or overloaded) 
    - rRNA: in RNA-seq  is a good control of rRNA depletion during library preparation has not beeen amplified. 
    - Mitochondrial: in single nucleus RNA-seq is a good control of the nuclear isolation during the DNA extraction. 
    - Lambda
    - Vectors: to check that vectors used during library preprartion 
    - Adapters 

Example of a FASTQ-Screen report: 


When working with several samples and reports theese could be aggregate in a unique report using "MULTIQC"" (https://multiqc.info/)

Pre-processing
---------------

After the quality control, in case adapter content or low quality bases are detected,
the reads need to be pre-processed in order to get rid of them and improve quality of the reads for further analysis.

Typical tools used for pre-processing are: 

    - Trimmomatic
    - Cutadapt, only remove the adapaters (it needs to be used in combination with sickle), requires the adapter sequence to be known.
    - Sickle, remove low quality tail bases. 
    - fastp

fastp source: *https://academic.oup.com/bioinformatics/article/34/17/i884/5093234*

Fastp performs in all one the following corrections:

- Adapter removal: in paired-end data, fastp seeks the overlap of each pair and considers the bases that fall out of the
 overlapped regions as adapter contents. Not need to specify the adapter sequence.
- Base correction:  for good quality overlapped sequences, quality differences are corrected if one of the bases has a higher score. 
  Tipically base quality decrease towards the 3' end of the read, poor quality tails are removed to leave only-high quality reads for aligment.
  sliding window method to drop the low-quality bases of each read’s head and tail. The window can slide from either 5′ to 3′ or from 3′ to 5′, and the average quality score within the window is evaluated. 
  If the average quality is lower than a given threshold, then the bases in the window will be marked as discarded
- Reads which are below a certain length are also removed.
- Poly-G tails are recognised and removed (Sequencing error in the end of the read produced by some artifacts, such as Illumina and Novaseq, for the use of two colors to detect the four bases)

After preprocessing our reads, its important to check again the Quality. Fastp generates both htm and json report for asses the quality of our reads.
The json reports could be aggregated with MULTIQC.