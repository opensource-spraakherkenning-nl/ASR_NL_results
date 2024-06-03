# Dutch Open Speech Recognition Benchmark

Welcome to the website created for researchers and developers of Dutch ASR technology to share obtained evaluation results. 

It is accessible at: https://opensource-spraakherkenning-nl.github.io/ASR_NL_results

## Local setup
To test changes locally, you can set up the website on your own machine by following the [official Github guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll).

## File structure
Each page of the website has its own markdown file. `index.md` corresponds to the main page of the website. Each folder must contain at least the WER/main performance metric results, in the format of a matrix. Optional, but recommended, information that can be added is time performance, hardware setup, or normalization steps applied.

Each researcher/developer should create a new folder with an unique and semnificative name. The structure inside that folder can vary, according to how the researcher/developer wants to structure it. Some ideas include reporting the WER and time in 2 separate files, for all datasets/corpora, or the same structure as in the `UT` folder, reporting all results for each dataset/corpus used.

## Add your own work!
We encourage all Dutch ASR researchers and developers to upload the results they obtained on our website. This can be simply done by:

1. Forking this repository
2. Adding the results and testing the changes on your fork locally
3. Opening a PR from your fork to this repository

## Feedback
If you have any suggestions or feedback to share about this website or its structure, we encourage you to open an issue or a pull request.