Description

  Like in many animals, Tetrahymena’s Piwi family proteins (Twis) bind to small RNA (sRNA) to help maintain genome stability. sRNA classes Twis8p, Twi-Associated Short RNA-Targeting Ligase (TASL) and Adenine (A) rich pseudogenes become bound to Twis and are important for genome regulation and expression (Couvillion 2009). Twis influence DNA amplification and elimination (Farley 2017) and Twis8p knockouts have higher DNA damage responses (Lee 2021). TASLs facilitate the assembly of functional RNA-protein complexes necessary for vegetative growth and sexual reproduction. Similarly, pseudogenes, once considered unnecessary, can produce sRNAs that influence protein-coding sections in the genome (Farley 2017). These sRNAs importance and relation to Twis suggest being conserved in other Tetrahymena species but they have only been described in Tetrahymena thermophila. Here we show that some of these sRNAs are present in other Tetrahymena species.  

  The sRNA coordinates are originally described in table 1 of Farley 2017 but have since been updated to be more complete in a comma separated values (CSV) excel file with general feature format (GFF). Using the updated coordinates, we can ask how evolutionarily conserved the sRNAs are between species of Tetrahymena. To do this I’ve written three code cells in Jupyter using the biopython library to make a pipeline which allows for this sequence analysis to be easily repeatable (Figure 1A). The code CSVFastaBlastnPipeline.ipynb is publicly available on GitHub in the link below. The Jupyter server being used must have all the necessary libraries downloaded to run the code. 
  
  The first cell uses the pandas library in python to read the CSV file and the biopython library to manipulate fasta files. The Tetrahymena thermophila genome (Ciliate database 2023), the CSV file with the coordinates and an output file are labeled to the files in the directory at the top of cell 1. These should be downloaded and made, in the directory with the code. The T. thermophila genome has chromosome labels that are different than the ones in the provided CSV file, so a map is created between chromosome names. The start and end of a sequence can be easily expanded by the variable “difference”. 50 was chosen as the default setting so we expect 100 more nucleotides than described in the coordinates. Sequences are saved into a single fasta output file with their sRNA ID being their main title and their chromosome and coordinates saved in their description. After the code is run on a complete T. thermophila genome we’d expect to find all sequences. Although the downloadable provided genomes are described as being complete, they are not, as JBrowse on ciliate.org shows the complete genome and the missing sections. These missing sections can be millions of nucleotides long but only have a few pseudogenes or hypothetical proteins described with them so it can be inferred they were left out of the downloadable genome to save memory space. This reduces our amount of sRNA’s from the CSV file from 36 to 24 (Figure 1B). 
  
  The second cell uses the biopython library to branch one fasta file with multiple sequences into their own files in an output folder. Sequences from the output file from cell 1 are grabbed and placed into their own fasta file with the file name being the sRNA ID. Each new fasta file is created and placed into an output folder in the directory. This cell is easily adaptable to any fasta file by changing the name of the output file from cell 1 in the code.
  
  The third cell uses the fasta files in the output folder from cell 2 and the subprocess module to run basic local alignment search tool nucleotide (BLASTn) (Altschul 1990) on the uploaded ciliate genome. One ciliate genome is compared per run to make one database at a time. This temporary database made in the directory needs to be deleted after each run. The sequences in the output folder of cell 2 are compared to the database. A threshold for an acceptable E value for the alignment can be set by the variable “evalue_threshold” with a default setting of 1e-5. The best alignment is saved into a fasta file with all the alignments for that species. The sRNAs and the species they are found in are shown in figure 1B. Cell 3 was run with the T. thermophila genome and only had e values equal to 0, this shows it was working as expected. 
  
  At the time of writing, only the 4 species shown in figure 1B are publicly available on ciliate.org. Moving from left to right there are less sRNAs found in the Tetrahymena species and more E values greater than 0. We expect this as T. malaccensis is a sister taxa to T. thermophila and T.elliotti branches off from the internal node of this clade. T. borealis is the furthest phylogenetically from T. thermophila and we see the most variation as shown with more E values greater than 0. We expect some variability because speciation between Tetrahymena has been found to be associated with changes at high repeat regions (Xiong 2019). Although the amount of sRNAs found in other species is lower, the E values are consistent with expected results. Because of T. thermophila’s genome being incomplete it could be possible that the other genomes are incomplete too. When we focus on the sequences found in all genomes and their E values, Twis 4, 5 ,7, 9 and 12 are extremely conserved in the Tetrahymena species and the other sRNAs that are found are also highly conserved. In the future this pipeline can be run again with a complete T. thermophila genome and more Tetrahymena genomes to get a more complete picture of how conserved these sRNAs are.

![image](https://github.com/user-attachments/assets/53572f9e-fbb6-47fa-9885-cef1564ab96f)

Figure 1 Small RNA sequences found in different Tetrahymena species and the workflow in Jupyter. (A) The Jupyter workflow and what the code cells set to accomplish is described. (B) A full list of ID’s from the given coordinates is shown on the left under the "Small RNA" column. To the right four Tetrahymena species are listed with their column of x's showing if that rows sRNA was found in the genome. Top E-values found during BLASTn are shown when greater than 0.

Publicly available sequences

T.thermophila.genome.fasta
T.elliotti.genome.fasta
T.borealis.genome.fasta
T.malaccensis.genome.fasta

References

Altschul, S.F., Gish, W., Miller, W., Myers, E.W., Lipman, D.J. (1990) “Basic local alignment search tool.” J. Mol. Biol. 215:403-410.

Ciliate Database. (2023). T. Borealis genome database. Institute of Hydrobiology. Retrieved 11 14, 2023, from Ciliates (ihb.ac.cn)

Ciliate Database. (2023). T. Eliotti genome database. Institute of Hydrobiology. Retrieved 11 14, 2023, from Ciliates (ihb.ac.cn)

Ciliate Database. (2023). T. Malaccensis genome database. Institute of Hydrobiology. Retrieved 11 14, 2023, from Ciliates (ihb.ac.cn)

Ciliate Database. (2023). T. Thermophila genome database. Institute of Hydrobiology. Retrieved 11 14, 2023, from Ciliates (ihb.ac.cn)

Couvillion, M. T., Lee, S. R., Hogstad, B., et al. (2009). Sequence, biogenesis, and function of diverse small RNA classes bound to the Piwi family proteins of Tetrahymena thermophila. Genes & Development, 23(17), 2016-2032. DOI: 10.1101/gad.1821209.

Farley, B. M., & Collins, K. (2017). Transgenerational function of Tetrahymena Piwi protein Twi8p at distinctive noncoding RNA loci. RNA, 23(4), 530-545. doi:10.1261/rna.060012.116.

Lee, S. R., Pollard, D. A., Galati, D. F., et al. (2021). Disruption of a ∼23-24 nucleotide small RNA pathway elevates DNA damage responses in Tetrahymena thermophila. Molecular Biology of the Cell, 32(15), 1335-1346. doi:10.1091/mbc.E20-10-0631.

Xiong, J., Yang, W., Chen, K., Jiang, C., Ma, Y., Chai, X., et al. (2019). Hidden genomic evolution in a morphospecies—The landscape of rapidly evolving genes in Tetrahymena. PLoS Biology, 17(6), e3000294. https://doi.org/10.1371/journal.pbio.3000294.
