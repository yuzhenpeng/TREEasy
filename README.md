# TREEasy
  This tool can be used to infer species trees and phylogenetic networks from sequences

# Run the program & Parameters
  1.  Inferring species trees and phylogenetic networks from protein-coding sequences

    python TREEasy.py –d DIRECTORY –s SPECIES_NAME_FILE –g GENE_NAME_FILE –b BOOTSTRAP_CUTOFF –r ROOTED_TAXON –n MAX_NUMBER_NETWORK –k CROSS_VALUE_NETWORK –t PROCESSOR_NUMBER –c DATA_TYPE

-d: A directory path. This directory contains the required input files.

-s: A text file. This file contains species-individual(s) information. 

-g: A text file. This file contains gene-species name information. 

-b: A value from 0 to 100. This parameter is a cutoff value for bootstrap values in gene trees. If bootstrap values of all nodes in a gene tree are greater than the cutoff value, the gene tree will be used to infer species tree and networks.

-r: (a) species name(s). The TREEasy regards this taxon as root. If you have multi-outgroups, use “,” to separate species names.

    eg:
        Aten
        Asub, Agem

-n: An integer. This parameter is the maximum number of hybridizations that can be inferred. This value has a big impact on running time. We suggest that this value should be less than 5.

-k: An integer. This value is a cross-validation value for PhyloNet. This value has to be a multiple of the number of gene trees which are used to infer the phylogenetic network.

-t: An integer. This parameter is the number of processors to be used. We do not suggest using all processors in your device to run this program.  

-c: Data type. Data type. This parameter describes the input data type. There are two possible data types for the TREEasy. The first type is protein-coding sequences (CDS). You have to prepare two FASTA files for one gene. The first is the protein amino acid sequences in FASTA file named as XXX_aa.fasta (eg. CO1_aa.fasta), the other is corresponding nucleotide sequences in FASTA file named as XXX_nc.fasta (eg. CO1_nc.fasta). The second type is non-cds. Only one FASTA file is required as input named as XXX.fasta (eg. CO1.fasta). 

Here, we presented the command line for running empirical Acropora data below:
     
     cd examples
     tar zxvf Acropora_data.tar.gz
     cd ..
     python TREEasy.py -d examples/Acropora -s examples/Acro_spe_name.txt -g examples/Acro_gene_name.txt -b 50 -r Aten -n 3 -k 3 -t 8 -c CDS


# Input
  1-1. For CDS data type (-c cds):
   1-1-1. Nuclear_sequence_files in a directory, and each FASTA file contains nuclear sequences of all taxa (No missing data allowed). Moreover, each FASTA file must be named as *_nc.fasta.
    
    eg: CO1_nc.fasta
        >Taxon1
          ATCG
        >Taxon2
          ATCC
        ...
 
   1-1-2. Protein_sequence_files in the same directory, and each FASTA file contains protein amino acid sequences of all taxa (No missing data allowed). Moreover, each FASTA file must be named as *_aa.fasta.
    
    eg: CO1_aa.fasta
        > Taxon1
          PAPA
        > Taxon2
          PAPA
        ...


  1-2. For Non-CDS data type (-c noncds):
   	Nuclear_sequence_files in a directory, and each FASTA file contains molecular sequences of all taxa (No missing data allowed). Moreover, each of FASTA file must be named as *.fasta.

    eg: CO1.fasta
        >Taxon1
          ATCG
        >Taxon2
          ATCC
        ...
  
  1-3. Species-individual(s) information (-s). There are at least three columns separated by tab. The first column is a species name. The second column is the number of individuals for a species. The third, fourth and continued columns are individual names. 

    eg:
        Adif 1 Adif
        Aech 1 Aech
        Agem 2 Agem-1 Agem-2
        ...

  1-4. Gene - species name information (-g). There are two columns separated by tab. The first column is a species name. The second column is a gene name.

    eg:
        Adif    Adif_sc0000028.g769.t1
        Asub    Asub_sc0000129.g5077.t1
        Adif    Adif_sc0000104.g157.t1
        ...

  1-5. Other required inputs (-r/-n/-t/-k/-b) could see above Parameter section.

# Output

  1. aln_seqs: a directory including all alignment results and IQ-TREE outputs.
  2. ASTRAL: a directory including all required inputs for ASTRAL and outputs generated by ASTRAL.
  3. CONCAT: a directory including concatenated sequences and the species tree built by concatenated sequences with IQ-TREE.
  4. MP_EST: a directory including all required inputs for MP_EST and outputs generated by MP-EST.
  5. STELLS2: a directory including all required inputs for STELLS2 and outputs generated by ASTRAL.
  6. SNAQ: a directory including all required inputs for SNaQ and outputs generated by SNaQ.
  7. PHYLONET: a directory including all required inputs for PhyloNet and outputs by generated PhyloNet.
  8. 5 text files:
  
	  8-1: all_iqtree.contree. This file contains all gene trees generated by IQ-TREE.
    
	  8-2: all_iqtree_spename.contree. This file contains all gene trees generated by IQ-TREE, but gene names have been changed into species names.
    
	  8-3: all_iqtree_btstraped.txt. This file contains gene trees, of which nodes’ bootstrap values are greater than –b parameter.
    
	  8-4: all_iqtree_namechange_nonbranch.txt. This file contains gene trees, of which nodes’ bootstrap values are greater than –b parameter. Only gene tree topologies are represented.
    
	  8-5: all_iqtree_rooted.txt. This file contains gene trees, of which nodes’ bootstrap values are greater than –b parameter. And each gene tree has been rooted as required (-r).

# Visualization

 Dendroscope can be used to present species trees and networks.
  
# Citations
     1. XXXX
     2. Abascal, Federico, Rafael Zardoya, and Maximilian J. Telford. "TranslatorX: multiple alignment of nucleotide sequences guided by amino acid translations." Nucleic acids research 38.suppl_2 (2010): W7-W13.
     3. Katoh, Kazutaka, and Daron M. Standley. "MAFFT multiple sequence alignment software version 7: improvements in performance and usability." Molecular biology and evolution 30.4 (2013): 772-780.
     4. Bastide, P., Solis-Lemus, C., Kriebel, R., William Sparks, K., and Ané, C. (2018). Phylogenetic comparative methods on phylogenetic networks with reticulations. Systematic biology 67, 800-820.
     5. Borowiec, M.L. (2016). AMAS: a fast tool for alignment manipulation and computing of summary statistics. PeerJ 4, e1660.
     6. Nguyen, L.-T., Schmidt, H.A., von Haeseler, A., and Minh, B.Q. (2014). IQ-TREE: a fast and effective stochastic algorithm for estimating maximum-likelihood phylogenies. Molecular biology and evolution 32, 268-274.
     7. Pei, J., and Wu, Y. (2017). STELLS2: fast and accurate coalescent-based maximum likelihood inference of species trees from gene tree topologies. Bioinformatics 33, 1789-1797.
     8. Wen, D., Yu, Y., Zhu, J., and Nakhleh, L. (2018). Inferring phylogenetic networks using PhyloNet. Systematic biology 67, 735-740.
     9. Liu, L., Yu, L., and Edwards, S.V. (2010). A maximum pseudo-likelihood approach for estimating species trees under the coalescent model. Bmc Evol Biol 10, 302.
     10. Mirarab, S., Reaz, R., Bayzid, M.S., Zimmermann, T., Swenson, M.S., and Warnow, T. (2014). ASTRAL: genome-scale coalescent-based species tree estimation. Bioinformatics 30, i541-i548.
     

# Others
    The simulated data and emprical data are from below literatures:
      1. Mao, Y., Economo, E.P. and Satoh, N., 2018. The Roles of Introgression and Climate Change in the Rise to Dominance of Acropora Corals. Current Biology, 28(21), pp.3373-3382.
      2. Shen, X.-X., Opulente, D.A., Kominek, J., Zhou, X., Steenwyk, J.L., Buh, K.V., Haase, M.A.B., Wisecaver, J.H., Wang, M., and Doering, D.T. (2018). Tempo and Mode of Genome Evolution in the Budding Yeast Subphylum. Cell 175, 1533-1545. e1520.
      3. Solís-Lemus, C., Bastide, P. and Ané, C., 2017. PhyloNetworks: a package for phylogenetic networks. Molecular biology and evolution, 34(12), pp.3292-3298.

