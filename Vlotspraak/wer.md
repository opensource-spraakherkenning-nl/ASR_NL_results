[**Back to homepage**](../index.md)

# WER results — Vlotspraak

- This page reports the WER of **Vlotspraak Dutch ASR**, a proprietary commercial Dutch ASR model (Whisper large-v3 architecture, fine-tuned from [`yuriyvnv/whisper-large-v3-high-mixed-nl`](https://huggingface.co/yuriyvnv/whisper-large-v3-high-mixed-nl), Apache-2.0, on CommonVoice 25 NL, FLEURS NL, VoxPopuli NL, MLS NL and VoxForge NL), on two benchmarks: the **Common Voice 17.0 NL test set**, the same test set used for the [community Common Voice benchmark](../OH-SMArt/CommonVoice/cv.md), and the Medicijnjournaal corpus from the [HoMed](https://homed.ruhosting.nl/) project.
- Scoring used the official [ASR_NL_benchmark](https://github.com/opensource-spraakherkenning-nl/ASR_NL_benchmark) Docker tool (text normalization + `variations.glm` + NIST sclite), image `asrnlbenchmark/asr-nl-benchmark@sha256:080f6c9f7727…`, the same tool and image [this board](../OH-SMArt/CommonVoice/cv.md) uses for its own numbers.
- The detailed sclite output is committed for both benchmarks: `.dtl` files under [`CommonVoice/`](./CommonVoice/) and the per-episode `.sys` file (CORR, SUB, DEL, INS) under [`1_MJ/`](./1_MJ/).

<br>

## 1. Common Voice (nl)

Common Voice 17.0 [(**CV**)](https://commonvoice.mozilla.org): **11,266 test clips, 102,697 reference words**

| ASR system | WER (%) | Test set | GPUs |
|---|---|---|---|
| **Vlotspraak Dutch ASR (proprietary)** | **3.5** | CV17.0 NL test — full (11,266 clips) | Yes |
| Vlotspraak Dutch ASR (proprietary) | 3.6 | CV17.0 NL test — leak-free subset (10,485 clips) | Yes |
| faster-whisper large-v3 (control, our pipeline) | 4.3 | CV17.0 NL test — leak-free subset (10,485 clips) | Yes |
| faster-whisper v3 ([this board](../OH-SMArt/CommonVoice/cv.md)'s incumbent) | 4.3 | CV17.0 NL test — full (11,266 clips) | Yes |

Breakdown (full set, from [`vlotspraak-cv17-full.dtl`](./CommonVoice/vlotspraak-cv17-full.dtl)): Correct 97.0%, Substitutions 2.6%,
Deletions 0.4%, Insertions 0.4%, Word accuracy 96.5%.

<br>

### Contamination check (train-on-test)

Common Voice re-splits on every release, and Vlotspraak fine-tunes on Common Voice 25 train.
Because Common Voice clip filenames (`common_voice_nl_<id>.mp3`) are stable across releases, we
checked by exact filename match whether any CV17 test clip had entered our CV25 training data
before scoring:

- 9 of 11,266 CV17 test clips (0.08%) were present in our CV25 acoustic-training data.
- 772 more appeared only in our CV25 dev split (used to tune language-model fusion weights, never
  for acoustic training).

The table reports both the full 11,266-clip set (comparable to [this board](../OH-SMArt/CommonVoice/cv.md)'s incumbent) and the
leak-free 10,485-clip subset. They differ by 0.1 pp, so the 0.08% overlap does not move the result.

### Same-model control

[This board](../OH-SMArt/CommonVoice/cv.md)'s incumbent is faster-whisper v3 (large-v3) at 4.3%. To check the gain is real and not a
pipeline effect, we ran faster-whisper large-v3 through our own pipeline on the identical clips and
scored it with the same sclite tool. It came out at 4.3% (see [`control-largev3-cv17-clean.dtl`](./CommonVoice/control-largev3-cv17-clean.dtl)),
matching this board's published number. So the 3.5% is a real gain over the same model class, not a
decoding artifact.

<br>

## 2. Medicijnjournaal (HoMed)

Medicijnjournaal [(**MJ**)](https://github.com/opensource-spraakherkenning-nl/ASR_NL_results/tree/master/Vlotspraak/1_MJ/): **30 episodes, 38,743 reference words**

*Ground truth*: [https://doi.org/10.34973/dpjc-0v85](https://doi.org/10.34973/dpjc-0v85)

*Subset note*: 30 of the 35 HoMed episodes (the episodes whose source audio we could retrieve at benchmark-construction time). Results are indicative but not computed on the identical 35-file set used in [the HoMed evaluation](../HoMed/wer.md) (Wav2vec2.0 12.8%, Kaldi-NL 16.1% on 35 files).

|ASR system|WER (%)|GPUs|
|---|---|---|
|Vlotspraak Dutch ASR (proprietary)|11.4|Yes|

<br>

## Transparency notes

- **Fine-tuned vs zero-shot.** Vlotspraak is fine-tuned on Common Voice 25 train; the board's
  faster-whisper v3 is zero-shot. Fine-tuning on a benchmark's train split is legitimate, but it
  does give a real edge on Common Voice's recording conditions, so we flag it. The `XLS-R FT on
  Dutch` entry already on [this board](../OH-SMArt/CommonVoice/cv.md) is likewise CV-fine-tuned.
- Vlotspraak Dutch ASR is a **general-domain Dutch** model with **no medical fine-tuning**. No Medicijnjournaal audio or transcript text entered the training data for the model benchmarked on this page, at any stage: it is a sealed held-out set on our side, and the decode path used here is the acoustic model alone, with no language-model fusion or rescoring (see [environment setup](./environment.md) for the exact decoding configuration).
- Model weights are commercial and not publicly released. The full sclite output is committed here (the `.dtl` files including the confusion-pair table for Common Voice, the per-episode `.sys` breakdown for Medicijnjournaal) so the scoring itself is inspectable.
- **Decoding (both benchmarks):** faster-whisper (CTranslate2 float16), `beam_size=5`, `temperature=0.0`, `condition_on_previous_text=False`, VAD off, `language=nl`. See [environment setup](./environment.md).
