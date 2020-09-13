* [Youtube: Understanding RNA folding energy dot-plots](https://www.youtube.com/watch?v=v1UbIUZ8k9o&ab_channel=TheW.C.RayLab)

* [RNA secondary structure prediction using an ensemble of two-dimensional deep neural networks and transfer learning](https://www.nature.com/articles/s41467-019-13395-9.pdf)
    * The majority of our human genome transcribes into noncoding RNAs with unknown structures and functions. Obtaining functional clues for noncoding RNAs requires accurate base-pairing or secondary-structure prediction. However, the performance of such predictions by current folding-based algorithms has been stagnated for more than a decade. Here, we propose the use of deep contextual learning for base-pair prediction including those noncanonical and non-nested (pseudoknot) base pairs stabilized by tertiary interactions. Since only <250 nonredundant, high-resolution RNA structures are available for model training, we utilize transfer learning from a model initially trained with a recent high-quality bpRNA dataset of >10,000 nonredundant RNAs made available through comparative analysis. The resulting method achieves large, statistically significant improvement in predicting all base pairs, noncanonical and non-nested base pairs in particular. The proposed method (SPOT-RNA), with a freely available server and standalone software, should be useful for improving RNA structure modeling, sequence alignment, and functional annotations.
    * https://www.kaggle.com/c/stanford-covid-vaccine/discussion/182303
    * https://dash.plotly.com/dash-bio/fornacontainer
    * in my previous competition on DNA, you will get better results to encode k-mers, rather than using single nucleotide
    e,g:
    single nucleotide : GACGACG --> 1,2,3,1,2,3,1
    k-mers: [GAC][GAC][G…] --> 47, 47, 56, …
* [Arnie Software](https://github.com/DasLab/arnie):
    * Python API to compute RNA energetics and do structure prediction across multiple secondary structure packages.
    * [Jupyter Notebook](https://github.com/DasLab/arnie/blob/master/notebooks/start_here.ipynb)

* [RNA secondary structure packages ranked and improved by highthroughput experiments](The computer-aided study and design of RNA molecules is increasingly prevalent across a
range of disciplines, yet little is known about the accuracy of commonly used structure
prediction packages in real-world tasks. Here, we evaluate the performance of current packages
using EternaBench, a dataset comprising 23 in vitro structure mapping and 11 riboswitch activity
datasets involving 18,509 synthetic sequences from the crowdsourced RNA design project
Eterna. We find that CONTRAfold and RNAsoft, packages with parameters derived through
statistical learning, achieve consistently higher accuracy than more widely used packages like
the ViennaRNA software, which derive parameters primarily from thermodynamic experiments.
Motivated by these results, we develop a multitask-learning-based model, EternaFold, which
demonstrates improved performance that generalizes to diverse external datasets, including
complete viral genomes probed in vivo and synthetic designs modeling mRNA vaccines.)

* [Theoretical basis for stabilizing messenger RNA through secondary structure design" - Hannah K. Wayment-Steele](https://www.biorxiv.org/content/10.1101/2020.08.22.262931v1)
    * RNA hydrolysis presents problems in manufacturing, long-term storage, world-wide delivery, and in vivo stability of messenger RNA (mRNA)-based vaccines and therapeutics. A largely unexplored strategy to reduce mRNA hydrolysis is to redesign RNAs to form double-stranded regions, which are protected from in-line cleavage and enzymatic degradation, while coding for the same proteins. The amount of stabilization that this strategy can deliver and the most effective algorithmic approach to achieve stabilization remain poorly understood. Motivated by the need for stabilized COVID-19 mRNA vaccines, we present simple calculations for estimating RNA stability against hydrolysis, and a model that links the average unpaired probability of an mRNA, or AUP, to its overall rate of hydrolysis. To characterize the stabilization achievable through structure design, we compare optimization of AUP by conventional mRNA design methods to results from the LinearDesign algorithm, a new Monte Carlo tree search algorithm called RiboTree, and crowdsourcing through the OpenVaccine challenge on the Eterna platform. Tests were carried out on mRNAs encoding nanoluciferase, green fluorescent protein, and COVID-19 mRNA vaccine candidates encoding SARS-CoV-2 epitopes, spike receptor binding domain, and full-length spike protein. We find that Eterna and RiboTree significantly lower AUP while maintaining a large diversity of sequence and structure features that correlate with translation, biophysical size, and immunogenicity. Our results suggest that increases in in vitro mRNA half-life by at least two-fold are immediately achievable and that further stability improvements may be enabled with thorough experimental characterization of RNA hydrolysis.

* [Capturing alternative secondary structures of RNA by decomposition of base-pairing probabilities" -Taichi Hagio](https://bmcbioinformatics.biomedcentral.com/track/pdf/10.1186/s12859-018-2018-4)
    * Background: It is known that functional RNAs often switch their functions by forming different secondary structures.
Popular tools for RNA secondary structures prediction, however, predict the single ‘best’ structures, and do not produce
alternative structures. There are bioinformatics tools to predict suboptimal structures, but it is difficult to detect which
alternative secondary structures are essential.
Results: We proposed a new computational method to detect essential alternative secondary structures from RNA
sequences by decomposing the base-pairing probability matrix. The decomposition is calculated by a newly
implemented software tool, RintW, which efficiently computes the base-pairing probability distributions over the
Hamming distance from arbitrary reference secondary structures. The proposed approach has been demonstrated on
ROSE element RNA thermometer sequence and Lysine RNA ribo-switch, showing that the proposed approach
captures conformational changes in secondary structures.
Conclusions: We have shown that alternative secondary structures are captured by decomposing base-paring
probabilities over Hamming distance. Source code is available from http://www.ncRNA.org/RintW.
Keywords: RNA secondary structure, Dynamic programming, Base-pairing probability, Partition function