[Back to homepage](../index.md)

## Detailed results for WhisperX

[**WhisperX**](https://github.com/m-bain/whisperX/) is an implementation of Whisper with support for batching, word/character level time alignment using wav2vec 2.0, and speaker diarization.

There are 4 components/parts that we can define: **loading** Whisper + speaker diarization module, the **transcriber** (the part where Whisper runs to generate the text transcription without any timestamps), the **aligner** (generates the word-level timestamps using wav2vec 2.0), and the **diarizer** (identifies the speaker per segment and per word by assigning speaker IDs).

Due to the wav2vec 2.0 based aligner which doesn't support aligning digits and currency symbols, numbers and currencies have been converted to their written form by setting `suppress_numerals=True`. In addition, the [original aligner](https://huggingface.co/jonatasgrosman/wav2vec2-large-xlsr-53-dutch) used in WhisperX, based on XLSR-53, has been replaced with an [aligner based on XLS-R](https://huggingface.co/jonatasgrosman/wav2vec2-xls-r-1b-dutch). This was done because the original aligner struggled with aligning some characters that are less common in Dutch, but part of the orthography of it (mainly accents on vowels). This might have led to more time spent on aligning compared to the XLSR-53 version, but an ablation study is planned for future work to confirm this hypothesis.

<br>

Two variables have been experimented with:
- The model version: `large-v2` vs. `large-v3` (to confirm the hypothesis from the UT evaluation)
- The compute type: `float16` vs. `float32` (check [here](./res_labelled.md) for more details about this parameter)

## Labelled data

The batch size used is `64` for `float16` and `16` for `float32`.

Here's a matrix with the **time** spent by each component of WhisperX, using the various parameter configurations mentioned in the previous page, on the labelled data:

|Configuration\Component|Loading|Transcriber|Aligner|Diarizer|Total|Total+Saving to JSON|
|---|---|---|---|---|---|---|
|large-v2 with `float16`|7.73s|4m:17s|6m:53s|3m:58s|15m:16s|15m:45s|
|large-v2 with `float32`|10.51s|8m:07s|7m:36s|4m:01s|19m:54s|20m:26s|
|large-v3 with `float16`|3.21s|4m:14s|7m:11s|4m:01s|15m:29s|16m:01s|
|large-v3 with `float32`|6.12s|8m:00s|6m:59s|4m:00s|19m:05s|19m:36s|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each configuration (**on average**):

|Max. memory / Max. power|Transcriber|Aligner|Diarizer|
|---|---|---|---|
|large-v2 with `float16`|9419 MiB / 246 W|11916 MiB / 227 W|13578 MiB / 229 W|
|large-v2 with `float32`|13548 MiB / 249 W|14749 MiB / 234 W|16480 MiB / 234 W|
|large-v3 with `float16`|9417 MiB / 243 W|11918 MiB / 235 W|13605 MiB / 231 W|
|large-v3 with `float32`|13539 MiB / 247 W|14715 MiB / 232 W|16411 MiB / 228 W|

## Unlabelled data

The batch size used is `48` for `float16` and `16` for `float32`

Here's a matrix with the **time** spent by each component of WhisperX, using the various parameter configurations mentioned in the previous page, on the unlabelled data:

|Configuration\Component|Loading|Transcriber|Aligner|Diarizer|Total|Total+Saving to JSON|
|---|---|---|---|---|---|---|
|large-v2 with `float16`|2.35s|15m:23s|11m:34s|12m:18s|39m:17s|39m:25s|
|large-v2 with `float32`|6.48s|20m:35s|11m:21s|11m:51s|43m:53s|44m:01s|
|large-v3 with `float16`|4.79s|15m:23s|11m:37s|12m:10s|39m:15s|39m:21s|
|large-v3 with `float32`|7.27s|20m:22s|11m:21s|11m:55s|43m:45s|43m:52s|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each configuration (**on average**):

|Max. memory / Max. power|Transcriber|Aligner|Diarizer|
|---|---|---|---|
|large-v2 with `float16`|22273 MiB / 268 W|12649 MiB / 298 W|14502 MiB / 277 W|
|large-v2 with `float32`|21375 MiB / 281 W|15381 MiB / 294 W|17316 MiB / 278 W|
|large-v3 with `float16`|22142 MiB / 267 W|12977 MiB / 296 W|14502 MiB / 278 W|
|large-v3 with `float32`|21298 MiB / 279 W|15381 MiB / 297 W|17316 MiB / 276 W|