# Campy-4G: Campylobacter Plasmid Typing Database (ABRicate format)

**Campy-4G** is a four-gene plasmid backbone typing database for *Campylobacter* plasmids.  
It enables rapid, standardized typing of plasmids from whole-genome assemblies using **ABRicate**.

The scheme contains curated marker genes representing the core *Campylobacter* plasmid backbone:

- **rep** – replication genes  
- **mob** – mobilization / relaxase genes  
- **ssb** – single-stranded DNA binding protein genes  
- **virD4** – Type IV secretion system coupling protein genes

These markers can be detected directly from contigs using ABRicate, enabling consistent plasmid typing across *Campylobacter* species.

## Contents

```
Campy-4G/
 ├── Campy-4G.fa       # FASTA file with all rep, mob, ssb and virD4 markers
 ├── README.md       # this file
```

## Installation

Campy-4G works exactly like any custom ABRicate database.  
ABRicate expects a directory inside its `--datadir` (default: `~/.abricate/db`) containing:

- a directory named `Campy-4G/`
- a FASTA file named `sequences` (no extension)
- indexes created by `abricate --setupdb`

### 1. Copy the database into ABRicate’s database folder

```
cd /path/to/abricate/db
mkdir Campy-4G
cp /path/to/Campy-4G.fa Campy-4G/sequences
```

### 2. Inspect database (optional)

```
>Campy-4G~~~GENE_TYPE~~~GENE
nucleotide sequences of marker genes
```

### 3. Build BLAST database

```
abricate --setupdb
```

or

```
cd Campy-4G
makeblastdb -in sequences -title Campy-4G -dbtype nucl -hash_index
```

### 4. Verify installation

```
abricate --list

DATABASE  SEQUENCES  DBTYPE  DATE
Campy-4G   108        nucl    2025-Nov-19
```

## Usage

```
abricate --db Campy-4G assembly.fasta
```

Recommended:  
--minid: Proportion of gene covered - 80%  
--mincov: Proportion of exact nucleotide matches - 90%  

```
abricate --db Campy-4G --minid 80 --mincov 90 assembly.fasta
```

## Interpretation
Campy-4G produces a tap-separated output file with in column "GENE" the marker genes:   

| GENE | description |
| ---- | ----------- |
| rep_00 | replication gene followed by typing number |
| mob_00 | mobilization gene followed by typing number |
| ssb_00 | single-stranding DNA binding protein gene followed by typing number |
| vir_00 | T4SS virD4 gene followed by typing number |

Typing patterns can be noted as follows:
```
rep59-mob04-ssb03-vir01
rep07-mob15-ssb08-vir03
```

## Citation

Campy-4G: van der Graaf-van Bloois et al. *Manuscript submitted.*  
Abricate: T. Seemann. Github https://github.com/tseemann/abricate

## Contact

Maintainer: Aldert Zomer  
Utrecht University  
A.L.Zomer@uu.nl
