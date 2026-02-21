# Benchmarking PubMed Central

## General

This is the end-to-end benchmarking result for GROBID version **0.8.2** against the `PMC_sample_1943` dataset, see
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

Evaluation on 1943 random PDF PMC files out of 1943 PDF from 1943 different journals (0 PDF parsing failure).

Runtime for processing 1943 PDF: **1467** seconds, (0.75s per PDF) on Ubuntu 22.04, 16 CPU (32 threads), 128GB RAM and
with a GeForce GTX 1080 Ti GPU.

Note: with CRF only models, runtime is 470s (0.24 seconds per PDF) with 4 CPU, 8 threads.

## Header metadata

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 16.41     | 16.12     | 16.26     | 1911    |
| authors                     | 92.26     | 92.17     | 92.22     | 1941    |
| first_author                | 96.7      | 96.6      | 96.65     | 1941    |
| keywords                    | 63.96     | 62.1      | 63.01     | 1380    |
| title                       | 84.35     | 84.05     | 84.2      | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **71.55** | **70.89** | **71.22** | 9116    |
| all fields (macro avg.)     | 70.74     | 70.21     | 70.47     | 9116    |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall   | f1        | support |
|-----------------------------|-----------|----------|-----------|---------|
| abstract                    | 63.35     | 62.22    | 62.78     | 1911    |
| authors                     | 94.22     | 94.13    | 94.18     | 1941    |
| first_author                | 97.11     | 97.01    | 97.06     | 1941    |
| keywords                    | 72.39     | 70.29    | 71.32     | 1380    |
| title                       | 91.89     | 91.56    | 91.72     | 1943    |
|                             |           |          |           |         |
| **all fields (micro avg.)** | **84.69** | **83.9** | **84.29** | 9116    |
| all fields (macro avg.)     | 83.79     | 83.04    | 83.41     | 9116    |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 90.41     | 88.8      | 89.6      | 1911    |
| authors                     | 96.24     | 96.14     | 96.19     | 1941    |
| first_author                | 97.37     | 97.27     | 97.32     | 1941    |
| keywords                    | 83.28     | 80.87     | 82.06     | 1380    |
| title                       | 98.19     | 97.84     | 98.01     | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **93.77** | **92.89** | **93.33** | 9116    |
| all fields (macro avg.)     | 93.1      | 92.18     | 92.64     | 9116    |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| abstract                    | 86.47     | 84.93     | 85.69     | 1911    |
| authors                     | 95.2      | 95.11     | 95.15     | 1941    |
| first_author                | 96.7      | 96.6      | 96.65     | 1941    |
| keywords                    | 77.69     | 75.43     | 76.54     | 1380    |
| title                       | 96.07     | 95.73     | 95.9      | 1943    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.3**  | **90.45** | **90.87** | 9116    |
| all fields (macro avg.)     | 90.43     | 89.56     | 89.99     | 9116    |

#### Instance-level results

```
Total expected instances: 	1943
Total correct instances: 	213 (strict) 
Total correct instances: 	900 (soft) 
Total correct instances: 	1410 (Levenshtein) 
Total correct instances: 	1259 (ObservedRatcliffObershelp) 

Instance-level recall:	10.96	(strict) 
Instance-level recall:	46.32	(soft) 
Instance-level recall:	72.57	(Levenshtein) 
Instance-level recall:	64.8	(RatcliffObershelp) 
```

## Citation metadata

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 83.13     | 76.25     | 79.54     | 85778   |
| date                        | 94.69     | 84.12     | 89.09     | 87067   |
| first_author                | 89.85     | 82.39     | 85.96     | 85778   |
| inTitle                     | 73.34     | 71.77     | 72.54     | 81007   |
| issue                       | 91.15     | 87.61     | 89.35     | 16635   |
| page                        | 94.64     | 83.58     | 88.77     | 80501   |
| title                       | 79.81     | 75.26     | 77.47     | 80736   |
| volume                      | 96.15     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **87.32** | **80.64** | **83.85** | 597569  |
| all fields (macro avg.)     | 87.84     | 81.33     | 84.44     | 597569  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 83.6      | 76.68     | 79.99     | 85778   |
| date                        | 94.69     | 84.12     | 89.09     | 87067   |
| first_author                | 90.02     | 82.55     | 86.12     | 85778   |
| inTitle                     | 85.08     | 83.25     | 84.15     | 81007   |
| issue                       | 91.15     | 87.61     | 89.35     | 16635   |
| page                        | 94.64     | 83.58     | 88.77     | 80501   |
| title                       | 91.59     | 86.36     | 88.9      | 80736   |
| volume                      | 96.15     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **90.72** | **83.78** | **87.11** | 597569  |
| all fields (macro avg.)     | 90.86     | 84.23     | 87.4      | 597569  |

#### Levenshtein Matching (Minimum Levenshtein distance at 0.8)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 89.29     | 81.9      | 85.43     | 85778   |
| date                        | 94.69     | 84.12     | 89.09     | 87067   |
| first_author                | 90.23     | 82.74     | 86.32     | 85778   |
| inTitle                     | 86.32     | 84.47     | 85.39     | 81007   |
| issue                       | 91.15     | 87.61     | 89.35     | 16635   |
| page                        | 94.64     | 83.58     | 88.77     | 80501   |
| title                       | 93.87     | 88.52     | 91.12     | 80736   |
| volume                      | 96.15     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **92.06** | **85.01** | **88.39** | 597569  |
| all fields (macro avg.)     | 92.04     | 85.33     | 88.53     | 597569  |

#### Ratcliff/Obershelp Matching (Minimum Ratcliff/Obershelp similarity at 0.95)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| authors                     | 86.07     | 78.95     | 82.35     | 85778   |
| date                        | 94.69     | 84.12     | 89.09     | 87067   |
| first_author                | 89.87     | 82.41     | 85.98     | 85778   |
| inTitle                     | 83.64     | 81.84     | 82.73     | 81007   |
| issue                       | 91.15     | 87.61     | 89.35     | 16635   |
| page                        | 94.64     | 83.58     | 88.77     | 80501   |
| title                       | 93.48     | 88.15     | 90.74     | 80736   |
| volume                      | 96.15     | 89.66     | 92.79     | 80067   |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **91.11** | **84.14** | **87.48** | 597569  |
| all fields (macro avg.)     | 91.21     | 84.54     | 87.73     | 597569  |

#### Instance-level results

```
Total expected instances: 		90125
Total extracted instances: 		85309
Total correct instances: 		38774 (strict) 
Total correct instances: 		50926 (soft) 
Total correct instances: 		55751 (Levenshtein) 
Total correct instances: 		52311 (RatcliffObershelp) 

Instance-level precision:	45.45 (strict) 
Instance-level precision:	59.7 (soft) 
Instance-level precision:	65.35 (Levenshtein) 
Instance-level precision:	61.32 (RatcliffObershelp) 

Instance-level recall:	43.02	(strict) 
Instance-level recall:	56.51	(soft) 
Instance-level recall:	61.86	(Levenshtein) 
Instance-level recall:	58.04	(RatcliffObershelp) 

Instance-level f-score:	44.2 (strict) 
Instance-level f-score:	58.06 (soft) 
Instance-level f-score:	63.56 (Levenshtein) 
Instance-level f-score:	59.64 (RatcliffObershelp) 

Matching 1 :	68288

Matching 2 :	4092

Matching 3 :	1852

Matching 4 :	655

Total matches :	74887
```

#### Citation context resolution

```

Total expected references: 	 90125 - 46.38 references per article
Total predicted references: 	 85309 - 43.91 references per article

Total expected citation contexts: 	 139835 - 71.97 citation contexts per article
Total predicted citation contexts: 	 115045 - 59.21 citation contexts per article

Total correct predicted citation contexts: 	 97438 - 50.15 citation contexts per article
Total wrong predicted citation contexts: 	 17607 (wrong callout matching, callout missing in NLM, or matching with a bib. ref. not aligned with a bib.ref. in NLM)

Precision citation contexts: 	 84.7
Recall citation contexts: 	 69.68
fscore citation contexts: 	 76.46
```

## Fulltext structures

Fulltext structure contents are complicated to capture from JATS NLM files. They are often normalized and different from
the actual PDF content and are can be inconsistent from one document to another. The scores of the following metrics are
thus not very meaningful in absolute term, in particular for the strict matching (textual content of the srtructure can
be very long). As relative values for comparing different models, they seem however useful.

Evaluation on 1943 random PDF files out of 1941 PDF (ratio 1.0).

#### Strict Matching (exact matches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| figure_title                | 32.03     | 26.71     | 29.13     | 7281    |
| reference_citation          | 58.13     | 58.81     | 58.47     | 134196  |
| reference_figure            | 60.58     | 68.28     | 64.2      | 19330   |
| reference_table             | 82.86     | 89.65     | 86.12     | 7327    |
| section_title               | 72.49     | 67.67     | 70        | 27619   |
| table_title                 | 67.74     | 49.66     | 57.31     | 3971    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **60.57** | **60.73** | **60.65** | 199724  |
| all fields (macro avg.)     | 62.31     | 60.13     | 60.87     | 199724  |

#### Soft Matching (ignoring punctuation, case and space characters mismatches)

**Field-level results**

| label                       | precision | recall    | f1        | support |
|-----------------------------|-----------|-----------|-----------|---------|
| figure_title                | 79.87     | 66.61     | 72.64     | 7281    |
| reference_citation          | 62.41     | 63.14     | 62.77     | 134196  |
| reference_figure            | 61.08     | 68.84     | 64.72     | 19330   |
| reference_table             | 83.02     | 89.83     | 86.29     | 7327    |
| section_title               | 77.88     | 72.7      | 75.2      | 27619   |
| table_title                 | 94.33     | 69.15     | 79.8      | 3971    |
|                             |           |           |           |         |
| **all fields (micro avg.)** | **66.07** | **66.24** | **66.15** | 199724  |
| all fields (macro avg.)     | 76.43     | 71.71     | 73.57     | 199724  |

**Document-level ratio results**

| label                       | precision | recall | f1    | support |
|-----------------------------|-----------|--------|-------|---------|
|                             |           |        |       |         |
| **all fields (micro avg.)** | **0**     | **0**  | **0** | 0       |
| all fields (macro avg.)     | 0         | 0      | 0     | 0       |

Evaluation metrics produced in 1270.333 seconds
