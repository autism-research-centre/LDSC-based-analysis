# LDSC-based-analysis

## These are basic commands for running LDSC based analyses

### Partitioned heritability

```bash
ldsc.py --h2 sumstats/file.sumstats --ref-ld-chr 1000G_EUR_Phase3_baseline/baseline. --w-ld-chr weights_hm3_no_hla/weights. --overlap-annot --frqfile-chr 1000G_Phase3_frq/1000G.EUR.QC. --out results/file_baseline_parther
```
