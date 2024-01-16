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
|Whisper v2|2h:04m:55s|1h:52m:51s|1h:35m:06s|1h:24m:08s|2h:04m:16s|
|Whisper v3|3h:12m:07s|2h:27m:29s|6h:13m:02s<b>*</b>|3h:04m:10s|3h:08m:52s|
|Whisper v2 w/ VAD|2h:13m:51s|1h:51m:26s|1h:49m:27s|4h:18m:27s<b>*</b>|2h:07m:43s|
|Whisper v3 w/ VAD|2h:58m:03s|2h:19m:21s|2h:38m:04s|2h:31m:13s|2h:46m:56s|

<b>*</b> Performance might have been impacted by other processes from other users running on the same GPU since the hardware is available via a cluster system. A rerun using different hardware might be done in the near future.
