# VISAtlas — Reproduction Talk

> A 25-slide presentation that **explains, reproduces and critically discusses** the VISAtlas paper: a system that turns a large collection of visualization images into an interactive, explorable map.

**Authors:** Youssra Abouelmawahib and [teammate's name]
**Original repository:** [github.com/yaojunhe123/VA](https://github.com/yaojunhe123/VA)

**[Open the slides (talk.pdf)](talk.pdf)**

---

## What the talk covers

| # | Section | In short |
|---|---|---|
| 1 | **Context** | Where, when and by whom the paper was published |
| 2 | **Motivation & research questions** | The problem VISAtlas solves, and the four questions it asks |
| 3 | **Related work & contributions** | A citation graph of the 37 papers that cite VISAtlas, and what is new |
| 4 | **System & method** | How images are collected, turned into embeddings with a CNN (ResNet50), trained with a triplet loss (as in FaceNet), and laid out in an interactive map. Why VISAtlas avoids PCA and t-SNE. |
| 5 | **Evaluation** | The case studies (real-world data, comparing collections, composites and retrieval) and the user study |
| 6 | **Our reproduction** | We ran the released system ourselves, documented its weak spots, and tested it with extreme composites and minimal pairs. Our critical take. |
| 7 | **Impact & conclusion** | From one paper to a research programme, and the take-home messages |

## Highlights

- **A real reproduction, not just a summary:** we ran the released VISAtlas code and tested its limits.
- **Real network activations:** the embedding slide shows actual ResNet50 feature maps computed with the released model weights.
- **Citation provenance graph:** how the paper has been used by 37 follow-up works (data from Semantic Scholar).
- **Custom "Lumen" Beamer theme**, included in the repository.

---

## Repository structure

```
VA/
├── talk.tex / talk.pdf        → the presentation (source + compiled slides)
├── beamer*lumen.sty           → the custom "Lumen" theme (5 files)
├── figures/                   → all images used in the slides
│   ├── *.py                   → scripts that generate or crop the figures
│   └── *.png / *.pdf          → the resulting figures
└── data/
    ├── citations.json         → the 37 papers citing VISAtlas
    └── references.json        → reference metadata
```

<details>
<summary><b>Details of the figure scripts</b></summary>

| Script | Produces |
|---|---|
| `citation_provenance.py` | Citation provenance graph over time |
| `extract_overview_parts.py` | Crops for the *System Overview* slide |
| `extract_embedding_figs.py` | Crops of Fig. 2 (inputs → ResNets → embeddings) |
| `extract_facenet_figs.py` | FaceNet Fig. 3 (triplet geometry) and Fig. 7 (face-cluster strip) |
| `extract_interface_figs.py` | Interface figures: Fig. 4(d), Fig. 6 (PCA / t-SNE), Fig. 7 |
| `extract_resnet_stages.py` | Real ResNet50 activations (run in the `visatlas` environment) |
| `make_resnet_stages_fig.py` | Activation panel: pixels → feature maps → embedding |
| `make_collection_thumbs.py` | Thumbnails for the *Data Collection* slide |

Files in `figures/` not listed here are earlier iterations, kept for reference.

</details>

---

## Build the slides

**Requirements:** TeX Live with `lualatex`, and the fonts Fira Sans, Fira Mono and FiraMath.

```bash
lualatex -interaction=nonstopmode talk.tex
lualatex -interaction=nonstopmode talk.tex   # second run, for the page numbers
```

## Regenerate the figures (optional)

The scripts in `figures/` crop and build the figures from local copies of the source material:

- **VISAtlas paper (PDF):** Fig. 1 (system overview), Fig. 2 (image embedding via CNN), Fig. 4(d), 6, 7 (interface) and Fig. 10 (real-world thumbnails).
- **FaceNet paper** (Schroff et al., CVPR 2015, [arXiv:1503.03832](https://arxiv.org/abs/1503.03832)): Fig. 3 and Fig. 7. The script expects a local copy at `/tmp/opencode/facenet.pdf`.
- **Released VISAtlas code** ([github.com/yilinye/VisAtlas-Code](https://github.com/yilinye/VisAtlas-Code)): the demo and collection images, and the model weights (`11250.h5`, `forvis2.h5`).
  1. Run `extract_resnet_stages.py` inside the `visatlas` conda environment.
  2. Then run `make_resnet_stages_fig.py` with your normal Python.

The paths in the scripts point to local copies: adjust them to your own machine.

---

## References

- **VISAtlas** — the paper being reproduced, and its [released code](https://github.com/yilinye/VisAtlas-Code).
- **FaceNet** — F. Schroff, D. Kalenichenko, J. Philbin, *FaceNet: A Unified Embedding for Face Recognition and Clustering*, CVPR 2015.
