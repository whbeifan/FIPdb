FIPdb（Fungal Immunomodulatory Proteins Database）
==============
## Version: 1.0.0
A total of 1005 fungal immunomodulatory proteins were collected from the UniProt, Pfam and NR databases, which were reduced to 739 non-redundant proteins after deduplication.

Third-party
-----------
FIPdb includes some third-party software:
* [diamond](https://github.com/bbuchfink/diamond)
* [hmmer](http://hmmer.org/)
* [PF09259](https://www.ebi.ac.uk/interpro/entry/pfam/PF09259/logo/)
* [interpro](https://www.ebi.ac.uk/interpro/search/sequence/) #Annotation result verification


Usage
------------
```
git clone https://github.com/whbeifan/FIPdb
#or
#wget -c https://github.com/whbeifan/FIPdb/archive/refs/tags/v1.0.0.tar.gz
gunzip FIPdb.faa.gz PF09259.hmm.gz
#Build a database
diamond makedb --in FIPdb.faa -d FIPdb
#Perform alignment and annotation
diamond blastp --query BF.faa --db FIPdb.dmnd --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore qlen slen stitle --max-target-seqs 5 --evalue 1e-05 --threads 10 --out BF.FIPdb.m6
#For better accuracy, we recommend setting the identity at 90% and validating the results.
blast_filter.py BF.FIPdb.m6 --outfmt std qlen slen stitle --out qseqid sseqid pident length qlen slen qstart qend sstart send stitle evalue bitscore --min_pident 50 --min_qcov 80 --min_scov 80 --evalue 1e-05 --best_evalue 1 > BF.FIPdb.tsv
#Strictly compare
hmmsearch --cut_tc --cpu 8 --tblout BF.FIPdb_pfam.tsv PF09259.hmm BF.faa > pfam_log.txt
```

References
------------
[1] Paaventhan P, Joseph JS, Seow SV, et al. A 1.7A structure of Fve, a member of the new fungal immunomodulatory protein family. J Mol Biol. 2003;332(2):461-470. doi:[10.1016/s0022-2836(03)00923-9](https://pubmed.ncbi.nlm.nih.gov/12948495/)
