# singularity_cellranger
## Reusing the Recipe

Upon reusing the recipe to create container images, note that each time a new download link has to be generated from 10X website
https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest
Delete the old link in the recipe and replace it with the new link.

## Starting the Singularity Container and Bind-moungting 
### Using the pre-built version
First pull the singularity image from Singularity Hub with the optional renaming parameter. The --disable-cache command is also optional. If working on a machine/server where the cache size is limited to below the image size (11G), then --disable-cache can be added for the work-around. This option is required if working on Duke Compute Cluster as each user there only has 10G of personal space in the home directory, which will lead to interruption of pulling.
```
singularity pull [--disable-cache] [--name your_image_name.sif] shub://DylanYang7225/Cellranger
```

Given that the pre-built image has been pulled or a singularity image has been built (suppose the self-built image is also named your_image_name.sif), then the following command could be run to start the container
```
singularity shell --bind /local_data_directory:/data,/local_cellranger_output_directory:/cellranger_output your_image_name.sif
```

## Running Cellranger 
Please make sure that /cellranger_output is bind-mounted to a local directory where you have writing permission. Before running Cellranger, we need to change to the output directory as cellranger automatically writes to the current directory
```
cd /cellranger_output
```
Processing Single-cell RNA-seq Data
```
cellranger count --id=your_result_name --transcriptome=/cellranger/refdata-cellranger-GRCh38-3.0.0 --fastqs=/data/your_fastq_file_directory
```
Processing TCR-seq Data
```
cellranger vdj --id=your_result_name --reference=/cellranger/refdata-cellranger-vdj-GRCh38-alts-ensembl-3.1.0 --fastqs/data/your_fastq_file_directory
```
