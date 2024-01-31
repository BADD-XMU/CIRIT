# README

## Description

Cirit is a completely reference-free algorithm for genome-wide circular RNA (circRNA) detection from RNA sequencing (RNA-seq) transcriptome. This new algorithm, other than current BSJ-based algorithms, will provide direct sequence evidence for RNA circularization. It breaks the dependency of good quality genome in circRNA detection, and thus allows easy deployment to any organism, even under the circumstance of draft genome or no genome.

## Software Download

*de novo* circRNA detection with full-length sequence: [Cirit.jar](http://bioinf.xmu.edu.cn/CIRIT/files/download/Cirit-1.0.jar)

****Recovery of partially assembled circRNA: [Patch (Applicable with reference genome)](http://bioinf.xmu.edu.cn/CIRIT/files/download/Additional%20procedure.zip)

Annotate the circRNAs and determine the back-splice junctions (BSJs): [Cirit-BSJ.jar](http://bioinf.xmu.edu.cn/CIRIT/files/download/trCirit_BSJ-1.0.1-SNAPSHOT.jar)

Genome assembly T2T-CHM13: [Github](https://github.com/marbl/CHM13#telomere-to-telomere-consortium-chm13-project)

Bed file of genome assembly T2T-CHM13: [chm13.bed](http://bioinf.xmu.edu.cn/CIRIT/files/download/chm13.bed)

## **Prerequisites**

1. Undertake the RNA-seq dataset assembly in advance using *de novo* assembler such as IDBA-Trans or Velvet. The output transcriptome should be deposit as a single sequence file in **.fasta* format. Please follow the best procedure of the assembler to obtain good transcriptome, which will substantially affect the circRNA detection.
2. Make sure the Java Runtime Environment (JRE) has been properly installed and is running. JRE version > 1.7 is recommended.

## Commands and Options

Cirit includes two modules, `Cirit`, and `Cirit-BSJ`. These modules should be performed sequentially in the following order:  `Cirit`, and `Cirit-BSJ`.

### The Cirit module

A *de novo* method, to overcome the genomic constraints on transcriptome-wide circRNA detection.

The Cirit module runs from a command line as follows:

```bash
java -jar Cirit.jar -i <fasta> [OPTIONS]
```

Options:

```bash
usage: java -jar Cirit.jar -i <fasta> [OPTIONS]
 -h,--help              Print help
 -i,--input       Input FASTA file
 -o,--output      name of output file.
                        By default, the output file is put in current
                        directory, named "CircRNAs_Cirit.fa"
 -w,--window    window/seed (integer), used to initial search.
                        By default, window is 10.
```

Cirit module will generate one output files:

```bash
CircRNAs_Cirit.fa
```

Recovery of partially assembled circRNA：

```bash
Step1: python Pred1 -genePredExt -geneNameAsName2 -r -o output.gene.Pred

Step2: python Pred2.py -o output.gene.Pred -i > circRNA_anno.bed

Step3: python Pred3.py circRNA_anno.bed -reference > circRNA_full.fasta

-r,--input hg19.gtf or hg38.gtf
-i,--input circRNA.bed

-reference,--input GRCh38.p10.genome.fa or GRCh19.p10.genome.fa
```

### The Cirti-BSJ module

Annotate the circRNAs and determine the back-splice junctions (BSJs) by mapping the circRNA sequences to genome.

The Cirit-BSJ module runs from a command line as follows:

```bash
java -jar Cirit-BSJ.jar -i <Cirit.fa> -i2 <genome.bed> -i3 <genome_index>
```

Options:

```bash
usage: java -jar Cirit-BSJ.jar -i <Cirit.fa> -i2 <genome.bed> -i3
            <genome_index>
 -h,--help              Print help
 -i,--input <file>      Input Cirit.fa file
 -i2,--input2 <file2>   Input genoemeBed file
 -i3,--input3 <file3>   Input genome_index file
 -o,--output <file>     name of output file.
                        By default, the output file is put in current
                        directory, named "circ_anno.gtf"

```

Cirit-BSJ module will generate following output files:

```bash
circ_anno.gtf
```

## CircRNA download

HepG2 circRNAs detected by Cirit are available for downloading

1. CircRNA-enriched library (RNase R+/ribo-)

[CirRNAseq_CircRNAsWithFullSequence.fa](http://bioinf.xmu.edu.cn/CIRIT/files/download/cirRNAseq/CirRNAseq_CircRNAsWithFullSequence.fa)

[CirRNAseq_PotentialCircRNA.bed](http://bioinf.xmu.edu.cn/CIRIT/files/download/cirRNAseq/CirRNAseq_PotentialCircRNA.bed)

1. Total RNA library (ribo-)

[TotalRNAseq_CircRNAsWithFullSequence.fa](http://bioinf.xmu.edu.cn/CIRIT/files/download/totalRNAseq/TotalRNAseq_CircRNAsWithFullSequence.fa)

## License

The Bioinformatics-Aided Drug Discovery Group (BADD)@Xiamen University declare the full copyright of this software. It is free for academic use.