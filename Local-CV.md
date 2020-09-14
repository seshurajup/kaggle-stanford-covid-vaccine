In this competition, you will be **predicting the degradation rates at various locations along RNA sequence**.

There are multiple ground truth values provided in the training data. While the submission format requires all 5 to be predicted, only the following are **scored: reactivity, deg_Mg_pH10, and deg_Mg_50C**.

**Files**
* train.json - the training data
* test.json - the test set, without any columns associated with the ground truth.
* sample_submission.csv - a sample submission file in the correct format

**Columns**
* **id** - An arbitrary identifier for each sample.
**seq_scored** - **(68 in Train and Public Test, 91 in Private Test)** Integer value denoting the number of positions used in scoring with predicted values. This should match the length of reactivity, deg_* and *_error_* columns. Note that molecules used for the Private Test will be longer than those in the Train and Public Test data, so **the size of this vector will be different**.
* **seq_length** - **(107 in Train and Public Test, 130 in Private Test)** Integer values, denotes the length of sequence. Note that molecules used for the Private Test will be longer than those in the Train and Public Test data, so the size of this vector will be different.
* **sequence** - **(1x107 string in Train and Public Test, 130 in Private Test)** Describes the RNA sequence, a combination of A, G, U, and C for each sample. Should be 107 characters long, and **the first 68 bases should correspond to the 68 positions specified in seq_scored (note: indexed starting at 0)**.
* **structure** - **(107 string in Train and Public Test, 130 in Private Test) An array of (, ), and . characters** that describe whether a **base is estimated to be paired or unpaired**. Paired bases are denoted by opening and closing parentheses e.g. (....) means that base 0 is paired to base 5, and bases 1-4 are unpaired.
* **reactivity** - (1x68 vector in Train and Public Test, 1x91 in Private Test) An array of floating point numbers, should have the same length as seq_scored. These numbers are reactivity values for the first 68 bases as denoted in sequence, and used to determine **the likely secondary structure of the RNA sample**.
* **deg_pH10** - (1x68 vector in Train and Public Test, 1x91 in Private Test) An array of floating point numbers, should have the same length as seq_scored. These numbers are reactivity values for the first 68 bases as denoted in sequence, and used to determine **the likelihood of degradation at the base/linkage after incubating without magnesium at high pH (pH 10)**.
* **deg_Mg_pH10** - (1x68 vector in Train and Public Test, 1x91 in Private Test) An array of floating point numbers, should have the same length as seq_scored. These numbers are reactivity values for the first 68 bases as denoted in sequence, and used to determine **the likelihood of degradation at the base/linkage after incubating with magnesium in high pH (pH 10)**.
* **deg_50C** - (1x68 vector in Train and Public Test, 1x91 in Private Test) An array of floating point numbers, should have the same length as seq_scored. These numbers are reactivity values for the first 68 bases as denoted in sequence, and used to determine **the likelihood of degradation at the base/linkage after incubating without magnesium at high temperature (50 degrees Celsius)**.
* **deg_Mg_50C** - (1x68 vector in Train and Public Test, 1x91 in Private Test) An array of floating point numbers, should have the same length as seq_scored. These numbers are reactivity values for the first 68 bases as denoted in sequence, and used to determine **the likelihood of degradation at the base/linkage after incubating with magnesium at high temperature (50 degrees Celsius)**.
* ***_error_*** - An array of floating point numbers, should have the same length as the corresponding reactivity or deg_* columns, calculated **errors in experimental values obtained in reactivity and deg_* columns**.
* **predicted_loop_type** - (107 string) Describes the **structural context (also referred to as 'loop type')of each character in sequence**. Loop types assigned by **bpRNA from Vienna RNAfold 2 structure. From the bpRNA_documentation: S: paired "Stem" M: Multiloop I: Internal loop B: Bulge H: Hairpin loop E: dangling End X: eXternal loop**

**Additional Notes**

At the beginning of the competition, Stanford scientists have data on **3029 RNA sequences of length 107**. For technical reasons, measurements cannot be carried out on the final bases of these RNA sequences, so we have **experimental data (ground truth) in 5 conditions for the first 68 bases**.

We have **split out 629 of these 3029 sequences** for a **public test set** to allow for continuous evaluation through the competition, on the public leaderboard. These sequences, in **test.json(public 629, private 3029)**, have been additionally filtered based on three criteria detailed below to ensure that this subset is not dominated by any large cluster of RNA molecules with poor data, which might bias the public leaderboard. **The remaining 2400 sequences for which we have data are in train.json**.

For our final and most important scoring **(the Private Leaderbooard)**, Stanford scientists are carrying out measurements on **3005 new RNAs**, which have somewhat **longer lengths of 130 bases. For these data, we expect to have measurements for the first 91 bases, again missing the ends of the RNA**. These sequences constitute another 3005 of the 3634 sequences in test.json.

For those interested in how the **629 107-base sequences in test.json** were filtered, here were the steps to ensure a diverse and high quality test set for public leaderboard scoring:

1. **Minimum value across all 5 conditions must be greater than -0.5**.
2. **Mean signal/noise across all 5 conditions must be greater than 1.0. [Signal/noise is defined as mean( measurement value over 68 nts )/mean( statistical error in measurement value over 68 nts)]**
3. To help ensure sequence diversity, **the resulting sequences were clustered into clusters with less than 50% sequence similarity**, and **the 629 test set sequences were chosen from clusters with 3 or fewer members. That is, any sequence in the test set should be sequence similar to at most 2 other sequences**.


**Note that these filters have not been applied to the 2400 RNAs in the public training data train.json**
    * **Some of those measurements have negative values or poor signal-to-noise, or some RNA sequences have near-identical sequences in that set. But we are providing all those data in case competitors can squeeze out more signal**.

**The three filters noted above will also not be applied to Private Test on 3005 sequences**.

---
**Public Rows / (Public Rows + Private Rows + Ignored Rows)**

* Public rows = 629*68
* Private rows = 3005*91
* Ignored rows = 629 * (107-68) + 3005*(130-91)
* 9% = 42772 / (42772 + 273455 + 141726)

* The training data has sequences of lengths 107 (68)
* The test data has sequences of lengths 107 and 130 (68, 91)
* The public LB has sequences of lengths 107 (68)
* The private LB has sequences of lengths 130 (91)

**Conclusions**

* No Hidden private set.
* Public vs Private data set stagery is shared.
* Based on 3 rules, build local cv also as - 9% rows logic as per public cv above rule and 91% rows as private cv.
* Build model to improve 0.09 x public_local_cv + 0.91 x private_local_cv.
* Apply Stratified KFold on public_local_cv and private_local_cv.
* Public LB score based on all 68 sequences only, then 91 sequence in private.