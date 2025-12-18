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

| label                       | precision | recall   | f1       | support |
|-----------------------------|-----------|----------|----------|---------|
| abstract                    | 15.24     | 14.97    | 15.1     | 1911    |
| authors                     | 90.76     | 90.57    | 90.67    | 1941    |
| first_author                | 96.33     | 96.14    | 96.24    | 1941    |
| keywords                    | 35.71     | 34.06    | 34.87    | 1380    |
| title                       | 83.45     | 83.27    | 83.36    | 1943    |
|                             |           |          |          |         |
| **all fields (micro avg.)** | **66.6**  | **65.8** | **66.2** | 9116    |
| all fields (macro avg.)     | 64.3      | 63.8     | 64.05    | 9116    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 58        | 56.93     | 57.46     | 1911    |
| authors                     | 92.72     | 92.53     | 92.63     | 1941    |
| first_author                | 96.75     | 96.55     | 96.65     | 1941    |
| keywords                    | 44.82     | 42.68     | 43.73     | 1380    |
| title                       | 90.97     | 90.79     | 90.88     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.98** | **78.01** | **78.49** | 9116    |
| all fields (macro avg.)     | 76.65     | 75.9      | 76.27     | 9116    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| abstract                    | 86.62     | 85.03     | 85.82    | 1911    |
| authors                     | 94.99     | 94.8      | 94.89    | 1941    |
| first_author                | 97.01     | 96.81     | 96.91    | 1941    |
| keywords                    | 72.37     | 68.91     | 70.6     | 1380    |
| title                       | 97.73     | 97.53     | 97.63    | 1943    |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **90.97** | **89.84** | **90.4** | 9116    |
| all fields (macro avg.)     | 89.74     | 88.62     | 89.17    | 9116    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 82.57     | 81.06     | 81.81     | 1911    |
| authors                     | 93.75     | 93.56     | 93.66     | 1941    |
| first_author                | 96.33     | 96.14     | 96.24     | 1941    |
| keywords                    | 57.76     | 55        | 56.35     | 1380    |
| title                       | 95.46     | 95.27     | 95.36     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **87.09** | **86.01** | **86.55** | 9116    |
| all fields (macro avg.)     | 85.18     | 84.2      | 84.68     | 9116    |

#### Instance-level results

```
Total expected instances: 	1943
Total correct instances: 	130 (strict) 
Total correct instances: 	581 (soft) 
Total correct instances: 	1199 (Levenshtein) 
Total correct instances: 	974 (ObservedRatcliffObershelp) 

Instance-level recall:	6.69	(strict) 
Instance-level recall:	29.9	(soft) 
Instance-level recall:	61.71	(Levenshtein) 
Instance-level recall:	50.13	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 83.12     | 76.1     | 79.46     | 85778   |
| date                        | 94.7      | 84.02    | 89.04     | 87067   |
| first_author                | 89.87     | 82.26    | 85.89     | 85778   |
| inTitle                     | 73.35     | 71.64    | 72.48     | 81007   |
| issue                       | 91.09     | 87.4     | 89.2      | 16635   |
| page                        | 94.62     | 83.45    | 88.68     | 80501   |
| title                       | 79.8      | 75.11    | 77.38     | 80736   |
| volume                      | 96.17     | 89.54    | 92.73     | 80067   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **87.32** | **80.5** | **83.77** | 597569  |
| all fields (macro avg.)     | 87.84     | 81.19    | 84.36     | 597569  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 83.59     | 76.53     | 79.91     | 85778   |
| date                        | 94.7      | 84.02     | 89.04     | 87067   |
| first_author                | 90.04     | 82.41     | 86.06     | 85778   |
| inTitle                     | 85.1      | 83.12     | 84.1      | 81007   |
| issue                       | 91.09     | 87.4      | 89.2      | 16635   |
| page                        | 94.62     | 83.45     | 88.68     | 80501   |
| title                       | 91.57     | 86.2      | 88.8      | 80736   |
| volume                      | 96.17     | 89.54     | 92.73     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.73** | **83.64** | **87.04** | 597569  |
| all fields (macro avg.)     | 90.86     | 84.08     | 87.32     | 597569  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 89.29     | 81.75     | 85.36     | 85778   |
| date                        | 94.7      | 84.02     | 89.04     | 87067   |
| first_author                | 90.25     | 82.6      | 86.26     | 85778   |
| inTitle                     | 86.35     | 84.34     | 85.33     | 81007   |
| issue                       | 91.09     | 87.4      | 89.2      | 16635   |
| page                        | 94.62     | 83.45     | 88.68     | 80501   |
| title                       | 93.91     | 88.39     | 91.07     | 80736   |
| volume                      | 96.17     | 89.54     | 92.73     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.07** | **84.88** | **88.33** | 597569  |
| all fields (macro avg.)     | 92.05     | 85.19     | 88.46     | 597569  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall | f1        | support |
|-----------------------------|-----------|--------|-----------|---------|
| authors                     | 86.07     | 78.8   | 82.27     | 85778   |
| date                        | 94.7      | 84.02  | 89.04     | 87067   |
| first_author                | 89.89     | 82.27  | 85.91     | 85778   |
| inTitle                     | 83.66     | 81.72  | 82.68     | 81007   |
| issue                       | 91.09     | 87.4   | 89.2      | 16635   |
| page                        | 94.62     | 83.45  | 88.68     | 80501   |
| title                       | 93.51     | 88.02  | 90.68     | 80736   |
| volume                      | 96.17     | 89.54  | 92.73     | 80067   |
|                             |           |        |           |         |
| **all fields (micro avg.)** | **91.12** | **84** | **87.42** | 597569  |
| all fields (macro avg.)     | 91.21     | 84.4   | 87.65     | 597569  |

#### Instance-level results

```
Total expected instances: 		90125
Total extracted instances: 		85086
Total correct instances: 		38645 (strict) 
Total correct instances: 		50777 (soft) 
Total correct instances: 		55619 (Levenshtein) 
Total correct instances: 		52178 (RatcliffObershelp) 

Instance-level precision:	45.42 (strict) 
Instance-level precision:	59.68 (soft) 
Instance-level precision:	65.37 (Levenshtein) 
Instance-level precision:	61.32 (RatcliffObershelp) 

Instance-level recall:	42.88	(strict) 
Instance-level recall:	56.34	(soft) 
Instance-level recall:	61.71	(Levenshtein) 
Instance-level recall:	57.9	(RatcliffObershelp) 

Instance-level f-score:	44.11 (strict) 
Instance-level f-score:	57.96 (soft) 
Instance-level f-score:	63.49 (Levenshtein) 
Instance-level f-score:	59.56 (RatcliffObershelp) 

Matching 1 :	68157

Matching 2 :	4123

Matching 3 :	1853

Matching 4 :	658

Total matches :	74791
```

#### Citation context resolution

```

Total expected references: 	 90125 - 46.38 references per article
Total predicted references: 	 85086 - 43.79 references per article

Total expected citation contexts: 	 139835 - 71.97 citation contexts per article
Total predicted citation contexts: 	 114956 - 59.16 citation contexts per article

Total correct predicted citation contexts: 	 97373 - 50.11 citation contexts per article
Total wrong predicted citation contexts: 	 17583 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 84.7
Recall citation contexts: 	 69.63
fscore citation contexts: 	 76.43
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
| figure_title                | 31.98     | 26.58     | 29.03     | 7281    |
| reference_citation          | 58.03     | 58.83     | 58.43     | 134196  |
| reference_figure            | 60.59     | 68.28     | 64.21     | 19330   |
| reference_table             | 82.89     | 89.7      | 86.16     | 7327    |
| section_title               | 72.31     | 67.69     | 69.93     | 27619   |
| table_title                 | 67.92     | 49.63     | 57.35     | 3971    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **60.49** | **60.75** | **60.62** | 199724  |
| all fields (macro avg.)     | 62.29     | 60.12     | 60.85     | 199724  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| figure_title                | 79.89     | 66.39     | 72.52     | 7281    |
| reference_citation          | 62.3      | 63.17     | 62.73     | 134196  |
| reference_figure            | 61.08     | 68.84     | 64.73     | 19330   |
| reference_table             | 83.05     | 89.87     | 86.33     | 7327    |
| section_title               | 77.7      | 72.74     | 75.14     | 27619   |
| table_title                 | 94.42     | 69        | 79.73     | 3971    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **65.97** | **66.25** | **66.11** | 199724  |
| all fields (macro avg.)     | 76.41     | 71.67     | 73.53     | 199724  |

**Document-level ratio results**

| label                       | precision | recall | f1    | support |
|-----------------------------|-----------|--------|-------|---------|
|                             |           |        |       |         |
| **all fields (micro avg.)** | **0**     | **0**  | **0** | 0       |
| all fields (macro avg.)     | 0         | 0      | 0     | 0       |

Evaluation metrics produced in 1282.248 seconds


