# TENET.AnnotationHub_files

### Hosting .narrowPeak and .bed files downloaded/processed from GEO and ENCODE sources that were used to create [TENET.AnnotationHub](https://github.com/rhielab/TENET.AnnotationHub) objects

## Dataset descriptions

Component datasets were first identified using the [Cistrome Data Browser v2.0](http://cistrome.org/db/). *Homo sapiens* was selected as the species, while H3K4me1 and H3K27ac (for enhancers), H3K4me3 (for promoters), or ATAC-seq and DNase-seq (for open chromatin) were selected as factors of interest. For each of 10 cancer types (BLCA, BRCA, COAD, ESCA, HNSC, KIRP, LIHC, LUAD, LUSC, and THCA; see the [TCGA study abbreviations](https://gdc.cancer.gov/resources-tcga-users/tcga-code-tables/tcga-study-abbreviations)), an initial search was performed using the organ each cancer type arose from as the search term.

First, we removed datasets which were derived from biological sources which were not directly relevant to the cancer type of interest (e.g., lung fibroblasts and A549 cells, a LUAD cell line, from the LUSC relevant datasets). We also removed datasets which failed at least three of the six quality control metrics recorded by Cistrome (sequence quality, mapping quality, library complexity, ChIP enrichment, signal to noise ratio, and regulatory region ratio). Samples that had a chemical, siRNA, or genetic alteration performed on them were also removed, though we elected to keep samples which had mild control treatments (e.g., EtOH or vehicle control) applied to them. Finally, we removed samples with fewer than 10 million reads, as well as any samples for which we were unable to acquire the FASTQ files to perform peak calling.

Peak calling was performed using the [ENCODE ChIP-seq pipeline](https://github.com/ENCODE-DCC/chip-seq-pipeline) for H3K4me1, H3K4me3, and H3K27ac datasets, and the [ENCODE ATAC-seq pipeline](https://github.com/ENCODE-DCC/atac-seq-pipeline) for ATAC-seq and DNase-seq datasets. All datasets were aligned to the hg38 human genome.

After peaks had been called, we performed a second round of curation, where we removed datasets with fewer than 10,000 called peaks. Finally, for each combination of biological source and data type (i.e. MCF7 cells and H3K27ac), we collected all datasets that passed other curation criteria, then kept all datasets tied for the most Cistrome quality control metrics passed and removed datasets which had fewer. Experimental replicates were considered as individual datasets, though input replicates from those experiments were pooled into single datasets for use in peak calling.

The enhancer and promoter datasets use only these peak files, while the open chromatin dataset also includes ATAC-seq peaks from TCGA for the 10 cancer types of interest (see [Corces et al., The chromatin accessibility landscape of primary human cancers](https://www.science.org/doi/10.1126/science.aav1898)).

Manifests for these files detailing, among other information, the ENCODE/GEO experiments where the files originate, are available as .tsv files in this repository. These manifests are also available in the [data-raw directory of the TENET.AnnotationHub repository](https://github.com/rhielab/TENET.AnnotationHub/tree/devel/data-raw).
