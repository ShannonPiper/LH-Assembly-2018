# BWA preprocessing
Index completed assembly for BWA (example with hc1neg)

`bwa index /mnt/md0/piper/LH-Assembly/redundans/hc1neg_redundans/hc1negred/contigs.reduced.fa`

# Picard preprocessing
`java -jar /mnt/md0/piper/LH-Assembly/picard/picard.jar CreateSequenceDictionary R=/mnt/md0/piper/LH-Assembly/redundans/hc1neg_redundans/hc1negred/contigs.reduced.fa O=hc1negtest.dict`
