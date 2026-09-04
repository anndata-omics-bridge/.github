# anndata-omics-bridge

**One interoperable data layer for quantitative omics, starting with proteomics.**

Quantification tools each emit their own result table, and every downstream analysis re-implements
the same reading, joining, and annotating. This organization converts those vendor tables into one
structured container that keeps **protein-, peptide-, and ion-level evidence linked** — and
fragment-level evidence for DIA — while **preserving tool-specific columns rather than only the
intersection across tools**. The result reads from Python, R, Julia, and JavaScript, and exports to
Parquet or DuckDB.

**APB** — the *AnnData Proteomics Bridge* — is the proteomics implementation of that spine, and
lives in [apb2](https://github.com/anndata-omics-bridge/apb2). The organization is named for the
wider scope, since it also holds a viewer, plasma reference data, and a FASTA library.

## Why this exists

The [Functional Genomics Center Zurich (FGCZ)](https://fgcz.ch/service_and_support/bioinformatics_services.html) provides bioinformatics support across genomics, transcriptomics, proteomics, metabolomics/lipidomics, and other omics technologies. On the genomics side, [AnnData](https://anndata.readthedocs.io/) is already a practical common structure for annotated data matrices. Quantitative proteomics, however, still arrives in many tool-specific tables, making shared analysis and multi-omics integration unnecessarily difficult.

APB2 is based on the work of [ProteoBench](https://github.com/proteobench/proteobench), which has built extensive parsing infrastructure for upstream proteomics formats: software-specific result tables, search-parameter files, and modification encodings. APB2 ports that infrastructure into one rules-driven converter while preserving the original tool-specific information. See the ProteoBench preprint, [*ProteoBench: the community-curated platform for comparing proteomics data analysis workflows*](https://doi.org/10.64898/2025.12.09.692895).

The work that became APB2 was discussed and started during the Copenhagen ProteoBench Hackathon, 13–17 April 2026, as part of the effort to improve the backend of the [ProteoBench platform](https://proteobench.cubimed.rub.de/). The hackathon included the public [EuBIC-MS Seminar 2026 on 15 April](https://eubic-ms.org/events/latest-developments-and-tools-for-data-analysis/).

APB2 is a refactoring and performance improvement of the now-discontinued [AnnData Proteomics Bridge (APB v1)](https://github.com/anndata-omics-bridge/anndata-proteomics-bridge). It was also motivated by the vendor-specific readers behind [`prolfquapp::preprocess_software()`](https://github.com/prolfqua/prolfquapp/blob/master/R/preprocess_software.R#L137) and [`prolfquappPTMreaders`](https://github.com/prolfqua/prolfquappPTMreaders). The aim is to consolidate the remaining upstream formats into a shared parser that can serve ProteoBench, prolfquapp, and other quantitative-proteomics tools.

## Repositories

| Repository | What it is |
| --- | --- |
| [apb2](https://github.com/anndata-omics-bridge/apb2) | APB — rules-driven conversion of quantification output tables to AnnData/MuData, with vendor parameter parsing |
| [protein-fasta](https://github.com/anndata-omics-bridge/protein-fasta) | Streaming FASTA parsing, header interpretation, classification, and validation |
| [apb-proteobench](https://github.com/anndata-omics-bridge/apb-proteobench) | ProteoBench-specific annotation and scoring for APB results |
| [prozor](https://github.com/anndata-omics-bridge/prozor) | Python port of the R `prozor` package for typed peptide-to-protein matching and deterministic greedy-parsimony protein inference |
| [apb-plasma](https://github.com/anndata-omics-bridge/apb-plasma) | Plasma MS quality control: reference datasets, quality-marker panels, and the QC metric catalogue |
| [abp_studio](https://github.com/anndata-omics-bridge/abp_studio) | ⚠️ **Down for refactoring.** Fixture manager and corpus runner that drives the APB CLI over real vendor files |
| [visualiser-test](https://github.com/anndata-omics-bridge/visualiser-test) | Interactive browser viewer for the converted objects |
| [anndata-omics-bridge](https://github.com/anndata-omics-bridge/anndata-omics-bridge) | Format specification and cross-project documentation |
| [anndata-proteomics-bridge](https://github.com/anndata-omics-bridge/anndata-proteomics-bridge) | Archived APB v1 repository, retained as the parity reference for APB2 |

**`abp_studio` is down at the moment.** It is being refactored, its corpus runs are not expected to
work in the meantime, and it should not be used as a starting point until this note goes away.

## Licensing

**All code is MIT. Reference data is CC BY 4.0**, and third-party material keeps its own terms,
recorded per file in the repository that vendors it.
