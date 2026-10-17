BIRCH: An Efficient Data Clustering Method for Very Large
Databases
Tian Zhang Raghu Ramakrishnan Miron Livny”
(“lornputer Sciences Dept. Computer Sciences Dept. Computer Sciences Dept.
[Jniv. of Wisconsin-Maciison [Jniv. of Wisconsin-Maciison LJniv. of Wisconsin-Maclison
zhang@cs. wise.edu raghuf~cs.wise.edu mironf~cs. wise.eclu
Abstract Generally, there are two types of attributes involved
Finding useful patterns in large datasets has attracted in the data to be clustered: metrtc and nonmetrzri. ln
considerable interest recently, and one of the most widely this paper, we consider metric attributes, as in most,
st,udied problems in this area is the identification of clusters, of the Statistics literature, where the clustering prol>-
or deusel y populated regions, in amulti-dir nensional clataset. lern is formalized as follows: G’tven the destred rlum-
Prior work does not adequately address the problem of large ber of clusters K and a dataset of N potnts, and a
datasets and minimization of 1/0 costs. dzstance-based measurement functzon (e.g., the uletghted
This paper presents a data clustering method named totrd/average dwtunce betuleeri pazr-s of pozrtts tn clus-
Bfll (;”H (Balanced Iterative Reducing and Clustering using
ters), rue are asked to find a partatzon of the dataset that
Hierarchies), and demonstrates that it is especially suitable
rrl~nrmizes the value of thf measurement functton. This
for very large databases. BIRCH incrementally and clynami-
is a nonconvm dtscrete [KR90] optimization problem.
cally clusters incoming multi-dimensional metric data points
Due to an abundance of local minima, there is typically
to try to produce the best quality clustering with the avail-
able resources (i.e., available memory and time constraints). no way to find a global minimal solution without trying
BIRCH can typically find agoocl clustering with asingle scan all possible partitions.
of the data, and improve the quality further with a few acl- We adopt, the problem definition used in Statistics,
ditioual scans. BIRCH is also the first clustering algorithm but with an additional, database-oriented constraint,:
proposerl in the database area to handle “noise)’ (data points The amount of memory available M ltrntted (t~yptcall~y,
that are not part of the underlying pattern) effectively.
much -smaller than the data set .sw~) and ule rvant to
We evaluate BIRCH’S time/space efficiency, data input
rninzmt.ze the tzrne required for 1/0. A related point, is
order sensitivity, and clustering quality through several
that it is desirable to Lre able to take into account the
experiments. We also present a performance comparisons
amount of ttmethat a user is willing to wait for the
of BIR (;’H versus CLARA NS, a clustering method proposed
results of the clustering algorithm.
recently for large datasets, and S11OWthat BIRCH is
consistently superior. We present a clustering method named BIRCH and
demonstrate that it is especially suitable for very large
1 Introduction
databases. Its 1/(> cost is linear in the size of the
In this paper, we examine dataclustering, which is
dataset: a .szngle scan of the dataset yields a good
a particular kind of clatla mining problem. (~iven a
clustering, ancl one or more additional passes can
large set of rnulti-clirnensional data points, the data
(optionally) be used to improve the quality further.
spare is usually not uniformly occupied. Data clustering
By evaluating BIRCH’S time/space eficieucy, data ill-
identifies the sparse and the crowded places, and
put order sensitivity, and clustering quality, and com-
hence discovers the overall distribution patterns of
paring with other existing algorithms through experi-
the dataset. Besides, the derived clusters can be
ments, we argue that BIRCH is the best available clus-
visualized more efficiently and effectively than the
tering method for very large databases. BIRCIPs ar-
original dataset[Lee81, D,J80].
chitecture also offers opportunities for parallelism, and
*This research has been supported by NSF Grant IRI-9057562 for interactive or dynamic performance tuning based on
and NASA (;rant 144-EC 78. knowledge about the ciataset, gained over the course of
Permission tomake digitalhard copy of part orall ofthis work for personal the execution. Finally, BIRCH is the first clustering al-
orclassroom use is ranted without fee provided that copies are not made
or distributed for pro7ttor commercial advantage, the aopyright notice, the
title ofthe publication and itsdate appear, and notice isgiven that 1Informally, a metmc attribute is an attribote whose values
copying isbypermission ofACM, Inc. To copy otherwise, to republish, to satisfy the requirements of Eucltdtan space, i.e., self identity (for
post onservers, orto redistribute tolists, requires prior specific permission any X, X = X) and triangular inequality (there exists a distance
andlor afee. definition such that for any XI ,XZ,X3, d(XI ,X2) + d(X2, X3) ~
[1(X1,X3)).
SIGMOD ’966/96 Montreal, Canada
IQ 1996 ACM 0-89791-794-4/96/0006 ...$3.50
103

goritlhm proposed in the datlahase area that addresses glol]al measurements, which require scanning all data
outl~~rs (intuitively, data points that, should be regarded points or all currently existing clusters. Hence none of
a,s “noispi’ ) and proposes a plausible solution. them have linear time scalability with stal)le quality,
1.1 Outline of Paper For example, using exhausttvt eTmnltratzort (EE),
The rest of the paper is organized as follows. Sec. 2 there are approximately IiN/I< ! [DH73] ways of par-
surveys relat,ed work ancl summarizes BIRCH’S contri- titioning a set of N data points into K subsets. So in
l)utlunh Sec. 3 presents some background material. practice, though it can find the global minimum, it is
Ser. 4 introduces the concepts of clustering feature ((~F) infeasible except, when IV and K are extremely small.
au(i (~F tree, which are central to BIRCH. The details Iterattve optzmwatzon (10) [DH73, KR90] starts with
of BIll(’H algorithm is described in Sec. 5, and a pre- an initial partition, then tries all possible moving or
liminary performance study of BIRCH is presented in swapping of data points from one group to another to
Sec. 6, Finally our conclusions and directions for fw see if such a moving or swapping improves the value of
ture rmearch are presented in Sec. 7, the measurement function, It can find a local minimum,
hut, the c!uality of the local minimum is vpry sensitivp to
2 Summary of Relevant Research
the initially selected partition, ancl the worst, case tirnp
Data clustering has been studied in the Statistics complexity is still exponential. Hierarchtml clustertn[g
[DHi’3, D.J80, Lee81, Mur83], Machine Learning [CKS88, (HC) [DH73, KR90, Mur83] does not try to find “lwst,”
Fis87, Fis95, Lel>87] and Database [NH94, EKX95a, clusters, but keeps merging the closest, pair (or splitting
E1iX951]] communities with different, methods and dif- the farthest, pair) of objects to form clusters, Witlh a
ferent emphases, Previous approaches, probability- reasonable distance measurement,, the best time com-
I)ased (like most approaches in Machine Learning) or plexity of a practical HC algorithm is 0(N2). Scj it is
distauce-basecl (like most work in Statistics) , C1Onot, still unable to scale well with large N.
adequately consider the case that, the clataset can he too
Clustering has been recognized as a useful spatial data
large to fit in main memory. In particular, they do not
mining method recently. [NH94] presents (’L,4BAN,$’
rerognize that, the problem must be viewed in terms of
that is based on ranclornizecl search, and proposes
how to work with a limited resources (e.g., memory that,
that (_’LARAN,$ outperforms traditional clustering al-
is typirally, mu[-h smaller than the size of the dataset) to
gorithms in Statistics. In CLARANS, a rluster is repre-
do the clustering as accurately as possible while keeping
sented by its medotd, or the most, centrally loc-ated data
the 1/() costs low.
point in the cluster The clustering process is formali-
Probability-based approaches: They typically
zed as searching a graph in which each uocle is a Ii”-
[FisH7, (‘KSt38] make the assumption that probahilit,y
partition representeci by a set of Ii rnedoi(ls, and two
distributions on separate attributes are statistically
nodes are neighbors if they only differ by one medoid,
independent of each other, In reality, this is far
CLARANS starts with a randomly selectecl node. For
from true. (correlation between attributes exists, and
the current node, it checks at most the n~om~e~ghbor
sometimes this kind of correlation is exactly what we are
number of neighbors randomly, ancl if a better neigh-
looking for. The probability representations of c-lusters
bor is founcl, it moves to the neighbor ancl contiulles;
make updating and storing the clusters very expensive,
otherwise it records the current, node as a 10CCZ1T7LZnZ-
eslxv-ially if the attributes have a large number of values
mum, and restarts with a new randomly selected node
because their complexities are dependent not, only on
to search for another local mtntmum, {“?LARAN,S stops
the number of attributes, but also on the number of
after the numlocol number of the so-called loccd nLznz71w
values for each attribute. A related problem is that
have been found , and returns the best, of these,
often (e.g., [Fis87]), the probability-based tree that is
(YA RA N,S suffers from the same ch-awbacks as the
hllilt to identify clusters is not, height, -balanced, For
shove IO method wrt. efficiency In addition, it, may
skpwed input data, this may cause the performance to
not find a real local minimum due to the searching
(Iqiyade drarnatlically,
trimming controlled by mmmezghbor. Later [EKX9,5aj
Distance-based apprc)aclles: They assume that all
and [EK.X95h] propose focusing techniques (based on
data points are given in advance and can be scanned
R*-trees) to improve CLARA N,S’s ability to deal with
freclueutly. They totally or partially ignore the fact that
data objects that, may reside on clisks by (1) clustering
not, all clata points in the clataset are eclually irrrportant
a sample of the ciat,aset that is drawn from each R*-tree
with respect to the clustering purpose, and that dat, a
data page; ancl (2) focusing on relevant data points for
points which are close ancl d;nse shoulci he considered
clist,ance and quality updates, Their experiments show
collectively insteacl of individually, They are global or
that, the time 1simproved with a small loss of quality,
.se771z-globol methods at the granularity of data points.
That, is, for each clustering decision, they inspect, all 2.1 Cent ributions of BIRCH
data l)oints or all currently existing clusters eclually no An important contribution is our formulation of the
matter how close or far away they are, and they use clustering, problem in a way that, is appropriate for
104

very large clatasets, by making the time and memo- ~he average in$er.clust er distancs D%, average
ry constraints explicit. In addition, BIRCH has the mtra-cluster distance D3 and variance increase
|           |            |     |      |          |                |     |     | distance | D4  | of the two | clusters | are | defined | as: |     |
| --------- | ---------- | --- | ---- | -------- | -------------- | --- | --- | -------- | --- | ---------- | -------- | --- | ------- | --- | --- |
| following | advantages |     | over | previous | distance-based |     | ap- |          |     |            |          |     |         |     |     |
proaches.
(6)
l
| BIRCH         | is local | (as           | opposed        | to        | global)   | in               | that each  |                |     |      |            |          |     |         |      |
| ------------- | -------- | ------------- | -------------- | --------- | --------- | ---------------- | ---------- | -------------- | --- | ---- | ---------- | -------- | --- | ------- | ---- |
| clustering    | decision |               | is made        | without   |           | scanning         | all data   |                |     |      |            |          |     |         |      |
| points        | or all   | currently     |                | existing  | clusters. |                  | It uses    |                |     |      |            |          |     |         |      |
| rneasnrements |          | that          | reflect        | the       | natural   | closeness        | of         |                |     |      |            |          |     |         |      |
| points,       | and      | at the        | same           | time,     | can       | be incrementally |            |                |     |      |            |          |     |         |      |
| maintained    |          | during        | the clustering |           | process.  |                  |            |                |     |      |            |          |     |         |      |
| lBIRCH        | exploits | the           | observation    |           | that      | the              | data space |                |     |      |            |          |     |         |      |
| is usually    |          | not uniformly |                | occupied, |           | and              | hence not  |                |     |      |            |          |     |         |      |
| every         | data     | point is      | equally        | important |           | for              | clustering |                |     |      |            |          |     |         |      |
|               |          |               |                |           |           |                  |            | D3 is actually |     | D of | the merged | cluster. |     | For the | sake |
purposes.
A dense region of points is treated of clarity, we treat X-O, R and D as properties of a
collectively as a single cluster. Points in sparse regions 1,D2,
|             |     |             |     |         |     |             |     | single cluster, |              | and DO, | D         | D3 and | D4          | as properties |        |
| ----------- | --- | ----------- | --- | ------- | --- | ----------- | --- | --------------- | ------------ | ------- | --------- | ------ | ----------- | ------------- | ------ |
| are treated |     | as outlters | and | removed |     | optionally. |     |                 |              |         |           |        |             |               |        |
|             |     |             |     |         |     |             |     | between         | two clusters |         | and state | them   | separately. |               | [Jsers |
. BIRt~H makes full use of available memory to derive can optionally preprocess data by weighting or shifting
| the finest     | possible   |                 | subclusters |         | (to             | ensure       | accuracy)    |                 |     |               |         |           |     |        |          |
| -------------- | ---------- | --------------- | ----------- | ------- | --------------- | ------------ | ------------ | --------------- | --- | ------------- | ------- | --------- | --- | ------ | -------- |
|                |            |                 |             |         |                 |              |              | along different |     | dimensions    | without | affecting |     | the    | relative |
| while          | minimizing |                 | 1/0 costs   |         | (to ensure      |              | efficiency). | placement.      |     |               |         |           |     |        |          |
| The clustering |            | and             | reducing    | process |                 | is organized | and          |                 |     |               |         |           |     |        |          |
|                |            |                 |             |         |                 |              |              | 4 Clustering    |     | Feature       |         | and       | CF  | Tree   |          |
| characterized  |            | by the          | use         | of      | an in-memory,   |              | height-      |                 |     |               |         |           |     |        |          |
|                |            |                 |             |         |                 |              |              | The concepts    |     | of Clustering |         | Feature   |     | and CF | tree     |
| balanced       | and        | highly-occupied |             |         | tree structure. |              | Due to       |                 |     |               |         |           |     |        |          |
these features, its running time is linearly scalable. are at the core of BIRCH’S incremental clustering.
|             |       |              |      |       |             |          |           | A Clustering |      | Feature     | is  | a triple | summarizing |     | the |
| ----------- | ----- | ------------ | ---- | ----- | ----------- | -------- | --------- | ------------ | ---- | ----------- | --- | -------- | ----------- | --- | --- |
| . If we     | ornit | the optional |      | Phase | 4           | 5, BIRCH | is an     |              |      |             |     |          |             |     |     |
|             |       |              |      |       |             |          |           | information  | that | we maintain |     | about    | a cluster.  |     |     |
| incremental |       | method       | that | does  | not require |          | the whole |              |      |             |     |          |             |     |     |
clataset in advance, and only scans the clataset once. Definition 4.1 Given N d-dimensional data points in
|     |     |     |     |     |     |     |     | a cluster: | {ii} | where | i = | 1, 2, ....N, | the | Clustering |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ---- | ----- | --- | ------------ | --- | ---------- | --- |
3 Background Feature (CF) vector of the cluster is defined as a
Assume that readers are familiar with the terminology triple: CF = (N, L%’, S’S), where N is the number of
| of vector    | spaces,       | we             | begin | by defining |                 | centroid, | radius      |             |         |                |            |           |        |        |         |
| ------------ | ------------- | -------------- | ----- | ----------- | --------------- | --------- | ----------- | ----------- | ------- | -------------- | ---------- | --------- | ------ | ------ | ------- |
|              |               |                |       |             |                 |           |             | data points | in      | the cluster,   | L~$        | is the    | linear | sum    | of the  |
| and diameter |               | for a cluste~. |       | Given       | N d-dimensional |           | data        |             |         |                |            |           |        |        |         |
|              |               |                |       |             |                 |           |             | N data      | points, | i.e., ~~       | ~~~,       | and S’5’  | is the | square | sum     |
| points       | in a cluster: |                | {.Xi} | where       | i =             | 1,2,      | ....N, the  |             |         |                |            |           |        |        |         |
|              |               |                |       |             |                 |           |             | of the N    | data    | points,        | i.e., ~~=1 | X-iz.     | q      |        |         |
| centroid     | XO,           | radius         | R and | diameter    |                 | D of      | the cluster |             |         |                |            |           |        |        |         |
| are defined  | as:           |                |       |             |                 |           |             |             |         |                |            |           |        |        |         |
|              |               |                |       |             |                 |           |             | Theorem     | 4.1     | (CF Additivity |            | Theorem); |        |        | Assu7ne |
|              |               |                | f,.   | Ztl         | ~,              |           |             |             |         |                |            |           |        |        |         |
AT (1) that CF1 = (Nl ,L~l ,,$,$1), a91~ CF2 = (N2, L3’2, ,$,$’z)
|     |     |     |     |     |     |     |     | are the | CF vectors | of  | two | dw~oint | clusters. | Then | the |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | --- | --- | ------- | --------- | ---- | --- |
(2)
Jx’mt-m’)+ CF vector of the cluster that is formed by merging the
|     |     |     |     |     |     |     |     | two disjoint | clusters, |     | is: |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --------- | --- | --- | --- | --- | --- | --- |
(3)
|          |         |          | N(N–1) |      |        |        |        | CF1 + | CF2 | = (Nl | + N2, | L~l + L~2, | ,$,$1 | + ,5’,5’2) | (9) |
| -------- | ------- | -------- | ------ | ---- | ------ | ------ | ------ | ----- | --- | ----- | ----- | ---------- | ----- | ---------- | --- |
| R is the | average | distance |        | from | member | points | to the |       |     |       |       |            |       |            |     |
centroid. D is the average pairwise distance within The proof consists of straightforward algebra. []
|            |      |     |     |             |     |          |        | From | the CF | definition | and | additivity |     | theorem, | we  |
| ---------- | ---- | --- | --- | ----------- | --- | -------- | ------ | ---- | ------ | ---------- | --- | ---------- | --- | -------- | --- |
| a cluster. | They | are | two | alternative |     | measures | of the |      |        |            |     |            |     |          |     |
tightness of the cluster around the centroid. Next know that the CF vectors of clusters can be stored and
between two clusters, we define 5 alternative distances calculated incrementally and accurately as clusters are
|               |     |                  |     |     |     |     |     | merged. | It is | also easy | to  | prove | that given | the | CF  |
| ------------- | --- | ---------------- | --- | --- | --- | --- | --- | ------- | ----- | --------- | --- | ----- | ---------- | --- | --- |
| for measuring |     | their closeness. |     |     |     |     |     |         |       |           |     |       |            |     |     |
(iiven the centroids of two clusters: X~l ancl X_62, vectors of clusters, the corresponding XO, R, D, DO,
the centroid Euclidian distance DO and centroid D1, D2, D3 and D4, as well as the usual quality rnet,rics
| Manhattan |     | distance | D1  | of  | the | two clusters | are |          |          |               |     |          |     |              |     |
| --------- | --- | -------- | --- | --- | --- | ------------ | --- | -------- | -------- | ------------- | --- | -------- | --- | ------------ | --- |
|           |     |          |     |     |     |              |     | (such as | weighted | total/average |     | diameter |     | of clusters) |     |
defined as:
|     |     |     |          |            |     |     |     | can all be | calculated | easily. |         |      |        |      |         |
| --- | --- | --- | -------- | ---------- | --- | --- | --- | ---------- | ---------- | ------- | ------- | ---- | ------ | ---- | ------- |
|     |     | Do  | = ((X731 | – xi12)’)+ |     |     | (4) |            |            |         |         |      |        |      |         |
|     |     |     |          |            |     |     |     | One can    | think      | of a    | cluster | as a | set of | data | points, |
d
Ixbl – X7121= ~ [Xhl(t) – xb2(t)\ but only the CF vector stored as summary. This
|     | 1)1 = |     |     |     |     |     | (5) |            |     |        |      |           |         |     |        |
| --- | ----- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------ | ---- | --------- | ------- | --- | ------ |
|     |       |     |     |     |     |     |     | CF summary |     | is not | only | efficient | because | it  | stores |
,=1
|        |                  |     |      |        |     |            |        | much less | than | all the | data | points | in the | cluster, | hut |
| ------ | ---------------- | --- | ---- | ------ | --- | ---------- | ------ | --------- | ---- | ------- | ---- | ------ | ------ | -------- | --- |
| (iiven | NI d-dimensional |     | data | points | in  | a cluster: | {.~i } |           |      |         |      |        |        |          |     |
where i = 1,2, ....N], and N2 data points in another also accurate because it is sufficient for calculating all
|          |       |       |     |      |      |             |       | the measurements |           | that | we  | need for | making | clustering |     |
| -------- | ----- | ----- | --- | ---- | ---- | ----------- | ----- | ---------------- | --------- | ---- | --- | -------- | ------ | ---------- | --- |
| cluster: | {X-’} | where | j = | N1 + | l,N1 | + 2, ...)Nl | + N2, |                  |           |      |     |          |        |            |     |
|          |       |       |     |      |      |             |       | decisions        | in BIRCH. |      |     |          |        |            |     |
105

4.1 CF Tree each nonleaf entry on the path to the leaf. In the
A CF tree is a height-balanced tree with two pararrl- absence of a split, this simply involves adding CF
et(ers: branching factor B and threshold T. Each vectors to reflect the addition of “Ent”. A leaf split,
nonleaf node contains at most B entries of the form requires us to insert a new nonleaf entry into the
[CFi, rhddi], where r’= 1,2,..., B, “~hildi’) is a pointer parent, node, to describe the newly created leaf, If
to its i-th child node, and CF, is the CF of the sub- the parent, has space for this entry, at all higher levels,
clust, er represented by this child. So a nonleaf node we only need to update the CF vectors to reflect, the
represents a cluster made up of all the subclusters rep- addition of “Ent”. In general, however, we may have
| resented | l>y its | entries. |     |     |     |     |     |     |     |     |     |     |     |     |
| -------- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
A leaf node contains at most, L to split the parent as well, ancl so on up to the root,,
entries, each of the form [CFi], where i = 1, 2, ....L, In If the root is split, the tree height increases by one.
| addition, | each | leaf node | has | two pointers, |     | “prev” | and |                             |     |     |     |            |           |          |
| --------- | ---- | --------- | --- | ------------- | --- | ------ | --- | --------------------------- | --- | --- | --- | ---------- | --------- | -------- |
|           |      |           |     |               |     |        |     | 4.A Mergz?~gRefi?lelrte?tt: |     |     |     | Splits are | caused hy | the page |
“nrxt” which are used to chain all leaf nodes together size, which is independent of the clustering properties
for efficient scans. A leaf node also represents a clus- of the data. In the presence of skewed data input,
ter made up of all the subclusters represented by its order , this can affect the clustering quality, and also
entries. But all entries in a leaf node must] satisfy a recluce space utilization. A simple additional merging
| thrr.shold |     |     | with | respect | to a thresholci |     | value |     |     |     |     |     |     |     |
| ---------- | --- | --- | ---- | ------- | --------------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
requirement, step often helps ameliorate these problems: Suppose
T: tht- dtametrr (or radtus) has to & less than T. that there is a leaf split, and the propagation of this
The tree size is a function of T. The larger ‘T is, the split stops at some nonleaf nocle NJ, i.e., N,T can
slllaller the tree is. We require a node to it, in a pa~e accommodate the additional entry resulting from the
of size P, once the dimension d of the data space 1s split. We now scan node N,T to find the two closest
| g]veu, the | sizes | of leaf | and | nonleaf | entries | are | known, |          |         |     |     |                        |     |        |
| ---------- | ----- | ------- | --- | ------- | ------- | --- | ------ | -------- | ------- | --- | --- | ---------------------- | --- | ------ |
|            |       |         |     |         |         |     |        | entries. | If they | are | not | the pair corresponding |     | to the |
then B and L are determined by P. So P can be varied split, we try to merge them and the corresponding two
for performance tuning. child nodes. If there are more entries in the two child
| Such | a CF | tree will | be built | dynamically |     | as new | data |       |      |          |     |          |           |         |
| ---- | ---- | --------- | -------- | ----------- | --- | ------ | ---- | ----- | ---- | -------- | --- | -------- | --------- | ------- |
|      |      |           |          |             |     |        |      | nodes | than | one page | can | hold, we | split the | merging |
ohjectls are inserted. It, is used to guide a new insertion result again. During the resplitting, in case one of
illtlo the correct suhcluster for clustering purposes just the seed attracts enough merged entries to fill a page,
the same as a B+--tree is USd to guide a new insertion we just put the rest entries with the other seed. In
il]tu the corrert position for sorting purposes. The CF summary, if the mergecl entries fit, on a single page, we
| tree is | a very | compact | representation |     | of  | the | dat,aset |        |      |       |           |             |          |       |
| ------- | ------ | ------- | -------------- | --- | --- | --- | -------- | ------ | ---- | ----- | --------- | ----------- | -------- | ----- |
|         |        |         |                |     |     |     |          | free a | node | space | for later | use, create | one more | entry |
I>eralme each entry in a leaf node is not a single data space in node NJ, thereby increasing space utilization
l)oint hut, a subcluster (which absorbs many data points and postponing future splits; otherwise we improve
with diameter (or radius) under a specific threshold T). the distribution of entries in the closest, two children.
| 4.2 Insertion |          | into | a CF      | Tree |           |     |       |       |      |      |          |        |         |           |
| ------------- | -------- | ---- | --------- | ---- | --------- | --- | ----- | ----- | ---- | ---- | -------- | ------ | ------- | --------- |
|               |          |      |           |      |           |     |       | Since | each | node | can only | hold a | limited | number of |
| We now        | present, | the  | algorithm | for  | inserting | an  | entry |       |      |      |          |        |         |           |
into a CF tree. (~iveu entry “Ent”, it proceeds as entries clue to its size, it does not always correspond
helnw: to a natural cluster. occasionally, two subclusters that
|             |     |                 |     |       |          |      |     | should    | have been | in  | one   | cluster are   | split, across | nodes.     |
| ----------- | --- | --------------- | --- | ----- | -------- | ---- | --- | --------- | --------- | --- | ----- | ------------- | ------------- | ---------- |
| ldentzf~ymg |     | the appropriate |     | leaf: | Starting | from | the |           |           |     |       |               |               |            |
|             |     |                 |     |       |          |      |     | Depending | upon      | the | order | of data input | and           | the degree |
root,, it recursively descends the CF tree by choosing of skew, it is also possible that two subclust,ers that
| tile closest |     | child node | according |     | to a chosen | distance |     |        |        |        |         |          |             |       |
| ------------ | --- | ---------- | --------- | --- | ----------- | -------- | --- | ------ | ------ | ------ | ------- | -------- | ----------- | ----- |
|              |     |            |           |     |             |          |     | should | not be | in one | cluster | are kept | in the same | node. |
metric: DO, D1 ,D2, D3 or D4 as defined in Sec. 3. These infrequent, but unclesirahle anomalies caused Ijy
Modtf?ytn~g the leaf: When it reaches a leaf node, it page size are remedied with a global (or semi-glo]>al)
|     | rlosest | leaf | entry, | say | L,, and | then | tests |     |     |     |     |     |     |     |
| --- | ------- | ---- | ------ | --- | ------- | ---- | ----- | --- | --- | --- | --- | --- | --- | --- |
finc]s the algorithm that arranges leaf entries across nodes (Phase
whether L! can “ahsorh” “Ent” withoutv iolatingthe 3 discussed in Sec. 5), Another undesirable artifact, is
| threshold | conclitionz. |     | If  | SO, the | CF vector | for | Li is |         |          |      |       |             |        |         |
| --------- | ------------ | --- | --- | ------- | --------- | --- | ----- | ------- | -------- | ---- | ----- | ----------- | ------ | ------- |
|           |              |     |     |         |           |     |       | that if | the same | data | point | is inserted | twice, | hut at, |
ul~dated to reflect this, If not,, a new entry for “Ent,” different, times, the two copies might be entered into
is addecl to the leaf. If there is space on the leaf for distinct leaf entries. or, in another word, occasionally
| this new | entry, | we     | are done, | otherwise |     | we must, | .sp/it |            |        |        |        |               |             |         |
| -------- | ------ | ------ | --------- | --------- | --- | -------- | ------ | ---------- | ------ | ------ | ------ | ------------- | ----------- | ------- |
|          |        |        |           |           |     |          |        | with a     | skewed | input  | order, | a point,      | might enter | a leaf  |
| the leaf | node.  | ,Nocle | splitting | is done   | by  | choosing | the    |            |        |        |        |               |             |         |
|          |        |        |           |           |     |          |        | entry that | it,    | should | not    | have entered. | This        | problem |
farthest pair of entries as seeds, and redistributing can he addressed with further refinement passes over
| the remaining  |     | entries | based  | on the      | closest   | criteria. |       |          |        |             |     |         |     |     |
| -------------- | --- | ------- | ------ | ----------- | --------- | --------- | ----- | -------- | ------ | ----------- | --- | ------- | --- | --- |
|                |     |         |        |             |           |           |       | the data | (Phase | 4 discussed |     | in Ser. | 5), |     |
| .x.Modtf;jzn!g | th~ | ~mth    | to the | leaf: After | inserting |           | “Ent” |          |        |             |     |         |     |     |
mt,o a leaf, we must, update the CF information for 5 The BIRCH Clustering Algorithm
|               |              |         |          |            |           |          |         | Fig. 1 presents |      | the        | overview | of BIRCH.     | The      | main task   |
| ------------- | ------------ | ------- | -------- | ---------- | --------- | -------- | ------- | --------------- | ---- | ---------- | -------- | ------------- | -------- | ----------- |
| 2Tl}at        | is, the      | cluster | n)erged  | with “Ent” | and       | L, n]ust | satisfy |                 |      |            |          |               |          |             |
|               |              |         |          |            |           |          |         | of Phase        | 1 is | to scan    | all      | data and      | build an | initial in- |
| the threshold | condition.   |         | Note     | that the   | CF vector | of       | the new |                 |      |            |          |               |          |             |
|               |              |         |          | CF         |           |          |         | memory          | CF   | tree using | the      | given amount, | of       | memory      |
| rluster cal}  | be eomputecl |         | from the | vectors    | for       | L! and   | “Ent”.  |                 |      |            |          |               |          |             |
106

| Data    |         | J/  |     |     |     |     |     |                  |              |           |      |             |                 |        |           |
| ------- | ------- | --- | --- | --- | --- | --- | --- | ---------------- | ------------ | --------- | ---- | ----------- | --------------- | ------ | --------- |
|         |         |     |     |     |     |     |     | of a subcluster, |              | we        | can  | treat       | each subcluster |        | as a      |
|         |         |     |     |     |     |     |     | single point     |              | and use   | an   | existing    | algorithm       |        | without,  |
|         |         |     |     |     |     |     |     | modification;    |              | (2) or to | be a | little more | sophisticated,  |        | we        |
| Initial | CF tree |     |     |     |     |     |     |                  |              |           |      |             |                 |        |           |
|         |         |     |     |     |     |     |     | can treat        | a subcluster |           | of   | n data      | points          | as its | cent,roid |
Phase 2 <optional): Condense tit. desirable rang. repeating n times and modify an existing algorithm
|     |     |     | by  | buildkpj | . sm.11.r |     | CF tree |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | -------- | --------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
1
|            |           |     |             |     |     |     |     | slightly        | to take   | the        | counting | information      |             | into        | account;    |
| ---------- | --------- | --- | ----------- | --- | --- | --- | --- | --------------- | --------- | ---------- | -------- | ---------------- | ----------- | ----------- | ----------- |
| .n, aller  | C-F tree  |     |             |     |     |     |     |                 |           |            |          |                  |             |             |             |
|            |           | +   |             |     |     |     |     | (3) or to       | be        | general    | and      | accurate,        | we          | can         | apply an    |
| r F’base.z | 3: Global |     | Clu steting |     |     |     | 1   |                 |           |            |          |                  |             |             |             |
|            |           |     |             |     |     |     |     | existing        | algorithm | directly   |          | to the           | subclusters |             | because     |
|            |           |     |             |     |     |     |     | the information |           | in their   | CF       | vectors          | is usually  |             | sufficient, |
|            |           |     |             |     |     |     |     | for calculating |           | most       | distance | and              | quality     | metrics.    |             |
|            |           |     |             |     |     |     |     | In this         | paper,    | we adapted |          | an agglomerative |             | hierarchic- |             |
Better clusters al clustering algorithm by applying it directly to the
+~
|     |     |     |     |     |     |     |     | subclusters | represented |     | by  | their | CF vectors. |     | It uses |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | --- | --- | ----- | ----------- | --- | ------- |
Figure 1: BIRCH OvervZcuI the accurate distance metric D2 or D4, which can he
|                   |            |       |              |                   |             |         |            | calculated      | from      | the          | CF vectors,  | during     |            | the whole | clus-    |
| ----------------- | ---------- | ----- | ------------ | ----------------- | ----------- | ------- | ---------- | --------------- | --------- | ------------ | ------------ | ---------- | ---------- | --------- | -------- |
| and recycling     |            | space | on disk.     |                   | This        | CF tree | tries to   |                 |           |              |              |            |            |           |          |
|                   |            |       |              |                   |             |         |            | tering, and     | has       | a complexity |              | of O(lV2). |            | It also   | provides |
| reflect the       | clustering |       | information  |                   | of the      | dataset | as fine    |                 |           |              |              |            |            |           |          |
|                   |            |       |              |                   |             |         |            | the flexibility |           | of allowing  |              | the user   | to specify | either    | the      |
| as possible       | under      |       | the memory   |                   | limit.      | With    | crowded    |                 |           |              |              |            |            |           |          |
|                   |            |       |              |                   |             |         |            | desired         | number    | of clusters, |              | or the     | desired    | diameter  | (or      |
| data points       | grouped    |       | as           | fine subclusters, |             |         | and sparse |                 |           |              |              |            |            |           |          |
|                   |            |       |              |                   |             |         |            | radius)         | threshold | for          | clusters.    |            |            |           |          |
| data points       | removed    |       | as outliers, |                   | this phase  | creates | a in-      |                 |           |              |              |            |            |           |          |
|                   |            |       |              |                   |             |         |            | After           | Phase     | 3, we        | obtain       | a          | set, of    | clusters  | that,    |
| memory            | summary    | of    | the          | data.             | The details |         | of Phase 1 |                 |           |              |              |            |            |           |          |
|                   |            |       |              |                   |             |         |            | captures        | the       | major        | distribution |            | pattern    | in the    | data,    |
| will be discussed |            | in    | Sec. 5.1.    | After             | Phase       | 1,      | subsequent |                 |           |              |              |            |            |           |          |
computations in later phases will be: However minor and localized inaccuracies might exist
|              |     |               |                |     |          |         |            | because   | of the  | rare misplacement |       |         | problem    | mentioned | in       |
| ------------ | --- | ------------- | -------------- | --- | -------- | ------- | ---------- | --------- | ------- | ----------------- | ----- | ------- | ---------- | --------- | -------- |
| 1fast became |     | (a) no        | 1/0 operations |     | are      | needed, | and (b)    |           |         |                   |       |         |            |           |          |
|              |     |               |                |     |          |         |            | Sec. 4.2, | and the | fact              | that  | Phase 3 | is applied | on        | a coarse |
| the problem  |     | of clustering |                | the | original | data    | is reduced |           |         |                   |       |         |            |           |          |
|              |     |               |                |     |          |         |            | summary   | of the  | data.             | Phase | 4 is    | optional   | and       | entails  |
to a smaller problem of clustering the subclusters in the cost of additional passes over the data to correct
| the leaf | entries; |     |     |     |     |     |     |                    |     |     |        |     |          |          |      |
| -------- | -------- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | ------ | --- | -------- | -------- | ---- |
|          |          |     |     |     |     |     |     | those inaccuracies |     | and | refine | the | clusters | further. | Note |
2. accurate because (a) a lot of outliers are eliminated, that up to this point, the original data has only been
| ancl (b) | the | remaining | data | is  | reflected | with | the finest |         |       |          |     |          |         |             |     |
| -------- | --- | --------- | ---- | --- | --------- | ---- | ---------- | ------- | ----- | -------- | --- | -------- | ------- | ----------- | --- |
|          |     |           |      |     |           |      |            | scanned | once, | although | the | tree and | outlier | information |     |
granularity that can be achieved given the available may have been scanned multiple times.
rnernory;
|     |     |     |     |     |     |     |     | Phase | 4 uses | the centroids |     | of the | clusters | produced | Ly  |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | ------ | ------------- | --- | ------ | -------- | -------- | --- |
3. less order sensitive because the leaf entries of the Phase 3 as seeds, and redistributes the data points to
| initial  | tree form | an  | input | order | containing |          | better data |             |       |           |           |            |           |     |            |
| -------- | --------- | --- | ----- | ----- | ---------- | -------- | ----------- | ----------- | ----- | --------- | --------- | ---------- | --------- | --- | ---------- |
|          |           |     |       |       |            |          |             | its closest | seed  | to obtain | a         | set of new | clusters. |     | Not only   |
| locality | compared  |     | with  | the   | arbitrary  | original | data        |             |       |           |           |            |           |     |            |
|          |           |     |       |       |            |          |             | does this   | allow | points    | belonging | to         | a cluster | to  | rnigrat,e, |
input, order. but also it ensures that all copies of a given data point
|               |      |             |     |            |          |         |         | go to the  | same   | cluster.   | Phase | 4      | can be | extended | with     |
| ------------- | ---- | ----------- | --- | ---------- | -------- | ------- | ------- | ---------- | ------ | ---------- | ----- | ------ | ------ | -------- | -------- |
| Phase         | 2 is | optional.   | We  | have       | observed | that    | the ex- |            |        |            |       |        |        |          |          |
|               |      |             |     |            |          |         |         | additional | passes | if desired |       | by the | user,  | and it   | has been |
| isting global | or   | semi-global |     | clustering |          | methods | applied |            |        |            |       |        |        |          |          |
in Phase 3 have different input size ranges within which proved to converge to a minimum [G G92]. As a bonus,
|                |         |         |          |           |         |          |             | during this  | pass       | each     | data      | point can | be labeled  |       | with the |
| -------------- | ------- | ------- | -------- | --------- | ------- | -------- | ----------- | ------------ | ---------- | -------- | --------- | --------- | ----------- | ----- | -------- |
| they perform   |         | well in | terms    | of both   | speed   | and      | quality.    |              |            |          |           |           |             |       |          |
|                |         |         |          |           |         |          |             | cluster that | it         | belongs  | to, if    | we wish   | to identify |       | the data |
| So potentially |         | there   | is a gap | between   |         | the size | of Phase    |              |            |          |           |           |             |       |          |
|                |         |         |          |           |         |          |             | points in    | each       | cluster. | Phase     | 4 also    | provides    | us    | with the |
| 1 results      | and the | input   | range    | of        | Phase   | 3. Phase | 2 serves    |              |            |          |           |           |             |       |          |
|                |         |         |          |           |         |          |             | option of    | discarding |          | outliers. | That      | is, a       | point | which is |
| as a cushion   | and     | bridges |          | this gap: | Similar |          | to Phase 1, |              |            |          |           |           |             |       |          |
it scans the leaf entries in the initial CF tree to rebuild too far from its closest, seed can be treated as an outlier
|           |         |             |       |          |        |          |     | and not | included | in  | the result. |     |     |     |     |
| --------- | ------- | ----------- | ----- | -------- | ------ | -------- | --- | ------- | -------- | --- | ----------- | --- | --- | --- | --- |
| a smaller | CF      | tree,       | while | removing | more   | outliers | and |         |          |     |             |     |     |     |     |
| grouping  | crowded | subclusters |       | into     | larger | ones.    |     |         |          |     |             |     |     |     |     |
The undesirable effect of the skewed input order, 5.1 Phase 1 Revisited
and splitting triggered by page size (Sec. 4.2) causes Fig. 2 shows the details of Phase 1. It starts with
us to be unfaithful to the actual clustering patterns an initial threshold value, scans the data, and inserts
in the data. This is remedied in Phase 3 by using points into the tree. If it runs out of memory before
a global or semi-global algorithm to cluster all leaf it finishes scanning the data, it increases the threshold
entries. We observe that existing clustering algorithms value, rebuilds a new, smaller CF tree, by re-inserting
for a set of data points can be readily adapted to work the leaf entries of the old tree. After the old leaf entries
with a set, of subclusters, each described by its CF have been re-inserted, the scanning of the data (and
vector. For example, with the CF vectors known, (1) insertion into the new tree) is resumed from the point
naively, by calculating the centroid as the representative at which it was interrupted.
107

proceeds as below:
1 Creatr thr corrrspondL7ig “Nru)(!urre~it[ ’atll” tn the
,
new tree: nodes are added to the new tree exactly
f (.ontmue scanning data and insert to +1 1 the same as in the old tree, so that there is no chance
out of mem”l-v.. Result? Fuush scamm~ data that the new tree ever hecornes larger than the old
v I tree.
(1) Increase T.
2 Insert leaf e7itrze.s tn “OldCurrmtI)atli” to thy neti)
(2) Rebudd (LFtxe t2ofnew Tfrom (.Ftreetl:
if. leaf entry oftl k potential outher and disk space .wadabks, tree: with the new threshold, each leaf entry in “olCi-
write to disk; othewise use itto mbudd t2.
(3) tl <-tz (.~urrentPath” is tested against the new tree to see if it,
can fit 3 in the “NewC1osest Pat,h” that, is found top
c Otherw’,.e ~ Out ofdisk space down with the closest criteria in the new tree. If yes
( Re-absmb tmtentid outiiers into tl 1 and ‘LNew(~losestPath” is before “New(.~urrentPa t,h”,
then it is inserted to “NewClosestPath”, and the space
c 1
in “NewCurrentPath” is left available for later use;
( otherwise it is inserted to “New( ;urrent F’ath” without
Re-.bamb potemi.+1 outkrs mto tl
creating any new node.
I
3, Frer spare iIt “OldCurrentPath” and “Ne W( ‘ur7rnt-
Path”: Once all leaf entries in “OICI( ;urrentF’ath” are
Figure 2: (!ontrol Flou) of Phase 1 processed, the un-needed nodes along “01[1( !urrent,-
old Tree New Tree Path>’ can be freed. It is also likely that some nodes
A-A
along “NewC;urrentPath” are empty because leaf en-
tries that originally correspond to this path are now
“pushed forward”. In this case the empty nodes can
be freed too.
4. “OldCurre71tPath” M set to thr next pdh z71the> old
OldCurrentPath NeWClOSeStPath NewCurrentPath
tnw tf ther-r rxzsts 071r, a71d repeat the abmw stq3s.
Figure 3: Ftebuddtmg <’F Tree
From the rebuilding steps, old leaf entries are re-
inserted, but the new tree can never become larger
5.1.1 Reducibility
Assume t, is a CF tree of threshold T,. Its height than the old tree. Since only nodes corresponding
to “OldC!urrent Path” and “New( k~rrentPath” need to
is h, and its size (numl>er of nodes) is ,’i’t, (iiven
exist simultaneously, the maximal extra space needed
T,+l > T,, we want to use all the leaf entries of tz to
for the tree transforrnation is h pages. So hy increasing
rebuild a CF tree. t%+l , of threshold T,+l such that the
the threshold, we can rebuild a smaller CF tree with a
size of tt+ 1 should not, be larger than ,$’~. Following
limited extra memory.
ifi the rebuilding algorithm as well as the consequent
reduril>ility theorem.
Theorem 5.1 (Tkducibilit y Theorem: ): .+!,ssunt c
Assome within each node of CF tree t,, the entries
we rekld CF tme t~+1 of thrr.shold Ti+ ~ from (“’F t,rr~
are labeled contiguously from O to nk — 1, where 71k is
t, of threshold T%by the about, al~gorlthm, and let ,5’, GItd
the number of entries in that node, then a path from
S,+l be the szz~s oft, and t,+l resprctzuel~j. If T,+l > T,,
an entry in the root (level 1) to a leaf node (level h)
then ,S1+l < ,S%,and the transforniatzo71 from t% to t,+,
(an he uniquely representeci by (il ,i2, ,.., i}~_, ), where
71eeds at Tnost h ext r-o pages of 7r~e7nory, 71111we h 1s the
i,),:1 = ll...,)/ – 1 is the label of the j-th level entry
Ileaght oft,.
.(1) .(1)
on that path. So naturally, path (tl ,Z2 ,....zl‘~(’_)l ) is
befc)re (or< )pat,h(i\2), i$), ....i~~l) ifi\l)=i~2) ..,., 5.1.2 Threshold Values
z . , ( 7 1 – ) 1 = ~ l_ (~ l, ) and i~l) < iJ2)(0 <j ~ h-l). It is obvious A good choice of threshold value can greatly reduce the
that, a leaf node corresponds to a path uniquely, and we number of rebuilds. Since the initial threshold value To
will use path and leaf node interchangeably from now is increased dynamically, we can adjust for its lwing tc)o
on. low. But if the initial TO is too high, we will obtain a
less detailed CF tree than is feasible with the available
The algorithm is illustrated in Fig. 3. With the
memory. So To should he set conservatively. BIR(~H
natural path order defined above, it, scans and frees the
sets it, t,o zero by default; a knowledgeable user could
old tree path by path, and at, the same time, creates the
change this,
new tree path hy path. The new tree starts with NIJLL,
an[l “ol~l(.~urrentpat n’” starts with the leftmost path
3Eit11er absorbed by an existing leaf entry, or created as a IIeW
in the old tree. For “old(!urrentpat h’”, the algorithr~l leaf entry witllOut splitting.
108

Suppose that T, turns out to lx= too small, and we obtained thus is less than T~ then we choose Tt+l = T! Y
| subsequently | run | out | of memory | after | Nt  | data points |       |     |       |               |     |             |     |      |           |
| ------------ | --- | --- | --------- | ----- | --- | ----------- | ----- | --- | ----- | ------------- | --- | ----------- | --- | ---- | --------- |
|              |     |     |           |       |     |             | (~)~. |     | (This | is equivalent |     | to assuming |     | that | aII iar:~ |
have been scanneci, and ~~%leaf entries have hem formed points are uniformly distributed in a d-(dimensional
(eaeh satisfying the threshold condition wrt. fi). Based sphere, and is really just a crude :tI>l]roxiI1l:iti t)ll,
on the portion of the data that we have scanned and the however, it is rarely called for. )
| tree that,          | we have   | built | up so           | far, we | need       | to estimate |       |                  |     |     |     |        |     |     |     |
| ------------------- | --------- | ----- | --------------- | ------- | ---------- | ----------- | ----- | ---------------- | --- | --- | --- | ------ | --- | --- | --- |
| the next            | threshold | value | T,+l            | This    | estimation | is a        |       |                  |     |     |     |        |     |     |     |
|                     |           |       |                 |         |            |             | 5.1.3 | Outlier-Handling |     |     |     | Option |     |     |     |
| diflirult i>roblemi |           | and   | a full solution |         | is beyond  | the scope   |       |                  |     |     |     |        |     |     |     |
of this paper. (!urrently, we use the following heuristie Optionally, we c-an use R bytes of disk space for handling
|     |     |     |     |     |     |     | outlters, | which |     | are leaf | entries | of  | low density |     | that are |
| --- | --- | --- | --- | --- | --- | --- | --------- | ----- | --- | -------- | ------- | --- | ----------- | --- | -------- |
approarh:
|     |     |     |     |     |     |     | judged | to  | be unimportant, |     | wrt. | the | overall | elllst,ering |     |
| --- | --- | --- | --- | --- | --- | --- | ------ | --- | --------------- | --- | ---- | --- | ------- | ------------ | --- |
1.We try to choose 2“%+1so that, N,+l = Min(2N,, N). pattern. When we rebuild the CF tree by re-inserting
That, is, whether N is known, we choose to estirnat,e the old leaf entries, the size of the new tree is reduce(l
| T,+ I at        | most in | proportion |             | to the    | data | we have seen |         |          |        |          |             |       |               |              |        |
| --------------- | ------- | ---------- | ----------- | --------- | ---- | ------------ | ------- | -------- | ------ | -------- | ----------- | ----- | ------------- | ------------ | ------ |
|                 |         |            |             |           |      |              | in two  | ways.    | First, |          | we increase |       | the threshold |              | value, |
| thus far.       |         |            |             |           |      |              | thereby | allowing |        | each     | leaf        | entry | to “ahsorh”   |              | more   |
| 2. Intuitivelyj | we      | want       | to increase | threshold |      | based on     |         |          |        |          |             |       |               |              |        |
|                 |         |            |             |           |      |              | points. | Second,  |        | we treat | some        | leaf  | entries       | as potential |        |
some measure of volrme. There are two distinct, outliers and write them out to disk. An old leaf entry 1s
notions of volume that we use in estimating threshold, considered to be a potential outlier if it has “far fewer”
The first is average volume, which is defineci as t~ = rd data points than the average. “Far fewer”, is of course
| where r  | is the | average  | radius          | of the | root | cluster in the | another       | heuristics. |     |          |       |     |     |      |         |
| -------- | ------ | -------- | --------------- | ------ | ---- | -------------- | ------------- | ----------- | --- | -------- | ----- | --- | --- | ---- | ------- |
| CF tree, | and    | d is the | (Iimensionality |        | of   | the space.     |               |             |     |          |       |     |     |      |         |
|          |        |          |                 |        |      |                | Periodically, |             |     | the disk | space | may | run | out, | and the |
Intuitively, this is a measure of the space oeeupied by potential outliers are scanned to see if they can he re-
| the portion | oft      | he data | seen   | thus far  | (the “footprint” | of     |          |     |          |         |          |         |               |     |          |
| ----------- | -------- | ------- | ------ | --------- | ---------------- | ------ | -------- | --- | -------- | ------- | -------- | ------- | ------------- | --- | -------- |
|             |          |         |        |           |                  |        | absorbed |     | into the | current | tree     | without | causing       |     | the tree |
| seen data). | A second |         | notion | of volume | packed           | tdum~, |          |     |          |         |          |         |               |     |          |
|             |          |         |        |           |                  |        | to grow  | in  | size.    | — An    | increase | in      | the threshold |     | value    |
which is defined as Vp = (~, * T%(i, where ~1~ is the or a change in the distribution due to the new (Iat,a
| number | of leaf | entries | and | Tt d is the | maximal | volume |      |       |             |     |         |            |     |            |      |
| ------ | ------- | ------- | --- | ----------- | ------- | ------ | ---- | ----- | ----------- | --- | ------- | ---------- | --- | ---------- | ---- |
|        |         |         |     |             |         |        | read | after | a potential |     | outlier | is written |     | out] could | well |
of a leaf entry. Intuitively, this is a measure of the mean that the potential outlier no longer qualities as an
| actual volume  |     | occupied | by       | the leaf | clusters. | Since ~~z |          |       |        |      |          |           |            |               |           |
| -------------- | --- | -------- | -------- | -------- | --------- | --------- | -------- | ----- | ------ | ---- | -------- | --------- | ---------- | ------------- | --------- |
|                |     |          |          |          |           |           | outlier. | When  | all    | data | has been | scanneci, |            | the potential |           |
| is essentially | the | same     | whenever | we       | run out   | of memory |          |       |        |      |          |           |            |               |           |
|                |     |          |          |          |           |           | outliers | left, | in the | disk | space    | must      | be scanned |               | to verify |
(since we work with a fixed amount, of memory), we if they are indeed outliers. If a potential outlier ran not
| can approximate |     | VP  | by Tid. |     |     |     |             |     |     |           |         |     |         |        |        |
| --------------- | --- | --- | ------- | --- | --- | --- | ----------- | --- | --- | --------- | ------- | --- | ------- | ------ | ------ |
|                 |     |     |         |     |     |     | he absorbed |     | at  | this last | chance, | it, | is very | likely | a real |
We make the assumption that r grows with the outlier and can be removed.
| number | of data | points | Ni. | By maintaining |     | a rerord |      |      |     |        |       |     |              |     |        |
| ------ | ------- | ------ | --- | -------------- | --- | -------- | ---- | ---- | --- | ------ | ----- | --- | ------------ | --- | ------ |
|        |         |        |     |                |     |          | Note | that | the | entire | cycle | —   | insufficient |     | memory |
of r and the number of points Ni, we ean estimate triggering a rebuilding of the tree, insufficient disk spare
| ri+ 1 using  | least, | squares | linear | regression. |          | We define |             |     |                |       |        |           |               |     |          |
| ------------ | ------ | ------- | ------ | ----------- | -------- | --------- | ----------- | --- | -------------- | ----- | ------ | --------- | ------------- | --- | -------- |
|              |        |         |        |             |          |           | triggering  |     | a re-absorbing |       | of     | outliers, | etc.          | —   | could    |
| the ezpnrmon |        | factor  | f =    | Maz(        | 1.01 *), | and use   |             |     |                |       |        |           |               |     |          |
|              |        |         |        |             |          |           | be repeated |     | several        | times | before |           | the datlasetf |     | is fldly |
it as a heuristic measure of how the data footprint scanned. This effort must be considered in a[l(lit,ion t,c
| is growing. | The     | use      | of Max   | is        | motivated | by our        |          |     |             |     |      |          |     |        |             |
| ----------- | ------- | -------- | -------- | --------- | --------- | ------------- | -------- | --- | ----------- | --- | ---- | -------- | --- | ------ | ----------- |
|             |         |          |          |           |           |               | the cost | of  | scanning    | the | data | in order | to  | assess | t,he (-Ost, |
| observation | that    | for most | large    | datasets, |           | the observeci | of Phase | 1   | accurately. |     |      |          |     |        |             |
| footprint   | heeomes | a        | constant | quite     | quickly   | (unless       |          |     |             |     |      |          |     |        |             |
the input order is skewed). Similarly, by making 5.1.4 Delay-Split Option
the assumption that VT, grows linearly with Ni, we When we run out of main memory, it may well he the
estimate Ti+ 1 using least squares linear regression. case that still more data points can fit, in the current, CF
3. We traverse a path from the root to a leaf in the CF tree, without changing the threshold. However, some of
tree, always going to the child with the most points the data points that we read may require us to sl)lit
| in a “greedy” |     | attempt | to find | the | most | crowded leaf |        |     |         |       |          |      |     |          |        |
| ------------- | --- | ------- | ------- | --- | ---- | ------------ | ------ | --- | ------- | ----- | -------- | ---- | --- | -------- | ------ |
|               |     |         |         |     |      |              | a node | in  | the (3F | tree, | A simple | idea | is  | to writ, | e such |
node. We calculate the distance (~),nin ) between the data points to disk (in a manner similar to how outliers
rlosest two entries on this leaf. If we want to build a are written), and to proceed reading the data until we
more condensed tree, it is reasonable to expeet that we run out, of disk space as well. The advantage of this
should at least increase the threshold value to D~Zn, approach is that in general, more data points ean fit in
| so that          | these two | entries  | can   | he merged. |         |        |          |        |     |      |             |     |     |     |     |
| ---------------- | --------- | -------- | ----- | ---------- | ------- | ------ | -------- | ------ | --- | ---- | ----------- | --- | --- | --- | --- |
|                  |           |          |       |            |         |        | the tree | before | we  | have | to rebuild. |     |     |     |     |
| 4. We multiplied |           | the Ti+l | value | obtained   | through | linear |          |        |     |      |             |     |     |     |     |
regression with the expansion factor f, ancl adjustecl 6 Performance Studies
| it using       | D~i~      | as follows: |      | Tt+l      | = Mwr(DTntn, | f *         |             |     |              |            |                |      |          |            |       |
| -------------- | --------- | ----------- | ---- | --------- | ------------ | ----------- | ----------- | --- | ------------ | ---------- | -------------- | ---- | -------- | ---------- | ----- |
|                |           |             |      |           |              |             | We present  |     | a complexity |            | analysis,      |      | and then | discuss    | the   |
| T%+,).         | To ensure | that        | the  | threshold |              | value grows |             |     |              |            |                |      |          |            |       |
|                |           |             |      |           |              |             | experiments |     | that         | we         | have conducted |      | on       | BIRC’H     | (an(l |
| monotonically, |           | in the      | very | unlikely  | case         | that, Ti+ 1 |             |     |              |            |                |      |          |            |       |
|                |           |             |      |           |              |             | (~LARAN,S)  |     | using        | synthetic’ | as             | well | as real  | dataset,s. |       |
109

6.1 Analysis Paran3eter Values or
First we analyze the cpu cost of Phase 1. The maximal ........ ~..-,
u... -
size of the tree is #. To insert a point, we need to follow Number of clusters h- 4.. 256
nt (Lower n) 0.. 2500
a path from root to leaf, touching about 1 + logB ~ ?Lh(Higher n) 50.. 2500
nodes. At each node we must examine B entries, looking u r-~(Lower r) 0.. d2 u
for the “closest”; the cost per entry is proportional to
the dimension d. So the cost for inserting all data points
is O(d * N * B(l + logB $)). In case we must rebuild
the tree, let ES be the CF entry size. There are at
most & leaf entries to re-insert, so the cost of re-
inserting leaf entries is O(d * & * B( 1+ logB ~)). The
Table 1: Data Generation Parameters and Thetr Values
number of times we have to re-builcl the tree depends
or Ranges Experimented
upon our threshold heuristics. Currently, it is about
logz & , where the value 2 arises from the fact that we dimension. We refer to these ranges as the “overview”
never estimate farther than twice of the cm-rent size, of the dataset.
and NO is the number of data points loaded into memory The location of the center of each cluster is deter-
with threshold To. So the total CPU cost of Phase 1 is mined by the pattern parameter. Three patterns —
()(d*N*B(l+logB *)+log2 ~*i*#$*B(l+logB *)). grzd, ,stne, and random — are currently supported by
The analysis of Phase 2 cpu cost is similar, and hence the generator. When the gnd pattern is used, the clus-
omitted. ter centers are placed on a ~ x @ grid. The distance
As for 1/0, we scan the data once in Phase 1 and between the centers of neighboring clusters on the same
not at all in Phase 2. With the outlier-handling and row/column is controlled by kg, and is set to k{+.
delay-split options on, there is some cost associated with This leads to an overview of [O,~kj~] on both
writing out outlier entries to disk and reading them dimensions. The szne pattern places the cluster cen-
back during a rebuilt. Considering that the amount ters on a curve of sine function. The K clusters are
of disk available for outlier-handling (and delay-split) divided into 71, groups, each of which is placecl on a
is not more than M, and that there are about log2 ~
different cycle of the sine function. The c location of
re-builds, the 1/0 cost of Phase 1 is not significantly the center of cluster i is 2ni whereas the y location is
different from the cost of reading in the dataset. Based ~ * sine (2ni/(~)). The overview of a sine dataset is
nc
on the above analysis — which is actually rather
therefore [0,2mK] and [–~ ,+~] on the x and y di-
pessimistic, in the light of our experimental results —
rections respectively. The random pattern places the
the cost of Phases 1 and 2 should scale linearly with N.
cluster centers randomly. The overview of the dataset is
There is no 1/0 in Phase 3. Since the input to
[O,K] on both dimensions since the the c and y locations
Phase 3 is bounded, the cpu cost of Phase 3 is therefore
of the centers are both randomly distributed within the
hounded hy a constant that depends upon the maximum
range [O,K].
input, size and the global algorithm chosen for this
Once the characteristics of each cluster are deter-
phase. Phase 4 scans the clataset again and puts each
mined, the data points for the cluster are generated ac-
data point into the proper cluster; the time taken is
cording to a 2-d independent normal distribution whose
proportional to IV * K. (However with the newest
mean is the center c, and whose variance in each di-
“nearest neighbor” techniques, it can be improved
mension is $. Note that due to the properties of the
[(i(~92] to be almost linear wrt. N.)
normal distribution, the maximum distance between a
6.2 Synthetic Dataset Generator
point in the cluster and the center is unbounded. In
To study the sensitivity of BIRCH to the characteristics
other words, a point may be arbitrarily far from its be-
of a wide range of input datasets, we have used a
longing cluster. So a data point that belongs to cluster
collection of synthetic datasets generated by a generator
A may be closer to the center of cluster B than to the
that, we have developed. The data generation is
center of A, and we refer to such points as “outsiders”.
controlled by a set of parameters that are summarized
In addition to the clustered data points, noise in the
in Table 1.
form of data points uniformly distributed throughout
Each dataset consists of 1{ clusters of 2-d data points.
the overview of the dataset can be added to the dataset.
A cluster is characterized by the number of data points
The parameter rn controls the percentage of data points
in it,(n), its radius(r), and its center(c). n is in the
in the dataset that are considered noise.
range of [7~/,nk], and r is in the range of [rl ,rh]4. once
The placement of the data points in the dataset
placed, the clusters cover a range of values in each
is controlled by the order parameter o. When the
4Note tllat wl)en ?LL = TLh tl]e nun)her of points is fixed and randomized option is used, the data points of all clusters
WlIeII rl = r,, tlle radius is fixed, and the noise are randomized throughout the entire
110

Scope Parameter Default Value entry of which the number of ciatla points is less than
(;lobal Memory (M) 8OX1O24 bytes a quarter of the average as an outlier.
20%M
Disk (R) L In Phase 3, most global algorithms can handle 1000
|     |     | Dista;lc~ | clef. | [)2       |     |       |     |           |         |       |       |          |     |             |     |
| --- | --- | --------- | ----- | --------- | --- | ----- | --- | --------- | ------- | ----- | ----- | -------- | --- | ----------- | --- |
|     |     |           |       |           |     |       |     | ol>jectls | cluitle | well. | So we | default, | the | input range | as  |
|     |     | Quality   | clef. | ::~~,,o,d |     | for ~ |     |           |         |       |       |          |     |             |     |
Threshold clef. 1000. We have chosen the adaptecl H(7 algorithm to use
F’hasel Initial tbresbold 0.0 here. We deciclecl to let Phase 4 refine the clusters only
Delay-split
011 once with its ciiscarcl-out,lier option off, so that all (Iat,a
|     |     | ~age             | size (P) | 1024     | bytes |         |     |                   |          |          |             |         |              |     |     |
| --- | --- | ---------------- | -------- | -------- | ----- | ------- | --- | ----------------- | -------- | -------- | ----------- | ------- | ------------ | --- | --- |
|     |     |                  |          |          |       |         |     | points            | will be  | counteci | in the      | quality | measurement, |     | for |
|     |     | outlier-handling |          | 01)      |       |         |     |                   |          |          |             |         |              |     |     |
|     |     | outlier          | clef.    | Leaf     | entry | which   |     | fair comparisons. |          |          |             |         |              |     |     |
|     |     |                  |          | contaias | <     | ~5Y0 of |     | 6.4 Base          | Workload |          | Performance |         |              |     |     |
the average aumt)er The first set of experiments was to evaluate the ability of
|     |     |     |     | of        | pOints per | leaf     |     |               |               |           |            |             |       |               |       |
| --- | --- | --- | --- | --------- | ---------- | -------- | --- | ------------- | ------------- | --------- | ---------- | ----------- | ----- | ------------- | ----- |
|     |     |     |     |           |            |          |     | J31R(.’H      | to cluster    | various   | lar~e      | datasets,   |       | All the       | times |
|     |     |     |     |           |            |          |     | are presented |               | in second | in         | tlus paper. | Three | synthetir     |       |
|     |     |     |     |           |            |          |     | datasets,     | one           | for each  | pattern,   |             | were  | used. Table   | 3     |
|     |     |     |     |           |            |          |     | presents      | the generator |           | settings   | for         | them. | The weight,wi |       |
|     |     |     |     |           |            |          |     | average       | diameters     | of        | the actual | clusters5   |       | , ~)<l,.t are | also  |
|     |     |     |     | Euclidian |            | distance |     | inclucie[i    | in the        | table.    |            |             |       |               |       |
to the closest seed Fig. 6 visualizes the actual clusters of 1)S1hy plotting
is larger than twire a cluster as a circle whose center is the centroid, radius
|     |     |     |     | of   | the radius | of  |     |                |          |         |            |        |        |                 |     |
| --- | --- | --- | --- | ---- | ---------- | --- | --- | -------------- | -------- | ------- | ---------- | ------ | ------ | --------------- | --- |
|     |     |     |     |      |            |     |     | is the cluster | ra[iius, |         | anti label | is the | number | of points       | in  |
|     |     |     |     | that | cluster    |     | u   |                |          |         |            |        |        |                 |     |
|     |     |     |     |      |            |     |     | the cluster,   | The      | BIR(”’H | clusters   |        | of DS  | 1 are presented |     |
Table 2: BIR(?H Parameters and Tlimr Dclault Wue.s in Fig. 7. We observe that the BIR(’H clusters are
|     |     |     |     |     |     |     |     | very similar | to  | the actual | clusters |     | in terms | of location, |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | ---------- | -------- | --- | -------- | ------------ | --- |
dataset. Whereas when the ordered option is selected, number of points, and raclii. The maximal and average
the data points of a cluster are placed together, the difference between the centroids of an actual cluster
c-lusters are placed in the order they are generated, and and its corresponding BIRCH cluster are 0.17 and 0.07
| the noise | is placed |     | at the end. |     |     |     |     |               |     |        |     |        |      |          |         |
| --------- | --------- | --- | ----------- | --- | --- | --- | --- | ------------- | --- | ------ | --- | ------ | ---- | -------- | ------- |
|           |           |     |             |     |     |     |     | respectively. | The | number | of  | points | in a | BIll(”~H | cluster |
6.3 Parameters and Default Setting is no more t$han 4°i1 ciifferentl from the correspon(ling
t?IR.(~H is capable of working under various settings. actual cluster. The radii of the BIR(~H clusters (ranging
Table 2 lists the parameters of BIRCH, their effecting from 1.25 to 1.40 with an average of 1.32) are close to,
scopes and their default, values. [Jnless specified those of the actual rlusters (1.41). Note that all the
explicitly otherwise. an experiments is conducted under BIR(~H raclii are smaller than the actual radii. This
this default setting. is because BIRCH assigns the “outsiders” of an art, ual
flf was selected to he 80 kbytes whirh is about 5% clusters to a proper BIRCH cluster. Similar conclusions
of the dataset size in the base workload used in our can be reached by analyzing the visual presentations
experiments. Since clisk space (R) is just used for of DS2 and 13S3 (but omitted here clue to the lack of
| outliers, | we  | assume | that, R | < M | and | set R | = 20% |     |     |     |     |     |     |     |     |
| --------- | --- | ------ | ------- | --- | --- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
space).
of M. The experiments on the effects of the 5 distance As summarized in Table 4, it took BIRC’H less than
metrics in the first 3 phases[ZR,L9.5] indicate that (1) 50 seconds (on an HP 9000/720 workstation) to cluster
| using D3 | in  | Phases | I and | 2 results | in a | much | higher |         |             |     |      |           |     |         |        |
| -------- | --- | ------ | ----- | --------- | ---- | ---- | ------ | ------- | ----------- | --- | ---- | --------- | --- | ------- | ------ |
|          |     |        |       |           |      |      |        | 100,000 | data points | of  | each | dataset,. | The | pattern | of the |
en(ling threshold, and hence produces clusters of poorer dataset haci almost no impact on the clustering time,
quality; (2) however, there is no distinctive performance Table 4 also presents the performance results for three
difference among the ot,hms. So we decided to choose additional ciatasets – DS 10, DS20 and DS30 – which
L)2 as default. Following Statistics tradition, we choose correspon(i to DS 1, DS2 anti 13S3, respectively exceljtl
| “weighted | average | diameter” |     | (denoted | as  | D) as | quality |          |           |     |        |           |     |                  |     |
| --------- | ------- | --------- | --- | -------- | --- | ----- | ------- | -------- | --------- | --- | ------ | --------- | --- | ---------------- | --- |
|           |         |           |     |          |     |       |         | that the | parameter | o   | of the | generator | is  | set, to ordered, |     |
measurement. The smaller ~ is, the het,ter the quality As demomtrateci in Table 4, changing the order of the
is. The threshold is defined as the threshold for cluster data points had almost no impact, on the performance
| diameter | as default. |     |     |     |     |     |     | of BIRCH. |     |     |     |     |     |     |     |
| -------- | ----------- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
In Phase 1, the initial threshold is default to O. Based 6.5 Sensitivity to Parameters
on a study of how page size affects perforrnance[ZR, L95], We studied the sensitivity of BIRCH’S performance to
we selected P = 1024. The delay-split, option is on the change of the values of some parameters. Due to
so that given a threshold, the CF tree accepts more the lack of space, here we can only present some major
data points and reaches a higher capacity. The outlier- conclusions (for details, see [ZRL95]).
| handling        | option        | is on | so that   | BIRL’H      | can remove |       | outliers |           |          |            |           |              |     |                     |         |
| --------------- | ------------- | ----- | --------- | ----------- | ---------- | ----- | -------- | --------- | -------- | ---------- | --------- | ------------ | --- | ------------------- | ------- |
|                 |               |       |           |             |            |       |          | 5From     | now on,  | we         | refer to  | the clusters |     | generated           | by tile |
| and concentrate |               | on    | the dense | places      | with       | the   | given    |           |          |            |           |              |     |                     |         |
|                 |               |       |           |             |            |       |          | generator | as the   | “actual    | clusters” | whereas      | the | clusters identifimi |         |
|                 |               |       | For       | simplicity, | we         | treat | a leaf   | BIRCH     |          | CH         |           |              |     |                     |         |
| amount          | of resources. |       |           |             |            |       |          | by        | as “t?I~ | clusters”. |           |              |     |                     |         |
111

Dataset C;enerator Setting L)act [
DSI grid, f<’ = 100, nt = 71h = 1000, r~ = rh = 42, kg = 4, r-n = 070,0 = randomized 2.00
DS2 sine, K = 100)711 = 7Lh = 1000, r~ = r~ = ~~, n. = 4, rn = 070, 0 = ra7ut07nized 2.00
DX3 random, A“ = 100, nt = O,n}, = 2000, rt = O,rh = 4, T-n= rn = 0~0, o = randomized 4.18
Table 3: Datasets Userl as Base Workload
Initial threshold: (1) BIRCH’S performance is Dataset Time D Dataset Time L)
stable as long as the initial threshold is not excessively DS1 47.1 1.87 DS1O 47’.4 1.87
high wrt. the dataset. (2) To = 0.0 works well with a DS2 47.5 1.99 DS20 46.4 1.99
DS3 49.5 3.39 DS30 48.4 3.26
little extra running time. (3) If a user does know a good
To, then she/he can be rewarded by saving up to 10%
Table 44: BIRCH Performance on Base Workload wrt.
of the time.
Time, ~ arid171put Order
Page Size P: In Phase 1, smaller (larger) P
tends to ciecrease (increase) the running time, requires Dataset Time D Dat=.=-.-~
”.
I
II
I T.;,.>me D I
higher (lower) ending threshold, produces less (more) DS1 &39.5 2.11 DS’10 II 1525.7 I 1(3.75
11 I
but “coarser (finer)” leaf entries, and hence degrades DS’2 777.5 2.56 DS20 1405.8 179.;:3
(improves) the quality. However with the refinement in DS3 15’20.2 3.36 D%30 2:390.5 6.9:3
Phase 4, the experiments suggest that from P = 256
Table 5: CLA RANS Performance on Base Workload
to 4096 , although the qualities at the end of Phase 3
wrt. Ttme, ~ and Input Order
are different, the final qualities after the refinement are
almost the same.
time is not exactly linear wrt. N. However the running
Outlier Options: BIRCH was tested on “noisy’) time for the first 3 phases is again confirmed to grow
datasets with all the outlier options on, and o~. The linearly wrt. N consistently for all three patterns.
results show that with all the outlier options on, BIRCH
is not slower but faster, and at the same time, its quality 6.7 Comparison of BIRCH and CLARANS
is much better. In this experiment we compare the performance of
Memory Size: In Phase 1, as memory size (or the C’LARAN,$ and BIRCH on the base workload. First
maximal tree size) increases, the running time increases CLARANS assumes that the memory is enough for
because of processing a larger tree per rebuilt, but only holding the whole clataset, so it needs much more
slightly because it is clone in memory; (2) more but memory than BIRCH does. In order for CLARAN,S
finer subclusters are generated to feed the next phase, to stop after an acceptable running time, we set its
and hence results in better quality; (3) the inaccuracy 7naxnezghbor value to be the larger of 50 (instead of
caused hy insufficient memory can be compensated 250) and 1.2.5~o of K(N-K), but no more than 100 (newly
to some extent by Phase 4 refinements. In another enforced upper limit recommended by Ng). Its numlocal
word, BIRCH can tradeoff between memory and time value is still 2. Fig. 8 visualizes the CLA RANS’ clusters
to achieve similar final quality. for DS 1. Comparing them with the actual clusters for
DSI we can observe that: (1) The pattern of the location
6.6 Time Scalability
of the cluster centers is distorted. (2) The number of
Two distinct ways of increasing the clataset size are used
data points in a CLARAN,S cluster can be as many as
to test the scalability of BIRCH.
57% different from the number in the actual cluster. (3)
Increasing the Number of Points per Cluster:
The radii of CLA RANS clusters varies largely from 1.15
For each of DS 1, DS2 and DS3, we create a range of
to 1.94 with an average of 1.44 (larger than those of the
clatasets by keeping the generator settings the same
actual clusters, 1.41). Similar behaviors can be observed
except for changing 711and nk to change 71,and hence
the visualization of CLARAN,S clusters for DS2 and DS3
N. The running time for the first 3 phases, as well as
(but omitted here due to the lack of space).
for all 4 phases are plotted against the dataset size N
Table 5 summarizes the performance of (’LA RAN,$.
in Fig. 4. Both of them are shown to grow linearly wrt.
For all three datasets of the base workload, (1) (TLARAN,5’
N consistently for all three patterns.
is at least 15 times slower than BIRCH, and is sensi-
Increasing the Number of Clwst ers: For each
tive to the pattern of the dataset. (2) The ~ value
of DS 1, DS2 and DS3, we create a range of datasets
for the C’LA RANS clusters is much larger than that for
by keeping the generator settings the same except for
the BIRCH clusters. (3) The results for DS 10, DS20,
changing 1{ to change N. The running time for the first
and DS30 show that when the data points are ordered,
3 phases, as well as for all 4 phases are plotted against
the time and quality of CLARAN,S degrade dramati-
the dataset size N in Fig. 5. Since both N and K are
cally. In conclusion, for the base workload, BIRCH uses
growing, and Phase 4’s complexity is now 0(1< *N) (can
much less memory, hut is faster, more accurate, and less
be improved to be almost linear in the future), the total
order-sensitive compared with C’LARAN,S,
112

|     |     |     | DS1   | : Phase    | 1-3 | ~           |     |     |     |     |     |     |     |     |
| --- | --- | --- | ----- | ---------- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | D     | S2: P base | 1-3 | -----I+---- |     |     |     |     |     |     |     |     |
|     |     |     |       |            |     | ......=     | .   |     |     |     |     |     |     |     |
|     |     |     | DS3:  | Phase      | 1-3 |             |     |     |     |     |     |     |     |     |
|     |     |     | DS1   | : Phase    | 1-4 | G           |     |     |     |     |     |     |     |     |
|     |     |     | D S2: | Phase      | 1-4 | ---------   |     |     |     |     |     |     |     |     |
|     |     |     | DS3:  | Phase      | 1-4 | ------      | 1   |     |     |     |     |     |     |     |
m
|     |     |     |     |     |     |     |     |     | 0   | 1.        | 20             |     |       | 4,  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------------- | --- | ----- | --- |
|     |     |     |     |     |     |     |     |     |     |           | ActualC’lustmx |     | D,5’1 |     |
|     |     |     |     |     |     |     |     |     |     | Figure 6: |                | of  |       |     |
I
0 L
|     |        | 0   |             | 100000 |             | 200000  |     |     |     |     |     |     |     |     |
| --- | ------ | --- | ----------- | ------ | ----------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |        |     | Number      | of     | Tuples      | (N)     |     |     |     |     |     |     |     |     |
|     | Figure | 4:  | scalability | wrt.   | I?tcreasing | ILL,n}, |     |     |     |     |     |     |     |     |
~~
|     |     |     | DS1  | : Phase    | 1-3  | —             |      |     |     |           |                |     |      |     |
| --- | --- | --- | ---- | ---------- | ---- | ------------- | ---- | --- | --- | --------- | -------------- | --- | ---- | --- |
|     | 140 |     | D    | S2: P base | i -3 | -----u----    | ,.;2 |     |     |           |                |     |      |     |
|     |     |     | DS3: | Phase      | 1-3  | ------=-.;j’\ |      |     |     |           |                |     |      |     |
|     |     |     | DS1  | : Phase    | 1-4  | - ok,”        |      |     |     |           |                |     |      |     |
|     | 120 |     | D    | S2: P base | 1-4  | ----7~~       |      |     |     |           |                |     |      |     |
|     |     |     | DS3: | Phase      | 1-4  | --;~,.J’-     |      |     |     |           |                |     |      |     |
|     |     |     |      |            |      |               |      |     |     | Figure 7: | BIRCH Clusters | of  | DiSl |     |
,#’
100
| g   |     |     |     |     |     | ,/.’” |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
./
| ~   |     |     |     |     | ,/  |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
80
| .i—% |     |     |     |     | /   |     |     |     |     |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
l--
|     | c   |     |     |     | ,/  |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
z 60
40
20
I
0
|          |             | o         |               | 100000        |          | 200000  |        |          |           |                  |                  |            |             |          |
| -------- | ----------- | --------- | ------------- | ------------- | -------- | ------- | ------ | -------- | --------- | ---------------- | ---------------- | ---------- | ----------- | -------- |
|          |             |           | Number        | of            | Tuples   | (N)     |        |          |           |                  |                  |            |             |          |
|          |             |           |               |               |          |         |        | and      | weighting | NI R and         | VIS values       | equally.   | We obtained |          |
|          |             | Figure 5: | ,Scalabilit~j | 7mt.          | [nmmsing | K       |        |          |           |                  |                  |            |             |          |
|          |             |           |               |               |          |         |        | 5 clust, | ers       | that, correspond | to (1) very      | bright     | part        | of sl{y, |
|          |             |           |               |               |          |         |        | (2)      | ordinary  | part of          | sky, (3) clouds, | (4) sunlit | leaves      | (5)      |
| 6.8      | Application |           | to            | Real Datasets |          |         |        |          |           |                  |                  |            |             |          |
|          |             |           |               |               |          |         |        | tree     | branches  | and shadows      | on the           | trees.     | This step   | took     |
| BIli(”’H |             | has been  | used          | for filtering | real     | images, | Fig. 9 |          |           |                  |                  |            |             |          |
284 seconds.
| are | two similar | images |     | of trees with | a partly | cloudy | sky |     |     |     |     |     |     |     |
| --- | ----------- | ------ | --- | ------------- | -------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
as the background, taken in two different wavelengt 11s. However the branches and shadows were too sinlilar
The top one is in near-infrared hand (NIR), and the to be distinguished from each other, although we COU1[l
bottom one is in visible wavelength band (VIS). Each separate them from the other [’luster categories, So we
| image | contains | 512xl1324 |     | pixels, | and each | pixel | act)llally |        |     |          |             |               |     |         |
| ----- | -------- | --------- | --- | ------- | -------- | ----- | ---------- | ------ | --- | -------- | ----------- | ------------- | --- | ------- |
|       |          |           |     |         |          |       |            | pulled | out | the part | of the data | corresponding |     | to (.5) |
has a pair of brightness values corresponding to NIR, and (146707 2-d tuples) and used BIRCH again, But, this
VIS. Soil scientists receive hundreds of such image pairs time, (1) NIR was weighted 10 times heavier than VIS
and try to first filter the trees from the background, because we observed that branches and shadows were
and then filter the trees into sunlit leaves, shadows and easier to tell apart from the NIR image than from the
| branches |     | for statistical |     | analysis. |     |     |     |     |        |           |            |     |                 |     |
| -------- | --- | --------------- | --- | --------- | --- | --- | --- | --- | ------ | --------- | ---------- | --- | --------------- | --- |
|          |     |                 |     |           |     |     |     | VIS | image; | (2) BIRCH | ended with | a   | finer threshold |     |
We applied BIRCH to the (NIR,, VIS) value pairs for because it processed a smaller dataset wit,h the same
all pixels in an image (512X 1024 2-d tuples) hy using 400 amount, of memory. The two clusters corresponding to
khytes of rnernory (about 5%, of the dataset size) and 80 branches and shadows were obtained with 71 secon(ls,
khytes of disk space (about 20% of the rnernory size), Fig. 10 shows the parts of image that, correspond to
113

|     |     |     |     |     |     |     | studying    |                | (1) more     | reasonable      |                | ways              | of increasing  |            | the     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | -------------- | ------------ | --------------- | -------------- | ----------------- | -------------- | ---------- | ------- |
|     |     |     |     |     |     |     | threshold   |                | dynamically, |                 | (2) the        | dynamic           | adjustment     |            | of      |
|     |     |     |     |     |     |     | outlier     | criteria,      |              | (3) more        | accurate       |                   | quality        | rneasure-  |         |
|     |     |     |     |     |     |     | me.nts,     | and            | (4)          | data parameters |                | that              | are            | good       | indica- |
|     |     |     |     |     |     |     | tors        | of how         | well         | BIRCH           | is likely      | to                | perform.       | We         | will    |
|     |     |     |     |     |     |     | explore     | BIRCH’S        |              | architecture    |                | for opportunities |                |            | of par- |
|     |     |     |     |     |     |     | allel       | executions     |              | as well         | as interactive |                   | learnings.     |            | As an   |
|     |     |     |     |     |     |     | incremental |                | algorithrr,  |                 | BIRCH          | will              | be able        | to read    | data    |
|     |     |     |     |     |     |     | directly    | from           | a            | tape drive,     | or             | from              | network        | by         | matchi- |
|     |     |     |     |     |     |     | ng          | its clustering |              | speed with      | the            | data              | reading        | speed.     | We      |
|     |     |     |     |     |     |     | will        | also study     | how          | to make         | use            | of                | the clustering |            | infor-  |
|     |     |     |     |     |     |     | mation      | obtained       |              | to help         | solve          | problems          | such           | as storage |         |
|     |     |     |     |     |     |     | or query    | optimization,  |              |                 | and data       | compression.      |                |            |         |
References
[CKS88]
|     |     |     |     |     |     |     |     | Peter      | (Ubeeseman, |            | James           | Kelly, | Matthew | Self,    | et al., |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ----------- | ---------- | --------------- | ------ | ------- | -------- | ------- |
|     |     |     |     |     |     |     |     | Auto Class | : A         | Bayesian   | (Ylassijlcation |        | SUstem, | Proc.    | of the  |
|     |     |     |     |     |     |     |     | 5tb Int’1  | Couf.       | on Machine | Learning,       |        | Morgan  | Kaufmau, | Jun.    |
1988.
|        |     |     |         |              |     |                            | [DH7:3]  | Richard     | Duda,     | and               | Peter    | E. Hart,    | Patter,L        | C/aSSijiCatiOn |         |
| ------ | --- | --- | ------- | ------------ | --- | -------------------------- | -------- | ----------- | --------- | ----------------- | -------- | ----------- | --------------- | -------------- | ------- |
| Figure | 9:  | The | ima~ges | taken in NIR | and | VIS                        |          |             |           |                   |          |             |                 |                |         |
|        |     |     |         |              |     |                            |          | and Sce7ze  | Analysis, | Wiley,            | 1973.    |             |                 |                |         |
|        |     |     |         |              |     |                            | [DJ80]   | f%.         | Dubes,    | and A.K.          | Jaiu,    | G’Imter-ing | Methodologies   |                | in      |
|        |     |     |         |              |     |                            |          | Ezplorator~ | Data      | Anczlgsis         | Advances |             | in (.~omputers, |                | Edited  |
|        |     |     |         |              |     |                            |          | by M.C.     | Yovits,   | Vol. 19,          | Academic | F’ress,     | New             | York,          | 19/30.  |
|        |     |     |         |              |     |                            | [EKX95a] | Martin      |           | Ester, Haus-Peter |          | Kriegel,    | aud             | Xiaowei        | Xu,     |
|        |     |     |         |              |     | ,. :h. ... d t .,. ,., =., |          |             |           |                   |          |             |                 |                |         |
|        |     |     |         |              |     | < ) , .. . . , ..          |          | A Database  |           | Interface         | for      | Clustering  | in              | Largr          | Spatial |
.... . . .
|        |     |            |         |          |     |         |          | Databases,       | Proc.        | of 1st            | Int’1      | Conf. ou        | Kuowledge     | Discuvery       |        |
| ------ | --- | ---------- | ------- | -------- | --- | ------- | -------- | ---------------- | ------------ | ----------------- | ---------- | --------------- | ------------- | --------------- | ------ |
|        |     |            |         |          |     |         |          | aud Data         | Miuiug,      | 1995.             |            |                 |               |                 |        |
|        |     |            |         |          |     |         | [EKX95b] |                  | Martiu       | Ester, Haus-Peter |            | Kriegel,        | and           | Xiaowei         | Xu,    |
|        |     |            |         |          |     |         |          | Knowl?dgr        | Discouery    |                   | in Larg?   | Spatial         | f)atabas~s:   | Focusing        |        |
|        |     |            |         |          |     |         |          | Techniques       | for          | Eficie~~t         | ~lass      | Identijlcation, |               | Proc.           | of 4tb |
|        |     |            |         |          |     |         |          | Int’1 Symposium  |              | ou                | Large      | Spatial         | Databases,    | F)ortlaud,      |        |
|        |     |            |         |          |     |         |          | Maine,           | I-J.S.A.,    | 1995.             |            |                 |               |                 |        |
|        |     |            |         |          |     |         | [Fis87]  | Douglas          | H.           | Fisher,           | Knowledge  | Acqui~itzon     |               | uia lncr.mew    |        |
|        |     |            |         |          |     |         |          | f~l (Tone-rptual |              | Clustering,       | Machine    |                 | Leamiug,      | 2(2),           | 1987   |
|        |     |            |         |          |     |         | [Fis95]  | Douglas          | H.           | Fisher,           | Iterative  | (optimization   |               | and Simp[ijica- |        |
|        |     |            |         |          |     |         |          | tion of          | Hierarchical | Clusterings,      |            | Technical       | Report        | (}S-95-01,      |        |
|        |     |            |         |          |     |         |          | Dept.            | of Computer  | Science,          | Vanderbilt |                 | IIuiver-sity, | Nashville,      |        |
| Figure | 10: | The sunlit | leaves, | branches | and | shadows |          | TN :372:35.      |              |                   |            |                 |               |                 |        |
|        |     |            |         |          |     |         | [(1(+92] | A.               | Gersbo       | and R.            | Gray,      |                 |               |                 |        |
|        |     |            |         |          |     |         |          |                  |              |                   |            | Vector          | quantization  | and             | signal |
sunlit leaves, tree branches and shadows on the trees, compression, Boston, Ma.: Kluwer Academic F)ublishers,
| obtained | hy clustering |     | using | BIRCH. | Visually, | we can |        | 1992.   |          |     |     |          |     |     |     |
| -------- | ------------- | --- | ----- | ------ | --------- | ------ | ------ | ------- | -------- | --- | --- | -------- | --- | --- | --- |
|          |               |     |       |        |           |        | [KR90] | Leonard | Kaufman, |     | and | Peter J. |     |     |     |
see that, it is asatisfactory filteringof the original image Rousseeuw, Finding
|     |     |     |     |     |     |     |     |     |     | I?Ltroductio?L |     | toCluster |     |     | Wiley |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | --------- | --- | --- | ----- |
according to the user’s intention. Groups in Data - An Analysis,
|           |                 |            |        |          |           |           |         | Series         | in F’robability | and        | Mathematical |           | Statistics,       | 1990.        |       |
| --------- | --------------- | ---------- | ------ | -------- | --------- | --------- | ------- | -------------- | --------------- | ---------- | ------------ | --------- | ----------------- | ------------ | ----- |
|           |                 |            |        |          |           |           | [Leb87] | Michael        | Lebowitz,       |            | Experiment.  |           |                   |              |       |
| 7 Summary |                 | and        | Future | Research |           |           |         |                |                 |            |              |           | with Incremental  |              | (;on- |
|           |                 |            |        |          |           |           |         |                |                 |            |              | Machine   | Learuiug,         | 1987.        |       |
|           |                 |            |        |          |           |           |         | cept Formation |                 | : UNIMEM,  |              |           |                   |              |       |
| BIli(~H   | is a clustering |            | method | for very | large     | datasets. |         |                |                 |            |              |           |                   |              |       |
|           |                 |            |        |          |           |           | [Lee81] | R.C.T.Lee,     |                 | Clustering | anrdgsis     | ar,d      | its application., |              | A+    |
| It makes  | a large         | clustering |        | problem  | tractable | hy con-   |         |                |                 |            |              |           |                   |              |       |
|           |                 |            |        |          |           |           |         | vauces         | in Information  |            | Systems      | ,Science, | Edited            | by J,T.Toum, |       |
centrating on densely occupied portions, and using a Vol. 8, pp. 169-292, Plenum Press, New York, 1981,
compact summary. It utilizes measurements that cap- [Mur8:3] F. Murtagb, A Survey of Recent Advance. in Hierarchi-
ture the natural closeness of data. These measurements cal 6’lustering A~g Orithms, The (.;omputer Jourmal, 1%3:3.
|              |        |             |                 |               |           |              | [NH94]   | Raymond     |         | T. Ng and | Jiawei      | Hau,       | Ejficimt | and          | ,Eflectiue |
| ------------ | ------ | ----------- | --------------- | ------------- | --------- | ------------ | -------- | ----------- | ------- | --------- | ----------- | ---------- | -------- | ------------ | ---------- |
| can he       | stored | and updated |                 | incrementally |           | in a height- |          |             |         |           |             |            |          |              |            |
|              |        |             |                 |               |           |              |          | (blustering | Methods |           | for Spatial | Data       | Mining,  | F’roe,       | of         |
| balanced     | tree.  | BIRCH       | can             | work with     | any given | amount       |          |             |         |           |             |            |          |              |            |
|              |        |             |                 |               |           |              |          | VLDB,       | 1994.   |           |             |            |          |              |            |
| of rnernory, | and    | the         | 1/() complexity | is            | a little  | more than    |          |             |         |           |             |            |          |              |            |
|              |        |             |                 |               |           |              | [01s9:3] | Clark       | F.      | L31son,   | Parallel    | Algorithms | for      | Hierarchical |            |
one scan of data. Experimentally, BIRCH is shown to C’[usteri?~g, Technical Report, Computer Scieuce Divisiou,
perform very well on several large datasetsj and is signif- IIuiv. of California at Berkeley, Dec.,1993.
icantly superior to CLARANS in terms of quality, speed [ZRL95] Tian Zbau.g, Ragbu Rau)akt-ishuan, aud Mirou Liv,,y,
BIRCH:
and order-sensitivity. An Ef%cient Data Clustering Mtthod for VPTV
Proper parameter setting is important to BIR(;H’s Largr Databases, Technical Report, Computer Scieuces
diiciency. In the near future, we will concentrate on Dept., (Juiv. of Wisconsiu-Madison, 1995,
114