[back to main page](./index.md)

<h1>WER results</h1>

<h2>UT's Kaldi_NL vs. Whisper evaluation</h2>

*UT = University of Twente*

Here is a matrix with **WER** results of the baseline model, Kaldi_NL, as well as different versions of zero-shot Whisper tested on various datasets:

|Model\Dataset|bn_nl|cts_nl|Jasmin_q_1|Jasmin_q_2|Jasmin_q_3|Jasmin_q_4|Jasmin_q_5|
|---|---|---|---|---|---|---|---|
|Kaldi_NL|12.6%|38.6%|28.1%|16.2%|43.6%|45.3%|20.9%|
|Whisper v2|12.9%|25.9%|22.6%|18.0%|36.5%|37.3%|22.2%|
|Whisper v3|13.8%|28.1%|34.2%|29.4%|50.4%|58.5%|34.4%|
|**Whisper v2 w/ VAD**|**11.7%**|**25.3%**|**20.1%**|**12.4%**|**30.2%**|**33.4%**|**14.9%**|
|Whisper v3 w/ VAD|14.2%|26.5%|34.7%|27.5%|46.7%|53.0%|30.2%|

**bn_nl** = Broadcast News programmes in the Netherlands, from the N-Best 2008 evaluation dataset<br>
**cts_nl** = Conversational Telephone Speech in the Netherlands, from the N-Best 2008 evaluation dataset<br>
**Jasmin_q_1** = Read speech (comp_**q**) of category **1** of speakers (***native children***) for the **Jasmin**-CGN corpus<br>
**Jasmin_q_2** = Read speech (comp_**q**) of category **2** of speakers (***native teenagers***) for the **Jasmin**-CGN corpus<br>
**Jasmin_q_3** = Read speech (comp_**q**) of category **3** of speakers (***non-native teenagers***) for the **Jasmin**-CGN corpus<br>
**Jasmin_q_5** = Read speech (comp_**q**) of category **5** of speakers (***native elderly***) for the **Jasmin**-CGN corpus

<!-- \* There is an issue with the alignment of the hypothesis and reference files. The first word of each segment is timestamped by Whisper before the start timestamp of the segment. Thus, it is recognized as an insertion and, in the actual segment, the first word is recognized as deleted by the transcriber, even though Whisper manages to transcribe it correctly. This issue was fixed by changing the start time of the first word of each segment to first word's end time minus 0.1s for the Whisper annotations. Kaldi annotations do not need any additional text preprocessing. -->

For a matrix with the time performance of each evaluation, click [here](./time.md).

<br><br>
And here are results for the same models on bn_nl with the foreign speech lines removed from the dataset:

|Model\Dataset|bn_nl|
|---|---|
|Kaldi_NL|12.1%|
|Whisper v2|12.4%|
|Whisper v3|13.7%|
|**Whisper v2 w/ VAD**|**11.3%**|
|Whisper v3 w/ VAD|14.0%|

Something to note about this setup of the dataset is that Whisper v3 was already able to recognize foreign speech and ignore it. The only notable exception was for a German speaker, where I assume that it was still transcribed because German and Dutch are very similar as languages. So, Whisper v3's hypothesis files were mostly unedited.

<!-- <h2>UvA's Whisper evaluation on Jasmin</h2>

The outcomes presented by [@Golesheed](https://github.com/Golesheed) in preparation for her pilot investigation on the performance of Whisper Large v2 across diverse age groups and linguistic backgrounds within the JASMIN CGN corpus are outlined below. The evaluation was conducted on individual subsets of the dataset without introducing additional divisions. Prior to the assessment, a normalization technique was applied to ensure uniformity in the datasets.

|Model/Age group|Native elderly|Non-native adults|Native children*|Non-native children|
|---|---|---|---|---|
|Whisper large v2|%|%|%|%|

\* Native children corresponds to groups 1 (aged 7-11) and 2 (aged 12-16) of JASMIN CGN corpus. -->
