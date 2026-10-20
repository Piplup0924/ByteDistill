# ByteDistill

**Cross-Tokenizer Distillation via Chunk-wise Byte-Level Distribution Alignment**

NeurIPS 2026

Yang Chen · Xianqi Yu · Shaowei Yao · Fuyu Lv · Dan Ou · Haihong Tang

ByteDistill distills knowledge between language models with different tokenizers. It groups overlapping token spans into shared text chunks, converts each model's native token probabilities into distributions over the same 256 byte values, and compares those distributions with the Byte-Level Distribution Alignment (BLDA) loss. Both models retain their own tokenizers and token histories.

![ByteDistill training pipeline](assets/training-pipeline.png)

## Release status

This repository currently contains project documentation and the initial repository layout. **The implementation, training recipes, evaluation tools, and data-preparation scripts have not been released.** There is no runnable training or evaluation entry point yet.

## Reported results

The following results are reported in the paper; they have not been reproduced from this repository.

| Setting | Reported result |
| --- | --- |
| GSM8K and MATH, Qwen3-8B → Gemma-2-2B | **49.27%** average zero-shot Pass@1; +5.40 percentage points over SFT and +1.78 over CTLS |
| DialogSum, 1,500 student training examples | **38.65** ROUGE-L |
| On-policy Countdown, three students | All three improve over their SFT initialization; mean accuracy is **64.31%**, compared with 63.48% for SFT initialization |

## Documentation

- [Method overview](docs/method.md): chunk alignment, native token histories, and training objectives.
- [Data notes](docs/data.md): the HighMATH split and pending reproducibility artifacts.
- [Contributing](CONTRIBUTING.md): questions, documentation improvements, and future code contributions.

```text
ByteDistill/
├── README.md
├── CITATION.cff
├── LICENSE
├── CONTRIBUTING.md
├── .github/                 # Issue and pull-request templates
├── assets/
│   └── training-pipeline.png
├── docs/
│   ├── method.md
│   └── data.md
├── src/                     # Implementation — pending release
├── configs/                 # Experiment configurations — pending release
├── scripts/                 # Data preparation and training — pending release
└── evaluation/              # Evaluation tools — pending release
```

## Citation

```bibtex
@inproceedings{chen2026bytedistill,
  title     = {{ByteDistill}: Cross-Tokenizer Distillation via Chunk-wise Byte-Level Distribution Alignment},
  author    = {Chen, Yang and Yu, Xianqi and Yao, Shaowei and Lv, Fuyu and Ou, Dan and Tang, Haihong},
  booktitle = {Advances in Neural Information Processing Systems},
  year      = {2026}
}
```

## License

This repository is licensed under [Apache License 2.0](LICENSE). Third-party models and datasets retain their respective licenses.
