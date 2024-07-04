[Back to homepage](../index.md)

# Environment setup

For **Kaldi_NL**, evaluation was run on a local machine instead of a cluster. The local machine used is a Lenovo ThinkPad P15v Gen 3 with AMD Ryzen 7 PRO 6850H CPU and 32 GB of RAM. The reasons are that it is trickier to set up a Docker container on the cluster used for Whisper (see below) since I do not have admin rights and that Kaldi_NL was meant to run on modern local machines rather than requiring to have a powerful GPU/CPU.

For **Whisper, XLS-R, and MMS**, a high-performance computing cluster was used. The cluster's hardware consists of 2 x Nvidia A10 with 24 GB VRAM each, using CUDA version 11.6, 256 GB RAM and 56 CPU cores. For more details, check the [wiki](https://jupyter.wiki.utwente.nl/) page of the cluster.

The implementation used to output word-level timestamps from Whisper is [whisper-timestamped](https://github.com/linto-ai/whisper-timestamped). In addition, a more optimized implementation of Whisper has been used, namely [faster-whisper](https://github.com/SYSTRAN/faster-whisper). Both of them use the same parameters as the original implementation from [OpenAI](https://github.com/openai/whisper). The parameters are:
- `beam_size=5`
- `best_of=5`
- `temperature=(0.0, 0.2, 0.4, 0.6, 0.8, 1.0)`
- `language="nl"`

<br>

As for Kaldi_NL, the repository can be found [here](https://github.com/opensource-spraakherkenning-nl/Kaldi_NL). The model used for Kaldi_NL is `radboud_OH` and its corresponding script is `decode_OH.sh`.

For XLS-R, a version of it fine-tuned on Dutch by Jonatas Grosman has been used which can be found [here](https://huggingface.co/jonatasgrosman/wav2vec2-xls-r-1b-dutch).

For MMS, both versions are the official models released by Meta AI. Links to the models are:
- [MMS - 102 languages](https://huggingface.co/facebook/mms-1b-fl102)
- [MMS - 1162 languages](https://huggingface.co/facebook/mms-1b-all)

<br>

It has been observed that `whisper-timestamped` (simplified to "Whisper" in the results matrix) requires on average 7 GB of VRAM per recording, with an initial memory requirement of 9.4 GB. A test has been done on a less-performant GPU, RTX 4070 with 12 GB VRAM, which proved that a GPU with 12 GB VRAM could also be used for the large versions of Whisper.

The better-optimized implementation, `faster-whisper`, however, uses on average 3.2 - 3.7 GB of VRAM per recording. Therefore, this implementation can be used on GPUs with smaller video memory capacity.

`XLS-R` and `MMS` use on average 4.3 GB of VRAM per recording, sometimes going as low as 4.0 GB and as high as 8.3 GB. Initial memory requirement varies from 8 GB to 13.7 GB, though the higher value could have been influenced by other previous processes that were executed on the GPU.

For Kaldi_NL, the memory it uses for diarization is 355 MB on average, and for NNet3 decoding, 1.6 GB. Keep in mind that RAM is used in this case since it runs on the CPU.