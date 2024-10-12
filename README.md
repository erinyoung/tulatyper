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

## AMR Genes Among the Subspecies of F. tularensis

The motive of this analysis was to identify the AMR genes responsible for drug resistance among F. tularensis using AMRFinderPlus by NCBI. These data from 141 genomes from the NCBI. Two genes were found to be responsible for the AMR among all the subspecies.

#### Output from AMRFinderPlus

```
Protein identifier	Contig id	Start	Stop	Strand	Gene symbol	Sequence name	Scope	Element type	Element subtype	Class	Subclass	Method	Target length	Reference sequence length	% coverage of reference sequence	% Identity to reference sequence	Alignment length	Accession of closest sequence	Name of closest sequence	HMM id	HMM description
NA	AJ749949.2	630250	631110	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	AM233362.1	857328	858188	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	AM286280.1	630203	631063	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	BK006741.1	860983	861843	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP000437.1	860983	861843	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP000439.1	1134341	1135201	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP000608.1	1059023	1059883	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP000803.1	859086	859946	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP000915.1	750758	751618	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP001633.1	630307	631167	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP003862.1	859299	860159	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP002557.1	1131947	1132807	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP003048.2	706100	706960	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP003049.2	630191	631051	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP003932.1	855185	856045	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP007148.1	853852	854712	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	98.95	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009353.1	1500571	1501431	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	95.12	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009693.1	1698980	1699840	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009694.1	1581890	1582750	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009607.1	1656363	1657223	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	97.56	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009633.1	994981	995841	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP010115.1	1430631	1431491	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP010288.1	1084380	1085240	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP010289.1	848836	849696	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP010290.1	183898	184758	+	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP010103.1	891206	892066	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	95.12	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP010446.2	630132	630992	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009753.1	1174072	1174932	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP012037.1	15013	15873	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP012372.1	630114	630974	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP066295.1	857101	857961	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP016635.1	1137375	1138235	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009653.1	1137813	1138673	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	95.12	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP009682.1	683397	684257	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP048229.1	859324	860184	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP025778.1	859226	859813	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	PARTIALX	196	287	68.29	98.47	196	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP021490.1	997030	997890	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	97.91	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP034466.1	692686	693546	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP034467.1	199125	199985	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP034468.1	773917	774777	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP044002.1	1582196	1583056	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP044003.1	1582195	1583055	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP044004.1	1582630	1583490	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP044005.1	1582352	1583212	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	AP023459.1	788095	788955	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	AP023460.1	899958	900818	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP063128.1	1580270	1581130	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073120.1	630213	631073	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073122.1	628659	629519	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073123.1	625407	626267	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073121.1	630209	631069	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073125.1	629019	629879	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073124.1	629335	630195	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073126.1	630667	631101	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	PARTIALX	145	287	50.52	100	145	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073128.1	630233	631093	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073129.1	629224	630084	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP073127.1	630265	631125	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP058274.1	859025	859885	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP058301.1	859061	859921	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP058275.1	859095	859955	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP058276.1	630214	631074	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP089548.1	859026	859886	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP089549.1	1134247	1135107	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP089550.1	630015	630875	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP098826.1	859322	860182	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP129998.1	568705	569565	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP129999.1	1489579	1490439	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP130000.1	751002	751862	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP130001.1	437753	438613	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP130002.1	655577	656437	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP130004.1	1010806	1011666	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	CP130003.1	918072	918932	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_006570.2	630250	631110	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_007880.1	857328	858188	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_008245.1	630203	631063	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_017463.1	860983	861843	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_008369.1	860983	861843	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_008601.1	1134341	1135201	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_009257.1	1059023	1059883	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_009749.1	859086	859946	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_010677.1	750758	751618	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_017453.1	630307	631167	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_019551.1	859299	860159	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_017450.1	1131947	1132807	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_016933.2	706100	706960	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_016937.2	630191	631051	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NC_019537.1	855185	856045	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP007148.1	853852	854712	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	98.95	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009353.1	1500571	1501431	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	95.12	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009693.1	1698980	1699840	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009694.1	1581890	1582750	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009607.1	1656363	1657223	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	97.56	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009633.1	994981	995841	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP010115.1	1430631	1431491	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP010288.1	1084380	1085240	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP010289.1	848836	849696	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP010290.1	183898	184758	+	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP010103.1	891206	892066	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	95.12	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP010446.2	630132	630992	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009753.1	1174072	1174932	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP012037.1	15013	15873	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP012372.1	630114	630974	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP066295.1	857101	857961	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP016635.1	1137375	1138235	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009653.1	1137813	1138673	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	95.12	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP009682.1	683397	684257	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	94.77	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP048229.1	859324	860184	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP025778.1	859226	859813	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	PARTIALX	196	287	68.29	98.47	196	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP021490.1	997030	997890	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	97.91	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP034466.1	692686	693546	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP034467.1	199125	199985	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP034468.1	773917	774777	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP044002.1	1582196	1583056	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP044003.1	1582195	1583055	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP044004.1	1582630	1583490	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP044005.1	1582352	1583212	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_AP023459.1	788095	788955	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_AP023460.1	899958	900818	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073122.1	628659	629519	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073123.1	625407	626267	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073121.1	630209	631069	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073125.1	629019	629879	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073124.1	629335	630195	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.65	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073126.1	630667	631101	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	PARTIALX	145	287	50.52	100	145	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073128.1	630233	631093	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073129.1	629224	630084	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP073127.1	630265	631125	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP058274.1	859025	859885	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP058301.1	859061	859921	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP058275.1	859095	859955	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP058276.1	630214	631074	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP089548.1	859026	859886	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP089549.1	1134247	1135107	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP089550.1	630015	630875	-	blaFTU-1	class A beta-lactamase FTU-1	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	ALLELEX	287	287	100	100	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP098826.1	859322	860182	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP129998.1	568705	569565	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP129999.1	1489579	1490439	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP130000.1	751002	751862	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP130001.1	437753	438613	+	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP130004.1	1010806	1011666	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
NA	NZ_CP130003.1	918072	918932	-	blaFTU	FTU family class A beta-lactamase	core	AMR	AMR	BETA-LACTAM	BETA-LACTAM	BLASTX	287	287	100	99.3	287	WP_003023375.1	class A beta-lactamase FTU-1	NA	NA
```

Created as part of the ASM-NGS 2024 Hackathon with assistance from [@erinyoung](https://github.com/erinyoung), [@wboateng72](https://github.com/wboateng72), [@David-Mahoney](https://github.com/David-Mahoney), [@phillma2](https://github.com/phillma2), [@VishnuRaghuram94](https://github.com/VishnuRaghuram94), [@rpetit3](https://github.com/rpetit3), [@Quadjo](https://github.com/QuadjoLegend)
