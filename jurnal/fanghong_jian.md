Received:5November2018 Revised:16August2019 Accepted:24September2019
DOI:10.1111/coin.12248
| ORIGINAL ARTICLE |               |           |               |             |               |     |     |     |     |
| ---------------- | ------------- | --------- | ------------- | ----------- | ------------- | --- | --- | --- | --- |
| A topic-based    | term          | frequency |               |             | normalization |     |     |     |     |
| framework        | to enhance    |           | probabilistic |             |               |     |     |     |     |
| information      | retrieval     |           |               |             |               |     |     |     |     |
| FanghongJian1,2  | JimmyX.Huang3 |           |               | JiashuZhao4 |               |     |     |     |     |
| ZhiweiYing3      | YuqiWang3     |           |               |             |               |     |     |     |     |
1NationalEngineeringResearchCenter
Abstract
forE-Learning,CentralChinaNormal
|     |     | Many | well-known | probabilistic |     | information |     | retrieval |     |
| --- | --- | ---- | ---------- | ------------- | --- | ----------- | --- | --------- | --- |
University,Wuhan,China
2SchoolofScience,JiujiangUniversity, modelshaveshownpromiseforuseindocumentrank-
Jiujiang,China ing, especially BM25. Nevertheless, it is observed that
3SchoolofInformationTechnology,York
|     |     | the | control | parameters | in  | BM25 | usually | need | to be |
| --- | --- | --- | ------- | ---------- | --- | ---- | ------- | ---- | ----- |
University,Toronto,Canada
|     |     | adjusted | to  | achieve | improved | performance |     | on  | differ- |
| --- | --- | -------- | --- | ------- | -------- | ----------- | --- | --- | ------- |
4DepartmentofPhysicsandComputer
|     |     | ent | data sets; | additionally, |     | the assumption |     | in  | BM25 |
| --- | --- | --- | ---------- | ------------- | --- | -------------- | --- | --- | ---- |
Science,WilfridLaurierUniversity,
Waterloo,Canada on the bag-of-words model prevents its direct utiliza-
|     |     | tion | of rich | information | that | lies | at the | sentence | or  |
| --- | --- | ---- | ------- | ----------- | ---- | ---- | ------ | -------- | --- |
Correspondence
JimmyX.Huang,SchoolofInformation document level. Inspired by the above challenges with
Technology,TechnologyEnhanced respecttoBM25,wefirstproposeanewnormalization
LearningBuilding,YorkUniversity,
methodonthetermfrequencyinBM25(calledBM25
| Toronto,OntarioM3J1P3Canada. |     |     |     |     |     |     |     |     | QL  |
| ---------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Email:jhuang@yorku.ca in this paper); in addition, the method is incorporated
|                    |     | intoCRTER |     | ,arecentBM25-basedmodel,toconstruct |     |     |     |     |     |
| ------------------ | --- | --------- | --- | ----------------------------------- | --- | --- | --- | --- | --- |
| Fundinginformation |     |           |     | 2                                   |     |     |     |     |     |
NaturalSciencesandEngineering CRTER QL. Then, we incorporate topic modeling and
2
ResearchCouncilofCanada;York wordembeddingintoBM25torelaxtheassumptionof
ResearchChair(YRC)Program
thebag-of-wordsmodel.Inthisdirection,weproposea
topic-basedretrievalmodel,TopTF,forBM25,whichis
thenfurtherincorporatedintothelanguagemodel(LM)
andthemultipleaspecttermfrequency(MATF)model.
Furthermore,anenhancedtopic-basedtermfrequency
|     |     | normalization |     | framework, |     | ETopTF, | based | on embed- |     |
| --- | --- | ------------- | --- | ---------- | --- | ------- | ----- | --------- | --- |
dingispresented.Experimentalstudiesdemonstratethe
|     |     | great | effectiveness | and | performance |     | of these | methods. |     |
| --- | --- | ----- | ------------- | --- | ----------- | --- | -------- | -------- | --- |
ComputationalIntelligence.2019;1–36. wileyonlinelibrary.com/journal/coin ©2019WileyPeriodicals,Inc. 1

2 JIANetal.
Specifically, on all tested data sets and in terms of the
mean average precision (MAP), our proposed models,
BM25 and CRTER QL, are comparable to BM25 and
QL 2
CRTER with the best b parameter value; the TopTF
2
models significantly outperform the baselines, and the
ETopTF models could further improve the TopTF in
termsoftheMAP.
KEYWORDS
Dirichletlanguagemodel,embedding,LDA,probabilisticmodel,
termfrequencynormalization,topicmodeling
1 INTRODUCTION AND MOTIVATION
The normalization of term frequency (TF) is of critical importance to the success of prob-
abilistic information retrieval (IR) models. Specifically, sublinear TF normalization in BM25
anditsenhancedversions1-3 representsthestate-of-the-art:itconsistsoftwoterm-independent
hyper-parameters (k and b), whose actual values often need to be adjusted with respect
1
to a given data set. Substantial recent research has been focusing on the automatic tun-
ing of document length normalization. TF normalization approaches as introduced in pre-
vious work4-9 are document and collection dependent, with settings on term-independent
parameters remaining unchanged compared to the settings in the original BM25. R.
Cummins10 investigated the role of query length on normalization; however, that work
did not measure the actual effect in a quantitative manner. Lv and Zhai11 used query
length normalization constraints to estimate term-specific parameters. Their approach, how-
ever, is computationally expensive and often at the risk of overfitting the data. Lv12 and
TLChungetal13combinedquerylengthconstraintandlinearregressionforvalueestimationof
theparameters,whichmeansthatpretrainingmustbeperformed.Howtoeasilyandeffectively
incorporatethequerylengthintotheprobabilisticIRmodelinworkablesolutionscallsrequires
furtherinvestigation.
IntraditionalIRmodels,querytermsareassumedtobepair-wiseindependent,andwerepre-
sentadocumentsimplyasabag-of-words.Theapplicabilityoftheseassumptions,however,can
bequestionableinpractice,especiallyincaseswherebetterresultsareknowntousbutexisting
modelsareunabletofindthem.Motivatedbythisfact,weconsiderincorporatingtopicinforma-
tion in documents in our new model in light of the observation that a document may contain
severaldifferenttopicsandthattermsappearinginthedocumentmightbelongtoseveraldiffer-
enttopics,eachofwhichconveyingaspecificpieceofinformation.Substantialcurrentresearchis
dedicatedtoconsideringtermtopicinformationinIR.14-17Inthiscase,howquerytermsareactu-
allyassociatedwitheachothertermsremainsaresearchproblemyettoseeextensivestudy.18-20
Existingcluster-basedapproachesoftenassumethatanygivendocumenthasonlyonetopic.15
However, for large collections of documents, this assumption is probably too strong. Topic-
based document representation is effective in the language modeling (LM) framework.14,16,17
ThispaperisanextendedjournalversionofearlierworkpublishedinACMSIGIR2016and2018,respectively.

JIANetal. 3
However,itremainsunclearhowgeneraltopicinformationcanbeintegratedintoprobabilistic
IRmodelssuchasBM25.
In addition, embedding-based methods21,22 have been widely used in many applications
andhaveachievedpromisingperformance,forexample,innaturallanguageprocessing(NLP).
The word embeddings are representations of words in vectors that can be used to represent
the contextual and semantic information of the words and can be naturally adapted to many
textual-related tasks. The documents can, therefore, be represented in the vector space instead
of the much more sparse word space. In recent years, IR researchers have begun to inves-
tigate word-embedding-based approaches, while most such IR work has been conducted for
language model frameworks.23-28 To the best of our knowledge, few studies have incorporated
wordembeddingapproachesintoprobabilisticIRmodels.
In this paper, we propose a simple and effective query-length-based TF normalization for
probabilistic BM25 and integrate it into the state-of-the-art CRTER . The effectiveness of the
2
three TF normalization functions is evaluated empirically, in particular, on TREC data sets.
Considering term-based information and topic-based semantic information as two features of
queryterms,wefurtherpresentTopTF,anenhancedIRmodelwithtopicmodelingtechniques
incorporated. We also extend it to the LM and MATF framework. Latent Dirichlet allocation
(LDA)29asatopicmodelisutilizedtocombinethesetwofeaturesandenhancethreewell-known
traditional IR models: BM25,3 MATF30 and Dirichlet LM.31,32 In particular, four hybrid mod-
els, denoted as LDA-BM25 , LDA-BM25, LDA-MATF and LDA-LM, are proposed. Finally, an
QL
enhancedtopic-basedtermfrequencynormalizationframeworkbasedonembedding,ETopTF,
isproposed.
Themaincontributionsofthispaperareasfollows.First,wepresentthreeTFnormalization
functionsinBM25.Second,weproposeseveralsimplebuteffectiveIRmodelsbycombiningtradi-
tionalIRmodelswithtopicmodelingtechniques.Finally,weutilizeembedding-basedsimilarity
to enhance the topic-based retrieval models. Extensive experiments are performed to evaluate
the effectivenessandperformanceofour proposedBM25 modelandthe TopTFandETopTF
QL
frameworks.
Theremainderofthispaperisorganizedasfollows.InSection2,wedescribetherelatedwork.
Next in Section 3, we present a modified BM25 via a new TF normalization method, and then
theenhancedtopic-basedframeworkETopTFviaembeddingisproposed.InSection4,14rep-
resentativetestcollectionsusedinourexperiments,togetherwithparametersettingsinbaseline
models,andtheextendedtopic-basedIRmodelinMATFandLM,areintroduced.Resultsandan
extendedanalysisontheseresultsarereportedinSection5.Weconcludeourworkandprovide
abriefdiscussiononpossiblefutureresearchinSection6.
2 RELATED WORK
InprobabilisticIRmodels,TFnormalizationsareveryeffective.SublinearTFnormalizationis
effective in many models, including BM25.3 In BM25, it uses document length normalization,
whichiscontrolledbytwofixedterm-independentpriorparameters,k andb,wherek addresses
1 1
the scope hypothesis on the documents, and b concerns the verbosity hypothesis (eg, slop).33
BothparametersneedtobetunedtoimprovetheperformanceofBM25withrespecttoagiven
data set.34,35 In what follows,5,6,36 normalization is used for collection-dependent parameters.
In particular, some considerable efforts have been directed toward understanding and remov-
ingtheparametersinBM25.LvandZhai11 notedthatitismoreeffectivetouseaterm-specific

4 JIANetal.
k , and it is possible to estimate k using an information gain measure to quantify the con-
1 1
tributions of repeated term occurrences. Lipani et al37 used the mean average term frequency
of the collection to characterize b. Chung et al13 incorporated the query length into the vec-
tor space model, and experiments on both Chinese and English corpora were conducted. The
researchsuggestedthatthequerylengthshouldbeincorporatedintootherexistingrankingfunc-
tions.CumminsandO’Riordan10 firstobservedthequerylengtheffectsonTFnormalizationin
BM25,andLv12 usedquerylengthheuristicsandaregressionmodeltoobtainvaluesofk and
1
bthroughpriordatatraining.Althoughtheabove-mentionedworksandresearchareeffective,
some methods are quite complicated in nature, while other methods are highly dependent on
eachother.
Since the 1990s, integrating term associations into IR models has been actively
investigated.17,38-41 Most query-term associations have been modeled in these approaches with
respect to the distance of the query terms in documents. For example, Buttcher et al42 used
a proximity accumulator to associate each query term. Lv and Zhai43 proposed a positional
language model (PLM) that incorporates the term proximity into a model-based approach
usingterm-propagationfunctions.MetzlerandCroft39 proposedaMarkovrandomfield(MRF)
model that modeled the joint distribution over queries and documents. Song et al44 proposed
a proximity probabilistic model (PPM), which uses a position-dependent term count to rep-
resent both the number of occurrences of a term and the term counts propagated from other
terms. Quite recently, topic models have been widely used to explore latent term associations
inknowledgediscovery45-48 andotherrelatedareas.49-51 LiuandCroft15 inparticularproposed
cluster-based retrieval models under the language modeling framework, which has been used
to smooth the probabilities in the document model. In that approach, a document is assumed
to contain only one topic—an assumption that is too strong for modeling a large collection of
documents. Azzopardi et al14 showed that it was effective to use the LDA model29 to smooth
the probabilitiesin the document model on several small collections. Wei and Croft16 also dis-
cussed the applications of LDA in large collections and presented a detailed evaluation of the
effectiveness.YiandAllan52 exploredtheutilityofthemixtureofunigrams(MU)model,LDA
and Pachinko allocation model (PAM)53 for IR. They showed that topic models were effective
for document smoothing. More rigorous topic models, such as LDA, have achieved gains over
cluster-based models and more elaborate topic models that capture topic dependencies but
providenoadditionalgains.Althoughitiseffectivetointegratetopicmodelsintolanguagemod-
elingframeworks,howtointegratetopicalinformationintoothertraditionalIRmodelsrequires
furtherstudy.
In addition, word embedding is a distributed representation for words that can be learned
fromaneuralprobabilisticlanguagemodel.54 Theembeddingmethodhasseengreatsuccessin
NLP,whichhasinspiredresearcherstouseitforIR.23-28 However,substantialamountsofwork
naturally integrate the probability of words expressed in terms of their distributed representa-
tionsinthelanguagemodelframework,andlessworkhasexploredhowtoutilizetheembedding
methodtoenhanceothertraditionalIRmodels.
3 OUR PROPOSED FRAMEWORK
InSection3.1,wefirstpresenttheclassicalBM25model,discussitsparametersandproposea
newtermfrequencynormalizationmodelcalledBM25 .Wealsopresentthreedifferentfunc-
QL
tionsusingthequerylengthforthenewTFnormalizationtoavoidthetuningofbinBM25on

JIANetal. 5
individual data sets. In Section 3.2, we formulate how to integrate the topic model and word
embeddingintoprobabilisticretrievalmodels.Anoverallframeworkisproposedforanenhanced
topic-basedretrievalmodelwithwordembedding.
3.1 AnewTFnormalizationmodel:BM25
QL
We first investigate the parameters in probabilistic BM25 and attempt to address the
parameter-tuning problem. In this section, we discuss all the parameters in BM25 and mainly
focusonthemostcrucialtermfrequency(TF).ThreefunctionsareproposedtonormalizetheTF,
anddetaileddeductionsarepresented.
Forclarification,thenotationsusedinthispaperarelistedinTable1.
| 3.1.1 | BM25anditsparameters |     |     |     |     |     |     |
| ----- | -------------------- | --- | --- | --- | --- | --- | --- |
In BM25, the weight of a query term is assigned based on its within-document TF and
within-queryTF.Specifically,theweightingfunctionis
|           |                            | (k +1)⋅TF(q,d) |     | (k +1)⋅qtf(q) |                            | N−n(q)+0.5 |     |
| --------- | -------------------------- | -------------- | --- | ------------- | -------------------------- | ---------- | --- |
|           | w′(q,d)=                   | 1              | i   | ⋅ 3           | i ⋅log                     |            | i , |
|           | i                          | +TF(q,d)       |     |               |                            |            | (1) |
|           |                            | k              |     | k +qtf(q)     |                            | n(q)+0.5   |     |
|           |                            | 1              | i   | 3             | i                          |            | i   |
| TABLE     | 1 Notationsusedinthispaper |                |     |               |                            |            |     |
| Notations | Description                |                |     | Notations     | Description                |            |     |
| c         | Thecollection              |                |     | N             | Numberofindexeddocumentsin |            |     |
collection
| d   | Adocument |     |     | n(q) i | Numberofindexeddocuments |     |     |
| --- | --------- | --- | --- | ------ | ------------------------ | --- | --- |
containingatermq
i
| q   | Aquery |     |     | TF(q,d) | Normalizedwithin-documentterm |     |     |
| --- | ------ | --- | --- | ------- | ----------------------------- | --- | --- |
i
frequency
| q i | Aqueryterm           |     |     | TF QL    | NormalizedTFwithb           |     | QL  |
| --- | -------------------- | --- | --- | -------- | --------------------------- | --- | --- |
| ql  | Querylength          |     |     | w,w′,w′′ | Weightingfunction           |     |     |
| dl  | Lengthofdocument     |     |     | 𝜇        | DirichletpriorinDirichletLM |     |     |
| cl  | Totalnumberoftermsin |     |     | P,P      | Probabilityfunction         |     |     |
ml
thecollection
| avdl    | Averagedocumentlength |     |     | z   | Atopic         |     |     |
| ------- | --------------------- | --- | --- | --- | -------------- | --- | --- |
| tf(q,d) | Within-documentterm   |     |     | K   | Numberoftopics |     |     |
| i       |                       |     |     | t   |                |     |     |
frequency
𝛼,𝛽,𝜃,𝜑
| avgtf(d) | Averagetermfrequencyof |     |     |     | ParametersinLDA |     |     |
| -------- | ---------------------- | --- | --- | --- | --------------- | --- | --- |
documentd
| qtf | Within-queryterm |     |     | V ,V | Embeddingvectors |     |     |
| --- | ---------------- | --- | --- | ---- | ---------------- | --- | --- |
|     |                  |     |     | q d  |                  |     |     |
frequency
b,k 1 ,k 3 ParametersinBM25 sim(q,d) i Similaritybetweenqueryand
document
b Functiontoquerylength 𝜆,𝜆 ,𝜆 ,𝛾 Interpolationcoefficientsinhybrid
| QL  |     |     |     | 1 2 |     |        |     |
| --- | --- | --- | --- | --- | --- | ------ | --- |
|     | ql. |     |     |     |     | models |     |

6 JIANetal.
where w′(q,d) is the weight of a query term q in document d and TF(q,d)= tf(q i ,d) is the
i i i (1−b)+b⋅ dl
avdl
pivoted document length normalization, which is an effective method for TF normalization.
Variablestothisformulacanbegroupedintothefollowingtwocategories:
• Thefirstcategoryofvariablesisparameterfree.Inthiscategory,thereareNindexeddocuments
inthecollection,n(q)isdefinedasthenumberofdocumentscontainingaspecificterm,and
i
tf(q,d)isthewithin-documentTF.qtf (q)isthewithin-queryTF.
i i
• ThevaluesoftheotherBM25variablesareparameterdependent.Inthiscategory,theparam-
eters k and k are tuning constants whose values are dependent on the data set in use and
1 3
may also be query specific. b is a parameter used to balance the impact of the document
lengthdl.
Therearethreeparameters,b,k ,andk inBM25,andtherearethreefields(title,descrip-
1 3
tion and narrative) for each query that we can utilize. We only use the “title” part of the
query to search the entire document in this paper because the title field contains very few
keywords related to the query and because the title-only queries are usually short, represent-
ing a realistic snapshot of real user queries in practice.41,55 Since each query term always
occurs one time in each query, the value of k does not need to be adjusted in most cases.
3
The parameter b in BM25 is sensitive and generally needs to be adjusted for different data
sets. Certain previous works10,12,13 have used supervised machine learning methods to fit the
parameter b as a function of the query length. In the following, we will focus on exploring
the relationship between the parameter b and the query length in an unsupervised man-
ner. The relationship between the parameter k and the query length will be studied in
1
futurework.
Finally,adocument’sweightforaqueryisgivenbythesumforeachterminthequery:
∑
BM25(q,d)= w′(q,d), (2)
i
q∈q
i
wherew′isthetermweightobtainedfromEquation(1).
3.1.2 AnewmethodforTFnormalization
A previous study12 showed that the query length ql actually interacts with the TF normaliza-
tion. From an information theoretic perspective, adding one more term to a query necessarily
meansthatmoreinformationisprovidedinthequery.Wehypothesizethatwhenthequerylength
increasestoalargeextent,theeffectoftheTFnormalizationshouldbehighlightedtoindicate
a preference for shorter documents. Based on this assumption, we propose a new method for
documentTFnormalizationusingthequerylength:
tf(q,d)
TF (q,d)= i , (3)
QL i (1−b (ql))+b (ql)⋅ dl
QL QL
avdl
whereb (ql)isafunctionofquerylengthql.Thefunctionhasarangeof(0,1),andthefunction
QL
should be monotonically nondecreasing. When ql goes to infinity, the function asymptotically
approaches 1. For example, the change of “b” caused by increasing ql from 2 to 3 should be

| JIANetal. |     |     |     |     |     |     |     |     |     |     | 7   |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
higherthanthatcausedbyincreasingqlfrom9to10.Specifically,thefunctionshouldhavethe
followingproperties:
Domain:ql≥0,
•
| • Boundedness:b  |     | (1)=0,and |         | lim b | (ql)=1,  |     |         |        |       |            |     |
| ---------------- | --- | --------- | ------- | ----- | -------- | --- | ------- | ------ | ----- | ---------- | --- |
|                  |     | QL        | ql→+∞   | QL    |          |     |         |        |       |            |     |
|                  |     | (ql)<b    | (ql+1)⇒ |       | db >0and |     |         | db     |       |            |     |
| • Monotonicity:b |     | QL        | QL      |       | QL       |     | lim     | QL =0, |       |            |     |
|                  |     |           |         |       | dql      |     | ql→+∞   | dql    |       |            |     |
|                  |     |           | (ql)>b  |       |          |     | (ql+1)⇒ | d2b    | <0and | d2b        |     |
| • Convexity:b    |     | (ql+1)−b  |         |       | (ql+2)−b |     |         |        | QL    | lim QL     | =0. |
|                  | QL  |           | QL      | QL    |          | QL  |         | dql2   |       | ql→+∞ dql2 |     |
| db               | d2b |           |         |       |          |     |         |        |       |            |     |
where QL and QL representthefirstandsecondderivatives,respectively.
| dql | dql2 |     |     |     |     |     |     |     |     |     |     |
| --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Threefunctionssatisfyingtheaboverequirementsonfunctionalpropertiesarepresentedin
thefollowing.
| 3.1.3 | Threetypesoffunctions |     |     |     |     |     |     |     |     |     |     |
| ----- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
LogarithmFunction:bLOG(ql).
QL
The first function bLOG(ql) was originally proposed by Paik30 and effectively uses the query
QL
lengthtobalancetwotermfrequencyfactors.
n
|     |     | bLOG(ql)=1− |     |     |     |     | , n=1,2,3, |     | … . |     | (4) |
| --- | --- | ----------- | --- | --- | --- | --- | ---------- | --- | --- | --- | --- |
QL
|     |     |     |     | n−1+log |     | (1+ql) |     |     |     |     |     |
| --- | --- | --- | --- | ------- | --- | ------ | --- | --- | --- | --- | --- |
2
ItcanbeconvenientlyshownthatbLOG(ql)satisfiesalltherequirements.
QL
| • bLOG(1)=0,and |     | lim | bLOG(ql)=1, |     |     |     |     |     |     |     |     |
| --------------- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
| QL              |     |     | QL          |     |     |     |     |     |     |     |     |
ql→+∞
| dbL O G |          |          |           |       | dbL O | G   |     |     |     |     |     |
| ------- | -------- | -------- | --------- | ----- | ----- | --- | --- | --- | --- | --- | --- |
| Q L     |          | n        | ⋅ 1 >0and |       | Q     | L   |     |     |     |     |     |
| • =     |          |          |           | lim   |       | =0, |     |     |     |     |     |
| dql     | [n−1+log | (1+ql)]2 | 1+ql      | ql→+∞ | dql   |     |     |     |     |     |     |
2
| d2bL O G | 1       | ⋅        | n        | ⋅[n+1+log |     | (1+ql)]<0and |     |       | d2bL  | O G   |     |
| -------- | ------- | -------- | -------- | --------- | --- | ------------ | --- | ----- | ----- | ----- | --- |
| • Q L =− |         |          |          |           |     |              |     |       | lim Q | L =0. |     |
| dql2     | (1+ql)2 | [n−1+log | (1+ql)]3 |           |     | 2            |     | ql→+∞ | dql2  |       |     |
2
Next,weprovidetwomorecandidatefunctions:bEXP(ql)andbREC(ql).
|     |     |     |     |     |     | QL  |     | QL  |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Exponentialfunction:bEXP(ql).
QL
d2b <0
Although QL and 1−b >0, their values both become closer to 0 when ql increases.
|     | dql2 |     | QL  |     |     |     |     |     |     |     |     |
| --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Wearethenmotivatedtopresentthefollowinghypothesis:
d2b
| HypothesisI. |     | QL   | isnegativelyproportionalto1−b |     |     |     | .   |     |     |     |     |
| ------------ | --- | ---- | ----------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
|              |     | dql2 |                               |     |     |     | QL  |     |     |     |     |
d2b
|     |     |     | QL  | =−k⋅(1−b |     |          |     | −1), |     |     |     |
| --- | --- | --- | --- | -------- | --- | -------- | --- | ---- | --- | --- | --- |
|     |     |     |     |          |     | QL )=k(b | QL  |      |     |     | (5) |
dql2
wherek>0isthecoefficientofproportionality.Equation(5)isasecond-orderordinarydifferen-
tialequation(ODE).
db
| Solution.Letp= |     |     | QL;thus, |     |     |     |     |     |     |     |     |
| -------------- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
dql
|     |     |     | d2b  | dp  | dp  | db   |     | dp  |     |     |     |
| --- | --- | --- | ---- | --- | --- | ---- | --- | --- | --- | --- | --- |
|     |     |     | QL   |     |     | ⋅ QL |     | ⋅p. |     |     |     |
|     |     |     |      | =   | =   |      | =   |     |     |     |     |
|     |     |     | dql2 | dql | db  | ql   | db  |     |     |     |     |
|     |     |     |      |     | QL  |      |     | QL  |     |     |     |

| 8   |     |     | JIANetal. |     |
| --- | --- | --- | --------- | --- |
Specifically,
dp
⋅p=k(b −1).
QL
db
QL
ThesolutiontotheaboveODEisp2=√k(b −1)2+C ,whereC issomeconstant.Withthe
|     |     | QL  | 1 1 |     |
| --- | --- | --- | --- | --- |
db
previouscharacteristicsofb ,p= QL = k(1−b )isalsoafirst-orderODE,anditssolution
|     | QL dql | QL  |     |     |
| --- | ------ | --- | --- | --- |
√
e− k⋅ql,whereC
isb QL (ql)=1−C 2 2 isalsoaconstant.Sinceb QL (1)=0,thefinalsolutionis
√
b (ql)=1−e− k(ql−1).
QL
√
| Letn=1∕ k.Weobtainacompactexponentialfunction. |     |     |     |     |
| ---------------------------------------------- | --- | --- | --- | --- |
( )
|     | bEXP(ql)=1−e | −ql −1 ,n=1,2,3, | .   |     |
| --- | ------------ | ---------------- | --- | --- |
|     |              | n                | …   | (6) |
QL
db >0,
Additionally, QL and its value becomes closer to 0 with increasing ql. We can also
dql
| d2b |     | db  |     |     |
| --- | --- | --- | --- | --- |
suppose that QL is negatively proportional to QL, which could lead to the same function as
| dql2 |     | dql |     |     |
| ---- | --- | --- | --- | --- |
Formula(6).
Reciprocalfunction:bREC(ql).
QL
|     |     | d2b | db  |     |
| --- | --- | --- | --- | --- |
According to the previous analysis of QL, 1−b and QL, we can propose the following
|     |     | dql2 QL | dql |     |
| --- | --- | ------- | --- | --- |
hypothesis.
|               | d2b                              |            | db      |     |
| ------------- | -------------------------------- | ---------- | ------- | --- |
| HypothesisII. | QL isnegativelyproportionalto1−b |            | and QL. |     |
|               | dql2                             |            | QL dql  |     |
|               | d2b                              | db         | db      |     |
|               | QL =−k⋅(1−b                      | )⋅ QL =k(b | −1) QL, | (7) |
|               |                                  | QL         | QL      |     |
|               | dql2                             | dql        | dql     |     |
wherek>0isthecoefficientofproportionality.Equation(7)isalsoasecond-orderODE.
db dp
Solution.Let p= QL.ODE(7)issimplifiedtoafirst-orderODE,namely, =k(b −1).
|     | dql |     | db  | QL  |
| --- | --- | --- | --- | --- |
QL
Thesolutionisp= k(b −1)2+C ,whereC isaconstant.Withanapplicationoftheconditions
|     | QL 1 | 1   |     |     |
| --- | ---- | --- | --- | --- |
2
db
| lim QL =0and | lim b =1,wecanobtain |     |     |     |
| ------------ | -------------------- | --- | --- | --- |
| ql→+∞ dql    | ql→+∞ QL             |     |     |     |
db QL k
p= = (b −1)2.
QL
dql 2
2
Thefinalsolutionisthusb QL (ql)=1− ,whereC 2 isaconstant.Undertheconstraint
k⋅ql+C
2
b QL (1)=0,weobtainthesolutiontoODE(7):
2∕k
.
b (ql)=1−
QL 2∕k+ql−1
Letn=2/k.Acompactreciprocalfunctionis.
n
|     | bREC(ql)=1− | , n=1,2,3, | … . | (8) |
| --- | ----------- | ---------- | --- | --- |
|     | QL          | n−1+ql     |     |     |

JIANetal. 9
FIGURE 1 Functionb (ql)with 1
QL
querylengthql[Colorfigurecanbe
0.9
viewedatwileyonlinelibrary.com]
0.8
0.7
0.6
0.5
0.4
0.3
0.2
0.1
0
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
ql
b
LQ
bEXP
QL
bLOG
QL
bREC
QL
Ourexperimentsonallthecollectionssuggestthatnshouldbesetto2,6,and4inFunctions
(4),(6),and(8),respectively;thesechoicesperformconsistentlybetterthantheothercases.
WelabelthesethreefunctionsasFormulas(9)-(11).
2
bLOG(ql)=1− . (9)
QL 1+log (1+ql)
2
4
bREC(ql)=1− . (10)
QL 3+ql
( )
bEXP(ql)=1−e
−ql
6
−1
. (11)
QL
In addition, from Figure 1, the proposed functions grow differently when the query length
ql increases: bLOG(ql) is based on the logarithm function, which grows the slowest; bREC(ql) is
QL QL
based on the reciprocal function, which grows with a medium speed; and bEXP(ql) is based on
QL
the exponential function, which grows the fastest. In this paper, we only consider these three
functions,andadditionalfunctionscouldbeevaluatedinourfutureresearch.
3.1.4 BM25 model
QL
We use the query length for the TF normalization deduced above in BM25 and propose a new
BM25 formulabelow:
QL
∑ (k +1)⋅TF (q,d) (k +1)⋅qtf(q) N−n(q)+0.5
BM25 (q,d)= 1 QL i ⋅ 3 i ⋅log i . (12)
QL k +TF (q,d) k +qtf(q) n(q)+0.5
q∈d 1 QL i 3 i i
i
Additionally,weexplorethreeTFnormalizationfunctionsforBM25,andthecorresponding
BM25 aredenotedasBM25 LOG,BM25 EXPandBM25 REC.
QL QL QL QL
In recent years, some state-of-the-art BM25-based models have performed well in IR.
For example, the bigram cross term model CRTER 40,41 is a well-known probabilistic prox-
2
imity model. We incorporate our proposed BM25 into CRTER by rep1acing its BM25,
QL 2

| 10  |     |     |     |     |     |     |     |     |     | JIANetal. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- |
namely, CRTER QL. Similarly, we a1so investigate our TF norma1ization functions (Formulas
2
QL.
| (9)-(11))inCRTER |     | 2   |     |     |     |     |     |     |     |     |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
3.2 Enhancedtopic-basedtermfrequencynormalizationframework
basedonembedding
| 3.2.1 | Topic-basedretrievalmodel |     |     |     |     |     |     |     |     |     |
| ----- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Ingeneral,thetopicmode1isusedtocapturethe1atentsemanticinformationoftermsindocu-
ments.Therearenumeroustopicmodelssuchasprobabilisticlatentsemanticindexing(pLSI),56
LDA29 andPAM.53
LDAisasimp1eandeffectivetopicmodelforIRandisa1sowidelyutilized.
Thispapera1sousesLDA.
TheLDAmode1assumesthefollowinggenerativeprocessforeachdocumentdinadocument
collectionc:
Foreachtopicz,amu1tinomia1distribution𝜑
| 1.  |     |     |     |     |     | z issamp1edfromaDirichletdistributionwith |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- |
hyper-parameter𝛽.𝛽 istheparameteroftheuniformDirich1etpriorontheper-topicword
distribution.
Foreachdocumentd,amultinomia1distribution𝜃
| 2.  |     |     |     |     |     | d issamp1edfromaDirich1etdistribution |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------------------------- | --- | --- | --- | --- |
withhyper-parameterα.αistheparameteroftheuniformDirich1etpriorontheper-document
topicdistributions.
3. Foreachwordwindocumentd,
chooseatopicz fromthemultinomia1distribution𝜃 ,wherez ∈{1,2,…,K
| a.  |                                               | k   |     |     |     |     | d   | k   | t }and. |     |
| --- | --------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ------- | --- |
| b.  | choosethewordwfromthemultinomia1distribution𝜑 |     |     |     |     |     | .   |     |         |     |
z
k
Thus,theprobabi1ityofgeneratingacollectioncisgivenas.
|     |               |        |     |     |      |          | (   | )        |      |      |
| --- | ------------- | ------ | --- | --- | ---- | -------- | --- | -------- | ---- | ---- |
|     |               |        |     | ∏K  | ∏N   |          | ∏N  | ∑K       |      |      |
|     |               |        |     | t   |      |          | d   | t        |      |      |
|     | P(d ,d ,···,d | |𝛼,𝛽)= |     | P(𝜑 | |𝛽)⋅ | P(𝜃 |𝛼)⋅ |     | P(w|z,𝜑) | d𝜃d𝜑 | (13) |
|     | 1 2           | N      | ∫∫  | z   |      | d        |     | i        |      |      |
|     |               |        |     | z=1 | d=1  |          | i=1 | z=1      |      |      |
whereNisthenumberofdocumentsincollectionc,N isthenumberofworddocumentsdandK
|     |     |     |     |     |     | d   |     |     |     | t   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
isthenumberoftopicsintheLDAmodel.Figure2depictsthep1atenotationfortheLDAmode1,
whicha1socapturesdependenciesamongallthevariables.TheLDAmodelisverycomplexandis
intractableinacomputationalsenseingeneral.Althoughtheposteriordistributionisintractable
for exact inference, a wide variety of approximate inference algorithms can be considered for
|     |     |     |     |     |     | FIGURE | 2   | PlatenotationfortheLDAmodel |     |     |
| --- | --- | --- | --- | --- | --- | ------ | --- | --------------------------- | --- | --- |

| JIANetal. |     |     |     |     |     |     |     |     | 11  |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
LDA,includingLaplaceapproximation,variationalapproximation,MarkovchainMonteCarlo57
sampling.58
and Gibbs In this article, we use a new high1y efficient imp1ementation of LDA,
1ightLDA,59whoserunningcostisagnosticofthemode1sizeandempiricallyconvergesatarate
closetoanorderofmagnitudefasterthanthestate-of-the-artGibbssamp1er.
TheLDAmodelcangeneratetheprobabilityoftopicsoccurringinadocumentandtheprob-
ability of words occurring in a topic, these can be used to obtain the generated probability of
words in a document. We take the probability of a query term in a document as its implicit
topic-basedsemanticinformationinthedocument.Higherprobabilityvaluesimplyacloserrela-
tionshipbetweenthetermandthedocument.Tobealignedwithweightsintraditionalmodels,
theweightofaquerytermtiforadocumentdintheLDAmodelusesthelogvalueofthegenerated
probability:
|     |     |     |     |     | (   |     |     | )   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
∑K
t
|     |     | w′′(q,d)=logP(q|d)=log |     |     |     | P(q|z)⋅P(z|d) |     | .   | (14) |
| --- | --- | ---------------------- | --- | --- | --- | ------------- | --- | --- | ---- |
|     |     |                        | i   | i   |     | i             |     |     |      |
z=1
Traditionalretrievalmodelsonlycaptureterm-basedinformation.Ontheotherhand,topic
models extract the latent topics based on the higher order word co-occurrences. In this sense,
eveniftheTFvalueissmallforagivenword,itcouldobtainalargeweightscoreifthedocument
is highly relevant to the topics to which the word is most relevant. In this paper, we propose
enhanced retrieval models that consider not only the TF, document frequency and document
lengthbutalsothetermtopicalinformation.Wetreatterm-basedinformationandtopic-based
semantic information as two features for query terms. The enhanced retrieval models should
combinethesetwofeatures.
Givenaqueryq,foreachtermq inqueryq,w(q,d)istheenhancedweightfordocumentd.
|     |     |     |     | i   |     | i   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Tocapturethetwotypesofinformation,weuseaparameter𝜆tobalancetheirimportance.Thus,
theweightofaquerytermforadocumentisasfollows:
w(q,d)=(1−𝜆)⋅w′(q,d)+𝜆⋅w′′(q,d),
(15)
|     |     |     | i   |     | i   |     | i   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
where w′(q,d) represents the explicit term-based related information in the traditional IR
i
model for document d, and w′′(q,d) is the implicit topic-based semantic information in the
i
topicmodel.𝜆isasmoothingparameterusedtobalancebothtypesofinformation.Finally,inour
proposedtopic-basedframeworkTopTF,adocument’sweightforaqueryisgivenbythesumof
itsweightsforeachterminthequery.
|     |             |     | ∑   |               |     | ∑          |     | ∑         |     |
| --- | ----------- | --- | --- | ------------- | --- | ---------- | --- | --------- | --- |
|     | TopTF(q,d)= |     |     | w(q,d)=(1−𝜆)⋅ |     | w′(q,d)+𝜆⋅ |     | w′′(q,d), |     |
(16)
|     |     |     |     | i   |     | i   |     | i   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | q∈q |     |     | q∈q |     | q∈q |     |
|     |     |     | i   |     |     | i   |     | i   |     |
wherewisthetermweightobtainedfromEquation(15).Thetwoweightsarenormalizedinde-
pendentlyto[0,1]withthemin-maxnormalization x−x min ,whereastheywerenotnormalized
x m ax −x min
| inourpreviouswork.1 |     | When𝜆equals0,ourTopTFb |     |     |     |                                       |     |     |     |
| ------------------- | --- | ---------------------- | --- | --- | --- | ------------------------------------- | --- | --- | --- |
|                     |     |                        |     |     |     | e com esthetraditionalmodel(eg,BM25), |     |     |     |
and when 𝜆 equals 1, TopTF becomes the LDA model. In particular, we incorporate LDA into
| BM25andBM25 | QL                            | asLDA-BM25andLAD-BM25 |     |     | QL  | ,respectively. |     |     |     |
| ----------- | ----------------------------- | --------------------- | --- | --- | --- | -------------- | --- | --- | --- |
| 3.2.2       | Embedding-basedretrievalmodel |                       |     |     |     |                |     |     |     |
Topic-basedretrievalmodelscansuccessfullycapturebothexplicitterm-basedrelatedinforma-
tionandimplicittopic-basedsemanticinformation.However,document-levelinformationisnot

| 12  |     |     |     |     |     | JIANetal. |
| --- | --- | --- | --- | --- | --- | --------- |
considered. Inspired by the recent work of Doc2Vec,22 a pretrained document embedding for
documentsimilaritythathasbeenwidelyadoptedandachievedsuccessinmanyNLPtasks,we
proposedasimpleembedding-basedretrievalmodel:EmbedIR.In2014,LeandMikolovproposed
adistributedrepresentationofsentencesanddocumentsthatcouldachievethequeryembedding
vectorV andthedocumentembeddingvectorV
| q   |     |     | d .Then,thesimilaritybetweenadocumentd |     |     |     |
| --- | --- | --- | -------------------------------------- | --- | --- | --- |
andaqueryqisadoptedasthecosinevaluebetweenV andV ,whichisformulatedasfollows:
|     |     |                   | q   | d   |     |      |
| --- | --- | ----------------- | --- | --- | --- | ---- |
|     |     | sim(q,d)=cosine(V | ,V  | ),  |     |      |
|     |     |                   | q d |     |     | (17) |
Our proposed EmbedIR utilizes the similarity between documents and queries to improve
the performance of traditional retrieval models at the document level using the following
formula:
∑
|     | EmbedIR(q,d)=(1−𝛾)⋅ |     | w′(q,d)+𝛾 | ⋅sim(q,d), |     | (18) |
| --- | ------------------- | --- | --------- | ---------- | --- | ---- |
i
q∈q
i
wherew′(q,d)isthetermweightinadocumentdobtainedfromatraditionalretrievalmodel
i
(eg,BM25),andthefirstcomponentisalsonormalizedbymin-maxnormalization.sim(q,d)is
thesimilaritybetweenthedocumentandqueryobtainedfromEquation(17).𝛾
isthecoefficient
used to balance the importance of two components.When𝛾 issetto 0,EmbedIRbecomesthe
traditionalmodel,andwhen𝛾
issetto1,EmbedIRbecomesthesimilarityofembeddingvectors.
3.2.3 Enhancedtopic-basedretrievalmodelbasedonembedding
Tocapturetheinformationbetweenaqueryandadocumentatthetermlevel,thelatenttopic
level,andthewordvectorlevelsimultaneously,wecanusethepredefinedembedding-basedsim-
ilaritytoenhancethetopic-basedretrievalmodels.Adocument’sweightforagivenqueryinthe
enhancedTopTF(ETopTF)frameworkispresentedasfollows:
|                  |     | ∑     | ∑           |            |            |     |
| ---------------- | --- | ----- | ----------- | ---------- | ---------- | --- |
| ETopTF(q,d)=(1−𝜆 |     | −𝜆 )⋅ | w′(q,d)+𝜆 ⋅ | w′′(q,d)+𝜆 | ⋅sim(q,d), |     |
(19)
|     |     | 1 2 | i 1 | i   | 2   |     |
| --- | --- | --- | --- | --- | --- | --- |
|     |     | q∈q | q∈q |     |     |     |
i
in which w′(q,d), w′′(q,d) and sim(q,d) are obtained from the traditional retrieval model,
| i   | i   |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
topic-based retrieval and embedding-based retrieval model, respectively, and 𝜆 , 𝜆 are the
|     |     |     |     |     | 1 2 |     |
| --- | --- | --- | --- | --- | --- | --- |
coefficientsusedtosmooththethreecomponents,where𝜆 +𝜆 shouldbebetween0and1.
1 2
| 4 EXPERIMENTAL |     | SETTINGS |     |     |     |     |
| -------------- | --- | -------- | --- | --- | --- | --- |
4.1 Datasetsandevaluationmeasures
We conduct extensive experiments on 14 standard TREC collections, including newswire arti-
cles from various sources and a general web crawl of web documents. The test collections are
split into AP90, AP88-89, AP88-90, DISK1&2, DISK4&5, TREC8, ROBUST04, FBIS, FT, LA,
WSJ, SJMN, WT2G, WT10G, and GOV2 by source or year. These data sets are different in size
genre.16,40
and The statistics associated with each collection are presented in Table 2. As we

JIANetal. 13
| TABLE 2    | Informationaboutthetestcollections |        |                 |                 |
| ---------- | ---------------------------------- | ------ | --------------- | --------------- |
| Collection | NumberofDocs                       | Size   | Queries         | NumberofQueries |
| AP90       | 78321                              | 0.23Gb | 51-100          | 50              |
| AP88-89    | 164597                             | 0.50Gb | 51-100          | 50              |
| AP88-90    | 242918                             | 0.73Gb | 51-150          | 100             |
| DISK1&2    | 741853                             | 1.92Gb | 51-150          | 100             |
| DISK4&5    | 528155                             | 1.86Gb | 301-450         | 150             |
| TREC8      | 528155                             | 1.86Gb | 401-450         | 50              |
| ROBUST04   | 528155                             | 1.86Gb | 301-450&601-700 | 250             |
| FBIS       | 130471                             | 0.47Gb | 351-450         | 100             |
| FT         | 210158                             | 0.56Gb | 301-400         | 100             |
| LA         | 131896                             | 0.48Gb | 301-400         | 100             |
| SJMN       | 90257                              | 0.29Gb | 51-150          | 100             |
| WSJ        | 173252                             | 0.51Gb | 151-200         | 50              |
| WT2G       | 247491                             | 2.14Gb | 401–450         | 50              |
| WT10G      | 1692096                            | 10Gb   | 451-550         | 100             |
| GOV2       | 25178548                           | 426Gb  | 701-850         | 150             |
can see from this table, a relatively large number of queries are tested against the proposed
methods.
Forfaircomparisonwithstate-of-the-artmodels,weonlyusethetitlefieldoftheTRECqueries
inalltheexperimentsforretrieval.Thisisclosertotheactualqueriesusedintherealapplica-
tion.Querieswithoutjudgmentsareremoved.Foralltestcollectionsused,thetermsarestemmed
byusingPorter’sEnglishstemmer.StandardEnglishstopwordsareremoved.TheofficialTREC
evaluationmeasure,theMAP,isusedinourexperiments.Toinvestigatethetopretrieveddocu-
ments,P@5andP@20arealsousedforevaluation.AllstatisticaltestsarebasedontheWilcoxon
matched-pairsigned-ranktest.AllexperimentsareconductedwithLucene.∗Thesourcecodewill
bemadepubliclyavailableathttps://github.com/jfhrecoba/TopTFuponacceptanceofthepaper.
4.2 IntegratingtopicintoMATFandLM
Todemonstratetheeffectivenessofourtopic-basedIRframework,hereweextendtointegratethe
LDAmodelintotwostate-of-the-arttraditionalmodels,MATFandLM,denotedasLDA-MATF
andLDA-LM,respectively.
4.2.1 MATF
In 2013, Paik30 proposed a novel TF-IDF term weighting scheme MATF that employed two
differentwithindocumentTFnormalizationstocapturetwodifferentaspectsoftermsaliency.
∗https://lucene.apache.org/.

14 JIANetal.
OnecomponentisRelativeIntradocumentTF(RITF),definedas
(1+tf(q,d))
log
|     |     | RITF(q,d)= |     |     | 2   | i , |     | (20) |
| --- | --- | ---------- | --- | --- | --- | --- | --- | ---- |
i
|     |     |     |     | log | (1+avgtf(d)) |     |     |     |
| --- | --- | --- | --- | --- | ------------ | --- | --- | --- |
2
where tf(q,d) and avgtf(d) denote the frequency of the term q in d and the average term
| i   |     |     |     |     |     | i   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
frequencyofd,respectively.TheotherisLengthRegularizedTF(LRTF),definedas
|     |     |                       |     |     | (   | )      |     |      |
| --- | --- | --------------------- | --- | --- | --- | ------ | --- | ---- |
|     |     | LRTF(q,d)=tf(q,d)⋅log |     |     |     | avdl , |     |      |
|     |     |                       |     |     | 1+  |        |     | (21) |
|     |     |                       | i   | i   | 2   | dl     |     |      |
wheredlandavdldenotethelengthofthedocumentdandtheaveragedocumentlengthinthe
collection,respectively.RITF iseffectiveforshortqueries,whileLRTF performsbetteronlong
queries.Then,thetermdiscriminationfactor(TDF)isdefinedas
|     |     |         |     | cf(q)∕n(q) |        | N+1 |     |      |
| --- | --- | ------- | --- | ---------- | ------ | --- | --- | ---- |
|     |     | TDF(q)= |     | i          | i ⋅log | ,   |     | (22) |
i
|     |     |     | 1+cf(q)∕n(q) |     |     | n(q) |     |     |
| --- | --- | --- | ------------ | --- | --- | ---- | --- | --- |
|     |     |     |              | i   | i   | i    |     |     |
where cf(q) is the frequency of q over the collection, n(q) is the number of documents
| i   |     |     | i   |     |     | i   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
containingtermq,andN i isthenumberofindexeddocumentsinthecollection.
Finally, we use function f(x)= x to normalize RITF and LRTF, and the final weight
1+x
of a query term q for document is measured by taking a weighted combination of
i
these components, which is determined on the basis of the length of the corresponding
query.
|          | (   |           |     |         |           | )          |     |     |
| -------- | --- | --------- | --- | ------- | --------- | ---------- | --- | --- |
|          |     | RITF(q,d) |     |         | LRTF(q,d) |            |     |     |
| w′(q,d)= | 𝜔⋅  |           | i   | +(1−𝜔)⋅ |           | i ⋅TDF(q), |     |     |
(23)
| i   |     | 1+RITF(q,d) |     |     | 1+LRTF(q,d) |     | i   |     |
| --- | --- | ----------- | --- | --- | ----------- | --- | --- | --- |
|     |     |             | i   |     |             | i   |     |     |
where 𝜔= 2 is a query length factor. As a result, in the MATF model, a document’s
1+log(1+ql) 2
weightforaqueryisgivenbythesumofitsweightforeachterminthequery:
∑
|     |     |     | MATF(q,d)= |     | w′(q,d), |     |     | (24) |
| --- | --- | --- | ---------- | --- | -------- | --- | --- | ---- |
i
q∈q
i
wherew′isthetermweightobtainedfromEquation(23),
Paik30 shows that MATF outperforms several well-known state-of-the-art TF-IDF baselines
withasignificantlylargemarginonasetofnewsandwebdatasets.
4.2.2 LM
Inalanguagemodel,31adocumentisrankedusingthefollowingformula:
|     |     |          | ∑   |          | ∑          |     |     |     |
| --- | --- | -------- | --- | -------- | ---------- | --- | --- | --- |
|     |     | LM(q,d)= |     | w′(q|d)= | logP(q|d), |     |     |     |
(25)
|     |     |     |     | i   |     | i   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | q∈q |     | q∈q |     |     |     |
|     |     |     | i   |     | i   |     |     |     |
whereP(q|d)isthedocumentlanguagemodel.
i

JIANetal. 15
Several approaches can smooth P(q|d) to avoid the unwanted probability of zero. Dirichlet
i
smoothingisoneofthemostpopularapproachesandisreportedtohavethebestaverageprecision
inmostcases.31,32TheconditionalprobabilityP(q|d)inthesametimeissmoothedby
i
𝜇
dl
P(q|d)= P (q|d)+ P (q|c), (26)
i dl+𝜇 ml i dl+𝜇 ml i
where 𝜇 is the Dirichlet smoothing parameter, P (q|d)= tf(q i ,d) is the document language
ml i dl
model, P (q|c)= cf(q i ) is the collection language model, c represents the collection, cl is
ml i cl
the total number of terms in the collection, and cf(q) is the frequency of q over the
i i
collection.
4.3 Parametersettings
To test the effectiveness of BM25 , in BM25, parameters k and k are set to 1.2 and 8,
QL 1 3
respectively.Meanwhile,wesweepoverthevaluesofbfrom0to1.0withanintervalof0.05.In
CRTER ,thevalueofthenormalizationparameter𝜎 issweptinagroupofdifferentvalues2,5,
2
10,20,25,50,75,100,andthevalueofthebalancingparameter,𝜆issweptfrom0.1to0.9withan
intervalof0.1.CRTER usingatrianglekernelfunctioncanachievethebestMAPformostofthe
2
datasets.40,41TheparameterninTFnormalizationissweptfrom1to10withanintervalof1and
isrecommendedtobe2,6,and4inthelogarithmfunction,exponentialfunctionandreciprocal
function,respectively.
In topic-based test experiments, for fair comparisons, we use the following parameter set-
tingsforboththebaselinesandourproposedtopic-basedmodels,whichare popularintheIR
domain for building strong baselines. First, in BM25, setting k , k and b to 1.2, 8.0, and 0.35,
1 3
respectively, gives the best MAP for most data sets.41 Second, in Dirichlet LM, 𝜇 =1000 was
showntoachievethebestMAPformostdatasets.16Third,intheLDAmodel,weusesymmetric
Dirichletpriorswith𝛼=50/K and𝛽 =0.01,whicharecommonsettingsintheliterature.Ithas
t
been shown that retrieval results were not very sensitive to the values of these parameters.1,16
ThenumberoftopicsK issetto400asrecommended.1,16 Finally,wesweepthevaluesofbal-
t
ancingparameters𝜆,𝛾,𝜆 and𝜆 from0to1.0withanintervalof0.1inourTopTFandETopTF
1 2
frameworkandthedimofdocumentembeddingissweptinagroupofdifferentvalues100,200,
and300.
5 EXPERIMENTAL RESULTS
5.1 EffectivenessofBM25
QL
We first investigated the performance of our proposed BM25 compared with BM25.
QL
Experimental results are presented in Figure 3. As demonstrated in the figure, our pro-
posed BM25 models are comparable to BM25 with best b on almost all data sets in
QL
terms of MAP. Additionally, each TF normalization function has its advantage on some
aspects. There is no single function that outperforms all others on all the data sets. With-
out much knowledge of a new data set, the logarithmic function is recommended for
BM25 .
QL

| 16    |     |         |      |     |         |       |     | JIANetal. |
| ----- | --- | ------- | ---- | --- | ------- | ----- | --- | --------- |
|       |     | AP88−90 |      |     | AP88−89 |       |     | AP90      |
| 0.236 |     |         | 0.29 |     |         | 0.274 |     |           |
| 0.234 |     |         |      |     |         | 0.273 |     |           |
0.285
| 0.232 |     |     |      |     |     | 0.272 |     |     |
| ----- | --- | --- | ---- | --- | --- | ----- | --- | --- |
|       |     |     | 0.28 |     |     | 0.271 |     |     |
0.23
0.27
| 0.228 |     |     | 0.275 |     |     |           |     |     |
| ----- | --- | --- | ----- | --- | --- | --------- | --- | --- |
| PAM   |     |     | PAM   |     |     | PAM 0.269 |     |     |
| 0.226 |     |     | 0.27  |     |     |           |     |     |
0.268
0.224
|        | BM25       |     | 0.265  | BM25              |     | 0.267  | BM25       |     |
| ------ | ---------- | --- | ------ | ----------------- | --- | ------ | ---------- | --- |
| 0.222  | BM25QL EXP |     |        | BM25QL EXP        |     | 0.266  | BM25QL EXP |     |
|        | BM25QL LOG |     | 0.26   | B M 2 5 L O G     |     |        | BM25QL LOG |     |
| 0.22   |            |     |        | Q L               |     | 0.265  |            |     |
|        | BM25QL REC |     |        | B M 2 5 Q L R E C |     |        | BM25QL REC |     |
| 0.2180 |            |     | 0.2550 |                   |     | 0.2640 |            |     |
0.1 0.2 0.3 0.4 b−value 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 b−value 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 b−value 0.5 0.6 0.7 0.8 0.9 1.0
|      |     | DISK1&2 |      |     | DISK4&5 |       |     | FBIS |
| ---- | --- | ------- | ---- | --- | ------- | ----- | --- | ---- |
| 0.25 |     |         | 0.23 |     |         | 0.275 |     |      |
0.27
| 0.24 |     |     | 0.225 |     |     |     |     |     |
| ---- | --- | --- | ----- | --- | --- | --- | --- | --- |
0.26
0.23
0.22
0.25
0.22
| PAM |     |     | PAM 0.215 |     |     | PAM |     |     |
| --- | --- | --- | --------- | --- | --- | --- | --- | --- |
0.24
0.21
0.21
| 0.2   | BM25             |     |       | BM25       |     | 0.23  | BM25       |     |
| ----- | ---------------- | --- | ----- | ---------- | --- | ----- | ---------- | --- |
|       | B M 2 5 E XP     |     |       | BM25QL EXP |     |       | BM25QL EXP |     |
|       | Q L              |     | 0.205 |            |     |       |            |     |
| 0.19  | B M 2 5 Q L LO G |     |       | BM25QL LOG |     | 0.22  | BM25QL LOG |     |
|       | BM25QL REC       |     |       | BM25QL REC |     |       | BM25QL REC |     |
| 0.180 |                  |     | 0.20  |            |     | 0.210 |            |     |
0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|       |     | b−value |       |     | b−value |       |     | b−value  |
| ----- | --- | ------- | ----- | --- | ------- | ----- | --- | -------- |
|       |     | FT      |       |     | LA      |       |     | ROBUST04 |
| 0.265 |     |         | 0.255 |     |         | 0.255 |     |          |
| 0.26  |     |         | 0.25  |     |         | 0.25  |     |          |
|       |     |         | 0.245 |     |         | 0.245 |     |          |
0.255
|     |     |     | 0.24 |     |     | 0.24 |     |     |
| --- | --- | --- | ---- | --- | --- | ---- | --- | --- |
0.25
| PAM |     |     | PAM 0.235 |     |     | PAM |     |     |
| --- | --- | --- | --------- | --- | --- | --- | --- | --- |
0.235
| 0.245 |     |     | 0.23 |     |     |     |     |     |
| ----- | --- | --- | ---- | --- | --- | --- | --- | --- |
0.23
0.225
| 0.24  | BM25              |     |       | B M 2 5       |     | 0.225 | BM25       |     |
| ----- | ----------------- | --- | ----- | ------------- | --- | ----- | ---------- | --- |
|       | BM25QL EXP        |     | 0.22  | B M 2 5QL EXP |     |       | BM25QL EXP |     |
| 0.235 | B M 2 5 L O G     |     |       | BM25QL LOG    |     | 0.22  | BM25QL LOG |     |
|       | B M 2 5 Q L R E C |     | 0.215 | BM25QL REC    |     |       | BM25QL REC |     |
Q L
0.230 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.210 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.2150 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|       |     | b−value |       |     | b−value |      |     | b−value |
| ----- | --- | ------- | ----- | --- | ------- | ---- | --- | ------- |
|       |     | SJMN    |       |     | TREC8   |      |     | WSJ     |
| 0.22  |     |         | 0.245 |     |         | 0.34 |     |         |
| 0.215 |     |         | 0.24  |     |         | 0.33 |     |         |
0.32
| 0.21 |     |     | 0.235 |     |     |     |     |     |
| ---- | --- | --- | ----- | --- | --- | --- | --- | --- |
0.31
| PAM 0.205 |     |     | PAM 0.23 |     |     | PAM |     |     |
| --------- | --- | --- | -------- | --- | --- | --- | --- | --- |
0.3
| 0.2   |             |      | 0.225  |            |     |       |            |     |
| ----- | ----------- | ---- | ------ | ---------- | --- | ----- | ---------- | --- |
|       | BM25        |      |        | BM25       |     | 0.29  | BM25       |     |
|       | B M 2 5     | E XP |        | BM25QL EXP |     |       | BM25QL EXP |     |
| 0.195 | B M 2 5 Q L | LO G | 0.22   | BM25QL LOG |     |       | BM25QL LOG |     |
|       | Q L         |      |        |            |     | 0.28  |            |     |
|       | BM25QL      | REC  |        | BM25QL REC |     |       | BM25QL REC |     |
| 0.190 |             |      | 0.2150 |            |     | 0.270 |            |     |
0.1 0.2 0.3 0.4 b−value 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 b−value 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 b−value 0.5 0.6 0.7 0.8 0.9 1.0
|     |     | 0.21 | WT10G |     | 0.33 | WT2G |     |     |
| --- | --- | ---- | ----- | --- | ---- | ---- | --- | --- |
|     |     | 0.2  |       |     | 0.32 |      |     |     |
0.19
0.3
0.18
0.28
0.17
|     |     | PAM  |     |     | PAM  |     |     |     |
| --- | --- | ---- | --- | --- | ---- | --- | --- | --- |
|     |     | 0.16 |     |     | 0.26 |     |     |     |
0.15
0.24
|     |     | 0.14 BM25 EXP   |                 |         | BM25 EXP        |             |             |         |
| --- | --- | --------------- | --------------- | ------- | --------------- | ----------- | ----------- | ------- |
|     |     | BM25QL          |                 |         | BM25QL          |             |             |         |
|     |     | 0.13 BM25QL LOG |                 |         | 0.22 BM25QL LOG |             |             |         |
|     |     | BM25QL REC      |                 |         | BM25QL REC      |             |             |         |
|     |     | 0.120           |                 |         | 0.20            |             |             |         |
|     |     | 0.1 0.2         | 0.3 0.4 0.5 0.6 | 0.7 0.8 | 0.9 1.0 0.1 0.2 | 0.3 0.4 0.5 | 0.6 0.7 0.8 | 0.9 1.0 |
|     |     |                 | b−value         |         |                 | b−value     |             |         |
FIGURE 3 ComparisonBM25 QL withBM25intermsofMAP[Colorfigurecanbeviewedat
wileyonlinelibrary.com]

JIANetal. 17
One way to show the robustness of our proposed BM25 models is incorporating them
QL
into BM25-based models. In addition, we incorporate our proposed BM25 models into
QL
state-of-the-artBM25-basedmodelswithtermproximityapproaches.Zhaoetal40,41showedthat
the bigram cross-term model CRTER is at least comparable to the major probabilistic prox-
2
imity models PPM44 and BM25TP42 in the BM25-based framework. We compare our proposed
CRTER QLwithCRTER .TheresultsintermsofMAParepresentedinFigure4.Figure4shows
2 2
that the proposed CRTER QL models are also comparable to CRTER with best b on almost all
2 2
datasets.
From Tables 3 and 4, we can see that our proposed term frequency normalization
model consistently has good performance in all experiments. On some occasions, the per-
formance is even better than the heuristic best b-value. This is because the variable b
QL
is self-adjusted for each query, while given the heuristic b-value is tested for all queries
on a collection. The b is more adaptive, especially in real applications when the queries
QL
are quite different from each other. The functions proposed in Formula (9)-(11) show
similar performance in terms of MAP. Although more functions could be considered to
define the b , most of the functions grow faster than the logarithm function and slower
QL
compared with the exponential function. Based on the experimental results, we can see
that the retrieval performance can be guaranteed using any of the proposed functions
in Formula (9)-(11). Because logarithm function has a better overall performance, with-
out too much information about the data set, we recommend choosing the logarithm
function.
5.2 Performanceoftopic-basedhybridmodels
We investigate the performance of our proposed topic-based models compared with the
corresponding strong baselines BM25, MATF and Dirichlet LM. The experimental results
are presented in Tables 5 and 6. We did not present the results of LDA in Tables 5
and 6 because our TopTF always performs better than LDA and traditional models
when the 𝜆 values are between 0 and 1, that can be seen from Figure 5 in the next
section.
From Table 5, we can clearly see that our proposed LDA-BM25 and LDA-BM25 outper-
QL
formthecorrespondingbaselineBM25onalmostalldatasetsintermsofMAP,P@5andP@20.
StatisticallysignificantimprovementcanbeobservedonmostofthedatasetsintermsofMAP
and P@20. At the same time, according to the results, LDA-BM25 models are better than
QL
LDA-BM25inmostcases.Moreover,theresultsonceagainjustifytheeffectivenessofthreeTF
normalizationfunctions.
As shown from the results in Table 6, our extended topic-based models LDA-MATF
and LDA-LM also outperform the corresponding baselines MATF and LM on almost
all data sets in terms of MAP, P@5 and P@20, which could also show the supe-
riority of topic-based hybrid models. According to the results in Tables 5 and 6,
each topic-based hybrid model has an advantage in some aspects. However, there
is no single topic-based hybrid model that can achieve the best performance on all
datasets.

| 18    |     |         |       |     |         |       |     | JIANetal. |
| ----- | --- | ------- | ----- | --- | ------- | ----- | --- | --------- |
|       |     | AP88−90 |       |     | AP88−89 |       |     | AP90      |
| 0.238 |     |         | 0.298 |     |         | 0.278 |     |           |
0.295
| 0.236 |     |     |     |      |     | 0.277 |     |     |
| ----- | --- | --- | --- | ---- | --- | ----- | --- | --- |
| 0.234 |     |     |     | 0.29 |     | 0.276 |     |     |
0.275
| 0.232 |     |     | 0.285 |     |     |     |     |     |
| ----- | --- | --- | ----- | --- | --- | --- | --- | --- |
0.274
| PAM | 0.23 |     | PAM |      |     | PAM   |     |     |
| --- | ---- | --- | --- | ---- | --- | ----- | --- | --- |
|     |      |     |     | 0.28 |     | 0.273 |     |     |
0.228
|       |                |     | 0.275 |                   |     | 0.272 |               |     |
| ----- | -------------- | --- | ----- | ----------------- | --- | ----- | ------------- | --- |
| 0.226 | C R T E R E2XP |     |       | C R T E R E2XP    |     |       | C R T E R 2   |     |
|       | C R T E R      |     |       | C R T E R         |     | 0.271 | C R T E R EXP |     |
|       | CRTER2 2 LOG   |     |       | 0.27 CRTER2 2 LOG |     |       | CRTER2 2 LOG  |     |
| 0.224 |                |     |       |                   |     |       | 0.27          |     |
|       | CRTER2 REC     |     |       | CRTER2 REC        |     |       | CRTER2 REC    |     |
0.2220 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.2650 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.2690 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|     |      | b−value |       |     | b−value |     |     | b−value |
| --- | ---- | ------- | ----- | --- | ------- | --- | --- | ------- |
|     |      | DISK1&2 |       |     | DISK4&5 |     |     | FBIS    |
|     | 0.25 |         | 0.235 |     |         |     | 0.3 |         |
0.29
0.24
0.23
0.28
0.23
|     |      |     | 0.225 |     |     | 0.27     |     |     |
| --- | ---- | --- | ----- | --- | --- | -------- | --- | --- |
| PAM | 0.22 |     | PAM   |     |     | PAM 0.26 |     |     |
0.22
|     | 0.21           |     |       |                |     | 0.25  |                 |     |
| --- | -------------- | --- | ----- | -------------- | --- | ----- | --------------- | --- |
|     | C R T E R      |     |       | C R T E R      |     |       | C R T E R       |     |
|     | C R T E R E2XP |     |       | C R T E R E2XP |     | 0.24  | C R T E R 2 EXP |     |
|     | 0.2 2          |     | 0.215 | 2              |     |       | 2               |     |
|     | CRTER2 LOG     |     |       | CRTER2 LOG     |     | 0.23  | CRTER2 LOG      |     |
|     | CRTER2 REC     |     |       | CRTER2 REC     |     |       | CRTER2 REC      |     |
|     | 0.190          |     |       | 0.210          |     | 0.220 |                 |     |
0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|       |     | b−value |       |     | b−value |     |      | b−value  |
| ----- | --- | ------- | ----- | --- | ------- | --- | ---- | -------- |
|       |     | FT      |       |     | LA      |     |      | ROBUST04 |
| 0.275 |     |         | 0.258 |     |         |     | 0.26 |          |
0.255
0.27
|     |     |     |     | 0.25 |     | 0.255 |     |     |
| --- | --- | --- | --- | ---- | --- | ----- | --- | --- |
0.265
|       | 0.26 |     | 0.245 |      |     |       | 0.25 |     |
| ----- | ---- | --- | ----- | ---- | --- | ----- | ---- | --- |
| PAM   |      |     | PAM   | 0.24 |     | PAM   |      |     |
| 0.255 |      |     |       |      |     | 0.245 |      |     |
|       | 0.25 |     | 0.235 |      |     |       |      |     |
0.24
| 0.245 | CRTER2          |     |       | 0.23 CRTER2      |     |       | CRTER2     |     |
| ----- | --------------- | --- | ----- | ---------------- | --- | ----- | ---------- | --- |
|       | CRTER2 EXP      |     |       | C R T E R 2 E XP |     |       | CRTER2 EXP |     |
|       | 0.24 CRTER2 LOG |     | 0.225 | C R T E R LO G   |     | 0.235 | CRTER2 LOG |     |
|       | CRTER2 REC      |     |       | CRTER2 2 REC     |     |       | CRTER2 REC |     |
0.2350 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.220 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.230 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|       |      | b−value |     |      | b−value |       |      | b−value |
| ----- | ---- | ------- | --- | ---- | ------- | ----- | ---- | ------- |
|       |      | SJMN    |     |      | TREC8   |       |      | WSJ     |
|       | 0.22 |         |     | 0.26 |         |       | 0.35 |         |
| 0.218 |      |         |     |      |         | 0.345 |      |         |
0.255
| 0.216 |     |     |     |      |     |       | 0.34 |     |
| ----- | --- | --- | --- | ---- | --- | ----- | ---- | --- |
| 0.214 |     |     |     | 0.25 |     | 0.335 |      |     |
| 0.212 |     |     |     |      |     |       | 0.33 |     |
0.245
| PAM | 0.21 |     | PAM |     |     | PAM 0.325 |     |     |
| --- | ---- | --- | --- | --- | --- | --------- | --- | --- |
0.24
| 0.208 |        |     |        |                   |     |       | 0.32       |     |
| ----- | ------ | --- | ------ | ----------------- | --- | ----- | ---------- | --- |
| 0.206 | CRTER2 |     | 0.235  | CRTER2            |     | 0.315 | CRTER2     |     |
|       | CRTER2 | EXP |        | CRTER2 EXP        |     |       | CRTER2 EXP |     |
| 0.204 |        | LOG |        | L O G             |     |       | 0.31 LOG   |     |
| 0.202 | CRTER2 |     |        | 0.23 C R T E R 2  |     | 0.305 | CRTER2     |     |
|       | CRTER2 | REC |        | C R T E R 2 R E C |     |       | CRTER2 REC |     |
|       | 0.20   |     | 0.2250 |                   |     |       | 0.30       |     |
0.1 0.2 0.3 0.4 b−0v.a5lue0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4b−v0a.5lue0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4b−v0a.5lue 0.6 0.7 0.8 0.9 1.0
|     |     |       | WT10G |     |      | WT2G |     |     |
| --- | --- | ----- | ----- | --- | ---- | ---- | --- | --- |
|     |     | 0.225 |       |     | 0.35 |      |     |     |
0.22
0.34
0.21
0.32
0.2
0.19
|     |     | PAM |     |     | PAM 0.3 |     |     |     |
| --- | --- | --- | --- | --- | ------- | --- | --- | --- |
0.18
|     |     | 0.17   |     |     | 0.28   |     |     |     |
| --- | --- | ------ | --- | --- | ------ | --- | --- | --- |
|     |     | CRTER2 |     |     | CRTER2 |     |     |     |
0.16
|        |     | CRTER2 EXP        |                  |         | 0.26 CRTER2 EXP                         |                  |         |         |
| ------ | --- | ----------------- | ---------------- | ------- | --------------------------------------- | ---------------- | ------- | ------- |
|        |     | 0.15 CRTER2 LOG   |                  |         | CRTER2 LOG                              |                  |         |         |
|        |     | CRTER2 REC        |                  |         | CRTER2 REC                              |                  |         |         |
|        |     | 0 0.1 0.2 0.3     | 0.4b−0v.a5lue0.6 | 0.7 0.8 | 0.9 1.0 0.240 0.1 0.2 0.3               | 0.4b−v0a.5lue0.6 | 0.7 0.8 | 0.9 1.0 |
| FIGURE |     | 4 ComparisonCRTER | QLwithCRTER      |         |                                         |                  |         |         |
|        |     |                   | 2                |         | 2 intermsofMAP[Colorfigurecanbeviewedat |                  |         |         |
wileyonlinelibrary.com]

| JIANetal. |                               |     |                        |     |     | 19  |
| --------- | ----------------------------- | --- | ---------------------- | --- | --- | --- |
| TABLE     | 3 SummaryofcomparisonwithBM25 |     | QL andBM25intermsofMAP |     |     |     |
DISK
DISK
|             | AP88-90 | AP88-89 | AP90 1&2      | 4&5    | FBIS   | FT     |
| ----------- | ------- | ------- | ------------- | ------ | ------ | ------ |
| BM25-b=0.35 | 0.2347  | 0.2854  | 0.2718 0.2402 | 0.2258 | 0.2460 | 0.2594 |
| BM25-b=0.4  | 0.2344  | 0.2838  | 0.2720 0.2396 | 0.2251 | 0.2403 | 0.2567 |
BM25-b=0.75
|            | 0.2290 | 0.2720 | 0.2731 0.2245 | 0.2163 | 0.2283 | 0.2462 |
| ---------- | ------ | ------ | ------------- | ------ | ------ | ------ |
| BM25-bestb | 0.2347 | 0.2882 | 0.2738 0.2402 | 0.2258 | 0.2701 | 0.2614 |
BM25 EXP 0.2346bc 0.2871abc 0.2716 0.2404abcd 0.2255bc 0.2522abc 0.2613abc
QL
BM25 LOG 0.2346bc 0.2867abc 0.2716 0.2411abcd 0.2262abcd 0.2497abc 0.2612abc
QL
BM25 REC 0.2348abcd 0.2865abc 0.2716 0.2406abcd 0.2264abcd 0.2509abc 0.2612abc
QL
|             | LA     | ROUST04 | SJMN TREC8    | WSJ    | WT10G  | WT2G   |
| ----------- | ------ | ------- | ------------- | ------ | ------ | ------ |
| BM25-b=0.35 | 0.2513 | 0.2510  | 0.2132 0.2448 | 0.3298 | 0.2037 | 0.3139 |
| BM25-b=0.4  | 0.2494 | 0.2504  | 0.2150 0.2434 | 0.3296 | 0.2006 | 0.3109 |
| BM25-b=0.75 | 0.2373 | 0.2397  | 0.2139 0.2343 | 0.3090 | 0.1793 | 0.2632 |
| BM25-bestb  | 0.2519 | 0.2510  | 0.2166 0.2448 | 0.3323 | 0.2050 | 0.3191 |
BM25 QL EXP 0.2508bc 0.2497c 0.2161abc 0.2430c 0.3320abc 0.1995c 0.3204abcd
BM25 LOG 0.2525abcd 0.2505bc 0.2155abc 0.2443bc 0.3335abcd 0.2029bc 0.3196abcd
QL
BM25 REC 0.2512bc 0.2506bc 0.2160abc 0.2445bc 0.3329abcd 0.2029bc 0.3203abcd
QL
Note:Itemsboldhighlightthebestresultineachgroup.“a,b,c,d”denotesourproposedmodelsoutperformBM25withthe
settingsforbas0.35,0.4,0.75andbest,respectively.
| TABLE | 4 SummaryofcomparisonwithCRTER |         | QLandCRTER   | intermsofMAP |      |     |
| ----- | ------------------------------ | ------- | ------------ | ------------ | ---- | --- |
|       |                                |         | 2            | 2            |      |     |
|       | AP88-90                        | AP88-89 | AP90 DISK1&2 | DISK4&5      | FBIS | FT  |
CRTER 2 -b=0.35 0.2368 0.2923 0.2774 0.2457 0.2320 0.2820 0.2708
CRTER -b=0.4 0.2367 0.2913 0.2770 0.2453 0.2312 0.2784 0.2640
2
CRTER -b=0.75 0.2314 0.2823 0.2749 0.2303 0.2226 0.2453 0.2505
2
CRTER -bestb 0.2369 0.2954 0.2775 0.2457 0.2332 0.2890 0.2723
2
CRTER EXP 0.2371abcd 0.2942abc 0.2472abcd 0.2344abcd 0.2855abc 0.2726abcd
| 2   |     |     | 0.2742 |     |     |     |
| --- | --- | --- | ------ | --- | --- | --- |
CRTER 2 LOG 0.2371abcd 0.2936abc 0.2748 0.2473abcd 0.2334abcd 0.2826abc 0.2723abC
CRTER REC 0.2371abcd 0.2939abc 0.2741 0.2472abcd 0.2337abcd 0.2840abc 0.2725abcd
2
|     | LA  | ROUST04 | SJMN TREC8 | WSJ | WT10G | WT2G |
| --- | --- | ------- | ---------- | --- | ----- | ---- |
CRTER 2 -b=0.35 0.2528 0.2574 0.2160 0.2555 0.3472 0.2137 0.3300
CRTER 2 -b=0.4 0.2510 0.2567 0.2172 0.2549 0.3458 0.2117 0.3261
CRTER -b=0.75 0.2462 0.2453 0.2167 0.2425 0.3282 0.1857 0.2861
2
CRTER -bestb 0.2533 0.2583 0.2189 0.2572 0.3472 0.2189 0.3432
2
CRTER EXP 0.2550abcd 0.2593abcd 0.2185abc 0.2559abc 0.3461bc 0.2153abc 0.3416abc
2
LOG 0.2549abcd 0.2584abcd 0.2178abc 0.2561abc 0.3477abcd 0.2145abc 0.3369abc
CRTER 2
CRTER 2 REC 0.2549abcd 0.2590abcd 0.2191abcd 0.2563abc 0.3472bc 0.2145abc 0.3377abc
Note:Itemsboldhighlightthebestresultineachgroup.“a,b,c,d”denotesourproposedmodelsoutperformCRTER
2with
thesettingsforbas0.35,0.4,0.75andbest,respectively.

20 JIANetal.
)seunitnoC(
|     |     | )%53.3+( | )%78.2−( | )%00.2+( | )%77.1+( | )%78.2−( | )%87.3+( | )%40.2+( | )%10.4−( )%98.2+( |
| --- | --- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ----------------- |
4952.0 3663.0 3532.0 *1862.0 8553.0 0042.0 *0462.0 8553.0 *2442.0 *7462.0 6153.0 *1242.0
TF
|     |         | )%94.5+( |         | )%21.2+( | )%30.7+( | )%77.2−( | )%32.0−( | )%16.5+( | )%76.0−( )%71.1+( |
| --- | ------- | -------- | ------- | -------- | -------- | -------- | -------- | -------- | ----------------- |
|     | *5952.0 |          | )%00.0( |          |          |          | *8952.0  |          |                   |
SIBF 0642.0 0853.0 2462.0 0853.0 8962.0 3362.0 1843.0 6362.0 6553.0 3762.0
5&4KSID
|               |         | )%18.3+( | )%89.4+( | )%94.1+( | )%36.3+( | )%93.4+( | )%82.0+( | )%52.4+( | )%97.3+( )%12.1+( |
| ------------- | ------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ----------------- |
|               | *4432.0 | *7874.0  |          | *0432.0  |          |          | *4532.0  |          |                   |
| 8522.0 0654.0 | 3263.0  |          | 7763.0   |          | 0674.0   | 3363.0   |          | 3374.0   | 7663.0            |
2&1KSID
|     |         | )%54.8+( | )%25.6+( | )%14.5+( | )%38.8+( | )%15.4+( | )%43.5+( | )%38.8+( | )%62.6+( )%62.5+( |
| --- | ------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ----------------- |
|     | *5062.0 | *7665.0  | *0105.0  | *4162.0  | *0655.0  | *7005.0  | *4162.0  | *3565.0  | *3005.0           |
2042.0 0235.0 3574.0
|     |         |          |          |          | )%43.01+( |          |          | )%65.01+( |                   |
| --- | ------- | -------- | -------- | -------- | --------- | -------- | -------- | --------- | ----------------- |
|     |         | )%17.9+( | )%33.4+( | )%83.2+( |           | )%74.3+( | )%24.3+( |           | )%06.2+( )%07.3+( |
|     | *2892.0 |          |          | *9992.0  |           |          | *5003.0  |           |                   |
09PA 8172.0 4984.0 2304.0 6015.0 8214.0 4605.0 0714.0 1205.0 1814.0
98-88PA )%97.8+( )%36.3+( )%51.7+( )%40.9+( )%45.4+( )%09.7+( )%09.8+( )%27.2+( )%71.8+(
|               | *5013.0 |           | *6824.0 | *2113.0 |           | *6134.0 | *8013.0 |           | *7234.0 |
| ------------- | ------- | --------- | ------- | ------- | --------- | ------- | ------- | --------- | ------- |
| 4582.0 0944.0 | 0004.0  | 3564.0    |         |         | 4964.0    |         |         | 2164.0    |         |
|               |         | )%07.21+( |         |         | )%28.21+( |         |         | )%19.21+( |         |
09-88PA )%47.3+( )%61.7+( )%28.0+( )%61.7+( )%32.1+( )%40.7+(
|               | *5462.0 |        | *0644.0 | *8462.0 |        | *0644.0 | *0562.0 |        | *5544.0 |
| ------------- | ------- | ------ | ------- | ------- | ------ | ------- | ------- | ------ | ------- |
| 7432.0 9684.0 | 2614.0  | 1505.0 |         |         | 9094.0 |         |         | 9294.0 |         |
senilesabdnaFTpoThtiwnosirapmoC
cirteMlavE
| PAM | 02@P PAM |     | 02@P | PAM      |     | 02@P | PAM      |     | 02@P |
| --- | -------- | --- | ---- | -------- | --- | ---- | -------- | --- | ---- |
| 5@P |          | 5@P |      |          | 5@P |      |          | 5@P |      |
|     |          |     |      | PXE      |     |      | GOL      |     |      |
|     |          |     |      | LQ       |     |      | LQ       |     |      |
|     | 52MB-ADL |     |      | 52MB-ADL |     |      | 52MB-ADL |     |      |
5
ELBAT
52MB

| JIANetal. |     |     |     |     |     |     |     |     |     | 21  |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
)seunitnoC(
|     | )%61.2+(       | )%10.4−( | )%01.3+( |        |         |          |          |          |          |                   |
| --- | -------------- | -------- | -------- | ------ | ------- | -------- | -------- | -------- | -------- | ----------------- |
|     |                |          |          |        |         | )%16.2+( | )%47.0−( | )%70.4+( | )%04.4+( | )%07.3−( )%72.1+( |
|     | *0562.0 6153.0 | *6242.0  | G2TW     | 0045.0 | *1223.0 |          | *0904.0  | *7723.0  |          |                   |
|     |                |          |          | 9313.0 | 0393.0  | 0635.0   |          |          | 0025.0   | 0893.0            |
TF
)%81.6+( )%70.2−( )%04.1+( )%75.1+( )%21.1−( )%75.0−( )%60.2+( )%40.5−( )%01.4−(
|     | *2162.0 |     | G01TW |     | *9602.0 |     |     |     |     |     |
| --- | ------- | --- | ----- | --- | ------- | --- | --- | --- | --- | --- |
SIBF 6053.0 9762.0 7302.0 3563.0 2162.0 2163.0 7952.0 9702.0 9643.0 5052.0
5&4KSID )%73.6+( )%11.5+( )%52.4+( )%88.6+( )%29.2+( )%73.5+(
|     | )%52.4+( | )%22.3+( | )%12.1+( |     | *8053.0 |     |     | *5253.0 |     | *0174.0 |
| --- | -------- | -------- | -------- | --- | ------- | --- | --- | ------- | --- | ------- |
*4532.0 7074.0 7663.0 8923.0 0845.0 0744.0 0675.0 0664.0 0465.0
JSW
|         |     |     |       |     |         | )%88.5+( | )%47.5+( | )%41.8+( | )%93.5+( | )%20.9+( )%43.5+( |
| ------- | --- | --- | ----- | --- | ------- | -------- | -------- | -------- | -------- | ----------------- |
| 2&1KSID |     |     | 8CERT |     | *2952.0 |          | *0524.0  |          |          |                   |
)%78.8+( )%20.5+( )%74.5+( 8442.0 0884.0 0393.0 0615.0 *0852.0 0235.0 *0414.0
|     | *5162.0 *7855.0 | *3105.0 |     |     |     |           |          |          |           |          |
| --- | --------------- | ------- | --- | --- | --- | --------- | -------- | -------- | --------- | -------- |
|     |                 |         |     |     |     | )%47.01+( | )%65.0+( | )%81.8+( | )%59.21+( | )%53.9+( |
)%17.01+(
)%06.2+( )%22.4+( NMJS 2312.0 5473.0 9372.0 *1632.0 6673.0 *3692.0 *8042.0 5473.0 )%00.0( *5992.0
|     | *9003.0 1205.0 | 2024.0 |     |     |     |     |     |     |     |     |
| --- | -------------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
09PA
40TSUOR
98-88PA )%39.8+( )%64.5+( )%09.7+( )%05.4+( )%99.2+( )%26.2+( )%22.4+( )%94.2+( )%22.2+(
|     | *9013.0 | *6134.0 |     |               | *3262.0 | *6994.0 | *7463.0 | *6162.0 |        | *3363.0 |
| --- | ------- | ------- | --- | ------------- | ------- | ------- | ------- | ------- | ------ | ------- |
|     | 5374.0  |         |     | 0152.0 1584.0 | 4553.0  |         |         |         | 2794.0 |         |
)%28.21+( )%16.5+( )%74.4+( )%77.4+( )%35.6+( )%75.0+( )%56.3+(
| 09-88PA |     |     | )%09.6+( |     | *4562.0 |     |     | *7762.0 |     |     |
| ------- | --- | --- | -------- | --- | ------- | --- | --- | ------- | --- | --- |
*8462.0 )%00.0( *9444.0 3152.0 3763.0 5422.0 7383.0 2532.0 4963.0 7232.0
9684.0
AL
cirteMlavE
cirteMlavE
02@P
|     | PAM 5@P |     |     | PAM 5@P | 02@P PAM | 5@P | 02@P | PAM | 5@P | 02@P |
| --- | ------- | --- | --- | ------- | -------- | --- | ---- | --- | --- | ---- |
)deunitnoC(
|     | CER      |     |     |     |          |     |     | PXE      |     |     |
| --- | -------- | --- | --- | --- | -------- | --- | --- | -------- | --- | --- |
|     | LQ       |     |     |     |          |     |     | LQ       |     |     |
|     | 52MB-ADL |     |     |     | 52MB-ADL |     |     | 52MB-ADL |     |     |
5
ELBAT
52MB

22 JIANetal.
)deunitnoC(
5
ELBAT
TF
SIBF
5&4KSID
2&1KSID
09PA
98-88PA
09-88PA
cirteMlavE
*8623.0
5702.0
*9153.0
*9852.0
*4832.0
*7262.0
*1762.0
PAM
GOL
52MB-ADL
LQ
)%11.4+(
)%78.1+(
)%07.6+(
)%67.5+(
)%28.11+(
)%66.4+(
)%92.6+(
0235.0
0153.0
0465.0
0025.0
9083.0
8494.0
6773.0
5@P
)%84.1−(
)%19.3−(
)%29.2+(
)%65.6+(
)%17.1+(
)%00.2+(
)%08.2+(
0404.0
5152.0
0264.0
*0124.0
*0003.0
*5463.0
7632.0
02@P
)%08.2+(
)%17.3−(
)%63.3+(
)%21.7+(
)%35.9+(
)%65.2+(
)%34.5+(
*9623.0
8702.0
*0253.0
*9852.0
*5142.0
*8262.0
*0762.0
PAM
CER
52MB-ADL
LQ
)%41.4+(
)%10.2+(
)%37.6+(
)%67.5+(
)%72.31+(
)%07.4+(
)%52.6+(
0425.0
1353.0
0465.0
0425.0
5473.0
0494.0
5373.0
5@P
)%69.2−(
)%43.3−(
)%29.2+(
)%83.7+(
)%00.0(
)%38.1+(
)%96.1+(
0204.0
5152.0
*0864.0
*0814.0
*5003.0
*7463.0
7432.0
02@P
)%92.2+(
)%17.3−(
)%07.4+(
)%63.6+(
)%17.9+(
)%26.2+(
)%45.4+(
sriap-dehctamnoxocliW(senilesabgnidnopserrocrevostnemevorpmitnacifingisyllacitsitatsetoned)”*“(sratS.dlobnisitesatadhcaenodeniatbotlusertsebehT:etoN
.senilesabgnidnopserrocrevosledomdesoporpfotnemevorpmiegatnecrepehterawolebsegatnecrepehT.)50.0<Phtiwtsetsknar-dengis

JIANetal. 23
| TABLE | 6 SummaryofcomparisonwithLDA-MATFandMATF,LDA-LMandLM |               |               |               |
| ----- | ---------------------------------------------------- | ------------- | ------------- | ------------- |
|       | Eval AP                                              | AP            | DISK          |               |
|       | Metric 88-90                                         | 88-89 AP90    | DISK1&2 4&5   | FBIS FT       |
| MATF  | MAP 0.2354                                           | 0.2922 0.2772 | 0.2407 0.2350 | 0.2639 0.2621 |
|       | P@5 0.4707                                           | 0.4653 0.4851 | 0.5213 0.4800 | 0.3654 0.3579 |
|       | P@20 0.4111                                          | 0.4071 0.4191 | 0.4823 0.3767 | 0.2735 0.2353 |
LDA-MATF MAP 0.2636* 0.3121* 0.3028* 0.2608* 0.2419* 0.2758 0.2658*
(+11.98%) (+6.81%) (+9.24%) (+8.35%) (+2.94%) (+4.51%) (+1.41%)
|     | P@5 0.4828 | 0.4571 0.4936 | 0.5627* 0.4907 | 0.3877 0.3516 |
| --- | ---------- | ------------- | -------------- | ------------- |
(+2.57%) (−1.76%) (+1.75%) (+7.94%) (+2.23%) (+6.10%) (−1.76%)
|     | P@20 0.4394* | 0.4265* 0.4181 | 0.5047* 0.3860 | 0.2790 0.2374 |
| --- | ------------ | -------------- | -------------- | ------------- |
(+6.88%) (+4.77%) (−0.24%) (+4.64%) (+2.47%) (+2.01%) (+0.89%)
| LM  | MAP 0.2267  | 0.2822 0.2652 | 0.2337 0.2247 | 0.2618 0.2522 |
| --- | ----------- | ------------- | ------------- | ------------- |
|     | P@5 0.4646  | 0.4694 0.4723 | 0.5240 0.4453 | 0.3728 0.3558 |
|     | P@20 0.4152 | 0.4112 0.3979 | 0.4667 0.3547 | 0.2593 0.2347 |
LDA-LM MAP 0.2582* 0.3089* 0.2871* 0.2558* 0.2373* 0.2721 0.2740*
(+13.90%) (+9.46%) (+8.26%) (+9.46%) (+5.61%) (+3.93%) (+8.64%)
|     | P@5 0.5030 | 0.4776 0.4723 | 0.5573* 0.4547 | 0.3753 0.3642 |
| --- | ---------- | ------------- | -------------- | ------------- |
(+8.27%) (+1.75%) (0.00%) (+6.35%) (+2.11%) (+0.67%) (+2.36%)
|     | P@20 0.4369* | 0.4184 0.4032 | 0.4943* 0.3703* | 0.2710 0.2453* |
| --- | ------------ | ------------- | --------------- | -------------- |
(+5.23%) (+1.75%) (+1.33%) (+5.91%) (+4.40%) (+4.51%) (+4.52%)
Eval
|      | Metric LA   | ROUST04 SJMN  | TREC8 WSJ     | WT10G WT2G    |
| ---- | ----------- | ------------- | ------------- | ------------- |
| MATF | MAP 0.2554  | 0.2593 0.2157 | 0.2598 0.3303 | 0.2174 0.3330 |
|      | P@5 0.3612  | 0.4964 0.3809 | 0.5160 0.5360 | 0.3796 0.5400 |
|      | P@20 0.2245 | 0.3669 0.2766 | 0.4190 0.4450 | 0.2663 0.4130 |
LDA-MATF MAP 0.2679* 0.2694* 0.2346* 0.2701* 0.3511* 0.2198 0.3380
(+4.89%) (+3.90%) (+8.76%) (+3.96%) (+6.30%) (+1.10%) (+1.50%)
|     | P@5 0.3837* | 0.5084 0.3851 | 0.5240 0.5720 | 0.3755 0.5480 |
| --- | ----------- | ------------- | ------------- | ------------- |
(+6.23%) (+2.42%) (+1.10%) (+1.55%) (+6.72%) (−1.08%) (+1.48%)
|     | P@20 0.2347 | 0.3761* 0.2899 | 0.4380 0.4700* | 0.2689 0.4110 |
| --- | ----------- | -------------- | -------------- | ------------- |
(+4.54%) (+2.51%) (+4.81%) (+4.53%) (+5.62%) (+0.98%) (−0.48%)
| LM  | MAP 0.2500  | 0.2490 0.2067 | 0.2473 0.3266 | 0.2095 0.3092 |
| --- | ----------- | ------------- | ------------- | ------------- |
|     | P@5 0.3490  | 0.4803 0.3702 | 0.4960 0.5400 | 0.3571 0.5040 |
|     | P@20 0.2250 | 0.3552 0.2798 | 0.3930 0.4350 | 0.2663 0.3920 |
(Continues)

24 JIANetal.
TABLE 6 (Continued)
Eval AP AP DISK DISK
Metric 88-90 88-89 AP90 1&2 4&5 FBIS FT
LDA-LM MAP 0.2648* 0.2642* 0.2339* 0.2653* 0.3469* 0.2134* 0.3178
(+5.92%) (+6.10%) (+13.16%) (+7.28%) (+6.22%) (+1.86%) (+2.78%)
P@5 0.3735* 0.4916 0.3766 0.5080 0.5760 0.3531 0.5120
(+7.02%) (+2.35%) (+1.73%) (+2.42%) (+6.67%) (−1.12%) (+1.59%)
P@20 0.2342 0.3689* 0.2963* 0.4270* 0.4620* 0.2628 0.3900
(+4.09%) (+3.86%) (+5.90%) (+8.65%) (+6.21%) (−1.31%) (−0.51%)
Note:Stars“*”denotestatisticallysignificantimprovementsovercorrespondingbaselines(Wilcoxonmatched-pairs
signed-rankstestwithp<.05).Thepercentagesbelowarethepercentageimprovementsofproposedmodelsover
correspondingbaselines.
5.3 Parametersensitivity
An important issue that may affect the robustness of our proposed models is the sensi-
tivity of their parameter 𝜆 to retrieval performance. Since the weights of query terms in
traditional retrieval models and topic models are normalized independently, the value of 𝜆
reflects the influence of using a topic-based model. Figure 5 plots the evaluation metrics
MAP obtained by the proposed hybrid models over 𝜆 values ranging from 0 to 1 on all
the data sets. It is clear that hybrid models perform better than either traditional models
or topic models on all data sets. As shown in Figure 5, our proposed models LDA-BM25 ,
QL
LDA-BM25,LDA-MATF,andLDA-LMgenerallyperformwelloverdifferentdatasetswhen𝜆is
near0.5.
5.4 Rerankingfortopic-basedhybridmodels
Intopic-basedIRmodels,thetopicmodelisamaintime-consumingpart.Forexample,thecom-
plexityoftheGibbssamplinginLDAmodelislinearwiththenumberofiterations,thenumber
oftopicsthenumberofdocumentsandtheaveragenumberoftokensinonedocument.16 Asa
result,itisdifficulttoimplementtopic-basedIRmodelsonaverylargedataset,suchasGOV2.
Fortunately,rerankingisagoodapproachininformationretrievaltoreducethecomputational
complexity and running time.41 In the first retrieval pass, we use the traditional IR model to
retrieve.Then,weimplementourtopic-basedhybridmodelsonthetop-Nr(eg,Nr=1000)doc-
umentsinthefirstpasstorerankthem.BecauseNr≪N,thecomputationalcomplexityandthe
runningtimeofLDAcanbegreatlyreduced,soourexperimentscanbeconductedonthevery
largedatasetGOV2.
Table7presentsthererankingresultsofourtopic-basedhybridmodelsonfiverepresentative
data sets. From Table 7, we can see that the reranking results of our topic-based hybrid mod-
els significantly outperform traditional models in terms of MAP in almost all cases. Generally
speaking,inthesameretrievalmodel,theperformanceofrerankingmaydecrease.Accordingto
Tables5-7,thererankingresultsofourproposedtopic-basedhybridmodelsperformevenbetter
intermsofMAPonDISK4&5andWT10GandmoreorlessonWT2G.Therefore,itisreasonable
tobelievethatrerankingisaneffectiveandefficientapproachforourtopic-basedhybridmodels
inIR.

JIANetal. 25
|      |     | AP88−90 |      |     | AP88−89 |      |     | AP90 |
| ---- | --- | ------- | ---- | --- | ------- | ---- | --- | ---- |
| 0.27 |     |         | 0.32 |     |         | 0.31 |     |      |
| 0.26 |     |         |      |     |         | 0.3  |     |      |
0.3
| 0.24 |     |     |     |     |     | 0.28 |     |     |
| ---- | --- | --- | --- | --- | --- | ---- | --- | --- |
0.28
| 0.22 |     |     |     |     |     | 0.26 |     |     |
| ---- | --- | --- | --- | --- | --- | ---- | --- | --- |
0.26
| PAM |     |     | PAM |     |     | PAM  |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | --- |
| 0.2 |     |     |     |     |     | 0.24 |     |     |
0.24
|      | LDA−BM25       |     |       | LDA−BM25       |     |       | LDA−BM25       |     |
| ---- | -------------- | --- | ----- | -------------- | --- | ----- | -------------- | --- |
| 0.18 | LDA−BM25QL EXP |     | 0.22  | LDA−BM25QL EXP |     | 0.22  | LDA−BM25QL EXP |     |
|      | LDA−BM25QL LOG |     |       | LDA−BM25QL LOG |     |       | LDA−BM25QL LOG |     |
|      | REC            |     |       | REC            |     |       | REC            |     |
| 0.16 | LDA−BM25QL     |     | 0.2   | LDA−BM25QL     |     | 0.2   | LDA−BM25QL     |     |
|      | LDA−LM         |     |       | LDA−LM         |     |       | LDA−LM         |     |
|      | LDA−MATF       |     | 0.180 | LDA−MATF       |     | 0.180 | LDA−MATF       |     |
0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|      |     | λ       |      |     | λ       |      |     | λ    |
| ---- | --- | ------- | ---- | --- | ------- | ---- | --- | ---- |
|      |     | DISK1&2 |      |     | DISK4&5 |      |     | FBIS |
| 0.27 |     |         | 0.26 |     |         | 0.28 |     |      |
0.26
|     |     |     | 0.24 |     |     | 0.26 |     |     |
| --- | --- | --- | ---- | --- | --- | ---- | --- | --- |
0.24
|     |     |     | 0.22 |     |     | 0.24 |     |     |
| --- | --- | --- | ---- | --- | --- | ---- | --- | --- |
0.22
|     |     |     | 0.2 |     |     | 0.22 |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | --- |
0.2
|          |     |     | 0.18 |     |     | 0.2  |     |     |
| -------- | --- | --- | ---- | --- | --- | ---- | --- | --- |
| PAM 0.18 |     |     | PAM  |     |     | PAM  |     |     |
|          |     |     | 0.16 |     |     | 0.18 |     |     |
0.16 L D A − B M 2 5 EXP 0.14 L D A − B M 2 5 EXP 0.16 LDA−BM25 EXP
|      | L D A − B M 2 5QL   |     |       | L D A − B M 2 5QL   |     |      | LDA−BM25QL     |     |
| ---- | ------------------- | --- | ----- | ------------------- | --- | ---- | -------------- | --- |
| 0.14 | LDA−BM25QL LOG      |     | 0.12  | LDA−BM25QL LOG      |     | 0.14 | LDA−BM25QL LOG |     |
|      | L D A − B M25QL REC |     |       | L D A − B M25QL REC |     |      | LDA−BM25QL REC |     |
| 0.12 | L D A − LM          |     | 0.1   | L D A − LM          |     | 0.12 | LDA−LM         |     |
|      | LDA−MATF            |     |       | LDA−MATF            |     |      | LDA−MATF       |     |
| 0.10 |                     |     | 0.080 |                     |     | 0.10 |                |     |
0.1 0.2 0.3 0.4 0.5 λ 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 λ 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 λ 0.6 0.7 0.8 0.9 1.0
| 0.28 |     | FT  | 0.28 |     | LA  | 0.28 |     | ROBUST04 |
| ---- | --- | --- | ---- | --- | --- | ---- | --- | -------- |
| 0.26 |     |     |      |     |     | 0.26 |     |          |
0.26
0.24
0.24
|     |     |     | 0.24 |     |     | 0.22 |     |     |
| --- | --- | --- | ---- | --- | --- | ---- | --- | --- |
0.22
|         |     |     | 0.22 |     |     | 0.2 |     |     |
| ------- | --- | --- | ---- | --- | --- | --- | --- | --- |
| PAM 0.2 |     |     | PAM  |     |     | PAM |     |     |
0.18
| 0.18 |                |     | 0.2  |                           |     | 0.16 |                |     |
| ---- | -------------- | --- | ---- | ------------------------- | --- | ---- | -------------- | --- |
|      | LDA−BM25       |     |      | LDA−BM25                  |     |      | LDA−BM25       |     |
| 0.16 | LDA−BM25QL EXP |     |      | LDA−BM25QL EXP            |     | 0.14 | LDA−BM25QL EXP |     |
|      | LOG            |     | 0.18 | L O G                     |     |      | LOG            |     |
| 0.14 | LDA−BM25QL     |     |      | L D A − B M 2 5 Q L       |     | 0.12 | LDA−BM25QL     |     |
|      | LDA−BM25QL REC |     | 0.16 | L D A − B M 2 5 Q L R E C |     |      | LDA−BM25QL REC |     |
| 0.12 | LDA−LM         |     |      | LDA−LM                    |     | 0.1  | LDA−LM         |     |
|      | LDA−MATF       |     |      | LDA−MATF                  |     |      | LDA−MATF       |     |
0.10 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.080 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|      |     | λ    |      |     | λ     |      |     | λ   |
| ---- | --- | ---- | ---- | --- | ----- | ---- | --- | --- |
|      |     | SJMN |      |     | TREC8 |      |     | WSJ |
| 0.25 |     |      | 0.28 |     |       | 0.36 |     |     |
| 0.24 |     |      | 0.25 |     |       | 0.34 |     |     |
0.23
0.32
| 0.22 |     |     |     |     |     | 0.3 |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- |
0.2
| 0.21 |     |     |     |     |     | 0.28 |     |     |
| ---- | --- | --- | --- | --- | --- | ---- | --- | --- |
0.2
| PAM  |     |     | PAM  |     |     | PAM 0.26 |     |     |
| ---- | --- | --- | ---- | --- | --- | -------- | --- | --- |
| 0.19 |     |     | 0.15 |     |     |          |     |     |
0.24
| 0.18 | LDA−BM25       |     |     | L D A − B M 2 5       |     | 0.22 | LDA−BM25       |     |
| ---- | -------------- | --- | --- | --------------------- | --- | ---- | -------------- | --- |
| 0.17 | LDA−BM25QL EXP |     |     | L D A − B M 2 5QL EXP |     |      | LDA−BM25QL EXP |     |
|      | LDA−BM25QL LOG |     | 0.1 | LDA−BM25QL LOG        |     | 0.2  | LDA−BM25QL LOG |     |
| 0.16 | LDA−BM25QL REC |     |     | LDA−BM25QL REC        |     |      | LDA−BM25QL REC |     |
0.18
| 0.15 | LDA−LM LDA−MATF |     |       | LDA−LM LDA−MATF |     |      | LDA−LM LDA−MATF |     |
| ---- | --------------- | --- | ----- | --------------- | --- | ---- | --------------- | --- |
|      |                 |     | 0.050 |                 |     | 0.16 |                 |     |
0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0 0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
|     |     | λ    |       |     | λ    |      |     | λ   |
| --- | --- | ---- | ----- | --- | ---- | ---- | --- | --- |
|     |     |      | WT10G |     |      | WT2G |     |     |
|     |     | 0.23 |       |     | 0.35 |      |     |     |
0.22
0.2
0.3
0.18
|     |     | 0.16     |     |     | 0.25 |     |     |     |
| --- | --- | -------- | --- | --- | ---- | --- | --- | --- |
|     |     | PAM 0.14 |     |     | PAM  |     |     |     |
|     |     | 0.12     |     |     | 0.2  |     |     |     |
0.1
|     |     | L D A − B M 2 5 EXP    |               |             | 0.15 LDA−BM25 EXP  |               |             |     |
| --- | --- | ---------------------- | ------------- | ----------- | ------------------ | ------------- | ----------- | --- |
|     |     | 0.08 L D A − B M 2 5QL |               |             | LDA−BM25QL         |               |             |     |
|     |     | LDA−BM25QL LOG         |               |             | LDA−BM25QL LOG     |               |             |     |
|     |     | 0.06 LDA−BM25QL REC    |               |             | 0.1 LDA−BM25QL REC |               |             |     |
|     |     | 0.04 LDA−LM            |               |             | LDA−LM             |               |             |     |
|     |     | LDA−MATF               |               |             | LDA−MATF           |               |             |     |
|     |     | 0.020                  |               |             | 0.050              |               |             |     |
|     |     | 0.1 0.2 0.3            | 0.4 0.5 λ 0.6 | 0.7 0.8 0.9 | 1.0 0.1 0.2 0.3    | 0.4 0.5 λ 0.6 | 0.7 0.8 0.9 | 1.0 |
FIGURE 5 ParametersensitivityofλonalldatasetsintermsofMAP[Colorfigurecanbeviewedat
wileyonlinelibrary.com]

| 26  |     |     |     |     |     | JIANetal. |
| --- | --- | --- | --- | --- | --- | --------- |
ML-ADL )%29.4+( )%10.1−( )%97.2+( )%41.6+( )%10.3+( )%97.4+( )%62.1+( )%95.1+( )%18.2−( )%50.2+( )%00.4+( )seunitnoC(
| *2542.0 | *7974.0 | *5832.0 | *1313.0 |               | *8312.0 |        |
| ------- | ------- | ------- | ------- | ------------- | ------- | ------ |
|         | 7815.0  | 7854.0  | 7173.0  | 0215.0 0183.0 |         | 4173.0 |
7332.0 0425.0 7664.0 7422.0 3544.0 7453.0 2903.0 0405.0 0293.0 5902.0 1753.0
ML
)%70.5+( )%50.2+( )%93.1+( )%58.4+( )%87.4+( )%59.1+( )%47.0−( )%12.1−( )%54.3+( )%16.1−(
| FTAM *9252.0 |        | *4642.0 | )%00.0( *7493.0 *5933.0 |               |        |        |
| ------------ | ------ | ------- | ----------------------- | ------------- | ------ | ------ |
| -ADL         | 0235.0 |         |                         | 0635.0 0804.0 | 9422.0 | 5373.0 |
984.0
84.0
FTAM 7042.0 3125.0 3284.0 0532.0 0084.0 7673.0 0333.0 0045.0 0314.0 4712.0 6973.0
CER
)%02.4+( )%05.2−( )%16.2+( )%00.7+( )%29.2+( )%13.3+( )%98.3+( )%39.5−( )%67.0+( )%83.6+( )%76.1+(
LQ *3052.0 7815.0 7784.0 *6142.0 3964.0 3473.0 *1623.0 0805.0 0693.0 *7612.0 4173.0
-ADL 52MB
GOL
)%66.4+( )%42.0−( )%36.0+( )%61.6+( )%40.2+( )%75.1+( )%80.4+( )%22.2−( )%40.2+( )%34.6+( )%73.3+(
| LQ *4152.0 |               | *7932.0 | *7623.0 |               | *8612.0 |        |
| ---------- | ------------- | ------- | ------- | ------------- | ------- | ------ |
| -ADL 52MB  | 7035.0 3784.0 | 3564.0  | 0863.0  | 0825.0 0104.0 |         | 6773.0 |
PXE
)%92.4+( )%15.0+( )%04.2+( )%42.6+( )%15.3+( )%60.4+( )%14.3+( )%47.0−( )%52.0+( )%85.6+( )%21.1+(
| LQ *5052.0 | *7684.0 | *9932.0 | *0773.0 *6423.0 |               | *1712.0 |        |
| ---------- | ------- | ------- | --------------- | ------------- | ------- | ------ |
|            | 7435.0  | 0274.0  |                 | 0635.0 0493.0 |         | 4963.0 |
-ADL 52MB
gniknarerybdeniatbostluserlatnemirepxE
)%85.4+( )%00.4+( )%45.5+( )%29.2+( )%79.3+( )%73.1+( )%47.0−( )%35.1+( )%66.4+( )%19.3+(
| *2152.0   | )%00.0( *3494.0 | *3832.0 | *7673.0 |               | *2312.0 |        |
| --------- | --------------- | ------- | ------- | ------------- | ------- | ------ |
| -ADL 52MB | 0235.0          | 3964.0  | 2813.0  | 0635.0 0993.0 |         | 6973.0 |
|           | *3574.0         |         | *3263.0 |               |         |        |
52MB 2042.0 0235.0 8522.0 0654.0 9313.0 0045.0 0393.0 7302.0 3563.0
9661.0 7013.0 *7392.0 9831.0 7032.0 *3612.0 9900.0 0651.0 0741.0 0201.0
| ADL |     |     |     |     | 680.0 |     |
| --- | --- | --- | --- | --- | ----- | --- |
cirteM
|          | 02@P |         | 02@P | 02@P |     |     |
| -------- | ---- | ------- | ---- | ---- | --- | --- |
| lavE PAM | 5@P  | PAM 5@P | PAM  | 5@P  | PAM | 5@P |
7
| 2&1KSID |     | 5&4KSID |     |     |       |     |
| ------- | --- | ------- | --- | --- | ----- | --- |
| ELBAT   |     |         |     |     | G01TW |     |
G2TW

JIANetal. 27
egatnecrepehT.level50.ehttatsetsknar-dengissriap-dehctamnoxocliWehtotgnidroccatnemevorpmitnacifingisyllacitsitatsasetacidnilobmys”*“A:etoN
| ML-ADL | )%97.0+( )%69.0+( | )%22.0+( )%64.0+( |
| ------ | ----------------- | ----------------- |
*6303.0
| 4862.0 | 3795.0        | 2625.0 |
| ------ | ------------- | ------ |
| 3662.0 | 7003.0 0695.0 | 8325.0 |
ML
|             | )%57.0−( )%31.2+( | )%04.0+( )%29.1+( |
| ----------- | ----------------- | ----------------- |
| FTAM        | *9123.0           | *2375.0           |
| -ADL 3462.0 | 3256.0            |                   |
| FTAM 3662.0 | 2513.0 7946.0     | 4265.0            |
CER
| LQ     | )%91.0−( )%15.2+( | )%99.1+( )%96.2+( |
| ------ | ----------------- | ----------------- |
| 7062.0 | *8603.0 8816.0    | 3945.0            |
-ADL 52MB
GOL
|                  | )%75.0−( )%17.2+( | )%45.3+( )%75.1+( |
| ---------------- | ----------------- | ----------------- |
| LQ               | *4703.0           |                   |
| -ADL 52MB 7652.0 | 2826.0            | 3345.0            |
PXE
|     | )%59.1−( )%44.1+( | )%44.2−( )%70.1−( |
| --- | ----------------- | ----------------- |
LQ
| -ADL 52MB 1652.0 | 6303.0 9195.0     | 6045.0            |
| ---------------- | ----------------- | ----------------- |
|                  | )%00.1+( )%76.2+( | )%12.0−( )%73.0−( |
*3703.0
| -ADL 52MB 8362.0 | 4506.0        | 4506.0 |
| ---------------- | ------------- | ------ |
| 52MB 2162.0      | 3992.0 7606.0 | 9435.0 |
.tnemevorpmiehtsisesehtnerapehtni
| )deunitnoC( 3290.0 | 9202.0 3243.0 | 8623.0 |
| ------------------ | ------------- | ------ |
ADL
cirteM
| 02@P | PAM | 02@P |
| ---- | --- | ---- |
| lavE | 5@P |      |
7
ELBAT
2VOG

| 28    |                       |        |                       |         |         |      | JIANetal. |
| ----- | --------------------- | ------ | --------------------- | ------- | ------- | ---- | --------- |
| TABLE | 8 ComparisonwithCRTER |        | 2 andLBDMintermsofMAP |         |         |      |           |
|       |                       | LDA-   | LDA-                  | LDA-    | LDA-    |      | LDA-      |
|       |                       |        | EXP                   | LOG     | REC     |      |           |
|       | CRTER                 | 2 BM25 | BM25 QL               | BM25 QL | BM25 QL | LBDM | LM        |
AP88-90 0.2368 0.2645↑* 0.2648↑* 0.2650↑* 0.2648↑* 0.2623 0.2582
AP88-89 0.2923 0.3105↑* 0.3112↑* 0.3108↑* 0.3109↑* 0.3094 0.3089
| AP90     | 0.2774 | 0.2982↑  | 0.2999↑* | 0.3005↑* | 0.3009↑* | 0.2944 | 0.2871   |
| -------- | ------ | -------- | -------- | -------- | -------- | ------ | -------- |
|          |        | 0.2605↑* | 0.2614↑* | 0.2614↑* | 0.2615↑* |        | 0.2558↑↑ |
| DISK1&2  | 0.2457 |          |          |          |          | 0.2538 |          |
|          |        | 0.2344↑  | 0.2340↑  | 0.2354↑* | 0.2354↑* |        |          |
| DISK4&5  | 0.2303 |          |          |          |          | 0.2378 | 0.2373   |
| FBIS     | 0.2820 | 0.2595   | 0.2633   | 0.2598   | 0.2612   | 0.2802 | 0.2721   |
| FT       | 0.2708 | 0.2681   | 0.2640   | 0.2647   | 0.2650   | 0.2706 | 0.2740↑↑ |
|          |        | 0.2654↑  | 0.2677↑  | 0.2671↑  | 0.2670↑  |        | 0.2648↑↑ |
| LA       | 0.2528 |          |          |          |          | 0.2631 |          |
|          |        | 0.2623↑* | 0.2616↑* | 0.2627↑* | 0.2628↑* |        | 0.2642↑↑ |
| ROBUST04 | 0.2574 |          |          |          |          | 0.2617 |          |
SJMN 0.2160 0.2361↑* 0.2408↑* 0.2384↑* 0.2415↑* 0.2276 0.2339↑↑
| TREC8 | 0.2555 | 0.2592↑ | 0.2580↑ | 0.2589↑ | 0.2589↑ | 0.2585 | 0.2653↑↑ |
| ----- | ------ | ------- | ------- | ------- | ------- | ------ | -------- |
| WSJ   | 0.3472 | 0.3508↑ | 0.3525↑ | 0.3519↑ | 0.3520↑ | 0.3532 | 0.3469   |
| WT10G | 0.2137 | 0.2069  | 0.2079  | 0.2075  | 0.2078  | 0.2134 | 0.2134   |
0.3178↑↑
| WT2G | 0.3300 | 0.3221 | 0.3277 | 0.3268 | 0.3269 | 0.3116 |     |
| ---- | ------ | ------ | ------ | ------ | ------ | ------ | --- |
Note:A“*”symbolindicatesastatisticallysignificantimprovementaccordingtotheWilcoxonmatched-pairs
signed-rankstestatthe0.05level.Arrows“↑”denotetopic-basedmodelsoutperformCRTER ,whilearrows“↑↑”denote
2
LDA-LMoutperformsLBDM.
| 5.5 ComparisonwithCRTER |     |     |     | andLBDM |     |     |     |
| ----------------------- | --- | --- | --- | ------- | --- | --- | --- |
2
In addition, we compare our proposed models with two state-of-the-art approaches. Zhao
et al40,41 showed that the bigram cross-term model (CRTER2) is at least comparable to the
|     |     |     | PPM44 | BM25TP42 |     |     |     |
| --- | --- | --- | ----- | -------- | --- | --- | --- |
major probabilistic proximity models and in the BM25-based framework. Yi
and Allan showed LDA-based model (LBDM)16 achieves the best performance in topic-based
LM framework,52 which is closest to our proposed model LDA-LM. Hence, we make a direct
comparison with CRTER and LBDM. Results in terms of MAP are presented in Table 8.
2
Arrows “↑” denote LDA-BM25 outperforms CRTER , while arrows “↑↑” denote LDA-LM out-
2
performs LBDM. Among 14 data sets, LDA-BM25 and LDA-BM25 QL models all win 10 times,
and LDA-LM wins seven times. By comparison, we can conclude that our proposed models
LDA-BM25, LDA-BM25 and LDA-LM are at least comparable to the state-of-the-art models
QL
CRTER andLBDM.
2
5.6 Embedding-basedIRmodels:casestudies
Tofurtherevaluateourproposedmodels,wecomparetwolatestembedding-basedmodelsthat
areclosetoours.Oneisthewordembedding-basedgeneralizedlanguagemodel(GLM),24which
models term dependencies using the embedding vectors of terms in the Jelinek-Mercer lan-
guagemodel(JMLM)approach.TheotheristheParagraphVector(PV)model,26whichusesthe
paragraph vector to improve estimation in the Dirichlet language model (LM) approach. The
experimentalresultsarepresentedinTables9and10,respectively.TheresultsofGLMandPV
arebothdirectlyobtainedfromthereferences24,26.

JIANetal. 29
| )%61.2+( | )%77.2+( | )%69.3+( )%69.4+( |
| -------- | -------- | ----------------- |
FTAM
| -ADL 3152.0 | 6402.0 1072.0 | 9013.0 |
| ----------- | ------------- | ------ |
| FTAM 0642.0 | 1991.0 8952.0 | 2692.0 |
CER
| )%46.3+(  | )%82.3+(      | )%77.5+( )%22.5+( |
| --------- | ------------- | ----------------- |
| LQ 5842.0 | 1991.0 9852.0 | 2403.0            |
-ADL 52MB
GOL
| )%74.3+( | )%74.3+( | )%77.5+( )%42.5+( |
| -------- | -------- | ----------------- |
LQ
| -ADL 52MB 1842.0 | 4991.0 9852.0 | 2403.0 |
| ---------------- | ------------- | ------ |
PXE
| )%09.2+( | )%51.3+( | )%83.5+( )%09.4+( |
| -------- | -------- | ----------------- |
LQ
| -ADL 52MB 8642.0 | 8891.0 0852.0 | 3303.0            |
| ---------------- | ------------- | ----------------- |
| )%49.2+(         | )%33.2+(      | )%78.5+( )%73.5+( |
| -ADL 52MB 9642.0 | 2791.0 2952.0 | 6403.0            |
| 52MB 8932.0      | 7291.0 8442.0 | 1982.0            |
| ML-ADL )%41.6+(  | )%40.4+(      | )%82.7+( )%56.6+( |
| 2942.0           | 7991.0 3562.0 | 9403.0            |
| 8432.0           | 0291.0 3742.0 | 9582.0            |
ML
PAMfosmretniMLGhtiwnosirapmoC
|          | )%65.01+( | )%90.21+( |
| -------- | --------- | --------- |
| )%74.6+( |           | )%91.6+(  |
42MLG
| 7822.0 | 8591.0 3052.0 | 4682.0 |
| ------ | ------------- | ------ |
42MLMJ
| 8412.0 | 1771.0 7532.0 | 5552.0 |
| ------ | ------------- | ------ |
seireuQ
| 053-103 | 004-153 054-104 | 007-106 |
| ------- | --------------- | ------- |
9
| ELBAT tesataD | 5&4KSID |     |
| ------------- | ------- | --- |

30 JIANetal.
ruofotnemevorpmiehtetoned”↑“sworrA.tnemevorpmiehtsisesehtnerapehtniegatnecrepehT52.lateiAmorfdeniatboyltcerideraenilesabstidnaledomVPehtfostluserehT:etoN
|     | ↑)%15.2+( | ↑)%31.2+( ↑)%29.1+( |
| --- | --------- | ------------------- |
)%09.3+(
-ADL FTAM
| 962.0 | 673.0 223.0 | 375.0 |
| ----- | ----------- | ----- |
FTAM
| 952.0 | 763.0 513.0 | 265.0 |
| ----- | ----------- | ----- |
CER
|                 | ↑)%26.2+(   | ↑)%15.2+( ↑)%96.2+( |
| --------------- | ----------- | ------------------- |
| LQ              | )%07.4+(    |                     |
| -ADL 52MB 362.0 | 563.0 703.0 | 945.0               |
)%66.4+(362.0
GOL
|     | ↑)%65.2+( | ↑)%17.2+( )%75.1+( |
| --- | --------- | ------------------ |
LQ
| -ADL 52MB 362.0 | 563.0 703.0 | 345.0 |
| --------------- | ----------- | ----- |
PXE
|     | ↑)%22.2+( | ↑)%44.1+( |
| --- | --------- | --------- |
|     | )%22.4+(  | )%70.1+(  |
LQ
| -ADL 52MB 262.0 | 363.0 403.0 | 145.0 |
| --------------- | ----------- | ----- |
.dlobnisitesatadhcaenodeniatbotlusertsebehT.ledomVPehtfotahtnahtrehgihsisledomdesab-cipot
|     | ↑)%26.2+( | ↑)%76.2+( |
| --- | --------- | --------- |
|     | )%05.4+(  | )%73.0−(  |
52MB
| -ADL 262.0 | 563.0 703.0 | 335.0 |
| ---------- | ----------- | ----- |
52MB
| 152.0 | 553.0 992.0 | 535.0 |
| ----- | ----------- | ----- |
02@PdnaPAMfosmretniledomVPhtiwnosirapmoC
|     | ↑)%01.6+( ↑)%68.3+( | ↑)%69.0+( |
| --- | ------------------- | --------- |
)%64.0+(
-ADL
| 462.0 | 963.0 403.0 | 625.0 |
| ----- | ----------- | ----- |
ML
| 942.0 | 553.0 103.0 | 425.0 |
| ----- | ----------- | ----- |
ML
|            | )%35.5+( )%09.1+( | )%86.0+( )%67.1+( |
| ---------- | ----------------- | ----------------- |
| 62VP 762.0 | 673.0 792.0       | 915.0             |
| 62ML 352.0 | 963.0 592.0       | 015.0             |
cirteM
|          | 02@P | 02@P |
| -------- | ---- | ---- |
| lavE PAM | PAM  |      |
01
40TSUBOR
ELBAT tesataD
2VOG

JIANetal. 31
40TSUBORtesatadnoFTpoTEdnaFTpoT,RIdebmEneewtebnosirapmoC
11
ELBAT
FTAM
CER
52MB
GOL
52MB
PXE
52MB
52MB
ML
cirteMlavE
LQ
LQ
LQ
952.0
152.0
152.0
052.0
152.0
942.0
PAM
enilesab
763.0
353.0
353.0
453.0
553.0
553.0
02@P
)%65.0+(162.0
)%56.0+(252.0
)%17.0+(252.0
)%20.1+(252.0
)%74.0+(252.0
)%88.0+(152.0
PAM
RIdebmE
)%32.0−(663.0
)%54.0−(253.0
)%71.0−(253.0
)%60.0+(453.0
)%60.0+(653.0
)%79.0+(953.0
02@P
)%47.3+(962.0
)%59.4+(362.0
)%99.4+(362.0
)%39.4+(262.0
)%83.4+(262.0
)%20.6+(462.0
PAM
FTpoT
)%84.2+(673.0
)%43.3+(563.0
)%64.3+(563.0
)%06.2+(363.0
)%07.2+(563.0
)%98.3+(963.0
02@P
)%82.5+(372.0
)%49.6+(862.0
)%99.6+(862.0
)%33.7+(862.0
)%71.7+(962.0
)%36.7+(862.0
PAM
FTpoTE
)%03.3+(973.0
)%98.5+(473.0
)%10.6+(473.0
)%68.4+(173.0
)%32.5+(473.0
)%40.3+(663.0
02@P
.tnemevorpmiehtsisesehtnerapehtniegatnecrepehT:etoN

32 JIANetal.
FromTable9,theresultsshowthattheimprovementofourproposedLDA-LMishigherthan
theGLMonlyonDISK4&5withqueries401-450.However,wecanalsoseethatourbaselineLM
performs much better than the baseline JMLM, and our proposed topic-based models outper-
formthePVmodelonallthedatasets.Thereisareasontosaythattopic-basedmodelsarestill
competitive,althoughembedding-basedmethodsarepromising.
InTable10,wecanseethatourbaselineLMisclosetothatofthePVmodel.Theimprove-
ment of our topic-based models is higher than that of the PV model in terms of P@20 on data
setROBUST04,whileintermsofMAPondatasetGOV2.Asaresult,ourproposedtopic-based
modelsareatleastcomparabletotheembedding-basedmodelPV.
Furthermore, we explore how document embedding enhances our TopTF framework. The
resultsarepresentedinTable11.FromTable11,wecanseethatEmbedIRmodelshavelessthan
1% improvement over all the corresponding traditional models in terms of MAP but are even
worseintermsofP@20.TopTFcouldoutperformallthecorrespondingtraditionalmodelsand
EmbedIRmodelsintermsofMAPandP@20.ETopTFmodelsachievethebestperformancein
termsofMAPandP@20inmostcases.Therefore,itisworthexploringhowembeddingcould
significantlyimproveTopic-basedIRmodels,whichisalsoourresearchinthecoming.
6 CONCLUSIONS AND FUTURE WORK
In this paper, we first propose a new TF normalization model, BM25 , for probabilistic IR.
QL
Specifically,wepresentthreeTFnormalizationfunctions:logarithmicfunction,reciprocalfunc-
tionandexponentialfunction.WealsoincorporateBM25 intothestate-of-the-artBM25-based
QL
modelCRTER .Experimentalresultson14standarddatasetsshowthegoodperformanceofboth
2
BM25 andCRTER QLintermsofMAP.
QL 2
In addition, the topic-based term frequency normalization framework TopTF is proposed
bycombiningprobabilisticBM25andtopicmodelingtechniques.WealsoextenditintoMATF
and LM. Specifically, we present four hybrid models, LDA-BM25, LDA-BM25 , LDA-MATF
QL
and LDA-LM, for enhancing traditional IR models via topic modeling. These four models cap-
turebothterm-basedinformationandlatentsemantictopic-basedinformationatthesametime.
Experimentalresultson14standarddatasetsshowthattheproposedmodelsareeffectiveand
outperformthecorrespondingstrongbaselinesonmostofthedatasetsintermsofMAP,P@5and
P@20.Meanwhile,ourproposedmodelsareatleastcomparabletothestate-of-the-artCRTER
2
and topic-based model LBDM. Additionally, we studied the role of 𝜆 to our proposed mod-
els, and the performance of our proposed models with different numbers of topics. Finally, we
also compared our topic-based models with embedding-based models GLM and PV. Although
embedding-basedmodelsarethetrend,topic-basedmodelsarestillcompetitive.
There are several interesting future research directions that can be explored. First, we will
investigatetheoptimaltermfrequencynormalizationfunction.Second,itisinterestingtocon-
duct an in-depth study on complete parameter-free term frequency normalization without
hyper-parameters k and b. Third, we would like to study more the optimal topic number on
1
each data set. Fourth, we would like to conduct an in-depth study on the combination tradi-
tionalIRmodelwithtopicmodelandfindthebestcombination.Lastbutnotleast,wealsoplan
tointegratethepopularwordembeddingintotopic-basedIRmodels,forexample,topicalword
embedding.60
In addition, it will be interesting to research the integration of our proposed methods
into transformer-based neural network models (such as newly proposed BERT model,61

JIANetal. 33
XLNET model62 and RoBERTa model63). We also plan to evaluate our proposed framework
and methods on more data sets, including some real document collections (for instance, in
References34,64-67).
ACKNOWLEDGMENTS
We gratefully appreciate the anonymous reviewers for their valuable comments that greatly
helpedtoimprovethequalityofthearticle.Inparticular,wethanktheareaeditorandactionedi-
torforreviewingandprovidinginsightfulfeedbackforthisarticle.Inaddition,weacknowledge
Prof. Tingting He and Dr Xing Tan for their advice and support. We thank our team members
Prof. Xinhui Tu, Dr Min Pan, Xiao Han and Jie Yan for helping us with data processing, cod-
ingandsettingupserverenvironments.ThisresearchissubstantiallysupportedbytheNatural
SciencesandEngineeringResearchCouncil(NSERC)ofCanadaanNSERCCREATEawardin
ADERSIM,† theYorkResearchChairs(YRC)programandanOntarioResearchFund-Research
Excellence(ORF-RE)awardinBRAINAlliance.‡ThisresearchisalsosupportedbytheNational
NaturalScienceFoundationofChina.
ORCID
JimmyX.Huang https://orcid.org/0000-0003-1292-1491
REFERENCES
1. Jian F, Huang JX, Zhao J, He T, Hu P. A simple enhancement for ad-hoc information retrieval via topic
modelling. Proceedings of the 39th International ACM SIGIR Conference on Research and Development in
InformationRetrieval.NewYork,NY:ACM;2016:733-736.
2. Jian F, Huang JX, Zhao J, He T. A new term frequency normalization model for probabilistic informa-
tionretrieval.Proceedingsofthe41stInternationalACMSIGIRConferenceonResearchandDevelopmentin
InformationRetrieval.NewYork,NY:ACM;2018:1237-1240.
3. BeaulieuM,GatfordM,HuangX,RobertsonS,WalkerS,WilliamsP.OkapiatTREC-5.Proceedingsofthe5th
TextRetrievalConference.Gaithersburg,Maryland:NationalInstituteofStandardsandTechnology(NIST);
1996:143-166.
4. RobertsonS,ZaragozaH,TaylorM.SimpleBM25extensiontomultipleweightedfields.Proceedingsofthe
13thACMInternationalonConferenceonInformationandKnowledgeManagement.NewYork,NY:ACM;
2004:42-49.
5. He B, Ounis I. Term frequency normalisation tuning for BM25 and DFR models. Proceedings ofthe 27th
EuropeanConferenceonInformationRetrieval.Berlin,Heidelberg,Germany:Springer;2005:200-214.
6. HeB,OunisI.Onsettingthehyper-parametersoftermfrequencynormalizationforinformationretrieval.
ACMTransactionsonInformationSystems(TOIS).2007;25(3):13.
7. LvY,ZhaiC.Lower-boundingtermfrequencynormalization.Proceedingsofthe20thACMInternationalon
ConferenceonInformationandKnowledgeManagement.NewYork,NY:ACM;2011:7-16.
8. LvY,ZhaiC.Whendocumentsareverylong,BM25fails!Proceedingsofthe34thInternationalACMSIGIR
ConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;2011:1103-1104.
9. CumminsR,O’RiordanC.Aconstrainttoautomaticallyregulatedocument-lengthnormalisation.Proceedings
ofthe21stACMInternationalonConferenceonInformationandKnowledgeManagement.NewYork,NY:ACM;
2012:2443-2446.
†http://www.yorku.ca/adersim.
‡http://brainalliance.ca.

34 JIANetal.
10. CumminsR,O’RiordanC.Theeffectofquerylengthonnormalisationininformationretrieval.Proceedingsof
the20thIrishConferenceonArtificialIntelligenceandCognitiveScience.Berlin,Heidelberg,Germany:Springer;
2009:26-32.
11. LvY,ZhaiC.AdaptivetermfrequencynormalizationforBM25.Proceedingsofthe20thACMInternationalon
ConferenceonInformationandKnowledgeManagement.NewYork,NY:ACM;2011:1985-1988.
12. LvY.Astudyofquerylengthheuristicsininformationretrieval.Proceedingsofthe24thACMInternationalon
ConferenceonInformationandKnowledgeManagement.NewYork,NY:ACM;2015:1747-1750.
13. ChungTL,LukRWP,WongKF,KwokKL,LeeDL.Adaptingpivoteddocument-lengthnormalizationfor
querysize:experimentsinChineseandEnglish.ACMTransactionsonAsianLanguageInformationProcessing
(TALIP).2006;5(3):245-263.
14. AzzopardiL,GirolamiM,VanRijsbergenCJ.Topicbasedlanguagemodelsforadhocinformationretrieval.
2004IEEEInternationalJointConferenceonNeuralNetworks.Piscataway,NewJersey:IEEE;2004:3281-3286.
15. Liu X, Croft WB. Bruce. Cluster-based retrieval using language models. Proceedings of the 27th Interna-
tionalACMSIGIRConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;
2004:186-193.
16. WeiX,CroftWB.LDA-baseddocumentmodelsforad-hocretrieval.Proceedingsofthe29thInternationalACM
SIGIRConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;2006:178-185.
17. Wei X, Croft WB. Modeling term associations for ad-hoc retrieval performance within language model-
ing framework. Proceedingsofthe29thEuropeanConferenceonInformationRetrieval. Berlin, Heidelberg,
Germany:Springer;2007:52-63.
18. LiJ,ZhaoX,ZhangP,SongD.ModelingmultipleinteractionswithaMarkovrandomfieldinqueryexpansion
forsessionsearch.ComputationalIntelligence.2018;34(1):345-362.
19. SongD,ShiY,ZhangP,HuangQ,KruschwitzU,HouY,WangB.Incorporatingintra-querytermdependen-
ciesinanaspectquerylanguagemodel.ComputationalIntelligence.2015;31(4):699-720.
20. HuangX,RobertsonS,CerconeN,AnA.Probability-basedChinesetextprocessingandretrieval.Computa-
tionalIntelligence.2000;16(4):552-569.
21. Mikolov T, Chen K, Corrado G, Dean J. Efficient estimation of word representations in vector space.
Proceedingsofthe1stInternationalConferenceonLearningRepresentations.Scottsdale,Arizona:ICLR;2013.
22. LeQ,MikolovT.Distributedrepresentationsofsentencesanddocuments.Proceedingsofthe31stInternational
ConferenceonMachineLearning.Bejing,China:PMLR;2014:1188-1196.
23. ZucconG,KoopmanB,BruzaP,AzzopardiL.IntegratingandevaluatingneuralwordEmbeddingsininfor-
mationretrieval.Proceedingsofthe20thAustralasianDocumentComputingSymposium.NewYork,NY:ACM;
2015:12.
24. Ganguly D, Roy D, Mitra M, Jones GJ. Word embedding based generalized language model for informa-
tionretrieval.Proceedingsofthe38thInternationalACMSIGIRConferenceonResearchandDevelopmentin
InformationRetrieval.NewYork,NY:ACM;2015:795-798.
25. NalisnickE,MitraB,CraswellN,CaruanaR.ImprovingdocumentrankingwithdualwordEmbeddings.
Proceedingsofthe25thInternationalConferenceonWorldWideWeb.NewYork,NY:ACM;2016:83-84.
26. AiQ,YangL,GuoJ,CroftWB.Improvinglanguageestimationwiththeparagraphvectormodelforad-hoc
retrieval. Proceedings of the 39th International ACM SIGIR Conference on Research and Development in
InformationRetrieval.NewYork,NY:ACM;2016:869-872.
27. AiQ,YangL,GuoJ,CroftWB.Analysisoftheparagraphvectormodelforinformationretrieval.Proceed-
ingsofthe2016ACMInternationalConferenceontheTheoryofInformationRetrieval.NewYork,NY:ACM;
2016:133-142.
28. Gysel CV, De Rijke M, Kanoulas E. Neural vector spaces for unsupervised information retrieval. ACM
TransactionsonInformationSystems(TOIS).2018;36(4):38.
29. Blei DM, Ng AY, Jordan MI. Latent Dirichlet allocation. Journal of Machine Learning Research.
2003;3:993-1022.
30. PaikJH.AnovelTF-IDFweightingschemeforeffectiveranking.Proceedingsofthe36thInternationalACM
SIGIRConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;2013:343-352.
31. ZhaiC,LaffertyJ.Astudyofsmoothingmethodsforlanguagemodelsappliedtoad-hocinformationretrieval.
Proceedingsofthe24thInternationalACMSIGIRConferenceonResearchandDevelopmentinInformation
Retrieval.NewYork,NY:ACM;2001:334-342.

JIANetal. 35
32. ZhaiC,LaffertyJ.Astudyofsmoothingmethodsforlanguagemodelsappliedtoinformationretrieval.ACM
TransactionsonInformationSystems(TOIS).2004;22(2):179-214.
33. RobertsonS,ZaragozaH.Theprobabilisticrelevanceframework:BM25andbeyond.FoundTrendsInfRetr.
2009;3(4):333-389.
34. HuangX,HuQ.Abayesianlearningapproachtopromotingdiversityinrankingforbiomedicalinforma-
tionretrieval.Proceedingsofthe32ndInternationalACMSIGIRConferenceonResearchandDevelopmentin
InformationRetrieval.NewYork,NY:ACM;2009:307-314.
35. HuangX,PengF,SchuurmansD,CerconeN,RobertsonS.ApplyingmachineLearningtotextsegmentation
forinformationretrieval.InformationRetrieval.2003;6(3–4):333-362.
36. HeB,OunisI.Astudyofparametertuningfortermfrequencynormalization.Proceedingsofthe12thACM
InternationalonConferenceonInformationandKnowledgeManagement.NewYork,NY:ACM;2003:10-16.
37. LipaniA,LupuM,HanburyA,AizawaA.VerbosenessfissionforBM25documentlengthnormalization.
Proceedingsofthe2015InternationalConferenceontheTheoryofInformationRetrieval.NewYork,NY:ACM;
2015:385-388.
38. HuQ,HuangJX,HuX.Modelingandminingtermassociationforimprovingbiomedicalinformationretrieval
performance.BMCBioinformatics.2012;13(2):S2.
39. MetzlerD,CroftWB.AMarkovrandomfieldmodelfortermdependencies.Proceedingsofthe28thInterna-
tionalACMSIGIRConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;
2005:472-479.
40. ZhaoJ,HuangJX,HeB.CRTER:usingcrosstermstoenhanceprobabilisticIR.Proceedingsofthe34thInter-
nationalACMSIGIRConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;
2011:155-164.
41. ZhaoJ,HuangJX,YeZ.Modelingtermassociationsforprobabilisticinformationretrieval.ACMTransactions
onInformationSystems(TOIS).2014;32(2):1-47.
42. BüttcherS,ClarkeCL,LushmanB.Termproximityscoringforad-hocretrievalonverylargetextcollections.
Proceedingsofthe29thInternationalACMSIGIRConferenceonResearchandDevelopmentinInformation
Retrieval.NewYork,NY:ACM;2006:621-622.
43. LvY,ZhaiC.Positionallanguagemodelsforinformationretrieval.Proceedingsofthe32ndInternationalACM
SIGIRConferenceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;2009:299-306.
44. Song R, Yu L, Wen JR, Hon HW. A proximity probabilistic model for information retrieval. Tech Rept:
MicrosoftResearch;2011.
45. SongM,KimS,LeeK.Ensembleanalysisoftopicaljournalrankinginbioinformatics.JAssocInfSciTechnol.
2017;68(6):1564-1583.
46. LiuY,XuS.Alocalcontext-awareLDAmodelfortopicmodelinginadocumentnetwork.JAssocInfSci
Technol.2017;68(6):1429-1448.
47. ZhangJ,ZhaiS,LiuH,StevensonJA.Socialnetworkanalysisonatopic-basednavigationguidancesystemin
apublichealthportal.JAssocInfSciTechnol.2016;67(5):1068-1088.
48. ThelwallM,BuckleyK.Topic-basedsentimentanalysisforthesocialweb:theroleofmoodandissue-related
words.JAssocInfSciTechnol.2013;64(8):1608-1617.
49. YeZ,HuangJX,LinH.Findingagoodquery-relatedtopicforboostingPseudo-relevancefeedback.JAssoc
InfSciTechnol.2011;62(4):748-760.
50. MiaoJ,HuangJX,ZhaoJ.TopPRF:aprobabilisticframeworkforintegratingtopicspaceintoPseudorelevance
feedback.ACMTransactionsonInformationSystems(TOIS).2016;34(4):22.
51. Cotelo JM, Cruz FL, Troyano JA. Dynamic topic-related tweet retrieval. J Assoc Inf Sci Technol.
2014;65(3):513-523.
52. YiX,AllanJ.Acomparativestudyofutilizingtopicmodelsforinformationretrieval.Proceedingsofthe31st
EuropeanConferenceonInformationRetrieval.Berlin,Heidelberg,Germany:Springer;2009:29-41.
53. LiW,McCallumA.Pachinkoallocation:DAG-structuredmixturemodelsoftopiccorrelations.Proceedingsof
the23rdInternationalConferenceonMachineLearning.NewYork,NY:ACM;2006:577-584.
54. Bengio Y, Ducharme R, Vincent P, Jauvin C. A neural probabilistic language model. JournalofMachine
LearningResearch.2003;3:1137-1155.
55. HeB,HuangJX,ZhouX.Modelingtermproximityforprobabilisticinformationretrievalmodels.InformSci.
2011;181(14):3017-3031.

36 JIANetal.
56. HofmannT.Probabilisticlatentsemanticindexing.Proceedingsofthe22ndInternationalACMSIGIRConfer-
enceonResearchandDevelopmentinInformationRetrieval.NewYork,NY:ACM;1999:50-57.
57. JordanMI.LearninginGraphicalModels.Berlin,Heidelberg,Germany:SpringerScience&BusinessMedia;
1998.
58. Geman S, Geman D. Stochastic relaxation, Gibbs distributions, and the Bayesian restoration of images.
ReadingsinComputerVision.1987;6:564-584.
59. YuanJ,GaoF,HoQ,etal.LightLDA:bigtopicmodelsonmodestcomputerclusters.Proceedingsofthe24th
InternationalConferenceonWorldWideWeb.NewYork,NY:ACM;2015:1351-1361.
60. LiuY,LiuZ,ChuaTS,SunM.TopicalwordEmbeddings.Proceedingsofthe29thAAAIConferenceonArtificial
Intelligence.Austin,Texas:AAAIPress;2015.
61. DevlinJ,ChangMW,LeeK,ToutanovaK.BERT:pre-trainingofdeepbidirectionaltransformersforlanguage
understanding.Proceedingsofthe2019ConferenceoftheNorthAmericanChapteroftheAssociationforCompu-
tationalLinguistics:HumanLanguageTechnologies.Vol1(LongandShortPapers).Cambridge,Massachusetts:
ACL;2019:4171-4186.
62. YangZ,DaiZ,YangY,CarbonellJ,SalakhutdinovR,LeQV.XLNet:generalizedautoregressivepretraining
forlanguageunderstanding.arXivpreprintarXiv:1906.08237.2019.
63. Liu Y, Ott M, Goyal N, et al. RoBERTa: a robustly optimized BERT pretraining approach. arXiv preprint
arXiv:1907.11692.2019.
64. LiuY,HuangX,AnA,YuX.ARSA:Asentiment-awaremodelforpredictingsalesperformanceusingblogs.
Proceedingsofthe30thInternationalACMSIGIRConferenceonResearchandDevelopmentinInformation
Retrieval.NewYork,NY:ACM;2007:607-614.
65. YuX,LiuY,HuangX,AnA.Miningonlinereviewsforpredictingsalesperformance:acasestudyinthemovie
domain.IEEETransactionsonKnowledgeandDataEngineering.2010;24(4):720-734.
66. HuangX,ZhongM,SiL.YorkUniversityatTREC2005:GenomicsTrack.Gaithersburg,Maryland:NIST;2005.
67. Liang Z, Zhang G, Huang JX, Hu QV. Deep learning for healthcare decision making with EMRs. 2014
IEEE International Conference on Bioinformatics and Biomedicine (BIBM). Piscataway, New Jersey: IEEE;
2014:556-559.
Howtocitethisarticle:JianF,HuangJX,ZhaoJ,YingZ,WangY.Atopic-basedterm
frequencynormalizationframeworktoenhanceprobabilisticinformationretrieval.
ComputationalIntelligence.2019;1–36.https://doi.org/10.1111/coin.12248