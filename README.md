# AnnData

## Overview

This repository contains a Claude skill for working with AnnData, a data structure commonly used to represent annotated data matrices in single-cell and related scientific workflows. The skill provides structured guidance for understanding, manipulating, and managing AnnData objects.

## What It Covers

- AnnData object structure and core components.
- Data input, output, and file handling.
- Data manipulation and concatenation workflows.
- Recommended practices for reliable and reproducible analysis.

## Repository Structure

```text
SKILL.md
references/
  best_practices.md
  concatenation.md
  data_structure.md
  io_operations.md
  manipulation.md
LICENSE
```

## Requirements

- A Claude-compatible environment with skill support.
- Python and the AnnData ecosystem for executing related workflows.
- Appropriate scientific data and project context.

## Getting Started

1. Read `SKILL.md` for the complete skill instructions.
2. Review the reference documents relevant to your task.
3. Install the skill in the skills directory supported by your Claude environment.
4. Provide a focused task and describe the data structure, desired operation, and constraints.
5. Validate results using suitable checks before continuing analysis.

## Reproducibility

Keep track of input data, package versions, and transformations. Validate object dimensions and annotations after operations, and preserve original data when performing destructive changes.

## License

MIT. See [LICENSE](LICENSE).
