Document Similarity from Vector Space Densities
Ilia Rushkin
Harvard University
Cambridge, USA
ilia_rushkin@harvard.edu
Abstract. We propose a computationally light method for estimating
similarities between text documents, which we call the density similarity (DS)
method. The method is based on a word embedding in a high-dimensional
Euclidean space and on kernel regression, and takes into account semantic
relations among words. We find that the accuracy of this method is virtually the
same as that of a state-of-the-art method, while the gain in speed is very
substantial. Additionally, we introduce generalized versions of the top-k
accuracy metric and of the Jaccard metric of agreement between similarity
models.
Keywords: document retrieval, text similarity, kernel regression, word
embedding.
1 Introduction
Estimating similarities among texts is essential for document retrieval, clustering and
recommendation systems. Taking into account semantic connections is an interesting
way of enhancing the similarity estimation, since it alleviates two interconnected
shortcomings of the simpler word-matching methods. One is the difficulty with
polysemy and semantics in natural languages, and the other is the near-orthogonality,
meaning that the number of matching features is low for most pairs of documents,
causing a large uncertainty in the match-based similarities [3]. To incorporate
semantic connections, the algorithm should have some kind of a “meaning-distance
map” among words. A popular method of doing this is word embedding, also known
as vectorization ([5], [7], [9]), where such a map is trained on the frequency of words
being near each other in the document corpus. This method achieves mapping words
(or, more generally, features such as n-grams) onto points in a Euclidean space in
such a way that the Euclidean distance between points represents semantic distance.
Word embeddings can now be trained relatively easily, and pre-trained ones are freely
available (e.g. [6]).
However, even when the word embedding exists, there remains a question of
getting from similarities between features (words) to similarities between documents.
At present, it appears that the existing methods for this task are either computationally
very heavy (e.g. the relaxed word-moving distance of RWMD, introduced by [8]
following [10]), or light but with a significantly lower accuracy (e.g. representing
each document by a single centroid point in the embedding space). In this work we

propose a method that appears to be both accurate and fast. We call it the density
similarity method, or DS for short, since it represents documents as probability
densities in the embedding space. On our example data, the DS method performed
very similarly to that of RWMD, while being orders of magnitude faster.
Furthermore, we think that the idea of the DS method is very natural and
straightforward mathematically, giving it interpretability.
The rest of this paper is organized as follows. In Section 2 we introduce and
discuss the DS method, with subsections 2.1 and 2.2 devoted to the questions of
bandwidth and sampling the space, respectively. In Section 3 we propose new
generalizations of accuracy metrics. In particular, they are used in Section 4, where
we apply the DS and the benchmark method to several datasets. Section 5 contains the
discussion and further thoughts.
2 Description of the Method
Word embedding, or vectorization, is a mapping of document features (informally
referred to as “words”) onto points in a 𝑑-dimensional Euclidean space ℝ𝑑, where 𝑑
is usually in the hundreds. Each document becomes a sequence of points, containing a
point multiple times if a word is used multiple times in a document. If we ignore the
word order, then the document is a set of distinct points with multiplicity weights
assigned to them, i.e. it is a distribution. More formally, the weights form a document-
feature matrix 𝑤 where the index 𝑡 =1,..𝑁 enumerates documents in the corpus
𝑡,𝑖 𝑑
and 𝑖 =1,..𝑁 enumerates the features. In the simplest case, the elements of this
𝑓
matrix can be the counts of features in documents, but it is common to subject it to
various transformations, such as normalizing rows to unit sum and applying the TF-
IDF transformation with the goal of lowering weights of those features that are
present in too many documents and therefore are not believed to be as informative as
the rare features. The word embedding maps 𝑖 →𝑥, where each 𝑥 is a 𝑑-dimensional
𝑖 𝑖
vector (the “feature-point”), and therefore a document 𝑡 is represented by a
distribution defined on the set of all feature-points in the corpus: 𝑓(𝑥)≡𝑤 .
𝑡 𝑖 𝑡,𝑖
The density similarity method that we propose here is to view the document
distributions as statistical sample densities and to estimate their distribution density
values on a small set of sample points {𝑧}. Transition from the full set of feature-
𝑗
points to the set {𝑧} involves distances in the embedding space, thus incorporating
𝑗
semantic connections into the method. We call it the “density similarity method”.
To estimate the densities, we can use kernel (or “non-parametric”) regression,
which is a well-developed field (see [4] or [12] for an introduction to it). Namely, let
us define the density of a document at an arbitrary point 𝑧∈ℝ𝑑 as a kernel
regression:
∑
𝑁𝑓
𝑘(
𝑧−𝑥
𝑖)𝑤
𝑖=1 ℎ 𝑡,𝑖
𝜌 (𝑧)= (1)
𝑡 ∑ 𝑁𝑓 𝑘( 𝑧−𝑥 𝑖)
𝑖=1 ℎ
Here 𝑘(𝑦) is the kernel and ℎ> 0 is the kernel bandwidth. The most commonly used
kernel is Gaussian: 𝑘(𝑦)=(2𝜋)−𝑑/2exp(−|𝑦|2/2). Another notable choice is the
radially-symmetric Epanechnikov kernel 𝑘(𝑦)=max(0,𝑑−|𝑦|2), based on [2],

where the 𝑑=1 version of this kernel was first studied and demonstrated to be the
asymptotically optimal.
We note that the denominator in Eq. 1 is just a normalization constant. For our
purposes normalization plays no role, so we could use only the numerator of Eq. 1.
Applying Eq. 1 at the 𝑛 sample points 𝑧, we obtain the density matrix of the
𝑗
corpus: 𝜌 ≡𝜌 (𝑧). Presuming that 𝑛 <𝑁 , this matrix can be seen as a condensed
𝑡,𝑗 𝑡 𝑗 𝑓
version of the document-feature matrix 𝑤 , transformed from the 𝑁 original features
𝑡,𝑖 𝑓
to 𝑛 new features. This transformation plays the role similar to latent semantic
indexing (LSI) or a topic model such as latent Dirichlet allocation (LDA). Like these
examples, the construction of the density matrix incorporates semantic relations
among features, since it uses distances in the Euclidean space.
Now the document-document similarity can be extracted as similarity among the
rows of the density matrix. Given the interpretation of each row of as a probability
distribution, it is conceptually appealing to use the Jensen-Shannon divergence [1],
but a simple cosine-similarity measure is a faster alternative.
In the above we were dealing with one corpus of documents. In document retrieval
and recommendation problems there are usuallytwo corpora, queries and items, and it
is the cross-corpus (query-item) similarity that needs to be found. The generalization
of the entire discussion is straightforward: the two matrices 𝑤(𝑞𝑢𝑒𝑟𝑖𝑒𝑠) and 𝑤(𝑖𝑡𝑒𝑚𝑠)
𝑡,𝑖 𝑡,𝑖
will be independently transformed into two densities 𝜌(𝑞𝑢𝑒𝑟𝑖𝑒𝑠) and 𝜌(𝑖𝑡𝑒𝑚𝑠), and
𝑡,𝑗 𝑡,𝑗
similarity will be computed between them.
Eq. 1 is readily generalizable in a variety of ways. For instance, we used a
spherically-symmetric kernel, but it is not a requirement. Generally speaking, instead
of a single bandwidth parameter ℎ one has a 𝑑×𝑑 bandwidth matrix 𝐻, in which
case the kernel arguments (𝑧−𝑥 )/ℎ in Eq. 1 are replaced by matrix products
𝑖
𝐻−1(𝑧−𝑥 ). However, this level of generality is often too complex, and a common
𝑖
intermediate approximation is to use a diagonal bandwidth matrix 𝐻=
diag(ℎ(1),…,ℎ(𝑑)), i.e. each Cartesian axis is served by its own bandwidth. Note,
however, that it makes 𝜌 dependent on the choice of the coordinate system in ℝ𝑑.
Let us briefly discuss the speed of the proposed DS method. If a document
contains, on average, 𝐹 unique features, creation of the density matrix has time
complexity of at most 𝑂(𝐹𝑁 𝑛), assuming straightforward calculation of sums in Eq.
𝑑
1 (although faster methods may exist). The cosine similarity among rows of this
matrix (size 𝑁 ×𝑛) has time complexity 𝑂(𝑁2𝑛). Hence, the time complexity of the
𝑑 𝑑
entire calculation is: 𝑂(𝐹𝑁 𝑛+𝑁2𝑛). By contrast, for the RWMD method the best-
𝑑 𝑑
case time complexity is 𝑂(𝑁2) for each document-document pair ([8]), therefore
𝑓
𝑂(𝑁2𝑁2) for the entire corpus. The dependence on the number of features (even
𝑓 𝑑
ignoring the fact that 𝐹 < 𝑁 ) is quadratic in RWMD and linear in DS, indicating that
𝑓
on large corpora DS must be significantly faster. In order to make the comparison
more direct, let us estimate that 𝐹 =𝑁 𝑁−𝑏. Evidently, 𝑏 may lie in the interval
𝑓 𝑑
between two extreme values: 0 (each document contains all the features of the corpus)
and 1 (no two documents have any features in common). With this, the time
complexities are: 𝑂(𝑁 𝑁1−𝑏𝑛+𝑁2𝑛) for DS, versus 𝑂(𝑁2𝑁2) for RWMD. Below,
𝑓 𝑑 𝑑 𝑓 𝑑
when we compare RWMD and the DS methods on example datasets, we will see that
this indeed translates into a very sizeable difference in speed. We chose RWMD as a

benchmark its authors, when introducing it, found it to compare favorably with many
other popular algorithms.
The DS method involves a number of meta-parameters:
1. The bandwidth ℎ (or, more generally, the bandwidth matrix 𝐻).
2. The number 𝑛 of the sample points.
3. The kernel shape 𝑘(𝑦).
4. The type of similarity measure to be applied to the density matrix rows.
In the last two, it is easy to settle on Gaussian kernel and cosine-similarity. These are
simple and standard, and the results are not expected to be too sensitive to them. The
bandwidth and the sample points, on the other hand, affect the outcome strongly, as is
well known for any kernel regression. In principle, the optimal bandwidth and sample
points should be found by training on a labeled training set. Such a training, however,
is costly, which makes it essential to look for quick estimates of these parameters
instead. In the next two sections we discuss our strategy for such estimates.
2.1 Choice of Bandwidth
Selection of the bandwidth ℎ in kernel regression like Eq. 1 lies at the heart of kernel
regression theory ([4], [12]). The methods fall into two broad categories:
computationally heavy methods that perform the optimization of bandwidth (i.e.
training), and computationally light “rules-of-thumb”. The classic example of the first
category is the least-squares cross-validation, which determines ℎ as the minimizer of
the following cost function:
𝑁
1 𝑥 −𝑥 2𝑁 𝑥 −𝑥 2𝑘(0)
𝑖 𝑗 𝑖 𝑗
𝐶(ℎ)= ∑ [𝐾( )− 𝑘( )]+ (2)
ℎ𝑑𝑁2 ℎ 𝑁−1 ℎ ℎ𝑑(𝑁−1)
𝑖,𝑗=1
Here 𝐾 is the convolution kernel: 𝐾(𝑦)=∫𝑘(𝑢)𝑘(𝑦−𝑢)𝑑𝑑𝑢. For the Gaussian
kernel 𝑘(𝑦)=(2𝜋)−𝑑/2exp(−|𝑦|2/2), it is a broader Gaussian: 𝐾(𝑦)=
(4𝜋)−𝑑/2exp(−|𝑦|2/4). In the more general case of a bandwidth matrix 𝐻, the ℎ𝑑 in
the denominators should be replaced with det𝐻, and the kernel arguments (𝑥 −
𝑖
𝑥 )/ℎ with 𝐻−1(𝑥 −𝑥 ).
𝑗 𝑖 𝑗
The Silverman rule [11] is an example from the “rule-of-thumb” category. It estimates
the bandwidth separately for each Cartesian axis in ℝ𝑑, i.e. gives a diagonal
bandwidth matrix, and a single bandwidth can be formed as the geometric mean of the
diagonal. Namely, if 𝜎(𝑎) is the standard deviation of the 𝑎-th components (𝑎=
1,..𝑑) of 𝑥,
𝑖
1 1/𝑑
4 𝑑+4 𝑑
ℎ(𝑎) =𝜎(𝑎) ( ) , ℎ =(∏ ℎ(𝑎)) (3)
𝑆 𝑁(𝑑+2) 𝑆 𝑆
𝑎=1
Another option is to take the average spacing between the feature points. To estimate
the volume populated by the 𝑥, we circumscribe a 𝑑-dimensional sphere of radius 𝑅
𝑖
centered at origin. The log-volume of a ball of radius 𝑅 is

𝜋𝑑/2
log𝑣(𝑅)=log +𝑑log𝑅, (4)
Γ(1+𝑑/2)
We may also cut out a smaller unpopulated ball of radius 𝑟<𝑅, so the remaining
volume is a spherical layer in which 𝑥 lie. The log-volume of the described spherical
𝑖
layer is
log𝑉(𝑟,𝑅)=log𝑣(𝑅)+log(1−𝑒log𝑣(𝑟)−log𝑣(𝑅)) (5)
In fact, the second logarithm is only a small correction unless 𝑟 is close to 𝑅: in a
high-dimensional ball, the volume is highly concentrated near the surface. But we
keep it here for generality. The bandwidth is then estimated as the typical spacing that
the data points would have if they were distributed in that volume uniformly:
ℎ =𝑒(log𝑉(𝑟,𝑅)−log𝑁)/𝑑 (6)
𝑉
The straightforward choices for 𝑟 and 𝑅 are the minimum and the maximum of |𝑥 |.
𝑖
However, to avoid making ℎ sensitive to outliers, we selected 𝑟 and 𝑅 as the 0.1 and
𝑉
0.9 quantiles of |𝑥 |.
𝑖
On our data, the volume method of Eq. 6 gave the best results. The Silverman rule
gave somewhat smaller bandwidth and led to lower accuracy. The minimization of
Eq. 2 was not only computationally heavy, but also produced much smaller
bandwidth values, leading to the worst accuracy of all. For this reason, we suggest
using Eq. 6 for bandwidth estimation. If labeled training data is available, one can
also try to adjust the estimated bandwidth by a multiplicative factor.
2.2 Sampling the Space
For a high 𝑑 (a typical value in word embeddings is 300), creating a regular grid of
sample points is not practical due to the “curse of dimensionality”: a single cube in
ℝ𝑑 has 2𝑑 vertices. The regularity of the sampling array is not required, however. We
just need to sample the space sufficiently for measuring distribution differences,
wherever they may occur. One solution is to generate any desired number 𝑛 of sample
points randomly, from a distribution that is uniform in a ball of radius 𝑅. It is
essentially the same concept as was considered in the previous section for bandwidth
estimation. Logically, one should take a spherical layer 𝑉(𝑟,𝑅) rather than a ball, but,
as we saw, the difference is negligible unless 𝑟 is very close to 𝑅.
As in the previous section, we select 𝑅 as a high quantile of the norms |𝑥 | (we
𝑖
used quantile 0.95), rather than max|𝑥 |, due to the possibility of outliers. The way to
𝑖
generate 𝑛 uniform random points 𝑧 in a 𝑑-dimensional ball of radius 𝑅 is as follows.
𝑗
We first generate 𝑛 points 𝑍 from a 𝑑-variate standard normal distribution (in
𝑗
Cartesian components, it means generating a 𝑑×𝑛 matrix of independent standard
normal variables). Then, each point is normalized: 𝑧 =𝑍 𝑢1/𝑑𝑅/|𝑍|, where 𝑢 are 𝑛
𝑗 𝑗 𝑗 𝑗 𝑗
numbers independently drawn from the standard uniform distribution on the [0,1]
interval.

There is no simple way to choose 𝑛 optimally. Given the uniform distribution of 𝑧,
𝑗
there is no expectation of results deteriorating if 𝑛 is too high. Rather, the
approximation is always expected to improve with higher 𝑛, but at an ever-decreasing
rate. This situation of “diminishing returns” makes the choice of 𝑛 similar to that of
the number of trees in a random forest algorithm, rather than to the number of
components in LSI or the number of topics in LDA. At the same time, since sampling
involves randomness, a small 𝑛 increases the probability of fluctuations in the
similarity results. It is even possible for a lower 𝑛 to give higher accuracy, but not
consistently. In our application of the method we tried several values of 𝑛 ranging
from 100 and to 10,000.
3 Performance Metrics
On labeled data we can compare the accuracies of the DS method and a benchmark
method, and on a non-labeled one we can measure the agreement between them.
While standard metrics for accuracy and agreement exist, it seemed useful to us to
introduce versions of them that are modified with a “softness” parameter 𝑠, and
present the results for several values of 𝑠. Of course, we include 𝑠 =0, at which the
modification disappears. The remainder of this section describes these metrics.
The output of a document-similarity method can be described by a distance matrix
𝑀 , where the row-index 𝑡′ enumerates documents in the corpus of queries and the
𝑡′,𝑡
column-index 𝑡 – those in the corpus of items. Without loss of generality, we can
consider only one query, treating 𝑡′ as a spectator index. Furthermore, the actual
values of distance (equivalently, of similarity) are not important, only their ranks are,
because they determine which items, and in what order are returned for a query.
Therefore, we consider the vector 𝑟 of ranks of the values in a row of 𝑀.
𝑡
An accuracy metric should give more weight to lower ranks: the top-k items are
important, but we don’t care much in what order it places the almost-irrelevant items
in the long tail of high ranks. A standard method is to take only items with rank not
higher than a threshold 𝑘. More generally, even within these items, we can weigh
lower ranks higher. Given a labeled data set, we take the 𝑘 items with the lowest rank,
ordered by that rank. The label-correctness values form a 0-or-1 (boolean) vector 𝑐 ,
𝑘′
𝑘′=1,..𝑘, with which we define the soft top-𝑘 accuracy:
∑𝑘 𝑐 𝑤 1
𝐴(𝑘,𝑠)=
𝑘′=1 𝑘′ 𝑘′
, 𝑤 = (7)
∑𝑘 𝑤 𝑘′ 𝑘′𝑠
𝑘′=1 𝑘′
Here 𝑠≥0 is the softness parameter. The values of 𝐴(𝑘,𝑠) lie in the [0,1] interval. At
𝑠=0 the metric reduces to the usual top-k average correctness.
Another metric of performance is needed to measure the agreement between two
models which produce two ranking vectors, 𝑟(𝐴) and 𝑟(𝐵). Choosing a rank threshold
𝑡 𝑡
𝑘, we can measure the agreement as a Jaccard similarity between the items assigned
rank ≤𝑘 in the two models:
𝑈(𝐴)(𝑘)={𝑡:𝑟(𝐴) ≤𝑘}, 𝑈(𝐵)(𝑘)={𝑡:𝑟(𝐴) ≤𝑘}, 𝑈(𝑘)=𝑈(𝐴)(𝑘)∪𝑈(𝐵)(𝑘),
𝑡 𝑡
with which the Jaccard similarity index is

|𝑈(𝐴)(𝑘)∩𝑈(𝐵)(𝑘)|
|     |     |     |     | (8)  |
| --- | --- | --- | --- | ---- |
𝐽(𝑘)=
|𝑈(𝑘)|
This metric has a sharp cutoff: if a model ranked an item beyond 𝑘, it is penalized
regardless of how far beyond 𝑘 it ranked the item. We want to generalize it to make
|     |     |     | 1 min(1,(𝑟(𝐴)/ |     |
| --- | --- | --- | -------------- | --- |
the penalty depend on the rank. Observe that the quantity  ∑ 𝑡∈𝑈(𝑘)
|     |     |     | |𝑈(𝑘)| | 𝑡   |
| --- | --- | --- | ------ | --- |
𝑘) −1/𝑠 ) penalizes the model 𝐴 in just that way (here 𝑠≥0). Taking, for symmetry,
the sum of that quantity and its counterpart from model 𝐵, and subtracting 1, we
obtain the soft Jaccard index:
−1/𝑠
|     | 1   |     | 𝑟(𝐴) |     |
| --- | --- | --- | ---- | --- |
[min(1,(𝑡
| 𝐽(𝑘,𝑠)=−1+ |        | ∑   | ) )+[𝐴→𝐵]]  | (9)  |
| ---------- | ------ | --- | ----------- | ---- |
|            | |𝑈(𝑘)| |     | 𝑘           |      |
𝑡∈𝑈(𝑘)
By the meaning of 𝑈, at least one of the two terms in the summand is always 1, so
𝐽(𝑘,𝑠) takes values between 0 and 1, and the upper bound is achieved if and only if
the two models completely agree on which items they rank within 𝑘. At 𝑠=0, the
metric reduces to the standard Jaccard measure of Eq. 8:
| |𝑈(1)(𝑘)|+|𝑈(2)(𝑘)| |        |      | |𝑈(𝑘)|+|𝑈(1)(𝑘)∩𝑈(2)(𝑘)| |        |
| ------------------- | ------ | ---- | ------------------------ | ------ |
| 𝐽(𝑘,0)=−1+          |        | =−1+ |                          | =𝐽(𝑘)  |
|                     | |𝑈(𝑘)| |      | |𝑈(𝑘)|                   |        |
We note in passing that our choice of a power-law dependence was made for
simplicity, but one could also generalize 𝐴 and 𝐽 using, e.g., an exponential decay.
Recalling now the query-index 𝑡′, the quantities of Eq. 7 and Eq. 9 can be
computed for every query: 𝐴 (𝑘,𝑠),  𝐽 (𝑘,𝑠), and then their distribution over 𝑡′ can
|     | 𝑡′  | 𝑡′  |     |     |
| --- | --- | --- | --- | --- |
be examined.
4  Experiment
Our data set consisted of texts scraped from personal webpages of faculty members
and researchers in Harvard University (dataset “People”), the descriptions of events,
talks, seminars and public lectures (dataset “Events”), and the news articles recently
published  at the same institution (dataset “News”). All texts were cleaned and
tokenized on the basis of single lemmatized words, dropping stopwords and words
shorter than 4 characters. The tokens were then used as features in word embedding.
A subset of the dataset “People” was labeled by people’s affiliation with Harvard
departments (number of classes: 60; class sizes: 10-479, with mean 58 and median
33). Some descriptive statistics of the data are given in Table 1.
Table 1. Descriptive statistics of the data.
| Dataset           | # documents  | Max # tokens/document  | Mean # tokens/document  |     |
| ----------------- | ------------ | ---------------------- | ----------------------- | --- |
| “People”          | 11,863       | 66,258                 | 1,030                   |     |
| “People” labeled  | 3,495        | 55,565                 | 1,696                   |     |
| “Events”          | 5,177        | 535                    | 30                      |     |
| “News”            | 5,118        | 2,115                  | 146                     |     |

The “People” dataset always plays the role of the “queries” corpus, and the role of the
“items” corpus can be played by any of the three datasets (when the same dataset
“People” is used as “queries” and as “items”, we remove self-recommendations).
We used the same word2vec embedding for all methods, pre-trained on a corpus of
Wikipedia articles, with dimensionality 𝑑 =300 ([6]). The tokens that are absent in
our corpora were dropped from the embedding, leaving 138,030 tokens.
We computed the query-item similarity matrices using the RWMD method and
using the DS method with several different numbers of sample points. As was
mentioned earlier, the RWMD model for document similarity was shown by its
authors to compare favorably with a number of other algorithms, which is why we
confine ourselves to using it as a benchmark. All calculations were done on the same
machine (2.4 GHz processor and 16 GB memory), in an R environment. For RWMD,
we used the implementation of this method in the R package text2vec, with Euclidean
distance. Creation of the density matrices was done with a custom R script, and the
subsequent calculation of the similarity matrices was done using the R package
quanteda.
In the DS method, the kernel was Gaussian, and the bandwidth was determined by
Eq. 6, with several adjustment factors tried from 0.25 to 64, in powers of 2. We first
used the dataset “People” as both queries and items (recommendation of people to
other people), and looked at the top-5 accuracy on the labeled subset of this dataset.
As Fig. 1 illustrates, the accuracy of RWMD is only slightly higher than that of
density similarity with 500 or more points. For 1,000 and 10,000 points the difference
from RWMD is statistically insignificant (𝑝>0.1).
Fig. 1. Top-5 accuracy comparison among RWMD and several versions of density similarity
method, differing by the number of sample points. Bandwidth is ℎ from Eq. 6. The vertical
𝑉
axis is the accuracy measure of Eq. 7, averaged across queries. The horizontal axis is the
softness parameter. The error-bars show 3 standard errors.
Larger rank-cutoffs demonstrate a similar picture: top-10 accuracy values are
consistently lower than the top-5 values, but the difference between RWMD and DS

with 1,000 or 10,000 points not exceeding 0.02.At the same time, the difference in
computation speed was large: the RWMD calculation took over 100 hours, whereas
the density similarity with 1,000 points took less than 11 minutes (more precisely, 654
sec., consisting of 392 sec. on density estimation and 262 sec. on the similarity
matrix), and the calculation with 500 points took about 5 minutes (175 sec. on density
estimation and 124 sec. on the similarity matrix).1
We also calculated the recommendations of news and events to people, where the
dataset “People” serves as queries and is paired either with “Events” or “News” as
items. The RWMD method for both recommendations together took about 60,000 sec.
(about 16,000 sec. for “News” and 45,000 sec. for “Events”). By comparison, the
density similarity method with 1,000 sample points took about 930 seconds for the
same task, and with 500 sample points – under 600 sec.
We can measure the agreement with RWMD on unlabeled datasets using the soft
Jaccard index of Eq. 9, and the results are shown in Fig. 3. They show a strong overall
correlation between the model outcomes (this gives no indication which model gives
a better recommendation when they do not agree).
As a minimal form of training the model, we repeated the calculation using
adjusted bandwidth: multiplying the Eq. 6 by several simple factors. This exploration
showed that ℎ is close to the optimum. Significant deviations from it lead to a
𝑉
decrease either in accuracy, or in the Jaccard index of agreement with RWMD, or in
both. For instance, Fig. 2 shows the accuracy at a halved bandwidth which is lower
than in Fig 1.
Fig. 2. Accuracy comparison among RWMD and several versions of density similarity method,
differing by the number of sample points. Bandwidth is adjusted by a factor 0.5. The vertical
axis is the accuracy measure of Eq. 7, averaged across queries. The horizontal axis is the
softness parameter. The error-bars show 3 standard errors.
1 In this case, queries and items are represented by the same corpus, so only one density matrix
is needed.

5 Discussion and further work
The density similarity (DS) method, which we propose here, estimates document
similarities – a crucial task for document retrieval and clustering.
The speed of the DS method strongly depends on the number of sample points. We
found that a sample of 500 or 1,000 points is sufficient: increasing it further produces
only a small additional improvement. Even with 10,000 sample points, the DS method
is much faster than RWMD, while its top-k accuracy turns out essentially the same.
We believe that the gain in speed compensates well for the slight difference in
accuracy, even if it turns out that that difference is systematic. Elsewhere, RWMD has
been shown to be more accurate than a number of other popular methods ([8]), and by
amounts that are significantly larger than the difference that we observe here.
Our application of the DS method relies on direct estimates of meta-parameters
(bandwidth, sampling the space). In this form, it is an unsupervised machine learning
algorithm. However, if a labeled dataset is available, it is straightforward to
incorporate some training into the method, as we did with the bandwidth adjustment
coefficient. We found the bandwidth is the single most important parameter of the
method – as is typical in non-parametric regressions.
The DS method is essentially a kernel regression in the embedding space. In our
view, it is a very straightforward idea, making the results easier to interpret and the
method – easier to develop further. Moreover, the corpus density matrix, computed as
a step of the method, is an interesting condensed version of the document-feature
matrix, and can be used as such for purposes other than finding document similarity,
e.g. clustering, or visual representations of document corpora.
In the future, we hope to pursue several possible directions of further research:
generalization of document features from single words to n-grams; sensitivity to
transformations of the document-feature matrices (in this work we used a standard
TF-IDF transformation); possibility of combining this method with others in a multi-
step fashion.
6 Acknowledgments
The author is grateful for the support from the Office of the Vice Provost for
Advances in Learning at Harvard University.

Fig. 3. Agreement of two versions of density similarity methods (differing in the number of
sample points) with RWMD in three recommendation problems: recommending people to
people, events to people, and news to people. The vertical axis is the generalized Jaccard
measure of Eq. 9. The colors represent three values of the softness parameter. The box plots
show the quartiles of the distribution of this quantity across all queries, and the added diamond
shapes show the mean values ± one standard deviation.

References
1. Briët, J. and Harremoës, P.: Properties of classical and quantum Jensen-Shannon
divergence. Physical review A, 79(5), p.052311 (2009).
2. Epanechnikov, V.A.: Non-parametric estimation of a multivariate probability density.
Theory of Probability & Its Applications, 14(1), 153-158 (1969).
3. Greene, D. and Cunningham, P.: Practical solutions to the problem of diagonal dominance
in kernel document clustering. In: Proceedings of the 23rd international conference on
Machine learning, pp. 377-384. ACM, New York (2006).
4. Hansen, B.E.: Lecture Notes on Nonparametrics. Lecture notes (2009).
https://www.ssc.wisc.edu/~bhansen/718/NonParametrics1.pdf, last accessed 2020/01/14.
5. Mikolov, T., Chen, K., Corrado, G. and Dean, J.: Efficient estimation of word
representations in vector space. arXiv preprint arXiv:1301.3781 (2013).
6. Mikolov, T., Grave, E., Bojanowski, P., Puhrsch, C. and Joulin, A.: Advances in pre-
training distributed word representations. arXiv preprint arXiv:1712.09405 (2017).
7. Mikolov, W. Yih, and Zweig, G.: Distributed representations of words andphrases and
their compositionality. In: Proc. of theConference on Neural Information Processing
Systems. Lake Tahoe, NV (2013).
8. Kusner, M., Sun, Y., Kolkin, N. and Weinberger, K.: From word embeddings to document
distances. In: International conference on machine learning, pp. 957-966. JMLR, Lille
(2015).
9. Pennington J., Socher, R., Manning, C. D.: GloVe: Global vectors for word representation.
In: Proc. of the Conference on Empirical Methods on Natural Language Processing. ACL,
Doha, Qatar (2014).
10. Rubner, Y., Tomasi, C., and Guibas, L. J.: A metric for distributions with applications to
image databases. In: Sixth International Conference on Computer Vision, pp. 59–66.
IEEE, Bombay (1998).
11. Silverman, B. W.: Density estimation for statistics and data analysis. Monographs on
Statistics and Applied Probability. Chapman and Hall, London (1986).
12. Tsybakov, A. B.: Introduction to Nonparametric Estimation. Springer-Verlag, New York
(2009).