<p align="center"><img src="ariadne-logo.svg" alt="Ariadne Lit logo" width="120"></p>

# Ariadne Lit

Ariadne Lit is a web application for browsing and visualizing a coding scheme applied to academic papers. This instance explores research artifacts coded from Business Process Management (BPM) conference proceedings: which artifacts each paper contributes, which research and evaluation methods it uses, what data it relies on, whether an implementation is available, and which threats to validity it reflects on.

Open the application: [Ariadne Lit Web Application](https://andreamalhera.github.io/AriadneLit-pages/)

This repository holds the built site that GitHub Pages serves.

## Features

- **Overview**: browse and search the papers, group them into tiles by any coded dimension (Types of Artifact by default), and see them on the Publication Timeline, arranged by year and track. Tiles and timeline follow the active filters.
- **Paper Metagraph**: connects papers through shared keywords (IDF-weighted Jaccard). It starts at the top 2% of similarities, clusters papers by a chosen group (e.g. type of artifact), and lists the most similar papers for a selected paper.
- **Patterns & Trends**: a co-occurrence matrix of any two coded dimensions, tested with Fisher's exact test, and trends over time, tested with the Cochran–Armitage test. Benjamini–Hochberg or Holm corrections apply when many tests run at once.
- **About**: the coding scheme, the method, how to add papers, and the JSON Schema the data is coded against, with the views each attribute appears in. You can also build or upload your own schema there.
- Filters generated from the coded fields, shared across all views (including Conference and Track), plus an option to tell categories apart by shape as well as color
- "How to read this" guides next to each view
- Side-by-side comparison of two or more papers
- **Add Paper**: extract one or more papers from DOIs (via Crossref), BibTeX, or plain-text citations, code each one, and add them locally. Research Method, Evaluation Method and Reflection on Threats to Validity offer an "Other" choice that requires the name of the other value. Added papers are stored only in your browser, are visually marked, can be edited, and can be proposed to the maintainers as a pre-filled GitHub issue in this repository.
- **Your own review**: use Ariadne Lit for your own literature review, coded against your own schema (see [Your Own Review](#your-own-review))
- Dark/light theme toggle (follows the system setting by default)

## Data

The papers come from the BPM conference proceedings and were coded manually against a fixed coding scheme. Each paper is coded with exactly one artifact. The coding process is part of a work under review and will be described once it is published.

The dataset is under review. Until it is published, only a sample of papers is listed by name, but all papers count in every chart and statistic.

Each paper is coded against `data/research_artifacts.schema.json`. An entry has a `metadata` block (title, authors, DOI/URL, year, conference name and abbreviation, track) and a `contribution` block. The `contribution` block holds keywords, the paper's focus/intent, its research components, and the paper's artifact. The artifact carries its type(s), research method, evaluation method, data collection, reflection on threats to validity, and implementation status.

```json
{
  "metadata": {
    "title": "Paper Title",
    "authors": ["Author A", "Author B"],
    "doi_or_url": "https://doi.org/...",
    "year": 2025,
    "conference_name": "International Conference on Business Process Management",
    "conference_abbreviation": "BPM",
    "track": "Engineering"
  },
  "contribution": {
    "keywords": ["process mining", "conformance checking"],
    "focus_intent": {
      "type_of_inquiry": ["information_systems_engineering"]
    },
    "research_components": {
      "type_of_theory": ["formal_theory"],
      "emphasis": ["artifact"],
      "formal_concepts": true,
      "algorithms": true,
      "hypothesis": false
    },
    "artifacts": [
      {
        "type_of_artifact": ["method"],
        "research_method": { "methods": ["design_science_engineering", "other"], "other": "Name of the other method" },
        "evaluation_method": ["case_study"],
        "data_collection": {
          "data_type": ["real_world_data"],
          "material_accessibility": true,
          "data_accessibility": true,
          "participants": { "total_participants": 0, "students": 0, "practitioners": 0 }
        },
        "threats_to_validity": ["external_validity"],
        "implementation": { "existence": true, "availability": true }
      }
    ]
  }
}
```

Research method, evaluation method and threats to validity accept the value `other`. Choosing it requires the name of the other value, stored in `research_method.other`, `evaluation_method_other` or `threats_to_validity_other`.

## Your Own Review

Ariadne Lit also works for your own literature review. Everything happens on the About page and in your browser; nothing is uploaded.

1. Build a schema with **+ Build Schema**, or upload a JSON Schema and choose how the views use each attribute.
2. Use **Load Papers…** to read your papers from BibTeX, DOIs, citations or JSON. Title, authors, year and DOI are filled in from Crossref.
3. Choose **Show Your Review**. Every view then shows your papers, and a bar at the top shows how many are fully coded.
4. Code your papers in a form built from your schema, with **Code Next Uncoded** in that bar or **Code This Paper** on a paper. The Coding filter finds papers that are not fully coded or have problems.
5. Use **Download** to keep a copy of your review; **Open Review File…** restores it, also in another browser.

**Back to the Published Dataset** in the bar switches back at any time.

## Contributing

Missing a paper? Use **+ Add Paper** on the Overview, code it, and propose it for the shared dataset. Proposals arrive as issues in this repository and are reviewed by the maintainers.

## License

The source code is licensed under the [MIT License](LICENSE). The dataset and site content are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) (see the About page in the application for the full notice). The NFDIxCS logo belongs to NFDIxCS and is not covered by either license.

### Citation

`Ariadne Lit` is part of an [NFDIxCS Service](https://nfdixcs.org/services). For extensions, please contact the authors, Maximilian Britton and [Andrea Maldonado](mailto:andreamalher.works@gmail.com).

Ariadne Lit has been iteratively improved from the [Research Artifacts MetaGraph](https://doi.org/10.5281/zenodo.21946693), a former version of this work that included only the Paper Metagraph. It was published on Zenodo to gather feedback within NFDIxCS. We thank everyone, who provided usability feedback during the iterative improvement process. 

### Funding

Funded by the German Research Foundation (DFG) within the framework of NFDIxCS (DFG project number 501930651).
