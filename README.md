# SEQC Custom Genes

## Input FASTA File Requirements

1. Each FASTA file must conform to the standard FASTA file format specification.
1. The entire sequence must be in one line.
1. The last line of the FASTA file must end with a newline character (i.e. `\n`)
1. The FASTA filename must have a extension `.fa` (not `.fasta`)

*Bad Example 1*

```bash
$ cat egfp.fa
>EGFP
AGCAAGGGCGAGGAGCTGTTCACCGGGGTG
GTGCCCATCCTGGTCGAGCTGGACGGCGAC
GTAAACGGCCACAAGTTCAGCGTGTCCGGC
GAGGGCGAGGGCGATGCCACCTACGGCAAG
CTGACCCTGAAGTTCATCTGCACCACCGGC
AAGCTGCCCGTGCCCTGGCCCACCCTCGTG
ACCACCCTGACCTACGGCGTGCAGTGCTTC
AGCCGCTACCCCGACCACATGAAGCAGCAC
GACTTCTTCAAGTCCGCCATGCCCGAAGGC
TACGTCCAGGAGCGCACCATCTTCTTCAAG
GACGACGGCAACTACAAGACCCGCGCCGAG
GTGAAGTTCGAGGGCGACACCCTGGTGAAC
CGCATCGAGCTGAAGGGCATCGACTTCAAG
GAGGACGGCAACATCCTGGGGCACAAGCTG
GAGTACAACTACAACAGCCACAACGTCTAT
ATCATGGCCGACAAGCAGAAGAACGGCATC
AAGGTGAACTTCAAGATCCGCCACAACATC
GAGGACGGCAGCGTGCAGCTCGCCGACCAC
TACCAGCAGAACACCCCCATCGGCGACGGC
CCCGTGCTGCTGCCCGACAACCACTACCTG
AGCACCCAGTCCGCCCTGAGCAAAGACCCC
AACGAGAAGCGCGATCACATGGTCCTGCTG
GAGTTCGTGACCGCCGCCGGGATCACTCTC
GGCATGGACGAGCTGTACAAG
```

- Why: The whole sequence must not be splitted into multiple lines.
- How to correct: The entire sequence must be in one line as shown below:

```bash
>EGFP
AGCAAGGGCGAGGAGCTGTTCACCGGGGTGGTGCCCATCCTGGTCGAGCTGGACGGCGACGTAAACGGCCACAAGTTCAGCGTGTCCGGCGAGGGCGAGGGCGATGCCACCTACGGCAAGCTGACCCTGAAGTTCATCTGCACCACCGGCAAGCTGCCCGTGCCCTGGCCCACCCTCGTGACCACCCTGACCTACGGCGTGCAGTGCTTCAGCCGCTACCCCGACCACATGAAGCAGCACGACTTCTTCAAGTCCGCCATGCCCGAAGGCTACGTCCAGGAGCGCACCATCTTCTTCAAGGACGACGGCAACTACAAGACCCGCGCCGAGGTGAAGTTCGAGGGCGACACCCTGGTGAACCGCATCGAGCTGAAGGGCATCGACTTCAAGGAGGACGGCAACATCCTGGGGCACAAGCTGGAGTACAACTACAACAGCCACAACGTCTATATCATGGCCGACAAGCAGAAGAACGGCATCAAGGTGAACTTCAAGATCCGCCACAACATCGAGGACGGCAGCGTGCAGCTCGCCGACCACTACCAGCAGAACACCCCCATCGGCGACGGCCCCGTGCTGCTGCCCGACAACCACTACCTGAGCACCCAGTCCGCCCTGAGCAAAGACCCCAACGAGAAGCGCGATCACATGGTCCTGCTGGAGTTCGTGACCGCCGCCGGGATCACTCTCGGCATGGACGAGCTGTACAAG
```

*Bad Example 2*

```bash
$ cat mCherry.fa
>mCherry
ATGGTGAGCAAGGGCGAGGAGGATAACATGGCCATCATCAAGGAaTTtATGCGCTTCAAaGTtCACATGGAGGGCTCCGTGAACGGCCACGAGTTCGAGATCGAGGGCGAGGGCGAGGGCCGCCCCTACGAGGGCACCCAaACaGCCAAGCTGAAGGTtACCAAGGGTGGCCCCCTGCCCTTCGCCTGGGACATCCTGTCCCCTCAaTTtATGTAtGGCTCCAAGGCCTACGTGAAGCACCCCGCCGACATCCCCGACTACTTGAAGCTGTCCTTCCCCGAGGGCTTCAAGTGGGAGCGCGTGATGAACTTCGAGGACGGCGGCGTGGTGACCGTGACCCAGGACTCCTCCCTGCAaGACGGCGAGTTCATCTACAAaGTtAAGCTGCGgGGaACCAACTTCCCCTCCGACGGCCCCGTAATGCAGAAGAAGACCATGGGCTGGGAGGCCTCCTCCGAGCGGATGTACCCCGAGGACGGCGCCCTGAAGGGCGAGATCAAGCAGAGGCTGAAGCTGAAGGACGGCGGCCACTACGACGCTGAGGTCAAGACCACCTACAAGGCCAAGAAGCCCGTGCAGCTGCCCGGCGCCTACAACGTCAACATCAAGTTGGACATCACCTCCCACAACGAGGACTACACCATCGTGGAACAaTACGAACGCGCCGAGGGCCGCCACTCCACCGGCGGCATGGACGAGCTGTACAAG$
```

- Why: The sequence line does not end with a newline character (`\n`). Your bash prompt (i.e. `$`) is displayed at the end of the sequence when you run the `cat` command to display the contents of the file.
- How to correct: Add a new line character (`\n`) at the end of the sequence as shown below. Your bash prompt must show up at the next line when you run the `cat` command:

```bash
$ cat mCherry.fa
>mCherry
ATGGTGAGCAAGGGCGAGGAGGATAACATGGCCATCATCAAGGAaTTtATGCGCTTCAAaGTtCACATGGAGGGCTCCGTGAACGGCCACGAGTTCGAGATCGAGGGCGAGGGCGAGGGCCGCCCCTACGAGGGCACCCAaACaGCCAAGCTGAAGGTtACCAAGGGTGGCCCCCTGCCCTTCGCCTGGGACATCCTGTCCCCTCAaTTtATGTAtGGCTCCAAGGCCTACGTGAAGCACCCCGCCGACATCCCCGACTACTTGAAGCTGTCCTTCCCCGAGGGCTTCAAGTGGGAGCGCGTGATGAACTTCGAGGACGGCGGCGTGGTGACCGTGACCCAGGACTCCTCCCTGCAaGACGGCGAGTTCATCTACAAaGTtAAGCTGCGgGGaACCAACTTCCCCTCCGACGGCCCCGTAATGCAGAAGAAGACCATGGGCTGGGAGGCCTCCTCCGAGCGGATGTACCCCGAGGACGGCGCCCTGAAGGGCGAGATCAAGCAGAGGCTGAAGCTGAAGGACGGCGGCCACTACGACGCTGAGGTCAAGACCACCTACAAGGCCAAGAAGCCCGTGCAGCTGCCCGGCGCCTACAACGTCAACATCAAGTTGGACATCACCTCCCACAACGAGGACTACACCATCGTGGAACAaTACGAACGCGCCGAGGGCCGCCACTCCACCGGCGGCATGGACGAGCTGTACAAG
$
```

## Outputs

- STAR index and `annotations.gtf` for SEQC.
- SEQC outputs if specified.
- FASTA/Index file for IGV visualization (`fa.gz` and `fa.gz.gzi`).

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
