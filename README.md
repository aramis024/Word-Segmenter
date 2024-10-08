<div align="center">

# Back to Supervision: Boosting Word Boundary Detection through Frame Classification
Simone Carnemolla (simone.carnemolla@phd.unict.it),
Salvatore Calcagno (salvatore.calcagno@phd.unict.it),
Simone Palazzo (simone.palazzo@unict.it),
Daniela Giordano (daniela.giordano@unict.it)

</div>

# Overview
Official PyTorch implementation of paper: <b>"Back to Supervision: Boosting Word Boundary Detection through Frame Classification"</b>

# Abstract
Speech segmentation at both word and phoneme levels is crucial for various speech processing tasks. It significantly aids in extracting meaningful units from an utterance, thus enabling the generation of discrete elements. In this work we propose a model-agnostic framework to perform word boundary detection in a supervised manner also employing a labels augmentation technique and an output-frame selection strategy. We trained and tested on the Buckeye dataset and only tested on TIMIT one, using state-of-the-art encoder models, including pre-trained solutions (Wav2Vec 2.0 and HuBERT), as well as convolutional and convolutional recurrent networks. Our method, with the HuBERT encoder, surpasses the performance of other state-of-the-art architectures, whether trained in supervised or self-supervised settings on the same datasets. Specifically, we achieved F-values of 0.8427 on the Buckeye dataset and 0.7436 on the TIMIT dataset, along with R-values of 0.8489 and 0.7807, respectively. These results establish a new state-of-the-art for both datasets. Beyond the immediate task, our approach offers a robust and efficient preprocessing method for future research in audio tokenization.



# Method
![alt text](https://github.com/aramis024/Word-Segmenter/blob/main/pictures/Method.png)

# How to get the data and organize it

## Buckeye
Buckeye Corpus can be downloaded from the following link: [buckeye corpus](https://buckeyecorpus.osu.edu/). 

After downloading the corpus, extract all the files and place them within the ```data/Buckeye/``` folder. the final result should be similar to:

```
Buckeye
├── s01_5945.phn
├── s01_5945.wav
├── s01_5945.word
└── ...
```


## TIMIT
TIMIT dataset can be downloaded from the official site from the following link [official release](https://catalog.ldc.upenn.edu/LDC93S1).
A free version of the dataset is also available on kaggle ([darpa timit](https://www.kaggle.com/datasets/mfekadu/darpa-timit-acousticphonetic-continuous-speech)). There are no license specified,  the work may be protected by copyright.

After the download you will get a ```.zip``` file. Unzip the content and place it within the ```data/TIMIT/``` folder. The final result should be similar to:

```
TIMIT
└── data
    ├── TEST
    ├── TRAIN
├── PHONECODE.DOC
├── PROMPTS.txt
├── README.doc
└── ...

```

# How to get the weights
The weights for all tested models are available on [Zenodo](https://zenodo.org/records/13351564). After the download place the weights within the ```checkpoint/``` folder.

The final result should be similar to:

```
checkpoint
├── WBD_HuBERT.pt
├── WBD_W2V.pt
├── WBD_CNN.pt
└── WBD_CRNN.pt
```


# How to run
Open the file [example.ipynb](example.ipynb) and follow the instructions.

## Pre-requisites
- NVIDIA GPU (Tested on Nvidia A6000 GPUs )
- [Requirements](requirements.txt)

### **Test Examples**
The output expected for each model should be as follow:

<b>Buckeye</b>

| Modello       | Precision | Recall | F-Value | OS | R-Value |
|---------------|-----------------|-------------|--------------|---------|--------------|
| **CNN**       | 0.3843          | 0.3605      | 0.3709       | **-0.0576** | 0.4694       |
| **CRNN**      | 0.4113          | 0.3712      | 0.3896       | -0.0973 | 0.4924       |
| **Wav2Vec 2.0** | 0.6557          | 0.4737      | 0.5495       | -0.2767 | 0.6139       |
| **HuBERT Large** | **0.9000**          | **0.7928**      | **0.8428**       | -0.1187 | **0.8490**       |

<b>TIMIT</b>

| Modello       | Precisione | Recall | F-Value | OS | R-Value |
|---------------|-----------------|-------------|--------------|---------|--------------|
| **CNN**       | 0.2490          | 0.1697      | 0.2008       | -0.3170 | 0.3722       |
| **CRNN**      | 0.2611          | 0.2247      | 0.2411       | -0.1378 | 0.3794       |
| **Wav2Vec 2.0** | 0.4434          | 0.3538      | 0.3931       | -0.2005 | 0.5032       |
| **HuBERT Large** | **0.7566**          | **0.7315**      | **0.7437**       | **-0.0328** | **0.7807**       |


# Acknowledgements
- To split buckeye dataset we employed the script ```buckeye_preprocess.py``` by [ML Speech Research Lab](https://github.com/MLSpeech/DSegKNN/blob/main/buckeye_preprocess.py)
- Financial support from: PNRR MUR project PE0000013-FAIR.

# References 
[1] Bhati, Saurabhchand, et al. "Unsupervised speech segmentation and variable rate representation learning using segmental contrastive predictive coding." IEEE/ACM Transactions on Audio, Speech, and Language Processing 30 (2022): 2002-2014.

[2] Fuchs, Tzeviya Sylvia, and Yedid Hoshen. "Unsupervised word segmentation using temporal gradient pseudo-labels." ICASSP 2023-2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP). IEEE, 2023. 

[3] Fuchs, Tzeviya Sylvia, Yedid Hoshen, and Joseph Keshet. "Unsupervised word segmentation using k nearest neighbors." arXiv preprint arXiv:2204.13094 (2022).

[4] Garofolo, John S. "Timit acoustic phonetic continuous speech corpus." Linguistic Data Consortium, 1993 (1993).

[5] Pitt, Mark A., et al. "Buckeye corpus of conversational speech (2nd release)." Columbus, OH: Department of Psychology, Ohio State University (2007): 265-270.


