# hse21_hw1

Код  такой 

```
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq


seqtk sample -s601 oil_R1.fastq 5000000 > R1_pe.fastq
seqtk sample -s601 oil_R2.fastq 5000000 > R2_pe.fastq
seqtk sample -s601 oilMP_S4_L001_R1_001.fastq 1500000 > R1_mp.fastq
seqtk sample -s601 oilMP_S4_L001_R2_001.fastq 1500000 > R2_mp.fastq

rm oil_R1.fastq oil_R2.fastq oilMP_S4_L001_R1_001.fastq oilMP_S4_L001_R2_001.fastq

mkdir fastqc
ls *.fastq | xargs -P 4 -tI{} fastqc -o fastqc {}
mkdir multiqc
multiqc -o multiqc fastqc

platanus_trim R1_pe.fastq R2_pe.fastq 
platanus_internal_trim R1_mp.fastq R2_mp.fastq 

mkdir trimmed
mv -v *trimmed trimme/
mkdir trimmed_fastqc
ls trimmed/* | xargs -P 4 -tI{} fastqc -o trimmed_fastqc {}
mkdir trimmed_multiqc
multiqc -o trimmed_multiqc trimmed_fastqc
```
