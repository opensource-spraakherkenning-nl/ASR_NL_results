<h1>Dutch ASR Performance</h1>

Welcome to the page where researchers and developers report performance of various ASR models on Dutch datasets.

<h2>UT's Kaldi_NL vs. Whisper evaluation</h2>

*UT = University of Twente*

- [Results for N-Best 2008 Dutch Evaluation corpus](./UT/N-Best/nbest_res.md)
- [Results for Jasmin-CGN corpus](./UT/Jasmin/jasmin.md)

The results in **bold** indicate the best performance for the specific subset(s) between all models.

For Kaldi_NL, evaluation was run on a local machine instead of a cluster. The local machine used is a Lenovo ThinkPad P15v Gen 3 with AMD Ryzen 7 PRO 6850H CPU and 32 GB of RAM.

For Whisper, a high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia A10 with 24 GB VRAM each, using CUDA version 11.6, 256 GB RAM and 56 CPU cores. For more details, check the [wiki](https://jupyter.wiki.utwente.nl/) page of the cluster.

The implementation used to output word-level timestamps from Whisper is [whisper-timestamped](https://github.com/linto-ai/whisper-timestamped).

## Contributions
Feel free to click the link at the top that leads you to the GitHub repository of this website. You may add changes if you want by forking the repository, making changes on your fork, then opening a pull request on the source repository.

## FAQ
**Coming soon**
