# m3

This repository contains the dataset intoduced in our EMNLP 2022 Findings paper [M3: Multi-level dataset for Multi-document summarisation of Medical studies](https://aclanthology.org/2022.findings-emnlp.286/). Below is the description of the files included and (where applicable) their structure.

## Unstructured document-level files

**unprocessed1.zip** and **unprocessed2.zip** contain the original files which we retrieved and mapped; these correspond to the **Document** level in the paper, with full abstracts of the systematic reviews mapped to the full abstracts of the clinical studies which were included into them.

## Document level (structured)

**level1.jsonl** contains the conlusions (not full abstracts!) of the systematic reviews mapped to the full abstracts of the clinical studies. The structure is as follows:

**docid**: PMID of the systematic review.

**target_text**: the Conclusions section of the review's abstract (or manually selected conclusions, if the abstract was unstructured)

**input_text**: the abstracts of the included clinical trials, separated by the standard separator for multi-document summarisation (|||||)

**input_studies**: a list of dictionaries, each of which contains the PMID (**source_pmid**) and the abstract's text (**source_text**) of an included study 

## Sentence level

**level2.jsonl** contains sentences from the conclusions of a systematic review (separate entry/line for each of the sentences) mapped to the corresponding evidence sentences from the included primary studies. The structure is as follows:

**docid**: PMID of the systematic review with an index that corresponds to the sentence in the conclusions (i.e. for PMID 26258610 where we include two sentences from the conclusions, their docid are 26258610_0 and 26258610_1). We use this index even if the conclusions have only one sentence (30845235_0).

**target_text**: the sentence from the conclusions in the abstract of the systematic review.

**input_text**: the evidence sentences from the abstracts of the clinical trials, separated by |||||. We include only the sentences that are directly relevant for the conclusions sentence.

**input_studies**: a list of dictionaries, each of which contains the PMID (**source_pmid**) of the included study where thee evidence sentence was taken from, and the text of that evidence sentence (**source_text**).

## Claim level (Proposition level in the paper)

At the claim level (**level3.jsonl**), the conclusions and evidence sentences are mapped even more precisely, i.e. if a conclusions sentence contains several distinct claims (clauses or phrases that refer to a different Patient/problem, Intervention, Comparator, or Outcome), we separate them and map each claim only with the evidence sentences that correspond to it. The structure is the follows:

**docid**: PMID of the systematic review with an index that corresponds to each of the claims.

**pico**: a dictionary with PICO elements of the claim ("p", "i", "c", "o"). 

**discourse_relation**: shows if all of the included studies have the same results regarding the claim ("agreement"), or if some studies contradict the others ("contradiction").

**target_modality**: the certainty of the claim in the review (strong, moderate, weak, no evidence).

**target_modality_span**: the text span which shows that certainty (usually empty/underspecified for moderate modality)

**target_direction**: the direction of findings in the conclusions (positive, negative, no effect).

**target_direction_span**: the text spans which reflects that direction.

**target_text**: the sentence from the conclusions in the abstract of the systematic review which contains the claim.

**input_text**: the evidence sentences from the abstracts of the clinical trials, separated by |||||. We include only the sentences that are directly relevant for the claim.

**input_studies**: again, a list of dictionaries, each corresponding to a relevant evidence sentence from the input studies. Each of them has the following elements:

**source_pmid**: PMID of the clinical trial the evidence sentence is taken from.

**source_text**: the text of the evidence sentence.

**source_modality**: the certainty of the evidence sentence (strong, moderate, weak, no evidence).

**source_modality_span**: the text span which shows that certainty (usually empty/underspecified for moderate modality).

**source_direction**: the direction of findings in evidence sentence (positive, negative, no effect).

**source_direction_span**: the text spans which reflects that direction.


## Citation

Please cite us when using this dataset:

```
@inproceedings{otmakhova-etal-2022-m3,
    title = "{M}3: Multi-level dataset for Multi-document summarisation of Medical studies",
    author = "Otmakhova, Yulia  and
      Verspoor, Karin  and
      Baldwin, Timothy  and
      Jimeno Yepes, Antonio  and
      Lau, Jey Han",
booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2022",
    year = "2022",
    pages = "3887--3901",
}
```





