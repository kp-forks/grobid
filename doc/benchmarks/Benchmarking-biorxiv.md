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
| abstract                    | 2.31      | 2.26      | 2.29      | 1989    |
| authors                     | 85.17     | 84.48     | 84.82     | 1998    |
| first_author                | 96.92     | 96.24     | 96.58     | 1996    |
| keywords                    | 57.56     | 58.59     | 58.07     | 838     |
| title                       | 77.33     | 76.64     | 76.98     | 1999    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **64.94** | **64.37** | **64.65** | 8820    |
| all fields (macro avg.)     | 63.86     | 63.64     | 63.75     | 8820    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 59.93     | 58.57     | 59.24     | 1989    |
| authors                     | 85.57     | 84.88     | 85.23     | 1998    |
| first_author                | 97.12     | 96.44     | 96.78     | 1996    |
| keywords                    | 62.72     | 63.84     | 63.28     | 838     |
| title                       | 79.51     | 78.79     | 79.15     | 1999    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **78.88** | **78.19** | **78.53** | 8820    |
| all fields (macro avg.)     | 76.97     | 76.51     | 76.73     | 8820    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 80.4      | 78.58     | 79.48     | 1989    |
| authors                     | 92.68     | 91.94     | 92.31     | 1998    |
| first_author                | 97.38     | 96.69     | 97.03     | 1996    |
| keywords                    | 79.25     | 80.67     | 79.95     | 838     |
| title                       | 92.02     | 91.2      | 91.61     | 1999    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **89.56** | **88.76** | **89.16** | 8820    |
| all fields (macro avg.)     | 88.35     | 87.82     | 88.08     | 8820    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 76.75     | 75.01     | 75.87     | 1989    |
| authors                     | 88.75     | 88.04     | 88.39     | 1998    |
| first_author                | 96.92     | 96.24     | 96.58     | 1996    |
| keywords                    | 70.81     | 72.08     | 71.44     | 838     |
| title                       | 87.68     | 86.89     | 87.29     | 1999    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **85.94** | **85.18** | **85.56** | 8820    |
| all fields (macro avg.)     | 84.18     | 83.65     | 83.91     | 8820    |

#### Instance-level results

```
Total expected instances: 	1999
Total correct instances: 	38 (strict) 
Total correct instances: 	716 (soft) 
Total correct instances: 	1231 (Levenshtein) 
Total correct instances: 	1054 (ObservedRatcliffObershelp) 

Instance-level recall:	1.9	(strict) 
Instance-level recall:	35.82	(soft) 
Instance-level recall:	61.58	(Levenshtein) 
Instance-level recall:	52.73	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 2000 random PDF files out of 1998 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| authors                     | 88.22     | 83.08    | 85.57     | 97132   |
| date                        | 91.69     | 86.08    | 88.8      | 97579   |
| doi                         | 70.8      | 83.66    | 76.69     | 16894   |
| first_author                | 95.09     | 89.48    | 92.2      | 97132   |
| inTitle                     | 82.84     | 79.2     | 80.98     | 96379   |
| issue                       | 94.29     | 91.72    | 92.99     | 30312   |
| page                        | 94.99     | 78.06    | 85.7      | 88551   |
| pmcid                       | 66.44     | 86.12    | 75.01     | 807     |
| pmid                        | 69.73     | 84.52    | 76.41     | 2093    |
| title                       | 84.79     | 83.26    | 84.02     | 92415   |
| volume                      | 96.21     | 94.94    | 95.57     | 87661   |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **89.84** | **85.1** | **87.41** | 706955  |
| all fields (macro avg.)     | 85.01     | 85.46    | 84.9      | 706955  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 89.38     | 84.17     | 86.69     | 97132   |
| date                        | 91.69     | 86.08     | 88.8      | 97579   |
| doi                         | 75.26     | 88.94     | 81.53     | 16894   |
| first_author                | 95.52     | 89.88     | 92.61     | 97132   |
| inTitle                     | 92.32     | 88.27     | 90.25     | 96379   |
| issue                       | 94.29     | 91.72     | 92.99     | 30312   |
| page                        | 94.99     | 78.06     | 85.7      | 88551   |
| pmcid                       | 75.72     | 98.14     | 85.48     | 807     |
| pmid                        | 74.14     | 89.87     | 81.25     | 2093    |
| title                       | 93.12     | 91.43     | 92.27     | 92415   |
| volume                      | 96.21     | 94.94     | 95.57     | 87661   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.65** | **87.77** | **90.14** | 706955  |
| all fields (macro avg.)     | 88.42     | 89.23     | 88.47     | 706955  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 94.63     | 89.12     | 91.79     | 97132   |
| date                        | 91.69     | 86.08     | 88.8      | 97579   |
| doi                         | 77.54     | 91.62     | 83.99     | 16894   |
| first_author                | 95.67     | 90.02     | 92.76     | 97132   |
| inTitle                     | 93.33     | 89.23     | 91.23     | 96379   |
| issue                       | 94.29     | 91.72     | 92.99     | 30312   |
| page                        | 94.99     | 78.06     | 85.7      | 88551   |
| pmcid                       | 75.72     | 98.14     | 85.48     | 807     |
| pmid                        | 74.14     | 89.87     | 81.25     | 2093    |
| title                       | 96.07     | 94.33     | 95.19     | 92415   |
| volume                      | 96.21     | 94.94     | 95.57     | 87661   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **94**    | **89.04** | **91.45** | 706955  |
| all fields (macro avg.)     | 89.48     | 90.28     | 89.52     | 706955  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 91.59     | 86.25     | 88.84     | 97132   |
| date                        | 91.69     | 86.08     | 88.8      | 97579   |
| doi                         | 75.95     | 89.75     | 82.27     | 16894   |
| first_author                | 95.14     | 89.52     | 92.24     | 97132   |
| inTitle                     | 91.08     | 87.08     | 89.04     | 96379   |
| issue                       | 94.29     | 91.72     | 92.99     | 30312   |
| page                        | 94.99     | 78.06     | 85.7      | 88551   |
| pmcid                       | 66.44     | 86.12     | 75.01     | 807     |
| pmid                        | 69.73     | 84.52     | 76.41     | 2093    |
| title                       | 95.41     | 93.68     | 94.54     | 92415   |
| volume                      | 96.21     | 94.94     | 95.57     | 87661   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.03** | **88.12** | **90.51** | 706955  |
| all fields (macro avg.)     | 87.5      | 87.97     | 87.4      | 706955  |

#### Instance-level results

```
Total expected instances: 		98748
Total extracted instances: 		97659
Total correct instances: 		43524 (strict) 
Total correct instances: 		54446 (soft) 
Total correct instances: 		58679 (Levenshtein) 
Total correct instances: 		55424 (RatcliffObershelp) 

Instance-level precision:	44.57 (strict) 
Instance-level precision:	55.75 (soft) 
Instance-level precision:	60.09 (Levenshtein) 
Instance-level precision:	56.75 (RatcliffObershelp) 

Instance-level recall:	44.08	(strict) 
Instance-level recall:	55.14	(soft) 
Instance-level recall:	59.42	(Levenshtein) 
Instance-level recall:	56.13	(RatcliffObershelp) 

Instance-level f-score:	44.32 (strict) 
Instance-level f-score:	55.44 (soft) 
Instance-level f-score:	59.75 (Levenshtein) 
Instance-level f-score:	56.44 (RatcliffObershelp) 

Matching 1 :	78921

Matching 2 :	4556

Matching 3 :	4369

Matching 4 :	2097

Total matches :	89943
```

#### Citation context resolution

```

Total expected references: 	 98746 - 49.37 references per article
Total predicted references: 	 97659 - 48.83 references per article

Total expected citation contexts: 	 142776 - 71.39 citation contexts per article
Total predicted citation contexts: 	 134504 - 67.25 citation contexts per article

Total correct predicted citation contexts: 	 115917 - 57.96 citation contexts per article
Total wrong predicted citation contexts: 	 18587 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 86.18
Recall citation contexts: 	 81.19
fscore citation contexts: 	 83.61
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
| availability_stmt           | 29.41     | 25.78     | 27.48     | 446     |
| figure_title                | 4.21      | 2.34      | 3.01      | 22967   |
| funding_stmt                | 3.63      | 23.16     | 6.28      | 747     |
| reference_citation          | 71.99     | 70.93     | 71.45     | 147384  |
| reference_figure            | 70.3      | 76.85     | 73.43     | 47896   |
| reference_table             | 45.19     | 84.98     | 59        | 5957    |
| section_title               | 68.82     | 68.57     | 68.69     | 32368   |
| table_title                 | 6.94      | 2.55      | 3.73      | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **65.11** | **64.78** | **64.94** | 261690  |
| all fields (macro avg.)     | 37.56     | 44.39     | 39.13     | 261690  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 51.92     | 45.52     | 48.51     | 446     |
| figure_title                | 66.52     | 36.97     | 47.52     | 22967   |
| funding_stmt                | 3.84      | 24.5      | 6.65      | 747     |
| reference_citation          | 84.27     | 83.03     | 83.64     | 147384  |
| reference_figure            | 70.93     | 77.54     | 74.09     | 47896   |
| reference_table             | 45.59     | 85.71     | 59.52     | 5957    |
| section_title               | 74.24     | 73.98     | 74.11     | 32368   |
| table_title                 | 81.53     | 29.91     | 43.77     | 3925    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **76.28** | **75.89** | **76.08** | 261690  |
| all fields (macro avg.)     | 59.85     | 57.14     | 54.72     | 261690  |

**Document-level ratio results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| availability_stmt           | 84.82     | 87.67     | 86.22     | 446     |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **84.82** | **87.67** | **86.22** | 446     |
| all fields (macro avg.)     | 84.82     | 87.67     | 86.22     | 446     |

Evaluation metrics produced in 1563.714 seconds


