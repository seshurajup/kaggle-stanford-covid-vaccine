## Models ##
* GRU
* LSTM
* CNN + GRU
* CNN + Bi-GRU
* CNN + Bi-GRU + attention layer
* Bert (already done in public kernels)
* Graph Neural Network (already done in public kernels)
* is possible transfer learning - [Tape](https://github.com/songlab-cal/tape)
* Local Graph based encoded features

## Custom loss ##
* msse already done and shared in kaggle

## Input ##
* K-words ( k = 1, 2, 3, 4, 5 )
* Build word2vec for k = 1, 2, 3, 4, 5
* Combinations of ( k= 1-2-3 combinations )
* Extra generated features
* different secondary structure genertated for same sequence using software annie

## Augmentation ##
* reverse sequence
* cutmix without losing pair () blocks i.e always move one block with other block

## Few Samples data
* Do soft labeling with test samples and train again with train and test together a final model
