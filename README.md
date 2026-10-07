# GPT-2 Over-Encoding Experiments

An academic NLP group project at the National Technical University of Athens (2025), exploring n-gram input representations and embedding adaptation in GPT-2.

The work is inspired by [Over-Tokenized Transformer: Vocabulary is Generally Worth Scaling](https://arxiv.org/abs/2501.16975) by Huang et al. It includes experiments with synthetic context-free grammar (CFG) sequences and pretrained GPT-2 on natural-language text.

This repository contains the coursework notebooks, saved experimental outputs, final report, and presentations.

## Experiments

| Notebook | Scope |
| --- | --- |
| [CFG_Experiments.ipynb](notebooks/CFG_Experiments.ipynb) | Generate synthetic character sequences; train a small GPT-2 baseline and models with hashed 2-gram and 3-gram input embeddings; compare training loss and held-out next-token accuracy. |
| [Over_Encoding_Fine_Tuning.ipynb](notebooks/Over_Encoding_Fine_Tuning.ipynb) | Initialize phrase embeddings from pretrained token embeddings, freeze the base GPT-2 parameters, and train the additional embeddings on a subset of WikiText-2. Includes evaluation sections for HellaSwag, PIQA and Story Cloze. |
| [4_gram_experiments.ipynb](notebooks/4_gram_experiments.ipynb) | Extend the phrase-embedding experiment to include 4-grams. |

The CFG experiment enriches the input representation while keeping the output vocabulary fixed. The fine-tuning notebooks add pseudo-tokens and resize GPT-2's token embeddings, which also expands its tied output vocabulary. This distinction matters when interpreting the experiments as input/output vocabulary decoupling.

## Authors and contributions

- Giorgos Tzamouranis
- Nikos Katsaidonis
- Andreas Fotakis
- Kyriakos Katsiadramis

National Technical University of Athens.

The team's task distribution, as recorded in the final presentation:

| Team members | Contribution |
| --- | --- |
| Kyriakos Katsiadramis and Nikos Katsaidonis | CFG experiments, report writing and presentation preparation. |
| Andreas Fotakis and Giorgos Tzamouranis | Downstream-task experiments, report writing and presentation preparation. |

## Recorded CFG results

The CFG notebook records ten training epochs with an 80/20 training/validation split. Validation next-token accuracy is measured under teacher forcing.

| Model configuration in code | Parameters | Final training loss | Validation next-token accuracy |
| --- | ---: | ---: | ---: |
| Baseline GPT-2 | 2,476,032 | 0.7889 | 59.99% |
| Over-encoding, `m=4` | 2,495,360 | 0.7797 | 60.32% |
| Over-encoding, `m=64` | 2,503,040 | 0.7795 | 60.32% |

The recorded over-encoding configurations reach 60.32% validation next-token accuracy, compared with 59.99% for the baseline: an increase of 0.33 percentage points.

## Environment and data

The notebooks were developed in Google Colab. The main technologies are:

- Python and PyTorch
- Hugging Face Transformers and Datasets
- scikit-learn
- Matplotlib

The experiments use synthetic CFG sequences and WikiText-2 for language modeling, with evaluation sections for HellaSwag, PIQA and Story Cloze. The notebooks can be opened in Google Colab or Jupyter to explore the experiment code and saved outputs.

## Documents

- [Final report](reports/Report.pdf)
- [Final presentation in English](presentations/English_NLP_Semester_Assignment_Final_Presentation.pdf)
- [Final presentation in Greek](presentations/Greek_NLP_Semester_Assignment_Final_Presentation.pdf)
- [Original coursework README](docs/original_README.md)

## References

- Huang et al. (2025), [Over-Tokenized Transformer: Vocabulary is Generally Worth Scaling](https://arxiv.org/abs/2501.16975).
- [Hugging Face GPT-2 documentation](https://huggingface.co/docs/transformers/en/model_doc/gpt2).
- [ROCStories and the Story Cloze Test](https://cs.rochester.edu/nlp/rocstories/).
