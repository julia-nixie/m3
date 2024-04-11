# m3

This repository contains the dataset intoduced in our EMNLP 2022 Findings paper [M3: Multi-level dataset for Multi-document summarisation of Medical studies](https://aclanthology.org/2022.findings-emnlp.286/). Below is the description of the files included and (where applicable) their structure.

### Unstructured files

**unprocessed1.zip** and **unprocessed2.zip** contain the original files which we retrieved and mapped; these correspond to the **Document** level in the paper, with full abstracts of the systematic reviews mapped to the full abstracts of the clinical studies which were included into them.

### Document level (structured)

**level1.jsonl** contains the conlusions (not full abstracts!) of the systematic reviews mapped to the full abstracts of the clinical studies. The structure is as follows:

**docid**: PMID of the systematic review.
**target_text**: the Conclusions section of the review's abstract (or manually selected conclusions, if the abstract was unstructured)
**input_text**: the abstracts of the included clinical trials, separated by the standard separator for multi-document summarisation (|||||)
**input_studies**: a list of dictionaries, each of which contains the PMID (**source_pmid**) and the abstract's text (**source_text**) of an included study 
