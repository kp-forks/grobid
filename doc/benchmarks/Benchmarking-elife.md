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

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| abstract                    | 8.05      | 7.83      | 7.94     | 984     |
| authors                     | 84.58     | 83.72     | 84.15    | 983     |
| first_author                | 94.14     | 93.28     | 93.71    | 982     |
| title                       | 90.02     | 88.01     | 89       | 984     |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **69.41** | **68.19** | **68.8** | 3933    |
| all fields (macro avg.)     | 69.2      | 68.21     | 68.7     | 3933    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 19.98     | 19.41     | 19.69     | 984     |
| authors                     | 84.79     | 83.93     | 84.36     | 983     |
| first_author                | 94.14     | 93.28     | 93.71     | 982     |
| title                       | 95.63     | 93.5      | 94.55     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **73.81** | **72.51** | **73.16** | 3933    |
| all fields (macro avg.)     | 73.64     | 72.53     | 73.08     | 3933    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 46.13     | 44.82     | 45.46     | 984     |
| authors                     | 90.13     | 89.22     | 89.67     | 983     |
| first_author                | 94.24     | 93.38     | 93.81     | 982     |
| title                       | 96.67     | 94.51     | 95.58     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **81.91** | **80.47** | **81.19** | 3933    |
| all fields (macro avg.)     | 81.8      | 80.48     | 81.13     | 3933    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 43.2      | 41.97     | 42.58     | 984     |
| authors                     | 86.95     | 86.06     | 86.5      | 983     |
| first_author                | 94.14     | 93.28     | 93.71     | 982     |
| title                       | 96.26     | 94.11     | 95.17     | 984     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **80.25** | **78.85** | **79.54** | 3933    |
| all fields (macro avg.)     | 80.14     | 78.85     | 79.49     | 3933    |

#### Instance-level results

```
Total expected instances: 	984
Total correct instances: 	68 (strict) 
Total correct instances: 	185 (soft) 
Total correct instances: 	395 (Levenshtein) 
Total correct instances: 	361 (ObservedRatcliffObershelp) 

Instance-level recall:	6.91	(strict) 
Instance-level recall:	18.8	(soft) 
Instance-level recall:	40.14	(Levenshtein) 
Instance-level recall:	36.69	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 984 random PDF files out of 982 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 79.51     | 78.45     | 78.97     | 63265   |
| date                        | 95.95     | 94.26     | 95.09     | 63662   |
| first_author                | 94.9      | 93.59     | 94.24     | 63265   |
| inTitle                     | 95.87     | 94.93     | 95.4      | 63213   |
| issue                       | 2.01      | 75        | 3.92      | 16      |
| page                        | 96.3      | 95.51     | 95.9      | 53375   |
| title                       | 90.33     | 90.95     | 90.64     | 62044   |
| volume                      | 97.93     | 98.46     | 98.19     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.76** | **92.21** | **92.48** | 429889  |
| all fields (macro avg.)     | 81.6      | 90.14     | 81.54     | 429889  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 79.64     | 78.58     | 79.11     | 63265   |
| date                        | 95.95     | 94.26     | 95.09     | 63662   |
| first_author                | 94.98     | 93.67     | 94.32     | 63265   |
| inTitle                     | 96.35     | 95.41     | 95.88     | 63213   |
| issue                       | 2.01      | 75        | 3.92      | 16      |
| page                        | 96.3      | 95.51     | 95.9      | 53375   |
| title                       | 96        | 96.66     | 96.33     | 62044   |
| volume                      | 97.93     | 98.46     | 98.19     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.69** | **93.13** | **93.41** | 429889  |
| all fields (macro avg.)     | 82.39     | 90.94     | 82.34     | 429889  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 93.39     | 92.14     | 92.76     | 63265   |
| date                        | 95.95     | 94.26     | 95.09     | 63662   |
| first_author                | 95.42     | 94.12     | 94.77     | 63265   |
| inTitle                     | 96.68     | 95.74     | 96.21     | 63213   |
| issue                       | 2.01      | 75        | 3.92      | 16      |
| page                        | 96.3      | 95.51     | 95.9      | 53375   |
| title                       | 97.73     | 98.4      | 98.06     | 62044   |
| volume                      | 97.93     | 98.46     | 98.19     | 61049   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **96.06** | **95.49** | **95.78** | 429889  |
| all fields (macro avg.)     | 84.43     | 92.95     | 84.36     | 429889  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 86.83     | 85.67    | 86.24     | 63265   |
| date                        | 95.95     | 94.26    | 95.09     | 63662   |
| first_author                | 94.91     | 93.61    | 94.25     | 63265   |
| inTitle                     | 96.36     | 95.42    | 95.89     | 63213   |
| issue                       | 2.01      | 75       | 3.92      | 16      |
| page                        | 96.3      | 95.51    | 95.9      | 53375   |
| title                       | 97.58     | 98.25    | 97.91     | 62044   |
| volume                      | 97.93     | 98.46    | 98.19     | 61049   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **94.96** | **94.4** | **94.68** | 429889  |
| all fields (macro avg.)     | 83.48     | 92.02    | 83.43     | 429889  |

#### Instance-level results

```
Total expected instances: 		63664
Total extracted instances: 		65159
Total correct instances: 		42449 (strict) 
Total correct instances: 		45299 (soft) 
Total correct instances: 		52965 (Levenshtein) 
Total correct instances: 		49558 (RatcliffObershelp) 

Instance-level precision:	65.15 (strict) 
Instance-level precision:	69.52 (soft) 
Instance-level precision:	81.29 (Levenshtein) 
Instance-level precision:	76.06 (RatcliffObershelp) 

Instance-level recall:	66.68	(strict) 
Instance-level recall:	71.15	(soft) 
Instance-level recall:	83.19	(Levenshtein) 
Instance-level recall:	77.84	(RatcliffObershelp) 

Instance-level f-score:	65.9 (strict) 
Instance-level f-score:	70.33 (soft) 
Instance-level f-score:	82.23 (Levenshtein) 
Instance-level f-score:	76.94 (RatcliffObershelp) 

Matching 1 :	58768

Matching 2 :	1012

Matching 3 :	1249

Matching 4 :	363

Total matches :	61392
```

#### Citation context resolution

```

Total expected references: 	 63664 - 64.7 references per article
Total predicted references: 	 65159 - 66.22 references per article

Total expected citation contexts: 	 109022 - 110.79 citation contexts per article
Total predicted citation contexts: 	 99969 - 101.59 citation contexts per article

Total correct predicted citation contexts: 	 96267 - 97.83 citation contexts per article
Total wrong predicted citation contexts: 	 3702 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 96.3
Recall citation contexts: 	 88.3
fscore citation contexts: 	 92.13
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
| availability_stmt           | 25.53     | 27.01     | 26.25     | 585     |
| figure_title                | 0.09      | 0.03      | 0.04      | 31718   |
| funding_stmt                | 3.18      | 14.77     | 5.24      | 921     |
| reference_citation          | 57.11     | 55.98     | 56.54     | 108949  |
| reference_figure            | 58.42     | 51.05     | 54.48     | 68926   |
| reference_table             | 70.84     | 73.46     | 72.12     | 2381    |
| section_title               | 83.34     | 77.34     | 80.23     | 21831   |
| table_title                 | 0         | 0         | 0         | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **56.03** | **48.52** | **52.01** | 237236  |
| all fields (macro avg.)     | 37.31     | 37.45     | 36.86     | 237236  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 36.19     | 38.29     | 37.21     | 585     |
| figure_title                | 49.65     | 16.02     | 24.23     | 31718   |
| funding_stmt                | 3.18      | 14.77     | 5.24      | 921     |
| reference_citation          | 93.67     | 91.82     | 92.74     | 108949  |
| reference_figure            | 58.7      | 51.3      | 54.75     | 68926   |
| reference_table             | 70.92     | 73.54     | 72.21     | 2381    |
| section_title               | 84.38     | 78.31     | 81.23     | 21831   |
| table_title                 | 95.38     | 27.9      | 43.17     | 1925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **77.99** | **67.54** | **72.39** | 237236  |
| all fields (macro avg.)     | 61.51     | 48.99     | 51.35     | 237236  |

**Document-level ratio results**

| label                       | precision | recall  | f1        | support |
|-----------------------------|-----------|---------|-----------|---------|
| availability_stmt           | 93.36     | 105.81  | 99.2      | 585     |
|                             |           |         |           |         |
| **all fields (micro avg.)** | **93.36** | **100** | **96.57** | 585     |
| all fields (macro avg.)     | 93.36     | 100     | 99.2      | 585     |

Evaluation metrics produced in 1289.467 seconds


