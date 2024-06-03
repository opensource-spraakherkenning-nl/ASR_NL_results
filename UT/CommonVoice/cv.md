[Back to homepage](../../index.md)

<h2>Common Voice</h2>

Common Voice is a crowdsourced and open initiative to create a multilingual speech dataset. Users can record themselves speaking an utterance and also review the utterances others have spoken via an upvote/downvote system to ensure that recordings correspond to the given prompts and are of sufficient audio quality. For more information about the project, check [the official website](https://commonvoice.mozilla.org).

Multiple versions of the dataset are available, released by Mozilla every few months. The **test** subset has been evaluated and the version used in this benchmark is **17.0**, which contains around 15 hours of speech for the test set.

<br>

Here is a matrix with **WER** results and the **time** each model/configuration spent transcribing the dataset:

|Model|WER|Time|
|---|---|---|
|Kaldi_NL|20.7%|8h:15m:54s*|
|faster-whisper v2|5.6%|1h:58m:37s|
|*faster-whisper v3*|**4.3%**|1h:55m:20s|
|faster-whisper v2 w/ VAD|5.6%|1h:58m:50s|
|faster-whisper v3 w/ VAD|4.4%|2h:01m:33s|
|XLS-R FT on Dutch|6.5%|1h:04m:00s|
|*MMS - 102 languages*|13.4%|**0h:37m:50s**|
|MMS - 1162 languages|9.5%|0:53m:56s|

\* Most of the time was spent by the configuration running the speaker diarization module.


### Normalization

Text normalization techniques have been applied to both the reference and hypothesis files when calculating the WER, such as normalization of numbers and characters or variations of different words that are acceptable spellings in the context of evaluation. For more details, check the [ASR-NL-benchmark](https://github.com/opensource-spraakherkenning-nl/ASR_NL_benchmark) repository, where details about the hypothesis/reference files format can also be found.