[Go back](./jasmin.md)

## Jasmin Dutch results
Here is a matrix with **WER** results of the baseline model, Kaldi_NL, as well as different models tested on **Dutch read speech**:

|Model\Dataset|Native Children|Native Teenagers|Non-native Minors|Non-native Adults|Native Elderly|
|---|---|---|---|---|---|
|Kaldi_NL|28.1%|16.2%|43.6%|45.3%|20.9%|
|Whisper v2|22.6%|18.0%|36.5%|37.3%|22.2%|
|Whisper v3|34.2%|29.4%|50.4%|58.5%|34.4%|
|Whisper v2 w/ VAD|20.1%|12.4%|30.2%|33.4%|14.9%|
|Whisper v3 w/ VAD|34.7%|27.5%|46.7%|53.0%|30.2%|
|faster-whisper v2|20.3%|11.3%|29.9%|30.6%|13.7%|
|faster-whisper v3|28.1%|25.2%|50.9%|62.6%|27.6%|
|**faster-whisper v2 w/ VAD**|**19.1%**|**11.1%**|**29.5%**|**30.0%**|**12.8%**|
|faster-whisper v3 w/ VAD|27.5%|22.4%|42.6%|49.4%|25.2%|
|XLS-R FT on Dutch|22.4%|13.3%|33.8%|36.1%|17.2%|
|MMS - 102 languages|31.6%|20.3%|54.2%|55.1%|23.9%|
|MMS - 1162 languages|28.9%|20.0%|50.1%|54.0%|28.3%|

<br>

And for **Dutch conversational speech**:

|Model\Dataset|Native Children|Native Teenagers|Non-native Minors|Non-native Adults|Native Elderly|
|---|---|---|---|---|---|
|Kaldi_NL|55.4%|62.4%|69.1%|60.0%|44.0%|
|Whisper v2|95.8%|107.4%|124.0%|88.1%|61.9%|
|Whisper v3|75.7%|72.6%|94.3%|84.2%|58.4%|
|Whisper v2 w/ VAD|32.6%|29.4%|42.6%|54.0%|33.1%|
|Whisper v3 w/ VAD|40.3%|31.7%|57.1%|63.2%|41.3%|
|faster-whisper v2|58.9%|65.8%|107.4%|77.7%|39.9%|
|faster-whisper v3|85.8%|68.3%|84.4%|84.5%|51.4%|
|**faster-whisper v2 w/ VAD**|**28.2%**|**22.9%**|**39.2%**|**51.4%**|**26.8%**|
|faster-whisper v3 w/ VAD|34.4%|28.6%|48.7%|58.2%|33.6%|
|XLS-R FT on Dutch|60.2%|62.2%|70.5%|59.1%|47.0%|
|MMS - 102 languages|79.8%|79.9%|90.7%|80.5%|56.4%|
|MMS - 1162 languages|82.4%|87.9%|94.5%|83.3%|59.9%|


**Jasmin_{p,q}_{1,2,3,4,5}** = **p** stands for **comp_p (HMI speech)**, whereas **q** stands for **comp_q (read speech)**. The number that can range from **1-5** represents the corresponding **age group/nativeness** from the corpus (for more details, go back one page).

<br>

And its corresponding matrix with the **time** spent in total by each model **to evaluate** the respective subset:

|Model\Dataset|Jasmin_q_1|Jasmin_q_2|Jasmin_q_3|Jasmin_q_4|Jasmin_q_5|
|---|---|---|---|---|---|
|Kaldi_NL|0h:30m:21s|0h:23m:25s|0h:27m:51s|0h:27m:17s|0h:29m:36s|
|Whisper v2|2h:05m:29s|1h:53m:11s|1h:35m:28s|1h:24m:41s|2h:04m:35s|
|Whisper v3|3h:12m:26s|2h:27m:52s|6h:13m:28s<b>*</b>|3h:04m:32s|3h:09m:49s|
|Whisper v2 w/ VAD|2h:14m:40s|1h:51m:46s|1h:49m:48s|4h:18m:51s<b>*</b>|2h:08m:02s|
|Whisper v3 w/ VAD|2h:58m:24s|2h:19m:43s|2h:38m:23s|2h:31m:35s|2h:47m:33s|
|faster-whisper v2|0h:30m:45s|0h:26m:48s|0h:23m:48s|0h:21m:55s|0h:30m:02s|
|faster-whisper v3|0h:41m:58s|0h:38m:13s|0h:48m:28s|0h:55m:48s|0h:44m:12s|
|faster-whisper v2 w/ VAD|0h:32m:55s|0h:27m:16s|0h:25m:51s|0h:21m:58s|0h:32m:09s|
|faster-whisper v3 w/ VAD|0h:40m:33s|0h:31m:45s|0h:37m:36s|0h:37m:11s|0h:38m:00s|
|XLS-R FT on Dutch|0h:35m:18s|0h:27m:33s|0h:32m:39s|0h:31m:49s|0h:39m:05s|
|*MMS - 102 languages*|0h:17m:59s|**0h:13m:22s**|0h:16m:01s|0h:15m:38s|**0h:17m:35s**|
|**MMS - 1162 languages**|**0h:17m:46s**|**0h:13m:22s**|**0h:16m:00s**|**0h:15m:37s**|**0h:17m:35s**|

|Model\Dataset|Jasmin_p_1|Jasmin_p_2|Jasmin_p_3|Jasmin_p_4|Jasmin_p_5|
|---|---|---|---|---|---|
|*Kaldi_NL*|0h:16m:09s|0h:10m:29s|0h:11m:28s|0h:19m:09s|**0h:21m:32s**|
|Whisper v2|1h:23m:33s|1h:12m:52s|1h:13m:23s|1h:31m:20s|2h:39m:12s|
|Whisper v3|2h:30m:51s|1h:59m:19s|2h:13m:38s|3h:07m:55s|4h:39m:06s<b>*</b>|
|Whisper v2 w/ VAD|0h:48m:52s|0h:42m:17s|0h:37m:07s|1h:02m:36s|1h:47m:58s|
|Whisper v3 w/ VAD|1h:05m:32s|0h:37m:53s|0h:55m:46s|1h:38m:03s|2h:16m:09s|
|faster-whisper v2|0h:22m:10s|0h:17m:19s|0h:20m:16s|0h:23m:23s|0h:34m:06s|
|faster-whisper v3|0h:54m:15s|0h:32m:13s|0h:34m:35s|0h:55m:02s|1h:12m:22s|
|***faster-whisper v2 w/ VAD***|**0h:09m:59s**|0h:07m:37s|**0h:07m:57s**|**0h:13m:32s**|0h:22m:31s|
|*faster-whisper v3 w/ VAD*|0h:13m:43s|**0h:07m:17s**|0h:09m:57s|0h:22m:45s|0h:25m:52s|
|XLS-R FT on Dutch|0h:42m:20s|0h:24m:19s|0h:26m:52s|0h:36m:42s|0h:48m:26s|
|MMS - 102 languages|0h:18m:02s|0h:14m:02s|0h:14m:01s|0h:18m:59s|0h:25m:34s|
|MMS - 1162 languages|0h:17m:55s|0h:13m:56s|0h:13m:59s|0h:18m:54s|0h:25m:24s|

<b>*</b> Performance might have been impacted by other processes from other users running on the same GPU since the hardware is available via a cluster system. A rerun using different hardware might be done in the near future.

## Jasmin Flemish results

Matrix with **WER** results for the **Flemish** part of the corpus:

|Model\Dataset|Jasmin_q_1|Jasmin_q_2|Jasmin_q_3|Jasmin_q_4|Jasmin_q_5|
|---|---|---|---|---|---|
|Kaldi_NL|59.2%|33.5%|51.3%|43.3%|24.7%|
|faster-whisper v2|42.4%|11.7%|19.9%|21.0%|16.7%|
|faster-whisper v3|57.2%|30.6%|44.4%|41.1%|38.7%|
|**faster-whisper v2 w/ VAD**|**41.8%**|**11.6%**|**19.4%**|**20.5%**|**14.4%**|
|faster-whisper v3 w/ VAD|56.2%|26.7%|38.4%|50.7%|33.6%|
|XLS-R FT on Dutch|47.4%|13.3%|30.1%|26.8%|16.4%|
|MMS - 102 languages|55.3%|22.4%|43.0%|37.0%|23.0%|
|MMS - 1162 languages|49.2%|21.8%|34.9%|35.8%|22.3%|

|Model\Dataset|Jasmin_p_1|Jasmin_p_2|Jasmin_p_3|Jasmin_p_4|Jasmin_p_5|
|---|---|---|---|---|---|
|Kaldi_NL|66.5%|49.8%|66.2%|64.4%|47.4%|
|faster-whisper v2|87.6%|51.7%|76.1%|67.3%|45.4%|
|faster-whisper v3|90.5%|65.2%|100.4%|79.9%|68.3%|
|**faster-whisper v2 w/ VAD**|**28.7%**|**24.3%**|**38.5%**|**49.3%**|**30.6%**|
|faster-whisper v3 w/ VAD|46.0%|37.7%|57.9%|57.9%|44.6%|
|XLS-R FT on Dutch|73.2%|62.2%|68.1%|52.2%|47.8%|
|MMS - 102 languages|86.7%|52.3%|87.8%|78.2%|56.4%|
|MMS - 1162 languages|86.1%|68.0%|86.3%|76.7%|60.8%|

<br>

And its corresponding matrix with the **time** spent in total by each model **to evaluate** the respective subset:

|Model\Dataset|Jasmin_q_1|Jasmin_q_2|Jasmin_q_3|Jasmin_q_4|Jasmin_q_5|
|---|---|---|---|---|---|
|Kaldi_NL|0h:15m:58s|0h:16m:03s|0h:25m:11s|0h:15m:46s|0h:29m:36s|
|faster-whisper v2|0h:09m:30s|0h:20m:12s|0h:18m:03s|0h:12m:09s|0h:14m:31s|
|faster-whisper v3|0h:14m:53s|0h:24m:33s|0h:29m:19s|0h:21m:47s|0h:23m:58s|
|faster-whisper v2 w/ VAD|0h:21m:27s|0h:27m:16s|0h:19m:09s|0h:13m:24s|0h:15m:29s|
|faster-whisper v3 w/ VAD|0h:13m:17s|0h:23m:29s|0h:23m:14s|0h:26m:40s|0h:19m:54s|
|XLS-R FT on Dutch|0h:11m:18s|0h:20m:03s|0h:22m:05s|0h:16m:28s|0h:13m:00s|
|*MMS - 102 languages*|**0h:05m:47s**|0h:09m:09s|**0h:10m:06s**|**0h:07m:37s**|**0h:08m:04s**|
|**MMS - 1162 languages**|**0h:05m:47s**|**0h:09m:07s**|**0h:10m:06s**|**0h:07m:37s**|**0h:08m:04s**|

|Model\Dataset|Jasmin_p_1|Jasmin_p_2|Jasmin_p_3|Jasmin_p_4|Jasmin_p_5|
|---|---|---|---|---|---|
|Kaldi_NL|0h:07m:09s|0h:07m:36s|0h:08m:37s|0h:10m:51s|0h:14m:45s|
|faster-whisper v2|0h:12m:48s|0h:10m:45s|0h:14m:34s|0h:11m:58s|0h:34m:06s|
|faster-whisper v3|0h:24m:08s|0h:26m:42s|0h:28m:56s|0h:27m:12s|0h:31m:16s|
|**faster-whisper v2 w/ VAD**|**0h:05m:41s**|**0h:07m:03s**|**0h:07m:01s**|**0h:08m:11s**|**0h:09m:45s**|
|faster-whisper v3 w/ VAD|0h:06m:44s|0h:08m:23s|0h:10m:08s|0h:13m:52s|0h:10m:40s|
|XLS-R FT on Dutch|0h:20m:36s|0h:16m:58s|0h:20m:55s|0h:17m:47s|0h:19m:34s|
|MMS - 102 languages|0h:10m:55s|0h:09m:10s|0h:11m:00s|0h:09m:43s|0h:10m:33s|
|MMS - 1162 languages|0h:10m:06s|0h:09m:09s|0h:10m:42s|0h:09m:36s|0h:10m:15s|
