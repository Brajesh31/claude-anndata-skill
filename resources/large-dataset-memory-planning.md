# AnnData Large-Dataset Memory Planning

Use this guide before transforming large AnnData objects or moving between sparse, dense, in-memory, and backed representations.

## 1. Estimate the matrix footprint

A rough dense matrix estimate is:

matrix rows × matrix columns × bytes per value

For example, a float32 matrix requires approximately four bytes per element before accounting for indexes, metadata, temporary arrays, and copies. A real workflow may need substantially more memory than the primary matrix alone.

For sparse matrices, memory depends on non-zero values, index arrays, pointer arrays, and data types. Sparse storage is not automatically smaller for every density or operation.

## 2. Inspect before transforming

Record:

- Number of observations and variables.
- Matrix dtype and sparse format.
- Non-zero count or density, where available.
- Sizes of layers and pairwise matrices.
- Observation and variable metadata sizes.
- Existing views or copies.
- Expected output size and available memory.

Avoid converting a large sparse matrix to a dense array without estimating the memory requirement first.

## 3. Choose a processing strategy

| Situation | Consider | Watch for |
|---|---|---|
| Small dataset | In-memory AnnData | Extra copies during filtering or normalization |
| Large read-only inspection | Backed read mode | Operations that require loading data into memory |
| Sparse measurements | CSR or CSC sparse matrix | Algorithm support and matrix conversion costs |
| Repeated subsets | Filter using metadata first | Creating many overlapping copies |
| Large concatenation | On-disk or lazy workflows where supported | Alignment and merge behavior |
| Cloud or distributed workflow | Chunked storage and explicit I/O boundaries | Network latency and inconsistent metadata |

## 4. Views and copies

- Use a view for lightweight inspection or selection when mutation is not required.
- Create an explicit copy before modifying a subset when independent data are required.
- Avoid repeated full-object copies inside loops.
- Keep a raw snapshot only when it serves a defined downstream need, because it can increase storage and memory costs.
- Confirm which operations materialize data from backed storage.

## 5. Write and reopen

- Select a storage format appropriate for the downstream tool.
- Consider compression and chunking based on access patterns.
- Write outputs to a new path until validation passes.
- Reopen the output and check dimensions, indices, annotations, layers, and matrix representation.
- Record package versions and processing parameters.

## 6. Execution record

- Dataset dimensions:
- X dtype and representation:
- Non-zero count or density:
- Layers and auxiliary matrices:
- Estimated memory:
- Available memory:
- Processing mode:
- Copy/materialization points:
- Output format:
- Output size:
- Validation results:
