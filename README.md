# MT Tutorial for the JSALT 2019 Summer School

This is the Machine Translation tutorial given at the 2019 JSALT summer school.

forked.

For Google Colaboratory

## Clone

```sh
git clone https://github.com/forest1040/jsalt-2019-mt-tutorial.git
```

## Setup

```sh
sudo pip3 install torch
sudo pip3 install tqdm
sudo pip3 install sentencepiece
sudo pip3 install sacrebleu
```

## get data

```sh
wget http://www.phontron.com/kftt/download/kftt-data-1.0.tar.gz
tar zxvf kftt-data-1.0.tar.gz
mv kftt-data-1.0/data/orig/ jsalt-2019-mt-tutorial/data
```

## Subwords

### subwords-model 作成

```sh
python3 lab/subwords.py train \
    --model_prefix data/subwords \
    --vocab_size 16000 \
    --model_type bpe \
    --input data/kyoto-train.en,data/kyoto-train.ja
```

### Train データの subwords 化

```sh
cat data/kyoto-train.en | python3 lab/subwords.py segment --model data/subwords.model > data/kyoto-train.bpe.en
cat data/kyoto-train.ja | python3 lab/subwords.py segment --model data/subwords.model > data/kyoto-train.bpe.ja
cat data/kyoto-test.en | python3 lab/subwords.py segment --model data/subwords.model > data/kyoto-test.bpe.en
cat data/kyoto-test.ja | python3 lab/subwords.py segment --model data/subwords.model > data/kyoto-test.bpe.ja
```

## Train

```sh
python3 lab/training.py \
    --cuda \
    --n-layers 4 \
    --n-heads 4 \
    --embed-dim 512 \
    --hidden-dim 512 \
    --dropout 0.1 \
    --lr 2e-4 \
    --n-epochs 15 \
    --tokens-per-batch 8000 \
    --clip-grad 1.0
```
```sh
sudo python3 lab/training.py \
    --cuda \
    --n-layers 6 \
    --n-heads 8 \
    --embed-dim 512 \
    --hidden-dim 2048 \
    --dropout 0.1 \
    --lr 2e-4 \
    --n-epochs 4 \
    --tokens-per-batch 8000 \
    --clip-grad 1.0

```