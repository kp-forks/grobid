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
| abstract                    | 2.11      | 2.06      | 2.09      | 1990    |
| authors                     | 83.27     | 82.69     | 82.98     | 1999    |
| first_author                | 95.42     | 94.84     | 95.13     | 1997    |
| keywords                    | 48.52     | 48.87     | 48.69     | 839     |
| title                       | 74.57     | 73.9      | 74.23     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **62.66** | **62.05** | **62.35** | 8825    |
| all fields (macro avg.)     | 60.78     | 60.47     | 60.62     | 8825    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| abstract                    | 57.31     | 55.93     | 56.61    | 1990    |
| authors                     | 83.68     | 83.09     | 83.38    | 1999    |
| first_author                | 95.62     | 95.04     | 95.33    | 1997    |
| keywords                    | 52.78     | 53.16     | 52.97    | 839     |
| title                       | 76.78     | 76.05     | 76.41    | 2000    |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **75.98** | **75.23** | **75.6** | 8825    |
| all fields (macro avg.)     | 73.23     | 72.65     | 72.94    | 8825    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 78.48     | 76.58     | 77.52     | 1990    |
| authors                     | 91.49     | 90.85     | 91.16     | 1999    |
| first_author                | 95.82     | 95.24     | 95.53     | 1997    |
| keywords                    | 70.89     | 71.39     | 71.14     | 839     |
| title                       | 89.5      | 88.65     | 89.07     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **87.14** | **86.28** | **86.71** | 8825    |
| all fields (macro avg.)     | 85.23     | 84.54     | 84.89     | 8825    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 75.8      | 73.97     | 74.87     | 1990    |
| authors                     | 86.85     | 86.24     | 86.55     | 1999    |
| first_author                | 95.42     | 94.84     | 95.13     | 1997    |
| keywords                    | 61.42     | 61.86     | 61.64     | 839     |
| title                       | 85.11     | 84.3      | 84.7      | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **83.49** | **82.66** | **83.07** | 8825    |
| all fields (macro avg.)     | 80.92     | 80.24     | 80.58     | 8825    |

#### Instance-level results

```
Total expected instances: 	2000
Total correct instances: 	32 (strict) 
Total correct instances: 	635 (soft) 
Total correct instances: 	1109 (Levenshtein) 
Total correct instances: 	965 (ObservedRatcliffObershelp) 

Instance-level recall:	1.6	(strict) 
Instance-level recall:	31.75	(soft) 
Instance-level recall:	55.45	(Levenshtein) 
Instance-level recall:	48.25	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 2000 random PDF files out of 1998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 88.2      | 83.3      | 85.68     | 97183   |
| date                        | 91.73     | 86.34     | 88.95     | 97630   |
| doi                         | 70.75     | 83.9      | 76.77     | 16894   |
| first_author                | 95.08     | 89.73     | 92.33     | 97183   |
| inTitle                     | 82.88     | 79.47     | 81.14     | 96430   |
| issue                       | 94.37     | 92.08     | 93.21     | 30312   |
| page                        | 94.99     | 78.39     | 85.89     | 88597   |
| pmcid                       | 66.28     | 85.75     | 74.77     | 807     |
| pmid                        | 69.58     | 84.71     | 76.41     | 2093    |
| title                       | 84.93     | 83.63     | 84.28     | 92463   |
| volume                      | 96.26     | 95.25     | 95.76     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.87** | **85.39** | **87.57** | 707301  |
| all fields (macro avg.)     | 85.01     | 85.69     | 85.02     | 707301  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 89.35     | 84.39     | 86.8      | 97183   |
| date                        | 91.73     | 86.34     | 88.95     | 97630   |
| doi                         | 75.22     | 89.2      | 81.62     | 16894   |
| first_author                | 95.51     | 90.13     | 92.74     | 97183   |
| inTitle                     | 92.37     | 88.56     | 90.43     | 96430   |
| issue                       | 94.37     | 92.08     | 93.21     | 30312   |
| page                        | 94.99     | 78.39     | 85.89     | 88597   |
| pmcid                       | 75.57     | 97.77     | 85.25     | 807     |
| pmid                        | 73.98     | 90.06     | 81.23     | 2093    |
| title                       | 93.28     | 91.86     | 92.57     | 92463   |
| volume                      | 96.26     | 95.25     | 95.76     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.69** | **88.06** | **90.32** | 707301  |
| all fields (macro avg.)     | 88.42     | 89.46     | 88.59     | 707301  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| authors                     | 94.61     | 89.36     | 91.91    | 97183   |
| date                        | 91.73     | 86.34     | 88.95    | 97630   |
| doi                         | 77.47     | 91.87     | 84.06    | 16894   |
| first_author                | 95.66     | 90.28     | 92.89    | 97183   |
| inTitle                     | 93.35     | 89.5      | 91.38    | 96430   |
| issue                       | 94.37     | 92.08     | 93.21    | 30312   |
| page                        | 94.99     | 78.39     | 85.89    | 88597   |
| pmcid                       | 75.57     | 97.77     | 85.25    | 807     |
| pmid                        | 73.98     | 90.06     | 81.23    | 2093    |
| title                       | 96.09     | 94.62     | 95.35    | 92463   |
| volume                      | 96.26     | 95.25     | 95.76    | 87709   |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **94.01** | **89.32** | **91.6** | 707301  |
| all fields (macro avg.)     | 89.46     | 90.5      | 89.63    | 707301  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 91.56     | 86.48    | 88.95     | 97183   |
| date                        | 91.73     | 86.34    | 88.95     | 97630   |
| doi                         | 75.91     | 90.02    | 82.37     | 16894   |
| first_author                | 95.13     | 89.77    | 92.37     | 97183   |
| inTitle                     | 91.1      | 87.35    | 89.19     | 96430   |
| issue                       | 94.37     | 92.08    | 93.21     | 30312   |
| page                        | 94.99     | 78.39    | 85.89     | 88597   |
| pmcid                       | 66.28     | 85.75    | 74.77     | 807     |
| pmid                        | 69.58     | 84.71    | 76.41     | 2093    |
| title                       | 95.41     | 93.95    | 94.67     | 92463   |
| volume                      | 96.26     | 95.25    | 95.76     | 87709   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **93.04** | **88.4** | **90.66** | 707301  |
| all fields (macro avg.)     | 87.49     | 88.19    | 87.5      | 707301  |

#### Instance-level results

```
Total expected instances: 		98799
Total extracted instances: 		98017
Total correct instances: 		43800 (strict) 
Total correct instances: 		54818 (soft) 
Total correct instances: 		59005 (Levenshtein) 
Total correct instances: 		55718 (RatcliffObershelp) 

Instance-level precision:	44.69 (strict) 
Instance-level precision:	55.93 (soft) 
Instance-level precision:	60.2 (Levenshtein) 
Instance-level precision:	56.85 (RatcliffObershelp) 

Instance-level recall:	44.33	(strict) 
Instance-level recall:	55.48	(soft) 
Instance-level recall:	59.72	(Levenshtein) 
Instance-level recall:	56.4	(RatcliffObershelp) 

Instance-level f-score:	44.51 (strict) 
Instance-level f-score:	55.7 (soft) 
Instance-level f-score:	59.96 (Levenshtein) 
Instance-level f-score:	56.62 (RatcliffObershelp) 

Matching 1 :	79353

Matching 2 :	4422

Matching 3 :	4354

Matching 4 :	2116

Total matches :	90245
```

#### Citation context resolution

```

Total expected references: 	 98797 - 49.4 references per article
Total predicted references: 	 98017 - 49.01 references per article

Total expected citation contexts: 	 142862 - 71.43 citation contexts per article
Total predicted citation contexts: 	 134742 - 67.37 citation contexts per article

Total correct predicted citation contexts: 	 116243 - 58.12 citation contexts per article
Total wrong predicted citation contexts: 	 18499 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 86.27
Recall citation contexts: 	 81.37
fscore citation contexts: 	 83.75
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
| availability_stmt           | 29.12     | 27.35     | 28.21     | 446     |
| conflict_stmt               | 69.44     | 58.95     | 63.77     | 609     |
| contribution_stmt           | 44.95     | 43.84     | 44.39     | 609     |
| figure_title                | 4.35      | 2.37      | 3.07      | 22978   |
| funding_stmt                | 3.94      | 23.83     | 6.76      | 747     |
| reference_citation          | 71.99     | 70.92     | 71.45     | 147470  |
| reference_figure            | 70.36     | 77.2      | 73.62     | 47984   |
| reference_table             | 45.56     | 86.5      | 59.68     | 5957    |
| section_title               | 71.56     | 70        | 70.77     | 32398   |
| table_title                 | 7.62      | 2.75      | 4.04      | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **65.55** | **65.01** | **65.28** | 263123  |
| all fields (macro avg.)     | 41.89     | 46.37     | 42.58     | 263123  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 50.12     | 47.09     | 48.55     | 446     |
| conflict_stmt               | 84.72     | 71.92     | 77.8      | 609     |
| contribution_stmt           | 75.93     | 74.06     | 74.98     | 609     |
| figure_title                | 68.44     | 37.26     | 48.25     | 22978   |
| funding_stmt                | 4.2       | 25.44     | 7.21      | 747     |
| reference_citation          | 84.34     | 83.09     | 83.71     | 147470  |
| reference_figure            | 71.01     | 77.92     | 74.31     | 47984   |
| reference_table             | 45.97     | 87.29     | 60.23     | 5957    |
| section_title               | 77.08     | 75.4      | 76.23     | 32398   |
| table_title                 | 82.85     | 29.91     | 43.95     | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.87** | **76.23** | **76.55** | 263123  |
| all fields (macro avg.)     | 64.47     | 60.94     | 59.52     | 263123  |

**Document-level ratio results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 83.3      | 93.95     | 88.3      | 446     |
| conflict_stmt               | 96.64     | 84.89     | 90.38     | 609     |
| contribution_stmt           | 93.69     | 97.54     | 95.58     | 609     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.51** | **91.95** | **91.73** | 1664    |
| all fields (macro avg.)     | 91.21     | 92.13     | 91.42     | 1664    |

Evaluation metrics produced in 1576.58 seconds



