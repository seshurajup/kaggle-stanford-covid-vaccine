* Don't miss @hengck23 all discussionss

* base model is [Notebook from hengck23](https://www.kaggle.com/xhlulu/openvaccine-simple-gru-model)
use one hot encoding for in put (to better visualized the first covn filter for interpret-ability)
GRU only (LB 0.27072)
added a 1d CNN embedding before GRU (LB 0.26990)
add a new seq for bbp, see below(LB 0.26356 )
train samples = signal ration>1
fold 5 ensemble average

* in my previous competition on DNA, you will get better results to encode k-mers, rather than using single nucleotide
e,g:
single nucleotide : GACGACG --> 1,2,3,1,2,3,1
k-mers: [GAC][GAC][G…] --> 47, 47, 56, …

* as alternative, i am trying now:
    rna_dict    = {x:i for i, x in enumerate('ACGU')} #4
    struct_dict = {x:i for i, x in enumerate('().')}  #3
    loop_dict   = {x:i for i, x in enumerate('BEHIMSX')}#7
    vobcab size = 437

    i was wondering if a 107*107 attention map in BERT model will work too?
    https://bair.berkeley.edu/blog/2019/11/04/proteins/
    https://blog.einstein.ai/provis/

    alternatively, graph convolution net, GCN. Note the relation

    out = GCN(node,adjency_matrix) where adjency_matrix is basically a fixed attention map.
    out = Transformer(node) , self learn attention map

* I think transformer models pre-trained on RNA sequences would be very interesting, since RNA sequences are widely available and can be easily processed to perform self-supervision in the same way as documents.

* https://www.biorxiv.org/content/10.1101/676825v1.full.pdf

* Great question. The bpps are numpy arrays we pre-calculated for each sequence. hidehisaarai1213 is right; they're matrices of base pair probabilities, calculated using a recently developed algorithm in our lab.
What you use them for is totally up to you. Biophysically speaking, this matrix gives the probability that each pair of nucleotides in the RNA forms a base pair (given a particular model of RNA folding). You've probably already seen the structural features: imagine that this matrix describes the whole distribution from which one could sample more structures.
At the simplest level -- it's a symmetric square matrix with the same length as the sequence, so you can get N more features out of it, if you want them. Each column and each row should sum to one (up to rounding error), but more than one entry in each column/row will be nonzero -- usually somewhere between 1-5 entries.
Feel free to use them or ignore them based on your own judgement; we pre-generated them because it would take a little specialized knowledge to do so, as well as a little time (a bit under a second for each sequence). At the same time, feel free to generate and share other biophysically inspired features of your own, if you suspect they might be helpful!

* https://medium.com/eternaproject/how-to-build-a-better-vaccine-from-the-comfort-of-your-own-web-browser-233343e0210d
