[**Back to homepage**](../index.md)

# Environment setup

**Vlotspraak Dutch ASR**: proprietary Dutch ASR model (Whisper large-v3 architecture, 1.55B parameters), fine-tuned from [`yuriyvnv/whisper-large-v3-high-mixed-nl`](https://huggingface.co/yuriyvnv/whisper-large-v3-high-mixed-nl) (Apache-2.0) on CommonVoice 25 NL, FLEURS NL, VoxPopuli NL, MLS NL and VoxForge NL train splits. Served via [faster-whisper](https://github.com/SYSTRAN/faster-whisper) 1.2.1 / CTranslate2 (float16 weights).

**Training-corpus licensing**: Common Voice 25 NL is CC0-1.0; FLEURS NL and MLS NL are CC-BY-4.0 (attribution to Google Research and to Pratap et al. respectively); VoxPopuli NL is CC0 plus European Parliament source terms; VoxForge NL is **GPL-3.0**. On the last one: there is no industry consensus that model weights trained on GPL-licensed audio become GPL-encumbered, and Vlotspraak treats trained weights as not a derivative work of the training data, since the model redistributes neither the audio nor the transcripts. It is listed here explicitly so the corpus composition can be judged rather than assumed. A VoxForge-free build variant is available on request.

**Hardware**: single NVIDIA GeForce RTX 5090 Laptop GPU (24 GB VRAM), driver 595.71, Linux (Ubuntu).

**Decoding configuration**: `language=nl`, `beam_size=5`, `temperature=0.0`, `condition_on_previous_text=False`, `vad_filter=False`, `word_timestamps=True` (word timestamps are required to produce the CTM hypothesis files).

**Scoring**: the official [ASR_NL_benchmark](https://github.com/opensource-spraakherkenning-nl/ASR_NL_benchmark) Docker image (`asrnlbenchmark/asr-nl-benchmark@sha256:080f6c9f77273080b84fa59e5ae70340a19d0251bcf8ed9312f2a5e0065e1a64`) was used unmodified: hypothesis CTM + reference STM → normalization → `variations.glm` → NIST sclite. The committed `.sys` file is sclite's standard summary report (`-o sum`); per-episode references are single-segment STM entries built from the public HoMed ground-truth transcripts ([doi:10.34973/dpjc-0v85](https://doi.org/10.34973/dpjc-0v85)).

**Note on conditioning**: with faster-whisper's default `condition_on_previous_text=True`, several long episodes degenerate into repetition loops (WER on affected episodes rises from ~15% to 40–88%). All results reported here use `condition_on_previous_text=False`.
