this document keeps How-To install and use Speech-to-text model.

first model
first, you need to install gdown to download folder from google drive

```bash
pip install gdown
```
Second, gdown the following link as follow.

```bash
gdown --fuzzy https://drive.google.com/drive/folders/1jiTiYPIdBFce2Ajvf7k7uzui2PGarPdx?usp=drive_link --folder ####Whisper large v3 

gdown --fuzzy https://drive.google.com/drive/folders/1fzJfk-Iy5ywxLiMNaWN-FD6ORH0nuyyK?usp=drive_link --folder #### whisper large v3 Adaptor

gdown --fuzzy https://drive.google.com/drive/folders/172remEcr3yJi3aEhe7KIhvZxejtpuawd?usp=drive_link --folder #### whisper large v3 turbor Adapter

gdown --fuzzy https://drive.google.com/drive/folders/1BpFv_zjL0iDfdmwPvYSxhkkSlFbzJJfW?usp=drive_link --folder #### whisper large v3 turbo
```
or you can download this link folder by folder
```bash
https://drive.google.com/drive/folders/1LA5WwZm8TElhwtBxZ5BRpa_54CqvULht?usp=drive_link
```

> to use model correctly with Adaptor you need to use the rght adaptor with the right model e.g. (whisper large v3 + whisper large v3 adaper). for a finetune_whisper.ipynb you need to use from this repo only.

**if you can not gdown with anyone with the link error you can do this as follow [link](https://github.com/wkentaro/gdown?tab=readme-ov-file#faq)**

```
Google restricts access to a file when the download is concentrated. If you can still access to the file from your browser, downloading cookies file might help. Follow this step: 1) download cookies.txt using browser extensions like (Get cookies.txt LOCALLY); 2) mv the cookies.txt to ~/.cache/gdown/cookies.txt; 3) run download again. If you're using gdown>=5.0.0, it should be able to use the cookies same as your browser.
```






finetuning code will be as follow in finetune_whisper.ipynb


Second model
Thonburian whisper from this link https://github.com/biodatlab/thonburian-whisper
```bash
git clone https://github.com/biodatlab/thonburian-whisper model
```
```python
then run this code to run a model

import torch
from transformers import pipeline

MODEL_NAME = "biodatlab/whisper-th-medium-combined"  # see alternative model names below
lang = "th"
device = 0 if torch.cuda.is_available() else "cpu"
pipe = pipeline(
    task="automatic-speech-recognition",
    model=MODEL_NAME,
    chunk_length_s=30,
    device=device,
)

# Perform ASR with the created pipe.
pipe("audio.mp3", generate_kwargs={"language":"<|th|>", "task":"transcribe"}, batch_size=16)["text"]
```



the example of path directory
```
|--- speech-to-text
    |--- whisper-large-v3
    |--- whisper-large-v3-output
    |--- whisper-turbo-output
    |--- whisper-large-v3-turbo
    |--- finetune_whisper.ipynb
    |--- model ## store honburain whisper
```