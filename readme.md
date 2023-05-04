# Introduction

The document is the official source code of **Clustering-Aware Negative Sampling for Unsupervised Sentence Representation**, a paper in *Finding of ACL2023*. We introduce how to run ClusterNS and reproduce the main results here.

# Preparation

Before running the code, you may need to implement some preparation, including:
* Download unsupervised training dataset in *data/download_wiki.sh*
* Download testing dataset in *SentEval/data/downstream/download_dataset.sh*
* Prepare the python environment according to *requirements.txt*

# Main Results

We provide two bash scripts **run_non_prompt.sh** and **run_prompt.sh** for training and evaluating *Non-prompt* and *Prompt-based* ClusterNS, respectively. We have also released all checkpoints in Huggingface.
|              Model              | Avg. STS |
|:-------------------------------|:--------:|
|  [ClusterNS-non-prmt-bert-base-uncased](https://huggingface.co/djz233/ClusterNS-nonPrompt-bert-base) |   77.55 |
| [ClusterNS-non-prmt-bert-large-uncased](https://huggingface.co/djz233/ClusterNS-nonPrompt-bert-large) |   79.19  |
|    [ClusterNS-non-prmt-roberta-base](https://huggingface.co/djz233/ClusterNS-nonPrompt-roberta-base)    |   77.98  |
|    [ClusterNS-non-prmt-roberta-large](https://huggingface.co/djz233/ClusterNS-nonPrompt-roberta-large)  |   79.43  |
|   [ClusterNS-prmt-bert-base-uncased](https://huggingface.co/djz233/ClusterNS-Prompt-bert-base)|   78.72  |
|  [ClusterNS-prmt-bert-large-uncased](https://huggingface.co/djz233/ClusterNS-Prompt-bert-large)  |   80.30  |
|     [ClusterNS-prmt-roberta-base](https://huggingface.co/djz233/ClusterNS-Prompt-roberta-base)     |   79.74  |

# Hyperparameters

We provide some importance hyperparameters in our models for reproducing. Note that we use distributed data parallel for some of model trainings, thus 128*4 in batch_size means **per_device_train_batch_size**=128 with 4 GPUs.
 Hyperparameter | BERT-base | BERT-large | RoBERTa-base | RoBERTa-large | prompt-BERT-base | prompt-BERT-large | prompt-RoBERTa-base  
----------------|-----------|------------|--------------|---------------|------------------|-------------------|----------------------
 batch_size     | 256       | 128*4      | 256*2        | 128*4         | 512              | 64*4              | 256*2                
 model_lr       | 5e-5  | 5e-5   | 5e-5     | 5e-5      | 5e-5         | 3e-5          | 5e-5             
 kmeans         | 128       | 128        | 128          | 128           | 96               | 96                | 128                  
 kmeans_lr      | 1e-3  | 1e-3   | 1e-3     | 5e-4      | 5e-4         | 1e-4          | 1e-3             
 kmean_cosine   | 0.4       | 0.5        | 0.4          | 0.4           | 0.4              | 0.2               | 0.4                  
 enable_hardneg | TRUE      | TRUE       | TRUE         | TRUE          | TRUE             | TRUE              | FALSE                
 bml_weight     | 1e-3  | 5e-5   | 1e-4     | 0             | 1e-2         | 5e-4          | 1e-2             
 bml_alpha      | 0         | 0.25       | 0.2          |               | 0                | 0.25              | 0.2                  
 bml_beta       | 0.3       | 0.3        | 0.5          |               | 0.2              | 0.3               | 0.6                  

