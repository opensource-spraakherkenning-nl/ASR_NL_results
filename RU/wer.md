[Back to homepage](../index.md)

# WER results
- This file presents the **average (avg.) WER** scores of the three datasets tested within the [HoMed](https://homed.ruhosting.nl/) project (2021-2024).
- Kaldi_NL was fine-tuned with 50 hours of real conversations between patient and medical providers at [Nivel](https://www.nivel.nl/en) facilities.
- The concrete results (INS, DEL, SUB) of each one of the files of the three datasets are included in the .sys files generated with [SCLITE](https://github.com/usnistgov/SCTK).

<br>

1.Medicijnjournaal (**MJ**): 35 files

*Ground truth*: [https://doi.org/10.34973/dpjc-0v85](https://doi.org/10.34973/dpjc-0v85)

|ASR system|WER (%)|GPUs|
|---|---|---|
|Wav2vec2.0|12.8|Yes|
|Kaldi-NL|16.1|Yes|

<br>


2.Medical video material (**MV**): 11 files

*Ground truth*: Ask via email: [cristian.tejedorgarcia@ru.nl](mailto:cristian.tejedorgarcia@ru.nl)

*Notes*: Monologues, dialogues, music in background, good audio quality overall.

|ASR system|WER (%)|GPUs|
|---|---|---|
|Whisper-large-v2|10.9|Yes|
|Wav2vec2.0|24.2|Yes|
|Kaldi-NL|28.4|Yes|

 <br>
			
3.Patient-provider medical conversations at Nivel (**Nivel**): 38 files

*Ground truth*: You need permission to access to Nivel files. Ask via email: [cristian.tejedorgarcia@ru.nl](mailto:cristian.tejedorgarcia@ru.nl)

|ASR system|WER (%)|GPUs|
|---|---|---|
|Whisper-large-v2|57.1|No|
|Kaldi-NL (fine-tuned)|68.0|No|
|Kaldi-NL|71.2|No|
