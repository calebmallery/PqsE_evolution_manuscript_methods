PqsE and HhqE orthologous sequences were downloaded from the following links: Pseudomonas Genome DB (https://pseudomonas.com/orthologs/list?id=1653897) and Burkholderia Genome DB (https://www.burkholderia.com/orthologs/list?id=21479956) which resulted in the following .csv files `PqsE_ortholog.csv` and `HhqE_ortholog.csv`.

Since there are a lot of unwanted symbols from `HhqE_ortholog.csv` file, I used regex commands to find and replace a few things
    
    searched for "," replaced with "\n". Then searched for "(^B)" and replaced with >\1.

Some species names had "assembly" tacked onto the end. To get rid of that:
    
    I searched for \s-\sAssembly\s and replaced with "_"

I followed the same as above for `PqsE_ortholog.csv`.

The two cleaned files were renamed `PqsE_ortholog.faa` and `HhqE_ortholog.faa` and concatonated into one file `PqsE_HhqE_ortholog.faa`

    cat PqsE_ortholog.faa HhqE_ortholog.faa > PqsE_HhqE_ortholog.faa

Some sequence names still sucked and were too janky for MUSCLE, so I removed the symbols with the following sed commands

   
    sed -i 's/ /_/g' pqsE_orthologs.faa
    sed -i 's/-/_/g' pqsE_orthologs.faa
    sed -i 's/[.]/_/g' pqsE_orthologs.faa
    sed -i 's/#/_/g' pqsE_orthologs.faa
    sed -i 's/[/]/_/g' pqsE_orthologs.faa
    sed -i 's/__/_/g' pqsE_orthologs.faa

Sequence was aligned with MUSCLE

    muscle -in PqsE_HhqE_ortholog.faa -out PqsE_HhqE_ortholog_aln.faa

Trimmed with trimal
    
    trimal -in PqsE_HhqE_ortholog_aln.faa -out PqsE_HhqE_ortholog_aln_trm.faa -keepheader 
> Note: The '**-keepheader**' option sepcifies to keep headers, I've had unfortunate times with trimal stealing my headers without

Tree made with iqtree

    iqtree -s PqsE_HhqE_ortholog_aln_trm.faa -bb 1000 -m

The file `PqsE_HhqE_ortholog_aln_trm.faa.treefile` was uploaded to iTOL for visualization
