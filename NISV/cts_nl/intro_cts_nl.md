[**Back to homepage**](../../index.md)

<h2>N-Best 2008 Dutch</h2>

The N-Best 2008 Dutch Evaluation corpus is a corpus designed to evaluate Dutch/Flemish Speech Recognition systems in 2008. The corpus consists of 4 subsets:
- `bn_nl`: Broadcast News programmes in the Netherlands;
- `cts_nl`: Conversational Telephone Speech in the Netherlands;
- `bn_vl`: Broadcast News programmes in Belgium;
- `cts_vl`: Conversational Telephone Speech in Belgium.

For more details about the corpus, click [here](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=32b10cb0f4cb99ba934f5be5066638a5ad9b19f2).

**The subset used in this benchmark is `cts_nl` (Conversational Telephone Speech in the Netherlands).**

- [Results on labelled data](./res_labelled.md)
- [Results on unlabelled data](./res_unlabelled.md)

## Detailed results per pipeline component for WhisperX
[Click here](./whisperx.md)

## Hardware setup

A high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia Quadro RTX 6000 with 24 GiB VRAM each, using CUDA version 12.4, with an Intel(R) Xeon(R) Gold 5220 CPU @ 2.20GHz and 256 GB of RAM available.

The OS installed on the cluster is [RHEL 9.3](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/9.3_release_notes/index).