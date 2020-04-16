# singularity_cellranger

## Starting the Singularity Container and Bind-moungting 
```
singularity shell --bind /local_data_directory:/data,/local_cellranger_output_directory:/cellranger_output singularity_cellranger.sif
```

## Running Cellranger 
Please make sure that /cellranger_output is bind-mounted to a local directory where you have writing permission. Change to the output directory (as cellranger automatically writes to the current directory)
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
