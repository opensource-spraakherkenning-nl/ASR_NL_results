[Back to homepage](../index.md)

<h2>Results on the labelled audio of Broadcast News in the Netherlands</h2>

The N-Best 2008 Dutch Evaluation corpus is a corpus designed to evaluate Dutch/Flemish Speech Recognition systems in 2008. The corpus consists of 4 subsets:
- `bn_nl`: Broadcast News programmes in the Netherlands;
- `cts_nl`: Conversational Telephone Speech in the Netherlands;
- `bn_vl`: Broadcast News programmes in Belgium;
- `cts_vl`: Conversational Telephone Speech in Belgium.

For more details about the corpus, click [here](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=32b10cb0f4cb99ba934f5be5066638a5ad9b19f2).

**The subset used in this benchmark is `bn_nl` (Broadcast News programmes in the Netherlands).**

This data does not reflect the type of content on which the ASR will be applied to in terms of length of the audio, but it offers some rough estimates on the WER performance of the model, particularly when it comes to the time alignment of the word-level timestamps with the reference files.

<br>

For each Whisper implementation, 2 variables have been modified:
- The model version: `large-v2` vs. `large-v3` (to confirm the hypothesis from the UT evaluation)
- The compute type: `float16` vs. `float32`
- **For Huggingface and WhisperX:** `batch_size`
    - `2` for HF
    - `64` for `WhisperX float16`, `16` for `WhisperX float32`

The compute type refers to data types used to represent real numbers such as the weights of the Whisper model. In our case, `float16`, also known as **half-precision**, uses 16 bits to store a single floating-point number, whereas `float32`, known as **single-precision**, uses 32 bits to store a single floating-point number. It is known throughout various deep learning applications that `float16` uses less memory and is faster, with the trade-off of loss in accuracy. However, in the case of Whisper, it has been reported that `float16` leads to only a 0.1% increase in WER with the benefit of significantly reducing time and memory required to run the model.

<br>

Here is a matrix with **WER** results of the baseline implementation from OpenAI, as well as different, more optimized implementations:

|Model\Parameters|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|11.1%|11.0%|12.9%|13.2%|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|17.1%|16.9%|16.6%|16.6%|
|**[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)**|**10.3%**|**10.2%**|**11.8%**|**11.8%**|
|[WhisperX](https://github.com/m-bain/whisperX/)|12.3%|12.4%|13.0%|12.9%|

<br>

And a matrix with the **time** spent in total by each implementation **to load and transcribe** the dataset:

|Load+transcribe|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|36m:06s|32m:41s|42m:08s|30m:25s|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|21m:48s|19m:13s|23m:22s|22m:02s|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|11m:40s|22m:27s|**11m:18s**|21m:56s|
|**[WhisperX](https://github.com/m-bain/whisperX/)\***|**11m:17s**|**15m:54s**|11m:29s|**15m:05s**|

\* For WhisperX, a separate alignment model based on wav2vec 2.0 has been applied in order to obtain word-level timestamps. Therefore, the time measured contains the time to load the model, time to transcribe, and time to align to generate timestamps. Speaker diarization has also been applied for WhisperX, which is measured separately and covered in [this section](./whisperx.md).

<br>

Finally, a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each implementation (**on average**):

|Max. memory / Max. power|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|10621 MiB / 240 W|**10639 MiB** / 264 W|10927 MiB / 238 W|10941 MiB / 266 W|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)*|15073 MiB / **141 W**|12981 MiB / **215 W**|14566 MiB / **123 W**|19385 MiB / **235 W**|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|**8576 MiB** / 188 W|11694 MiB / 235 W|**8567 MiB** / 195 W|**6942 MiB** / 237 W|
|[WhisperX](https://github.com/m-bain/whisperX/)*|9419 MiB / 246 W|13548 MiB / 249 W|9417 MiB / 243 W|13539 MiB / 247 W|

\* For these implementations, batching is supported. Setting a higher `batch_size` will lead to faster inference at the cost of extra memory used.

## Detailed results per pipeline component for WhisperX
[Click here](./whisperx.md)

## Hardware setup

A high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia Quadro RTX 6000 with 24 GiB VRAM each, using CUDA version 12.4, with an Intel(R) Xeon(R) Gold 5220 CPU @ 2.20GHz and 256 GB of RAM available.

The OS installed on the cluster is [RHEL 9.3](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/9.3_release_notes/index).

