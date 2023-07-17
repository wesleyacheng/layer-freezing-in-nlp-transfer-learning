# layer-freezing-in-nlp-transfer-learning
Layer Freezing in NLP Transfer Learning

# Introduction

Hello, I'm **Wesley**, nice to meet you. 👋

**Transfer learning** is the technique of using a pre-trained base model (e.g. BERT) and adapating it to a particular domain to do a particular task. The name we call this type of training in the transfer learning domain is *fine-tuning*.

**Traditionally**, the process of *fine-tuning* has usually been done with **all** the layers of a base model as trainable parameters with a low learning rate to get the **best performance** possible. This is done in the hopes that we can reuse most of the **semantic representations** that it had learned from its the pretrained dataset while having the flexibility to adapt the model to a different domain with similar dataset characteristics. For example, **BERT** is pre-trained on *English* datasets (**BookCorpus** and **Wikipedia**), and so it would be **ideal** that we *fine-tune* the model on an *English* dataset to leverage its previous understanding of English and use it to do other tasks like sentiment classification to have **minimal** data distribution shift.

![bert](https://github.com/wesleyacheng/layer-freezing-in-nlp-transfer-learning/assets/15952538/d2dca473-48a7-4458-b063-1ce9e477ba1d)

Since we don't have to train the model from **scratch** to achieve **state-of-the-art** results, transfer learning saves us **substantial amount of compute time and cost** and **allows anyone with just even a single GPU** to adapt a pre-trained base model to their own domain for **high-speed prototyping** and even an eventual **production deployment**.

The question we will explore in this notebook is **"Can we save even more compute time and cost by freezing certain layers of the base model while achieving marginal reduction in relative performance compared to that of the traditional unfrozen pre-trained base model"**? Let's find out!

We will be using the **[HuggingFace DistilBert model](https://huggingface.co/distilbert-base-uncased)** to do a **sentiment classification** on the **[Stanford Sentiment dataset (SST2)](https://paperswithcode.com/dataset/sst)** in this experiment to **measure NLP transfer learning performance differences with layer freezing**.

**TLDR**:
- Freezing the embedding layer seems to increase test performance, while decreasing around half the trainable parameters.
- Freezing more layers does decrease test performance, but not as much as you think.
- Freezing most layers except the last 1 or 2 transformer layer seems to be the goldilock zone to reduce compute time and cost while achieving similar unfrozen results.
