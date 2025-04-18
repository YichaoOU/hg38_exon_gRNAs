# Database of CRISPR-Cas9 gRNAs for Human Gene-Knockout

## Summary

All human exons were taken from `Gencode V47 basic` GTF file, extended +/- 10bp. Then gRNAs with `NGG` PAM were identified using `find_all_gRNA.py` from [HemTools](https://raw.githubusercontent.com/YichaoOU/HemTools/6e4bf88da9aa0a8ceaddd0884d12faef6d8ed87f/bin/find_all_gRNA.py). 

## gRNA information

1. Column `numOffTargets`. Number of off-targets for each gRNA. The on-target sequence was searched against hg38 with `mismiatch=0` and `NGG` PAM. 

2. Associated genes and whether or not the exon is a constitutive exon defined by `HexEvent` or `GeCKOv1`.

## Cas9 editing activity scores

1. GC content. Column `gc`

2. `homopolymer`, length of identical repeated base

3. `shannon_index`, ACGT diversity score, max is 2

4. `N_repeatMask` number of lower-case base (i.e., softmasked) in hg38.fa

5. `CDS%` gRNA occuring position in transcript CDS. ideal is between 5% to 65%.

6. many various editing scores: CRISPRaterScores	DeepHFScores	RuleSet1Scores	RuleSet3Scores	DeepSpCas9Scores	CRISPRscanScores


## final candidate set

see `hg38.Gene_KO.candidateg_RNA.bed.gz`

`df = df[(df.gc.between(0.2,0.8))&(df.numOffTargets==0)&(df.N_repeatMask==0)&(df.homopolymer<=4)&(df.shannon_index>=1)&(df['CDS%'].between(0.05,0.65))]`

Personally, I think `DeepSpCas9Scores` is a more accurate editing activity score.


## All gRNA info

see `gRNA.all_info.0xx.tsv.gz`.

Too large that I need to split them.

