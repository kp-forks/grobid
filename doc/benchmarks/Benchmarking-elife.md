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
| abstract                    | 8.46      | 8.13      | 8.29      | 984     |
| authors                     | 65.57     | 64.9      | 65.24     | 983     |
| first_author                | 89.21     | 88.39     | 88.8      | 982     |
| title                       | 75.62     | 74.39     | 75        | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **60.05** | **58.94** | **59.49** | 3933    |
| all fields (macro avg.)     | 59.71     | 58.95     | 59.33     | 3933    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 21.14     | 20.33     | 20.73     | 984     |
| authors                     | 65.88     | 65.21     | 65.54     | 983     |
| first_author                | 89.21     | 88.39     | 88.8      | 982     |
| title                       | 82.54     | 81.2      | 81.86     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **64.97** | **63.77** | **64.37** | 3933    |
| all fields (macro avg.)     | 64.69     | 63.78     | 64.23     | 3933    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 46.41     | 44.61     | 45.49     | 984     |
| authors                     | 80.88     | 80.06     | 80.47     | 983     |
| first_author                | 89.62     | 88.8      | 89.21     | 982     |
| title                       | 89.77     | 88.31     | 89.04     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.87** | **75.44** | **76.15** | 3933    |
| all fields (macro avg.)     | 76.67     | 75.45     | 76.05     | 3933    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| abstract                    | 43.45     | 41.77     | 42.59    | 984     |
| authors                     | 70.91     | 70.19     | 70.55    | 983     |
| first_author                | 89.21     | 88.39     | 88.8     | 982     |
| title                       | 87.6      | 86.18     | 86.89    | 984     |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **72.98** | **71.62** | **72.3** | 3933    |
| all fields (macro avg.)     | 72.79     | 71.63     | 72.21    | 3933    |

#### Instance-level results

```
Total expected instances: 	984
Total correct instances: 	70 (strict) 
Total correct instances: 	185 (soft) 
Total correct instances: 	345 (Levenshtein) 
Total correct instances: 	292 (ObservedRatcliffObershelp) 

Instance-level recall:	7.11	(strict) 
Instance-level recall:	18.8	(soft) 
Instance-level recall:	35.06	(Levenshtein) 
Instance-level recall:	29.67	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 984 random PDF files out of 982 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| authors                     | 79.5      | 78.48     | 78.99    | 63265   |
| date                        | 95.94     | 94.3      | 95.11    | 63662   |
| first_author                | 94.88     | 93.64     | 94.26    | 63265   |
| inTitle                     | 95.85     | 94.98     | 95.41    | 63213   |
| issue                       | 2.01      | 75        | 3.91     | 16      |
| page                        | 96.31     | 95.57     | 95.93    | 53375   |
| title                       | 90.32     | 90.98     | 90.65    | 62044   |
| volume                      | 97.91     | 98.5      | 98.2     | 61049   |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **92.75** | **92.25** | **92.5** | 429889  |
| all fields (macro avg.)     | 81.59     | 90.18     | 81.56    | 429889  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 79.63     | 78.62     | 79.12     | 63265   |
| date                        | 95.94     | 94.3      | 95.11     | 63662   |
| first_author                | 94.96     | 93.72     | 94.34     | 63265   |
| inTitle                     | 96.34     | 95.45     | 95.89     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.31     | 95.57     | 95.93     | 53375   |
| title                       | 95.99     | 96.69     | 96.34     | 62044   |
| volume                      | 97.91     | 98.5      | 98.2      | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.68** | **93.17** | **93.43** | 429889  |
| all fields (macro avg.)     | 82.39     | 90.98     | 82.36     | 429889  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 93.38     | 92.19     | 92.78     | 63265   |
| date                        | 95.94     | 94.3      | 95.11     | 63662   |
| first_author                | 95.41     | 94.16     | 94.78     | 63265   |
| inTitle                     | 96.67     | 95.78     | 96.22     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.31     | 95.57     | 95.93     | 53375   |
| title                       | 97.72     | 98.44     | 98.08     | 62044   |
| volume                      | 97.91     | 98.5      | 98.2      | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **96.05** | **95.54** | **95.79** | 429889  |
| all fields (macro avg.)     | 84.42     | 92.99     | 84.38     | 429889  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 86.82     | 85.71     | 86.26     | 63265   |
| date                        | 95.94     | 94.3      | 95.11     | 63662   |
| first_author                | 94.9      | 93.65     | 94.27     | 63265   |
| inTitle                     | 96.34     | 95.46     | 95.9      | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.31     | 95.57     | 95.93     | 53375   |
| title                       | 97.57     | 98.28     | 97.92     | 62044   |
| volume                      | 97.91     | 98.5      | 98.2      | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **94.95** | **94.44** | **94.69** | 429889  |
| all fields (macro avg.)     | 83.47     | 92.06     | 83.44     | 429889  |

#### Instance-level results

```
Total expected instances: 		63664
Total extracted instances: 		65207
Total correct instances: 		42464 (strict) 
Total correct instances: 		45317 (soft) 
Total correct instances: 		52990 (Levenshtein) 
Total correct instances: 		49581 (RatcliffObershelp) 

Instance-level precision:	65.12 (strict) 
Instance-level precision:	69.5 (soft) 
Instance-level precision:	81.26 (Levenshtein) 
Instance-level precision:	76.04 (RatcliffObershelp) 

Instance-level recall:	66.7	(strict) 
Instance-level recall:	71.18	(soft) 
Instance-level recall:	83.23	(Levenshtein) 
Instance-level recall:	77.88	(RatcliffObershelp) 

Instance-level f-score:	65.9 (strict) 
Instance-level f-score:	70.33 (soft) 
Instance-level f-score:	82.24 (Levenshtein) 
Instance-level f-score:	76.95 (RatcliffObershelp) 

Matching 1 :	58787

Matching 2 :	1021

Matching 3 :	1251

Matching 4 :	361

Total matches :	61420
```

#### Citation context resolution

```

Total expected references: 	 63664 - 64.7 references per article
Total predicted references: 	 65207 - 66.27 references per article

Total expected citation contexts: 	 109022 - 110.79 citation contexts per article
Total predicted citation contexts: 	 100009 - 101.64 citation contexts per article

Total correct predicted citation contexts: 	 96268 - 97.83 citation contexts per article
Total wrong predicted citation contexts: 	 3741 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 96.26
Recall citation contexts: 	 88.3
fscore citation contexts: 	 92.11
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
| availability_stmt           | 25.53     | 26.84     | 26.17     | 585     |
| figure_title                | 0.07      | 0.02      | 0.03      | 31718   |
| funding_stmt                | 4.31      | 17.37     | 6.91      | 921     |
| reference_citation          | 57.1      | 55.98     | 56.53     | 108949  |
| reference_figure            | 58.41     | 51.06     | 54.49     | 68926   |
| reference_table             | 71.24     | 73.46     | 72.33     | 2381    |
| section_title               | 83.31     | 77.27     | 80.17     | 21831   |
| table_title                 | 0         | 0         | 0         | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **56.19** | **48.53** | **52.08** | 237236  |
| all fields (macro avg.)     | 37.5      | 37.75     | 37.08     | 237236  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 35.93     | 37.78     | 36.83     | 585     |
| figure_title                | 49.66     | 16.01     | 24.21     | 31718   |
| funding_stmt                | 4.31      | 17.37     | 6.91      | 921     |
| reference_citation          | 93.64     | 91.81     | 92.71     | 108949  |
| reference_figure            | 58.7      | 51.31     | 54.75     | 68926   |
| reference_table             | 71.32     | 73.54     | 72.42     | 2381    |
| section_title               | 84.35     | 78.23     | 81.18     | 21831   |
| table_title                 | 95.24     | 28.05     | 43.34     | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.2**  | **67.53** | **72.48** | 237236  |
| all fields (macro avg.)     | 61.64     | 49.26     | 51.54     | 237236  |

**Document-level ratio results**

| label                       | precision | recall  | f1       | support |
|-----------------------------|-----------|---------|----------|---------|
| availability_stmt           | 93.61     | 105.13  | 99.03    | 585     |
|                             |           |         |          |         |
| **all fields (micro avg.)** | **93.61** | **100** | **96.7** | 585     |
| all fields (macro avg.)     | 93.61     | 100     | 99.03    | 585     |

Evaluation metrics produced in 1279.917 seconds



