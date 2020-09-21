# MT Tutorial for the JSALT 2019 Summer School

This is the Machine Translation tutorial given at the 2019 JSALT summer school.

forked.

## Setup For Google Colaboratory

```sh
sudo pip3 install torch
sudo pip3 install tqdm
sudo pip3 install sentencepiece
sudo pip3 install sacrebleu
```

## get data

```sh
wget http://www.phontron.com/kftt/download/kftt-data-1.0.tar.gz
```

## Subwords

```sh
python lab/subwords.py train \
    --model_prefix data/subwords \
    --vocab_size 16000 \
    --model_type bpe \
    --input data/train.en,data/train.fr

```
