[Back to homepage](../../index.md)

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
|large-v2 with `float16`|79.98s|7m:16s|22m:32s|4m:22s|35m:30s|36m:14s|
|large-v2 with `float32`|82.74s|12m:31s|19m:28s|4m:14s|37m:36s|38m:10s|
|large-v3 with `float16`|78.02s|7m:07s|20m:03s|4m:17s|32m:45s|33m:26s|
|large-v3 with `float32`|53.35s|12m:35s|20m:13s|4m:16s|37m:57s|39m:04s|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each configuration (**on average**):

|Max. memory / Max. power|Transcriber|Aligner|Diarizer|
|---|---|---|---|
|large-v2 with `float16`|9401 MiB / 181 W|11282 MiB / 171 W|12091 MiB / 122 W|
|large-v2 with `float32`|12714 MiB / 197 W|13937 MiB / 164 W|14925 MiB / 140 W|
|large-v3 with `float16`|9402 MiB / 186 W|11114 MiB / 178 W|12096 MiB / 138 W|
|large-v3 with `float32`|12721 MiB / 198 W|14009 MiB / 166 W|15916 MiB / 136 W|

## Unlabelled data

The batch sizes used:
- `48` for `float16`
- `16` for `float32`

Here's a matrix with the **time** spent by each component of WhisperX, using the various parameter configurations mentioned in the previous page, on the unlabelled data:

|Configuration\Component|Loading|Transcriber|Aligner|Diarizer|Total|Total+Saving to JSON|
|---|---|---|---|---|---|---|
|large-v2 with `float16`|77.50s|8m:58s|11m:14s|7m:34s|29m:03s|29m:59s|
|large-v2 with `float32`|57.55s|12m:28s|8m:49s|6m:53s|29m:07s|29m:22s|
|large-v3 with `float16`|62.37s|9m:00s|10m:26s|7m:29s|27m:57s|28m:09s|
|large-v3 with `float32`|7.47s|12m:15s|9m:14s|6m:55s|28m:31s|28m:34s|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each configuration (**on average**):

|Max. memory / Max. power|Transcriber|Aligner|Diarizer|
|---|---|---|---|
|large-v2 with `float16`|19053 MiB / 257 W|12354 MiB / 289 W|14289 MiB / 275 W|
|large-v2 with `float32`|22013 MiB / 276 W|15200 MiB / 288 W|17135 MiB / 275 W|
|large-v3 with `float16`|19096 MiB / 256 W|12514 MiB / 290 W|14289 MiB / 275 W|
|large-v3 with `float32`|22042 MiB / 276 W|15200 MiB / 294 W|17135 MiB / 274 W|