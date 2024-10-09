# RNASeq


RNA Seq Pipeline developed from notes provided by Matthew Hinderhofer. You can see his notes in the file "ASDvSCZbulkRNAlog.html".

In order to keep the versions of the software consistent, it is going to be best practice to generate some sort of virtual environment to run the analysis. This can be done with the conda install and a fresh environment.

I am tempted to set this pipeline up within the nextflow framework, and perhaps in future analysis I will do so. For this initial run for the presentation, it might be most quickly accomplished by doing the work in a one-off file. 

Matthew used fastqc on each sample, which I will do also. I also like the idea of generating a summary report that can be used to combine the six different runs into one file. 

I expect that adapters will not have been trimmed, so we will use FastP. In previous runs I have used trimadept but it seems that Matthew prefers FastP. I do not remember why it is advantageous.

I think the fastqc and fastp trimming as well as the star alignment could all be taken care of by the nextflow pipeline. 

I want both the ATACSeq pipeline and the RNASeq pipeline to use the same reference genome files. 
I used a script to retrieve those previously, but perhaps it would be better to collect them myself? The reference files needed for both ATACSeq and RNASeq are:

MAJIQ requires a gff3 file for its annotation database. There is an improved script for requesting the latest FASTA and GTF files which can be found on the RNASeq nextflow webpage:
latest_release=$(curl -s 'http://rest.ensembl.org/info/software?content-type=application/json' | grep -o '"release":[0-9]*' | cut -d: -f2)
wget -L ftp://ftp.ensembl.org/pub/release-${latest_release}/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz
wget -L ftp://ftp.ensembl.org/pub/release-${latest_release}/gtf/homo_sapiens/Homo_sapiens.GRCh38.${latest_release}.gtf.gz

We should specify these same genome files to ATACSeq.

I will define the settings for the nextflow run through a parameter yaml/json file, using the launch tool provided through
the nextflow core website.

After peforming the above pull commands the output has generated an updated .gtf file, version 112. Therefore, the atacseq analysis should be used
again. We will perform the indexing on the RNASeq pipeline and then use these to crossreference the two runs.






