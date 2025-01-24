[toc]

# Data Information

## File information

### data

path : './data/'

| file_name             | size        | description                               |
| --------------------- | ----------- | ----------------------------------------- |
| *miRNA_name.npy*      | (1245,)     | All miRNA names.                          |
| *disease_name.npy*    | (2077,)     | All disease names.                        |
| *lncRNA_name.npy*     | (557,)      | All lncRNA names.                         |
| *miRNA_miRNA.npy*     | (1245,1245) | Sequence similarity between miRNAs.       |
| *disease_disease.npy* | (2077,2077) | Semantic similarity of two diseases.      |
| *lncRNA_lncRNA.npy*   | (557,557)   | Sequence similarity between lncRNAs.      |
| *miRNA_disease.npy*   | (1245,2077) | Association between miRNAs and diseases.  |
| *miRNA_lncRNA.npy*    | (1245,557)  | Association between miRNAs and lncRNAs.   |
| *disease_lncRNA.npy*  | (2077,557)  | Association between diseases and lncRNAs. |

### raw_data

path : './data/raw_data/'

| file_name                        | source                                              | description                                                  |
| -------------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| *alldata_v4.xlsx*                | [HMDD](http://www.cuilab.cn/hmdd)                   | HMDD v4.0: The whole dataset of miRNA-disease association data (version 2023.07). Used to generate *miRNA_name.npy*, *disease_name.npy* and *miRNA_disease.npy*. |
| *desc2024.xml*                   | [MeSH](https://www.nlm.nih.gov/mesh/meshhome.html)  | The Medical Subject Headings (MeSH) thesaurus is a controlled and hierarchically-organized vocabulary produced by the National Library of Medicine (version 2024). Used to generate *disease_disease.npy*. |
| *miRNA.dat*                      | [miRBase](https://mirbase.org/)                     | miRBase v22: the archive for microRNA sequences and annotations (version 2019). Used to generate *miRNA_miRNA.npy*. |
| *lncrna-diseases_experiment.txt* | [lncRNASNP](https://guolab.wchscu.cn/lncRNASNP/#!/) | lncRNASNP2: an updated database of functional SNPs and mutations in human and mouse lncRNAs (version 2018). Used to generate *diease_lncRNA.npy*. |
| *mirnas_lncrnas_validated.txt*   | [lncRNASNP](https://guolab.wchscu.cn/lncRNASNP/#!/) | Used to generate *miRNA_lncRNA.npy*.                         |
| *outLncRNA.fa*                   | [NONCODE](http://www.noncode.org/index.php)         | NONCODE v6.0: An integrated knowledge database dedicated to ncRNAs, especially lncRNAs (version 2021).Used to generate *lncRNA_lncRNA.npy*. |

## Process

0. Specific details refer to './data/raw_data/process_data.ipynb'

1. Load raw_data.
2. Eliminate noise, such as synonyms and special symbols '\xa0' in in HMDD v4.0.
2. Align names within database.
2. Merge data for miRNA, disease, and lncRNA.
2. Align names between databases. 
3. Based on miRNA-miRNA, disease-disease, and lncRNA-lncRNA database, to match miRNA, disease, and lncRNA for miRNA-disease, miRNA-lncRNA, and disease-lncRNA. 
3. Screen miRNA-disease, miRNA-lncRNA, and disease-lncRNA by matched miRNA, disease, and lncRNA.
4. Calculating semantic similarity between diseases through directed acyclic graphs. [paper](https://watermark.silverchair.com/bioinformatics_26_13_1644.pdf?token=AQECAHi208BE49Ooan9kkhW_Ercy7Dm3ZL_9Cf3qfKAc485ysgAAA8AwggO8BgkqhkiG9w0BBwagggOtMIIDqQIBADCCA6IGCSqGSIb3DQEHATAeBglghkgBZQMEAS4wEQQMlqnmAcu2p7VAfzM1AgEQgIIDc8OiHvPzWOPifIQn_KgeQpvYIBS8MlljJlQK06sRUAtIseclR6xj4DDP9aYE1oMaAqDVQteRD2_PAYp34ZsUeMtE_pi2gSvTqo2XfT_Nt7UAhKk_-6vRiDlXLWb3ePNSHAd1K6lNwcTzOUSDQSlPghZMW3yoL26Z9Y2ZPpU-t7_N7cBngfNbpWR3PrP3xXGV-hpYzPe5i8gvuleYnh5iUniRFNyZRRrTF61-bbaqKY42uypMhV7R3OkHOcqNc0Ay6vddtsrcAe735rYtunIqueS8F90BDNK7VaO0GJ-Ks7K-QBtsrFJm-WWjBkC-RsFHt_FxY5ksFPS_aT0c2q1414xMoQIEDzx_bN3h4zmz6aSEoz0bxIIIg0HOJlDNZn3Q1iSktdwelk8XHz8MK-e0EO4aOaCC_iTx-NEFFAcsjNyJVLlOBBxt9ulXFer0RNMylqjr-LVolHFLUASTPhusgeQ8Nzy3L2XzbesD2WlW3wDujKDwCzb-rTxPNpANg_e5bTEsZQcZlJflnbKF8CGJ_yJYDXAFGamA2eV2u-f0WudfPDYi0OD3zA9VaPC83ZrwFXixGgA-kwZ0c1hbw-b9dEea09Zvyy89cGPCrGS6xzfsVSS1azivslPjwGHfuJlE1nLqm8mMGuuMngmWi9dbWRbCgX47_CXAx6aHOd8LRahL5_UO1RwTVTlT6FqlKlJZT5zl7OLQCVgDQFd8lPmkfmMfKKGvLVv6KA4KM9vK4ERIxSi9ekPPm2qzrAaoKzoD2ya19jZ8NPTMDt8oy7G4oKaKPA4dpXYcmYAWxEx2i_MbBjc9mAGDhgqXXUcIG-dqWFzsDzaOFrSRz2NEnmDCLpLMpi3E189MJfTi8r1UJX0pLbXqLpE8ECAMKzPE5iMoe1d8Vpad-9zKrAH7iCsWHh2osxSu3oGSP_zeWbr6cz_MK-BuBGZM4Eott0gdomJ5eymb_fLBkYM5ari7Ou7DK2AhGbRQBhJUyqSjvMeabnEAR8uvxgGneP1R1x3DVXfhclbxdgo4b-K41ZbdU3_XK0aG8nhc092OSKzXzC8FBi9-heNQW0rgDbsmusI_0fD3lVzCYfcUufTMAUgZhFOoiQTO5pJmdSxGjbows7N4vg0t4En6RTHgGF0oOHIBWZTfj-P8yZ6E5qf_PMo4aqqE-YgdYTg) 
5. Calculating sequence similarity based on miRNA sequences.
6. Calculating sequence similarity based on lncRNA sequences.

## Environment

* python 3.9.0
* pandas 2.0.1
* numpy 1.23.5
* biopython 1.83

# Training preprocessing 

## File information

path : './data/train_data/'

| file_name        | type | description                                             |
| ---------------- | ---- | ------------------------------------------------------- |
| *common_set.pkl* | dict | Data matrix that does not change with dataset splitting |
| *test_set.pkl*   | dict | Test set.                                               |
| *train_set.pkl*  | dict | Train set.                                              |

### detail

| common_set.key() | type           | size        | description                                                  |
| ---------------- | -------------- | ----------- | ------------------------------------------------------------ |
| 'md'             | tensor.int64   | (1245,2077) | Uncovered miRNA and disease association matrix. sum=23337    |
| 'ml'             | tensor.int64   | (1245,557)  | Uncovered miRNA and lncRNA interaction matrix. sum=1438      |
| 'dl'             | tensor.int64   | (2077,557)  | Uncovered disease and lncRNA association matrix. sum=320     |
| 'mm_seq'         | tensor.float32 | (1245,1245) | The miRNA sequence similarity matrix                         |
| 'dd_sem'         | tensor.float32 | (2077,2077) | The disease semantic similarity matrix                       |
| 'll_seq'         | tensor.float32 | (557,557)   | The lncRNA sequence similarity matrix                        |
| 'mm_mlG'         | tensor.float32 | (1245,1245) | The miRNA GIP kernel similarity matrix by miRNA and lncRNA interaction |
| 'dd_dlG'         | tensor.float32 | (2077,2077) | The disease GIP kernel similarity matrix by disease and lncRNA association |
| 'll_lmG'         | tensor.float32 | (557,557)   | The lncRNA GIP kernel similarity matrix by lncRNA and miRNA interaction |
| 'll_ldG'         | tensor.float32 | (557,557)   | The lncRNA GIP kernel similarity matrix by lncRNA and disease association |
| 'mm_mlF'         | tensor.float32 | (1245,1245) | The miRNA functional similarity matrix by miRNA and lncRNA interaction |
| 'dd_dlF'         | tensor.float32 | (2077,2077) | The disease functional similarity matrix by disease and lncRNA association |
| 'll_ldF'         | tensor.float32 | (557,557)   | The lncRNA functional similarity matrix by lncRNA and disease association |
| 'll_lmF'         | tensor.float32 | (557,557)   | The lncRNA functional similarity matrix by lncRNA and miRNA interaction |

| test_set.key() | type           | size        | description                                                  |
| -------------- | -------------- | ----------- | ------------------------------------------------------------ |
| 'edge'         | tensor.int64   | (517174,2)  | The miRNA and disease edge matrix of test set                |
| 'label'        | tensor.int64   | (517174,)   | The miRNA and disease label matrix of test set               |
| 'md'           | tensor.int64   | (1245,2077) | Covered miRNA and disease association matrix of test set     |
| 'mm_mdG'       | tensor.float32 | (1245,1245) | Covered miRNA GIP kernel similarity matrix of test set by miRNA and disease association |
| 'dd_dmG'       | tensor.float32 | (2077,2077) | Covered disease GIP kernel similarity matrix of test set by disease and miRNA association |
| ‘mm_mdF'       | tensor.float32 | (1245,1245) | Covered miRNA functional similarity matrix of test set by miRNA and disease association |
| 'dd_dmF'       | tensor.float32 | (2077,2077) | Covered disease functional similarity matrix of test set by disease and miRNA association |

| train_set.key()                   | type           | size        | description                                                  |
| --------------------------------- | -------------- | ----------- | ------------------------------------------------------------ |
| 'edge_train_%d'%k  k=[0,1,2,3,4]  | tensor.int64   | (1654952,2) | The miRNA and disease edge matrix of train set of 5 fold     |
| 'label_train_%d'%k  k=[0,1,2,3,4] | tensor.int64   | (1654952,)  | The miRNA and disease label matrix of train set of 5 fold    |
| 'edge_valid_%d'%k  k=[0,1,2,3,4]  | tensor.int64   | (413739,2)  | The miRNA and disease edge matrix of valid set of 5 fold     |
| 'label_valid_%d'%k  k=[0,1,2,3,4] | tensor.int64   | (413739,)   | The miRNA and disease label matrix of valid set of 5 fold    |
| 'md_%d'%k  k=[0,1,2,3,4]          | tensor.int64   | (1245,2077) | Covered miRNA and disease association matrix of train set of 5 fold |
| 'mm_mdG_%d'%k  k=[0,1,2,3,4]      | tensor.float32 | (1245,1245) | Covered miRNA GIP kernel similarity matrix of train set by miRNA and disease association |
| 'dd_dmG_%d'%k  k=[0,1,2,3,4]      | tensor.float32 | (2077,2077) | Covered disease GIP kernel similarity matrix of train set by disease and miRNA association |
| 'mm_mdF_%d'%k  k=[0,1,2,3,4]      | tensor.float32 | (1245,1245) | Covered miRNA functional similarity matrix of train set by miRNA and disease association |
| 'dd_dmF_%d'%k  k=[0,1,2,3,4]      | tensor.float32 | (2077,2077) | Covered disease functional similarity matrix of train set by disease and miRNA association |

## Process

0. Specific details refer to './data/train_data/process_data.ipynb'
1. Set hyperparameter. $^{1}$ 
2. Load data.
3. Calculate the data matrices that does not change with dataset splitting.
4. Split dataset. $^{2}$ 
5. Calculate the test data matrices.
6. Calculate the test data matrices.

```markdown
1. Hyperparameter description
kfolds :(int) k-fold cross validation
train_ratio :(float) The ratio of training set in total set
seed :(int) random seed
no_cuda :(bool) whether to use GPU
```

```markdown
2. Dataset splitting description
**split train & test set**
|-------------------- -----| : |total set|
|--------------------|-----| : |train set|test set|
**5 fold for train set**
|####----------------|
|----####------------|
|--------####--------|
|------------####----|
|----------------####|
'#' : valid set sample
'-' : train set sample
```

## Environment

* python 3.10.12
* numpy 1.25.0
* scikit-learn 1.3.0

# Author's message

I am AntarcticaLu. Hahaha...