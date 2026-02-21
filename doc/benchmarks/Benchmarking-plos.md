# Benchmarking PLOS

## General

This is the end-to-end benchmarking result for GROBID version **0.8.2** against the `PLOS` test set, see
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

Evaluation on 1000 PDF preprints out of 1000 (no failure).

Runtime for processing 1000 PDF: **999** seconds, (0.99 seconds per PDF) on Ubuntu 22.04, 16 CPU (32 threads), 128GB RAM
and with a GeForce GTX 1080 Ti GPU.

Note: with CRF only models runtime is 304s (0.30 seconds per PDF) with 4 CPU, 8 threads.

## Header metadata

Evaluation on 1000 random PDF files out of 998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 13.12     | 13.44     | 13.28     | 960     |
| authors                     | 98.97     | 98.97     | 98.97     | 969     |
| first_author                | 99.17     | 99.17     | 99.17     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 95.55     | 94.5      | 95.02     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.57** | **76.81** | **76.69** | 3898    |
| all fields (macro avg.)     | 76.7      | 76.52     | 76.61     | 3898    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 49.64     | 50.83     | 50.23     | 960     |
| authors                     | 98.97     | 98.97     | 98.97     | 969     |
| first_author                | 99.17     | 99.17     | 99.17     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.19     | 98.1      | 98.64     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **86.68** | **86.94** | **86.81** | 3898    |
| all fields (macro avg.)     | 86.74     | 86.77     | 86.75     | 3898    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 75.79     | 77.6      | 76.69     | 960     |
| authors                     | 99.38     | 99.38     | 99.38     | 969     |
| first_author                | 99.28     | 99.28     | 99.28     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.6      | 98.5      | 99.04     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.48** | **93.77** | **93.62** | 3898    |
| all fields (macro avg.)     | 93.51     | 93.69     | 93.6      | 3898    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 65.41     | 66.98     | 66.19     | 960     |
| authors                     | 99.28     | 99.28     | 99.28     | 969     |
| first_author                | 99.17     | 99.17     | 99.17     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.39     | 98.3      | 98.84     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.77** | **91.05** | **90.91** | 3898    |
| all fields (macro avg.)     | 90.81     | 90.93     | 90.87     | 3898    |

#### Instance-level results

```
Total expected instances: 	1000
Total correct instances: 	128 (strict) 
Total correct instances: 	486 (soft) 
Total correct instances: 	740 (Levenshtein) 
Total correct instances: 	643 (ObservedRatcliffObershelp) 

Instance-level recall:	12.8	(strict) 
Instance-level recall:	48.6	(soft) 
Instance-level recall:	74	(Levenshtein) 
Instance-level recall:	64.3	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1000 random PDF files out of 998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.21     | 78.45     | 79.8      | 44770   |
| date                        | 84.64     | 81.25     | 82.91     | 45457   |
| first_author                | 91.5      | 88.36     | 89.9      | 44770   |
| inTitle                     | 81.71     | 83.59     | 82.64     | 42795   |
| issue                       | 93.6      | 92.69     | 93.14     | 18983   |
| page                        | 93.72     | 77.58     | 84.89     | 40844   |
| title                       | 60.01     | 60.5      | 60.25     | 43101   |
| volume                      | 95.91     | 96.12     | 96.01     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **84.26** | **81.46** | **82.83** | 321178  |
| all fields (macro avg.)     | 85.29     | 82.32     | 83.69     | 321178  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.52     | 78.75     | 80.11     | 44770   |
| date                        | 84.64     | 81.25     | 82.91     | 45457   |
| first_author                | 91.71     | 88.57     | 90.11     | 44770   |
| inTitle                     | 85.55     | 87.51     | 86.52     | 42795   |
| issue                       | 93.6      | 92.69     | 93.14     | 18983   |
| page                        | 93.72     | 77.58     | 84.89     | 40844   |
| title                       | 92.04     | 92.8      | 92.42     | 43101   |
| volume                      | 95.91     | 96.12     | 96.01     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.36** | **86.39** | **87.85** | 321178  |
| all fields (macro avg.)     | 89.84     | 86.91     | 88.26     | 321178  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 90.68     | 87.6      | 89.11     | 44770   |
| date                        | 84.64     | 81.25     | 82.91     | 45457   |
| first_author                | 92.26     | 89.09     | 90.65     | 44770   |
| inTitle                     | 86.49     | 88.48     | 87.47     | 42795   |
| issue                       | 93.6      | 92.69     | 93.14     | 18983   |
| page                        | 93.72     | 77.58     | 84.89     | 40844   |
| title                       | 94.6      | 95.38     | 94.99     | 43101   |
| volume                      | 95.91     | 96.12     | 96.01     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.2**  | **88.17** | **89.66** | 321178  |
| all fields (macro avg.)     | 91.49     | 88.52     | 89.9      | 321178  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 84.97     | 82.08     | 83.5      | 44770   |
| date                        | 84.64     | 81.25     | 82.91     | 45457   |
| first_author                | 91.5      | 88.36     | 89.9      | 44770   |
| inTitle                     | 85.2      | 87.16     | 86.17     | 42795   |
| issue                       | 93.6      | 92.69     | 93.14     | 18983   |
| page                        | 93.72     | 77.58     | 84.89     | 40844   |
| title                       | 94        | 94.77     | 94.38     | 43101   |
| volume                      | 95.91     | 96.12     | 96.01     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.03** | **87.04** | **88.51** | 321178  |
| all fields (macro avg.)     | 90.44     | 87.5      | 88.86     | 321178  |

#### Instance-level results

```
Total expected instances: 		48449
Total extracted instances: 		48186
Total correct instances: 		13506 (strict) 
Total correct instances: 		22287 (soft) 
Total correct instances: 		24923 (Levenshtein) 
Total correct instances: 		23279 (RatcliffObershelp) 

Instance-level precision:	28.03 (strict) 
Instance-level precision:	46.25 (soft) 
Instance-level precision:	51.72 (Levenshtein) 
Instance-level precision:	48.31 (RatcliffObershelp) 

Instance-level recall:	27.88	(strict) 
Instance-level recall:	46	(soft) 
Instance-level recall:	51.44	(Levenshtein) 
Instance-level recall:	48.05	(RatcliffObershelp) 

Instance-level f-score:	27.95 (strict) 
Instance-level f-score:	46.13 (soft) 
Instance-level f-score:	51.58 (Levenshtein) 
Instance-level f-score:	48.18 (RatcliffObershelp) 

Matching 1 :	35393

Matching 2 :	1243

Matching 3 :	3263

Matching 4 :	1800

Total matches :	41699
```

#### Citation context resolution

```

Total expected references: 	 48449 - 48.45 references per article
Total predicted references: 	 48186 - 48.19 references per article

Total expected citation contexts: 	 69755 - 69.75 citation contexts per article
Total predicted citation contexts: 	 73309 - 73.31 citation contexts per article

Total correct predicted citation contexts: 	 56815 - 56.81 citation contexts per article
Total wrong predicted citation contexts: 	 16494 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 77.5
Recall citation contexts: 	 81.45
fscore citation contexts: 	 79.43
```

## Fulltext structures

Fulltext structure contents are complicated to capture from JATS NLM files. They are often normalized and different from
the actual PDF content and are can be inconsistent from one document to another. The scores of the following metrics are
thus not very meaningful in absolute term, in particular for the strict matching (textual content of the srtructure can
be very long). As relative values for comparing different models, they seem however useful.

Evaluation on 1000 random PDF files out of 998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 57.22     | 57.51     | 57.36     | 779     |
| conflict_stmt               | 91.23     | 90.85     | 91.04     | 962     |
| figure_title                | 0.18      | 0.09      | 0.12      | 8943    |
| funding_stmt                | 5.87      | 31.59     | 9.91      | 1507    |
| reference_citation          | 87.95     | 94.54     | 91.13     | 69741   |
| reference_figure            | 74.12     | 85.8      | 79.53     | 11010   |
| reference_table             | 70.21     | 94.34     | 80.51     | 5159    |
| section_title               | 73        | 66.28     | 69.48     | 17540   |
| table_title                 | 0         | 0         | 0         | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **74.55** | **76.95** | **75.73** | 121733  |
| all fields (macro avg.)     | 51.09     | 57.89     | 53.23     | 121733  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 85.06     | 85.49     | 85.28     | 779     |
| conflict_stmt               | 94.36     | 93.97     | 94.17     | 962     |
| figure_title                | 93.24     | 45.82     | 61.45     | 8943    |
| funding_stmt                | 7.38      | 39.68     | 12.44     | 1507    |
| reference_citation          | 87.96     | 94.54     | 91.13     | 69741   |
| reference_figure            | 74.36     | 86.09     | 79.79     | 11010   |
| reference_table             | 70.37     | 94.55     | 80.69     | 5159    |
| section_title               | 78.81     | 71.56     | 75.01     | 17540   |
| table_title                 | 53.02     | 7.49      | 13.12     | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **79.23** | **81.79** | **80.49** | 121733  |
| all fields (macro avg.)     | 71.62     | 68.8      | 65.9      | 121733  |

**Document-level ratio results**

| label                       | precision | recall  | f1        | support |
|-----------------------------|-----------|---------|-----------|---------|
| availability_stmt           | 99.49     | 100.51  | 100       | 779     |
| conflict_stmt               | 99.9      | 99.58   | 99.74     | 962     |
|                             |           |         |           |         |
| **all fields (micro avg.)** | **99.71** | **100** | **99.86** | 1741    |
| all fields (macro avg.)     | 99.69     | 100     | 99.87     | 1741    |

Evaluation metrics produced in 805.05 seconds
