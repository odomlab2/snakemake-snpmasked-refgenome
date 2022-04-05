# SNP-masked refererence genome

Create a reference genome sequence with "injected" SNPs/SNVs from other mouse strains.

## Input files

- mouse reference genome
- mouse annotation (GTF)
- SNP file

## Dependencies

The `snpsplit` tool is defined in a conda environment in `workflow/envs/snpslit.yml`.

*CellRanger* is proprietary software and cannot be installed via Conda. It needs to be manually downloaded and the path
to its executable stored in `workflow/config.yaml`.

On the DKFZ Compute Cluster Cellranger is installed as module and available at:
`/software/cellranger/6.0.0/bin/cellranger mkref`

## Configuration

The configuration in `workflow/config.yaml` contains:

- path to reference genome
- path to gene annotation
- path to `cellranger mkref`
- list of Strains from the mouse genome project (MGP)

## Run

The workflow can be run by executing:

```bash
snakemake -c1 --configfile config.yaml --use-conda
```

To use the LSF job scheduler on the DKFZ cluster run with

```bash
snakemake --cluster "bsub -n4 -q verylong -R rusage[mem=100GB]" -p -j2 -c4 --configfile config.yaml --use-conda
```

## Output files

Output files of the workflow are stored in the subdirectory `output/`

# TO DO

- Add a download function for the SNP data
  from `ftp.sanger.ac.uk/pub/REL-1505-SNPs_Indels/mgp.v5.merged.snps_all.dbSNP142.vcf.gz`
  This is currently not activated due to proxy issues in the DKFZ working.
