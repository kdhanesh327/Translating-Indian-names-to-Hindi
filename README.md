# Translating-Indian-Names-to-Hindi


## Overview

This project performs task of translating Indian Names to Hindi, a sequence-to-sequence modeling task, using character-level conditional language models.

### 1. **Tokenization**
- **Loading the Dataset**: The dataset contains pairs of Indian names in their original form and their corresponding Hindi translations.
- Now with the data, Prepare a tokenization strategy for feeding name pairs as a sequence to different models. For English this could be as simple as using individual characters as tokens, but Hindi has accents (मात्राएँ), a larger set of vowels (स्वर), consonants (व्यंजन), and additional composition rules (half-letters, etc.), so such a simple strategy may not be effective.
- Given a set of initial tokens, learn suitable combinations which are added as new tokens until a certain vocabulary size is reached. Implemented this kind called [BPE Tokenization](https://arxiv.org/abs/1508.07909)
- Tokenizer that operates jointly over both languages or have separate tokenizers for English and Hindi.
- Tokenizer will learn the tokenization from data (BPE technique mentioned above) or can use a fixed set of rules for decomposition.

### 2.1 **Seq-2-Seq Modeling with RNNs**
   Implement an encoder-decoder network using RNNs(GRU implemented), to learn a conditional language model for the task of translating the names to Hindi.
   
   - **Encoder**: This part of the model takes in the input (Indian name) and encodes it into a fixed-size vector representation.
   - **Decoder**: The decoder generates the translated Hindi name character-by-character, conditioned on the encoder's output.
   
   The model is trained to minimize the loss between the predicted Hindi translation and the true translation, using techniques such as teacher forcing.

### 2.2 **Seq-2-Seq Modeling with RNN + Attention**
  Augment the Encoder-Decoder architecture to utilize attention, by implementing an Attention module that attends over the representations / inputs from the encoder.

- Popular approaches are desribed in the original [paper by Bahdanau et al., 2014 on NMT](https://arxiv.org/abs/1409.0473) and an [exploratory paper by Luong et al, 2015](https://arxiv.org/abs/1508.04025) which explores different effective approaches to attention, including global and local attention. Used Bahdanau's attention.

### 3. **Training the Model**
   - **Loss Function**: Cross-entropy loss is used as the primary loss function to evaluate the difference between predicted characters and actual Hindi characters.
   - **Optimizer**: Adam(or any other gradient-based) optimization technique is used to update the model's parameters during training.
   - **Evaluation**: The model is evaluated on a validation set, measuring metrics like accuracy or loss.

### 4. **Model Inference**
   After training, the model can be used to translate new Indian names into Hindi. The inference process uses the encoder to encode the input name and the decoder to predict the translation.

### 5. **Results**

#### 1. **Encoder-Decoder RNN**
- **Accuracy:** 13.25%
- **Character Error Rate (CER):** 33.77%
- **Token Error Rate (TER):** 51.12%
- **BLEU Score:** 0.5757

#### Validation Set Example Translations
| Name     | Translation (Expected) | Translation (Model) |
|----------|------------------------|---------------------|
| mhosin   | मोहसीन                 | एमएचओ               |
| qadeem   | क़दीम                 | क़ाम                |
| ashiqu   | आशिक़                 | आशिक               |
| midhana  | मिधना                 | मिना                |
| divakar  | दिवाकर                | दिवार               |

---

#### 2. **Encoder-Decoder RNN with Attention**
- **Accuracy:** 22.00%
- **Character Error Rate (CER):** 33.97%
- **Token Error Rate (TER):** 49.00%
- **BLEU Score:** 0.4132

#### Validation Set Example Translations
| Name     | Translation (Expected) | Translation (Model)         |
|----------|------------------------|-----------------------------|
| mhosin   | मोहसीन                 | एमएमएमएमएमएमएमएमए            |
| qadeem   | क़दीम                 | क़ाम                        |
| ashiqu   | आशिक़                 | आशिकूशीकूशीकूशीकूशीकूशी    |
| midhana  | मिधना                 | मीना                        |
| divakar  | दिवाकर                | दिवकर                      |



### 6. **Instructions to Run the Code**
   1. **Clone the Repository**:
      ```bash
      git clone https://github.com/yourusername/your-repo-name.git
      ```
   2. **Run the Code**:
      To run the model, simply execute the Python script:
      ```bash
      python DHANESH_KUMAR_22476_assignment3.py
      ```

## Author
- **Naveen Kumar Pallekonda**
