# Application of long read sequencing to determine expressed antigen diversity in *Trypanosoma brucei* infections.

Siddharth Jayaraman<sup>1*</sup>, Claire Harris<sup>2</sup>, Edith Paxton<sup>1</sup>, Anne-Marie Donachie<sup>3</sup>, Heli Vaikkinen<sup>3</sup>, Richard McCulloch<sup>3</sup>, James P. J. Hall<sup>4</sup>, John Kenny<sup>5</sup>, Luca Lenzi<sup>5</sup>, Christiane Hertz-Fowler<sup>5</sup>, Christina Cobbold<sup>2,6</sup>, Richard Reeve<sup>2</sup>, Tom Michoel<sup>1</sup> and Liam J. Morrison<sup>1*</sup>

1. Roslin Institute, University of Edinburgh, Easter Bush, Midlothian, EH25 9RG, United Kingdom.

2. Boyd Orr Centre for Population and Ecosystem Health, Institute of Biodiversity, Animal Health and Comparative Medicine, College of Medical and Life Sciences, University of Glasgow, 120 University Place, Glasgow G12 8TA, United Kingdom.

3. Wellcome Centre for Molecular Parasitology, Institute of Infection, Immunity and Inflammation, College of Medical and Life Sciences, University of Glasgow, 120 University Place, Glasgow G12 8TA, United Kingdom.

4. Department of Biology, Wentworth Way, University of York, York YO10 5DD, United Kingdom.

5. Centre for Genomic Research, Institute of Integrative Biology, University of Liverpool, Crown Street, Liverpool L69 7ZB, United Kingdom.

6. School of Mathematics and Statistics, University of Glasgow, University Place, Glasgow, G12 8QS, United Kingdom.

[*Liam.Morrison@roslin.ed.ac.uk](mailto:*Liam.Morrison@roslin.ed.ac.uk)
[*Siddharth.Jayaraman@roslin.ed.ac.uk](mailto:*Siddharth.Jayaraman@roslin.ed.ac.uk)


## Abstract
Antigenic variation is employed by many pathogens to evade the host immune response, and  *Trypanosoma brucei* has evolved a complex system to achieve this phenotype, involving sequential use of variant surface glycoprotein (VSG) genes encoded from a large repertoire of ~2,000 genes. *T. brucei* express multiple, sometimes closely related, VSGs in a population at any one time, and the ability to resolve and analyse this diversity has been limited. We applied long read sequencing (PacBio) to VSG amplicons generated from blood extracted from batches of mice sacrificed at time points (days 3, 6, 10 and 12) post-infection with T. brucei TREU927. The data showed that long read sequencing is reliable for resolving variant differences between VSGs, and demonstrated that there is significant expressed diversity (449 VSGs detected across 20 mice) and across the timeframe of study there was a clear semi-reproducible pattern of expressed diversity (median of 27 VSGs per sample at day 3 post infection (p.i.), 82 VSGs at day 6 p.i., 187 VSGs at day 10 p.i. and 132 VSGs by day 12 p.i.). There was also consistent detection of one VSG dominating expression across replicates at days 3 and 6, and emergence of a second dominant VSG across replicates by day 12. The innovative application of ecological diversity analysis to VSG reads enabled characterisation of  hierarchical VSG expression in the dataset, and resulted in a novel method for analysing such patterns of variation.  Additionally, the long read approach allowed detection of mosaic VSG expression from very few reads – the earliest in infection that such events have been detected. Therefore, our results indicate that long read analysis is a reliable tool for resolving diverse gene expression profiles, and provides novel insights into the complexity and nature of VSG expression in trypanosomes, revealing significantly higher diversity than previously shown and the ability to identify mosaic gene formation early during the infection process.

## Pacbio Sequencing analysis

### Raw data processing

1. Pacbio raw data was initially processed using the Pacbio SMRT Analysis - Read of Insert protocol (v2.3), to convert the data into a fasta file using the following parameter selections: minimum 1 full pass, minimum predicted accuracy of 90%. <br/><br/>**SMRT Analysis v2.3**
<br/>[SMRT Analysis v2.3 Release Notes](https://www.pacb.com/wp-content/uploads/SMRT-Analysis-Release-Notes-v2-3-0-p5.pdf)<br/>[SMRT Analysis v2.3 Installation guide](https://www.pacb.com/wp-content/uploads/SMRT-Analysis-Software-Installation-v2-3-0.pdf)
<br/><br/>**Raw Data**<br/>GEO Accession [GSE114843]( https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE114843)

2. Based on the read length distribution, a range of 1400-2000bp was used to filter the sequenced reads for downstream VSG analysis.
<br/><br/> Processed, filtered and sample annotated sequenced reads in fasta format used in downstream analysis (header format eg. *balbc_10_1/18/ccs5* [**Mouse_Day_Replicate**/**ZMW**/**number_of_passes**]): [PacBio_VSG_filtered_reads.fasta.gz](https://datasync.ed.ac.uk/index.php/s/kj4tpmkIdwFPBBE) 
<br/>**Data access password:** longreadvsgdata2019


#### VSG read analysis

1. We generated a local database of TREU927 VSGs, by downloading all transcripts annotated as ‘VSG’ from the most recent version of the TREU927 genome (v26) on  [www.tritrypdb.org](http://www.tritrypdb.org/).
<br/><br/> **VSG Database** used in this study: [TREU927-v26_VSGTranscripts.zip](https://datasync.ed.ac.uk/index.php/s/KoIXV2lgH95KhvA)
<br/>**Data access password:** longreadvsgdata2019

2. Reads were blasted (BLASTn) against the reference VSG database to identify the donor gene.
A minimum alignment coverage of 60% or above to the sequence read was used to identify the dominant donor transcript, and to generate a variant distribution chart for each sequenced sample. <br/><br/>`blastn  -query PacBio_VSG_filtered_reads.fasta -db TREU927-v26_VSGTranscripts.fasta -out PacBio_VSG_Filtered_Reads_VSGv27DB_blastn_outfmt6.txt  -max_target_seqs 1 -outfmt '6 qseqid sseqid qseq sseq qlen slen qstart qend sstart send evalue bitscore score length nident mismatch positive gapopen gaps ppos'
` 
<br/><br/>The raw blast result used in this study: [PacBio_VSG_Filtered_Reads_VSGv27DB_blastn_outfmt6.txt.zip](https://datasync.ed.ac.uk/index.php/s/wSDZV1LNAMoRVbr)
<br/>**Data access password:** longreadvsgdata2019
<br/><br/>The data representing the VSG transcript counts for the aligned reads used in figure 3 is presented in the tab-seperated text file : [PacBio_VSG_transcript_count_20Sample.txt](https://datasync.ed.ac.uk/index.php/s/27PLwwghMaY3C8R)
<br/>**Data access password:** longreadvsgdata2019

3. We also locally aligned the sequenced VSG reads to a blast database of 515 previously identified cloned reads from  *T. brucei* TREU927 infections.<br/><br/>`blastn  -query PacBio_VSG_filtered_reads.fasta -db Hall_Marcello_Barry_VSGs.fasta -out PacBio_VSG_Filtered_Reads_VSGClones_blastn_outfmt6.txt  -outfmt '6 qseqid sseqid qseq sseq qlen slen qstart qend sstart send evalue bitscore score length nident mismatch positive gapopen gaps ppos'
` 
<br/><br/>**Known VSG clone database**: [Hall_Marcello_Barry_VSGs.zip](https://datasync.ed.ac.uk/index.php/s/ZuUwIA3efFuiMqa)

<br/>**Blast alignment result**: [PacBio_VSG_Filtered_Reads_VSGClones_blastn_outfmt6.txt.zip](https://datasync.ed.ac.uk/index.php/s/oBsKqmmzjpVFB83)
<br/>**Data access password:** longreadvsgdata2019

4. Open reading frames were identified using ‘getorf’ in EMBOSS (v6.6.0.0), using the following parameters: minimum size 1200 nucleotides, all 3 reading frames and only forward strand.<br/><br/>`getorf -sequence PacBio_VSG_filtered_reads.fasta -outseq PacBio_VSG_filtered_reads_ORFs.fasta -minsize 1200 -find 3 -reverse N` 
<br/><br/> ORF dataset: [PacBio_VSG_filtered_reads_ORFs.fasta](https://datasync.ed.ac.uk/index.php/s/4ZAKW13l43iKYpM)
<br/>**Data access password:** longreadvsgdata2019


#### Mosaic gene identification

 1. We reasoned that putative mosaic genes could be identified as PacBio sequences with partial, non-overlapping alignments to multiple VSG genes. We therefore undertook full pairwise alignment using local blast of the 296,937 reads that align to VSGs at a 60% identity threshold post size-selection filtering (see above) against the curated VSG database described above. This resulted in all possible donors and their alignment regions for any specific read being identified.<br/><br/>`blastn  -query PacBio_VSG_filtered_reads.fasta -db TREU927-v26_VSGTranscripts.fasta -out PacBio_VSG_Filtered_Reads_VSGv27_MOSAIC_blasnt.txt  -outfmt '6 qseqid sseqid qseq sseq qlen slen qstart qend sstart send evalue bitscore score length nident mismatch positive gapopen gaps ppos'
` 
<br/><br/>The blast result used to identify the mosaic presented in paper: [PacBio_VSG_Filtered_Reads_VSGv27_MOSAIC_blasnt.txt.zip](https://datasync.ed.ac.uk/index.php/s/laYyatZ0pBnfSVn)
<br/>**Data access password:** longreadvsgdata2019
