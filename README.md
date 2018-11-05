# LH-Assembly-2018

Downloaded BBmaps to QC reads (https://sourceforge.net/projects/bbmap/)

edit this for your read files, lets test the first lane/first individual/first pair of reads

# Merging F and R reads

```bash
bbmap/bbduk.sh -Xmx23g in1=CP4R1.fq  in2=CP4R2.fq out1= CP4_R1_CLEAN.fq out2= CP4_R2_CLEAN.fq minlen= 25 qtrim= rl trimq= 6 ktrim=r k= 23 mink= 11 hdist= 1 tpe tbo 
```

```bash
bbmap/bbduk.sh -Xmx23g in1=/home/groves/Desktop/LH-Assembly/Raw/Hancock-1-Neg_S2_L001_R1_001.fastq.gz in2=/home/groves/Desktop/LH-Assembly/Raw/Hancock-1-Neg_S2_L001_R2_001.fastq.gz out1=/home/groves/Desktop/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R1_001_clean.fq out2=home/groves/Desktop/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R2_001_clean.fq  minlen=25 qtrim=rl trimq=6 ktrim=r k=23 mink=11 hdist=1 tpe tbo
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
Output:
```
Input is being processed as paired
Started output streams:	0.020 seconds.
Processing time:   		142.182 seconds.

Input:                  	91079944 reads 		13347205463 bases.
QTrimmed:               	631301 reads (0.69%) 	8621221 bases (0.06%)
Trimmed by overlap:     	332081 reads (0.36%) 	15670559 bases (0.12%)
Total Removed:          	194426 reads (0.21%) 	24291780 bases (0.18%)
Result:                 	90885518 reads (99.79%) 	13322913683 bases (99.82%)

Time:                         	142.207 seconds.
Reads Processed:      91079k 	640.47k reads/sec
Bases Processed:      13347m 	93.86m bases/sec
```

## test run to match P1 P2 based on Lane number:

```bash

for o in `cat hc_negR1.list`; do for l in `cat hc_negR2.list`; do for t in `cat t2.list`; do if [[ $o == Hancock-1-Neg_S2_"$t"_R1_001.fastq.gz ]] && [[ $l == Hancock-1-Neg_S2_"$t"_R2_001.fastq.gz ]]; then echo $o $l;fi; done; done; done
```

## Apply loop to bbmap/bbduk for Hancock-1

```
for o in `cat hc_negR1.list`; do for l in `cat hc_negR2.list`; do for t in `cat t2.list`; do if [[ $o == Hancock-1-Neg_S2_"$t"_R1_001.fastq.gz ]] && [[ $l == Hancock-1-Neg_S2_"$t"_R2_001.fastq.gz ]]; then /home/groves/Desktop/bbmap/bbduk.sh -Xmx23g in1=/home/groves/Desktop/LH-Assembly/Raw/$o in2=/home/groves/Desktop/LH-Assembly/Raw/$l out1=/home/groves/Desktop/LH-Assembly/cleaned/hc-1-Neg_S2_"$t"_R1_001_clean.fq out2=home/groves/Desktop/LH-Assembly/cleaned/hc-1-Neg_S2_"$t"_R2_001_clean.fq  minlen=25 qtrim=rl trimq=6 ktrim=r k=23 mink=11 hdist=1 tpe tbo;fi; done; done; done
```
Changing paths after putting on hard drive:
Run from `/media/groves/Data/LH-Assembly/Raw`

```
for o in `cat hc_negR1.list`; do for l in `cat hc_negR2.list`; do for t in `cat t2.list`; do if [[ $o == Hancock-1-Neg_S2_"$t"_R1_001.fastq.gz ]] && [[ $l == Hancock-1-Neg_S2_"$t"_R2_001.fastq.gz ]]; then /home/groves/Desktop/bbmap/bbduk.sh -Xmx23g in1=/media/groves/Data/LH-Assembly/Raw/FASTQ-files/STEM_Capstone_Project_HiSeq-90587841/HC-5/$o in2=/media/groves/Data/LH-Assembly/Raw/FASTQ-files/STEM_Capstone_Project_HiSeq-90587841/HC-5/$l out1=/media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_"$t"_R1_001_clean.fq out2=/media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_"$t"_R2_001_clean.fq  minlen=25 qtrim=rl trimq=6 ktrim=r k=23 mink=11 hdist=1 tpe tbo;fi; done; done; done
```

Re-ran lanes 1-3 because R2 output was not put in correct place. marked as 'clean2.fq'. 1 didn't run again so re-ran individually with new path (not loop)
```
/home/groves/Desktop/bbmap/bbduk.sh -Xmx23g in1=/media/groves/Data/LH-Assembly/Raw/FASTQ-files/STEM_Capstone_Project_HiSeq-90587841/HC-5/Hancock-1-Neg_S2_L001_R1_001.fastq.gz in2=/media/groves/Data/LH-Assembly/Raw/FASTQ-files/STEM_Capstone_Project_HiSeq-90587841/HC-5/Hancock-1-Neg_S2_L001_R2_001.fastq.gz out1=/media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R1_001_clean3.fq out2=/media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R2_001_clean3.fq  minlen=25 qtrim=rl trimq=6 ktrim=r k=23 mink=11 hdist=1 tpe tbo
```


# SPAdes assembly

* Run on SPAdes genome assembler v3.11.1 (http://spades.bioinf.spbau.ru/release3.11.1/manual.html)

## Zach's script
```
./spades.py --pe1-1 /var/lib/condor/execute/slot1/dir_3785419/SPAdes-3.9.0-Linux/bin/CP4_R1_CLEAN.fq --pe1-2 /var/lib/condor/execute/slot1/dir_3785419/SPAdes-3.9.0-Linux/bin/CP4_R2_CLEAN.fq -t 32 -k 37,59,71,85,97  -o /var/lib/condor/execute/slot1/dir_3785419/SPAdes-3.9.0-Linux/bin/CP4_spades
```

## First attempt at hancock-1-neg

* used SPAdes suggestion for Illumina 2x150 reads for kmers: 21,33,55,77

* started on 11/1/2018

script:
```
spades.py --pe1-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R1_001_clean2.fq --pe1-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R2_001_clean2.fq --pe2-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L002_R1_001_clean2.fq --pe2-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L002_R2_001_clean2.fq --pe3-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L003_R1_001_clean2.fq --pe3-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L003_R2_001_clean2.fq --pe4-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L004_R1_001_clean.fq --pe4-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L004_R2_001_clean.fq --pe5-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L005_R1_001_clean.fq --pe5-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L005_R2_001_clean.fq --pe6-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L006_R1_001_clean.fq --pe6-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L006_R2_001_clean.fq --pe7-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L007_R1_001_clean.fq --pe7-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L007_R2_001_clean.fq --pe8-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L008_R1_001_clean.fq --pe8-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L008_R2_001_clean.fq  -t 32 -k 21,33,55,77  -o /media/groves/Data/LH-Assembly/spades-assembly-output/hc-1-neg-1
```

First attempt crashed with error code:
```
/usr/lib/spades/bin/hammer(_ZN13MMappedReaderC1ERKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEEbmlm+0x39d) [0x559539a04add]
/usr/lib/spades/bin/hammer(_ZN24MMappedRecordArrayReaderImEC1ERKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEEmblm+0x1b) [0x559539a2b35b]
/usr/lib/spades/bin/hammer(_ZN5utils15KMerDiskCounterI3SeqILm21EmENS_17kmer_index_traitsIS2_EEE10MergeKMersERKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEESD_j+0x65) [0x559539a2bab5]
/usr/lib/spades/bin/hammer(+0x7fee1) [0x559539a2cee1]
/usr/lib/x86_64-linux-gnu/libgomp.so.1(+0x1697e) [0x7f04cddd597e]
/lib/x86_64-linux-gnu/libpthread.so.0(+0x76db) [0x7f04cd98f6db]
/lib/x86_64-linux-gnu/libc.so.6(clone+0x3f) [0x7f04cd6b888f]
Verification of expression '(intptr_t) MappedRegion != -1L' failed in function 'MMappedReader::MMappedReader(const string&, bool, size_t, off_t, size_t)'. In file '/build/spades-9nQbPn/spades-3.11.1+dfsg/src/common/io/kmers/mmapped_reader.hpp' on line 99. Message 'mmap(2) failed. Reason: Cannot allocate memory. Error code: 12'.
Verification of expression '(intptr_t) MappedRegion != -1L' failed in function 'MMappedReader::MMappedReader(const string&, bool, size_t, off_t, size_t)'. In file '/build/spades-9nQbPn/spades-3.11.1+dfsg/src/common/io/kmers/mmapped_reader.hpp' on line 99. Message 'mmap(2) failed. Reason: Cannot allocate memory. Error code: 12'.
hammer: /build/spades-9nQbPn/spades-3.11.1+dfsg/src/common/io/kmers/mmapped_reader.hpp:99: MMappedReader::MMappedReader(const string&, bool, size_t, off_t, size_t): Assertion `(intptr_t) MappedRegion != -1L' failed.


== Error ==  system call for: "['/usr/lib/spades/bin/hammer', '/media/groves/Data/LH-Assembly/spades-assembly-output/hc-1-neg-1/corrected/configs/config.info']" finished abnormally, err code: -6

In case you have troubles running SPAdes, you can write to spades.support@cab.spbu.ru
or report an issue on our GitHub repository github.com/ablab/spades
Please provide us with params.txt and spades.log files from the output directory.
```

Lowered the number of threads and set memory limit to 30 Gb (computer total is 31.1 Gb):
```
spades.py --pe1-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R1_001_clean2.fq --pe1-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L001_R2_001_clean2.fq --pe2-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L002_R1_001_clean2.fq --pe2-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L002_R2_001_clean2.fq --pe3-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L003_R1_001_clean2.fq --pe3-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L003_R2_001_clean2.fq --pe4-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L004_R1_001_clean.fq --pe4-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L004_R2_001_clean.fq --pe5-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L005_R1_001_clean.fq --pe5-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L005_R2_001_clean.fq --pe6-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L006_R1_001_clean.fq --pe6-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L006_R2_001_clean.fq --pe7-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L007_R1_001_clean.fq --pe7-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L007_R2_001_clean.fq --pe8-1 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L008_R1_001_clean.fq --pe8-2 /media/groves/Data/LH-Assembly/cleaned/hc-1-Neg_S2_L008_R2_001_clean.fq  -t 8 -m 30 -k 21,33,55,77  -o /media/groves/Data/LH-Assembly/spades-assembly-output/hc-1-neg-1
```

Crashed again because of memory limit. Ex. of error output:
```
Traceback (most recent call last):
  File "/usr/lib/python2.7/logging/__init__.py", line 892, in emit
    self.flush()
  File "/usr/lib/python2.7/logging/__init__.py", line 852, in flush
    self.stream.flush()
IOError: [Errno 28] No space left on device
Logged from file support.py, line 272
hammer: /build/spades-9nQbPn/spades-3.11.1+dfsg/src/common/io/kmers/mmapped_reader.hpp:99: MMappedReader::MMappedReader(const string&, bool, size_t, off_t, size_t): Assertion `(intptr_t) MappedRegion != -1L' failed.
Traceback (most recent call last):
  File "/usr/lib/python2.7/logging/__init__.py", line 892, in emit
    self.flush()
  File "/usr/lib/python2.7/logging/__init__.py", line 852, in flush
    self.stream.flush()
IOError: [Errno 28] No space left on device
Logged from file support.py, line 272
```


