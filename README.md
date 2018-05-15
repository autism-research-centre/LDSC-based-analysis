# LDSC-based-analysis

## These are basic commands for running LDSC based analyses

### Partitioned heritability

```bash
ldsc.py --h2 sumstats/file.sumstats --ref-ld-chr 1000G_EUR_Phase3_baseline/baseline. --w-ld-chr weights_hm3_no_hla/weights. --overlap-annot --frqfile-chr 1000G_Phase3_frq/1000G.EUR.QC. --out results/file_baseline_parther
```


## To create a new annotation
Note, this version has now been updated. To follow the new version, see: https://github.com/bulik/ldsc/wiki/LD-Score-Estimation-Tutorial

### Step 1: Get Ensembl gene IDs and SNPs for the genes in your list from: https://www.ensembl.org/biomart/martview/477edf3f6d8e48eaba1b68f0b7b09393

For SNPs, please choose "Variant Germline" under Attributes. Choose the variant name to get the RSID. 

### Step 2: Update an old annot file in R using the following commands:

```{R}
library(data.table)
Module = fread("read the module/gene set")
Module = Module[,1] # Keep only the columns wiht variant name
Module = unique(Module) # Keep only unique RSids

for (i in 1:22) {
data = fread(paste0("path to directory.", i, ".annot"))
data$Finalcolumnname = ifelse(data$SNP %in% Module$'variant name', 1, 0)
write.table(data, file = paste0("path to directory", i, ".annot"), row.names = F, col.names = T, quote = F)}
```

### Step 3: Create the files
Next, create the files for LDPred

```bash
for i in {1..22}; do python2 ldsc.py --l2 --bfile 1000G.mac5eur.${i} --ld-wind-cm 1 --annot GTexmagenta.${i}.annot --out GTexmagenta.${i} --print-snps hm.${i}.snp; done

```

### Step 4: Run partitioned heritability

```bash

```
