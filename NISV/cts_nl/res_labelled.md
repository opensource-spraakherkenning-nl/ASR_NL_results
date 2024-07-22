[Go back](./intro_cts_nl.md)

<h2>Results on the labelled audio of Conversational Telephone Speech in the Netherlands</h2>

This data does not reflect the type of content on which the ASR will be applied to in terms of length of the audio, but it offers some rough estimates on the WER performance of the model, particularly in more difficult speech conditions (conversational speech) and when it comes to the time alignment of the word-level timestamps with the reference files.

<br>

For each Whisper implementation, 2 variables have been modified:
- The model version: `large-v2` vs. `large-v3` (to confirm the hypothesis from the UT evaluation)
- The compute type: `float16` vs. `float32`
- **For Huggingface, WhisperX, faster-whisper with batching:** `batch_size`
    - `2` for HF
    - `64` for `WhisperX float16`, `16` for `WhisperX float32`
    - `64` for faster-whisper with batching

The compute type refers to data types used to represent real numbers such as the weights of the Whisper model. In our case, `float16`, also known as **half-precision**, uses 16 bits to store a single floating-point number, whereas `float32`, known as **single-precision**, uses 32 bits to store a single floating-point number. It is known throughout various deep learning applications that `float16` uses less memory and is faster, with the trade-off of loss in accuracy. However, in the case of Whisper, it has been reported that `float16` leads to only a 0.1% increase in WER with the benefit of significantly reducing time and memory required to run the model.

<br>

Here is a matrix with **WER** results of the baseline implementation from OpenAI, as well as different, more optimized implementations:

|Model\Parameters|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|25.9%|25.7%|27.0%|27.0%|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|39.5%|39.8%|34.2%|34.2%|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|25.0%|**24.9%**|26.0%|26.1%|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**24.9%**|**24.9%**|**25.8%**|**25.8%**|
|[WhisperX](https://github.com/m-bain/whisperX/)|31.5%|31.6%|29.8%|29.8%|

<br>

And a matrix with the **time** spent in total by each implementation **to load and transcribe** the dataset:

|Load+transcribe|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|35m:15s|28m:38s|31m:20s|32m:11s|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|21m:00s|14m:10s|17m:09s|20m:59s|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|10m:21s|19m:35s|12m:36s|19m:24s|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**6m:50s**|**11m:45s**|**6m:22s**|**11m:32s**|
|[WhisperX](https://github.com/m-bain/whisperX/)\*|31m:08s|33m:22s|28m:28s|33m:41s|

\* For WhisperX, a separate alignment model based on wav2vec 2.0 has been applied in order to obtain word-level timestamps. Therefore, the time measured contains the time to load the model, time to transcribe, and time to align to generate timestamps. Speaker diarization has also been applied for WhisperX, which is measured separately and covered in [this section](./whisperx.md).

<br>

Here's also a matrix with the **Real-Time Factor or RTF** for short (defined as time to process all of the input divided by the duration of the input) for transcribing **2.18 hours of speech** (rounded to 4 decimals):

|RTF (process time/duration of audio)|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|0.2695|0.2189|0.2396|0.246|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|0.1606|0.1083|0.1311|0.1604|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|0.0791|0.1497|0.0963|0.1483|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**0.0522**|**0.0898**|**0.0487**|**0.0882**|
|[WhisperX](https://github.com/m-bain/whisperX/)\*|0.238|0.2551|0.2176|0.2575|

<br>

Finally, a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each implementation (**on average**):

|Max. memory / Max. power|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|10540 MiB / 220 W|10543 MiB / 260 W|10763 MiB / 207 W|10760 MiB / 258 W|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)*|4670 MiB / **113 W**|8114 MiB / **185 W**|4541 MiB / **118 W**|8020 MiB / **191 W**|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|**3959 MiB** / 190 W|**7212 MiB** / 252 W|**3945 MiB** / 185 W|**7182 MiB** / 252 W|
|[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)*|4600 MiB / 180 W|8000 MiB / 259 W|4600 MiB / 179 W|7998 MiB / 256 W|
|[WhisperX](https://github.com/m-bain/whisperX/)*|9401 MiB / 181 W|12714 MiB / 197 W|9402 MiB / 186 W|12721 MiB / 198 W|

\* For these implementations, batching is supported. Setting a higher `batch_size` will lead to faster inference at the cost of extra memory used.

## Detailed results per pipeline component for WhisperX
[Click here](./whisperx.md)
