# AnnData Dataset Intake and Provenance Template

## Dataset identity

- Dataset name:
- Study or project:
- Data owner:
- Received date:
- Source location:
- Original file name and format:
- File size:
- Checksum:
- License or permitted-use constraints:
- Contact for source questions:

## Biological or experimental context

- Species:
- Tissue, cell type, or material:
- Assay and platform:
- Study design:
- Samples and batches:
- Experimental conditions:
- Reference genome or annotation version:
- Known exclusions or quality concerns:

## AnnData structure inventory

| Component | Present? | Expected content | Validation notes |
|---|---|---|---|
| X | Yes / No | Primary observation-by-variable matrix | |
| obs | Yes / No | Observation metadata | |
| var | Yes / No | Variable metadata | |
| layers | Yes / No | Alternative matrix representations | |
| obsm | Yes / No | Observation-aligned multidimensional data | |
| varm | Yes / No | Variable-aligned multidimensional data | |
| obsp | Yes / No | Pairwise observation matrices | |
| varp | Yes / No | Pairwise variable matrices | |
| uns | Yes / No | Unstructured metadata | |
| raw | Yes / No | Preserved raw snapshot | |

## Index and schema checks

- Observation count:
- Variable count:
- Observation index name and uniqueness:
- Variable index name and uniqueness:
- Required obs columns:
- Required var columns:
- Categorical columns:
- Missing values:
- Sparse or dense X:
- Matrix dtype:
- Layer names and meaning:
- Raw snapshot meaning:
- Expected coordinate or embedding keys:

## Processing history

| Step | Input | Operation | Parameters | Output | Software/version |
|---|---|---|---|---|---|
| | | | | | |

## Handoff notes

- Known limitations:
- Required preprocessing:
- Fields that must be preserved:
- Safe storage format:
- Expected downstream tools:
- Reviewer:
- Review date:
