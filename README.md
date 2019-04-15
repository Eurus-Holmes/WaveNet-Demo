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

```

### 1. Preprocessing
