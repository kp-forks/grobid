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
| abstract                    | 13.33     | 13.33     | 13.33     | 960     |
| authors                     | 99.07     | 99.07     | 99.07     | 969     |
| first_author                | 99.28     | 99.28     | 99.28     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 95.97     | 95.3      | 95.63     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **77.18** | **77.04** | **77.11** | 3898    |
| all fields (macro avg.)     | 76.91     | 76.75     | 76.83     | 3898    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| abstract                    | 50.52     | 50.52     | 50.52    | 960     |
| authors                     | 99.07     | 99.07     | 99.07    | 969     |
| first_author                | 99.28     | 99.28     | 99.28    | 969     |
| keywords                    | 0         | 0         | 0        | 0       |
| title                       | 99.6      | 98.9      | 99.25    | 1000    |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **87.28** | **87.12** | **87.2** | 3898    |
| all fields (macro avg.)     | 87.12     | 86.94     | 87.03    | 3898    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| abstract                    | 76.67     | 76.67     | 76.67    | 960     |
| authors                     | 99.48     | 99.48     | 99.48    | 969     |
| first_author                | 99.38     | 99.38     | 99.38    | 969     |
| keywords                    | 0         | 0         | 0        | 0       |
| title                       | 99.7      | 99        | 99.35    | 1000    |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **93.88** | **93.71** | **93.8** | 3898    |
| all fields (macro avg.)     | 93.81     | 93.63     | 93.72    | 3898    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 66.56     | 66.56     | 66.56     | 960     |
| authors                     | 99.38     | 99.38     | 99.38     | 969     |
| first_author                | 99.28     | 99.28     | 99.28     | 969     |
| keywords                    | 0         | 0         | 0         | 0       |
| title                       | 99.7      | 99        | 99.35     | 1000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.34** | **91.17** | **91.26** | 3898    |
| all fields (macro avg.)     | 91.23     | 91.06     | 91.14     | 3898    |

#### Instance-level results

```
Total expected instances: 	1000
Total correct instances: 	142 (strict) 
Total correct instances: 	491 (soft) 
Total correct instances: 	729 (Levenshtein) 
Total correct instances: 	641 (ObservedRatcliffObershelp) 

Instance-level recall:	14.2	(strict) 
Instance-level recall:	49.1	(soft) 
Instance-level recall:	72.9	(Levenshtein) 
Instance-level recall:	64.1	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1000 random PDF files out of 998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 81.2      | 78.45     | 79.8      | 44770   |
| date                        | 84.65     | 81.27     | 82.92     | 45457   |
| first_author                | 91.49     | 88.37     | 89.9      | 44770   |
| inTitle                     | 81.7      | 83.6      | 82.64     | 42795   |
| issue                       | 93.64     | 92.74     | 93.18     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 60        | 60.51     | 60.26     | 43101   |
| volume                      | 95.92     | 96.13     | 96.03     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **84.26** | **81.47** | **82.84** | 321178  |
| all fields (macro avg.)     | 85.29     | 82.33     | 83.7      | 321178  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 81.52     | 78.76    | 80.11     | 44770   |
| date                        | 84.65     | 81.27    | 82.92     | 45457   |
| first_author                | 91.71     | 88.58    | 90.12     | 44770   |
| inTitle                     | 85.54     | 87.53    | 86.52     | 42795   |
| issue                       | 93.64     | 92.74    | 93.18     | 18983   |
| page                        | 93.72     | 77.57    | 84.89     | 40844   |
| title                       | 92.03     | 92.81    | 92.42     | 43101   |
| volume                      | 95.92     | 96.13    | 96.03     | 40458   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **89.36** | **86.4** | **87.85** | 321178  |
| all fields (macro avg.)     | 89.84     | 86.92    | 88.27     | 321178  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 90.67     | 87.61     | 89.11     | 44770   |
| date                        | 84.65     | 81.27     | 82.92     | 45457   |
| first_author                | 92.25     | 89.1      | 90.65     | 44770   |
| inTitle                     | 86.48     | 88.49     | 87.47     | 42795   |
| issue                       | 93.64     | 92.74     | 93.18     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 94.6      | 95.39     | 94.99     | 43101   |
| volume                      | 95.92     | 96.13     | 96.03     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.2**  | **88.18** | **89.67** | 321178  |
| all fields (macro avg.)     | 91.49     | 88.54     | 89.91     | 321178  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 84.96     | 82.09     | 83.5      | 44770   |
| date                        | 84.65     | 81.27     | 82.92     | 45457   |
| first_author                | 91.49     | 88.37     | 89.9      | 44770   |
| inTitle                     | 85.19     | 87.17     | 86.17     | 42795   |
| issue                       | 93.64     | 92.74     | 93.18     | 18983   |
| page                        | 93.72     | 77.57     | 84.89     | 40844   |
| title                       | 93.99     | 94.78     | 94.39     | 43101   |
| volume                      | 95.92     | 96.13     | 96.03     | 40458   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.03** | **87.05** | **88.52** | 321178  |
| all fields (macro avg.)     | 90.45     | 87.52     | 88.87     | 321178  |

#### Instance-level results

```
Total expected instances: 		48449
Total extracted instances: 		48222
Total correct instances: 		13503 (strict) 
Total correct instances: 		22283 (soft) 
Total correct instances: 		24920 (Levenshtein) 
Total correct instances: 		23277 (RatcliffObershelp) 

Instance-level precision:	28 (strict) 
Instance-level precision:	46.21 (soft) 
Instance-level precision:	51.68 (Levenshtein) 
Instance-level precision:	48.27 (RatcliffObershelp) 

Instance-level recall:	27.87	(strict) 
Instance-level recall:	45.99	(soft) 
Instance-level recall:	51.44	(Levenshtein) 
Instance-level recall:	48.04	(RatcliffObershelp) 

Instance-level f-score:	27.94 (strict) 
Instance-level f-score:	46.1 (soft) 
Instance-level f-score:	51.56 (Levenshtein) 
Instance-level f-score:	48.16 (RatcliffObershelp) 

Matching 1 :	35400

Matching 2 :	1244

Matching 3 :	3262

Matching 4 :	1799

Total matches :	41705
```

#### Citation context resolution

```

Total expected references: 	 48449 - 48.45 references per article
Total predicted references: 	 48222 - 48.22 references per article

Total expected citation contexts: 	 69755 - 69.75 citation contexts per article
Total predicted citation contexts: 	 73167 - 73.17 citation contexts per article

Total correct predicted citation contexts: 	 56715 - 56.72 citation contexts per article
Total wrong predicted citation contexts: 	 16452 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 77.51
Recall citation contexts: 	 81.31
fscore citation contexts: 	 79.36
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
| availability_stmt           | 56.8      | 54.69     | 55.72     | 779     |
| figure_title                | 0.2       | 0.1       | 0.13      | 8943    |
| funding_stmt                | 5.37      | 30.19     | 9.12      | 1507    |
| reference_citation          | 87.97     | 94.36     | 91.05     | 69741   |
| reference_figure            | 74.18     | 85.73     | 79.54     | 11010   |
| reference_table             | 70.29     | 94.3      | 80.55     | 5159    |
| section_title               | 72.67     | 66.21     | 69.29     | 17540   |
| table_title                 | 0         | 0         | 0         | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **74.08** | **76.69** | **75.36** | 120771  |
| all fields (macro avg.)     | 45.94     | 53.2      | 48.18     | 120771  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 79.73     | 76.77     | 78.22     | 779     |
| figure_title                | 91.01     | 45.82     | 60.95     | 8943    |
| funding_stmt                | 6.78      | 38.09     | 11.51     | 1507    |
| reference_citation          | 87.97     | 94.36     | 91.06     | 69741   |
| reference_figure            | 74.43     | 86.01     | 79.8      | 11010   |
| reference_table             | 70.45     | 94.51     | 80.73     | 5159    |
| section_title               | 78.45     | 71.48     | 74.8      | 17540   |
| table_title                 | 53.33     | 7.5       | 13.15     | 6092    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.73** | **81.49** | **80.09** | 120771  |
| all fields (macro avg.)     | 67.77     | 64.32     | 61.28     | 120771  |

**Document-level ratio results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| availability_stmt           | 100       | 96.28     | 98.1     | 779     |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **100**   | **96.28** | **98.1** | 779     |
| all fields (macro avg.)     | 100       | 96.28     | 98.1     | 779     |

Evaluation metrics produced in 795.217 seconds
