# anndata-omics-bridge

What if you use the same data format when running proteomics, genomics, or metabolomics analyses, and program in Python, R, Rust, or JavaScript?

Planning for __anndata-omics-bridge__ started in 2025 to use anndata for proteomics, genomics, and metabolomics analysis at the FGCZ.

Work on the __anndata-proteomics-bridge__ (APB) started during the Copenhagen ProteoBench Hackathon, 13–17 April 2026, as part of changes to the [ProteoBench](https://proteobench.cubimed.rub.de/) backend. [ProteoBench](https://github.com/proteobench/proteobench) contains parsers for software-specific result tables, search-parameter files, and modification encodings for a dozen quantification tools for DDA and DIA.  

The kernel of APB is two packages, side by side:

- [apb2](https://github.com/anndata-omics-bridge/apb2) ports those parsers into a rules-driven converter: the result tables of each quantification tool become one AnnData/MuData layout, which retains the fields specific to that tool. It reads AlphaDIA, DIA-NN, FragPipe, MaxQuant, Spectronaut and [9 more](https://anndata-omics-bridge.github.io/apb2/supported_software/).
- [apb-catalog](https://github.com/anndata-omics-bridge/apb-catalog) records what those fields mean, so an application asks for a meaning, such as a PEP or an unnormalized intensity, instead of a vendor column. Its API exists in Python, in R as [apbCatalogR](https://github.com/anndata-omics-bridge/apbCatalogR), and in TypeScript as [apb-catalog-ts](https://github.com/anndata-omics-bridge/apb-catalog-ts).

![Who does what: apb2 converts the results of quantification software into an APB result and the integrator fills the catalog; Bioconductor applications such as prolfqua, exploreDE and QFeatures read the result by meaning through the apb-catalog API, in R with apbCatalogR.](apb_actors.png)

Browse online:

- [Rules viewer](https://fgcz-ms.uzh.ch/public/apb-rules/): every vendor table's parse rules, as apb2 packages them
- [Catalog viewer](https://fgcz-ms.uzh.ch/public/apb-catalog/): every catalog set with its entries and coverage
- [APB Studio](https://fgcz-ms.uzh.ch/public/apb-studio/): APB's corpus runs over the test vendor files
- [APB Export](https://apps-dev.bfabric.org/apb-export/): convert a vendor table for a downstream tool in the browser

With [apb-fasta](https://github.com/anndata-omics-bridge/apb-fasta) and [apb-proteobench](https://github.com/anndata-omics-bridge/apb-proteobench), we demonstrate how to build analysis pipelines using APB.

See the ProteoBench preprint, [*ProteoBench: the community-curated platform for comparing proteomics data analysis workflows*](https://doi.org/10.64898/2025.12.09.692895).

The development of APB was further motivated by supporting vendor-specific readers in [`prolfquapp::preprocess_software()`](https://prolfqua.github.io/prolfquapp/man/preprocess_software.html) and [`prolfquappPTMreaders`](https://github.com/prolfqua/prolfquappPTMreaders), and the intention to transform it into a community effort.


## APB kernel

| Repository | What it is | Documentation |
| --- | --- | --- |
| [apb2](https://github.com/anndata-omics-bridge/apb2) | APB — rules-driven conversion of quantification output tables to AnnData/MuData, with vendor parameter parsing | [docs](https://anndata-omics-bridge.github.io/apb2/) |
| [apb-catalog](https://github.com/anndata-omics-bridge/apb-catalog) | Catalogues of what APB result fields mean, so consumers ask for a meaning instead of a vendor column: identification confidence, abundance, chromatography and ProteoBench entrapment fields | [docs](https://anndata-omics-bridge.github.io/apb-catalog/) |
| [apbCatalogR](https://github.com/anndata-omics-bridge/apbCatalogR) | apb-catalog's API in R: look up APB result fields by meaning | [docs](https://anndata-omics-bridge.github.io/apbCatalogR/) |
| [apb-catalog-ts](https://github.com/anndata-omics-bridge/apb-catalog-ts) | apb-catalog's API in TypeScript, on npm as `@anndata-omics-bridge/apb-catalog`: look up APB result fields by meaning in the browser | [docs](https://anndata-omics-bridge.github.io/apb-catalog-ts/) |

## APB tools

| Repository | What it is | Documentation |
| --- | --- | --- |
| [apb-fasta](https://github.com/anndata-omics-bridge/apb-fasta) | FASTA verification and protein annotation for APB2 results | [docs](https://anndata-omics-bridge.github.io/apb-fasta/) |
| [apb-proteobench](https://github.com/anndata-omics-bridge/apb-proteobench) | ProteoBench-specific annotation and scoring for APB results | [docs](https://anndata-omics-bridge.github.io/apb-proteobench/) |
| [apb-export](https://github.com/anndata-omics-bridge/apb-export) | Exports of APB2 results as the files downstream tools read: msmu, MSstats, Perseus, prolfqua, ProteoPy, exploreDE, alphapepttools, QFeatures and QPX | [docs](https://anndata-omics-bridge.github.io/apb-export/) |
| [apb-export-ui](https://github.com/anndata-omics-bridge/apb-export-ui) | Web application for APB Export: upload a vendor table, choose a target, check its quality, download the export; [try it](https://apps-dev.bfabric.org/apb-export/) | [docs](https://anndata-omics-bridge.github.io/apb-export-ui/) |
| [apb-pmultiqc](https://github.com/anndata-omics-bridge/apb-pmultiqc) | pMultiQC reports from stored APB results through the QPX export | — |
| [apb-plasma](https://github.com/anndata-omics-bridge/apb-plasma) | Plasma MS quality control: reference datasets, quality-marker panels, and the QC metric catalogue | — |
| [abp_studio](https://github.com/anndata-omics-bridge/abp_studio) | Fixture manager and corpus runner that drives the APB CLI over real vendor files | [docs](https://anndata-omics-bridge.github.io/abp_studio/) |

## Infrastructure packages

| Repository | What it is | Documentation |
| --- | --- | --- |
| [protein-fasta](https://github.com/anndata-omics-bridge/protein-fasta) | Streaming FASTA parsing, header interpretation, classification, and validation | [docs](https://anndata-omics-bridge.github.io/protein-fasta/) |
| [prozor](https://github.com/anndata-omics-bridge/prozor) | Python port of the R `prozor` package for typed peptide-to-protein matching and deterministic greedy-parsimony protein inference | [docs](https://anndata-omics-bridge.github.io/prozor/) |

## Specification and previous implementation

| Repository | What it is | Documentation |
| --- | --- | --- |
| [anndata-omics-bridge](https://github.com/anndata-omics-bridge/anndata-omics-bridge) | Format specification and cross-project documentation | — |
| [anndata-proteomics-bridge](https://github.com/anndata-omics-bridge/anndata-proteomics-bridge) | Archived APB v1 repository | [docs](https://anndata-omics-bridge.github.io/anndata-proteomics-bridge/) |

## Licensing

**All code is MIT, except the anndata-omics-bridge specification repository, which is CC BY 4.0. Reference data is CC BY 4.0**, and third-party material keeps its own terms, recorded per file in the repository that vendors it.
