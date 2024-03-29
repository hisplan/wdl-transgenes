# wdl-transgenes

- Creating a transgene-included reference package for Cell Ranger
- Creating a transgene-included genome index for STAR Aligner

## License

The code is available to everyone under the standard [MIT license](./LICENSE). However, the code internally uses 10x software for certain things, so please make sure that you read and agree to [10x End User Software License](https://www.10xgenomics.com/end-user-software-license-agreement).

## Setup

The pipeline is a part of SCING (Single-Cell pIpeliNe Garden; pronounced as "sing" /siŋ/). For setup, please refer to [this page](https://github.com/hisplan/scing). All the instructions below is given under the assumption that you have already configured SCING in your environment.

## Create Job Files

You need two files - one inputs file and one labels file. Use the following example files to help you create your job file:

- `config/template.inputs.json`
- `config/template.labels.json`

### Inputs

Each key in the inputs JSON must have either one of the following prefixes:

- For Cell Ranegr: `TransgenesCellRanger.`
- For SEQC (or STAR Aligner in general): `TransgenesSeqc.`

#### Input FASTA File Requirements

Please refer to to the document [here](./docs/user-instructions.md).

#### Gene ID Prefix

`ensembleIdPrefix` must be set to either `ENS` or `ENSMUS`. For human + mouse hybrid, you have no choice but to either specify `ENS` or `ENSMUS` because the STAR aligner doesn't like any other prefix, and it doesn't even complain, but simply won't include the trangenes/reporter genes in the final annotation file.

#### Biotype Filtering

Only biotypes specified in `*.biotypes` will be retained from the input GTF file (`*.annotationGtf`):

For example:

```json
"TransgenesCellRanger.annotationGtf": "s3://seqc-public/genomes/GRCm38-Ensembl-98/annotations.gtf",
"TransgenesCellRanger.biotypes": [
    "protein_coding",
    "lincRNA",
    "antisense",
    "IG_V_gene",
    "IG_D_gene",
    "IG_J_gene",
    "IG_C_gene",
    "TR_V_gene",
    "TR_D_gene",
    "TR_J_gene",
    "TR_C_gene"
],
```

#### References

You need to specify the standard reference genome and gene annotation file in `inputs.json`:

**Ensembl 85 (Human)**

Key                       | S3 URI
------------------------- | --------------------------------------------------------------
`*.genomeReferenceFasta`  | `s3://seqc-public/genomes/hg38_long_polya/homo_sapiens.fa`
`*.annotationGtf`         | `s3://seqc-public/genomes/hg38_long_polya/annotations.gtf`

This GTF is a pre-filtered annotation.

**Ensembl 87 (Mouse)**

Key                       | S3 URI
------------------------- | --------------------------------------------------------------
`*.genomeReferenceFasta`  | `s3://seqc-public/genomes/mm38_long_polya/mus_musculus.fa`
`*.annotationGtf`         | `s3://seqc-public/genomes/mm38_long_polya/annotations.gtf`

This GTF is a pre-filtered annotation.

**Ensembl 98 (Human)**

Key                       | S3 URI
------------------------- | --------------------------------------------------------------
`*.genomeReferenceFasta`  | `s3://seqc-public/genomes/GRCh38-Ensembl-98/homo_sapiens.fa`
`*.annotationGtf`         | `s3://seqc-public/genomes/GRCh38-Ensembl-98/annotations.gtf`

- This GTF is a pre-filtered annotation.
- Cell Ranger's default reference package 2020-A (July 7, 2020) is based on Ensembl 98.

**Ensembl 98 (Mouse)**

Key                       | S3 URI
------------------------- | --------------------------------------------------------------
`*.genomeReferenceFasta`  | `s3://seqc-public/genomes/GRCm38-Ensembl-98/mus_musculus.fa`
`*.annotationGtf`         | `s3://seqc-public/genomes/GRCm38-Ensembl-98/annotations.gtf`

- This GTF is a pre-filtered annotation.
- Cell Ranger's default reference package 2020-A (July 7, 2020) is based on Ensembl 98.

**Ensembl 100 (Human)**

Key                       | S3 URI
------------------------- | --------------------------------------------------------------
`*.genomeReferenceFasta`  | `s3://seqc-public/genomes/GRCh38-Ensembl-100/homo_sapiens.fa`
`*.annotationGtf`         | `s3://seqc-public/genomes/GRCh38-Ensembl-100/annotations.gtf`

This GTF is a pre-filtered annotation.

**Ensembl 100 (Mouse)**

Key                       | S3 URI
------------------------- | --------------------------------------------------------------
`*.genomeReferenceFasta`  | `s3://seqc-public/genomes/GRCm38-Ensembl-100/mus_musculus.fa`
`*.annotationGtf`         | `s3://seqc-public/genomes/GRCm38-Ensembl-100/annotations.gtf`

This GTF is a pre-filtered annotation.

## Submit Your Job

For Cell Ranger:

```bash
conda activate scing

./submit-cellranger.sh \
    -k ~/keys/cromwell-secrets.json \
    -i configs/sample.inputs.json \
    -l configs/sample.labels.json \
    -o TransgenesCellRanger.options.aws.json
```

For SEQC (or STAR Aligner in general):

```bash
conda activate scing

./submit-seqc.sh \
    -k ~/keys/cromwell-secrets.json \
    -i configs/sample.inputs.json \
    -l configs/sample.labels.json \
    -o TransgenesSeqc.options.aws.json
```

## Outputs

- STAR index and `annotations.gtf` for SEQC.
- Reference pakcage for Cell Ranger
- GTF filter log if only certain biotypes were kept.
- FASTA/Index file for IGV visualization (`fa.gz` and `fa.gz.gzi`).
