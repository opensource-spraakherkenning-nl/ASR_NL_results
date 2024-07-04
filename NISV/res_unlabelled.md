[Back to homepage](../index.md)

<h2>Computational performance on the unlabelled audio of Broadcast News in the Netherlands</h2>

More details about the parameters and the dataset can be found [here](./res_labelled.md).

<br>

For each Whisper implementation, 2 variables have been modified:
- The model version: `large-v2` vs. `large-v3` (to confirm the hypothesis from the UT evaluation)
- The compute type: `float16` vs. `float32` (check [here](./res_labelled.md) for more details about this parameter)

<br>

**TODO: Add results**

<!-- <br>

Here's a matrix with the **time** spent in total by each implementation **to load and transcribe** the data:

|Model\Parameters|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|36m:06s|32m:41s|42m:08s|30m:25s|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)|21m:48s|19m:13s|23m:22s|22m:02s|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|11m:40s|22m:27s|11m:18s|21m:56s|
|[WhisperX](https://github.com/m-bain/whisperX/)*|11m:17s|15m:54s|11m:29s|15m:05s|

\* For WhisperX, a separate alignment model based on wav2vec 2.0 has been applied in order to obtain word-level timestamps. Therefore, the time measured contains the time to load the model, time to transcribe, and time to align to generate timestamps. Speaker diarization has also been applied for WhisperX, which is measured separately and covered in a different section.

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each implementation (**on average**):

|Max. memory / Max. power|large-v2 with `float16`|large-v2 with `float32`|large-v3 with `float16`|large-v3 with `float32`|
|---|---|---|---|---|
|[OpenAI](https://github.com/openai/whisper)|10621 MiB / 240 W|10639 MiB / 264 W|10927 MiB / 238 W|10941 MiB / 266 W|
|[Huggingface (`transformers`)](https://huggingface.co/openai/whisper-large-v2#long-form-transcription)*|15073 MiB / 141 W|12981 MiB / 215 W|14566 MiB / 123 W|19385 MiB / 235 W|
|[faster-whisper](https://github.com/SYSTRAN/faster-whisper/)|8576 MiB / 188 W|11694 MiB / 235 W|8567 MiB / 195 W|6942 MiB / 237 W|
|[WhisperX](https://github.com/m-bain/whisperX/)*|9419 MiB / 246 W|13548 MiB / 249 W|9417 MiB / 243 W|13539 MiB / 247 W|

\* For these implementations, batching is supported. Setting a higher `batch_size` will lead to faster inference at the cost of extra memory used.

## Detailed results per pipeline component for WhisperX
Go [here]().

## Hardware setup

A high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia Quadro RTX 6000 with 24 GiB VRAM each, using CUDA version 12.4, with an Intel(R) Xeon(R) Gold 5220 CPU @ 2.20GHz and 256 GB of RAM available.

The OS installed on the cluster is [RHEL 9.3](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/9.3_release_notes/index). -->

