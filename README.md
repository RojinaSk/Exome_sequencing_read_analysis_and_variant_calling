# Exome_sequencing_read_analysis_and_variant_calling
Working with commonly used NGS tools to process and analyze short read data from the 1000 genome project. These tools including Bowtie 2Links to an external site., SAMtools/ BCFtoolsLinks to an external site. and IGVLinks to an external site.. You will analyze genome sequencing data from IGSR/1000 Genome ProjectLinks to an external site. using human genome reference hg38 from UCSC genome browserLinks to an external site..

 

Installation of Bowtie 2Links to an external site. and SAMtools/BCFtoolsLinks to an external site..
Bowtie 2Links to an external site. is a software suite for efficient short read alignment to a reference genome. Download Bowtie 2 binary code of v2.5.4 from sourceforgeLinks to an external site.. Note that the compiled binary code is available for mac OS and linux systems. There are linux computers available from CSE labs. You can apply for a CSE account here. To use Bowtie 2 on Windows, you need to recompile the source code. It will be better to install a CygwinLinks to an external site. to run the linux binary on the window OS.
After installation of Bowtie 2, test the example data following the instructionsLinks to an external site. to index a reference genome with bowtie-2-build (build the BWT of the reference genome), align example reads and paired-end reads to the indexed reference genome).
SAMtools/BCFtoolsLinks to an external site. are tools for processing aligned short reads and variant calling. Follow the instructions for the installation. To use SAMtools/BCFtools on Windows, you still need to compile their source codes with Cygwin.
Go back to the Bowtie 2 exampleLinks to an external site. and follow the steps in “Using SAMtools/BCFtools downstream” for variant calling.
Note: Note that if you have trouble running the executables of the tools on your computer, install minicondaLinks to an external site. and you can install and run the programs in a conda environment. Use the following links to create a conda environmentLinks to an external site., install bowtie2Links to an external site., install samtoolsLinks to an external site., install bcftoolsLinks to an external site.. Note that these tools should be installed in the conda environment you created. If you have difficulties installing bowtie2 and samtools in the same conda environment, please try creating two environments and install the tools separately in each one.

Building reference human genome
Browse human genome files of hg38 at UCSC genome browserLinks to an external site..
Download reference chromosome 19 as follows. The chromosome files are named by chrxx.fa.gz, xx∈{1,2,….,22, X,Y}. It is very likely your laptop/desktop cannot handle the whole genome very well. Thus, you will only work on one of the chromosomes, chr19.fa.gz.
Use bowtie2-build to build the index of the chromosome and save the index file for short read alignment.
 

Obtaining exome sequencing data from the 1000 genome project.
In this step, you will download exome sequencing data of a family trio (parent-child). The exome sequencing data are a pair of fastq files in several Gs, which are significantly smaller than whole genome sequencing data (fortunately). 

 

NA19238 (mother):

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089553/SRR089553_1.fastq.gzLinks to an external site.

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089553/SRR089553_2.fastq.gzLinks to an external site.

 

NA19239 (father):

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089545/SRR089545_1.fastq.gzLinks to an external site.

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089545/SRR089545_2.fastq.gzLinks to an external site.

 

NA19240 (daughter):

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089532/SRR089532_1.fastq.gzLinks to an external site.

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089532/SRR089532_2.fastq.gzLinks to an external site.

You can use UNIX “wget” command to download the exome sequencing data:

wget  'URL/Text'

        and then decompress the gz files:

gzip -d filename.gz

 

Note: if you are interested in browsing all the samples in 1000 genome data

Go to 1000 genome project data portalLinks to an external site..
Click “search” and search with the sample ID such as “HG00554”.
Click the found sample ID under “1 matching sample”.
In the “Analysis groups”, choose “Exome”.
Download the *fastq.gz files and unzip the files.
 

Short read alignment of the three samples.
Follow the steps in “Using SAMtools/BCFtools downstream” in Bowtie 2 exampleLinks to an external site. for variant calling with Samtools and BCFtools to align the short reads and report variants from the short read alignment using the reference genome (chromosomal) you build.
Save the BCF/VCF files. Remember to use -v option with BCFtools to output potential variants only. You can either work with VCF (text) format or BCF (binary) format.
Repeat the step for your 3 BAM files.
Also generate a single VCF/BCF file using samtool to process all the three bam files together.
 

Note:

The format of VCF files is described in detail here: https://samtools.github.io/hts-specs/VCFv4.2.pdfLinks to an external site. and here: https://en.wikipedia.org/wiki/Variant_Call_Format Links to an external site..
VCF files (or binary form bcf files) are used for further genetics analyses.
Here is an example of a vcf fileLinks to an external site. of a family trio from 1000 genome project. The file can be downloaded hereLinks to an external site..
 

Visualization of read alignments and variants by IGVLinks to an external site..
Install IGV in your machine from http://software.broadinstitute.org/software/igv/homeLinks to an external site..
Open IGV and select “Genomes” in the top menu to choose “Load Genome From File…”
Load the chromosome file “chrxx.fa” and it will be used as the reference sequence in the visualization.
To visualize your bam file, you need to create an index file. Go to menu Tools/Run igvtools….
Select the Command to be “index” and Input File to be your bam file. Click “Run”.
Next, you need to load your bam file. Go to the menu “File/Load From File…” and select to load the bam file. Now, you can browse the short read alignment.
Next, you need to load your bcf file. Go to menu “File/Load From File…” and select to load the bcf file generated from the loaded bam file. Now, you can browse the variants.
Select a few known disease genes from OMIMLinks to an external site.. Compare the SNPs in the region/gene that you selected across the three family members. Observe the relation of the SNPs among the parents and the child. 
