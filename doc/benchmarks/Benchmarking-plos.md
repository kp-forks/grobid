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
| abstract                    | 12.6      | 13.02     | 12.81     | 960     |
| authors                     | 98.86     | 98.76     | 98.81     | 969     |
| first_author                | 99.17     | 99.07     | 99.12     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 94.88     | 94.6      | 94.74     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.13** | **76.65** | **76.39** | 3898    |
| all fields (macro avg.)     | 76.38     | 76.36     | 76.37     | 3898    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 48.29     | 49.9      | 49.08     | 960     |
| authors                     | 98.86     | 98.76     | 98.81     | 969     |
| first_author                | 99.17     | 99.07     | 99.12     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 98.5      | 98.2      | 98.35     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **86.06** | **86.66** | **86.36** | 3898    |
| all fields (macro avg.)     | 86.2      | 86.48     | 86.34     | 3898    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 69.66     | 71.98     | 70.8      | 960     |
| authors                     | 99.28     | 99.17     | 99.23     | 969     |
| first_author                | 99.28     | 99.17     | 99.23     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.1      | 98.8      | 98.95     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.75** | **92.38** | **92.06** | 3898    |
| all fields (macro avg.)     | 91.83     | 92.28     | 92.05     | 3898    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 62.4      | 64.48     | 63.42     | 960     |
| authors                     | 99.17     | 99.07     | 99.12     | 969     |
| first_author                | 99.17     | 99.07     | 99.12     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 98.8      | 98.5      | 98.65     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.78** | **90.41** | **90.09** | 3898    |
| all fields (macro avg.)     | 89.89     | 90.28     | 90.08     | 3898    |

#### Instance-level results

```
Total expected instances: 	1000
Total correct instances: 	119 (strict) 
Total correct instances: 	468 (soft) 
Total correct instances: 	676 (Levenshtein) 
Total correct instances: 	608 (ObservedRatcliffObershelp) 

Instance-level recall:	11.9	(strict) 
Instance-level recall:	46.8	(soft) 
Instance-level recall:	67.6	(Levenshtein) 
Instance-level recall:	60.8	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1000 random PDF files out of 998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.19     | 78.43     | 79.78     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 91.49     | 88.35     | 89.89     | 44770   |
| inTitle                     | 81.69     | 83.57     | 82.62     | 42795   |
| issue                       | 93.59     | 92.66     | 93.12     | 18983   |
| page                        | 93.71     | 77.57     | 84.88     | 40844   |
| title                       | 59.97     | 60.46     | 60.21     | 43101   |
| volume                      | 95.9      | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **84.24** | **81.44** | **82.82** | 321178  |
| all fields (macro avg.)     | 85.27     | 82.3      | 83.68     | 321178  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.51     | 78.73     | 80.09     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 91.71     | 88.56     | 90.11     | 44770   |
| inTitle                     | 85.53     | 87.5      | 86.5      | 42795   |
| issue                       | 93.59     | 92.66     | 93.12     | 18983   |
| page                        | 93.71     | 77.57     | 84.88     | 40844   |
| title                       | 91.98     | 92.74     | 92.36     | 43101   |
| volume                      | 95.9      | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.34** | **86.37** | **87.83** | 321178  |
| all fields (macro avg.)     | 89.82     | 86.89     | 88.25     | 321178  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 90.66     | 87.57     | 89.09     | 44770   |
| date                        | 84.63     | 81.24     | 82.9      | 45457   |
| first_author                | 92.25     | 89.08     | 90.64     | 44770   |
| inTitle                     | 86.47     | 88.46     | 87.46     | 42795   |
| issue                       | 93.59     | 92.66     | 93.12     | 18983   |
| page                        | 93.71     | 77.57     | 84.88     | 40844   |
| title                       | 94.59     | 95.36     | 94.97     | 43101   |
| volume                      | 95.9      | 96.1      | 96        | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.19** | **88.15** | **89.64** | 321178  |
| all fields (macro avg.)     | 91.48     | 88.51     | 89.88     | 321178  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| authors                     | 84.95     | 82.06     | 83.48    | 44770   |
| date                        | 84.63     | 81.24     | 82.9     | 45457   |
| first_author                | 91.49     | 88.35     | 89.89    | 44770   |
| inTitle                     | 85.18     | 87.14     | 86.15    | 42795   |
| issue                       | 93.59     | 92.66     | 93.12    | 18983   |
| page                        | 93.71     | 77.57     | 84.88    | 40844   |
| title                       | 93.97     | 94.74     | 94.35    | 43101   |
| volume                      | 95.9      | 96.1      | 96       | 40458   |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **90.02** | **87.02** | **88.5** | 321178  |
| all fields (macro avg.)     | 90.43     | 87.48     | 88.85    | 321178  |

#### Instance-level results

```
Total expected instances: 		48449
Total extracted instances: 		48184
Total correct instances: 		13498 (strict) 
Total correct instances: 		22269 (soft) 
Total correct instances: 		24917 (Levenshtein) 
Total correct instances: 		23269 (RatcliffObershelp) 

Instance-level precision:	28.01 (strict) 
Instance-level precision:	46.22 (soft) 
Instance-level precision:	51.71 (Levenshtein) 
Instance-level precision:	48.29 (RatcliffObershelp) 

Instance-level recall:	27.86	(strict) 
Instance-level recall:	45.96	(soft) 
Instance-level recall:	51.43	(Levenshtein) 
Instance-level recall:	48.03	(RatcliffObershelp) 

Instance-level f-score:	27.94 (strict) 
Instance-level f-score:	46.09 (soft) 
Instance-level f-score:	51.57 (Levenshtein) 
Instance-level f-score:	48.16 (RatcliffObershelp) 

Matching 1 :	35369

Matching 2 :	1258

Matching 3 :	3267

Matching 4 :	1799

Total matches :	41693
```

#### Citation context resolution

```

Total expected references: 	 48449 - 48.45 references per article
Total predicted references: 	 48184 - 48.18 references per article

Total expected citation contexts: 	 69755 - 69.75 citation contexts per article
Total predicted citation contexts: 	 73318 - 73.32 citation contexts per article

Total correct predicted citation contexts: 	 56820 - 56.82 citation contexts per article
Total wrong predicted citation contexts: 	 16498 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 77.5
Recall citation contexts: 	 81.46
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
| availability_stmt           | 48.98     | 49.17     | 49.07     | 779     |
| conflict_stmt               | 83.76     | 67.57     | 74.8      | 962     |
| figure_title                | 0.18      | 0.09      | 0.12      | 8943    |
| funding_stmt                | 5.82      | 31.39     | 9.81      | 1507    |
| reference_citation          | 87.94     | 94.55     | 91.13     | 69741   |
| reference_figure            | 74.12     | 85.79     | 79.53     | 11010   |
| reference_table             | 70.21     | 94.34     | 80.51     | 5159    |
| section_title               | 72.96     | 66.27     | 69.45     | 17540   |
| table_title                 | 0         | 0         | 0         | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **74.4**  | **76.72** | **75.54** | 121733  |
| all fields (macro avg.)     | 49.33     | 54.35     | 50.49     | 121733  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 78.13     | 78.43     | 78.28     | 779     |
| conflict_stmt               | 86.86     | 70.06     | 77.56     | 962     |
| figure_title                | 93.24     | 45.79     | 61.42     | 8943    |
| funding_stmt                | 7.41      | 40.01     | 12.51     | 1507    |
| reference_citation          | 87.95     | 94.55     | 91.13     | 69741   |
| reference_figure            | 74.36     | 86.08     | 79.79     | 11010   |
| reference_table             | 70.37     | 94.55     | 80.69     | 5159    |
| section_title               | 78.76     | 71.53     | 74.97     | 17540   |
| table_title                 | 53.02     | 7.49      | 13.12     | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **79.09** | **81.56** | **80.31** | 121733  |
| all fields (macro avg.)     | 70.01     | 65.39     | 63.27     | 121733  |

**Document-level ratio results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 99.49     | 100.39    | 99.94     | 779     |
| conflict_stmt               | 100       | 80.67     | 89.3      | 962     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **99.74** | **89.49** | **94.34** | 1741    |
| all fields (macro avg.)     | 99.75     | 90.53     | 94.62     | 1741    |

Evaluation metrics produced in 776.494 seconds





