[**Back to homepage**](../index.md)

## Analysis of WER difference between whisper-timestamped (Whisper) and faster-whisper

What has been noticed is that faster-whisper, using the same version and same VAD setting, performs slightly better than whisper-timestamped. This is unexpected given that the base model is the same.

After some preliminary research into the results, it seems that faster-whisper outputs better aligned timestamps when compared to the reference file. The exact differences in the alignment algorithms of the 2 implementations are not clear, but they are visible in the results obtained when comparing the 2 implementations.

Further investigation has been done in comparing the texts without timestamping of the same model with same VAD setting for the 2 different implementations and the main differences that have been observed there is in the way names and words with hyphens (zo'n) or dashes (medisch-ethisch) are outputted.

In faster-whisper, hyphens and dashes split the word into 2, whereas in whisper-timestamped it is considered 1 word. This is sometimes helpful for faster-whisper as numbers can be normalized (in the case of 41-jarige), but in most cases it is detrimental since words like "medisch-ethisch" will increase the number of errors.

In addition, there are also differences with some functions words such as "er, de, en". But, overall, the words that are not functional or shortened/constructed from 2 smaller words are the same between the two implementations.

Therefore, the conclusion is that **time alignment** is the major factor that affects the performance of the 2 implementations of Whisper since the differences in functional and constructed words are negligible (some improve the performance of faster-whisper, whereas others decrease it).
