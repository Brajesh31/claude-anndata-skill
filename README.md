# claude-anndata-skill

A Claude Code skill for working with annotated data matrices and scientific datasets using AnnData.

## Overview

AnnData is a data structure for storing a data matrix together with observation metadata, variable metadata, and additional annotations. It is widely used in single-cell genomics and can also support other scientific workflows involving structured, annotated measurements.

This skill provides guidance for creating, inspecting, transforming, combining, reading, and writing AnnData objects. It also addresses memory-aware processing and integration with the broader scientific Python ecosystem.

## What the Skill Covers

### AnnData Structure

Understand the main components of an AnnData object:

- `X`: primary observation-by-variable data matrix.
- `obs`: metadata associated with observations.
- `var`: metadata associated with variables.
- `obsm` and `varm`: multidimensional annotations.
- `obsp` and `varp`: pairwise observation and variable annotations.
- `uns`: unstructured metadata.
- `layers`: alternative representations of the primary matrix.
- `raw`: a snapshot of data retained for downstream analysis.

### Input and Output

Work with common scientific data formats, including H5AD and Zarr, as well as supported tabular and matrix formats. The skill covers reading, writing, conversion, backed access, and remote or large-data considerations.

### Data Manipulation

Perform common operations such as:

- Subsetting observations and variables.
- Filtering by metadata.
- Reordering and renaming indices.
- Managing categorical values.
- Working with views and independent copies.
- Adding or removing annotations.
- Converting between sparse and dense representations.

### Concatenation and Integration

Combine datasets across samples, batches, or modalities. Choose appropriate join and merge behavior, preserve batch labels, and validate the resulting dimensions and metadata.

### Performance and Reproducibility

Use sparse matrices where appropriate, avoid unnecessary copies, consider backed mode for large files, and document transformations so that analysis can be reproduced.

## Installation

Install AnnData in the Python environment used by your analysis:

```bash
python -m pip install anndata
```

For a project managed with uv:

```bash
uv add anndata
```

Optional integrations may require additional packages such as Scanpy, SciPy, or other tools in the scverse ecosystem.

## Install the Skill

```bash
git clone https://github.com/Brajesh31/claude-anndata-skill.git ~/.claude/skills/anndata
```

Adjust the destination if your Claude-compatible environment uses a different skills directory.

## Usage

1. Provide the task involving an AnnData object or scientific matrix.
2. Include the input format and approximate dataset size.
3. State whether the data should be modified in place or copied.
4. Specify the desired output format and any metadata that must be preserved.
5. Review the resulting dimensions, indices, annotations, and data types.

Invoke the skill directly when needed:

```text
/anndata
```

## Example Workflow

```python
import anndata as ad

# Read a dataset
adata = ad.read_h5ad("input.h5ad")

# Inspect its dimensions and annotations
print(adata)
print(adata.obs.head())
print(adata.var.head())

# Create a filtered view and an independent copy
subset = adata[adata.obs["quality"] > 0.8].copy()

# Write the processed dataset
subset.write_h5ad("filtered.h5ad")
```

The column names in this example are illustrative. Replace them with fields that exist in the actual dataset.

## Repository Structure

```text
claude-anndata-skill/
├── SKILL.md
├── references/
│   ├── best_practices.md
│   ├── concatenation.md
│   ├── data_structure.md
│   ├── io_operations.md
│   └── manipulation.md
└── README.md
```

Use `SKILL.md` for the main workflow and open the reference file that matches the operation being performed.

## Validation Checklist

- Confirm observation and variable counts after filtering or concatenation.
- Check that indices are unique when the workflow requires uniqueness.
- Verify that metadata remains aligned with the correct observations and variables.
- Confirm sparse or dense storage behavior before large transformations.
- Avoid accidental mutation of a view when an independent copy is required.
- Reopen saved files when persistence and format compatibility matter.
- Record input files, package versions, and major transformation steps.

## Common Pitfalls

- Assigning metadata by row order when index alignment is required.
- Converting large sparse matrices to dense arrays without checking memory requirements.
- Concatenating datasets with incompatible variable definitions.
- Overwriting raw data before preserving a required snapshot.
- Assuming a view behaves like an independent copy.

## Repository Contents

- `SKILL.md`: Main skill instructions.
- `references/data_structure.md`: AnnData object model.
- `references/io_operations.md`: File input, output, and storage.
- `references/manipulation.md`: Filtering and transformation workflows.
- `references/concatenation.md`: Combining datasets.
- `references/best_practices.md`: Reliability and performance guidance.
