.. _Library_preparation-page:

*******************
1 Library preparation
*******************

Main Causes of poor quality data
========================

Quality of the sequencing data starts before sequencing and library preparation. A proper Nucleic acid extractation is necessary to gurantee  a high quantity and purity. 
Depending on the sample nature and the nucleic acid (RNA or DNA) the extraction proceess may vary,then an appropiate protocol to each situation must be chosen. 
Thus, a rigorous quality control of the nucleic acid quantification extraction must to be performed, to asses the **quantity, purity and integrity**. DNA Typically could be measured whether
UV spectrocopy (Nanodrop) or electrophoresis (Agilent TapeStation), RNA concentration is typically measured by Qubit fluorometer (ThermoFisherScientific).

.. note::
	**RNA is more critical**, sample contamination is very common. 


Library preparation 
========================

Selecting  a suitable NGS library according to the type of sample, and the downstream analysis is essential to gurantee the quality of the data and get de desired information for our research. 
In a nutshell, library is defined as a collection of nucleic acid (RNA or DNA) fragments of a defined lenght distribution with adapters attached. 

.. image:: images/library_prep_explanation_Van_Djik_2014.jpg
  :width: 400


Main steps of a Library Preparation Kit:

- **Fragmentation**

Acid nucleic must be broken into smaller fragments. Generally physical and enzimatic fragmentation methods are popular for DNA, 
whilst chemical fragmentation is more often applied to RNA fragmentation. 

- **End-repair**

With the use of enzymes (polymerases) are repaired  the 5' and 3' overhangs produced during the fragmentation, thus creating blunt ends.
Additionally, the 5' ends are phosphorylated so they are compatible for the adapter ligation process. Some sequencing platforms (as Illumina) may also  require
the addition os a single adenine base to create a 3' overhang before adapter ligation. 

- **Adapter ligation**

short sequences of synthetic oligonucleotides (adapters) are attached to both ends of the DNA fragments. These short sequences interact with oligonucleotides on the sequencing instrument's flow cells to ensure that library is recognised and sequenced.
Adapters may also contain a barcode (short index) for multiplexing capabilities, This means that the fragments of the sample are identified when sequencing a pool of samples in the same flow cell.

- **Amplification**

It is an optional step that enbales the sequencing library to be amplified via polymerase chain reaction (PCR), ehich allows lower samples inputs to be used for library preparation. 
Can introduce **GC bias, duplicates or artifacts** that can hinder downstream analysis. In case a good quantity sample is preferable a PCR-free protocols to ensure high library complexity
and more readily enable specific applications (like Whole Genome Sequencing and SNP detection). 

- **Purification**

removal of unwanted products to leave only the nucleic acid fragments. Often is perfomed size selection by agarose gel or magnetic bead purification. 

- **Quality control**

Check if DNA mmets the quantity and quality requirements od the sequencing instrument. Assesss the quantity and size distribution of the library. 


RNA Library preparation 
========================

Due that RNA is converted to cDNA, PCR-amplified libraries are necessary for many sequencing instruments.

RNA-seq applications requires the removal of the ribosomal RNA (rRNA), comprising up to 90% of the total RNA. rRNA can be isolated and removed by hybridisation
capture using rRNA-specific probes, then isolated from RNA sample using magnetic bead separation. 

For especific isolation of mRNA transcripts, in addition to rRNA depletion, poly(A) must be done for selecting the RNAs containing a polyadenilated tail using oligo primers.


Library preparation factors to consider
========================