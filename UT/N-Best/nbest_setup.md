[**Go back**](./nbest_res.md)

## N-Best setup
### Preprocessing

Not all speech was annotated in the reference files. After the very first results, I observed that there were a lot of insertions in the segments where speech was not annotated. Therefore, I decided to use a [script](https://github.com/greenw0lf/OH-SMArt/blob/master/reference2stm/segment_nbest.ipynb) that splits the audio files into smaller segments that can each be transcribed by the evaluated models. Spoken utterances are put together into one audio/transcription file if they are not apart from each other for more than 5 seconds.

The `cts_nl` subset of the dataset contained a string that was not properly encoded as a character in UTF-8. I replaced it with the correct character (\xE2 => â)

### Postprocessing

Whisper v3 with or without VAD (`whisper-timestamped` implementation) outputted sometimes segments such as "Beeld &". The issue is that only one word is expected per timestamp and the CTM format that I converted it uses whitespace as a delimiter. Thus, it would error when running the evaluation. This was fixed by adjusting the problematic lines manually, either by removing the second word or adjusting the timestamps such that the second word can fit in. The script used for finding the error lines can be found [here](https://github.com/greenw0lf/OH-SMArt/blob/master/whisper2ctm/validate_ctm.py).

Aside from that, there are other steps applied, such as normalization of numbers and characters or variations of different words that are acceptable spellings in the context of evaluation. For more details, check the [ASR-NL-benchmark](https://github.com/opensource-spraakherkenning-nl/ASR_NL_benchmark) repository, where details about the hypothesis/reference files format can also be found.