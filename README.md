# LH-Assembly-2018

Downloaded BBmaps to QC reads (https://sourceforge.net/projects/bbmap/)

edit this for your read files, lets test the first lane/first individual/first pair of reads

# Merging F and R reads

```bash
bbmap/bbduk.sh -Xmx23g in1=CP4R1.fq  in2=CP4R2.fq out1= CP4_R1_CLEAN.fq out2= CP4_R2_CLEAN.fq minlen= 25 qtrim= rl trimq= 6 ktrim=r k= 23 mink= 11 hdist= 1 tpe tbo 
```

```bash
bbmap/bbduk.sh -Xmx23g in1=/home/groves/Desktop/LH-Assembly/Raw/Hancock-1-Neg_S2_L001_R1_001.fastq.gz in2=/home/groves/Desktop/LH-Assembly/Raw/Hancock-1-Neg_S2_L001_R2_001.fastq.gz out1=/home/groves/Desktop/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R1_001_clean.fq out2=home/groves/Desktop/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R2_001_clean.fq  minlen= 25 qtrim= rl trimq= 6 ktrim=r k= 23 mink= 11 hdist= 1 tpe tbo
```
