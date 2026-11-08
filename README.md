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

## Practical Data Workflow

Use a consistent sequence when working with an AnnData object:

1. **Inspect first.** Record dimensions, index names, matrix representation, metadata columns, layers, embeddings, and any raw snapshot.
2. **Validate identity.** Confirm observation and variable identifiers, uniqueness requirements, and alignment between metadata and matrix rows or columns.
3. **Choose the storage strategy.** Decide whether in-memory, backed, sparse, dense, or chunked access is appropriate for the operation and dataset size.
4. **Make transformations explicit.** Document filtering, normalization, concatenation, renaming, and type conversion with their parameters.
5. **Preserve required state.** Keep raw data or source snapshots only when there is a defined downstream requirement.
6. **Validate the result.** Recheck dimensions, indices, metadata, matrix representation, and expected values after important transformations.
7. **Save and reopen.** Confirm that the serialized output can be read and still contains the information needed by downstream tools.

## Supporting Resources

| Resource | Purpose |
|---|---|
| [Dataset intake and provenance template](resources/dataset-intake-and-provenance-template.md) | Capture experimental context, AnnData components, schema, and processing history. |
| [Concatenation validation checklist](resources/concatenation-validation-checklist.md) | Check joins, labels, metadata alignment, dimensions, and output integrity. |
| [Large-dataset memory planning guide](resources/large-dataset-memory-planning.md) | Estimate memory requirements and choose in-memory, backed, sparse, or chunked workflows. |
| [Data structure reference](references/data_structure.md) | Understand X, obs, var, layers, multidimensional annotations, pairwise matrices, uns, and raw. |
| [I/O operations reference](references/io_operations.md) | Review supported storage formats, reading, writing, and backed access. |
| [Manipulation reference](references/manipulation.md) | Review slicing, views, copies, indexing, and transformation patterns. |
| [Concatenation reference](references/concatenation.md) | Review join, merge, labels, and large-scale concatenation behavior. |
| [Best practices reference](references/best_practices.md) | Review memory, metadata, and reproducibility practices. |

## Data Integrity Rules

Keep observation and variable metadata aligned to their corresponding indexes. When joining external metadata, align by identifiers rather than assuming row order. After concatenation, verify that the resulting labels and variable definitions match the intended study design. An outer join can introduce missing values, while an inner join can remove variables, so record the choice and inspect the result.

A concatenated object is not automatically batch-corrected or biologically harmonized. Preserve batch and sample identity, then evaluate integration or correction as a distinct analytical step.

## Memory-Safety Guidance

Avoid unnecessary dense conversions and full-object copies. Use backed access for appropriate read-heavy workflows, while recognizing that some operations require data to be materialized in memory. A view is not the same as an independent copy. Before modifying a subset, make the copy behavior explicit and test that the source object remains unchanged where that is required.

## Reproducible Handoff

A useful handoff records the input dataset identity, dimensions, observation and variable identifiers, package versions, transformation sequence, parameters, output format, and validation results. Include a brief note describing which annotations, layers, embeddings, and raw data were preserved or intentionally omitted.
