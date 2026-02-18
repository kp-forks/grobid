# Benchmarking biorXiv

## General

This is the end-to-end benchmarking result for GROBID version **0.8.2** against the `bioRxiv` test set (
`biorxiv-10k-test-2000`), see the [End-to-end evaluation](End-to-end-evaluation.md) page for explanations and for
reproducing this evaluation.

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

Evaluation on 2000 PDF preprints out of 2000 (no failure).

Runtime for processing 2000 PDF: **1713** seconds (0.85 seconds per PDF file) on Ubuntu 22.04, 16 CPU (32 threads),
128GB RAM and with a GeForce GTX 1080 Ti GPU.

Note: with CRF only models runtime is 622s (0.31 second per PDF) with 4 CPU, 8 threads.

## Header metadata

Evaluation on 2000 random PDF files out of 1998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 2.2       | 2.16      | 2.18      | 1990    |
| authors                     | 84.79     | 84.19     | 84.49     | 1999    |
| first_author                | 96.68     | 96.09     | 96.38     | 1997    |
| keywords                    | 56.19     | 56.26     | 56.22     | 839     |
| title                       | 76.57     | 76        | 76.29     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **64.45** | **63.88** | **64.16** | 8825    |
| all fields (macro avg.)     | 63.29     | 62.94     | 63.11     | 8825    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 58.89     | 57.74     | 58.31     | 1990    |
| authors                     | 85.19     | 84.59     | 84.89     | 1999    |
| first_author                | 96.88     | 96.29     | 96.58     | 1997    |
| keywords                    | 61.55     | 61.62     | 61.58     | 839     |
| title                       | 78.78     | 78.15     | 78.46     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.25** | **77.54** | **77.89** | 8825    |
| all fields (macro avg.)     | 76.26     | 75.68     | 75.97     | 8825    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 80.32     | 78.74     | 79.52     | 1990    |
| authors                     | 92.39     | 91.75     | 92.07     | 1999    |
| first_author                | 97.13     | 96.54     | 96.84     | 1997    |
| keywords                    | 78.21     | 78.31     | 78.26     | 839     |
| title                       | 91.18     | 90.45     | 90.81     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.14** | **88.33** | **88.73** | 8825    |
| all fields (macro avg.)     | 87.85     | 87.16     | 87.5      | 8825    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 77.45     | 75.93     | 76.68     | 1990    |
| authors                     | 88.36     | 87.74     | 88.05     | 1999    |
| first_author                | 96.68     | 96.09     | 96.38     | 1997    |
| keywords                    | 69.05     | 69.13     | 69.09     | 839     |
| title                       | 86.79     | 86.1      | 86.45     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **85.6**  | **84.83** | **85.21** | 8825    |
| all fields (macro avg.)     | 83.67     | 83        | 83.33     | 8825    |

#### Instance-level results

```
Total expected instances: 	2000
Total correct instances: 	35 (strict) 
Total correct instances: 	703 (soft) 
Total correct instances: 	1216 (Levenshtein) 
Total correct instances: 	1047 (ObservedRatcliffObershelp) 

Instance-level recall:	1.75	(strict) 
Instance-level recall:	35.15	(soft) 
Instance-level recall:	60.8	(Levenshtein) 
Instance-level recall:	52.35	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 2000 random PDF files out of 1998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 88.21     | 83.28     | 85.68     | 97183   |
| date                        | 91.71     | 86.3      | 88.92     | 97630   |
| doi                         | 70.73     | 83.75     | 76.69     | 16894   |
| first_author                | 95.09     | 89.7      | 92.31     | 97183   |
| inTitle                     | 82.85     | 79.41     | 81.09     | 96430   |
| issue                       | 94.31     | 91.85     | 93.07     | 30312   |
| page                        | 94.99     | 78.25     | 85.81     | 88597   |
| pmcid                       | 66.22     | 85.75     | 74.73     | 807     |
| pmid                        | 69.59     | 84.85     | 76.47     | 2093    |
| title                       | 84.84     | 83.51     | 84.17     | 92463   |
| volume                      | 96.21     | 95.17     | 95.69     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.85** | **85.31** | **87.52** | 707301  |
| all fields (macro avg.)     | 84.98     | 85.62     | 84.97     | 707301  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 89.37     | 84.37     | 86.8      | 97183   |
| date                        | 91.71     | 86.3      | 88.92     | 97630   |
| doi                         | 75.17     | 89        | 81.5      | 16894   |
| first_author                | 95.51     | 90.1      | 92.73     | 97183   |
| inTitle                     | 92.33     | 88.49     | 90.37     | 96430   |
| issue                       | 94.31     | 91.85     | 93.07     | 30312   |
| page                        | 94.99     | 78.25     | 85.81     | 88597   |
| pmcid                       | 75.5      | 97.77     | 85.21     | 807     |
| pmid                        | 73.98     | 90.21     | 81.29     | 2093    |
| title                       | 93.17     | 91.71     | 92.44     | 92463   |
| volume                      | 96.21     | 95.17     | 95.69     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.66** | **87.98** | **90.26** | 707301  |
| all fields (macro avg.)     | 88.39     | 89.38     | 88.53     | 707301  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 94.63     | 89.33     | 91.9      | 97183   |
| date                        | 91.71     | 86.3      | 88.92     | 97630   |
| doi                         | 77.46     | 91.71     | 83.98     | 16894   |
| first_author                | 95.66     | 90.24     | 92.87     | 97183   |
| inTitle                     | 93.33     | 89.45     | 91.35     | 96430   |
| issue                       | 94.31     | 91.85     | 93.07     | 30312   |
| page                        | 94.99     | 78.25     | 85.81     | 88597   |
| pmcid                       | 75.5      | 97.77     | 85.21     | 807     |
| pmid                        | 73.98     | 90.21     | 81.29     | 2093    |
| title                       | 96.08     | 94.57     | 95.32     | 92463   |
| volume                      | 96.21     | 95.17     | 95.69     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **94**    | **89.25** | **91.56** | 707301  |
| all fields (macro avg.)     | 89.44     | 90.44     | 89.58     | 707301  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 91.59     | 86.46     | 88.95     | 97183   |
| date                        | 91.71     | 86.3      | 88.92     | 97630   |
| doi                         | 75.86     | 89.82     | 82.25     | 16894   |
| first_author                | 95.13     | 89.74     | 92.36     | 97183   |
| inTitle                     | 91.07     | 87.29     | 89.14     | 96430   |
| issue                       | 94.31     | 91.85     | 93.07     | 30312   |
| page                        | 94.99     | 78.25     | 85.81     | 88597   |
| pmcid                       | 66.22     | 85.75     | 74.73     | 807     |
| pmid                        | 69.59     | 84.85     | 76.47     | 2093    |
| title                       | 95.41     | 93.91     | 94.66     | 92463   |
| volume                      | 96.21     | 95.17     | 95.69     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.03** | **88.33** | **90.62** | 707301  |
| all fields (macro avg.)     | 87.46     | 88.13     | 87.46     | 707301  |

#### Instance-level results

```
Total expected instances: 		98799
Total extracted instances: 		97961
Total correct instances: 		43683 (strict) 
Total correct instances: 		54641 (soft) 
Total correct instances: 		58882 (Levenshtein) 
Total correct instances: 		55610 (RatcliffObershelp) 

Instance-level precision:	44.59 (strict) 
Instance-level precision:	55.78 (soft) 
Instance-level precision:	60.11 (Levenshtein) 
Instance-level precision:	56.77 (RatcliffObershelp) 

Instance-level recall:	44.21	(strict) 
Instance-level recall:	55.31	(soft) 
Instance-level recall:	59.6	(Levenshtein) 
Instance-level recall:	56.29	(RatcliffObershelp) 

Instance-level f-score:	44.4 (strict) 
Instance-level f-score:	55.54 (soft) 
Instance-level f-score:	59.85 (Levenshtein) 
Instance-level f-score:	56.53 (RatcliffObershelp) 

Matching 1 :	79217

Matching 2 :	4518

Matching 3 :	4359

Matching 4 :	2108

Total matches :	90202
```

#### Citation context resolution

```

Total expected references: 	 98797 - 49.4 references per article
Total predicted references: 	 97961 - 48.98 references per article

Total expected citation contexts: 	 142862 - 71.43 citation contexts per article
Total predicted citation contexts: 	 134929 - 67.46 citation contexts per article

Total correct predicted citation contexts: 	 116348 - 58.17 citation contexts per article
Total wrong predicted citation contexts: 	 18581 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 86.23
Recall citation contexts: 	 81.44
fscore citation contexts: 	 83.77
```

## Fulltext structures

Fulltext structure contents are complicated to capture from JATS NLM files. They are often normalized and different from
the actual PDF content and are can be inconsistent from one document to another. The scores of the following metrics are
thus not very meaningful in absolute term, in particular for the strict matching (textual content of the srtructure can
be very long). As relative values for comparing different models, they seem however useful.

Evaluation on 2000 random PDF files out of 1998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 29.34     | 28.03     | 28.67     | 446     |
| conflict_stmt               | 69.54     | 59.61     | 64.19     | 609     |
| contribution_stmt           | 44.72     | 43.84     | 44.28     | 609     |
| figure_title                | 4.25      | 2.35      | 3.03      | 22978   |
| funding_stmt                | 3.94      | 23.83     | 6.76      | 747     |
| reference_citation          | 71.95     | 70.91     | 71.43     | 147470  |
| reference_figure            | 70.3      | 76.95     | 73.48     | 47984   |
| reference_table             | 45.1      | 84.71     | 58.86     | 5957    |
| section_title               | 69.08     | 68.61     | 68.84     | 32398   |
| table_title                 | 6.99      | 2.55      | 3.73      | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **65.16** | **64.74** | **64.95** | 263123  |
| all fields (macro avg.)     | 41.52     | 46.14     | 42.33     | 263123  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 51.17     | 48.88     | 50        | 446     |
| conflict_stmt               | 84.67     | 72.58     | 78.16     | 609     |
| contribution_stmt           | 75.88     | 74.38     | 75.12     | 609     |
| figure_title                | 66.8      | 36.99     | 47.61     | 22978   |
| funding_stmt                | 4.18      | 25.3      | 7.18      | 747     |
| reference_citation          | 84.28     | 83.06     | 83.66     | 147470  |
| reference_figure            | 70.96     | 77.67     | 74.16     | 47984   |
| reference_table             | 45.49     | 85.45     | 59.37     | 5957    |
| section_title               | 74.49     | 73.98     | 74.24     | 32398   |
| table_title                 | 81.2      | 29.61     | 43.39     | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.41** | **75.92** | **76.17** | 263123  |
| all fields (macro avg.)     | 63.91     | 60.79     | 59.29     | 263123  |

**Document-level ratio results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| availability_stmt           | 83.2      | 95.52     | 88.94    | 446     |
| conflict_stmt               | 96.49     | 85.71     | 90.78    | 609     |
| contribution_stmt           | 93.57     | 98.03     | 95.75    | 609     |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **91.37** | **92.85** | **92.1** | 1664    |
| all fields (macro avg.)     | 91.09     | 93.09     | 91.82    | 1664    |

Evaluation metrics produced in 1898.536 seconds


