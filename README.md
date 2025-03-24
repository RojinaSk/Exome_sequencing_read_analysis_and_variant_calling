# Exome_sequencing_read_analysis_and_variant_calling
Working with commonly used NGS tools to process and analyze short read data from the 1000 genome project. These tools including [Bowtie 2.](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml), http://www.htslib.org/download/ , http://software.broadinstitute.org/software/igv/ . 
You will analyze genome sequencing data from IGSR/1000 Genome Project[](https://www.internationalgenome.org/data-portal/sample). using human genome reference hg38 from UCSC genome browser[..](https://hgdownload.cse.ucsc.edu/goldenpath/hg38/chromosomes/).

 

## Installation 
Bowtie 2. and SAMtools/BCFtools..
Bowtie 2. is a software suite for efficient short read alignment to a reference genome. Download Bowtie 2 binary code of v2.5.4 from sourceforge.
After installation of Bowtie 2, test the example data following the instructions. to index a reference genome with bowtie-2-build (build the BWT of the reference genome), align example reads and paired-end reads to the indexed reference genome).
SAMtools/BCFtools. are tools for processing aligned short reads and variant calling. 
##
Go back to the Bowtie 2 example. and follow the steps in “Using SAMtools/BCFtools downstream” for variant calling.
Note: Note that if you have trouble running the executables of the tools on your computer, install miniconda. and you can install and run the programs in a conda environment. Use the following links to create a conda environment., install bowtie2., install samtools., install bcftools. Note that these tools should be installed in the conda environment you created. If you have difficulties installing bowtie2 and samtools in the same conda environment, please try creating two environments and install the tools separately in each one.

## Building reference human genome
Browse human genome files of hg38 at UCSC genome browser..
Download reference chromosome 19 as follows. The chromosome files are named by chrxx.fa.gz, xx∈{1,2,….,22, X,Y}. It is very likely your laptop/desktop cannot handle the whole genome very well. Thus, you will only work on one of the chromosomes, chr19.fa.gz.
Use bowtie2-build to build the index of the chromosome and save the index file for short read alignment.
 

## Obtaining exome sequencing data from the 1000 genome project.
In this step, you will download exome sequencing data of a family trio (parent-child). The exome sequencing data are a pair of fastq files in several Gs, which are significantly smaller than whole genome sequencing data (fortunately). 
### NA19238 (mother):

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089553/SRR089553_1.fastq.gz.

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089553/SRR089553_2.fastq.gz. 

### NA19239 (father):

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089545/SRR089545_1.fastq.gz.

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089545/SRR089545_2.fastq.gz.

### NA19240 (daughter):

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089532/SRR089532_1.fastq.gz.

ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR089/SRR089532/SRR089532_2.fastq.gz.

You can use UNIX “wget” command to download the exome sequencing data:

wget  'URL/Text'

        and then decompress the gz files:

gzip -d filename.gz

 

## Note: 
if you are interested in browsing all the samples in 1000 genome data
Go to 1000 genome project data portal..
Click “search” and search with the sample ID such as “HG00554”.
Click the found sample ID under “1 matching sample”.
In the “Analysis groups”, choose “Exome”.
Download the *fastq.gz files and unzip the files.
 

## Short read alignment of the three samples.
Follow the steps in “Using SAMtools/BCFtools downstream” in Bowtie 2 example. for variant calling with Samtools and BCFtools to align the short reads and report variants from the short read alignment using the reference genome (chromosomal) you build.
Save the BCF/VCF files. Remember to use -v option with BCFtools to output potential variants only. You can either work with VCF (text) format or BCF (binary) format.
Repeat the step for your 3 BAM files.
Also generate a single VCF/BCF file using samtool to process all the three bam files together.
 

## Note:
The format of VCF files is described in detail here: https://samtools.github.io/hts-specs/VCFv4.2.pdf. and here: https://en.wikipedia.org/wiki/Variant_Call_Format ..
VCF files (or binary form bcf files) are used for further genetics analyses.
Here is an example of a vcf file. of a family trio from 1000 genome project. The file can be downloaded here..
 

## Visualization of read alignments and variants by IGV
Install IGV in your machine from http://software.broadinstitute.org/software/igv/home..
Open IGV and select “Genomes” in the top menu to choose “Load Genome From File…”
Load the chromosome file “chrxx.fa” and it will be used as the reference sequence in the visualization.
To visualize your bam file, you need to create an index file. Go to menu Tools/Run igvtools….
Select the Command to be “index” and Input File to be your bam file. Click “Run”.
Next, you need to load your bam file. Go to the menu “File/Load From File…” and select to load the bam file. Now, you can browse the short read alignment.
Next, you need to load your bcf file. Go to menu “File/Load From File…” and select to load the bcf file generated from the loaded bam file. Now, you can browse the variants.
Select a few known disease genes from OMIM. Compare the SNPs in the region/gene that you selected across the three family members. Observe the relation of the SNPs among the parents and the child. 
