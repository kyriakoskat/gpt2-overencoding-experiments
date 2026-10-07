# GPT-2 Over-Encoding Experiments

An academic NLP group project at the National Technical University of Athens (2025), exploring n-gram input representations and embedding adaptation in GPT-2.

The work is inspired by [Over-Tokenized Transformer: Vocabulary is Generally Worth Scaling](https://arxiv.org/abs/2501.16975) by Huang et al. It includes experiments with synthetic context-free grammar (CFG) sequences and pretrained GPT-2 on natural-language text.

**Status:** archive of the original coursework, with saved outputs and supporting documents. The downstream benchmark evaluation has known issues and its reported accuracies require correction and a fresh run. The notebooks are not currently a fully reproducible experiment pipeline.

## Experiments

| Notebook | Scope |
| --- | --- |
| [CFG_Experiments.ipynb](notebooks/CFG_Experiments.ipynb) | Generate synthetic character sequences; train a small GPT-2 baseline and models with hashed 2-gram and 3-gram input embeddings; compare training loss and held-out next-token accuracy. |
| [Over_Encoding_Fine_Tuning.ipynb](notebooks/Over_Encoding_Fine_Tuning.ipynb) | Initialize phrase embeddings from pretrained token embeddings, freeze the base GPT-2 parameters, and train the additional embeddings on a subset of WikiText-2. Contains historical evaluations on HellaSwag, PIQA and Story Cloze. |
| [4_gram_experiments.ipynb](notebooks/4_gram_experiments.ipynb) | Extend the phrase-embedding experiment to include 4-grams. Shares the evaluation and reproducibility limitations of the fine-tuning notebook. |

The CFG experiment enriches the input representation while keeping the output vocabulary fixed. The fine-tuning notebooks add pseudo-tokens and resize GPT-2's token embeddings, which also expands its tied output vocabulary. This distinction matters when interpreting the experiments as input/output vocabulary decoupling.

## Authors and contributions

- Giorgos Tzamouranis
- Nikos Katsaidonis
- Andreas Fotakis
- Kyriakos Katsiadramis

National Technical University of Athens.

The final presentation records the following task distribution. These are team contributions rather than claims of sole authorship:

| Team members | Contribution |
| --- | --- |
| Kyriakos Katsiadramis and Nikos Katsaidonis | CFG experiments, report writing and presentation preparation. |
| Andreas Fotakis and Giorgos Tzamouranis | Downstream-task experiments, report writing and presentation preparation. |

## Recorded CFG results

The original notebook contains an 80/20 training/validation split and saved logs for ten epochs. Its evaluation measures next-token accuracy under teacher forcing; it does not measure the validity of complete freely generated sequences.

| Model configuration in code | Parameters | Final training loss | Validation next-token accuracy |
| --- | ---: | ---: | ---: |
| Baseline GPT-2 | 2,476,032 | 0.7889 | 59.99% |
| Over-encoding, `m=4` | 2,495,360 | 0.7797 | 60.32% |
| Over-encoding, `m=64` | 2,503,040 | 0.7795 | 60.32% |

These values are transcribed from the saved logs, not from a new reproduction. The observed accuracy difference is 0.33 percentage points. No repeated-seed experiment or confidence interval is provided. Some original plot labels use `m=16` for the run whose code sets `m=64`.

## Known limitations

- **Benchmark scoring:** both fine-tuning notebooks compute manual cross-entropy without aligning predictions with the next token. Their Story Cloze evaluation uses a fixed first-option label instead of reading each example's answer. Historical benchmark percentages should not be interpreted as validated performance gains.
- **Training and evaluation setup:** padding labels are not masked out of the fine-tuning loss, and the fine-tuned model is not explicitly switched back to evaluation mode before scoring.
- **Experiment reproduction:** sections labelled with different n-gram vocabulary sizes reuse training blocks without rebuilding the corresponding models. Reproducing independent configurations requires fresh model/tokenizer setup, explicit configuration handling and separate result records.
- **Phrase preprocessing:** sequential substring replacement can miss longer overlapping n-grams or match inside words. Token-aware, longest-match handling is needed.
- **Documentation consistency:** saved outputs and current configuration values are not always aligned. The report's CFG embedding listing uses a different shift direction from the notebook. The documents discuss 5-gram experiments, but no 5-gram implementation is included in this archive.
- **External inputs:** the original notebooks reference Google Drive files that are not bundled. Dependencies are not version-pinned and model checkpoints are not supplied.

The original notebook code, outputs, report and presentations are retained unchanged so the coursework remains traceable. This README documents the current limitations; it does not claim that the underlying experiments have been repaired or rerun.

## Environment and data

The notebooks were developed for Google Colab. Their main dependencies are Python, PyTorch, Hugging Face Transformers and Datasets, scikit-learn, and Matplotlib. The original Python/package environment has not been reconstructed, so installation alone does not guarantee compatibility.

To inspect or adapt the experiments:

1. Open the relevant notebook in Jupyter or Google Colab and install compatible versions of the dependencies.
2. For the CFG notebook, generate or supply the intended 200,000-sequence dataset and update the file path. The included generation cell defaults to 20 million sequences and must be adjusted if reproducing the documented dataset size.
3. For the fine-tuning notebooks, provide access to pretrained GPT-2, WikiText-2 and the benchmark datasets. Story Cloze additionally requires the original CSV or an equivalent labelled dataset obtained from its provider.
4. Resolve the known evaluation/configuration issues before running new comparisons. Use separate runs for each configuration and export results directly from those runs.

Full model training and downstream evaluation have not been rerun for this repository preparation.

## Documents

- [Final report](reports/Report.pdf)
- [Final presentation in English](presentations/English_NLP_Semester_Assignment_Final_Presentation.pdf)
- [Final presentation in Greek](presentations/Greek_NLP_Semester_Assignment_Final_Presentation.pdf)
- [Original coursework README](docs/original_README.md)

The original documents describe the coursework as submitted. The limitations above take precedence when assessing which results have been verified.

## References

- Huang et al. (2025), [Over-Tokenized Transformer: Vocabulary is Generally Worth Scaling](https://arxiv.org/abs/2501.16975).
- [Hugging Face GPT-2 documentation](https://huggingface.co/docs/transformers/en/model_doc/gpt2).
- [ROCStories and the Story Cloze Test](https://cs.rochester.edu/nlp/rocstories/).
