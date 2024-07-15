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
    - For **WhisperX**:
        - `44` for `float16 large-v2`
        - `48` for `float16 large-v3`
        - `16` for `float32 large-v2/large-v3`
    - For `faster-whisper w/ batching`:
        - `40` for `float16`
        - `16` for `float32`

<br>

Here's a matrix with the **time** spent in total by each implementation **to load and transcribe** the data:

|Model\Parameters|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|1h:43m:47s|1h:20m:29s|1h:57m:06s|1h:28m:50s|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|43m:05s|1h:05m:17s|41m:39s|1h:01m:45s|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|38m:52s|1h:17m:38s|39m:26s|1h:24m:21s|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**12m:31s**|**23m:35s**|**10m:50s**|**22m:17s**|
|[WhisperX](https://github.com/m-bain/whisperX/)*|24m:52s|32m:01s|25m:42s|31m:24s|

\* For WhisperX, a separate alignment model based on wav2vec 2.0 has been applied in order to obtain word-level timestamps. Therefore, the time measured contains the time to load the model, time to transcribe, and time to align to generate timestamps. Speaker diarization has also been applied for WhisperX, which is measured separately and covered in a different section.

<br>

Here's also a matrix with the **Real-Time Factor or RTF** for short (defined as time to process all of the input divided by the duration of the input) for transcribing **9.02 hours of speech** (rounded to 4 decimals):

|RTF (process time/duration of audio)|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|0.1918|0.1487|0.2164|0.1641|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|0.0796|0.1206|0.077|0.1141|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|0.0718|0.1434|0.0728|0.1559|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**0.0231**|**0.0436**|**0.02**|**0.0412**|
|[WhisperX](https://github.com/m-bain/whisperX/)\*|0.0459|0.0592|0.0475|0.058|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each implementation (**on average**):

|Max. memory / Max. power|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|10943 MiB / 274 W|10955 MiB / 293 W|11094 MiB / 279 W|11164 MiB / 291 W|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)*|16629 MiB / 269 W|18563 MiB / 287 W|12106 MiB / **259 W**|15061 MiB / 288 W|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|**4811 MiB** / 269 W|**8519 MiB** / 286 W|**4865 MiB** / 267 W|**9179 MiB** / 282 W|
|[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)|19025 MiB / 270 W|19873 MiB / 281 W|18919 MiB / 266 W|19845 MiB / 282 W|
|[WhisperX](https://github.com/m-bain/whisperX/)*|21676 MiB / **268 W**|21657 MiB / **279 W**|22425 MiB / 267 W|21580 MiB / **279 W**|

\* For these implementations, batching is supported. Setting a higher `batch_size` will lead to faster inference at the cost of extra memory used.

## Detailed results per pipeline component for WhisperX
[Click here](./whisperx.md)

## Hardware setup

A high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia Quadro RTX 6000 with 24 GiB VRAM each, using CUDA version 12.4, with an Intel(R) Xeon(R) Gold 5220 CPU @ 2.20GHz and 256 GB of RAM available.

The OS installed on the cluster is [RHEL 9.3](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/9.3_release_notes/index). -->
