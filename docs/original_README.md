

# Decoupling Input and Output Vocabularies Using Over Encoding on GPT-2

## 📚 Description

This project explores enhancements to GPT-2 language models through **Over-Encoding** and **multi-gram embedding** strategies. The objective is to improve model performance—either by training from scratch or through targeted fine-tuning—without significant increases in computational cost.

---

## 🧪 Experiments

The experiments are organized into three main categories:

### 1. **Training GPT-2 from Scratch with Over-Encoding (CFG Experiments)**

- **Directory:** `CFG_Experiments`
- A synthetic dataset was generated using a Context-Free Grammar (CFG) with a small vocabulary.
- A GPT-2 model was trained from scratch using over-encoded input representations (1-gram, 2-gram, and 3-gram embeddings).
- Results showed consistent improvements in training loss and generation accuracy compared to the baseline.

---

### 2. **Fine-Tuning Pretrained GPT-2 with Multi-gram Embeddings (Over-Encoding Fine-Tuning)**

- **Directory:** `Over_Encoding_Fine_Tuining`
- The pretrained embedding layer was extended with new 2-gram and 3-gram embeddings, initialized as the mean of the corresponding token embeddings.
- Only the newly added multi-gram embeddings were fine-tuned; original parameters were frozen.
- Performance improved on contextual reasoning tasks like HellaSwag and Story Cloze, with minimal computational overhead.

---

### 3. **Extension to 4-gram and 5-gram Embeddings**

- **Directory:** `4_gram_experiments`
- The multi-gram embedding approach was further extended to include 4-grams and 5-grams.
- While results followed the same performance trends, gains diminished with higher-order n-grams due to increased complexity and reduced benefit.

---

## 📂 Project Structure


---

## 👥 Authors

- Giorgos Tzamouranis  
- Nikos Katsaidonis  
- Andreas Fotakis  
- Kyriakos Katsiadramis  

National Technical University of Athens

---

## 📄 Report

For a comprehensive explanation of the methodology and results, please refer to the final report:  
**`Report.pdf`**

---

## 🔗 References

- Huang et al. (2025), *Over-Tokenized Transformer: Vocabulary is Generally Worth Scaling*, [arXiv:2501.16975](https://arxiv.org/abs/2501.16975)
