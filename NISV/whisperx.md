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
|large-v2 with `float16`|3.34s|4m:32s|7m:00s|2m:53s|14m:28s|14m:56s|
|large-v2 with `float32`|6.30s|8m:10s|6m:59s|2m:55s|18m:10s|18m:32s|
|large-v3 with `float16`|3.16s|4m:15s|6m:42s|2m:53s|13m:53s|14m:20s|
|large-v3 with `float32`|6.59s|8m:03s|6m:55s|2m:54s|17m:58s|18m:21s|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each configuration (**on average**):

|Max. memory / Max. power|Transcriber|Aligner|Diarizer|
|---|---|---|---|
|large-v2 with `float16`|9947 MiB / 249 W|11667 MiB / 233 W|13011 MiB / 207 W|
|large-v2 with `float32`|13940 MiB / 252 W|14364 MiB / 229 W|15727 MiB / 206 W|
|large-v3 with `float16`|9944 MiB / 250 W|11697 MiB / 249 W|13011 MiB / 206 W|
|large-v3 with `float32`|14094 MiB / 254 W|14590 MiB / 248 W|15916 MiB / 207 W|

## Unlabelled data

The batch sizes used:
- `44` for `float16 large-v2`
- `48` for `float16 large-v3`
- `16` for `float32 large-v2/large-v3`

Here's a matrix with the **time** spent by each component of WhisperX, using the various parameter configurations mentioned in the previous page, on the unlabelled data:

|Configuration\Component|Loading|Transcriber|Aligner|Diarizer|Total|Total+Saving to JSON|
|---|---|---|---|---|---|---|
|large-v2 with `float16`|3.19s|13m:45s|11m:04s|11m:30s|36m:22s|36m:28s|
|large-v2 with `float32`|8.00s|20m:27s|11m:26s|11m:38s|43m:39s|43m:40s|
|large-v3 with `float16`|3.18s|14m:28s|11m:12s|11m:38s|37m:21s|37m:26s|
|large-v3 with `float32`|6.38s|20m:11s|11m:07s|11m:27s|42m:51s|42m:53s|

<br>

And also a matrix with the **maximum GPU memory consumption + maximum GPU power usage** of each configuration (**on average**):

|Max. memory / Max. power|Transcriber|Aligner|Diarizer|
|---|---|---|---|
|large-v2 with `float16`|21676 MiB / 268 W|12541 MiB / 295 W|14477 MiB / 277 W|
|large-v2 with `float32`|21657 MiB / 279 W|15355 MiB / 300 W|17291 MiB / 276 W|
|large-v3 with `float16`|22425 MiB / 267 W|12542 MiB / 294 W|14477 MiB / 276 W|
|large-v3 with `float32`|21580 MiB / 279 W|15355 MiB / 298 W|17291 MiB / 276 W|