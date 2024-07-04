[Back to homepage](../../index.md)

<h2>N-Best 2008 Dutch</h2>

The N-Best 2008 Dutch Evaluation corpus is a corpus designed to evaluate Dutch/Flemish Speech Recognition systems in 2008. The corpus consists of 4 subsets:
- `bn_nl`: Broadcast News programmes in the Netherlands;
- `cts_nl`: Conversational Telephone Speech in the Netherlands;
- `bn_vl`: Broadcast News programmes in Belgium;
- `cts_vl`: Conversational Telephone Speech in Belgium.

For more details about the corpus, click [here](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=32b10cb0f4cb99ba934f5be5066638a5ad9b19f2).

<br>

Here is a matrix with **WER** results of the baseline model, Kaldi_NL, as well as different end-to-end models tested on this corpus:

|Model\Dataset|bn_nl|cts_nl|bn_vl|cts_vl|
|---|---|---|---|---|
|Kaldi_NL|12.6%|38.6%|21.2%|59.4%|
|Whisper v2|12.7%|25.9%|-|-|
|Whisper v3|13.7%|28.1%|-|-|
|Whisper v2 w/ VAD|11.6%|25.3%|-|-|
|Whisper v3 w/ VAD|14.1%|26.5%|-|-|
|faster-whisper v2|10.6%|24.1%|**13.0%**|38.5%|
|faster-whisper v3|12.5%|25.5%|14.9%|38.4%|
|**faster-whisper v2 w/ VAD**|**10.0%**|**23.9%**|13.6%|37.9%|
|faster-whisper v3 w/ VAD|12.3%|25.1%|14.6%|**36.9%**|
|XLS-R FT on Dutch|14.8%|33.5%|17.0%|51.7%|
|MMS - 102 languages|23.4%|49.0%|25.0%|64.2%|
|MMS - 1162 languages|18.5%|42.7%|19.4%|57.7%|

<br>
And here are results for the same models on `bn_nl` with the foreign speech lines removed from the dataset:

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

|Model\Dataset|bn_nl|cts_nl|bn_vl|cts_vl|
|---|---|---|---|---|
|Kaldi_NL|0h:08m:58s|0h:14m:47s|0h:15m:57s|0h:20m:07s|
|Whisper v2|1h:11m:59s|0h:53m:55s|-|-|
|Whisper v3|1h:09m:00s|0h:40m:20s|-|-|
|Whisper v2 w/ VAD|0h:52m:03s|0h:40m:09s|-|-|
|Whisper v3 w/ VAD|1h:02m:13s|0h:37m:50s|-|-|
|faster-whisper v2|0h:11m:31s|0h:09m:30s|0h:10m:55s|0h:09m:39s|
|faster-whisper v3|0h:11m:21s|0h:09m:41s|0h:10m:36s|0h:09m:54s|
|faster-whisper v2 w/ VAD|0h:12m:13s|0h:09m:36s|0h:11m:01s|0h:09m:46s|
|faster-whisper v3 w/ VAD|0h:12m:25s|0h:09m:13s|0h:10m:45s|0h:09m:04s|
|XLS-R FT on Dutch|0h:07m:36s|0h:07m:52s|0h:08m:44s|0h:08m:21s|
|*MMS - 102 languages*|**0h:04m:33s**|0h:04m:23s|0h:04m:38s|**0h:03m:54s**|
|*MMS - 1162 languages*|0h:05m:26s|**0h:04m:14s**|**0h:04m:37s**|0h:03m:55s|

### Preprocessing, setup, and postprocessing
For more details, click [here](./nbest_setup.md).
