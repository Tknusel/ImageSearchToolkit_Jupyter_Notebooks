# Image Search & CLIP Toolkit — Notebook Collection

A modular series of Jupyter notebooks for learning Python, exploring pixel-level image analysis, and building semantic image search using CLIP. Designed for JupyterLab / JupyterHub.

---

## Notebooks

### Foundations

| Notebook | Description |
|---|---|
| `00_1_Basics_Python.ipynb` | Introduction to Python for JupyterLab — variables, data types, loops, functions, and the notebook workflow |
| `00_2_Basics_Markdown.ipynb` | Markdown syntax reference — headings, formatting, lists, tables, code blocks, LaTeX math, and inline HTML |

### Dataset Acquisition

| Notebook | Description |
|---|---|
| `01_Dork_Generator_v2.ipynb` | Search Dork Generator for artists, designers and researchers — constructs advanced Google/Bing search queries using operators like `site:`, `filetype:`, `intitle:` to surface hard-to-find image sources |

### Understanding Images

| Notebook | Description |
|---|---|
| `02_Pixel_channels.ipynb` | Interactive introduction to pixels, RGB channels, and image arrays — what a picture looks like to a computer |
| `02_1_Pixel_Explained.ipynb` | Extended explainer version of the above — same concepts with more guided commentary, suitable as a teaching resource |

### Image Search

| Notebook | Description |
|---|---|
| `03_1_Imagesearch_Pixel.ipynb` | **Pixel-based image search** — sort and filter a local image folder by brightness, hue, saturation, and visual complexity using PIL + NumPy (no ML, handles ~60k images) |
| `03_2_CLIP_Vocabulary.ipynb` | **CLIP vocabulary readout** — scores every word in the CLIP tokenizer vocabulary (~20k real English words) against an uploaded image and returns the top 100 matches |
| `03_3_CLIP_Imagesearch.ipynb` | **CLIP semantic image search** — text→image search, image→image search, multi-query with negatives, concept axis projection, HDBSCAN clustering, UMAP 2D map, and odd-one-out detection |
| `04_CLIP_Pixels_image_search_faceted.ipynb` | **Faceted search** — combined CLIP semantic query + dominant color picker + HSB range sliders in a single interactive panel; adjustable semantic ↔ color weighting |
| `05_CLIP_HeatmapForSearchTerms_interactive.ipynb` | **CLIP heatmap** — localizes where a free-text concept appears inside an image by sliding patches across it and rendering cosine similarity as an overlaid heatmap |

---

## Suggested Order

```
00_1 → 00_2           # Python & Markdown basics
  ↓
01                    # Build a source image dataset
  ↓
02 / 02_1             # Understand what images are
  ↓
03_1                  # Search by pixel properties
03_2                  # Explore CLIP's vocabulary
03_3                  # Search by meaning (CLIP)
  ↓
04                    # Combine both approaches (faceted)
05                    # Visualize where CLIP "looks"
```

---

## Requirements

All notebooks self-install their dependencies in the first cell. The core stack is:

- **Python 3.10+**
- `torch` / `torchvision` — accelerated on CUDA, Apple MPS, or CPU
- `openai/clip` — via `pip install git+https://github.com/openai/CLIP.git`
- `Pillow`, `numpy`, `matplotlib`, `opencv-python`
- `ipywidgets` — for interactive controls (enable via `jupyter nbextension enable --py widgetsnbextension` if needed)
- `faiss-cpu` / `faiss-gpu` — used automatically by `03_3` past 10k images
- `hdbscan`, `umap-learn` — for clustering and 2D map cells in `03_3`

---

## Common UX Conventions

All search notebooks share consistent interaction patterns:

- **Button-triggered search** — results never auto-update; click Run/Search explicitly
- **Filenames under thumbnails** — every result grid shows the source filename
- **Score-prefixed ZIP download** — exported files are renamed `0.543_imagename.jpg` so sort order is preserved
- **Pre-flight cleanup** — notebooks detect wrong-extension, corrupt, and duplicate (MD5) images and move them to a `_dump/` subdirectory before indexing
- **Progress bars** with staged status labels during indexing and search
