[Back to homepage](../index.md)

<h2>Computational performance on the unlabelled audio of Broadcast News in the Netherlands</h2>

The unlabelled data is considered to be long-form (one audio file that lasts for a longer period) which reflects more closely the type of data found in audiovisual/oral history archives. Thus, even if the WER is not calculated (due to the lack of complete labelling for this subset), the computational performance information will give us a better estimate of each implementation's performance when applied to longer individual audio files

More details about the parameters and the dataset can be found [here](./res_labelled.md).

<br>

For each Whisper implementation, 2 variables have been modified:
- The model version: `large-v2` vs. `large-v3` (to confirm the hypothesis from the UT evaluation)
- The compute type: `float16` vs. `float32` (check [here](./res_labelled.md) for more details about this parameter)
- For Huggingface (HF) and WhisperX: `batch_size`
    - `4` for `HF float16`, `2` for `HF float32`
    - `64/48` for `WhisperX float16 labelled/unlabelled`, `16` for `WhisperX float32`

<br>

Here's a matrix with the **time** spent in total by each implementation **to load and transcribe** the data:

|Model\Parameters|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|1h:43m:47s|1h:20m:29s|1h:57m:06s|1h:28m:50s|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|43m:05s|1h:05m:17s|41m:39s|1h:01m:45s|
|**[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)**|**4m:14s**|**4m:26s**|**3m:36s**|**5m:07s**|
|[WhisperX](https://github.com/m-bain/whisperX/)*|26m:57s|31m:57s|27m:00s|31m:43s|

\* For WhisperX, a separate alignment model based on wav2vec 2.0 has been applied in order to obtain word-level timestamps. Therefore, the time measured contains the time to load the model, time to transcribe, and time to align to generate timestamps. Speaker diarization has also been applied for WhisperX, which is measured separately and covered in a different section.

<br>

As well as the **time** spent in total by **faster-whisper** and **WhisperX** to **load, transcribe + save the output to files\***:

|Load+transcribe+save output|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|39m:59s|1h:18m:34s|40m:07s|1h:23m:07s|
|**[WhisperX](https://github.com/m-bain/whisperX/)\*\***|**39m:25s**|**44m:01s**|**39m:21s**|**43m:52s**|

\* It has been noticed after benchmarking that, for these 2 implementations, saving the output takes unusually long.

\** For WhisperX, this includes the entire pipeline (loading -> transcription -> alignment -> speaker diarization -> saving to file).

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each implementation (**on average**):

|Max. memory / Max. power|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|10943 MiB / 274 W|10955 MiB / 293 W|11094 MiB / 279 W|11164 MiB / 291 W|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)*|16629 MiB / 269 W|18563 MiB / 287 W|12106 MiB / 259 W|15061 MiB / 288 W|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|3789 MiB / 156 W|6813 MiB / 191 W|3750 MiB / 160 W|6953 MiB / 200 W|
|[WhisperX](https://github.com/m-bain/whisperX/)*|22273 MiB / 268 W|21375 MiB / 281 W|22142 MiB / 267 W|21298 MiB / 279 W|

\* For these implementations, batching is supported. Setting a higher `batch_size` will lead to faster inference at the cost of extra memory used.

## Detailed results per pipeline component for WhisperX
[Click here](./whisperx.md)

## Hardware setup

A high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia Quadro RTX 6000 with 24 GiB VRAM each, using CUDA version 12.4, with an Intel(R) Xeon(R) Gold 5220 CPU @ 2.20GHz and 256 GB of RAM available.

The OS installed on the cluster is [RHEL 9.3](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/9.3_release_notes/index). -->
