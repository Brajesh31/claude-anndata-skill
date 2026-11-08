# AnnData Concatenation Validation Checklist

Use this checklist after combining samples, batches, or modalities.

## Before concatenation

- [ ] Confirm that each object represents a compatible experiment or explicitly document differences.
- [ ] Compare variable identifiers and annotation definitions.
- [ ] Confirm observation and variable index conventions.
- [ ] Check for duplicate observation names.
- [ ] Identify the intended concatenation axis.
- [ ] Choose inner or outer join behavior deliberately.
- [ ] Define how batch or source labels will be represented.
- [ ] Decide which metadata should be merged, retained, or dropped.

## During concatenation

- [ ] Use explicit keys or labels to preserve sample identity.
- [ ] Select merge behavior intentionally.
- [ ] Preserve required layers and embeddings.
- [ ] Avoid silently losing annotations that are needed downstream.
- [ ] Monitor memory use when concatenating large matrices.
- [ ] Use on-disk or lazy approaches where appropriate for dataset size.

## After concatenation

- [ ] Confirm final observation and variable counts.
- [ ] Confirm expected batch labels and group sizes.
- [ ] Check uniqueness of observation names.
- [ ] Verify variable alignment and ordering.
- [ ] Inspect missing values introduced by outer joins.
- [ ] Confirm required obs and var columns are present.
- [ ] Verify layers and raw have the intended semantics.
- [ ] Check sparse/dense representation and matrix dtypes.
- [ ] Reopen the saved output and repeat key structural checks.
- [ ] Record join, merge, label, key, and fill-value settings.

## Interpretation checks

- [ ] Confirm that concatenation did not create an unintended biological comparison.
- [ ] Keep batch identity distinct from biological condition.
- [ ] Do not treat concatenation as batch correction.
- [ ] Apply and assess downstream integration separately.
- [ ] Record any incompatible data that were excluded.

## Result summary

- Input object count:
- Input observation/variable counts:
- Axis:
- Join:
- Merge:
- Label and keys:
- Output dimensions:
- Validation outcome:
- Known limitations:
