# anndata-omics-bridge

**A quantitative-proteomics spine built on AnnData and MuData.**

Quantification tools each emit their own result table, and every downstream analysis re-implements
the same reading, joining, and annotating. This organization converts those vendor tables into one
structured container that keeps **protein-, peptide-, and ion-level evidence linked** — and
fragment-level evidence for DIA — while **preserving tool-specific columns rather than only the
intersection across tools**. The result reads from Python, R, Julia, and JavaScript, and exports to
Parquet or DuckDB.

**APB** — the *AnnData Proteomics Bridge* — is the proteomics implementation of that spine, and
lives in [apb2](https://github.com/anndata-omics-bridge/apb2). The organization is named for the
wider scope, since it also holds a viewer, plasma reference data, and a FASTA library.

## Repositories

| Repository | What it is |
| --- | --- |
| [apb2](https://github.com/anndata-omics-bridge/apb2) | APB — rules-driven conversion of quantification output tables to AnnData/MuData, with vendor parameter parsing |
| [prozor](https://github.com/anndata-omics-bridge/prozor) | Typed peptide-to-protein matching and deterministic greedy-parsimony protein inference |
| [protein-fasta](https://github.com/anndata-omics-bridge/protein-fasta) | Streaming FASTA parsing, header interpretation, classification, and validation |
| [abp_studio](https://github.com/anndata-omics-bridge/abp_studio) | ⚠️ **Down for refactoring.** Fixture manager and corpus runner that drives the APB CLI over real vendor files |
| [visualiser-test](https://github.com/anndata-omics-bridge/visualiser-test) | Interactive browser viewer for the converted objects |
| [plasma-ms](https://github.com/anndata-omics-bridge/plasma-ms) | Plasma QC reference material: datasets, quality-marker panels, and the metric catalogue |

**`abp_studio` is down at the moment.** It is being refactored, its corpus runs are not expected to
work in the meantime, and it should not be used as a starting point until this note goes away.

`apb2` supersedes the original `anndata-proteomics-bridge`, which is now closed and kept only as a
parity reference.

## Licensing

**All code is MIT. Reference data is CC BY 4.0**, and third-party material keeps its own terms,
recorded per file in the repository that vendors it.
