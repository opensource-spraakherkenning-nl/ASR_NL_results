[Back to homepage](../index.md)

# Hardware setup


**Kaldi_NL**: [Official github repository](https://github.com/opensource-spraakherkenning-nl/Kaldi_NL). The model used for Kaldi_NL is `radboud_GN` and its corresponding script is `decode_GN.sh`.

For Kaldi_NL, a high-performance computing cluster was used (in particular, the *Thunderlane* cluster node) except for the Nivel's dataset (no GPUs, 16GB RAM and 4 CPU cores, under a Windows-Docker environment). The cluster's hardware consists of 3 x Nvidia Tesla T4 with 16GB VRAM each, using CUDA version 12, 512 GB RAM and 64 CPU cores. For more details, check the [wiki page](https://ponyland.science.ru.nl/ponyland/about/) of the cluster.
For Kaldi_NL, the memory it uses for diarization is 370 MB on average, and for NNet3 decoding, 1.8 GB. Keep in mind that RAM is used in this case since it runs on the CPU.

**Whisper**: [Official github repository](https://github.com/openai/whisper)

For Whisper, no GPUs were used. The computer's hardware consists of 16GB RAM and 4 CPU cores, under a Windows-Docker environment. It has been observed that Whisper requires on average 8 GB of RAM per recording, with an initial memory requirement of 9.9 GB.


**Wav2vec2.0-large-xlsr-53-dutch**: [Official github repository](https://huggingface.co/jonatasgrosman/wav2vec2-large-xlsr-53-dutch)

For Wav2vec2.0, a high-performance computing cluster was used (in particular, the *Thunderlane* cluster node). The cluster's hardware consists of 3 x Nvidia Tesla T4 with 16GB VRAM each, using CUDA version 12, 512 GB RAM and 64 CPU cores. For more details, check the [wiki page](https://ponyland.science.ru.nl/ponyland/about/) of the cluster.

<br>

**Note**: All these ASR systems can run without GPUs, but it is highly recommended to use GPUs, as the decoding time decreases drastically.
