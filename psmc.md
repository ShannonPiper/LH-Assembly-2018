# PSMC for getting demographic history of M. quad genomes

# Zach's code:
tutorial: https://informatics.fas.harvard.edu/psmc-journal-club-walkthrough.html

NOTE "*" is a wildcard for naming, and you don't want to write filenames like this.

map reads to scaffolded (spades) assembly the first build index of fasta:
`bwa index -a bwtsw *scaffolded_assembly*.fa`

then map using bwa mem, generate unsorted SAM file (huge):
`bwa mem *scaffolded_assembly*fa *PE_reads_1*.fq *PE_reads_2*.fq > *mapped_scaffs.sam`

convert sam to bam:
`samtools view -S -b *mapped_scaffs.sam > *mapped_scaffs.bam`

sort bam:
`samtools sort *mapped_scaffs.bam -o *mapped_scaffs.sorted.bam`

all consensus sequence using original fasta and sorted, mapped bam:
`samtools mpileup -C50 -uf *scaffolded_assembly*.fa *mapped_scaffs.sorted.bam | bcftools view -c - \
      | vcfutils.pl vcf2fq -d 10 -D 100 | gzip > *scaffed_mapped.fq.gz`
 or `bcftools mpileup ...`
### depending on your version of samtools, you might need to use bcftools. the -d (low) and -D (high) are the coverage cutoffs to reduce sequencing bias and might need some troubleshooting based on depth

now start inference using PSMC:
generate psmc fasta:
`./psmc/utils/fq2psmcfa *scaffed_mapped.fq.gz > *scaffed_mapped.psmcfa`

"default" parameters
`./psmc/psmc -p "4+25*2+4+6" -o *scaffed_mapped.psmc *scaffed_mapped.psmcfa`

plot with generation time of 2/year and mutation rate: drosophila 8.5E-09
`./psmc/utils/psmc_plot.pl -u 8.9e-09 -g 0.5 *scaffed_mapped.5 *scaffed_mapped.psmc`
