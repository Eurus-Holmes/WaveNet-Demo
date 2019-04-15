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


