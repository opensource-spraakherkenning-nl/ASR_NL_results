[back to main page](./index.md)

<h1>Kaldi_NL vs. Whisper time performance</h1>

Here is a matrix with the time spent in total by each model to evaluate the corresponding dataset:

|Model\Dataset|bn_nl|cts_nl|Jasmin_q_1|Jasmin_q_5|
|---|---|---|---|---|
|**Kaldi_NL**|**0h:08m:58s**|**0h:14m:47s**|**0h:30m:21s**|**0h:29m:36s**|
|Whisper v2|1h:10m:19s|0h:53m:25s|2h:04m:55s|2h:04m:16s|
|Whisper v3|1h:07m:01s|0h:39m:21s|3h:12m:07s|3h:08m:52s|
|Whisper v2 w/ VAD|0h:51m:40s|0h:39m:49s|2h:13m:51s|2h:07m:43s|
|Whisper v3 w/ VAD|1h:01m:43s|0h:37m:430s|-|2h:46m:56s|

For Kaldi_NL, evaluation was run on a local machine instead of a cluster. The local machine used is a Lenovo ThinkPad P15v Gen 3 with AMD Ryzen 7 PRO 6850H CPU and 32 GB of RAM.

For Whisper, a high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia A10 with 24 GB VRAM each, using CUDA version 11.6, 256 GB RAM and 56 CPU cores. For more details, check the [wiki](https://jupyter.wiki.utwente.nl/) page of the cluster.