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
| abstract                    | 1.95      | 1.91      | 1.93      | 1990    |
| authors                     | 83.58     | 82.74     | 83.16     | 1999    |
| first_author                | 95.76     | 94.89     | 95.32     | 1997    |
| keywords                    | 50.77     | 50.89     | 50.83     | 839     |
| title                       | 74.77     | 73.95     | 74.36     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **62.98** | **62.24** | **62.61** | 8825    |
| all fields (macro avg.)     | 61.37     | 60.88     | 61.12     | 8825    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| abstract                    | 56.86     | 55.58    | 56.21     | 1990    |
| authors                     | 83.98     | 83.14    | 83.56     | 1999    |
| first_author                | 95.96     | 95.09    | 95.52     | 1997    |
| keywords                    | 55.41     | 55.54    | 55.48     | 839     |
| title                       | 76.9      | 76.05    | 76.47     | 2000    |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **76.29** | **75.4** | **75.84** | 8825    |
| all fields (macro avg.)     | 73.82     | 73.08    | 73.45     | 8825    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 77.69     | 75.93     | 76.8      | 1990    |
| authors                     | 91.66     | 90.75     | 91.2      | 1999    |
| first_author                | 96.21     | 95.34     | 95.77     | 1997    |
| keywords                    | 73.96     | 74.14     | 74.05     | 839     |
| title                       | 89.59     | 88.6      | 89.09     | 2000    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **87.4**  | **86.38** | **86.89** | 8825    |
| all fields (macro avg.)     | 85.82     | 84.95     | 85.38     | 8825    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| abstract                    | 75.12     | 73.42    | 74.26     | 1990    |
| authors                     | 87.06     | 86.19    | 86.63     | 1999    |
| first_author                | 95.76     | 94.89    | 95.32     | 1997    |
| keywords                    | 63.61     | 63.77    | 63.69     | 839     |
| title                       | 85.14     | 84.2     | 84.67     | 2000    |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **83.67** | **82.7** | **83.18** | 8825    |
| all fields (macro avg.)     | 81.34     | 80.49    | 80.91     | 8825    |

#### Instance-level results

```
Total expected instances: 	2000
Total correct instances: 	30 (strict) 
Total correct instances: 	651 (soft) 
Total correct instances: 	1117 (Levenshtein) 
Total correct instances: 	967 (ObservedRatcliffObershelp) 

Instance-level recall:	1.5	(strict) 
Instance-level recall:	32.55	(soft) 
Instance-level recall:	55.85	(Levenshtein) 
Instance-level recall:	48.35	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 2000 random PDF files out of 1998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 88.18     | 83.29     | 85.67     | 97183   |
| date                        | 91.73     | 86.34     | 88.95     | 97630   |
| doi                         | 70.76     | 83.97     | 76.8      | 16894   |
| first_author                | 95.08     | 89.73     | 92.33     | 97183   |
| inTitle                     | 82.86     | 79.45     | 81.12     | 96430   |
| issue                       | 94.33     | 92.13     | 93.22     | 30312   |
| page                        | 95        | 78.37     | 85.89     | 88597   |
| pmcid                       | 66.28     | 85.75     | 74.77     | 807     |
| pmid                        | 69.58     | 84.71     | 76.41     | 2093    |
| title                       | 84.91     | 83.61     | 84.26     | 92463   |
| volume                      | 96.25     | 95.24     | 95.74     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.86** | **85.38** | **87.57** | 707301  |
| all fields (macro avg.)     | 85        | 85.69     | 85.01     | 707301  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 89.34     | 84.38     | 86.79     | 97183   |
| date                        | 91.73     | 86.34     | 88.95     | 97630   |
| doi                         | 75.22     | 89.27     | 81.65     | 16894   |
| first_author                | 95.51     | 90.13     | 92.74     | 97183   |
| inTitle                     | 92.36     | 88.55     | 90.42     | 96430   |
| issue                       | 94.33     | 92.13     | 93.22     | 30312   |
| page                        | 95        | 78.37     | 85.89     | 88597   |
| pmcid                       | 75.57     | 97.77     | 85.25     | 807     |
| pmid                        | 73.98     | 90.06     | 81.23     | 2093    |
| title                       | 93.27     | 91.84     | 92.55     | 92463   |
| volume                      | 96.25     | 95.24     | 95.74     | 87709   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.68** | **88.06** | **90.31** | 707301  |
| all fields (macro avg.)     | 88.41     | 89.46     | 88.58     | 707301  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| authors                     | 94.6      | 89.35     | 91.9     | 97183   |
| date                        | 91.73     | 86.34     | 88.95    | 97630   |
| doi                         | 77.48     | 91.95     | 84.1     | 16894   |
| first_author                | 95.66     | 90.28     | 92.89    | 97183   |
| inTitle                     | 93.34     | 89.5      | 91.38    | 96430   |
| issue                       | 94.33     | 92.13     | 93.22    | 30312   |
| page                        | 95        | 78.37     | 85.89    | 88597   |
| pmcid                       | 75.57     | 97.77     | 85.25    | 807     |
| pmid                        | 73.98     | 90.06     | 81.23    | 2093    |
| title                       | 96.08     | 94.61     | 95.34    | 92463   |
| volume                      | 96.25     | 95.24     | 95.74    | 87709   |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **94.01** | **89.32** | **91.6** | 707301  |
| all fields (macro avg.)     | 89.46     | 90.51     | 89.63    | 707301  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 91.55     | 86.47    | 88.94     | 97183   |
| date                        | 91.73     | 86.34    | 88.95     | 97630   |
| doi                         | 75.92     | 90.1     | 82.4      | 16894   |
| first_author                | 95.13     | 89.77    | 92.37     | 97183   |
| inTitle                     | 91.09     | 87.34    | 89.18     | 96430   |
| issue                       | 94.33     | 92.13    | 93.22     | 30312   |
| page                        | 95        | 78.37    | 85.89     | 88597   |
| pmcid                       | 66.28     | 85.75    | 74.77     | 807     |
| pmid                        | 69.58     | 84.71    | 76.41     | 2093    |
| title                       | 95.4      | 93.94    | 94.67     | 92463   |
| volume                      | 96.25     | 95.24    | 95.74     | 87709   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **93.04** | **88.4** | **90.66** | 707301  |
| all fields (macro avg.)     | 87.48     | 88.2     | 87.5      | 707301  |

#### Instance-level results

```
Total expected instances: 		98799
Total extracted instances: 		98005
Total correct instances: 		43780 (strict) 
Total correct instances: 		54792 (soft) 
Total correct instances: 		58974 (Levenshtein) 
Total correct instances: 		55686 (RatcliffObershelp) 

Instance-level precision:	44.67 (strict) 
Instance-level precision:	55.91 (soft) 
Instance-level precision:	60.17 (Levenshtein) 
Instance-level precision:	56.82 (RatcliffObershelp) 

Instance-level recall:	44.31	(strict) 
Instance-level recall:	55.46	(soft) 
Instance-level recall:	59.69	(Levenshtein) 
Instance-level recall:	56.36	(RatcliffObershelp) 

Instance-level f-score:	44.49 (strict) 
Instance-level f-score:	55.68 (soft) 
Instance-level f-score:	59.93 (Levenshtein) 
Instance-level f-score:	56.59 (RatcliffObershelp) 

Matching 1 :	79340

Matching 2 :	4436

Matching 3 :	4358

Matching 4 :	2112

Total matches :	90246
```

#### Citation context resolution

```

Total expected references: 	 98797 - 49.4 references per article
Total predicted references: 	 98005 - 49 references per article

Total expected citation contexts: 	 142862 - 71.43 citation contexts per article
Total predicted citation contexts: 	 134792 - 67.4 citation contexts per article

Total correct predicted citation contexts: 	 116277 - 58.14 citation contexts per article
Total wrong predicted citation contexts: 	 18515 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 86.26
Recall citation contexts: 	 81.39
fscore citation contexts: 	 83.76
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
| availability_stmt           | 29.3      | 27.13     | 28.17     | 446     |
| conflict_stmt               | 68.77     | 58.95     | 63.48     | 609     |
| contribution_stmt           | 45.5      | 44.01     | 44.74     | 609     |
| figure_title                | 4.35      | 2.36      | 3.06      | 22978   |
| funding_stmt                | 3.69      | 23.96     | 6.4       | 747     |
| reference_citation          | 71.95     | 70.95     | 71.44     | 147470  |
| reference_figure            | 70.4      | 77.16     | 73.63     | 47984   |
| reference_table             | 45.53     | 86.55     | 59.67     | 5957    |
| section_title               | 71.57     | 70.16     | 70.86     | 32398   |
| table_title                 | 7.46      | 2.7       | 3.97      | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **65.47** | **65.03** | **65.25** | 263123  |
| all fields (macro avg.)     | 41.85     | 46.39     | 42.54     | 263123  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 50.36     | 46.64     | 48.43     | 446     |
| conflict_stmt               | 83.91     | 71.92     | 77.45     | 609     |
| contribution_stmt           | 76.23     | 73.73     | 74.96     | 609     |
| figure_title                | 68.49     | 37.22     | 48.23     | 22978   |
| funding_stmt                | 3.94      | 25.57     | 6.83      | 747     |
| reference_citation          | 84.32     | 83.15     | 83.73     | 147470  |
| reference_figure            | 71.05     | 77.87     | 74.3      | 47984   |
| reference_table             | 45.95     | 87.34     | 60.22     | 5957    |
| section_title               | 77.1      | 75.58     | 76.34     | 32398   |
| table_title                 | 82.54     | 29.86     | 43.85     | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.78** | **76.27** | **76.52** | 263123  |
| all fields (macro avg.)     | 64.39     | 60.89     | 59.43     | 263123  |

**Document-level ratio results**

| label                       | precision | recall    | f1       | support |
|-----------------------------|-----------|-----------|----------|---------|
| availability_stmt           | 84.29     | 92.6      | 88.25    | 446     |
| conflict_stmt               | 96.13     | 85.71     | 90.62    | 609     |
| contribution_stmt           | 93.94     | 96.72     | 95.31    | 609     |
|                             |           |           |          |         |
| **all fields (micro avg.)** | **91.81** | **91.59** | **91.7** | 1664    |
| all fields (macro avg.)     | 91.45     | 91.68     | 91.39    | 1664    |

Evaluation metrics produced in 1586.758 seconds


