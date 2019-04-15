# WaveNet-Demo

### Reference: [WaveNet vocoder](https://github.com/r9y9/wavenet_vocoder)

----
## Installation

```shell
git clone https://github.com/r9y9/wavenet_vocoder
cd wavenet_vocoder
pip install -e ".[train]"
```

----
## Getting started

### 0. Download dataset
  - CMU ARCTIC (en): http://festvox.org/cmu_arctic/

```shell
cd ~
mkdir data
vim download_cmu_arctic.sh
```

  - [download_cmu_arctic.sh](https://github.com/Eurus-Holmes/WaveNet-Demo/blob/master/download_cmu_arctic.sh)

```shell
chmod a+x download_cmu_arctic.sh
./download_cmu_arctic.sh
```

  - LJSpeech (en): https://keithito.com/LJ-Speech-Dataset/
  
```shell
wget -c https://data.keithito.com/data/speech/LJSpeech-1.1.tar.bz2
tar -jxvf LJSpeech-1.1.tar.bz2
rm LJSpeech-1.1.tar.bz2
```

### 1. Preprocessing

```
python preprocess.py cmu_arctic ~/data/cmu_arctic ./data/cmu_arctic --preset=presets/cmu_arctic_8bit.json
```

----
Usage:

```
python preprocess.py ${dataset_name} ${dataset_path} ${out_dir} --preset=<json>
```

Supported `${dataset_name}`s for now are

  - `cmu_arctic` (multi-speaker)
  - `ljspeech` (single speaker)
Assuming you use preset parameters known to work good for CMU ARCTIC dataset and have data in `~/data/cmu_arctic`, 
then you can preprocess data by:

```
python preprocess.py cmu_arctic ~/data/cmu_arctic ./data/cmu_arctic --preset=presets/cmu_arctic_8bit.json
```

When this is done, you will see time-aligned extracted features (pairs of audio and mel-spectrogram) in `./data/cmu_arctic.`

----
### 2. Training

  - Training un-conditional WaveNet

```shell
python train.py --data-root=./data/cmu_arctic/ --hparams="cin_channels=-1,gin_channels=-1"
```
You have to disable global and local conditioning by setting gin_channels and cin_channels to negative values.

  - Training WaveNet conditioned on mel-spectrogram

```shell
python train.py --data-root=./data/cmu_arctic/ --speaker-id=0 \
    --hparams="cin_channels=80,gin_channels=-1"
```

  - Training WaveNet conditioned on mel-spectrogram and speaker embedding

```shell
python train.py --data-root=./data/cmu_arctic/ \
    --hparams="cin_channels=80,gin_channels=16,n_speakers=7"
```

----
> Note: for multi gpu training, you have better ensure that batch_size % num_gpu == 0

Usage:

```shell
python train.py --data-root=${data-root} --preset=<json> --hparams="parameters you want to override"
```

Important options:

  - `--speaker-id=<n>`: (Multi-speaker dataset only) it specifies which speaker of data we use for training. If this is not specified, all training data are used. This should only be specified when you are dealing with a multi-speaker dataset. For example, if you are trying to build a speaker-dependent WaveNet vocoder for speaker `awb` of CMU ARCTIC, then you have to specify `--speaker-id=0`. Speaker ID is automatically assigned as follows:

```python
In [1]: from nnmnkwii.datasets import cmu_arctic

In [2]: [(i, s) for (i,s) in enumerate(cmu_arctic.available_speakers)]
Out[2]:

[(0, 'awb'),
 (1, 'bdl'),
 (2, 'clb'),
 (3, 'jmk'),
 (4, 'ksp'),
 (5, 'rms'),
 (6, 'slt')]
```

  - Training un-conditional WaveNet

```shell
python train.py --data-root=./data/cmu_arctic/ --hparams="cin_channels=-1,gin_channels=-1"
```
You have to disable global and local conditioning by setting gin_channels and cin_channels to negative values.

  - Training WaveNet conditioned on mel-spectrogram

```shell
python train.py --data-root=./data/cmu_arctic/ --speaker-id=0 \
    --hparams="cin_channels=80,gin_channels=-1"
```

  - Training WaveNet conditioned on mel-spectrogram and speaker embedding

```shell
python train.py --data-root=./data/cmu_arctic/ \
    --hparams="cin_channels=80,gin_channels=16,n_speakers=7"
```

----




