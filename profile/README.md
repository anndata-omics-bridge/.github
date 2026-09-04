# anndata-omics-bridge

What if you use the same data format when running proteomics, genomics or metabolomics analysis and either programming, with python, R, Rust of java script?

# A short history

Planning for anndata-omics-bridge started 2025 with discussion to use the same format anndata for proteomics, genomics and metabolomics analysis at the FGCZ.

Work on the anndata proteomics bridge (APB) started during the Copenhagen ProteoBench Hackathon, 13–17 April 2026, as part of changes to the [ProteoBench](https://proteobench.cubimed.rub.de/) backend. [ProteoBench](https://github.com/proteobench/proteobench) contains parsers for software-specific result tables, search-parameter files, and modification encodings for a dozen of quantification tools for DDA and DIA.  

APB2 (link) ports those parsers into a rules-driven converter and in addition retains fields specific to each input tool.
With apb-fasta and apb-proteobench we demonstrate how to build analysis pipelines using abp.

See the ProteoBench preprint, [*ProteoBench: the community-curated platform for comparing proteomics data analysis workflows*](https://doi.org/10.64898/2025.12.09.692895).

The development of APB was further motivated by supporting vendor-specific readers in [`prolfquapp::preprocess_software()`](https://github.com/prolfqua/prolfquapp/blob/master/R/preprocess_software.R#L137) and [`prolfquappPTMreaders`](https://github.com/prolfqua/prolfquappPTMreaders), and the intention to transform it into an community effort.


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
