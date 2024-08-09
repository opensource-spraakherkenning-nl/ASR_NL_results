[**Go back**](./intro_cts_nl.md)

<h2>Computational performance on the unlabelled audio of Broadcast News in the Netherlands</h2>

The unlabelled data is considered to be long-form (one audio file that lasts for a longer period) which reflects more closely the type of data found in audiovisual/oral history archives. Thus, even if the WER is not calculated (due to the lack of complete labelling for this subset), the computational performance information will give us a better estimate of each implementation's performance when applied to longer individual audio files

More details about the parameters and the dataset can be found [here](./res_labelled.md).

<br>

For each Whisper implementation, 2 variables have been modified:
- The model version: `large-v2` vs. `large-v3` (to confirm the hypothesis from the UT evaluation)
- The compute type: `float16` vs. `float32` (check [here](./res_labelled.md) for more details about this parameter)
- For Huggingface (HF) and WhisperX: `batch_size`
    - `4` for `HF float16`, `2` for `HF float32`
    - `48` for `WhisperX float16`, `16` for `WhisperX float32`
    - For `faster-whisper w/ batching`:
        - `40` for `float16`
        - `16` for `float32`

<br>

Here's a matrix with the **time** spent in total by each implementation **to load and transcribe** the data:

|Model\Parameters|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|1h:12m:12s|57m:12s|1h:28m:55s|1h:09m:57s|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|38m:54s|1h:03m:06s|28m:21s|49m:05s|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|27m:53s|56m:13s|31m:50s|1h:02m:38s|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**7m:44s**|**14m:46s**|**6m:39s**|**13m:43s**|
|[WhisperX](https://github.com/m-bain/whisperX/)*|21m:29s|22m:14s|20m:28s|21m:36s|

\* For WhisperX, a separate alignment model based on wav2vec 2.0 has been applied in order to obtain word-level timestamps. Therefore, the time measured contains the time to load the model, time to transcribe, and time to align to generate timestamps. Speaker diarization has also been applied for WhisperX, which is measured separately and covered in a different section.

<br>

Here's also a matrix with the **Real-Time Factor or RTF** for short (defined as time to process all of the input divided by the duration of the input) for transcribing **5.69 hours of speech** (rounded to 4 decimals):

|RTF (process time/duration of audio)|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|0.2115|0.1675|0.2604|0.2049|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|0.1139|0.1848|0.083|0.1835|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|0.0817|0.1647|0.0932|0.1559|
|**[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)**|**0.0227**|**0.0433**|**0.0195**|**0.0402**|
|[WhisperX](https://github.com/m-bain/whisperX/)\*|0.0629|0.0651|0.0599|0.0633|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each implementation (**on average**):

|Max. memory / Max. power|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|10842 MiB / 276 W|11090 MiB / 290 W|10952 MiB / 278 W|10997 MiB / 286 W|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)*|11631 MiB / **215 W**|19850 MiB / 283 W|7566 MiB / **202 W**|14328 MiB / 283 W|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|**4761 MiB** / 261 W|**8684 MiB** / 283 W|**5106 MiB** / 266 W|**9285 MiB** / 281 W|
|[faster-whisper w/ batching](https://github.com/SYSTRAN/faster-whisper/pull/856)|15308 MiB / 266 W|18198 MiB / 278 W|15279 MiB / 266 W|18147 MiB / 277 W|
|[WhisperX](https://github.com/m-bain/whisperX/)*|19053 MiB / 257 W|22013 MiB / **276 W**|19096 MiB / 256 W|22042 MiB / **276 W**|

\* For these implementations, batching is supported. Setting a higher `batch_size` will lead to faster inference at the cost of extra memory used.

## Detailed results per pipeline component for WhisperX
[Click here](./whisperx.md)
