# Dealing with Typos for BERT-based Passage Retrieval and Ranking

Code, data and results for the paper ``Dealing with Typos for BERT-based Passage Retrieval and Ranking" submitted for review to EMNLP 2021.


## Install
To install the required dependencies run `pip install -r requirements.txt`.

## Dataset
We evaluate our typos-aware training strategy on the MS MARCO passage ranking dataset. 

To download the data required by this repo (`qidpidtriples.train.full.tsv.gz`, `collection.tsv`, `queries.train.tsv`,`qrels.train.tsv`,`queries.dev.small.tsv`,`qrels.dev.small.tsv`), we refer to [the official github repo for this dataset](https://github.com/microsoft/MSMARCO-Passage-Ranking).

We provide the synthetic typo queries generated for the experiments reported in the paper in the `./data` folder. You also can generate typo queries yourself:

```
python ./BERT_re-ranker/tools/make_typo_queries.py
```

Note the queries you will generated may differ from those used in the paper because our typos generation is a stochastic process.

## Train Dense Retriever (DR) Models
The code for reproducing the DR models used in our paper is in the `./DR` folder.
We use an open-source implementation forked (anonymously) from the [RepBERT-Index repository](https://github.com/jingtaozhan/RepBERT-Index).

To train DR with standard training settings, `cd` into the `./DR` folder and follow the instructions from the original repository.

To train typos-aware DR, run the following command without changing any other parameter:
 
```
python ./train.py --task train --insert_typo 1 --evaluate_during_training
```

## Train BERT re-ranker Models
The code for reproducing the BERT re-ranker models used in our paper is in the `./BERT_re-ranker` folder. 

To train the BERT re-ranker with standard training settings, `cd` into the `./BERT_re-ranker` folder and run:

```
python ./train_cross_encoder.py --training_setting standard
```

To train the BERT re-ranker with typos-aware training, run:

```
python ./train_cross_encoder.py --training_setting typos-aware
```



