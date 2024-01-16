[Back to homepage](../../index.md)

<h2>Kaldi_NL vs. Whisper - N-Best 2008 Dutch</h2>

The N-Best 2008 Dutch Evaluation corpus is a corpus designed to evaluate Dutch/Flemish Speech Recognition systems in 2008. UT has only evaluated the Dutch subset of the corpus. The Dutch part of the corpus consists of 2 subsets:
- `bn_nl`: Broadcast News programmes in the Netherlands,
- `cts_nl`: Conversational Telephone Speech in the Netherlands.

For more details about the corpus, click [here](https://www.isca-speech.org/archive/pdfs/interspeech_2009/leeuwen09b_interspeech.pdf).

<br>

Here is a matrix with **WER** results of the baseline model, Kaldi_NL, as well as different versions of zero-shot Whisper tested on this corpus:

|Model\Dataset|bn_nl|cts_nl|
|---|---|---|
|Kaldi_NL|12.6%|38.6%|
|Whisper v2|12.7%|25.9%|
|Whisper v3|13.7%|28.1%|
|**Whisper v2 w/ VAD**|**11.6%**|**25.3%**|
|Whisper v3 w/ VAD|14.1%|26.5%|

<br>
And here are results for the same models on bn_nl with the foreign speech lines removed from the dataset:

|Model\Dataset|bn_nl|
|---|---|
|Kaldi_NL|12.1%|
|Whisper v2|12.3%|
|Whisper v3|13.6%|
|**Whisper v2 w/ VAD**|**11.1%**|
|Whisper v3 w/ VAD|13.9%|

Something to note about this setup of the dataset is that Whisper v3 was already able to recognize foreign speech and ignore it. The only notable exception was for a German speaker, where I assume that it was still transcribed because German and Dutch are very similar as languages. So, Whisper v3's hypothesis files were mostly unedited.

<br>

Here is also a matrix with the **time** spent in total by each model **to evaluate** the respective subset:

|Model\Dataset|bn_nl|cts_nl|
|---|---|---|
|**Kaldi_NL**|**0h:08m:58s**|**0h:14m:47s**|
|Whisper v2|1h:10m:19s|0h:53m:25s|
|Whisper v3|1h:07m:01s|0h:39m:21s|
|Whisper v2 w/ VAD|0h:51m:40s|0h:39m:49s|
|Whisper v3 w/ VAD|1h:01m:43s|0h:37m:430s|

### Preprocessing, setup, and postprocessing
For more details, click [here](./nbest_setup.md).
