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
| abstract                    | 12.5      | 12.92     | 12.7      | 960     |
| authors                     | 98.97     | 98.97     | 98.97     | 969     |
| first_author                | 99.17     | 99.17     | 99.17     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 95.09     | 94.9      | 94.99     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.2**  | **76.78** | **76.49** | 3898    |
| all fields (macro avg.)     | 76.43     | 76.49     | 76.46     | 3898    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 48.49     | 50.1      | 49.28     | 960     |
| authors                     | 98.97     | 98.97     | 98.97     | 969     |
| first_author                | 99.17     | 99.17     | 99.17     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 98.7      | 98.5      | 98.6      | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **86.2**  | **86.87** | **86.53** | 3898    |
| all fields (macro avg.)     | 86.33     | 86.69     | 86.51     | 3898    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 70.97     | 73.33     | 72.13     | 960     |
| authors                     | 99.28     | 99.28     | 99.28     | 969     |
| first_author                | 99.28     | 99.28     | 99.28     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.4      | 99.2      | 99.3      | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.16** | **92.87** | **92.51** | 3898    |
| all fields (macro avg.)     | 92.23     | 92.77     | 92.5      | 3898    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 62.8      | 64.9      | 63.83     | 960     |
| authors                     | 99.17     | 99.17     | 99.17     | 969     |
| first_author                | 99.17     | 99.17     | 99.17     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.1      | 98.9      | 99        | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.97** | **90.66** | **90.31** | 3898    |
| all fields (macro avg.)     | 90.06     | 90.54     | 90.29     | 3898    |

#### Instance-level results

```
Total expected instances: 	1000
Total correct instances: 	116 (strict) 
Total correct instances: 	465 (soft) 
Total correct instances: 	684 (Levenshtein) 
Total correct instances: 	606 (ObservedRatcliffObershelp) 

Instance-level recall:	11.6	(strict) 
Instance-level recall:	46.5	(soft) 
Instance-level recall:	68.4	(Levenshtein) 
Instance-level recall:	60.6	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1000 random PDF files out of 998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.18     | 78.41     | 79.77     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 91.49     | 88.34     | 89.89     | 44770   |
| inTitle                     | 81.69     | 83.57     | 82.62     | 42795   |
| issue                       | 93.6      | 92.67     | 93.13     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 59.98     | 60.46     | 60.22     | 43101   |
| volume                      | 95.91     | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **84.24** | **81.44** | **82.82** | 321178  |
| all fields (macro avg.)     | 85.27     | 82.3      | 83.68     | 321178  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.49     | 78.72     | 80.08     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 91.71     | 88.55     | 90.1      | 44770   |
| inTitle                     | 85.53     | 87.49     | 86.5      | 42795   |
| issue                       | 93.6      | 92.67     | 93.13     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 91.99     | 92.74     | 92.36     | 43101   |
| volume                      | 95.91     | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.34** | **86.36** | **87.83** | 321178  |
| all fields (macro avg.)     | 89.82     | 86.89     | 88.25     | 321178  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 90.65     | 87.57     | 89.08     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 92.24     | 89.07     | 90.63     | 44770   |
| inTitle                     | 86.47     | 88.46     | 87.45     | 42795   |
| issue                       | 93.6      | 92.67     | 93.13     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 94.58     | 95.36     | 94.97     | 43101   |
| volume                      | 95.91     | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.19** | **88.15** | **89.64** | 321178  |
| all fields (macro avg.)     | 91.48     | 88.5      | 89.88     | 321178  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 84.94     | 82.05     | 83.47     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 91.49     | 88.34     | 89.89     | 44770   |
| inTitle                     | 85.18     | 87.14     | 86.15     | 42795   |
| issue                       | 93.6      | 92.67     | 93.13     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 93.97     | 94.74     | 94.35     | 43101   |
| volume                      | 95.91     | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.02** | **87.02** | **88.49** | 321178  |
| all fields (macro avg.)     | 90.43     | 87.48     | 88.85     | 321178  |

#### Instance-level results

```
Total expected instances: 		48449
Total extracted instances: 		48191
Total correct instances: 		13496 (strict) 
Total correct instances: 		22266 (soft) 
Total correct instances: 		24913 (Levenshtein) 
Total correct instances: 		23265 (RatcliffObershelp) 

Instance-level precision:	28.01 (strict) 
Instance-level precision:	46.2 (soft) 
Instance-level precision:	51.7 (Levenshtein) 
Instance-level precision:	48.28 (RatcliffObershelp) 

Instance-level recall:	27.86	(strict) 
Instance-level recall:	45.96	(soft) 
Instance-level recall:	51.42	(Levenshtein) 
Instance-level recall:	48.02	(RatcliffObershelp) 

Instance-level f-score:	27.93 (strict) 
Instance-level f-score:	46.08 (soft) 
Instance-level f-score:	51.56 (Levenshtein) 
Instance-level f-score:	48.15 (RatcliffObershelp) 

Matching 1 :	35368

Matching 2 :	1256

Matching 3 :	3269

Matching 4 :	1800

Total matches :	41693
```

#### Citation context resolution

```

Total expected references: 	 48449 - 48.45 references per article
Total predicted references: 	 48191 - 48.19 references per article

Total expected citation contexts: 	 69755 - 69.75 citation contexts per article
Total predicted citation contexts: 	 73271 - 73.27 citation contexts per article

Total correct predicted citation contexts: 	 56772 - 56.77 citation contexts per article
Total wrong predicted citation contexts: 	 16499 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 77.48
Recall citation contexts: 	 81.39
fscore citation contexts: 	 79.39
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
| availability_stmt           | 48.09     | 48.4      | 48.24     | 779     |
| conflict_stmt               | 78.89     | 63.72     | 70.5      | 962     |
| figure_title                | 0.23      | 0.11      | 0.15      | 8943    |
| funding_stmt                | 5.7       | 30.86     | 9.62      | 1507    |
| reference_citation          | 87.94     | 94.47     | 91.09     | 69741   |
| reference_figure            | 74.17     | 85.77     | 79.55     | 11010   |
| reference_table             | 70.2      | 94.3      | 80.49     | 5159    |
| section_title               | 72.78     | 66.2      | 69.34     | 17540   |
| table_title                 | 0         | 0         | 0         | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **74.31** | **76.62** | **75.45** | 121733  |
| all fields (macro avg.)     | 48.67     | 53.76     | 49.89     | 121733  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 74.11     | 74.58     | 74.34     | 779     |
| conflict_stmt               | 81.21     | 65.59     | 72.57     | 962     |
| figure_title                | 93.13     | 45.76     | 61.36     | 8943    |
| funding_stmt                | 7.29      | 39.48     | 12.31     | 1507    |
| reference_citation          | 87.94     | 94.48     | 91.09     | 69741   |
| reference_figure            | 74.41     | 86.05     | 79.81     | 11010   |
| reference_table             | 70.36     | 94.51     | 80.67     | 5159    |
| section_title               | 78.56     | 71.46     | 74.84     | 17540   |
| table_title                 | 53.15     | 7.47      | 13.1      | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.98** | **81.43** | **80.19** | 121733  |
| all fields (macro avg.)     | 68.91     | 64.38     | 62.23     | 121733  |

**Document-level ratio results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 99.12     | 100.64    | 99.87     | 779     |
| conflict_stmt               | 100       | 80.77     | 89.36     | 962     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **99.55** | **89.66** | **94.35** | 1741    |
| all fields (macro avg.)     | 99.56     | 90.71     | 94.62     | 1741    |

Evaluation metrics produced in 802.202 seconds




