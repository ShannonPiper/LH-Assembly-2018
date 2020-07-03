# mapping reads to nasuia_genomic

## index obligates
bwa index -a bwtsw ../nasuia_genomic.fna

#bwa mem
bwa mem ../nasuia_genomic.fna ../../cleaned/$1/$2 ../../cleaned/$1/$3 > $1_nasuia_mapped_scaffs.sam

# convert sam to bam:
samtools view -S -b $1_nasuia_mapped_scaffs.sam > $1_nasuia_mapped_scaffs.bam

# sort bam:
samtools sort $1_nasuia_mapped_scaffs.bam -o $1_nasuia_mapped_scaffs.sorted.bam

# call consensus sequence using original fasta and sorted, mapped bam:
#samtools mpileup -C50 -uf ../redundans/$1_redundans/$1red/_gapcloser.1.1.fa $1_mapped_scaffs.sorted.bam | bcftools view -c - \
      #| vcfutils.pl vcf2fq -d 10 -D 100 | gzip > $1_scaffed_mapped.fq.gz
# or bcftools mpileup ...

bcftools mpileup -C50 -f ../nasuia_genomic.fna $1_nasuia_mapped_scaffs.sorted.bam -d 500 | bcftools call -c - | vcfutils.pl vcf2fq -d 10 -D 20 | gzip > $1_nasuia_scaffed_mapped.fq.gz
