# NL-ASR-results

Welcome to the website created for researchers of Dutch ASR technology to share the results they obtained. It is at the moment accessible at https://greenw0lf.github.io/NL-ASR-results, but there are plans in the future to change its domain.

## Local setup
To test changes locally, you can set up the website on your own machine by following the [official Github guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll).

## File structure
Each page of the website has its own markdown file. `index.md` corresponds to the main page of the website. The folder `UT` contains the WER results and time performance of the models as reported by University of Twente. Inside the folder, there are 2 markdown files corresponding to the 2 different corpora used during evaluation.

Each researcher should create a new folder with an unique and significant name. The structure inside that folder can vary, according to how the researcher wants to structure it. Some ideas include reporting the WER and time in 2 separate files, for all datasets/corpora, or the same structure as in the `UT` folder, reporting all results for each dataset/corpus used.

## Add your own work!
We encourage all Dutch ASR researchers to upload the results they obtained on our website. This can be simply done by:

1. Forking this repository
2. Adding the results and testing the changes on your fork locally
3. Opening a PR from your fork to this repository

## Feedback
If you have any suggestions or feedback to share about this website or its structure, I encourage you to open an issue or a pull request and I will make sure to review them.