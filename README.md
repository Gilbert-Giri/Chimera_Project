# Chimera_Project

Documentation of all the analysis done on the Chimera Data

#Mapping Using BWA-mem2
bwa-mem2 mem -t threads Index Read_1.fq Read2.fq -o Output.sam

#Processing and Filtering Sam file

-f 2 Kepp only reads mapped in proper pair
-F 2572 Discard reads that are unmapped, Don't meet the quality standards and any supplementary alignment
-q 20 Discard Reads having MapQ below 20

samtools view -bhq 20 -f 2 -F 2572 DG3.sam > DG3.bam

samtools sort ${bam_file}.bam > ${bam_file}_sorted.bam

samtools index ${bam_file}_sorted.bam


##CNV Caller

#CNVkit 0.9.9
Python 3.7.9

cnvkit.py batch ../DG1_sorted.bam ../DG2_sorted.bam ../DG3_sorted.bam ../DG4_sorted.bam ../DG5_sorted.bam ../DG7_sorted.bam ../DG8_sorted.bam ../DG9_sorted.bam ../DG10_sorted.bam -n ../DG11_sorted.bam -m wgs -f Chimera.fa --annotate Chimera.gtf -p 16 --targets Chimera.bed --target-avg-size 10000
