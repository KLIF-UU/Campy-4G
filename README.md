# Campy-4G: Campylobacter Plasmid Typing Database (ABRicate format)

**Campy-4G** is a four-gene plasmid backbone typing database for *Campylobacter* plasmids.  
It enables rapid, standardized typing of plasmids from whole-genome assemblies using **ABRicate**.

The scheme contains curated marker genes representing the core *Campylobacter* plasmid backbone:

- **rep** – replication genes  
- **mob** – mobilization / relaxase genes  
- **ssb** – single-strand DNA binding protein genes  
- **virD4** – Type IV secretion system coupling protein genes

These markers can be detected directly from contigs using ABRicate, enabling consistent plasmid typing across *Campylobacter* species.

## Contents

```
Campy-4G/
 ├── sequences       # FASTA file with all rep, mob, ssb and virD4 markers
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

### 2. Inspect header format (optional)

```
>Campy-4G~~~GENE_ID~~~TYPE description...
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
```

## Usage

```
abricate --db Campy-4G assembly.fasta
```

Recommended:

```
abricate --db Campy-4G --minid 80 --mincov 90 assembly.fasta
```

## Interpretation

Patterns look like:

```
rep59-mob04-ssb03-vir01
rep07-mob15-ssb08-vir03
```

## Database Format

```
>Campy-4G~~~<GENE_ID>~~~<GENE_TYPE> optional description
nucleotide sequence of marker gene
```

## Citation

van der Graaf-van Bloois et al. *Manuscript submitted.*

## Contact

Maintainer: Aldert Zomer  
Utrecht University  
A.L.Zomer@uu.nl
