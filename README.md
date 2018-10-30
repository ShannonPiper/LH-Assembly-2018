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

```bash
minlen  = (25)  Reads shorter than this after trimming will be 
                discarded. Pairs will be discarded if both are shorter.
qtrim   = (rl)  Trim read ends to remove bases with quality below trimq.
                    Performed AFTER looking for kmers.
                    r (right end only) 
                    l (left end only)
trimq   = (6)   Regions with average quality BELOW this will be trimmed.
ktrim   = (r)   Trim to the right
k       = (23)  Kmer length used for finding contaminants. Contaminants shorter than k will not be found. 
                k must be at least 1.
mink    = (11)  Look for shorter kmers at read tips down to this length, when k-trimming or masking.
hdist   = (1)   Sets hdist for short kmers, when using mink
tpe     =       When kmer right-trimming, trim both reads to the minimum length of either
tbo     =       Trim adapters based on where paired reads overlap
```
