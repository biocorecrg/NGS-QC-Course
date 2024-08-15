.. _Library_preparation-page:

*******************
1 Library preparation
*******************

Main Causes of poor quality data
========================

Quality of the sequencing data starts before sequencing and library preparation. A proper Nucleic acid extractation is necessary to gurantee  a high quantity and purity. 
Depending on the sample nature and the nucleic acid (RNA or DNA) the extraction proceess may vary,then an appropiate protocol to each situation must be chosen. 
Thus, a rigorous quality control of the nucleic acid quantification extraction must to be performed, to asses the **quantity, purity and integrity**. 
DNA Typically could be measured whether UV spectrocopy (Nanodrop) or electrophoresis (Agilent TapeStation), RNA concentration is typically measured by Qubit fluorometer (ThermoFisherScientific).

.. danger::
	**RNA is more critical**, sample degradation and contamination is more frequent. 


Library preparation 
========================

Selecting  a suitable NGS library according to the type of sample (cell type or tissue), and the downstream analysis (WES, WGS, ChipSeq, RNA-seq, ...) is essential to gurantee the quality of the data and get de desired information for our research. 
In a nutshell, library is defined as a collection of nucleic acid (RNA or DNA) fragments of a defined lenght distribution with adapters attached. 

.. image:: images/library_prep_explanation_Van_Djik_2014.jpg
  :width: 400
  :align: center

*source: https://doi.org/10.1016/j.yexcr.2014.01.008*


.. image:: images/protocol_RNA-seq_library_bias_vanDjik_etal_2014.png
  :width: 400
  :align: center

*source: https://doi.org/10.1016/j.yexcr.2014.01.008*


Main steps of a Library Preparation Kit:

- **Fragmentation**

Acid nucleic must be broken into smaller fragments. Generally physical and enzimatic fragmentation methods are popular for DNA, 
whilst chemical fragmentation is more often applied to RNA fragmentation. 

- **End-repair**

With the use of enzymes (polymerases) are repaired  the 5' and 3' overhangs produced during the fragmentation, thus creating blunt ends.
Additionally, the 5' ends are phosphorylated so they are compatible for the adapter ligation process. Some sequencing platforms (as Illumina) may also  require
the addition of a single adenine base to create a 3' overhang before adapter ligation. 

- **Adapter ligation**

short sequences of synthetic oligonucleotides (adapters) are attached to both ends of the DNA fragments. These short sequences interact with oligonucleotides on the sequencing instrument's flow cells to ensure that library is recognised and sequenced.
Adapters may also contain a barcode (short index) for multiplexing capabilities, This means that the fragments of the sample are identified when sequencing a pool of samples in the same flow cell.

- **Amplification**

It is an optional step that enbales the sequencing library to be amplified via polymerase chain reaction (PCR), which allows lower samples inputs to be used for library preparation. 
Can introduce **GC bias, duplicates or artifacts** that can hinder downstream analysis. In case a good quantity sample is preferable a PCR-free protocols to ensure high library complexity
and more readily enable specific applications (like Whole Genome Sequencing and SNP detection). 

- **Purification**

removal of unwanted products to leave only the nucleic acid fragments. Often is perfomed size selection by agarose gel or magnetic bead purification. 

- **Quality control**

Check if DNA mets the quantity and quality requirements of the sequencing instrument. Assesss the quantity and size distribution of the library. 


..note::
	RNA library preparation is more complex due to the risk of degradation and requires additional steps respect DNA:

	- Due that RNA is converted to cDNA, PCR-amplified libraries are necessary for many sequencing instruments.
	- Most of the RNA-seq applications requires the removal of the ribosomal RNA (rRNA), comprising up to 90% of the total RNA. 
    - For especific isolation of mRNA transcripts, in addition to rRNA depletion, poly(A) must be done for selecting the RNAs containing a polyadenilated tail using oligo primers.
	

Library preparation bias 
========================

Among the different library preparation steps presented earlier, several biases can be introduced during the process. 
Here are presented the main biases introduced for either DNA or RNA, in each library preparation step and possible solutions to avoid them.

..tabs::

	.. tab:: DNA library bias

	  DNA Library preparation bias 

	  *Source: http://dx.doi.org/10.1016/j.yexcr.2014.01.008*

	  Here are presented the the different steps of the DNA library preparation that have been implicated in bias introduction:

	  #. Fragmentation
	  Chromatin sonication for ChIP-seq has been shown to be non-random, with euchromatin being sheared more efficiently than heterochromatin. 
	  ..tip::
	    To solve this it has been developed the double-fragmentation ChIP-seq protocol.

	  #. Size Selection
	  Agarose gel slices by heating to 50 ºC in chaotropic salt buffer decreased the representation of AT-rich sequences.
	  ..tip:: 
	    Simple solution to this problem is to melt the gel slices in the supplied buffer at room temperature (18–22 ºC), considerably reducing GC bias.

	  #. PCR
	  Introduce bias in sample composition, due to the fact that not all fragments in the mixture are amplified with the same efficiency. 
	  GC-neutral fragments are amplified more efficiently than GC-rich or AT-rich fragments, and as a result fragments with high AT- or GC content may become underrepresented or are completely lost during library preparation
	  ..tip::
	    - Ligate adapters that contain all necessary elements for bridge amplification on Illumina flowcells are preferred, eliminating the need for PCR to add these sequences afterwards. Nevertheless, requires relatively large quantities (41 mg) of input material.
		- In the extreme case of small input amount, the single cell,multiple displacement amplification (MDA) may be the preferred amplification method. MDA is an extremely powerful amplification method, allowing microgram quantities of DNA to be obtained from femtograms of starting material. For this reason, MDA has become the method of choice for whole genome amplification (WGA) from single cells
	    - PCR additives have also been reported to reduce bias, such as betaine or tetramethylammonium chloride (TMAC) may help to further improve coverage of extremely GC-rich or AT-rich regions.
	    - The best overall performing polymerase appears to be Kapa HiFi.

	  .. seealso::
	      .. _Library_preparation_methods_for_next_generation_sequencing_Tone_down_the_bias: http://dx.doi.org/10.1016/j.yexcr.2014.01.008
	   
	         For more information see the publication Library_preparation_methods_for_next_generation_sequencing_Tone_down_the_bias_ . 


	.. tab:: RNA library bias

	  RNA Library preparation bias 
	  *Source: https://doi.org/10.1155/2021/6647597*

	  On this field are presented the main source of bias in RNA-seq, and the solutions that would be implemented to reduce it. 

	  #. **Sample Preservation and Isolation**

	  	- Degradation of RNA: Minimizing the sample processing and freezing and thawing cycles, ensures that RNA is preserved as best as possible. 
		- RNA extraction: Use high concentrations of RNA samples or avoid TRIzol extraction altogether. 
		- Alien sequence contamination:
		- Low-quality and/or low-quantity RNA samples: RNase H has been the best method for detecting low-qualityRNA and even could eﬀectively replace the standard RNA-seq method based on oligo (dT). 
		For low-quantity RNA,the SMART and NuGEN approaches had lower duplicationrates and signiﬁcantly decreased the necessary amount ofstarting material compared to other methods.

	  #. **Library Construction**

	  	- mRNA enrichment bias: enrich for polyadenylated RNA transcripts with oligo (dT) primers have shown that this method remove all non-poly (A) RNAs, such a reolication-dependant histones and lncRNAs (lacking of polyA),
		or incomplete mRNAs. Targeting rRNA as depletion method will not limit to only mRNA molecules (also is more expensive). 
		- RNA fragmentation bias: can introduce lenght biases or errors (propagated to later cycles), Studies have shown that methods that involve nonspeciﬁc restriction endonucle-ases indicate less sequence bias and have been shown to per-form similarly to the physical methods
		- Primer bias: deviation due to primer during PCR amplification could be avoid using the Illumina Genome Analyzer, which perform the reverse transcription directly on the flowcells. 
		- Adapter ligation bias: due to substrate preferencesof T4 RNA ligases, protocols that  uses a set of randomnucleotide adapters at the ligation boundary evade the capture of miRNAs. 
		- Reverse transcription bias: reverse transcriptases tend to produce false second strand cDNA throughDNA-dependent DNA polymerase
		- PCR amplification bias: main source of artifactsand base composition bias in the process of library construc-tion,
		Extremely AT/GC-Rich, fragments of GC-neutral can be ampliﬁed more thanGC-rich or AT-rich fragments. Throughthe use of custom adapters, 
		the samples without ampliﬁca-tion and ligation can be hybridized directly with the oligonu-cleotides on the ﬂowcell surface, thus avoiding the biases andduplicates of PCR. However, 
		the ampliﬁcation-free methodrequires high sample input, which limits its widely used. The mosteﬀective PCR enhancing additives currently used are betaine[50]. 
		It is an amino acid mimic that acts to balance the diﬀer-ential T m between AT and GC base pairs and has been eﬀec-tively used to improve the coverage of GC-rich templates
		presence of tetramethylammonium chloride (TMAC). Theirresult showed that the TMAC can remarkably increase theampliﬁcation of AT-rich regions in Kapa HiFi in the pres-ence. Additionally, 
		a number of additives have been reportedto play an important role in reducing the bias of PCR ampli-ﬁcation, including small amides such as formamide, smallsulfoxides such as dimethyl sulfoxide (DMSO), 
		or reducingcompounds such as β-mercaptoethanol or dithiothreitol(DTT) [50].
		PCR cyle: CR can exponentiallyamplify DNA/cDNA templates, thus leading to a signiﬁcantincrease of ampliﬁcation bias with the number of PCR cycles[51]. Therefore, 
		it is recommended that PCR be performedusing as few cycle numbers as possible to mitigation bias
		- Machine failure







