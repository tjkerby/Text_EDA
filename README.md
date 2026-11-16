# STAT 386: Exploring Text with Embeddings

Open this folder in Positron. The lesson builds one visible step at a time, using **nomic-embed-text:v1.5**, conference kickers, PHATE defaults, and progressively richer plots.

## Start here

| File | Use |
|---|---|
| `slides.qmd` | Conceptual introduction, ending at the demo handoff |
| `demo_complete.ipynb` | Completed, sequential instructor demonstration |
| `demo_live.ipynb` | Matching scaffold for live coding |
| `practice.ipynb` | Separate student investigation |

`data/` holds the teaching CSV and its source notes. `assets/` holds the three instructional figures and the shared style. `docs/` is generated website output for GitHub Pages; edit the source files above.

Extract the project into a fresh folder and keep this small structure together. The demonstration contains the processing and plotting steps directly.

## Setup

Install [Ollama](https://ollama.com/download) separately, then start the Ollama desktop application. On a command-line installation, use `ollama serve` in another terminal. In the project terminal:

```bash
uv sync
ollama pull nomic-embed-text:v1.5
```

Select the `.venv` Python interpreter as the notebook kernel. The project requests Python 3.12 through `.python-version`. No cloud API key is needed for the downloaded local model.

Run the completed notebook once before class. If students will use `practice.ipynb`, also run the save-vectors cell and distribute `data/talk_embeddings.npz` with the project. It explicitly shows a phrase call, its returned vector, a few phrase embeddings and cosine similarities, one kicker, a plain loop over all kickers, the DataFrame's embedding column, `np.vstack`, PHATE, and each plot refinement. No custom helper functions or execution-mode switches hide the main operations.

Use `clustering: ` consistently as Nomic's task prefix. It tells the embedding model what kind of representation is wanted; it does not run a clustering algorithm. Talk titles, names, roles, and dates stay out of the model input. Only PHATE's random seed is specified; its other parameters use library defaults.

## Teaching route: 50 minutes

- **0-15:** Slides: review EDA and dimensionality reduction, motivate text features, predict similarities, work the 2D cosine example, introduce local/cloud execution, Ollama, and Nomic.
- **15-40:** Live notebook: build the text-to-vector-to-plot workflow, interpreting each new layer. Keep computation brief by running once before class. The sample has only 52 kickers.
- **40-47:** A short investigation in the notebook or the separate practice file. Choose a question, read several kickers, and identify a complication. Use random regrouping if time permits.
- **47-50:** Finish in the notebook: compare filtering with subset-and-refit, then state one supported finding and a next check.

There are more notebook examples than need to be typed in 25 minutes. The basic-to-interactive plotting sequence is the main route; subset-and-refit is clearly marked as an extension and can be discussed from prepared output. The diagrams, numerical prediction prompts, and read-the-kicker checks protect conceptual engagement.

## Reuse and student practice

The optional save-vectors section in both instructor notebooks saves a single `data/talk_embeddings.npz` file after genuine inference. It stores vectors with the ordered IDs/texts, model name, and prefix. Distribute that file with this folder if students should practice without running Ollama. The practice notebook loads it explicitly and checks alignment. No model output is supplied or simulated in this archive.

Section 20 in both instructor notebooks exports `talk_map.html` with Plotly's JavaScript included. Keep it beside `index.qmd`; Quarto copies it into `docs/`. The notebook includes an exact iframe block to paste into the page, the required resource configuration, and the `quarto preview` command. Filtering remains visible pandas code.

The homepage contains a fully working three-point example, `example_plot.html`, plus the short Python export and iframe instructions. It uses illustrative numbers, not model output, and previews immediately without Ollama. It is the only additional example file. Regenerate it with the short Python example on the homepage; there is no need to edit its generated HTML. The file can be several megabytes because it includes Plotly's JavaScript.

## Quarto and GitHub Pages

Install the [Quarto CLI](https://quarto.org/docs/get-started/) separately. Save notebook outputs after the local demonstration, then run:

```bash
quarto render
```

Quarto writes to **docs/** without rerunning notebook code. Commit the source and rendered docs. In GitHub, select **Settings > Pages > Deploy from a branch**, choose your branch, and select **/docs**. Relative paths work for a repository website.

The included `docs/` is a static preview of the source materials. Run `quarto render` locally to regenerate it with Quarto. The code and data workflow were checked, but local Nomic inference and a direct Quarto render still need a pre-class run on your machine.

## Data and figure attribution

The 52-record table is a purposive sample of short kickers from six conferences across 2020, 2023, and 2025. It is not a census or random sample. Each row includes the official source URL. See `data/README.md`.

The text-to-vector illustration is an original simplified redraw of the sentence-encoder idea in Reimers and Gurevych (2019), *Sentence-BERT*, Figure 2, https://arxiv.org/abs/1908.10084. It omits architecture/training details and does not claim to depict Nomic's exact architecture. Its vector entries are illustrative. Attribution for the adaptation: Nils Reimers and Iryna Gurevych; original paper CC BY-SA 4.0, https://creativecommons.org/licenses/by-sa/4.0/. The adapted diagram is provided under the same license. The cosine and local/cloud diagrams are original instructional figures.
