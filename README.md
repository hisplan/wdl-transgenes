# SEQC Custom Genes

## How to Test

### GCP

```bash
./submit.sh \
    -k ~/secrets-gcp.json \
    -i ./config/SeqcCustomGenes.inputs.gcp.json \
    -l ./config/SeqcCustomGenes.labels.gcp.json \
    -o SeqcCustomGenes.options.gcp.json
```

### AWS

```bash
./submit.sh \
    -k ~/secrets-aws.json \
    -i ./config/Tp53_Rb_PtenGEMM-TKO12_week_1.inputs.aws.json \
    -l ./config/Tp53_Rb_PtenGEMM-TKO12_week_1.labels.aws.json \
    -o SeqcCustomGenes.options.aws.json
```
