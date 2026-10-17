Topic Modeling in Embedding Spaces
AdjiB.Dieng FranciscoJ.R.Ruiz∗ DavidM.Blei
ColumbiaUniversity DeepMind ColumbiaUniversity
NewYork,NY,USA London,UK NewYork,NY,USA
abd2141@columbia.edu franrruiz@google.com david.blei@columbia.edu
Abstract proportions provide a low-dimensional represen-
tation of each document. LDA can be fit to large
Topic modeling analyzes documents to learn datasets of text by using variational inference
meaningfulpatternsofwords.However,exist- andstochasticoptimization(Hoffmanetal.,2010,
ing topic models fail to learn interpretable 2013).
topics when working with large and heavy- LDA is a powerful model and it is widely used.
tailed vocabularies. To this end, we develop However, it suffers from a pervasive technical
theembeddedtopicmodel(ETM),agenerative problem—itfailsinthefaceoflargevocabularies.
model of documents that marries traditional Practitionersmustseverelyprunetheirvocabular-
topicmodelswithwordembeddings.Morespe- ies in order to fit good topic models—namely,
cifically, the ETM models each word with a those that are both predictive and interpretable.
categorical distribution whose natural param- This is typically done by removing the most and
eter is the inner product between the word’s least frequent words. On large collections, this
embedding and an embedding of its assigned pruning may remove important terms and limit
topic. To fit the ETM, we develop an effi- the scope of the models. The problem of topic
cient amortized variational inference algo- modeling with large vocabularies has yet to be
rithm. The ETM discovers interpretable topics addressedintheresearchliterature.
evenwithlargevocabulariesthatincluderare Inparallelwithtopicmodelingcametheideaof
words and stop words. It outperforms exist- wordembeddings.Researchin word embeddings
ingdocumentmodels,suchaslatentDirichlet beginswith the neurallanguagemodelof Bengio
allocation, in terms of both topic quality and et al. (2003), published in the same year and
predictiveperformance. journal as Blei et al. (2003). Word embeddings
eschewthe‘‘one-hot’’representationofwords—a
vocabulary-length vector of zeros with a single
1 Introduction one—to learn a distributed representation, one
where words with similar meanings are close in
Topic models are statistical tools for discovering
alower-dimensionalvectorspace(Rumelhartand
the hidden semantic structure in a collection of
Abrahamson, 1973; Bengio et al., 2006). As for
documents (Blei et al., 2003; Blei, 2012). Topic
topic models, researchers scaled up embedding
models and their extensions have been applied
methodstolargedatasets(Mikolovetal.,2013a,b;
to many fields, such as marketing, sociology,
Penningtonetal.,2014;LevyandGoldberg,2014;
political science, and the digital humanities.
MnihandKavukcuoglu,2013).Wordembeddings
Boyd-Graberetal.(2017)provideareview.
havebeenextendedanddevelopedinmanyways.
Most topic models build on latent Dirichlet They have become crucial in many applications
allocation (LDA) (Blei et al., 2003). LDA is a ofnaturallanguageprocessing(Maasetal.,2011;
hierarchical probabilistic model that represents Li and Yang, 2018), and they have also been
each topic as a distribution over terms and re- extended to datasets beyond text (Rudolph et al.,
presents each document as a mixture of the top- 2016).
ics. When fit to a collection of documents, the
In this paper, we develop the embedded topic
topics summarize their contents, and the topic
model (ETM), a document model that marries LDA
∗Work done while at Columbia University and the and word embeddings. The ETM enjoys the good
UniversityofCambridge. propertiesoftopicmodelsandthegoodproperties
439
TransactionsoftheAssociationforComputationalLinguistics,vol.8,pp.439–453,2020.https://doi.org/10.1162/tacla00325
ActionEditor:DougDowney.Submissionbatch:2/2020;Revisionbatch:5/2020;Published7/2020.
(cid:13)c 2020AssociationforComputationalLinguistics.DistributedunderaCC-BY4.0license.

|     |     |     |     |     |     |     | Figure2:AtopicaboutChristianity |     | foundbytheETM |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------- | --- | ------------- | --- |
Figure1:Ratiooftheheld-outperplexityonadocument
completiontask andthetopiccoherenceasafunction on The New York Times. The topic is a point in the
wordembeddingspace.
| of the vocabulary |              | size        | for the             | ETM | and LDA       | on the  |     |     |     |     |
| ----------------- | ------------ | ----------- | ------------------- | --- | ------------- | ------- | --- | --- | --- | --- |
| 20NewsGroup       |              | corpus.     | The perplexity      |     | is normalized |         |     |     |     |     |
| by the size       | of the       | vocabulary. | While               | the | performance   |         |     |     |     |     |
| of LDA            | deteriorates | for         | large vocabularies, |     |               | the ETM |     |     |     |     |
maintainsgoodperformance.
ofwordembeddings.Asatopicmodel,itdiscovers
| an interpretable |                 | latent | semantic       | structure |          | of the  |     |     |     |     |
| ---------------- | --------------- | ------ | -------------- | --------- | -------- | ------- | --- | --- | --- | --- |
| documents;       | as              | a word | embedding      |           | model,   | it pro- |     |     |     |     |
| vides a          | low-dimensional |        | representation |           |          | of the  |     |     |     |     |
| meaning          | of words.       | The    |                | robustly  | accommo- |         |     |     |     |     |
ETM
| dates large | vocabularies |     | and | the long | tail | of lan- |     |     |     |     |
| ----------- | ------------ | --- | --- | -------- | ---- | ------- | --- | --- | --- | --- |
guagedata.
Figure3:TopicsaboutsportsfoundbytheETMonThe
| Figure | 1 illustrates |     | the advantages. |     | This | figure |                 |            |            |             |
| ------ | ------------- | --- | --------------- | --- | ---- | ------ | --------------- | ---------- | ---------- | ----------- |
|        |               |     |                 |     |      |        | New York Times. | Each topic | is a point | in the word |
showstheratiobetweentheperplexityonheld-out
embeddingspace.
documents(ameasureofpredictiveperformance)
| andthe | topic | coherence(ameasureofthe |     |     |     | quality |     |     |     |     |
| ------ | ----- | ----------------------- | --- | --- | --- | ------- | --- | --- | --- | --- |
of the topics), as a function of the size of the topic’s embedding and each term’s embedding.
|             |      |            |     |      |            |     | Figures2and | 3showtopicsfroma300-topicETM |     |     |
| ----------- | ---- | ---------- | --- | ---- | ---------- | --- | ----------- | ---------------------------- | --- | --- |
| vocabulary. | (The | perplexity | has | been | normalized |     |             |                              |     |     |
by the vocabulary size.) This is for a corpus of of The New York Times. The figures show each
11.2K articles from the 20NewsGroup and for topic’s embedding and its closest words; these
100 topics. The red line is LDA; its performance topicsareaboutChristianityandsports.
deterioratesasthevocabularysizeincreases—the
Representingtopicsaspointsintheembedding
predictive performance and the quality of the space allows the to be robust to the presence
ETM
topicsgetworse.ThebluelineistheETM;itmain- of stop words, unlike most topic models. When
tains good performance, even as the vocabulary stop words are included in the vocabulary, the
| sizebecomelarge. |     |     |     |     |     |     | assigns | topics to the | corresponding | area of |
| ---------------- | --- | --- | --- | --- | --- | --- | ------- | ------------- | ------------- | ------- |
ETM
Like LDA, the is a generative probabilistic the embedding space (we demonstrate this in
ETM
| model: | Each documentis |     | a mixture |     | of topics | and | Section6). |     |     |     |
| ------ | --------------- | --- | --------- | --- | --------- | --- | ---------- | --- | --- | --- |
each observed word is assigned to a particular As for most topic models, the posterior of the
topic.Incontrastto LDA,theper-topicconditional topic proportions is intractable to compute. We
probability of a term has a log-linear form that derive an efficient algorithm for approximating
involves a low-dimensional representation of the the posterior with variational inference (Jordan
vocabulary.Eachtermisrepresentedbyanembed- et al., 1999; Hoffman et al., 2013; Blei et al.,
ding and each topic is a point in that embedding 2017) and additionally use amortized inference
space. The topic’s distribution over terms is pro- to efficiently approximate the topic proportions
portionaltotheexponentiatedinnerproductofthe (KingmaandWelling,2014;Rezendeetal.,2014).
440

The resulting algorithm fits the ETM to large ment variables in the ETM are part of a larger
corpora with large vocabularies. This algorithm probabilistictopicmodel.
caneitherusepreviouslyfittedwordembeddings, One of the goals in developing the ETM is to
orfitthemjointly with the restoftheparameters. incorporate word similarity into the topic model,
(Inparticular,Figures1to3weremadeusingthe andthereispreviousresearchthatsharesthisgoal.
version of the ETM that uses pre-fitted skip-gram These methods either modify the topic priors
wordembeddings.) (Petterson et al., 2010; Zhao et al., 2017b; Shi
WecomparedtheperformanceoftheETMtoLDA, et al., 2017; Zhao et al., 2017a) or the topic
the neural variational document model (NVDM) assignmentpriors(Xieetal.,2015).Forexample,
(Miao et al., 2016), and PRODLDA (Srivastava and Pettersonetal.(2010)useawordsimilaritygraph
Sutton,2017).1TheNVDMisaformofmultinomial (as given by a thesaurus) to bias LDA towards
matrix factorization and PRODLDA is a modern assigning similar words to similar topics. As
version of LDA that uses a product of experts anotherexample,Xie etal.(2015)modeltheper-
to model the distribution over words. We also word topic assignments of LDA using a Markov
compare to a document model that combines random field to account for both the topic pro-
PRODLDAwithpre-fittedwordembeddings.TheETM portions and the topic assignments of similar
yieldsbetterpredictiveperformance,asmeasured words. These methods use word similarity as a
byheld-outlog-likelihoodonadocumentcomple- type of ‘‘side information’’ about language; in
tiontask(Wallachetal.,2009b).Italsodiscovers contrast,theETMdirectlymodelsthesimilarity(via
more meaningful topics, as measured by topic embeddings)initsgenerativeprocessofwords.
coherence (Mimno et al., 2011) and topic diver- However, a more closely related set of works
sity. The latter is a metric we introduce in this directly combine topic modeling and word
paperthat, together with topic coherence,gives a embeddings. One common strategy is to convert
better indication of the quality of the topics. The the discrete text into continuous observations
ETMisespeciallyrobusttolargevocabularies. of embeddings, and then adapt LDA to generate
real-valued data (Das et al., 2015; Xun et al.,
2016; Batmanghelich et al., 2016; Xun et al.,
2 Related Work
2017). With this strategy, topics are Gaussian
distributions with latent means and covariances,
Thisworkdevelopsanewtopicmodelthatextends
andthelikelihoodovertheembeddingsismodeled
LDA. LDA has been extended in many ways, and
withaGaussian(Dasetal.,2015)oraVon-Mises
topic modeling has becomea subfield ofits own.
Fisher distribution (Batmanghelich et al., 2016).
For a review, see Blei (2012) and Boyd-Graber
The ETM differs from these approaches in that
etal.(2017).
it is a model of categorical data, one that goes
A broadersetof related works are neuraltopic
through the embeddings matrix. Thus it does not
models. These mainly focus on improving topic
require pre-fitted embeddings and, indeed, can
modelinginferencethroughdeepneuralnetworks
learnembeddingsaspartofits inferenceprocess.
(Srivastava and Sutton, 2017; Card et al., 2017;
The ETM also differs from these approaches in
Congetal.,2017;Zhangetal.,2018).Specifically,
that it is amenable to large datasets with large
these methods reduce the dimension of the text
vocabularies.
datathroughamortizedinferenceandthevariatio-
There are few other ways of combining LDA
nal auto-encoder (Kingma and Welling, 2014;
and embeddings. Nguyen et al. (2015) mix the
Rezendeetal.,2014).Toperforminferenceinthe
likelihooddefinedbyLDAwithalog-linearmodel
ETM,wealsoavailourselvesofamortizedinference
that uses pre-fitted word embeddings; Bunk and
methods(GershmanandGoodman,2014).
Krestel (2018) randomly replace words drawn
As a document model, the ETM also relates to
from a topic with their embeddings drawn from
works that learn per-documentrepresentations as
a Gaussian; Xu et al. (2018) adopt a geometric
part of an embedding model (Le and Mikolov,
perspective, using Wasserstein distances to learn
2014; Moody, 2016; Miao et al., 2016; Li et al.,
topics and word embeddings jointly; and Keya
2016). In contrast to these works, the docu-
etal.(2019)proposetheneuralembeddingalloca-
tion(NEA),whichhasasimilargenerativeprocess
1Code is available at https://github.com/
adjidieng/ETM. totheETMbutisfitusingapre-fittedLDAmodelas
441

a target distribution. Because it requires LDA, the TheembeddingmatrixρisaL×V matrixwhose
NEAsuffersfromthesamelimitationasLDA.These columns contain the embedding representations
models often lack scalability with respect to the of the vocabulary, ρ ∈ RL. The vector α is
v dn
vocabularysizeandarefitusingGibbssampling, thecontextembedding.Thecontextembeddingis
limiting theirscalabilitytolargecorpora. thesumofthecontextembeddingvectors(α for
v
eachwordv)ofthewordssurroundingw .
dn
3 Background
4 The Embedded Topic Model
The ETM builds on two main ideas, LDA and word
embeddings. Consider a corpus of D documents, The ETM is a topic model that uses embedding
where the vocabulary contains V distinct terms. representations of both words and topics. It
Let w ∈ {1,...,V} denote the nth word in the contains two notions of latent dimension. First,
dn
dth document. it embeds the vocabulary in an L-dimensional
space. These embeddings are similar in spirit to
Latent Dirichlet Allocation. LDA is a probabi- classical word embeddings. Second, it represents
listic generative model of documents (Blei et al.,
eachdocumentintermsofK latenttopics.
2003).Itposits K topics β , eachofwhichis a
1:K In traditional topic modeling, each topic is a
distributionoverthevocabulary.LDAassumeseach
full distribution over the vocabulary. In the ETM,
documentcomesfroma mixture of topics, where however,the kth topic is a vector α ∈ RL in the
k
the topics are shared across the corpus and the
embeddingspace.Wecallα atopicembedding—
k
mixtureproportionsareuniqueforeachdocument.
itisadistributedrepresentationofthekth topicin
The generative process for each document is the
thesemanticspaceofwords.
following:
Initsgenerativeprocess,theETMusesthetopic
embedding to form a per-topic distribution over
1. Drawtopicproportionθ ∼ Dirichlet(α ).
d θ
the vocabulary. Specifically, the ETM uses a log-
2. Foreachwordninthedocument: linear model that takes the inner product of the
wordembeddingmatrixandthetopicembedding.
(a) Drawtopicassignmentz ∼ Cat(θ ).
dn d
With this form, the ETM assigns high probability
(b) Drawwordw ∼ Cat(β ).
dn z dn toawordvintopickbymeasuringtheagreement
Here, Cat(·) denotes the categorical distribu- between the word’s embedding and the topic’s
tion.LDAplacesaDirichletprioronthetopics, embedding.
Denote the L×V word embedding matrix by
β ∼ Dirichlet(α )fork = 1,...,K. ρ; the column ρ is the embedding of term v.
k β v
Under the ETM, the generative process of the dth
The concentration parameters α and α of the
β θ documentisthefollowing:
Dirichlet distributions are fixed model hyperpa-
1. Drawtopicproportionsθ ∼ LN(0,I).
rameters. d
2. Foreachwordninthedocument:
WordEmbeddings. Wordembeddingsprovide
modelsoflanguagethatusevectorrepresentations a. Drawtopicassignmentz ∼ Cat(θ ).
dn d
of words (Rumelhart and Abrahamson, 1973; b. Draw the word w ∼ softmax(ρ⊤
dn
Bengio et al., 2003). The word representations
α ).
z
dn
are fitted to relate to meaning, in that words with
In Step 1, LN(·) denotes the logistic-normal
similar meanings will have representations that
distribution (Aitchison and Shen, 1980; Blei and
are close. (In embeddings, the ‘‘meaning’’ of a
Lafferty,2007);ittransformsastandardGaussian
wordcomes fromthe contextsin which it is used
random variable to the simplex. A draw θ from
[Harris,1954].) d
thisdistributionisobtainedas
We focus on the continuous bag-of-words
(CBOW) variant of word embeddings (Mikolov
δ ∼ N(0,I); θ = softmax(δ ). (2)
d d d
et al., 2013b). In CBOW, the likelihood of each
(WereplacedtheDirichletwiththelogisticnormal
wordw is
dn
to easily use reparameterization in the inference
w ∼ softmax(ρ⊤α ). (1) algorithm;seeSection5.)
dn dn
442

Steps1and2aarestandardfortopicmodeling: topic proportions,which we write in terms of the
They represent documents as distributions over untransformedproportionsδ inEq.2,
d
topics and draw a topic assignment for each
observed word. Step 2b is different; it uses the N
d
embeddingsofthe vocabularyρandthe assigned p(w |α,ρ) = p(δ ) p(w |δ ,α,ρ)dδ .
d d dn d d
Z
topic embeddingα z to drawthe observedword n Y =1
dn
(4)
fromtheassignedtopic,asgivenbyz .
dn
The topic distribution in Step 2b mirrors the
CBOWlikelihoodinEq.1.RecallCBOWusesthe The conditional distribution p(w dn |δ d ,α,ρ) of
surroundingwordstoformthecontextvectorα . each word marginalizes out the topic assignment
dn
Incontrast,theETMusesthetopicembeddingα z z dn ,
dn
asthecontextvector,wheretheassignedtopicz
dn
is drawn from the per-documentvariable θ . The K
d
ETM draws its words from a document context, p(w dn |δ d ,α,ρ) = θ dk β k,w dn . (5)
X
ratherthanfromawindowofsurroundingwords. k=1
The ETM likelihood uses a matrix of word
Here,θ denotesthe(transformed)topicpropor-
embeddingsρ, a representationof the vocabulary dk
tions (Eq. 2) and β denotes a traditional
in a lower dimensional space. In practice, it can k,v
‘‘topic,’’ that is, a distribution over words,
either rely on previously fitted embeddings or
induced by the word embeddings ρ and the topic
learn themas partofits overallfitting procedure.
embeddingα ,
WhentheETMlearnstheembeddingsaspartofthe k
fitting procedure, it simultaneously finds topics
andanembeddingspace. β kv = softmax(ρ⊤α k ) v . (6)
(cid:12)
When the ETM uses previously fitted embed- (cid:12)
dings,itlearnsthetopicsofacorpusinaparticular Eqs.4,5,6fleshoutthelikelihoodinEq.3.
embedding space. This strategy is particularly
useful when there are words in the embedding
Variational Inference. We sidestep the intrac-
that are not used in the corpus. The ETM can
table integral in Eq. eq:integral with variational
hypothesize how those words fit in to the topics
inference (Jordan et al., 1999; Blei et al., 2017).
because it can calculate ρ⊤α even for words v
v k Variational inference optimizes a sum of per-
thatdonotappearinthecorpus.
document bounds on the log of the marginal
likelihoodofEq.4.
5 Inference and Estimation To begin, posit a family of distributions of the
untransformed topic proportions q(δ ; w ,ν).
We are given a corpus of documents {w ,..., d d
1 Thisfamilyofdistributionsisparameterizedbyν.
w }, where the dth document w is a collection
D d We use amortized inference, where q(δ ; w ,ν)
of N d words. How do we fit the ETM to this (calledavariationaldistribution)depend d son d both
corpus?
the document w and shared parameters ν. In
d
particular,q(δ ; w ,ν)isaGaussianwhosemean
d d
The Marginal Likelihood. The parameters of andvariancecomefroman‘‘inferencenetwork,’’
the ETM are the word embeddings ρ 1:V and the aneuralnetworkparameterizedbyν(Kingmaand
topic embeddings α 1:K ; each α k is a point in Welling, 2014). The inference network ingests
thewordembeddingspace.Wemaximizethelog a bag-of-words representation of the document
marginallikelihoodofthedocuments, w and outputs the mean and covariance of δ .
d d
(To accommodate documents of varying length,
D
we form the input of the inference network by
L(α,ρ) = logp(w |α,ρ). (3)
d
normalizingthebag-of-wordrepresentationofthe
X
d=1
documentbythenumberofwordsN .)
d
The problem is that the marginal likelihood We use this family of distributions to bound
ofeachdocument—p(w |α,ρ)—isintractableto the log of the marginal likelihood in Eq. 4. The
d
compute. It involves a difficult integral over the boundiscalledtheevidencelowerbound(ELBO)
443

andisafunctionofthemodelparametersandthe Algorithm1TopicmodelingwiththeETM
variationalparameters, Initializemodelandvariationalparameters
foriterationi=1,2,...do
D N d Computeβ =softmax(ρ⊤α )foreachtopick
L(α,ρ,ν) = Eq[logp(w |δ ,ρ,α)] k k
nd d ChooseaminibatchBofdocuments
XX
d=1 n=1 foreachdocumentdinBdo
D Getnormalizedbag-of-wordrepresentat.x
d
− KL(q(δ d ;w d ,ν) || p(δ d )). (7) Computeµ d =NN(x d ; ν µ )
X d=1 ComputeΣ d =NN(x d ; ν Σ )
The first term of the ELBO (Eq. 7) encourages Sampleθ d usingEq.9andθ d =softmax(δ d )
variational distributions q(δ ; w ,ν) that place foreachwordinthedocumentdo
d d Computep(w |θ ,ρ,α)=θ⊤β
mass on topic proportions δ that explain the dn d d ·,wdn
d endfor
observed words and the second term encourages
endfor
q(δ d ; w d ,ν) to be close to the prior p(δ d ). EstimatetheELBOusingEq.10andEq.11
Maximizing the ELBO with respect to the model TakegradientsoftheELBOviabackpropagation
parameters (α,ρ) is equivalent to maximizing Updatemodelparametersα (ρifnecessary)
1:K
the expected complete log-likelihood, d log Updatevariationalparameters(ν µ ,ν Σ )
p(δ ,w |α,ρ). P endfor
d d
The ELBO in Eq. 7 is intractable because the
expectation is intractable. However,we can form Given that the prior p(δ ) and q(δ ;w ,ν) are
d d d
aMonteCarloapproximationoftheELBO, both Gaussians, the KL admits a closed-form
expression,
1 D N d S
L˜(α,ρ,ν) = logp(w |δ(s),ρ,α)
S X d=1 X n=1 X s=1 nd d KL(q(δ d ;w d ,ν) || p(δ d )) =
D 1 tr(Σ )+µ⊤µ −logdet(Σ )−K . (11)
− KL(q(δ ;w ,ν) || p(δ )), (8) 2 d d d d
d d d (cid:8) (cid:9)
X
d=1
We optimize the stochastic ELBO in Equation 10
where δ(s) ∼ q(δ ;w ,ν) for s = 1...S. To with respect to both the model parameters (α,ρ)
d d d
form an unbiased estimator of the ELBO and its and the variational parameters ν. We set the
gradients, we use the reparameterization trick learningratewith Adam(Kingma andBa, 2015).
when sampling the unnormalized proportions TheprocedureisshowninAlgorithm1,wherewe
δ(1),...,δ(S) (KingmaandWelling,2014;Titsias set the number of Monte Carlo samples S = 1
d d
andLa´zaro-Gredilla,2014;Rezendeetal.,2014). and the notation NN(x; ν) represents a neural
Thatis,wesampleδ(s) fromq(δ ;w ,ν)as networkwithinputxandparametersν.
d d d
ǫ(s)
∼
N(0,I)andδ(s)
= µ +Σ
1 2ǫ(s),
(9)
d d d d d 6 Empirical Study
where µ and Σ arethe mean and covarianceof
d d
q(δ ;w ,ν)respectively,whichdependimplicitly
WestudytheperformanceoftheETMandcompare
d d
ittootherunsuperviseddocumentmodels.Agood
on ν andw via the inferencenetwork.Weusea
d
document model should provide both coherent
diagonalcovariancematrixΣ .
d
patterns of language and an accurate distribution
We also use data subsampling to handle large
of words, so we measure performance in terms
collections of documents (Hoffman et al., 2013).
of both predictive accuracy and topic interpret-
Denote by B a minibatch of documents. Then
ability. Wemeasureaccuracywith log-likelihood
the approximation of the ELBO using data sub-
onadocumentcompletion task(Rosen-Zvietal.,
samplingis
2004; Wallach et al., 2009b); we measure topic
D N d S interpretability as a blend of topic coherenceand
L˜(α,ρ,ν) = logp(w |δ(s),ρ,α)
|B| nd d diversity.Wefindthat,oftheinterpretablemodels,
XXX
d∈Bn=1 s=1
theETMis the onethatprovidesbetterpredictions
D
− KL(q(δ ;w ,ν) || p(δ )). andtopics.
d d d
|B|
X In a separate analysis (Section 6.1), we study
d∈B
(10) the robustness of each method in the presence
444

Dataset MinimumDF #TokensTrain #TokensValid #TokensTest Vocabulary
|     |              |     | 100   |     | 604.9K | 5,998 |     | 399.6K |     | 3,102   |     |     |
| --- | ------------ | --- | ----- | --- | ------ | ----- | --- | ------ | --- | ------- | --- | --- |
|     |              |     | 30    |     | 778.0K | 7,231 |     | 512.5K |     | 8,496   |     |     |
|     | 20Newsgroups |     | 10    |     | 880.3K | 6,769 |     | 578.8K |     | 18,625  |     |     |
|     |              |     | 5     |     | 922.3K | 8,494 |     | 605.9K |     | 29,461  |     |     |
|     |              |     | 2     |     | 966.3K | 8,600 |     | 622.9K |     | 52,258  |     |     |
|     |              |     | 5,000 |     | 226.9M | 13.4M |     | 26.8M  |     | 9,842   |     |     |
|     |              |     | 200   |     | 270.1M | 15.9M |     | 31.8M  |     | 55,627  |     |     |
|     | NewYorkTimes |     | 100   |     | 272.3M | 16.0M |     | 32.1M  |     | 74,095  |     |     |
|     |              |     | 30    |     | 274.8M | 16.1M |     | 32.3M  |     | 124,725 |     |     |
|     |              |     | 10    |     | 276.0M | 16.1M |     | 32.5M  |     | 212,237 |     |     |
Table1:Statisticsofthedifferentcorporastudied.DFdenotesdocumentfrequency,Kdenotes
athousand,andMdenotesamillion.
of stop words. Standard topic models fail in We consider latent Dirichlet allocation (LDA)
this regime—becausestop wordsappearin many (Blei et al., 2003), a standard topic model that
documents, every learned topic includes some posits Dirichlet priors for the topics β and topic
k
stop words, leading to poor topic interpretability. proportionsθ d .(Wesetthepriorhyperparameters
In contrast, the is able to use the information to 1.) It is a conditionally conjugate model,
ETM
fromthewordembeddingstoprovideinterpretable amenabletovariationalinferencewithcoordinate
| topics. |     |     |     |     |     | ascent.  | We consider | LDA   | because | it         | is the    | most |
| ------- | --- | --- | --- | --- | --- | -------- | ----------- | ----- | ------- | ---------- | --------- | ---- |
|         |     |     |     |     |     | commonly | used        | topic | model,  | and it has | a similar |      |
Corpora. We study the 20Newsgroups corpus generativeprocessastheETM.
| and | the New | York Times | corpus; | the | statistics of |         |          |     |        |             |     |       |
| --- | ------- | ---------- | ------- | --- | ------------- | ------- | -------- | --- | ------ | ----------- | --- | ----- |
|     |         |            |         |     |               | We also | consider | the | neural | variational |     | docu- |
bothcorporaaresummarizedinTable1.
mentmodel(NVDM)(Miaoetal.,2016).TheNVDM
The 20Newsgroup corpus is a collection of is a multinomial factor model of documents; it
newsgroup posts. We preprocess the corpus posits the likelihood w ∼ softmax (β⊤θ ),
|     |     |     |     |     |     |     |     |     | dn  |     |     | d   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
N(0,I
by filtering stop words, words with document where the K-dimensional vector θ ∼ )
|           |     |            |                 |     |         |                   |     |           |     | d     |      | K     |
| --------- | --- | ---------- | --------------- | --- | ------- | ----------------- | --- | --------- | --- | ----- | ---- | ----- |
| frequency |     | above 70%, | and tokenizing. |     | To form |                   |     |           |     |       |      |       |
|           |     |            |                 |     |         | is a per-document |     | variable, |     | and β | is a | real- |
the vocabulary, we keep all words that appear in valued matrix of size K × V. The uses
NVDM
morethanacertainnumberofdocuments,andwe a per-document real-valued latent vector θ
d
varythethresholdfrom100(asmallervocabulary,
toaverageovertheembeddingmatrixβinthelogit
whereV =3,102)to2(alargervocabulary,where space. Like the ETM, the uses amortized
NVDM
V = 52,258). After preprocessing, we further variational inference to jointly learn the approxi-
| remove | one-word   | documents | from       | the  | validation |                |     |          |          |                |     |     |
| ------ | ---------- | --------- | ---------- | ---- | ---------- | -------------- | --- | -------- | -------- | -------------- | --- | --- |
|        |            |           |            |      |            | mate posterior |     | over the | document | representation |     |     |
| and    | test sets. | We split  | the corpus | into | a training |                |     |          |          |                |     |     |
θ d andthemodelparameterβ.
set of 11,260 documents, a test set of 7,532 is not interpretable as a topic model;
NVDM
documents,andavalidationsetof100documents. its latent variables are unconstrained. We study
The New York Times corpus is a larger collec- a more interpretable variant of the NVDM which
| tion | of news | articles. | It contains | more | than 1.8 |            |     |           |              |     |           |     |
| ---- | ------- | --------- | ----------- | ---- | -------- | ---------- | --- | --------- | ------------ | --- | --------- | --- |
|      |         |           |             |      |          | constrains | θ d | to lie in | the simplex, |     | replacing | its |
million articles, spanning the years 1987–2007. Gaussian prior with a logistic normal (Aitchison
We follow the same preprocessing steps as for and Shen, 1980). (This can be thought of as a
| 20Newsgroups. |     | We form | versions | of  | this corpus |                  |     |        |                 |     |     |      |
| ------------- | --- | ------- | -------- | --- | ----------- | ---------------- | --- | ------ | --------------- | --- | --- | ---- |
|               |     |         |          |     |             | semi-nonnegative |     | matrix | factorization.) |     | We  | call |
with vocabularies ranging from V = 9,842 to thisdocumentmodel∆-NVDM.
V = 212,237. After preprocessing, we use 85% We also consider PRODLDA (Srivastava and
|                                             |     |     |     |     |     | Sutton,     | 2017). | It posits                  | the | likelihood | w   | ∼   |
| ------------------------------------------- | --- | --- | --- | --- | --- | ----------- | ------ | -------------------------- | --- | ---------- | --- | --- |
| ofthedocumentsfortraining,10%fortesting,and |     |     |     |     |     |             |        |                            |     |            |     | dn  |
| 5%forvalidation.                            |     |     |     |     |     | softmax(β⊤θ |        | )wherethetopicproportionsθ |     |            |     | are |
|                                             |     |     |     |     |     |             | d      |                            |     |            |     | d   |
fromthesimplex.ContrarytoLDA,thetopic-matrix
| Models. |     | We compare | the performance |     | of the |     |     |     |     |     |     |     |
| ------- | --- | ---------- | --------------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
β sunconstrained.
ETMagainstseveraldocumentmodels.Webriefly shares the generative model with
PRODLDA
describeeachbelow. ∆-NVDM but it is fit differently. PRODLDA uses
445

|         |              | Skip-gramembeddings |     |       |             |       |     | ETMembeddings |        |     |            |     |
| ------- | ------------ | ------------------- | --- | ----- | ----------- | ----- | --- | ------------- | ------ | --- | ---------- | --- |
| love    | family       |                     |     | woman | politics    | love  |     | family        | woman  |     | politics   |     |
| loved   | families     |                     |     | man   | political   | joy   |     | children      | girl   |     | political  |     |
| passion | grandparents |                     |     | girl  | religion    | loves |     | son           | boy    |     | politician |     |
| loves   | mother       |                     |     | boy   | politicking | loved |     | mother        | mother |     | ideology   |     |
affection friends teenager ideology passion father daughter speeches
adore relatives person partisanship wonderful wife pregnant ideological
|           |         | NVDMembeddings |     |          |             |       |     | ∆-NVDMembeddings |          |     |             |     |
| --------- | ------- | -------------- | --- | -------- | ----------- | ----- | --- | ---------------- | -------- | --- | ----------- | --- |
| love      | family  |                |     | woman    | politics    | love  |     | family           | woman    |     | politics    |     |
| loves     | sons    |                |     | girl     | political   | miss  |     | home             | life     |     | political   |     |
| passion   | life    |                |     | women    | politician  | young |     | father           | marriage |     | faith       |     |
| wonderful | brother |                |     | man      | politicians | born  |     | son              | women    |     | marriage    |     |
| joy       | son     |                |     | pregnant | politically | dream |     | day              | read     |     | politicians |     |
beautiful lived boyfriend democratic younger mrs young election
PRODLDAembeddings
|     |     |     |     | love        | family    | woman     |     | politics    |     |     |     |     |
| --- | --- | --- | --- | ----------- | --------- | --------- | --- | ----------- | --- | --- | --- | --- |
|     |     |     |     | loves       | husband   | girl      |     | political   |     |     |     |     |
|     |     |     |     | affection   | wife      | boyfriend |     | politician  |     |     |     |     |
|     |     |     |     | sentimental | daughters | boy       |     | liberal     |     |     |     |     |
|     |     |     |     | dreams      | sister    | teenager  |     | politicians |     |     |     |     |
|     |     |     |     | laugh       | friends   | ager      |     | ideological |     |     |     |     |
Table 2: Word embeddings learned by all document models (and skip-gram) on the New York Times
withvocabularysize118,363.
amortized variational inference with batch (2013):thedelayis10andtheforgettingfactoris
| normalization |     | (Ioffe | and | Szegedy, | 2015) and | 0.85. |     |     |     |     |     |     |
| ------------- | --- | ------ | --- | -------- | --------- | ----- | --- | --- | --- | --- | --- | --- |
dropout(Srivastavaetal.,2014). Within SVI, LDA enjoys coordinate ascent
|          |     |          |            |     |            | variational | updates; |     | we use | five inner | steps | to  |
| -------- | --- | -------- | ---------- | --- | ---------- | ----------- | -------- | --- | ------ | ---------- | ----- | --- |
| Finally, | we  | consider | a document |     | model that |             |          |     |        |            |       |     |
optimizethelocalvariables.Fortheothermodels,
| combines | PRODLDA | with | pre-fitted | word | embed- |     |     |     |     |     |     |     |
| -------- | ------- | ---- | ---------- | ---- | ------ | --- | --- | --- | --- | --- | --- | --- |
dings ρ, by using the likelihood w ∼ softmax weuseamortizedinferenceoverthelocalvariables
dn
(ρ⊤θ ). We call this document model PRODLDA- θ d . We use 3-layer inference networks and we
d
|            |     |        |     |                |      | set the | local | learning | rate to | 0.002. | We use | ℓ   |
| ---------- | --- | ------ | --- | -------------- | ---- | ------- | ----- | -------- | ------- | ------ | ------ | --- |
| PWE, where | PWE | stands |     | for Pre-fitted | Word |         |       |          |         |        |        | 2   |
Embeddings. regularization on the variational parameters (the
weightdecayparameteris1.2×10−6).
| We study | two | variants | of  | the ETM, | one where |     |     |     |     |     |     |     |
| -------- | --- | -------- | --- | -------- | --------- | --- | --- | --- | --- | --- | --- | --- |
thewordembeddingsarepre-fittedandonewhere
|             |         |         |      |            |             | Qualitative |     | Results. | We    | first examine |     | the |
| ----------- | ------- | ------- | ---- | ---------- | ----------- | ----------- | --- | -------- | ----- | ------------- | --- | --- |
| they are    | learned | jointly | with | the        | rest of the |             |     |          |       |               |     |     |
|             |         |         |      |            |             | embeddings. |     | The ETM, | NVDM, | ∆-NVDM,       |     | and |
| parameters. | The     | variant | with | pre-fitted | embed-      |             |     |          |       |               |     |     |
PRODLDAalllearnwordembeddings.Weillustrate
dingsiscalledtheETM-PWE.
|     |     |     |     |     |     | them by | fixing | a set | of  | terms and | showing |     |
| --- | --- | --- | --- | --- | --- | ------- | ------ | ----- | --- | --------- | ------- | --- |
For PRODLDA-PWE and the ETM-PWE, we first the closest words in the embedding space (as
| obtain | the word | embeddings |     | (Mikolov | et al., |          |     |        |            |     |             |     |
| ------ | -------- | ---------- | --- | -------- | ------- | -------- | --- | ------ | ---------- | --- | ----------- | --- |
|        |          |            |     |          |         | measured | by  | cosine | distance). | For | comparison, |     |
2013b)bytrainingskip-gramoneachcorpus.(We
wealsoillustratewordembeddingslearnedbythe
| reusethesameembeddingsacrosstheexperiments |     |     |     |     |     | skip-grammodel. |     |     |     |     |     |     |
| ------------------------------------------ | --- | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- | --- |
withvaryingvocabularysizes.)
Table2illustratestheembeddingsofthediffer-
entmodels.Allthemethodsprovideinterpretable
Algorithm Settings. Given a corpus, each embeddings—words with related meanings are
model comes with an approximate posterior close to each other. The ETM, the NVDM, and
inference problem. We use variational inference PRODLDAlearnembeddingsthataresimilartothose
for all of the models and employ SVI (Hoffman from the skip-gram. The embeddings of ∆-NVDM
et al., 2013) to speed up the optimization. The are different; the simplex constraint on the local
minibatch size is 1,000 documents. For LDA, we variable and the inference procedure change the
setthelearningrateassuggestedbyHoffmanetal. natureoftheembeddings.
446

LDA
| time | year    | officials  | mr        | city     | percent | state      |
| ---- | ------- | ---------- | --------- | -------- | ------- | ---------- |
| day  | million | public     | president | building | million | republican |
| back | money   | department | bush      | street   | company | party      |
| good | pay     | report     | white     | park     | year    | bill       |
| long | tax     | state      | clinton   | house    | billion | mr         |
NVDM
| scholars     | japan   | gansler       | spratt   | assn  | ridership    | pryce     |
| ------------ | ------- | ------------- | -------- | ----- | ------------ | --------- |
| gingrich     | tokyo   | wellstone     | tabitha  | assoc | mtv          | mickens   |
| funds        | pacific | mccain        | mccorkle | qtr   | straphangers | mckechnie |
| institutions | europe  | shalikashvili | cheetos  | yr    | freierman    | mfume     |
| endowment    | zealand | coached       | vols     | nyse  | riders       | filkins   |
∆-NVDM
| concerto | servings    | nato      | innings   | treas    | patients   | democrats   |
| -------- | ----------- | --------- | --------- | -------- | ---------- | ----------- |
| solos    | tablespoons | soviet    | scored    | yr       | doctors    | republicans |
| sonata   | tablespoon  | iraqi     | inning    | qtr      | medicare   | republican  |
| melodies | preheat     | gorbachev | shutout   | outst    | dr         | senate      |
| soloist  | minced      | arab      | scoreless | telerate | physicians | dole        |
PRODLDA
| temptation | grasp  | electron | played | amato    | briefly  | giant    |
| ---------- | ------ | -------- | ------ | -------- | -------- | -------- |
| repressed  | unruly | nuclei   | lou    | model    | precious | boarding |
| drowsy     | choke  | macal    | greg   | delaware | serving  | bundle   |
| addiction  | drowsy | trained  | bobby  | morita   | set      | distance |
| conquering | drift  | mediaone | steve  | dual     | virgin   | foray    |
PRODLDA-PWE
mercies cheesecloth scoreless chapels distinguishable floured gillers
lockbox overcook floured magnolias cocktails impartiality lacerated
| pharm | strainer | hitless | asea | punishable | knead | polshek |
| ----- | -------- | ------- | ---- | ---------- | ----- | ------- |
shims kirberger asterisk bogeyed checkpoints refrigerate decimated
| cp  | browned | knead | birdie | disobeying | tablespoons | inhuman |
| --- | ------- | ----- | ------ | ---------- | ----------- | ------- |
ETM-PWE
| music   | republican | yankees  | game   | wine        | court   | company |
| ------- | ---------- | -------- | ------ | ----------- | ------- | ------- |
| dance   | bush       | game     | points | restaurant  | judge   | million |
| songs   | campaign   | baseball | season | food        | case    | stock   |
| opera   | senator    | season   | team   | dishes      | justice | shares  |
| concert | democrats  | mets     | play   | restaurants | trial   | billion |
ETM
| game   | music | united     | wine       | company   | yankees  | art    |
| ------ | ----- | ---------- | ---------- | --------- | -------- | ------ |
| team   | mr    | israel     | food       | stock     | game     | museum |
| season | dance | government | sauce      | million   | baseball | show   |
| coach  | opera | israeli    | minutes    | companies | mets     | work   |
| play   | band  | mr         | restaurant | billion   | season   | artist |
Table 3: Top five words of seven most used topics from different document models on 1.8M
documentsoftheNewYorkTimescorpuswithvocabularysize212,237andK = 300topics.
Wenextlookatthelearnedtopics.Table3dis- interpretable topics. The rest of the models do
plays the seven most used topics for all methods, not provide interpretable topics; their matrices β
as given by the average of the topic proportions are unconstrained and thus are not interpretable
θ . and both variants of the provide as distributions over the vocabulary that mix to
| d LDA |     | ETM |     |     |     |     |
| ----- | --- | --- | --- | --- | --- | --- |
447

Figure 4: Interpretability as measured by the exponentiated topic quality (the higher the better) vs. predictive
performanceasmeasuredbylog-likelihoodondocumentcompletion(thehigherthebetter)onthe20NewsGroup
dataset. Both interpretabilityand predictivepowermetrics arenormalizedbysubtracting themeanand dividing
by the standard deviation across models. Better models are on the top right corner. Overall, the ETM is a better
topicmodel.
form documents. ∆-NVDM also suffers from this occur in the same documents. In other words,
effect although it is less apparent (see, e.g., the the most likely words in a coherent topic should
fifthlistedtopicfor∆-NVDM). havehigh mutual information. Documentmodels
withhighertopiccoherencearemoreinterpretable
| Quantitative |     | Results. |     | We next | study | the |     |     |     |     |     |     |     |
| ------------ | --- | -------- | --- | ------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
topicmodels.
| models | quantitatively. |         | We         | measure | the         | quality |            |     |           |      |          |     |         |
| ------ | --------------- | ------- | ---------- | ------- | ----------- | ------- | ---------- | --- | --------- | ---- | -------- | --- | ------- |
|        |                 |         |            |         |             |         | We combine |     | coherence | with | a second |     | metric, |
| of the | topics          | and the | predictive |         | performance | of      |            |     |           |      |          |     |         |
topicdiversity.Wedefinetopicdiversitytobethe
themodel.Wefoundthatamongthemodelswith
percentageofuniquewordsinthetop25wordsof
| interpretable |     | topics, | the | provides |     | the best |     |     |     |     |     |     |     |
| ------------- | --- | ------- | --- | -------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
ETM
alltopics.Diversitycloseto0indicatesredundant
predictions.
|          |         |           |         |           |            |     | topics; | diversity | close | to 1 indicates |     | more | varied |
| -------- | ------- | --------- | ------- | --------- | ---------- | --- | ------- | --------- | ----- | -------------- | --- | ---- | ------ |
| We       | measure | topic     | quality | by        | blending   | two |         |           |       |                |     |      |        |
| metrics: | topic   | coherence |         | and topic | diversity. |     | topics. |           |       |                |     |      |        |
Topic coherence is a quantitative measure of the We define the overall quality of a model’s
|     |     |     |     |     |     |     | topics as | the | product | of its | topic | diversity | and |
| --- | --- | --- | --- | --- | --- | --- | --------- | --- | ------- | ------ | ----- | --------- | --- |
interpretabilityofatopic(Mimnoetal.,2011).Itis
topiccoherence.
| the average |     | pointwise | mutual | information |     | of two |     |     |     |     |     |     |     |
| ----------- | --- | --------- | ------ | ----------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
wordsdrawnrandomlyfromthesamedocument, A good topic model also provides a good
|     |     |        |           |             |     |     | distribution                              | of                               | language. | To       | measure | predictive   |     |
| --- | --- | ------ | --------- | ----------- | --- | --- | ----------------------------------------- | -------------------------------- | --------- | -------- | ------- | ------------ | --- |
|     |     | K      | 10        | 10          |     |     |                                           |                                  |           |          |         |              |     |
|     |     | 1 1    |           | f(w(k),w(k) |     |     | power,wecalculateloglikelihoodonadocument |                                  |           |          |         |              |     |
|     | TC= |        |           |             |     | ),  |                                           |                                  |           |          |         |              |     |
|     |     |        |           |             | i j |     |                                           |                                  |           |          |         |              |     |
|     |     | K X 45 | X         | X           |     |     | completion                                | task(Rosen-Zvietal.,2004;Wallach |           |          |         |              |     |
|     |     | k=1    | i=1 j=i+1 |             |     |     |                                           |                                  |           |          |         |              |     |
|     |     |        |           |             |     |     | etal., 2009b).We                          |                                  | divide    | eachtest |         | documentinto |     |
where{w(k),...,w(k) two sets of words. The first half is observed: it
}denotesthetop-10most
|        |            | 1         | 10  |           |             |     |         |                |     |             |        |       |          |
| ------ | ---------- | --------- | --- | --------- | ----------- | --- | ------- | -------------- | --- | ----------- | ------ | ----- | -------- |
|        |            |           |     |           |             |     | induces | a distribution |     | over topics | which, |       | in turn, |
| likely | words      | in topic  | k.  | We choose | f(·,·)      | as  |         |                |     |             |        |       |          |
|        |            |           |     |           |             |     | induces | a distribution |     | over the    | next   | words | in the   |
| the    | normalized | pointwise |     | mutual    | information |     |         |                |     |             |        |       |          |
document.Wethenevaluatethesecondhalfunder
(Bouma,2009;Lauetal.,2014),
|     |     |     |     |     |     |     | this distribution. |     | A good | document |     | model | should |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | ------ | -------- | --- | ----- | ------ |
P(wi,wj)
|     |     |     | log |     |     |     | provide | high | log-likelihood |     | on the | second | half. |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---- | -------------- | --- | ------ | ------ | ----- |
P(wi)P(wj)
|     | f(w | ,w ) | =   |     | .   |     | (For all | methods, | we  | approximate |     | the likelihood |     |
| --- | --- | ---- | --- | --- | --- | --- | -------- | -------- | --- | ----------- | --- | -------------- | --- |
i j
|     |     |     | −logP(w |     | i ,w j ) |     |            |                        |     |     |     |     |     |
| --- | --- | --- | ------- | --- | -------- | --- | ---------- | ---------------------- | --- | --- | --- | --- | --- |
|     |     |     |         |     |          |     | bysettingθ | tothevariationalmean.) |     |     |     |     |     |
d
Here,P(w ,w )istheprobabilityofwordsw and We study both corpora and with different vo-
|     | i   | j   |     |     |     | i   |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
w co-occurring in a document and P(w ) is the cabularies. Figures 4 and 5 show interpretability
| j   |     |     |     |     |     | i   |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
marginalprobabilityofwordw i .Weapproximate ofthetopicsasafunctionofpredictivepower.(To
theseprobabilitieswithempiricalcounts. ease visualization, we exponentiate topic quality
The idea behind topic coherence is that a andnormalizeallmetricsbysubtractingthemean
coherent topic will display words that tend to and dividing by the standard deviation across
448

Figure 5: Interpretability as measured by the exponentiated topic quality (the higher the better) vs. predictive
performanceasmeasuredbylog-likelihoodondocumentcompletion(thehigherthebetter)ontheNewYorkTimes
dataset. Both interpretabilityand predictivepowermetrics arenormalizedbysubtracting themeanand dividing
by the standard deviation across models. Better models are on the top right corner. Overall, the ETM is a better
topicmodel.
| methods.)The |     |     | bestmodels | areon | the | upperright |     |     |     |     | Quality |
| ------------ | --- | --- | ---------- | ----- | --- | ---------- | --- | --- | --- | --- | ------- |
|              |     |     |            |       |     |            |     |     | TC  | TD  |         |
corner.
|     |          |     |       |           |               |     | LDA    |     | 0.13 | 0.14 | 0.0182 |
| --- | -------- | --- | ----- | --------- | ------------- | --- | ------ | --- | ---- | ---- | ------ |
|     | predicts |     | worst | in almost | all settings. | On  |        |     |      |      |        |
| LDA |          |     |       |           |               |     | ∆-NVDM |     | 0.17 | 0.11 | 0.0187 |
the 20NewsGroups,the NVDM’s predictions are in PRODLDA-PWE 0.03 0.53 0.0159
|                                             |     |     |                  |     |     |       |         |     | 0.18 |      | 0.0396 |
| ------------------------------------------- | --- | --- | ---------------- | --- | --- | ----- | ------- | --- | ---- | ---- | ------ |
| generalbetterthanLDAbutworsethanfortheother |     |     |                  |     |     |       | ETM-PWE |     |      | 0.22 |        |
| methods;on                                  |     | the | NewYorkTimes,the |     |     | gives |         |     |      |      |        |
NVDM
|     |     |     |     |     |     |     | Table | 4: Topic | quality | on  | the New York |
| --- | --- | --- | --- | --- | --- | --- | ----- | -------- | ------- | --- | ------------ |
thebestpredictions.However,topicqualityforthe
Timesdatainthepresenceofstopwords.
| NVDM | is far | belowthe |     | other methods. | (Itdoes | not |     |     |     |     |     |
| ---- | ------ | -------- | --- | -------------- | ------- | --- | --- | --- | --- | --- | --- |
provide‘‘topics’’,soweassesstheinterpretability Topicqualityhereisgivenbytheproduct
ofitsβmatrix.)Inprediction,bothversionsofthe of topic coherence and topic diversity
(higherisbetter).TheETM-PWEisrobust
ETMareatleastasgoodasthesimplex-constrained
|         |     |      |              |      |          |        | to stop | words; | it achieves |     | similar topic |
| ------- | --- | ---- | ------------ | ---- | -------- | ------ | ------- | ------ | ----------- | --- | ------------- |
| ∆-NVDM. |     | More | importantly, | both | versions | of the |         |        |             |     |               |
outperform the PRODLDA-PWE; signaling the coherence than when there are no stop
ETM
words.
|     | provides | a   | better | way of | integrating | word |     |     |     |     |     |
| --- | -------- | --- | ------ | ------ | ----------- | ---- | --- | --- | --- | --- | --- |
ETM
embeddingsintoatopicmodel.
These figures show that, of the interpretable to cope with stop words (Griffiths et al., 2004;
| models,     |     | the   | provides | the           | best | predictive |                                             |     |     |     |     |
| ----------- | --- | ----- | -------- | ------------- | ---- | ---------- | ------------------------------------------- | --- | --- | --- | --- |
|             |     | ETM   |          |               |      |            | Chemuduguntaetal.,2006;Wallachetal.,2009a); |     |     |     |     |
| performance |     | while | keeping  | interpretable |      | topics.    |                                             |     |     |     |     |
ourgoalhereisnottoestablishcomparisonswith
Itisrobusttolargevocabularies. thesemethodsbuttoshowtheperformanceofthe
ETM-PWEinthepresenceofstopwords.
6.1 StopWords
|     |     |     |     |     |     |     | We fit | LDA, the | ∆-NVDM, | the | PRODLDA-PWE, |
| --- | --- | --- | --- | --- | --- | --- | ------ | -------- | ------- | --- | ------------ |
We now study a version of the New York Times and the ETM-PWE with K = 300 topics. (We do
|        |      |          |     |          |           |        | not report | the  | because | it  | does not provide |
| ------ | ---- | -------- | --- | -------- | --------- | ------ | ---------- | ---- | ------- | --- | ---------------- |
| corpus | that | includes |     | all stop | words. We | remove |            | NVDM |         |     |                  |
infrequent words to form a vocabulary of size interpretable topics.) Table 4 shows the topic
10,283. Our goal is to show that the ETM-PWE quality (the product of topic coherence and topic
providesinterpretabletopicseveninthepresence diversity). Overall, the ETM-PWE gives the best
ofstopwords,anotherregimewheretopicmodels performanceintermsoftopicquality.
typically fail. In particular, given that stop words While the has a few ‘‘stop topics’’ that
ETM
appear in many documents, traditional topic are specific for stop words (see, e.g., Figure 6),
models learn topics that contain stop words, ∆-NVDMandLDAhavestopwordsinalmostevery
regardless of the actual semantics of the topic. topic.(Thetopicsarenotdisplayedhereforspace
Thisleadstopoortopicinterpretability.Thereare constraints.) The reason is that stop words co-
extensions of topic models specifically designed occurinthesamedocumentsaseveryotherword;
449

References
JohnAitchisonandShirMingShen.1980.Logis-
|     |     |     |     |     |     |     | tic normal |     | distributions: |     | Some | properties | and |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | -------------- | --- | ---- | ---------- | --- |
uses.Biometrika,67(2):261–272.
KayhanBatmanghelich,ArdavanSaeedi,Karthik
|     |     |     |     |     |     |     | Narasimhan,              |     | and | Sam | Gershman. | 2016.         | Non-      |
| --- | --- | --- | --- | --- | --- | --- | ------------------------ | --- | --- | --- | --------- | ------------- | --------- |
|     |     |     |     |     |     |     | parametricsphericaltopic |     |     |     | modeling  |               | with word |
|     |     |     |     |     |     |     | embeddings.InAssociation |     |     |     | for       | Computational |           |
Linguistics,volume2016,page537.
|     |     |     |     |     |     |     | Yoshua   | Bengio, |           | Re´jean | Ducharme, |       | Pascal   |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------- | --------- | ------- | --------- | ----- | -------- |
|     |     |     |     |     |     |     | Vincent, | and     | Christian |         | Janvin.   | 2003. | A neural |
Figure 6: A topic containing stop words found by the probabilistic language model. Journal of Ma-
ETM-PWE on The New York Times. The ETM is robust chineLearningResearch,3:1137–1155.
eveninthepresenceofstopwords.
YoshuaBengio,HolgerSchwenk,Jean-Se´bastien
|     |     |     |     |     |     |     | Sene´cal, |     | Fre´deric | Morin, |     | and | Jean-Luc |
| --- | --- | --- | --- | --- | --- | --- | --------- | --- | --------- | ------ | --- | --- | -------- |
thereforetraditionaltopicmodelshavedifficulties
|     |     |     |     |     |     |     | Gauvain. | 2006, |     | Neural | probabilistic |     | language |
| --- | --- | --- | --- | --- | --- | --- | -------- | ----- | --- | ------ | ------------- | --- | -------- |
telling apart content words and stop words. The models.InInnovationsinMachineLearning.
| ETM-PWE | recognizes |     | the location |     | of stop | words |     |     |     |     |     |     |     |
| ------- | ---------- | --- | ------------ | --- | ------- | ----- | --- | --- | --- | --- | --- | --- | --- |
in the embedding space;its sets themoffon their David M. Blei. 2012. Probabilistic topic models.
CommunicationsoftheACM,55(4):77–84.
owntopic.
|     |     |     |     |     |     |     | David      | M. Blei, | Alp   | Kucukelbir, |     | and        | Jon D. |
| --- | --- | --- | --- | --- | --- | --- | ---------- | -------- | ----- | ----------- | --- | ---------- | ------ |
|     |     |     |     |     |     |     | McAuliffe. |          | 2017. | Variational |     | inference: | A re-  |
7 Conclusion
|     |     |     |     |     |     |     | view | for statisticians. |     |     | Journal | of the | American |
| --- | --- | --- | --- | --- | --- | --- | ---- | ------------------ | --- | --- | ------- | ------ | -------- |
WedevelopedtheETM,agenerativemodelofdoc- StatisticalAssociation,112(518):859–877.
| uments  | that marries |      | with   | word | embeddings. |         |            |         |       |       |              |     |         |
| ------- | ------------ | ---- | ------ | ---- | ----------- | ------- | ---------- | ------- | ----- | ----- | ------------ | --- | ------- |
|         |              |      | LDA    |      |             |         | David      | M. Blei | and   | Jon   | D. Lafferty. |     | 2007. A |
| The ETM | assumes      | that | topics | and  | words       | live in |            |         |       |       |              |     |         |
|         |              |      |        |      |             |         | correlated |         | topic | model | of Science.  | The | Annals  |
the same embedding space, and that words are ofAppliedStatistics,1(1):17–35.
| generated | from | a categorical |     | distribution |     | whose |     |     |     |     |     |     |     |
| --------- | ---- | ------------- | --- | ------------ | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
naturalparameteristheinnerproductoftheword David M. Blei, Andrew Y. Ng, and Michael I.
|            |        |               |           |      |            |          | Jordan.          | 2003. |         | Latent | Dirichlet |     | allocation. |
| ---------- | ------ | ------------- | --------- | ---- | ---------- | -------- | ---------------- | ----- | ------- | ------ | --------- | --- | ----------- |
| embeddings | and    | the           | embedding | of   | the        | assigned |                  |       |         |        |           |     |             |
| topic.     |        |               |           |      |            |          | Journal          | of    | Machine |        | Learning  |     | Research,   |
| The        | learns | interpretable |           | word | embeddings |          | 3(Jan):993–1022. |       |         |        |           |     |             |
ETM
| and topics, | even | in corporawith |     | large | vocabular- |     |        |        |       |     |            |             |     |
| ----------- | ---- | -------------- | --- | ----- | ---------- | --- | ------ | ------ | ----- | --- | ---------- | ----------- | --- |
|             |      |                |     |       |            |     | Gerlof | Bouma. | 2009. |     | Normalized | (pointwise) |     |
ies.WestudiedtheperformanceoftheETMagainst
mutualinformationincollocationextraction.In
several document models. The ETM learns both German Society for Computational Linguistics
| coherent | patterns | of  | language | and | an  | accurate |     |     |     |     |     |     |     |
| -------- | -------- | --- | -------- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
andLanguageTechnologyConference.
distributionofwords.
|     |     |     |     |     |     |     | Jordan | Boyd-Graber, |              | Yuening |     | Hu, and | David   |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------------ | ------------ | ------- | --- | ------- | ------- |
|     |     |     |     |     |     |     | Mimno. | 2017.        | Applications |         | of  | topic   | models. |
Acknowledgments
|                      |     |                   |           |                   |              |     | Foundations                |          | and      | Trends   |                    | in Information |        |
| -------------------- | --- | ----------------- | --------- | ----------------- | ------------ | --- | -------------------------- | -------- | -------- | -------- | ------------------ | -------------- | ------ |
| DB and               |     | AD are            | supported |                   | by           | ONR | Retrieval,11(2–3):143–296. |          |          |          |                    |                |        |
| N00014-17-1-2131,    |     |                   | ONR       | N00014-15-1-2209, |              |     |                            |          |          |          |                    |                |        |
|                      |     |                   |           |                   |              |     | Stefan                     | Bunk     | and Ralf | Krestel. |                    | 2018.          | WELDA: |
| NIH 1U01MH115727-01, |     |                   |           | NSF               | CCF-1740833, |     |                            |          |          |          |                    |                |        |
|                      |     |                   |           |                   |              |     | Enhancingtopic             |          |          | modelsby | incorporatinglocal |                |        |
| DARPA                | SD2 | FA8750-18-C-0130, |           |                   | Amazon,      |     |                            |          |          |          |                    |                |        |
|                      |     |                   |           |                   |              |     | word                       | context. | In       | ACM/IEEE | Joint              | Conference     |        |
NVIDIA,andtheSimonsFoundation.FRreceived
onDigitalLibraries.
| funding | from | the | EU’s | Horizon | 2020 | R&I |     |     |     |     |     |     |     |
| ------- | ---- | --- | ---- | ------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
programme under the Marie Skłodowska-Curie Dallas Card, Chenhao Tan, and Noah A. Smith.
grant agreement 706760. AD is supported by a 2017.Aneuralframeworkforgeneralizedtopic
GooglePhDFellowship.
models.InarXiv:1705.09296.
450

Chaitanya Chemudugunta, Padhraic Smyth, and allocation: Distributed representations of topic
Mark Steyvers. 2006. Modeling general and models.arXivpreprintarXiv:1909.04702.
| specific | aspects | of     | documents | with     | a   | probab- |          |           |     |            |     |               |       |
| -------- | ------- | ------ | --------- | -------- | --- | ------- | -------- | --------- | --- | ---------- | --- | ------------- | ----- |
|          |         |        |           |          |     |         | Diederik | P. Kingma | and | Jimmy      |     | L. Ba.        | 2015. |
| ilistic  | topic   | model. | In        | Advances | in  | Neural  |          |           |     |            |     |               |       |
|          |         |        |           |          |     |         | Adam:    | A method  | for | stochastic |     | optimization. |       |
InformationProcessingSystems.
|             |            |                      |       |         |               |     | In International |            | Conference  |          |          | on Learning |          |
| ----------- | ---------- | -------------------- | ----- | ------- | ------------- | --- | ---------------- | ---------- | ----------- | -------- | -------- | ----------- | -------- |
| Yulai Cong, | Bo         | C.                   | Chen, | Hongwei | Liu,          | and | Representations. |            |             |          |          |             |          |
| Mingyuan    | Zhou.      | 2017.                | Deep  | latent  | Dirichlet     |     |                  |            |             |          |          |             |          |
|             |            |                      |       |         |               |     | Diederik         | P. Kingma  | and         | Max      | Welling. |             | 2014.    |
| allocation  | with       | topic-layer-adaptive |       |         | stochastic    |     |                  |            |             |          |          |             |          |
|             |            |                      |       |         |               |     | Auto-encoding    |            | variational |          | Bayes.   | In          | Interna- |
| gradient    | Riemannian |                      | MCMC. | In      | International |     |                  |            |             |          |          |             |          |
|             |            |                      |       |         |               |     | tional           | Conference | on          | Learning |          | Representa- |          |
ConferenceonMachineLearning.
tions.
| Rajarshi | Das,     | Manzil | Zaheer, | and   | Chris  | Dyer. |          |       |         |         |         |             |         |
| -------- | -------- | ------ | ------- | ----- | ------ | ----- | -------- | ----- | ------- | ------- | ------- | ----------- | ------- |
|          |          |        |         |       |        |       | Jey H.   | Lau,  | David   | Newman, |         | and Timothy |         |
| 2015.    | Gaussian | LDA    | for     | topic | models | with  |          |       |         |         |         |             |         |
|          |          |        |         |       |        |       | Baldwin. | 2014. | Machine |         | reading | tea         | leaves: |
wordembeddings.InAssociationforComputa-
|            |             |         |          |               |            |       | Automatically |       | evaluating | topic  | coherence   |     | and    |
| ---------- | ----------- | ------- | -------- | ------------- | ---------- | ----- | ------------- | ----- | ---------- | ------ | ----------- | --- | ------ |
| tional     | Linguistics |         | and      | International |            | Joint |               |       |            |        |             |     |        |
|            |             |         |          |               |            |       | topic         | model | quality.   | In     | Conference  |     | of the |
| Conference | on          | Natural | Language |               | Processing |       |               |       |            |        |             |     |        |
|            |             |         |          |               |            |       | European      |       | Chapter    | of the | Association |     | for    |
(Volume1:LongPapers).
ComputationalLinguistics.
SamuelJ.GershmanandNoahD.Goodman.2014.
|     |     |     |     |     |     |     | Quoc Le | and | Tomas Mikolov. |     | 2014. | Distributed |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- | -------------- | --- | ----- | ----------- | --- |
Amortizedinferenceinprobabilisticreasoning. representationsofsentencesanddocuments.In
| In Annual | Meeting |     | of the | Cognitive |     | Science |               |     |            |     |         |     |        |
| --------- | ------- | --- | ------ | --------- | --- | ------- | ------------- | --- | ---------- | --- | ------- | --- | ------ |
|           |         |     |        |           |     |         | International |     | Conference | on  | Machine |     | Learn- |
Society.
ing.
Thomas L. Griffiths, Mark Steyvers, David M. Omer Levy and Yoav Goldberg. 2014.
Blei,andJoshuaB.Tenenbaum.2004.Integrat-
|     |     |     |     |     |     |     | Neural | word | embedding |     | as implicit |     | matrix |
| --- | --- | --- | --- | --- | --- | --- | ------ | ---- | --------- | --- | ----------- | --- | ------ |
ing topics and syntax. In Advances in Neural factorization.InNeuralInformationProcessing
| InformationProcessingSystems. |     |     |     |     |     |     | Systems. |     |     |     |     |     |     |
| ----------------------------- | --- | --- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- |
Zellig S. Harris. 1954. Distributional structure. Shaohua Li, Tat-Seng Chua, Jun Zhu, and Chun-
Word,10(2–3):146–162. yan Miao. 2016. Generative topic embedding:
|     |     |     |     |     |     |     | A continuous |     | representation |     | of documents. |     | In  |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | -------------- | --- | ------------- | --- | --- |
MatthewD.Hoffman,DavidM.Blei,andFrancis
|     |     |     |     |     |     |     | AnnualMeeting |     | ofthe | Associationfor |     |     | Compu- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ----- | -------------- | --- | --- | ------ |
Bach.2010.OnlinelearningforlatentDirichlet
tationalLinguistics(Volume1:LongPapers).
| allocation. | In  | Advances | in  | Neural | Information |     |     |     |     |     |     |     |     |
| ----------- | --- | -------- | --- | ------ | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
ProcessingSystems. Yang Li and Tao Yang. 2018. Word Embedding
forUnderstandingNaturalLanguage:ASurvey,
| Matthew | D. Hoffman, |     | David | M.  | Blei, | Chong |     |     |     |     |     |     |     |
| ------- | ----------- | --- | ----- | --- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- |
SpringerInternationalPublishing.
Wang,andJohnPaisley.2013.Stochasticvaria-
|                        |     |         |     |            |          |     | Andrew | L. Maas, | Raymond |        | E. Daly, | Peter  | T.  |
| ---------------------- | --- | ------- | --- | ---------- | -------- | --- | ------ | -------- | ------- | ------ | -------- | ------ | --- |
| tional inference.      |     | Journal |     | of Machine | Learning |     |        |          |         |        |          |        |     |
| Research,14:1303–1347. |     |         |     |            |          |     | Pham,  | Dan      | Huang,  | Andrew |          | Y. Ng, | and |
ChristopherPotts.2011.Learningwordvectors
Sergey Ioffe and Christian Szegedy. 2015. Batch for sentiment analysis. In Annual Meeting of
normalization: Accelerating deep network theAssociationfor Computational Linguistics:
| training | by  | reducing | internal | covariate |     | shift. |     |     |     |     |     |     |     |
| -------- | --- | -------- | -------- | --------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
HumanLanguageTechnologies.
| In International |     |     | Conference |     | on Machine |     |       |       |         |     |      |          |     |
| ---------------- | --- | --- | ---------- | --- | ---------- | --- | ----- | ----- | ------- | --- | ---- | -------- | --- |
|                  |     |     |            |     |            |     | Yishu | Miao, | Lei Yu, | and | Phil | Blunsom. |     |
Learning.
|     |     |     |     |     |     |     | 2016. | Neural | variational |     | inference |     | for text |
| --- | --- | --- | --- | --- | --- | --- | ----- | ------ | ----------- | --- | --------- | --- | -------- |
MichaelI.Jordan,ZoubinGhahramani,TommiS.
|              |     |                |     |          |       |         | processing.      |     | In International |     | Conference |     | on  |
| ------------ | --- | -------------- | --- | -------- | ----- | ------- | ---------------- | --- | ---------------- | --- | ---------- | --- | --- |
| Jaakkola,    | and | Lawrence       |     | K. Saul. | 1999. | An      | MachineLearning. |     |                  |     |            |     |     |
| introduction |     | to variational |     | methods  | for   | graphi- |                  |     |                  |     |            |     |     |
calmodels.MachineLearning,37(2):183–233. Tomas Mikolov, Kai Chen, Greg S. Corrado,
|     |     |     |     |     |     |     | and Jeffrey |     | Dean. 2013a. |     | Efficient | estimation |     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ------------ | --- | --------- | ---------- | --- |
Kamrun Naher Keya, Yannis Papanikolaou, and of word representations in vector space. arXiv
James R. Foulds. 2019. Neural embedding preprintarXiv:1301.3781
451

TomasMikolov,IlyaSutskever,KaiChen,GregS. David E. Rumelhart and Adele A. Abrahamson.
Corrado, and Jeff Dean. 2013b. Distributed 1973. A model for analogical reasoning.
representations of words and phrases and CognitivePsychology,5(1):1–28.
| their compositionality. |     |     | In  | Neural | Information |     |          |     |      |        |     |         |        |
| ----------------------- | --- | --- | --- | ------ | ----------- | --- | -------- | --- | ---- | ------ | --- | ------- | ------ |
|                         |     |     |     |        |             |     | Bei Shi, | Wai | Lam, | Shoaib |     | Jameel, | Steven |
ProcessingSystems.
|     |     |     |     |     |     |     | Schockaert, |     | and | Kwun | P. Lai. | 2017. | Jointly |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --- | ---- | ------- | ----- | ------- |
David Mimno, Hanna M. Wallach, Edmund learning word embeddings and latent topics.
Talley, Miriam Leenders, and Andrew In ACM SIGIR Conference on Research and
DevelopmentinInformationRetrieval.
| McCallum. | 2011.    |         | Optimizing | semantic      |     | coher- |     |     |     |     |     |     |     |
| --------- | -------- | ------- | ---------- | ------------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
| ence      | in topic | models. |            | In Conference |     | on     |     |     |     |     |     |     |     |
AkashSrivastavaandCharlesSutton.2017.Auto-
| Empirical | Methods |     | in  | Natural | Language |     |     |     |     |     |     |     |     |
| --------- | ------- | --- | --- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
encodingvariationalinferencefortopicmodels.
Processing.
|          |      |            |     |              |     |       | In International |             |     | Conference |     | on      | Learning |
| -------- | ---- | ---------- | --- | ------------ | --- | ----- | ---------------- | ----------- | --- | ---------- | --- | ------- | -------- |
| Andriy   | Mnih | and Koray  |     | Kavukcuoglu. |     | 2013. | Representations. |             |     |            |     |         |          |
| Learning | word | embeddings |     | efficiently  |     | with  |                  |             |     |            |     |         |          |
|          |      |            |     |              |     |       | Nitish           | Srivastava, |     | Geoffrey   |     | Hinton, | Alex     |
noise-contrastiveestimation.InNeuralInform-
|     |     |     |     |     |     |     | Krizhevsky, |     | Ilya | Sutskever, |     | and | Ruslan |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ---- | ---------- | --- | --- | ------ |
ationProcessingSystems.
|             |        |        |       |            |           |      | Salakhutdinov. |     | 2014.   | Dropout: |          | a simple     | way       |
| ----------- | ------ | ------ | ----- | ---------- | --------- | ---- | -------------- | --- | ------- | -------- | -------- | ------------ | --------- |
|             |        |        |       |            |           |      | to prevent     |     | neural  | networks | from     | overfitting. |           |
| Christopher | E.     | Moody. | 2016. | Mixing     | Dirichlet |      |                |     |         |          |          |              |           |
|             |        |        |       |            |           |      | Journal        | of  | Machine |          | Learning |              | Research, |
| topic       | models | and    | word  | embeddings | to        | make |                |     |         |          |          |              |           |
15(1):1929–1958.
LDA2vec.arXiv:1605.02019.
|          |          |         |       |              |     |       | Michalis | K.     | Titsias    | and Miguel |             | La´zaro-Gredilla. |           |
| -------- | -------- | ------- | ----- | ------------ | --- | ----- | -------- | ------ | ---------- | ---------- | ----------- | ----------------- | --------- |
| Dat Q.   | Nguyen,  | Richard |       | Billingsley, | Lan | Du,   |          |        |            |            |             |                   |           |
|          |          |         |       |              |     |       | 2014.    | Doubly | stochastic |            | variational |                   | Bayes for |
| and Mark | Johnson. |         | 2015. | Improving    |     | topic |          |        |            |            |             |                   |           |
non-conjugateinference.InInternationalCon-
modelswithlatentfeaturewordrepresentations.
ferenceonMachineLearning.
| Transactions |     | of the | Association | for | Computa- |     |     |     |     |     |     |     |     |
| ------------ | --- | ------ | ----------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
tionalLinguistics,3:299–313. Hanna M. Wallach, David M. Mimno, and
|               |             |          |         |             |     |        | Andrew | McCallum. |         | 2009a. | Rethinking |     | LDA:   |
| ------------- | ----------- | -------- | ------- | ----------- | --- | ------ | ------ | --------- | ------- | ------ | ---------- | --- | ------ |
| Jeffrey       | Pennington, |          | Richard | Socher,     |     | and    |        |           |         |        |            |     |        |
|               |             |          |         |             |     |        | Why    | priors    | matter. | In     | Advances   | in  | Neural |
| ChristopherD. |             | Manning. |         | 2014.GloVe: |     | Global |        |           |         |        |            |     |        |
InformationProcessingSystems.
| vectorsforword |     | representation.InConference |     |     |     |     |     |     |     |     |     |     |     |
| -------------- | --- | --------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
on Empirical Methods on Natural Language Hanna M. Wallach, Iain Murray, Ruslan
| Processing.      |     |      |          |             |         |     | Salakhutdinov,   |     |         | and David  | Mimno. |       | 2009b.  |
| ---------------- | --- | ---- | -------- | ----------- | ------- | --- | ---------------- | --- | ------- | ---------- | ------ | ----- | ------- |
|                  |     |      |          |             |         |     | Evaluation       |     | methods |            | for    | topic | models. |
| James Petterson, |     | Wray | Buntine, |             | Shravan | M.  |                  |     |         |            |        |       |         |
|                  |     |      |          |             |         |     | In International |     |         | Conference |        | on    | Machine |
| Narayanamurthy,  |     |      | Tibe´rio | S. Caetano, |         | and |                  |     |         |            |        |       |         |
Learning.
| Alex J. | Smola. | 2010. | Word | features | for | latent |     |     |     |     |     |     |     |
| ------- | ------ | ----- | ---- | -------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
Advances in Neural Pengtao Xie, Diyi Yang, and Eric Xing. 2015.
| dirichlet | allocation. |     | In  |     |     |     |     |     |     |     |     |     |     |
| --------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
InformationProcessingSystems. Incorporatingwordcorrelationknowledgeinto
|     |     |     |     |     |     |     | topic | modeling. |     | In Conference |     | of  | the North |
| --- | --- | --- | --- | --- | --- | --- | ----- | --------- | --- | ------------- | --- | --- | --------- |
Danilo J. Rezende, Shakir Mohamed, and Daan American Chapter of the Association for
Wierstra.2014.Stochasticbackpropagationand
|             |     |           |     |         |            |     | Computational |     | Linguistics: |     | Human |     | Language |
| ----------- | --- | --------- | --- | ------- | ---------- | --- | ------------- | --- | ------------ | --- | ----- | --- | -------- |
| approximate |     | inference |     | in deep | generative |     |               |     |              |     |       |     |          |
Technologies.
| models. | In  | International |     | Conference |     | on  |          |     |        |       |     |     |          |
| ------- | --- | ------------- | --- | ---------- | --- | --- | -------- | --- | ------ | ----- | --- | --- | -------- |
|         |     |               |     |            |     |     | Hongteng | Xu, | Wenlin | Wang, |     | Wei | Liu, and |
MachineLearning.
|     |     |     |     |     |     |     | Lawrence |     | Carin. | 2018. | Distilled | Wasserstein |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | --- | ------ | ----- | --------- | ----------- | --- |
Michal Rosen-Zvi, Thomas Griffiths, Mark learning for word embedding and topic
Steyvers, and Padhraic Smyth. 2004. The modeling. In Advances in Neural Information
author-topicmodelforauthorsanddocuments.
ProcessingSystems.
InUncertaintyinArtificialIntelligence.
|     |     |     |     |     |     |     | Guangxu | Xun, |     | Vishrawas |     | Gopalakrishnan, |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---- | --- | --------- | --- | --------------- | --- |
Maja Rudolph, Francisco J. R. Ruiz, Stephan FenglongMa,YaliangLi,JingGao,andAidong
Mandt, and David M. Blei. 2016. Exponential Zhang. 2016. Topic discovery for short texts
family embeddings. In Advances in Neural usingwordembeddings.InIEEEInternational
| InformationProcessingSystems. |     |     |     |     |     |     | ConferenceonDataMining. |     |     |     |     |     |     |
| ----------------------------- | --- | --- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- | --- |
452

GuangxuXun,YaliangLi,WayneXinZhao,Jing He Zhao, Lan Du, and Wray Buntine. 2017a.
Gao, and Aidong Zhang. 2017. A correlated A word embeddings informed focused topic
topic model using word embeddings. In Joint model. In Asian Conference on Machine
| ConferenceonArtificialIntelligence. |     |     | Learning. |     |     |     |
| ----------------------------------- | --- | --- | --------- | --- | --- | --- |
Hao Zhang, Bo Chen, Dandan Guo, and He Zhao, Lan Du, Wray Buntine, and Gang
|          |             |               | Liu. 2017b. | MetaLDA: | A topic model | that |
| -------- | ----------- | ------------- | ----------- | -------- | ------------- | ---- |
| Mingyuan | Zhou. 2018. | WHAI: Weibull |             |          |               |      |
hybrid autoencoding inference for deep topic efficiently incorporates meta information. In
modeling. In International Conference on IEEE International Conference on Data
| LearningRepresentations. |     |     | Mining. |     |     |     |
| ------------------------ | --- | --- | ------- | --- | --- | --- |
453