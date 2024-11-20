PqsE and HhqE orthologous sequences were downloaded from the following links: Pseudomonas Genome DB (https://pseudomonas.com/orthologs/list?id=1653897) and Burkholderia Genome DB (https://www.burkholderia.com/orthologs/list?id=21479956) which resulted in the following .csv files `PqsE_ortholog.csv` and `HhqE_ortholog.csv`.
Sequences were aligned with MUSCLE

    muscle -in PqsE_HhqE_ortholog.faa -out PqsE_HhqE_ortholog_aln.faa

Trimmed with trimal
    
    trimal -in PqsE_HhqE_ortholog_aln.faa -out PqsE_HhqE_ortholog_aln_trm.faa -keepheader 
> Note: The '**-keepheader**' option sepcifies to keep headers, I've had unfortunate times with trimal stealing my headers without
Tree made with iTOL

    iqtree -s PqsE_HhqE_ortholog_aln_trm.faa -bb 1000 -m
