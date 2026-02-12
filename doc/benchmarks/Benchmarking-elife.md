# Benchmarking eLife

## General

This is the end-to-end benchmarking result for GROBID version **0.8.2** against the `eLife` test set, see
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

Evaluation on 984 PDF preprints out of 984 (no failure).

Runtime for processing 984 PDF: **1131** seconds (1.15 seconds per PDF file) on Ubuntu 22.04, 16 CPU (32 threads), 128GB
RAM and with a GeForce GTX 1080 Ti GPU.

Note: with CRF only models runtime is 492s (0.50 seconds per PDF) with 4 CPU, 8 threads.

## Header metadata

Evaluation on 984 random PDF files out of 982 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 9.53      | 9.25      | 9.39      | 984     |
| authors                     | 74.67     | 73.75     | 74.21     | 983     |
| first_author                | 92.48     | 91.45     | 91.96     | 982     |
| title                       | 86.92     | 85.06     | 85.98     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **66.09** | **64.86** | **65.47** | 3933    |
| all fields (macro avg.)     | 65.9      | 64.88     | 65.38     | 3933    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 22.41     | 21.75     | 22.07     | 984     |
| authors                     | 74.97     | 74.06     | 74.51     | 983     |
| first_author                | 92.48     | 91.45     | 91.96     | 982     |
| title                       | 94.91     | 92.89     | 93.89     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **71.35** | **70.02** | **70.68** | 3933    |
| all fields (macro avg.)     | 71.19     | 70.03     | 70.61     | 3933    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 47.43     | 46.04     | 46.73     | 984     |
| authors                     | 88.57     | 87.49     | 88.02     | 983     |
| first_author                | 92.79     | 91.75     | 92.27     | 982     |
| title                       | 96.37     | 94.31     | 95.33     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **81.4**  | **79.89** | **80.64** | 3933    |
| all fields (macro avg.)     | 81.29     | 79.9      | 80.59     | 3933    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 44.5      | 43.19     | 43.84     | 984     |
| authors                     | 80.23     | 79.25     | 79.73     | 983     |
| first_author                | 92.48     | 91.45     | 91.96     | 982     |
| title                       | 96.37     | 94.31     | 95.33     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.5**  | **77.04** | **77.76** | 3933    |
| all fields (macro avg.)     | 78.39     | 77.05     | 77.71     | 3933    |

#### Instance-level results

```
Total expected instances: 	984
Total correct instances: 	74 (strict) 
Total correct instances: 	197 (soft) 
Total correct instances: 	381 (Levenshtein) 
Total correct instances: 	338 (ObservedRatcliffObershelp) 

Instance-level recall:	7.52	(strict) 
Instance-level recall:	20.02	(soft) 
Instance-level recall:	38.72	(Levenshtein) 
Instance-level recall:	34.35	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 984 random PDF files out of 982 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 79.56     | 78.49     | 79.02     | 63265   |
| date                        | 95.91     | 94.22     | 95.06     | 63662   |
| first_author                | 94.87     | 93.57     | 94.21     | 63265   |
| inTitle                     | 95.86     | 94.92     | 95.39     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.29     | 95.46     | 95.87     | 53375   |
| title                       | 90.37     | 90.98     | 90.67     | 62044   |
| volume                      | 97.9      | 98.42     | 98.16     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.75** | **92.19** | **92.47** | 429889  |
| all fields (macro avg.)     | 81.59     | 90.13     | 81.54     | 429889  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| authors                     | 79.69     | 78.62     | 79.16    | 63265   |
| date                        | 95.91     | 94.22     | 95.06    | 63662   |
| first_author                | 94.95     | 93.65     | 94.29    | 63265   |
| inTitle                     | 96.34     | 95.39     | 95.86    | 63213   |
| issue                       | 2.01      | 75        | 3.91     | 16      |
| page                        | 96.29     | 95.46     | 95.87    | 53375   |
| title                       | 96.04     | 96.69     | 96.36    | 62044   |
| volume                      | 97.9      | 98.42     | 98.16    | 61049   |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **93.68** | **93.12** | **93.4** | 429889  |
| all fields (macro avg.)     | 82.39     | 90.93     | 82.33    | 429889  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 93.38     | 92.13     | 92.75     | 63265   |
| date                        | 95.91     | 94.22     | 95.06     | 63662   |
| first_author                | 95.4      | 94.09     | 94.74     | 63265   |
| inTitle                     | 96.66     | 95.71     | 96.19     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.29     | 95.46     | 95.87     | 53375   |
| title                       | 97.71     | 98.37     | 98.04     | 62044   |
| volume                      | 97.9      | 98.42     | 98.16     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **96.04** | **95.46** | **95.75** | 429889  |
| all fields (macro avg.)     | 84.41     | 92.93     | 84.34     | 429889  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 86.86     | 85.69     | 86.27     | 63265   |
| date                        | 95.91     | 94.22     | 95.06     | 63662   |
| first_author                | 94.89     | 93.58     | 94.23     | 63265   |
| inTitle                     | 96.34     | 95.4      | 95.87     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.29     | 95.46     | 95.87     | 53375   |
| title                       | 97.59     | 98.25     | 97.91     | 62044   |
| volume                      | 97.9      | 98.42     | 98.16     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **94.95** | **94.38** | **94.66** | 429889  |
| all fields (macro avg.)     | 83.47     | 92        | 83.41     | 429889  |

#### Instance-level results

```
Total expected instances: 		63664
Total extracted instances: 		66156
Total correct instances: 		42523 (strict) 
Total correct instances: 		45375 (soft) 
Total correct instances: 		52987 (Levenshtein) 
Total correct instances: 		49617 (RatcliffObershelp) 

Instance-level precision:	64.28 (strict) 
Instance-level precision:	68.59 (soft) 
Instance-level precision:	80.09 (Levenshtein) 
Instance-level precision:	75 (RatcliffObershelp) 

Instance-level recall:	66.79	(strict) 
Instance-level recall:	71.27	(soft) 
Instance-level recall:	83.23	(Levenshtein) 
Instance-level recall:	77.94	(RatcliffObershelp) 

Instance-level f-score:	65.51 (strict) 
Instance-level f-score:	69.9 (soft) 
Instance-level f-score:	81.63 (Levenshtein) 
Instance-level f-score:	76.44 (RatcliffObershelp) 

Matching 1 :	58788

Matching 2 :	974

Matching 3 :	1238

Matching 4 :	366

Total matches :	61366
```

#### Citation context resolution

```

Total expected references: 	 63664 - 64.7 references per article
Total predicted references: 	 66156 - 67.23 references per article

Total expected citation contexts: 	 109022 - 110.79 citation contexts per article
Total predicted citation contexts: 	 99963 - 101.59 citation contexts per article

Total correct predicted citation contexts: 	 96279 - 97.84 citation contexts per article
Total wrong predicted citation contexts: 	 3684 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 96.31
Recall citation contexts: 	 88.31
fscore citation contexts: 	 92.14
```

## Fulltext structures

Fulltext structure contents are complicated to capture from JATS NLM files. They are often normalized and different from
the actual PDF content and are can be inconsistent from one document to another. The scores of the following metrics are
thus not very meaningful in absolute term, in particular for the strict matching (textual content of the srtructure can
be very long). As relative values for comparing different models, they seem however useful.

Evaluation on 984 random PDF files out of 982 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 29.37     | 27.86     | 28.6      | 585     |
| figure_title                | 0.07      | 0.02      | 0.03      | 31718   |
| funding_stmt                | 6.23      | 29.97     | 10.31     | 921     |
| reference_citation          | 57.09     | 55.97     | 56.52     | 108949  |
| reference_figure            | 58.42     | 51.02     | 54.47     | 68926   |
| reference_table             | 71.77     | 73.46     | 72.6      | 2381    |
| section_title               | 82.92     | 77.28     | 80        | 21831   |
| table_title                 | 0         | 0         | 0         | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **56.05** | **48.56** | **52.04** | 237236  |
| all fields (macro avg.)     | 38.23     | 39.45     | 37.82     | 237236  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 40.9      | 38.8      | 39.82     | 585     |
| figure_title                | 49.82     | 16.02     | 24.25     | 31718   |
| funding_stmt                | 6.23      | 29.97     | 10.31     | 921     |
| reference_citation          | 93.66     | 91.82     | 92.73     | 108949  |
| reference_figure            | 58.7      | 51.26     | 54.73     | 68926   |
| reference_table             | 71.85     | 73.54     | 72.69     | 2381    |
| section_title               | 83.96     | 78.24     | 81        | 21831   |
| table_title                 | 94.26     | 28.16     | 43.36     | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78**    | **67.58** | **72.42** | 237236  |
| all fields (macro avg.)     | 62.42     | 50.98     | 52.36     | 237236  |

**Document-level ratio results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 97.03     | 94.87     | 95.94     | 585     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **97.03** | **94.87** | **95.94** | 585     |
| all fields (macro avg.)     | 97.03     | 94.87     | 95.94     | 585     |

Evaluation metrics produced in 1329.179 seconds

