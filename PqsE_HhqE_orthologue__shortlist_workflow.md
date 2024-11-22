
PqsE and HhqE sequences were downloaded from the following links: Pseudomonas Genome DB (https://pseudomonas.com/orthologs/list?id=1653897) and Burkholderia Genome DB (https://www.burkholderia.com/orthologs/list?id=21479956) which were manually copy/pasted into the following file `PqsE_homologs_shortlist.faa`.

Sequences were aligned with MUSCLE

    muscle -in PqsE_homologs_shortlist.faa -out PqsE_homologs_shortlist_aln.faa

Trimmed with trimal
    
    trimal -in PqsE_homologs_shortlist_aln.faa -out PqsE_homologs_shortlist_aln_trm.faa -keepheader 
> Note: The '**-keepheader**' option sepcifies to keep headers, I've had unfortunate times with trimal stealing my headers without

Tree made with iqtree

    iqtree -s PqsE_homologs_shortlist_aln_trm.faa -bb 1000 -m


