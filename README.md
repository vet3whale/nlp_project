## About the Project

This project investigates whether task-specific fine-tuning can enable a compact NLP model to extract numerical operating limits and their applicability conditions from unseen hardware datasheets, while approaching the extraction accuracy of a larger model.

## Get Started

```shell
git clone https://github.com/vet3whale/nlp_project.git
cd nlp_project
conda env create -f environment.yml
conda activate nlp_project
```

There are 220 examples across 12 datasheets: 177 positive and 43 negative (`requirements: []`).
Explicit operating and absolute-maximum stress bounds are included; stress-rating context is preserved in `condition`.

Data is split by device family: 135 training, 40 validation, and 45 test examples. The original 100 reviewed examples and their family assignments are preserved. 

Run `notebooks/01_data_extraction.ipynb` to extract text, combine the JSON files, and regenerate the seeded splits. Source URLs, PDF hashes, revisions, and page references for the new examples are in `data/source_references.json`.
