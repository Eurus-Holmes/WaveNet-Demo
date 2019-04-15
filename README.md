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
  - LJSpeech (en): https://keithito.com/LJ-Speech-Dataset/

```shell
cd ~
mkdir data
vim download_cmu_arctic.sh
```

```

### 1. Preprocessing
