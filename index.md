<h1>Dutch Open Speech Recognition Benchmark</h1>

Welcome to the Dutch Open Speech Recognition Benchmark website! We encourage contributions from all researchers and developers working with Dutch Automatic Speech Recognition.

## OH-SMArt Project Benchmark

The following results were achieved during the PDI-SSH **O**ral **H**istory - **S**tories at the **M**useum around **Art** ([OH-SMArt](https://www.uva.nl/en/discipline/conservation-and-restoration/research/research-projects/oh-smart/oh-smart.html)) project (2022-2025) and are reported by University of Twente:

### [Broadcast News and Telephone Conversations (N-Best) Benchmark](./OH-SMArt/N-Best/nbest_res.md)

### [Underrepresented Speakers (JASMIN-CGN) Benchmark](./OH-SMArt/JASMIN/jasmin.md)

### [Common Voice (CV) Benchmark](./OH-SMArt/CommonVoice/cv.md)

### [Pathological Speech (COPAS) Benchmark*](./OH-SMArt/COPAS/copas_res.md)

*These results were obtained during and after the project, in preparation for Interspeech 2025.

#### [Environment setup for benchmarks above](./OH-SMArt/environment.md)

#### [Why do the results differ between whisper-timestamped and faster-whisper?](./OH-SMArt/analysis.md)

## Medical Speech (HoMed) Benchmark

The following results were achieved during the PDI-SSH **Ho**mo **Med**icinalis ([HoMed](https://homed.ruhosting.nl/)) project (2021-2024) and are reported by Radboud University:

### [Results](./HoMed/wer.md)

### [Environment setup](./HoMed/environment.md)

## NISV's Whisper Benchmark

*NISV = Netherlands Institute for Sound & Vision (**NL**: Nederlands Instituut voor Beeld & Geluid)*

The following results were achieved during the same ([OH-SMArt](https://www.uva.nl/en/discipline/conservation-and-restoration/research/research-projects/oh-smart/oh-smart.html)) project mentioned above and are reported by University of Twente in collaboration with NISV:

### [Results for Broadcast News Speech](./NISV/bn_nl/intro_bn_nl.md)

### [Results for Conversational Telephone Speech](./NISV/cts_nl/intro_cts_nl.md)

## Data selection for ASR adaptation

The following results were achieved as part of a Ph.D study, funded by the first phase of the HOSAN project (2025) and the MediSpeech project (2025-2028), and are reported by University of Twente:

### [Results](./UT-data-selection/results.md)

## Vlotspraak's results

*Vlotspraak = a proprietary, on-premise commercial Dutch ASR model, developed by CodeSpark Tech*

The following results were produced by CodeSpark Tech and scored with the official [ASR_NL_benchmark](https://github.com/opensource-spraakherkenning-nl/ASR_NL_benchmark) Docker tool (text normalization + NIST sclite). The model weights are commercial and not publicly released, but the full sclite output is committed so the scoring itself is inspectable.

### [Common Voice (nl) and Medicijnjournaal (HoMed) Benchmarks](./Vlotspraak/wer.md)

Common Voice 17.0 NL test: **3.5% WER** on the full 11,266-clip set. A same-model faster-whisper-large-v3 control on the identical clips reproduces the 4.3% figure reported for that model on [this board](./OH-SMArt/CommonVoice/cv.md), and a train-on-test contamination check is documented (0.08% overlap).

Held-out medical audio, no medical data in training: **11.4% WER** on 30 of the 35 HoMed Medicijnjournaal episodes (the audio we could retrieve). This is a different subset than the 35-file RU evaluation, so it is indicative rather than a like-for-like comparison - see the page for the full caveat.

### [Environment setup](./Vlotspraak/environment.md)

## Contributions
Feel free to click the link at the top that leads you to the GitHub repository of this website. You may add changes if you want by forking the repository, making changes on your fork, then opening a pull request on the source repository.
