# WARNING : THIS REPO IS STILL IN DEVELOPMENT AND PROBABLE DOES NOT WORK AS INTENDED

# tulatyper
Subtyping of Francisella tularensis subtypes

![tulatyper logo with image of rabbit head as "l" and jumping rabbit as cross of second "t"](https://github.com/erinyoung/tulatyper/blob/main/tulalogo.png)

## background

Distinguishing the subspecies of Francisella tularensis is crucial for understanding the pathogen's epidemiology, virulence, and potential public health impact. The four recognized subspecies are tularensis (Type A), holarctica (Type B), mediasiatica, and novicida. The subspecies differ significantly in their geographic distribution, pathogenicity, and host reservoirs. Identifying the subspecies can inform epidemiological tracking and help implement targeted measures to control outbreaks, especially in regions where different subspecies are endemic.

Prior methods have identified hypervariable regions (https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0007041) and sets of primers (https://journals.asm.org/doi/full/10.1128/jcm.01495-19), but these methods are difficult to implement using next-generation sequencing data.

The logic behind this method uses genes identified [All the Bacteria](https://www.biorxiv.org/content/10.1101/2024.03.08.584059v1) after prokka annotation and panaroo alignment. Essentially, there are genes present or absent for each subtype.

![tulatyper workflow steps](https://github.com/erinyoung/tulatyper/blob/main/tulatyper_flow.drawio.png)

## installation

Get the dependencies camlhmp and blast. The easiest way is via conda.
```
conda install -c bioconda camlhmp
```

Clone the respository
```
git clone https://github.com/erinyoung/tulatyper
```

## Usage
```
./bin/tulatyper --input input.fasta --outdir output
```

## Example output
```
outdir
- cmlhmp.txt
- cmlhmp.details.tsv
- cmlhmp.blastn.tsv
```

```
$ head outdir/*
==> outdir/camlhmp.blastn.tsv <==
qseqid  sseqid  pident  qcovs   qlen    slen    length  nident  mismatch        gapopen qstart  qend    sstart  send    evalue  bitscore
group_965       NC_006570.2     100.000 100     180     1892775 180     180     0       0       1       180     774767  774588  1.22e-92        333
group_1008      NC_006570.2     99.154  99      714     1892775 709     703     5       1       1       708     1662198 1662906 0.0     1275
group_1009      NC_006570.2     98.180  96      1707    1892775 1648    1618    28      2       36      1682    1663016 1664662 0.0     2876
group_1012      NC_006570.2     97.661  100     342     1892775 342     334     2       4       1       342     365215  364880  2.19e-167       582
group_1013      NC_006570.2     99.111  100     450     1892775 450     446     4       0       1       450     364871  364422  0.0     809
group_317       NC_006570.2     98.695  100     996     1892775 996     983     13      0       1       996     352918  353913  0.0     1768
group_317       NC_006570.2     98.695  100     996     1892775 996     983     13      0       1       996     380977  379982  0.0     1768
group_317       NC_006570.2     98.695  100     996     1892775 996     983     13      0       1       996     1286036 1285041 0.0     1768
group_1065      NC_006570.2     99.446  100     360     1892775 361     359     1       1       1       360     103101  103461  0.0     654

==> outdir/camlhmp.details.tsv <==
sample  type    status  targets missing schema  schema_version  camlhmp_version params  comment
camlhmp F. tularensis subsp. tularensis subtype A.I     False   group_965,CARKD~~~nnr           tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90   Excluded target group_1012 found, failing type F. tularensis subsp. tularensis subtype A.I
camlhmp F. tularensis subsp. tularensis subtype A.II    False   CARKD~~~nnr             tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90   Excluded target group_1012 found, failing type F. tularensis subsp. tularensis subtype A.II
camlhmp F. tularensis subsp. holarctica (type B)        False   group_1008,group_1009,group_1012,CARKD~~~nnr            tulatyper_targets       0.1.24286      1.1.0    min-coverage=90;min-pident=90   Excluded target group_965 found, failing type F. tularensis subsp. holarctica (type B)
camlhmp F. tularensis subsp. mediasiatica       False   CARKD~~~nnr     group_958       tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90   Excluded target group_1012 found, failing type F. tularensis subsp. mediasiatica
camlhmp F. tularensis subsp. novicida   False           lysC,btrK,hepA,group_58,group_23        tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90   Excluded target CARKD~~~nnr found, failing type F. tularensis subsp. novicida
camlhmp F. tularensis subsp. tularensis subtype A.I all True    group_965,CARKD~~~nnr           tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90
camlhmp F. tularensis subsp. tularensis subtype A.II all        True    CARKD~~~nnr             tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90
camlhmp F. tularensis subsp. holarctica (type B) all    True    group_1008,group_1009,group_1012,CARKD~~~nnr            tulatyper_targets       0.1.24286      1.1.0    min-coverage=90;min-pident=90
camlhmp F. tularensis subsp. mediasiatica all   False   CARKD~~~nnr     group_958       tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90

==> outdir/camlhmp.tsv <==
sample  type    targets schema  schema_version  camlhmp_version params  comment
camlhmp multiple        group_965,group_1008,group_1009,group_1012,CARKD~~~nnr  tulatyper_targets       0.1.24286       1.1.0   min-coverage=90;min-pident=90  Found matches for multiple types including: F. tularensis subsp. tularensis subtype A.I all, F. tularensis subsp. tularensis subtype A.II all, F. tularensis subsp. holarctica (type B) all
```

Created as part of the ASM-NGS 2024 Hackathon with assistance from [@erinyoung](https://github.com/erinyoung), [@wboateng72](https://github.com/wboateng72), [@David-Mahoney](https://github.com/David-Mahoney), [@phillma2](https://github.com/phillma2), [@VishnuRaghuram94](https://github.com/VishnuRaghuram94), [@rpetit3](https://github.com/rpetit3)
