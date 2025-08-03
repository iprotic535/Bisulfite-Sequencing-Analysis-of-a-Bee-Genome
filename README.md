# Bisulfite-Sequencing-Analysis-of-a-Bee-Genome
(bch709) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/clean$ fastqc -o /media/ismam/Data/Bismark/AM2/reports/raw *.fastq
(Bismark) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/reports$ /media/ismam/Data/Bismark/FastQ-Screen-0.16.0/fastq_screen   --conf ../FastQ-Screen-0.16.0/fastq_screen.conf   --bisulfite   --outdir ./reports/raw_screen/   raw/*.fastq
(bch709) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/clean$ trim_galore --paired --clip_R1 2 --clip_R2 2 --three_prime_clip_R1 2 --three_prime_clip_R2 2 --illumina -o ../clean/ SRR445804_1.fastq SRR445804_2.fastq 
(Bismark) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/reports$ /home/ismam/anaconda3/envs/multiqc/bin/multiqc . 
(Bismark) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/reports$ /media/ismam/Data/Bismark/FastQ-Screen-0.16.0/fastq_screen   --conf ../../FastQ-Screen-0.16.0/fastq_screen.conf   --bisulfite   --outdir ./raw_screen/   ../clean/*.fq
(bch709) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/clean$ fastqc -o /media/ismam/Data/Bismark/AM2/reports/clean/ *.fq
(Bismark) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/reports$ /home/ismam/anaconda3/envs/multiqc/bin/multiqc . 
(Bismark) ismam@dap-lab:/media/ismam/Data/Bismark/AM2$ bismark --un --ambiguous --genome ./Ref_genome/ -1 ./clean/SRR445804_1_val_1.fq -2 ./clean/SRR445804_2_val_2.fq -o ./output//alignment/
(bch709) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/output/alignment$ cd ../methylation_calling/dedup/
(bch709) ismam@dap-lab:/media/ismam/Data/Bismark/AM2/output/methylation_calling/dedup$ awk 'BEGIN {OFS="\t"; print "chrom","pos","strand","mc_class","methylated_bases","total_bases"} \
{gsub("Group","",$1); gsub("\\.","",$1); print $1, $2, $3, $6, $4, $5}' SRR445804.CpG_report.txt > cytosine_data.tsv
