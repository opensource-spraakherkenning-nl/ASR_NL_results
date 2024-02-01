[Go back](./jasmin.md)

## Jasmin - Read speech (comp_q)
### Preprocessing 

The encoding used in the dataset for the transcriptions is latin_1. In order for the evaluation tool to work, I converted the encoding to UTF-8.

### Postprocessing

A large number of insertions was encountered when evaluating Whisper. This was due to time misalignment at the start of segments. This was addressed by adjusting the `start_time` of the first word of a segment to `end_time - 0.1s`.

Same issue as described [here](../N-Best/nbest_setup.md) was encountered for Jasmin too, where Whisper v3 would sometimes output segments such as "Beeld &". It was addressed with the same method. Normalization and variations have also been applied similar to [N-Best](../N-Best/nbest_setup.md).

## Jasmin - HMI speech (comp_p)

Same steps were applied as for `comp_q`. One additional step is described below:
### Preprocessing 

The machine voice is still audible in the human speaker's channel. To address this, a [script to silence](https://github.com/greenw0lf/OH-SMArt/blob/master/reference2stm/silence_jasmin.ipynb) the time segments where the human would not speak was used. The gaps between the human-spoken segments are annotated using `inter_segment_gap` as an identifier and those parts were therefore silenced. It uses pydub's `AudioSegment.silent()` function. The script also converts the audio to mono by saving only the human channel.
