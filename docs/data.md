# Data notes

This repository does not currently distribute datasets or data-preparation scripts. Third-party datasets remain subject to their original licenses and access terms.

## HighMATH

The paper uses the public [HighMATH repository](https://github.com/tjunlp-lab/HighMATH), containing **4,399 problems** across eight subject files. This count refers to the public release used in the experiments, rather than the 5,293 problems described in the HighMATH paper.

Because that release does not provide an official training split, the experiments use the following split:

| Property | Value |
| --- | --- |
| Stratification fields | Problem type (`type`) and difficulty level (`level`) |
| Random seed | `42` |
| Training problems | `3,399` |
| Held-out test problems | `1,000` |
| Train/test overlap | None at the problem level |

The held-out test problems are used only for evaluation.

| Reproducibility artifact | Status |
| --- | --- |
| Exact dataset revision | Pending |
| Data-preparation script | Pending release |

The split description above records the experimental protocol. The exact split cannot yet be reconstructed from this repository alone.
