##dnaseq_variant_calling
#Variant calling pipeline from whole genome or exome resequencing using GATK 3.8 and 4.


Variant calling pipeline using GATK 3.8 and 4 and picard from bwa aligned and deduplicated bam files based on GATK Best-Practices pipeline https://software.broadinstitute.org/gatk/best-practices/workflow?id=11145

The script pre-processes the provided bam files using GATK BaseRecalibrator. The variants are called with GATK4 HaplotypeCaller in GVCF mode.

The output of the script are recalibrated bam files, vcf files with raw and filtered snps and indels combined for all input samples (sample information preserved).

The script uses zebrafish GRCz11 genome as a reference, this can be modified accoriding to the reference used for producing alignments.

The script parallelizes the file processing per sample or per chromosomes, therefore chromosome names list should be provided in the path of reference genome.

#Input

input_parameters description as .json file. Should include "samples" as a list and "bam_prefix". Example:

``` {python}
{
	"samples" : ["wt", "mut", "sib"],
	"bam_prefix": "_dedup.bam"
}
```

One or multiple .bam files containing read group information. The bam names should start with sample name followed by "bam_prefix" (as in input_paramteres.json file). Example:

``` {python}
wt_dedup.bam
mut_dedup.bam
sib_dedup.bam
```

#Running the script

In the directory where the input bams (or links to them) are located:

``` {bash}
python3 /path/to/script/dnaseq_var_call.py /path/to/dnaseq_input_parameters.json
```
