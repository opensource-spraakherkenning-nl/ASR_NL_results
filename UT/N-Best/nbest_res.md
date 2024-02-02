[Back to homepage](../../index.md)

<h2>Kaldi_NL vs. Whisper - N-Best 2008 Dutch</h2>

The N-Best 2008 Dutch Evaluation corpus is a corpus designed to evaluate Dutch/Flemish Speech Recognition systems in 2008. UT has only evaluated the Dutch subset of the corpus. The Dutch part of the corpus consists of 2 subsets:
- `bn_nl`: Broadcast News programmes in the Netherlands,
- `cts_nl`: Conversational Telephone Speech in the Netherlands.

For more details about the corpus, click [here](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=32b10cb0f4cb99ba934f5be5066638a5ad9b19f2).

<br>

Here is a matrix with **WER** results of the baseline model, Kaldi_NL, as well as different versions of zero-shot Whisper tested on this corpus:

|Model\Dataset|bn_nl|cts_nl|
|---|---|---|
|Kaldi_NL|12.6%|38.6%|
|Whisper v2|12.7%|25.9%|
|Whisper v3|13.7%|28.1%|
|Whisper v2 w/ VAD|11.6%|25.3%|
|Whisper v3 w/ VAD|14.1%|26.5%|
|faster-whisper v2|10.6%|24.1%|
|faster-whisper v3|12.5%|25.5%|
|**faster-whisper v2 w/ VAD**|**10.0%**|**23.9%**|
|faster-whisper v3 w/ VAD|12.3%|25.1%|

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
|*Kaldi_NL*|**0h:08m:58s**|0h:14m:47s|
|Whisper v2|1h:11m:59s|0h:53m:55s|
|Whisper v3|1h:09m:00s|0h:40m:20s|
|Whisper v2 w/ VAD|0h:52m:03s|0h:40m:09s|
|Whisper v3 w/ VAD|1h:02m:13s|0h:37m:50s|
|faster-whisper v2|0h:11m:31s|0h:9m:30s|
|faster-whisper v3|0h:11m:21s|0h:9m:41s|
|faster-whisper v2 w/ VAD|0h:12m:13s|0h:9m:36s|
|*faster-whisper v3 w/ VAD*|0h:12m:25s|**0h:9m:13s**|

### Preprocessing, setup, and postprocessing
For more details, click [here](./nbest_setup.md).
