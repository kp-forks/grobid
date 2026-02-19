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
| abstract                    | 9.33      | 8.94      | 9.13      | 984     |
| authors                     | 75.1      | 74.57     | 74.83     | 983     |
| first_author                | 93.34     | 92.77     | 93.05     | 982     |
| title                       | 88.74     | 87.3      | 88.01     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **67.07** | **65.88** | **66.47** | 3933    |
| all fields (macro avg.)     | 66.63     | 65.89     | 66.26     | 3933    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 22.38     | 21.44     | 21.9      | 984     |
| authors                     | 75.51     | 74.97     | 75.24     | 983     |
| first_author                | 93.34     | 92.77     | 93.05     | 982     |
| title                       | 95.76     | 94.21     | 94.98     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **72.12** | **70.84** | **71.47** | 3933    |
| all fields (macro avg.)     | 71.75     | 70.85     | 71.29     | 3933    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 47.19     | 45.22     | 46.19     | 984     |
| authors                     | 87.6      | 86.98     | 87.29     | 983     |
| first_author                | 93.65     | 93.08     | 93.36     | 982     |
| title                       | 97.31     | 95.73     | 96.52     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **81.7**  | **80.24** | **80.96** | 3933    |
| all fields (macro avg.)     | 81.44     | 80.25     | 80.84     | 3933    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 44.33     | 42.48     | 43.38     | 984     |
| authors                     | 80.43     | 79.86     | 80.14     | 983     |
| first_author                | 93.34     | 92.77     | 93.05     | 982     |
| title                       | 97.21     | 95.63     | 96.41     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **79.08** | **77.68** | **78.37** | 3933    |
| all fields (macro avg.)     | 78.83     | 77.68     | 78.25     | 3933    |

#### Instance-level results

```
Total expected instances: 	984
Total correct instances: 	76 (strict) 
Total correct instances: 	203 (soft) 
Total correct instances: 	382 (Levenshtein) 
Total correct instances: 	332 (ObservedRatcliffObershelp) 

Instance-level recall:	7.72	(strict) 
Instance-level recall:	20.63	(soft) 
Instance-level recall:	38.82	(Levenshtein) 
Instance-level recall:	33.74	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 984 random PDF files out of 982 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 79.62     | 78.6     | 79.1      | 63265   |
| date                        | 95.96     | 94.32    | 95.13     | 63662   |
| first_author                | 94.94     | 93.69    | 94.31     | 63265   |
| inTitle                     | 95.9      | 95.02    | 95.46     | 63213   |
| issue                       | 2.01      | 75       | 3.91      | 16      |
| page                        | 96.31     | 95.58    | 95.95     | 53375   |
| title                       | 90.41     | 91.08    | 90.75     | 62044   |
| volume                      | 97.94     | 98.53    | 98.23     | 61049   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **92.8**  | **92.3** | **92.55** | 429889  |
| all fields (macro avg.)     | 81.64     | 90.23    | 81.61     | 429889  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 79.75     | 78.73     | 79.24     | 63265   |
| date                        | 95.96     | 94.32     | 95.13     | 63662   |
| first_author                | 95.02     | 93.77     | 94.39     | 63265   |
| inTitle                     | 96.39     | 95.49     | 95.94     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.31     | 95.58     | 95.95     | 53375   |
| title                       | 96.09     | 96.8      | 96.44     | 62044   |
| volume                      | 97.94     | 98.53     | 98.23     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.73** | **93.23** | **93.48** | 429889  |
| all fields (macro avg.)     | 82.43     | 91.03     | 82.4      | 429889  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 93.45     | 92.26     | 92.85     | 63265   |
| date                        | 95.96     | 94.32     | 95.13     | 63662   |
| first_author                | 95.47     | 94.22     | 94.84     | 63265   |
| inTitle                     | 96.71     | 95.82     | 96.26     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.31     | 95.58     | 95.95     | 53375   |
| title                       | 97.74     | 98.46     | 98.1      | 62044   |
| volume                      | 97.94     | 98.53     | 98.23     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **96.09** | **95.57** | **95.83** | 429889  |
| all fields (macro avg.)     | 84.45     | 93.02     | 84.41     | 429889  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 86.92     | 85.81     | 86.36     | 63265   |
| date                        | 95.96     | 94.32     | 95.13     | 63662   |
| first_author                | 94.96     | 93.71     | 94.33     | 63265   |
| inTitle                     | 96.39     | 95.5      | 95.94     | 63213   |
| issue                       | 2.01      | 75        | 3.91      | 16      |
| page                        | 96.31     | 95.58     | 95.95     | 53375   |
| title                       | 97.62     | 98.34     | 97.98     | 62044   |
| volume                      | 97.94     | 98.53     | 98.23     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **95**    | **94.49** | **94.74** | 429889  |
| all fields (macro avg.)     | 83.51     | 92.1      | 83.48     | 429889  |

#### Instance-level results

```
Total expected instances: 		63664
Total extracted instances: 		65198
Total correct instances: 		42585 (strict) 
Total correct instances: 		45443 (soft) 
Total correct instances: 		53068 (Levenshtein) 
Total correct instances: 		49691 (RatcliffObershelp) 

Instance-level precision:	65.32 (strict) 
Instance-level precision:	69.7 (soft) 
Instance-level precision:	81.4 (Levenshtein) 
Instance-level precision:	76.22 (RatcliffObershelp) 

Instance-level recall:	66.89	(strict) 
Instance-level recall:	71.38	(soft) 
Instance-level recall:	83.36	(Levenshtein) 
Instance-level recall:	78.05	(RatcliffObershelp) 

Instance-level f-score:	66.09 (strict) 
Instance-level f-score:	70.53 (soft) 
Instance-level f-score:	82.36 (Levenshtein) 
Instance-level f-score:	77.12 (RatcliffObershelp) 

Matching 1 :	58856

Matching 2 :	972

Matching 3 :	1239

Matching 4 :	361

Total matches :	61428
```

#### Citation context resolution

```

Total expected references: 	 63664 - 64.7 references per article
Total predicted references: 	 65198 - 66.26 references per article

Total expected citation contexts: 	 109022 - 110.79 citation contexts per article
Total predicted citation contexts: 	 99989 - 101.61 citation contexts per article

Total correct predicted citation contexts: 	 96318 - 97.88 citation contexts per article
Total wrong predicted citation contexts: 	 3671 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 96.33
Recall citation contexts: 	 88.35
fscore citation contexts: 	 92.17
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
| availability_stmt           | 25.73     | 27.01     | 26.36     | 585     |
| figure_title                | 0.07      | 0.02      | 0.03      | 31718   |
| funding_stmt                | 7.63      | 31.6      | 12.29     | 921     |
| reference_citation          | 57.13     | 55.99     | 56.55     | 108949  |
| reference_figure            | 58.41     | 51.07     | 54.49     | 68926   |
| reference_table             | 71.24     | 73.46     | 72.33     | 2381    |
| section_title               | 83.33     | 77.3      | 80.21     | 21831   |
| table_title                 | 0         | 0         | 0         | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **56.24** | **48.59** | **52.14** | 237236  |
| all fields (macro avg.)     | 37.94     | 39.56     | 37.78     | 237236  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 36.32     | 38.12     | 37.2      | 585     |
| figure_title                | 49.77     | 16.05     | 24.27     | 31718   |
| funding_stmt                | 7.63      | 31.6      | 12.29     | 921     |
| reference_citation          | 93.7      | 91.83     | 92.75     | 108949  |
| reference_figure            | 58.7      | 51.32     | 54.76     | 68926   |
| reference_table             | 71.32     | 73.54     | 72.42     | 2381    |
| section_title               | 84.38     | 78.27     | 81.21     | 21831   |
| table_title                 | 95.08     | 28.1      | 43.38     | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.26** | **67.61** | **72.55** | 237236  |
| all fields (macro avg.)     | 62.11     | 51.1      | 52.29     | 237236  |

**Document-level ratio results**

| label                       | precision | recall  | f1        | support |
|-----------------------------|-----------|---------|-----------|---------|
| availability_stmt           | 93.74     | 104.96  | 99.03     | 585     |
|                             |           |         |           |         |
| **all fields (micro avg.)** | **93.74** | **100** | **96.77** | 585     |
| all fields (macro avg.)     | 93.74     | 100     | 99.03     | 585     |

Evaluation metrics produced in 1255.899 seconds
