# Benchmarking PubMed Central

## General

This is the end-to-end benchmarking result for GROBID version **0.8.2** against the `PMC_sample_1943` dataset, see
the [End-to-end evaluation](End-to-end-evaluation.md) page for explanations and for reproducing this evaluation.

The following end-to-end results are using:

- **BidLSTM_ChainCRF_FEATURES** as sequence labeling for the header model

- **BidLSTM_ChainCRF_FEATURES** as sequence labeling for the reference-segmenter model

- **BidLSTM-CRF-FEATURES** as sequence labeling for the citation model

- **BidLSTM_CRF_FEATURES** as sequence labeling for the affiliation-address model

- **CRF Wapiti** as sequence labelling engine for all other models.

Header extractions are consolidated by default with [biblio-glutton](https://github.com/kermitt2/biblio-glutton)
service (the results with CrossRef REST API as consolidation service should be similar but much slower).

Other versions of these benchmarks with variants and **Deep Learning models** (e.g. newer master snapshots) are
available [here](https://github.com/kermitt2/grobid/tree/master/grobid-trainer/doc). Note that Deep Learning models
might provide higher accuracy, but at the cost of slower runtime and more expensive CPU/GPU resources.

Evaluation on 1943 random PDF PMC files out of 1943 PDF from 1943 different journals (0 PDF parsing failure).

Runtime for processing 1943 PDF: **1467** seconds, (0.75s per PDF) on Ubuntu 22.04, 16 CPU (32 threads), 128GB RAM and
with a GeForce GTX 1080 Ti GPU.

Note: with CRF only models, runtime is 470s (0.24 seconds per PDF) with 4 CPU, 8 threads.

## Header metadata

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 15.46     | 15.18     | 15.32     | 1911    |
| authors                     | 90.61     | 90.52     | 90.57     | 1941    |
| first_author                | 96.24     | 96.14     | 96.19     | 1941    |
| keywords                    | 40.59     | 33.77     | 36.87     | 1380    |
| title                       | 83.44     | 83.22     | 83.33     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **67.83** | **65.77** | **66.79** | 9116    |
| all fields (macro avg.)     | 65.27     | 63.76     | 64.45     | 9116    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 59.49     | 58.4      | 58.94     | 1911    |
| authors                     | 92.57     | 92.48     | 92.53     | 1941    |
| first_author                | 96.7      | 96.6      | 96.65     | 1941    |
| keywords                    | 48.08     | 39.93     | 43.63     | 1380    |
| title                       | 90.87     | 90.63     | 90.75     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **80.31** | **77.86** | **79.07** | 9116    |
| all fields (macro avg.)     | 77.54     | 75.61     | 76.5      | 9116    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 88.01     | 86.39     | 87.19     | 1911    |
| authors                     | 94.84     | 94.74     | 94.79     | 1941    |
| first_author                | 96.91     | 96.81     | 96.86     | 1941    |
| keywords                    | 71.29     | 59.2      | 64.69     | 1380    |
| title                       | 97.47     | 97.22     | 97.35     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.37** | **88.58** | **89.95** | 9116    |
| all fields (macro avg.)     | 89.7      | 86.87     | 88.18     | 9116    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 83.74     | 82.21     | 82.97     | 1911    |
| authors                     | 93.55     | 93.46     | 93.51     | 1941    |
| first_author                | 96.24     | 96.14     | 96.19     | 1941    |
| keywords                    | 61.26     | 50.87     | 55.58     | 1380    |
| title                       | 95.3      | 95.06     | 95.18     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **88.26** | **85.56** | **86.89** | 9116    |
| all fields (macro avg.)     | 86.02     | 83.55     | 84.68     | 9116    |

#### Instance-level results

```
Total expected instances: 	1943
Total correct instances: 	138 (strict) 
Total correct instances: 	594 (soft) 
Total correct instances: 	1104 (Levenshtein) 
Total correct instances: 	953 (ObservedRatcliffObershelp) 

Instance-level recall:	7.1	(strict) 
Instance-level recall:	30.57	(soft) 
Instance-level recall:	56.82	(Levenshtein) 
Instance-level recall:	49.05	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 83.09     | 76.22     | 79.51     | 85778   |
| date                        | 94.68     | 84.11     | 89.09     | 87067   |
| first_author                | 89.83     | 82.38     | 85.94     | 85778   |
| inTitle                     | 73.32     | 71.75     | 72.53     | 81007   |
| issue                       | 91.14     | 87.61     | 89.34     | 16635   |
| page                        | 94.64     | 83.57     | 88.76     | 80501   |
| title                       | 79.76     | 75.22     | 77.42     | 80736   |
| volume                      | 96.14     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **87.3**  | **80.62** | **83.83** | 597569  |
| all fields (macro avg.)     | 87.83     | 81.31     | 84.42     | 597569  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 83.57     | 76.65     | 79.96     | 85778   |
| date                        | 94.68     | 84.11     | 89.09     | 87067   |
| first_author                | 90.01     | 82.54     | 86.11     | 85778   |
| inTitle                     | 85.06     | 83.23     | 84.14     | 81007   |
| issue                       | 91.14     | 87.61     | 89.34     | 16635   |
| page                        | 94.64     | 83.57     | 88.76     | 80501   |
| title                       | 91.53     | 86.31     | 88.84     | 80736   |
| volume                      | 96.14     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.7**  | **83.76** | **87.09** | 597569  |
| all fields (macro avg.)     | 90.84     | 84.21     | 87.38     | 597569  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall | f1        | support |
|-----------------------------|-----------|--------|-----------|---------|
| authors                     | 89.26     | 81.87  | 85.41     | 85778   |
| date                        | 94.68     | 84.11  | 89.09     | 87067   |
| first_author                | 90.21     | 82.73  | 86.31     | 85778   |
| inTitle                     | 86.31     | 84.46  | 85.37     | 81007   |
| issue                       | 91.14     | 87.61  | 89.34     | 16635   |
| page                        | 94.64     | 83.57  | 88.76     | 80501   |
| title                       | 93.86     | 88.51  | 91.11     | 80736   |
| volume                      | 96.14     | 89.66  | 92.79     | 80067   |
|                             |           |        |           |         |
| **all fields (micro avg.)** | **92.05** | **85** | **88.38** | 597569  |
| all fields (macro avg.)     | 92.03     | 85.32  | 88.52     | 597569  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 86.04     | 78.92     | 82.32     | 85778   |
| date                        | 94.68     | 84.11     | 89.09     | 87067   |
| first_author                | 89.85     | 82.4      | 85.96     | 85778   |
| inTitle                     | 83.62     | 81.83     | 82.72     | 81007   |
| issue                       | 91.14     | 87.61     | 89.34     | 16635   |
| page                        | 94.64     | 83.57     | 88.76     | 80501   |
| title                       | 93.46     | 88.13     | 90.72     | 80736   |
| volume                      | 96.14     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.09** | **84.12** | **87.47** | 597569  |
| all fields (macro avg.)     | 91.2      | 84.53     | 87.71     | 597569  |

#### Instance-level results

```
Total expected instances: 		90125
Total extracted instances: 		85309
Total correct instances: 		38731 (strict) 
Total correct instances: 		50867 (soft) 
Total correct instances: 		55720 (Levenshtein) 
Total correct instances: 		52269 (RatcliffObershelp) 

Instance-level precision:	45.4 (strict) 
Instance-level precision:	59.63 (soft) 
Instance-level precision:	65.32 (Levenshtein) 
Instance-level precision:	61.27 (RatcliffObershelp) 

Instance-level recall:	42.97	(strict) 
Instance-level recall:	56.44	(soft) 
Instance-level recall:	61.83	(Levenshtein) 
Instance-level recall:	58	(RatcliffObershelp) 

Instance-level f-score:	44.15 (strict) 
Instance-level f-score:	57.99 (soft) 
Instance-level f-score:	63.52 (Levenshtein) 
Instance-level f-score:	59.59 (RatcliffObershelp) 

Matching 1 :	68240

Matching 2 :	4124

Matching 3 :	1861

Matching 4 :	658

Total matches :	74883
```

#### Citation context resolution

```

Total expected references: 	 90125 - 46.38 references per article
Total predicted references: 	 85309 - 43.91 references per article

Total expected citation contexts: 	 139835 - 71.97 citation contexts per article
Total predicted citation contexts: 	 115014 - 59.19 citation contexts per article

Total correct predicted citation contexts: 	 97398 - 50.13 citation contexts per article
Total wrong predicted citation contexts: 	 17616 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 84.68
Recall citation contexts: 	 69.65
fscore citation contexts: 	 76.44
```

## Fulltext structures

Fulltext structure contents are complicated to capture from JATS NLM files. They are often normalized and different from
the actual PDF content and are can be inconsistent from one document to another. The scores of the following metrics are
thus not very meaningful in absolute term, in particular for the strict matching (textual content of the srtructure can
be very long). As relative values for comparing different models, they seem however useful.

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| figure_title                | 31.97     | 26.63     | 29.06     | 7281    |
| reference_citation          | 58.13     | 58.81     | 58.47     | 134196  |
| reference_figure            | 60.58     | 68.27     | 64.2      | 19330   |
| reference_table             | 82.84     | 89.63     | 86.1      | 7327    |
| section_title               | 72.47     | 67.67     | 69.99     | 27619   |
| table_title                 | 67.74     | 49.61     | 57.28     | 3971    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **60.57** | **60.72** | **60.65** | 199724  |
| all fields (macro avg.)     | 62.29     | 60.1      | 60.85     | 199724  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| figure_title                | 79.81     | 66.49     | 72.54     | 7281    |
| reference_citation          | 62.42     | 63.14     | 62.78     | 134196  |
| reference_figure            | 61.08     | 68.83     | 64.72     | 19330   |
| reference_table             | 83.01     | 89.8      | 86.27     | 7327    |
| section_title               | 77.86     | 72.7      | 75.19     | 27619   |
| table_title                 | 94.36     | 69.1      | 79.78     | 3971    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **66.07** | **66.23** | **66.15** | 199724  |
| all fields (macro avg.)     | 76.42     | 71.68     | 73.55     | 199724  |

**Document-level ratio results**

| label                       | precision | recall | f1    | support |
|-----------------------------|-----------|--------|-------|---------|
|                             |           |        |       |         |
| **all fields (micro avg.)** | **0**     | **0**  | **0** | 0       |
| all fields (macro avg.)     | 0         | 0      | 0     | 0       |

Evaluation metrics produced in 1295.765 seconds



