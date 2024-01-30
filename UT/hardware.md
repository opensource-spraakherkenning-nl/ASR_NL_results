# Hardware setup

For **Kaldi_NL**, evaluation was run on a local machine instead of a cluster. The local machine used is a Lenovo ThinkPad P15v Gen 3 with AMD Ryzen 7 PRO 6850H CPU and 32 GB of RAM. The reasons are that it is trickier to set up a Docker container on the cluster used for Whisper (see below) since I do not have admin rights and that Kaldi_NL was meant to run on modern local machines rather than requiring to have a powerful GPU/CPU.

For Whisper, a high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia A10 with 24 GB VRAM each, using CUDA version 11.6, 256 GB RAM and 56 CPU cores. For more details, check the [wiki](https://jupyter.wiki.utwente.nl/) page of the cluster.

The implementation used to output word-level timestamps from Whisper is [whisper-timestamped](https://github.com/linto-ai/whisper-timestamped). As for Kaldi_NL, the repository can be found [here](https://github.com/opensource-spraakherkenning-nl/Kaldi_NL). The model used for Kaldi_NL is `radboud_OH` and its corresponding script is `decode_OH.sh`.

It has been observed that Whisper requires on average 7 GB of VRAM per recording, with an initial memory requirement of 9.4 GB. A test has been done on a less-performant GPU, RTX 4070 with 12 GB VRAM, which proved that a GPU with 12 GB VRAM could also be used for the large versions of Whisper.

For Kaldi_NL, the memory it uses for diarization is 355 MB on average, and for NNet3 decoding, 1.6 GB. Keep in mind that RAM is used in this case since it runs on the CPU.