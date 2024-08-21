.. _Sequencing_technologies-page:

***********************************
3 Quality Control and Preprocessing
***********************************

Illumina
===========================

Quality Control
---------------

Quality control of the reads contained in the fastq files needs to be check, in order to determine 
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

The html report generated for each file its divided in the following sections:

    #. **Basic Statistics**: display the information related with the file, number and leght of the sequences, and overall %GC. 
    #. **Per base sequence quality**: shows how the quality score (y axis) varys throughout the sequence reads (x axis). For each position a BoxWhisker is displayed, the red line represents the median and the blue the mean. Commonly the quality score tend to decrease at the end of the reads, because the polymerase tends to make more mistakes as the read progresses.
        is the median os any base is less than 25 a warning will arise.
    #. **Per sequence quality score**: 
    #. Per base sequence content
    #. Per base GC content
    #. Per sequence GC content 
    #. Per Base N content 
    #. Sequence Lenght Distribution
    #. Duplicate Sequences 
    #. Overrepresented sequences 
    #. Overrepresented kmers    