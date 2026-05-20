FIPdb（Fungal Immunomodulatory Proteins Database）
==============
## Version: 1.0.0
A total of 906 fungal immunomodulatory proteins were collected from the UniProt and NR databases, which were reduced to 688 non-redundant proteins after deduplication.

## Usage
```
#gunzip FIPdb.faa.gz
diamond makedb --in FIPdb.faa -d FIPdb
diamond blastp --query BF.faa --db FIPdb.dmnd --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore qlen slen stitle --max-target-seqs 5 --evalue 1e-05 --threads 10 --out BF.FIPdb.m6
blast_filter.py BF.FIPdb.m6 --outfmt std qlen slen stitle --out qseqid sseqid pident length qlen slen qstart qend sstart send stitle evalue bitscore --min_pident 50 --min_qcov 80 --min_scov 80 --evalue 1e-05 --best_evalue 1 > BF.FIPdb.tsv
```

