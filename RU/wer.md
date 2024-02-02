
# WER results
This file presents the average (avg.) WER scores of the three datasets tested within the [HoMed](https://homed.ruhosting.nl/) project (2021-2024).
The concrete results (INS, DEL, SUB) of each one of the files of the three datasets are included in the .sys files generated with [SCLITE](https://github.com/usnistgov/SCTK).


1. Medicijnjournaal (**MJ**): 35 files
*Ground truth*: [https://doi.org/10.34973/dpjc-0v85](https://doi.org/10.34973/dpjc-0v85)

  *Avg. results:*
   - Wav2vec2.0: **12.8% WER** 
 - Kaldi-NL:  **16.1% WER**



2. Medical video material (**MV**): 11 files
*Ground truth*: Ask via email: [cristian.tejedorgarcia@ru.nl](cristian.tejedorgarcia@ru.nl)
*Notes*: Monologues, dialogues, music in background, good audio quality overall.

*Avg. results:*
- Whisper-large-v2: **10.9% WER**
- Wav2vec2.0: **24.2% WER**
- Kaldi-NL:  **28.4% WER**

	
			
3. Patient-provider medical conversations at Nivel (**Nivel**): 38 files
*Ground truth*: You need permission to access to Nivel files. Ask via email: cristian.tejedorgarcia@ru.nl

*Avg. results:*
- Whisper-large-v2: **58.1% WER**
- Kaldi-NL (fine-tuned): **68.0% WER**
- Kaldi-NL:  **71.2% WER**
