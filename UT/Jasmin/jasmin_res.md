[Go back](./jasmin.md)

## Jasmin results
Here is a matrix with **WER** results of the baseline model, Kaldi_NL, as well as different versions of zero-shot Whisper tested on the read speech part of the corpus:

|Model\Dataset|Jasmin_q_1|Jasmin_q_2|Jasmin_q_3|Jasmin_q_4|Jasmin_q_5|
|---|---|---|---|---|---|
|Kaldi_NL|28.1%|16.2%|43.6%|45.3%|20.9%|
|Whisper v2|22.6%|18.0%|36.5%|37.3%|22.2%|
|Whisper v3|34.2%|29.4%|50.4%|58.5%|34.4%|
|**Whisper v2 w/ VAD**|**20.1%**|**12.4%**|**30.2%**|**33.4%**|**14.9%**|
|Whisper v3 w/ VAD|34.7%|27.5%|46.7%|53.0%|30.2%|

<br>

And its corresponding matrix with the **time** spent in total by each model **to evaluate** the respective subset:

|Model\Dataset|Jasmin_q_1|Jasmin_q_2|Jasmin_q_3|Jasmin_q_4|Jasmin_q_5|
|---|---|---|---|---|---|
|**Kaldi_NL**|**0h:30m:21s**|**0h:23m:25s**|**0h:27m:51s**|**0h:27m:17s**|**0h:29m:36s**|
|Whisper v2|2h:05m:29s|1h:53m:11s|1h:35m:28s|1h:24m:41s|2h:04m:35s|
|Whisper v3|3h:12m:26s|2h:27m:52s|6h:13m:28s<b>*</b>|3h:04m:32s|3h:09m:49s|
|Whisper v2 w/ VAD|2h:14m:40s|1h:51m:46s|1h:49m:48s|4h:18m:51s<b>*</b>|2h:08m:02s|
|Whisper v3 w/ VAD|2h:58m:24s|2h:19m:43s|2h:38m:23s|2h:31m:35s|2h:47m:33s|

<b>*</b> Performance might have been impacted by other processes from other users running on the same GPU since the hardware is available via a cluster system. A rerun using different hardware might be done in the near future.
