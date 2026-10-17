|     | Exploring |                   |       | the | Space | of Topic        | Coherence |     |                          |     | Measures  |     |     |     |
| --- | --------- | ----------------- | ----- | --- | ----- | --------------- | --------- | --- | ------------------------ | --- | --------- | --- | --- | --- |
|     |           | Michael           | Röder |     |       | Andreas         | Both      |     | Alexander                |     | Hinneburg |     |     |     |
|     |           | LeipzigUniversity |       |     |       | R&D,UnisterGmbH |           |     | Martin-Luther-University |     |           |     |     |     |
|     |           | R&D,UnisterGmbH   |       |     |       | Leipzig,Germany |           |     | Halle-Wittenberg,Germany |     |           |     |     |     |
Leipzig,Germany andreas.both@unister.de hinneburg@informatik.uni-
roeder@informatik.uni-
halle.de
leipzig.de
ABSTRACT
|             |     |               |     |          |            |           | quantifythecoherenceofafactset[5]. |            |     |      |            | Approachesproposed |          |     |
| ----------- | --- | ------------- | --- | -------- | ---------- | --------- | ---------------------------------- | ---------- | --- | ---- | ---------- | ------------------ | -------- | --- |
|             |     |               |     |          |            |           | in scientific                      | philosophy |     | have | formalized | such               | measures | as  |
| Quantifying |     | the coherence | of  | a set of | statements | is a long |                                    |            |     |      |            |                    |          |     |
functionsofjointandmarginalprobabilitiesassociatedwith
standingproblemwithmanypotentialapplicationsthathas
|           |             |     |                |           |     |             | thefacts. | BovensandHartmann[5]discussmanyexamples |           |     |            |            |     |        |
| --------- | ----------- | --- | -------------- | --------- | --- | ----------- | --------- | --------------------------------------- | --------- | --- | ---------- | ---------- | --- | ------ |
| attracted | researchers |     | from different | sciences. |     | The special |           |                                         |           |     |            |            |     |        |
|           |             |     |                |           |     |             | that lead | to a                                    | demanding | set | of complex | properties |     | such a |
caseofmeasuringcoherenceoftopicshasbeenrecentlystud-
|        |        |                 |      |               |         |               | measure  | needs        | to fulfill. | An       | example    | is the | non-monotonic  |         |
| ------ | ------ | --------------- | ---- | ------------- | ------- | ------------- | -------- | ------------ | ----------- | -------- | ---------- | ------ | -------------- | ------- |
| ied to | remedy | the problem     | that | topic         | models  | give no guar- |          |              |             |          |            |        |                |         |
|        |        |                 |      |               |         |               | behavior | of coherence |             | in case  | of growing | fact   | sets.          | The co- |
| anty   | on the | interpretablity | of   | their output. | Several | bench-        |          |              |             |          |            |        |                |         |
|        |        |                 |      |               |         |               | herence  | of the       | two fact    | sets“the | animal     | is     | a bird”and“the |         |
markdatasetswereproducedthatrecordhumanjudgements
of the interpretability of topics. We are the first to propose animal cannot fly”can be increased by adding the fact“the
a framework that allows to construct existing word based animal is a penguin”. The non-monotonicity becomes ap-
|                    |          |     |                                 |          |              |      | parent when    | the        | coherence |            | is lowered | again     | by adding | non-     |
| ------------------ | -------- | --- | ------------------------------- | -------- | ------------ | ---- | -------------- | ---------- | --------- | ---------- | ---------- | --------- | --------- | -------- |
| coherence          | measures | as  | well as                         | new ones | by combining | ele- |                |            |           |            |            |           |           |          |
|                    |          |     |                                 |          |              |      | related        | facts [5]. | The       | discussion | of         | coherence | measures  | in       |
| mentarycomponents. |          |     | Weconductasystematicsearchofthe |          |              |      |                |            |           |            |            |           |           |          |
|                    |          |     |                                 |          |              |      | that community |            | deals     | mainly     | with       | schemes   | that      | estimate |
spaceofcoherencemeasuresusingallpubliclyavailabletopic
|                                |         |                |         |                       |             |                | the hanging              | and           | fitting | together | of                          | the individual |              | facts of |
| ------------------------------ | ------- | -------------- | ------- | --------------------- | ----------- | -------------- | ------------------------ | ------------- | ------- | -------- | --------------------------- | -------------- | ------------ | -------- |
| relevancedatafortheevaluation. |         |                |         | Ourresultsshowthatnew |             |                |                          |               |         |          |                             |                |              |          |
|                                |         |                |         |                       |             |                | a larger                 | set. Examples |         | of such  | schemes                     | are            | (i) to       | compare  |
| combinations                   |         | of components  |         | outperform            | existing    | measures       |                          |               |         |          |                             |                |              |          |
|                                |         |                |         |                       |             |                | each fact                | against       | the     | rest of  | all other                   | fact,          | (ii) compare | all      |
| with                           | respect | to correlation | to      | human                 | ratings.    | Finally, we    |                          |               |         |          |                             |                |              |          |
|                                |         |                |         |                       |             |                | pairs against            | each          | other,  | and      | (iii) compare               |                | disjoints    | subsets  |
| outline                        | how     | our results    | can be  | transferred           | to          | further appli- |                          |               |         |          |                             |                |              |          |
|                                |         |                |         |                       |             |                | offactsagainsteachother. |               |         |          | Suchtheoreticalworkoncoher- |                |              |          |
| cations                        | in the  | context        | of text | mining,               | information | retrieval      |                          |               |         |          |                             |                |              |          |
encefromscientificphilosophy—see[7]foranoverview—has
| and | the world | wide web. |     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
potentialtobeadaptedincomputerscience,e.g.,coherence
of word sets.
CategoriesandSubjectDescriptors
|     |     |     |     |     |     |     | Interest | into | coherence | measures |     | has arisen | in  | text min- |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---- | --------- | -------- | --- | ---------- | --- | --------- |
[Document representation]: Document topic models ing,asunsupervisedlearningmethodsliketopicmodelsgive
|     |     |     |     |     |     |     | noguaranteesontheinterpreteabilityoftheiroutput. |     |     |     |     |     |     | Topic |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------ | --- | --- | --- | --- | --- | --- | ----- |
modelslearntopics—typicallyrepresentedassetsofimpor-
GeneralTerms
tantwords—automaticallyfromunlabeleddocumentsinan
Measurement unsupervised way. This is an attractive method to bring
|     |     |     |     |     |     |     | structure | to otherwise |     | unstructured |     | text | data. | The sem- |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------------ | --- | ------------ | --- | ---- | ----- | -------- |
Keywords inal work of [13] proposed automatic coherence measures
|       |             |       |            |       |       |     | that rate | topics     | regarding | to            | their     | understandability. |           | The    |
| ----- | ----------- | ----- | ---------- | ----- | ----- | --- | --------- | ---------- | --------- | ------------- | --------- | ------------------ | --------- | ------ |
| topic | evaluation; | topic | coherence; | topic | model |     |           |            |           |               |           |                    |           |        |
|       |             |       |            |       |       |     | proposed  | measures   | treat     | wordsasfacts. |           | This               | important | re-    |
|       |             |       |            |       |       |     | striction | will apply | to        | all analyses  | presented |                    | in this   | paper. |
1. INTRODUCTION
|     |     |     |     |     |     |     | An example | of  | such set | is {game, | sport, | ball, | team}, | which |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | -------- | --------- | ------ | ----- | ------ | ----- |
Asetofstatementsorfactsissaidtobecoherent,ifthey we will use throughout the paper to illustrate the methods.
support each other. Thus, a coherent fact set can be inter- Furthermore, [13] restricts coherence to be always based on
|        |      |              |        |             |     |               | comparing | word | pairs. | Our | analyses | will | go beyond | this |
| ------ | ---- | ------------ | ------ | ----------- | --- | ------------- | --------- | ---- | ------ | --- | -------- | ---- | --------- | ---- |
| preted | in a | context that | covers | all or most | of  | the facts. An |           |      |        |     |          |      |           |      |
point.
exampleofacoherentfactsetis“thegameisateamsport”,
Evaluationsin[13]basedonhumangeneratedtopicrank-
| “the     | game is   | played with | a ball”,“the |      | game demands | great     |             |      |          |     |       |         |               |     |
| -------- | --------- | ----------- | ------------ | ---- | ------------ | --------- | ----------- | ---- | -------- | --- | ----- | ------- | ------------- | --- |
|          |           |             |              |      |              |           | ings showed | that | measures |     | based | on word | co-occurrence |     |
| physical | efforts”. | A long      | standing     | open | question     | is how to |             |      |          |     |       |         |               |     |
statisticsestimatedonWikipediaoutperformmeasuresbased
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalor on WordNet and similar semantic resources. Subsequent
classroomuseisgrantedwithoutfeeprovidedthatcopiesarenotmadeordistributed
forprofitorcommercialadvantageandthatcopiesbearthisnoticeandthefullcitation empirical works on topic coherence [12, 18, 10] proposed a
onthefirstpage. Copyrightsforcomponentsofthisworkownedbyothersthanthe number of measures based on word statistics that differ in
author(s)mustbehonored.Abstractingwithcreditispermitted.Tocopyotherwise,or severaldetails: definition,normalizationandaggregationof
republish,topostonserversortoredistributetolists,requirespriorspecificpermission word statistics and reference corpus. In addition, a new
and/orafee.Requestpermissionsfrompermissions@acm.org. method based on word context vectors has been proposed
WSDM’15,February2–6,2015,Shanghai,China.
recently [1].
Copyrightisheldbytheowner/author(s).PublicationrightslicensedtoACM.
ACM978-1-4503-3317-7/15/02...$15.00.
http://dx.doi.org/10.1145/2684822.2685324.
399

Lookingatthetwolinesofresearchoncoherence,scientific evaluated. The coherence based on pointwise mutual infor-
philosophy and topic modelling, we note that the contribu- mation (PMI)gavelargestcorrelationswithhumanratings.
tionsaremainlycomplementary. Whiletheformerproposed UCI coherence is calculated by2:
agoodnumberofschemesforcomparingfactsorwords,the
latter proposed useful methods for estimating word prob- 2 N (cid:88) −1 (cid:88) N
C = PMI(w ,w ) (1)
abilities and normalizing numeric comparisons. However, UCI N ·(N −1) i j
a systematic, empirical evaluation of the methods of both i=1 j=i+1
worlds and their yet unexplored combinations is still miss- PMI(w ,w )=log P(w i ,w j )+(cid:15) (2)
ing. i j P(w i )·P(w j )
Human topic rankings serve as the gold standard for co-
Probabilitiesareestimatedbasedonwordco-occurrencecounts.
herenceevaluation. However,theyareexpensivetoproduce.
Those counts are derived from documents that are con-
There are three publicly available sources of such rankings:
structedbyaslidingwindowthatmovesovertheWikipedia,
first, Chang et al. [6] that have been prepared by Lau et
whichisusedasexternalreferencecorpus. Eachwindowpo-
al. [10] for topic coherence evaluation, second, Aletras and
sitiondefinessuchadocument. Forourexampletopicfrom
Stevenson [1] and third, Rosner et al. [16]. A systematic,
section 1 we would calculate:
empirical evaluation should take all these sources into ac-
count. Forthisreason,wechoosetheconceptofaframework 1 (cid:0)
C = · PMI(game,sport)+PMI(game,ball)
providing an objective platform for comparing the different UCI 6
approaches. Following our research agenda, this will lead +PMI(game,team)+PMI(sport,ball) (3)
to completely new insights of the behavior of different al-
(cid:1)
+PMI(sport,team)+PMI(ball,team)
gorithms with regard to the available benchmarks. Hence,
itwillbepossibletofinallyevaluatethereasonsforspecific
Mimno et al. [12] proposed to use an asymmetrical con-
behavior of topic coherences on a comparable basis.
firmation measure between top word pairs (smoothed con-
Our contributions are these: First, we propose a unifying
ditional probability). The summation of UMass coherence
frameworkthatspansaconfigurationspaceofcoherencedef-
accounts for the ordering among the top words of a topic.2
initions. Second, we exhaustively search this space for the
c sp oh ec e t re t n o c a e l d l e a fi va n i i l t a io b n le w h i u th m t a h n e t b o e p s i t c o r v a e n r k a i l n l g co d r a r t e a la . t T io h n is w s it e h ar r c e h - C = 2 (cid:88) N (cid:88) i−1 log P(w i ,w j )+(cid:15) (4)
UMass N ·(N −1) P(w )
empirically evaluates published coherence measures as well i=2j=1 j
as unpublished ones based on combinations of known ap-
Word probabilities are estimated based on document fre-
proaches. Our results reveal a coherence measure based on
quenciesoftheoriginaldocumentsusedforlearningthetop-
anewcombinationofknownapproachesthatapproximates
humanratingsbetterthanthestateoftheart.1 Finally,we ics. The calculation for our example would be:
note that coherence measures are useful beyond topic mod- 1(cid:16)
elling. We discuss applications to search, advertising and C UMass = 6 log(P(sport|game))+log(P(ball|game))
automatic translation.
+log(P(ball|sport))+log(P(team|game)) (5)
The rest of the paper is structured as follows: In section
(cid:17)
2,webrieflyreviewrelatedwork. Ourunifyingframeworkis +log(P(team|sport))+log(P(team|ball))
introducedinsection3. Section4describesdatapreparation
and evaluation results and section 5 discusses our findings. Stevensetal.[18]foundthatboth—UCIandUMasscohe-
In section 6 the runtimes of the measures ar analyzed. Sec- rence—perform better if parameter (cid:15) is chosen to be rather
tion 7 explains how coherence measures can be applied be- small instead of (cid:15)=1 as in respective original publications.
yondtopicmodelling. Ourconclusionsarestatedinsection AletrasandStevenson[1]introducedtopiccoherencebased
8. on context vectors for every topic top word. A context vec-
tor of a word w is created using word co-occurrence counts
2. RELATEDWORK determined using context windows that contain all words
located ±5 tokens around the ocurrences of the word w.
Theevaluationoftopicmodelsneedsnexttoholdoutper-
Largest correlation to human topic coherence ratings were
plexity an additional measure that can rate topics with re-
found when defining the elements of these vectors as nor-
spect to understandability and interpretability by humans
malized PMI (NPMI) [4]. Additionally, they showed that
[6]. Measures based on evaluation of topic model distribu-
restricting the word co-occurrences to those words that are
tions can produce useful results [2, 11]. However, they are
partofthesametopicperformsbest(topwordspace). Thus,
difficult to link with human generated gold standards.
the j-th element of the context vector v(cid:126) of word w has
i i
Newmanetal.[13]representedtopicsbysetsoftopwords
NPMI:
andaskedhumanstoratethesesetsasgood,neutralorbad.
Severalautomatictopicrankingmethodsthatmeasuretopic  log P(wi,wj)+(cid:15) γ
coherenceareevaluatedbycomparisontothesehumanrat- v ij =NPMI(w i ,w j )γ = −log(P P ( (w w i) , ·P w (w ) j + ) (cid:15))  (6)
ings. The evaluated topic coherence measures take the set i j
of N top words of a topic and sum a confirmation measure
over all word pairs. A confirmation measure depends on a 2(cid:15) is added to avoid logarithm of zero.
singlepairoftopwords. Severalconfirmationmeasureswere C as well as C can be used with the arithmetic
UCI UMass
mean or only with the sum of the single elements, because
1Data and tools for replicating our coherence calculations themeancalculationdoesn’tinfluencetheorderofevaluated
are available at https://github.com/AKSW/Palmetto . topics that have the same number of top words.
400

Forourexampletopic,thevectorofitstopwordgamewould Note that this approach takes relationships between word
be calculated as: sets into account and goes beyond averaging confirmations
|     |     |     |     |     |     |     |     | between | word | pairs.3 |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ---- | ------- | --- | --- | --- | --- |
(cid:8) NPMI(game,game)γ,NPMI(game,sport)γ,
(cid:126)v game =
|     |     |                                          |     |     |     |     | (7) | Douven | and      | Meijs        | [7] took | this approach    | further | by cre-   |
| --- | --- | ---------------------------------------- | --- | --- | --- | --- | --- | ------ | -------- | ------------ | -------- | ---------------- | ------- | --------- |
|     |     | NPMI(game,ball)γ,NPMI(game,team)γ(cid:9) |     |     |     |     |     |        |          |              |          | =(W(cid:48),W∗). |         |           |
|     |     |                                          |     |     |     |     |     | ating  | pairs of | word subsets | S        | i                | These   | pairs are |
testedwhethertheexistenceofthesubsetW∗
supportsthe
| An  | increase | of γ | gives | higher NPMI | values | more | weight. |                                 |     |     |     |                            |     |     |
| --- | -------- | ---- | ----- | ----------- | ------ | ---- | ------- | ------------------------------- | --- | --- | --- | -------------------------- | --- | --- |
|     |          |      |       |             |        |      |         | occurrenceofthesubsetW(cid:48). |     |     |     | Thisisdoneusingseveralcon- |     |     |
Confirmationmeasuresbetweenpairsofcontextvectorsare
|     |     |     |     |     |     |     |     | firmation | measures | and | has been | adapted | to the | evaluation |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------- | --- | -------- | ------- | ------ | ---------- |
vectorsimilaritieslikecosine,DiceorJaccardthatareaver-
|      |      |           |      |            |       |               |     | of topics                 | by Rosner | et  | al. [16]. | The authors               | found | that us- |
| ---- | ---- | --------- | ---- | ---------- | ----- | ------------- | --- | ------------------------- | --------- | --- | --------- | ------------------------- | ----- | -------- |
| aged | over | all pairs | of a | topics top | words | like in [13]. |     |                           |           |     |           |                           |       |          |
|      |      |           |      |            |       |               |     | inglargersubsetsW(cid:48) |           |     | andW∗     | canleadtobetterperforming |       |          |
|      |      | 1         |      |            |       |               |     | coherence                 | measures. |     |           |                           |       |          |
(cid:0)
|     | C   | cos = · | cos((cid:126)v | game ,(cid:126)v sport | )+cos((cid:126)v | game ,(cid:126)v ball | )   |     |     |     |     |     |     |     |
| --- | --- | ------- | -------------- | ---------------------- | ---------------- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
6
(8)
+cos((cid:126)v ,(cid:126)v )+cos((cid:126)v ,(cid:126)v ) 3. FRAMEWORK OF COHERENCE MEA-
|     |     |     | game | team |     | sport ball |     |     |     |     |     |     |     |     |
| --- | --- | --- | ---- | ---- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:1)
|     |     | +cos((cid:126)v |       | ,(cid:126)v )+cos((cid:126)v |     | ,(cid:126)v ) |     | SURES |     |     |     |     |     |     |
| --- | --- | --------------- | ----- | ---------------------------- | --- | ------------- | --- | ----- | --- | --- | --- | --- | --- | --- |
|     |     |                 | sport | team                         |     | ball team     |     |       |     |     |     |     |     |     |
Alternatively, topic coherence is computed as average simi- Ournewunifyingframeworkrepresentsacoherencemea-
|        |         |     |      |         |         |           |          | sure as | composition | of  | parts | that can | be freely | combined. |
| ------ | ------- | --- | ---- | ------- | ------- | --------- | -------- | ------- | ----------- | --- | ----- | -------- | --------- | --------- |
| larity | between | top | word | context | vectors | and their | centroid |         |             |     |       |          |           |           |
(cid:126)v c . Hence,existingmeasuresaswellasyetunexploredmeasures
|     |     |                        |             |             |             |     |     | can be | constructed. | The | parts | are grouped | into | dimensions |
| --- | --- | ---------------------- | ----------- | ----------- | ----------- | --- | --- | ------ | ------------ | --- | ----- | ----------- | ---- | ---------- |
|     |     | (cid:126)v =(cid:126)v | +(cid:126)v | +(cid:126)v | +(cid:126)v |     | (9) |        |              |     |       |             |      |            |
c game sport ball team that span the configuration space of coherence measures.
1 (cid:0) Each dimension is characterized by a set of exchangeable
|     |     | C = | · cos((cid:126)v | ,(cid:126)v | )+cos((cid:126)v | ,(cid:126)v ) |      |             |     |     |     |     |     |     |
| --- | --- | --- | ---------------- | ----------- | ---------------- | ------------- | ---- | ----------- | --- | --- | --- | --- | --- | --- |
|     |     | cen | 4                | game c      |                  | sport c       | (10) | components. |     |     |     |     |     |     |
+cos((cid:126)v ,(cid:126)v )+cos((cid:126)v ,(cid:126)v ) (cid:1) Coherence of a set of words measures the hanging and
|     |     |     |     | ball c | team | c   |     |         |          |           |       |            |     |             |
| --- | --- | --- | --- | ------ | ---- | --- | --- | ------- | -------- | --------- | ----- | ---------- | --- | ----------- |
|     |     |     |     |        |      |     |     | fitting | together | of single | words | or subsets | of  | them. Thus, |
Additionally, [1] showed that the UCI coherence performs the first dimension is the kind of segmentation that is used
better if the PMI is replaced by the NPMI. to divide a word set into smaller pieces. These pieces are
Lau et al. [10] structured the topic evaluation in two dif- compared against each other, e.g., segmentation into word
ferenttasks—wordintrusionandobservedcoherence. Inthe pairs. The set of different kinds of segmentation is S. The
| first             | task, | an intruder | word                            | has | to be identified | among | the |                                               |           |        |              |         |     |             |
| ----------------- | ----- | ----------- | ------------------------------- | --- | ---------------- | ----- | --- | --------------------------------------------- | --------- | ------ | ------------ | ------- | --- | ----------- |
|                   |       |             |                                 |     |                  |       |     | second                                        | dimension | is the | confirmation | measure |     | that scores |
| topwordsofatopic. |       |             | Forthesecondtask,topicshavetobe |     |                  |       |     |                                               |           |        |              |         |     |             |
|                   |       |             |                                 |     |                  |       |     | theagreementofagivenpair,e.g.,NPMIoftwowords. |           |        |              |         |     | The         |
ratedregardingtheircoherence,whileratingsarecompared
|     |     |     |     |     |     |     |     | set of | confirmation | measures |     | is M. Confirmation |     | measures |
| --- | --- | --- | --- | --- | --- | --- | --- | ------ | ------------ | -------- | --- | ------------------ | --- | -------- |
to human ratings. Both tasks can be done for single top- use word probabilities that can be computed in different
ics or the whole topic model. [10] confirmed that the UCI ways, which forms the third dimension of the configuration
coherence performs better with the NPMI. space. The set of methods to estimate word probabilities
Theoretical work on coherence of sets of statements in is P. Last, the methods of how to aggregate scalar val-
a broader sense are reviewed in [7]. We follow their nota- uescomputedbytheconfirmationmeasureformsthefourth
tionbutadaptpresentationofmeasurestowordcoherence. dimension. The set of aggregation functions is Σ.
Shogenji’s [17] and Olsson’s [14] coherences are defined as: Theworkflowofourframeworkasshowninfigure1com-
|     |     |     |     |              |     |     |     | prisesfoursteps. |     | First,thewordsettissegmentatedintoa |     |     |     |     |
| --- | --- | --- | --- | ------------ | --- | --- | --- | ---------------- | --- | ----------------------------------- | --- | --- | --- | --- |
|     |     |     |     | P(w 1 ,...,w | N ) |     |     |                  |     |                                     |     |     |     |     |
C S = (11) setofpairsofwordsubsetsS. Second,wordprobabilitiesP
|     |     |     |     | (cid:81)N P(w | )   |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
i=1 i are computed based on a given reference corpus. Both, the
P(w ,...,w ) set of word subsets S as well as the computed probabilities
|     |     |     | C = | 1   | N   |     | (12) |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
O P(w ∨...∨w ) P are consumed by the confirmation measure to calculate
|     |     |     |     | 1   | N   |     |     |                |     |            |     |          |       |                |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | ---------- | --- | -------- | ----- | -------------- |
|     |     |     |     |     |     |     |     | the agreements |     | ϕ of pairs | of  | S. Last, | those | values are ag- |
The usage of these coherences for our example is straight gregated to a single coherence value c.
| forward: |     |     |     |     |     |     |     | Insummary,theframeworkdefinesaconfigurationsspace |     |     |     |     |         |     |
| -------- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------- | --- | --- | --- | --- | ------- | --- |
|          |     |     |     |     |     |     |     | thatisthecrossproductofthefoursetsC               |     |     |     |     | =S×M×P× |     |
P(game,sport,ball,team)
C S = (13) Σ. In the following subsections, these four dimensions are
P(game)·P(sport)·P(ball)·P(team)
|     |     |     |     |     |     |     |     | explained | in more | detail. |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------- | ------- | --- | --- | --- | --- |
P(game,sport,ball,team)
|     | C O | =                       |     |     |     |     | (14) |     |                           |     |     |     |     |     |
| --- | --- | ----------------------- | --- | --- | --- | --- | ---- | --- | ------------------------- | --- | --- | --- | --- | --- |
|     |     | P(game∨sport∨ball∨team) |     |     |     |     |      | 3.1 | Segmentationofwordsubsets |     |     |     |     |     |
Fitelson [8] evaluated a single word in the context of all Following[7],coherenceofawordsetmeasuresthedegree
subsets that can be constructed from the remaining words. that a subset is supported by another subset. The result of
The set of all subsets without word w is denoted by S(i). the segmentation of a given word set W is a set of pairs of
i
|     |     |     |     |     |     |     |     | subsetsofW. |     | Thedefinitionofasubsetpairconsistsoftwo |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --------------------------------------- | --- | --- | --- | --- |
Fitelson’scoherenceisdefinedbycomparingtheprobability
partsthataredifferentlyusedbythefollowingconfirmation
| of  | the i-th | word | with every | single          | set in | S(i): |     |            |                                           |     |     |     |     |     |
| --- | -------- | ---- | ---------- | --------------- | ------ | ----- | --- | ---------- | ----------------------------------------- | --- | --- | --- | --- | --- |
|     |          |      |            |                 |        |       |     | mearsures. | Thefirstpartofapairisthesubsetforwhichthe |     |     |     |     |     |
|     |          |      | (cid:80)N  | (cid:80)2N−1−1m |        |       |     |            |                                           |     |     |     |     |     |
f (w i ,S(i) j ) support by the second part of the pair is determined. Most
|     |     | C = | i=1 | j= 1 |     |     | (15) |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ---- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
F N · (2N−1− 1) proposed coherence measures for topic evaluation compare
|     |     |     |     |             |          |               |     | pairs of | single | words, | e.g., the | UCI coherence. |     | Every single |
| --- | --- | --- | --- | ----------- | -------- | ------------- | --- | -------- | ------ | ------ | --------- | -------------- | --- | ------------ |
|     |     |     | P ( | W | S ( i ) | ) −P ( W | | ¬ S ( i ) ) |     |          |        |        |           |                |     |              |
m (w ,S(i) )= i j i j (16) 3 In s e c t i o n 3 .1 , w e w i ll g i v e an e x a m p le fo r S o n e w h ic h is t he
|     | f   | i j |     |     |     |     |     |     |     |     |     |     | a n | y   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
P ( W i | S ( i ) j )+ P ( W i | ¬ S ( i ) j ) e q ui v a l e n t t o t h e (w , S ( i ) ) pa i r s of F it el so n ’ s c oh e r en ce .
|     |     |     |     |     |     |     |     |     |     | i   | j   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
401

|     |              |     |     | Probability |     |     | Confirmation |     |             |     |     |     |
| --- | ------------ | --- | --- | ----------- | --- | --- | ------------ | --- | ----------- | --- | --- | --- |
|     | Segmentation |     |     |             |     |     |              |     | Aggregation |     |     |     |
|     |              |     |     | Calculation |     |     | Measure      |     |             |     |     |     |
|     | t            |     | S   |             |     | P   |              | φ   |             |     | c   |     |
Reference
Corpus
Figure 1: Overview over the unifying coherence framework—its four parts and their intermediate results.
| word is    | paired with every  | other | single  | word. Those | sege-    |     |     |     |     |     |     |     |
| ---------- | ------------------ | ----- | ------- | ----------- | -------- | --- | --- | --- | --- | --- | --- | --- |
| mentations | are called one-one |       | and are | defined as  | follows: |     |     |     |     |     |     |     |
(cid:110)
|     | Sone (W(cid:48),W∗)|W(cid:48) |     |          |     |           |      |     |     |     |     |     |     |
| --- | ----------------------------- | --- | -------- | --- | --------- | ---- | --- | --- | --- | --- | --- | --- |
|     | one =                         |     | ={w i }; |     |           |      |     |     |     |     |     |     |
|     |                               |     |          |     | (cid:111) | (17) |     |     |     |     |     |     |
W∗
={w j };w i ,w j ∈W;i(cid:54)=j
(cid:110)
|     | Sone (W(cid:48),W∗)|W(cid:48) |     |          |     |           |      |     |     |     |     |     |     |
| --- | ----------------------------- | --- | -------- | --- | --------- | ---- | --- | --- | --- | --- | --- | --- |
|     | pre =                         |     | ={w i }; |     |           |      |     |     |     |     |     |     |
|     |                               |     |          |     | (cid:111) | (18) |     |     |     |     |     |     |
W∗
={w j };w i ,w j ∈W;i>j
(cid:110)
|     | Sone (W(cid:48),W∗)|W(cid:48) |     |          |     |           |      |     |     |     |     |     |     |
| --- | ----------------------------- | --- | -------- | --- | --------- | ---- | --- | --- | --- | --- | --- | --- |
|     | suc =                         |     | ={w i }; |     |           |      |     |     |     |     |     |     |
|     |                               |     |          |     | (cid:111) | (19) |     |     |     |     |     |     |
W∗
={w j };w i ,w j ∈W;i<j
| The latter | two are variations |         | of the first | one that    | require |     |     |     |     |     |     |     |
| ---------- | ------------------ | ------- | ------------ | ----------- | ------- | --- | --- | --- | --- | --- | --- | --- |
| an ordered | word set. They     | compare |              | a word only | to      | the |     |     |     |     |     |     |
precedingandsucceedingwordsrespectively,asdonebythe
UMass coherence.
Douven and Meijs [7] proposed several other segmenta- Figure 2: S o n e,S o n e,S o n e and S a n y segmentations of
|     |     |     |     |     |     |     |     | o n e a l l | a n y | a n y |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----- | ----- | --- | --- |
tions that have been adapted to topic evaluation by [16]. the word set {game, ball, sport, team} and their
hierarchy.
Thesedefinitionsallowoneorbothsubsetstocontainmore
| than one | single word. |     |     |     |     |     |                           |     |     |     |     |     |
| -------- | ------------ | --- | --- | --- | --- | --- | ------------------------- | --- | --- | --- | --- | --- |
|          |              |     |     |     |     |     | 3.2 ProbabilityEstimation |     |     |     |     |     |
(cid:110)
Sone = (W(cid:48),W∗)|W(cid:48) ={w }; The method of probability estimation defines the way
| all |     |     | i   |     |     |      |                       |     |              |     |            |      |
| --- | --- | --- | --- | --- | --- | ---- | --------------------- | --- | ------------ | --- | ---------- | ---- |
|     |     |     |     |     |     | (20) | how the probabilities | are | derived from | the | underlying | data |
(cid:111)
w ∈W;W∗ =W \{w } source. Boolean document (P ) estimates the probability
|     | i   |     | i   |     |     |     |             |             | bd        |           |     |           |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | --------- | --------- | --- | --------- |
|     |     |     |     |     |     |     | of a single | word as the | number of | documents | in  | which the |
(cid:110)
Sone = (W(cid:48),W∗)|W(cid:48) ={w }; word occurs divided by the total number of documents. In
| any |     |     | i   |     |     |      |                                                     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --------------------------------------------------- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     | (21) | thesameway,thejointprobabilityoftwowordsisestimated |     |     |     |     |     |
(cid:111)
w ∈W;W∗ ⊆W \{w } bythenumberofdocumentscontainingbothwordsdivided
|     | i         |     | i   |     |           |     |                              |     |     |                      |     |     |
| --- | --------- | --- | --- | --- | --------- | --- | ---------------------------- | --- | --- | -------------------- | --- | --- |
|     |           |     |     |     |           |     | bythetotalnumberofdocuments. |     |     | Thisestimationmethod |     |     |
|     | (cid:110) |     |     |     | (cid:111) |     |                              |     |     |                      |     |     |
S a n y = (W(cid:48),W∗)|W(cid:48),W∗ ⊂W;W(cid:48)∩W∗ =∅ (22) is called boolean as the number of occurrences of words in
a n y
|     |     |     |     |     |     |     | a single document | as well | as distances | between |     | the occur- |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | ------- | ------------ | ------- | --- | ---------- |
Sone compareseverysinglewordtoallotherwordsofthe
| all |     |     |     |     |     |     | rences are | not considered. | UMass | coherence | is  | based on |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --------------- | ----- | --------- | --- | -------- |
Sone extendsSone
wordset. any all byusingeverysubsetascondi- an equivalent kind of estimation [12]. Text documents with
Sany
tion. any is another extension that compares every subset someformattingallowsimplevariations,namelytheboolean
with every other disjoint subset. Figure 2 shows the differ- paragraph (P ) and boolean sentence (P ). These estima-
|     |     |     |     |     |     |     |     | bp  |     | bs  |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ent sets of subset pairs produced by applying the different tionmethodsaresimilartobooleandocument exceptinstead
segmentations to the running example. ofdocumentsparagraphsorsentencesareusedrespectively.
The approach in [1] compares words to the total word Booleanslidingwindow (P )determineswordcountsus-
sw
set W using words context vectors. Therefore, we define ing a sliding window.4 The window moves over the docu-
another segmentation ments one word token per step. Each step defines a new
|      |                          |     |       |     |           |     | virtual document | by copying | the window |     | content. | Boolean |
| ---- | ------------------------ | --- | ----- | --- | --------- | --- | ---------------- | ---------- | ---------- | --- | -------- | ------- |
|      | (cid:110)                |     |       |     | (cid:111) |     |                  |            |            |     |          |         |
| Sone | (W(cid:48),W∗)|W(cid:48) |     | ∈W;W∗ |     |           |     |                  |            |            |     |          |         |
set = ={w i };w i =W (23) document isappliedtothesevirtualdocumentstocompute
| Note that | this segmentation | does | not obey | the requirement |     |     |     |     |     |     |     |     |
| --------- | ----------------- | ---- | -------- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
W(cid:48)∩W∗ =∅statedin[7]. Therefore,itisonlyusedtogether 4The window size is added to the name, e.g., P for a
sw(10)
with coherence measures based on the ideas in [1]. sliding window of size s=10.
402

word probabilities. Note that boolean sliding window cap- Why is this an advantage? For example, assume word x
tures to some degree proximity between word tokens. semantically supports word z but they do not appear fre-
quently together in the reference corpus and have therefore
3.3 ConfirmationMeasure low joint probability. Thus, their direct confirmation would
AconfirmationmeasuretakesasinglepairS =(W(cid:48),W∗) belowaswell. However,theconfirmationsofxandzcorre-
i
ofwordsorwordsubsetsaswellasthecorrespondingproba- late with respect to many other words y in W. An example
bilitiestocomputehowstrongtheconditioningwordsetW∗ is that x and z are both competing brands of cars, which
supportsW(cid:48). Thiscouldbedoneeitherdirectlyasproposed semantically support each other. However, both brands are
in [7, 12, 13] or indirectly as done in [1]. seldom mentioned together in documents in the reference
corpus. But their confirmations to other words like“road”
3.3.1 Directconfirmationmeasures or “speed” do strongly correlate. This would be reflected
by an indirect confirmation measure. Thus, indirect confir-
Measurestodirectlycomputetheconfirmationofasingle
mation measures may capture semantic support that direct
pair S of words or word subsets are:
i
measures would miss.
m (S )=P(W(cid:48)|W∗)−P(W(cid:48)) (24) Thisideacanbeformalizedbyrepresentingthewordsets
d i
W(cid:48) and W∗ as vectors with dimension of the total size of
P(W(cid:48),W∗)
m (S )= (25) thewordsetW. Suchvectorcanbecomputedwithrespect
r i P(W(cid:48))∗P(W∗) to any direct confirmation measure m. In case W(cid:48) and W∗
P(W(cid:48),W∗)+(cid:15) consistofsinglewords,thevectorelementsarejustthedirect
m (S )=log (26)
lr i P(W(cid:48))∗P(W∗) confirmations as suggested in [1]. In case W(cid:48) and W∗ are
m (S ) setsofmorethanoneword,thevectorelementsarethesum
m nlr (S i )= −log(P(W lr (cid:48),W i ∗)+(cid:15)) (27) of the direct confirmations of the single words. Following
[1], the vector elements can be non-linearly distorted.
P(W(cid:48)|W∗)
m(S )= (28)  
l i P(W(cid:48)|¬W∗)+(cid:15) (cid:126)v (W(cid:48))=  (cid:88) m(w ,w )γ  (34)
P(W(cid:48)|W∗)+(cid:15) m,γ i j
m ll (S i )=log P(W(cid:48)|¬W∗)+(cid:15) (29)  wi∈W(cid:48)  j=1,...,|W|
P(W(cid:48),W∗) Given context vectors (cid:126)u = (cid:126)v(W(cid:48)) and w(cid:126) = (cid:126)v(W∗) for the
m c (S i )= P(W∗) (30) word sets of a pair S i = (W(cid:48),W∗), indirect confirmation
is computed as vector similarity. Following [1], we equip
P(W(cid:48),W∗)+(cid:15)
m (S )=log (31) our framework with the vector similarities cosine, dice and
lc i P(W∗)
jaccard:
P(W(cid:48),W∗)
m j (S i )= P(W(cid:48)∨W∗) (32) s ((cid:126)u,w(cid:126))= (cid:80)| i W =1 |u i ·w i (35)
cos (cid:107)(cid:126)u(cid:107) ·(cid:107)w(cid:126)(cid:107)
P(W(cid:48),W∗)+(cid:15) 2 2
m lj (S i )=log P(W(cid:48)∨W∗) (33) s ((cid:126)u,w(cid:126))= (cid:80)| i W =1 |min(u i ,w i ) (36)
dice (cid:80)|W|v
+w
In [7], the confirmation measures m , m and m are called i=1 i i
difference-, ratio- and likelihood-me d asure r . There l , log-likeli- s ((cid:126)u,w(cid:126))= (cid:80)| i W =1 |min(u i ,w i ) (37)
hood (m ll ) and log-ratio measure (m lr ) are also defined— jac (cid:80)| i W =1 |max(u i ,w i )
the last is the PMI, the central element of the UCI coher-
Thus,givenasimilaritymeasuresim,adirectconfirmation
ence. Normalized log-ratio measure (m ) is the NPMI.
nlr
measuremandavalueforγ,anindirectconfirmationmea-
The log-conditional-probability measure (m ) is equivalent
lc
sure m˜ is
to the calculation used by UMass coherence [12]. The last
two confirmation measures are the Jaccard and log-Jaccard m˜ (W(cid:48),W∗)=s ((cid:126)v (W(cid:48)),(cid:126)v (W∗)) (38)
sim(m,γ) sim m,γ m,γ
measures.
A small constant (cid:15) is added to prevent logarithm of zero. 3.4 Aggregation
Following [18], we set it to a small value ((cid:15)=10−12).5 Ols- Finally, all confirmations ϕ(cid:126) = {ϕ ,...ϕ } of all subset
1 |S|
son’sandFitelson’scoherencesaswellasalogarithmicvari- pairs S are aggregated to a single coherence score. Arith-
i
ant of Shogenji’s coherence (formulas 12, 16 and 11) are metic mean (σ ) and median (σ ) have been used in the
a m
denoted by m o , m f and m ls . literature. Additionally, we evaluate geometric mean (σ g ),
harmonic mean (σ ), quadratic mean (σ ), minimum (σ )
3.3.2 Indirectconfirmationmeasures h q n
and maximum (σ ).
x
Instead of directly computing the confirmation of S =
i
(W(cid:48),W∗),indirectcomputationofconfirmationassumesthat 3.5 Representationofexistingmeasures
givensome wordof W, direct confirmationsof words inW(cid:48) Nowwearereadytodescribeallcoherencemeasuresfrom
areclosetodirectconfirmationsofwordsinW∗withrespect section 2 as instances within the new framework. The co-
to this given word. Thus, indirect confirmation computes herences of [12, 13, 1] can be written as:
similarity of words in W(cid:48) and W∗ with respect to direct C = (cid:0) P ,Sone,m ,σ (cid:1) (39)
confirmations to all words. UMass bd pre lc a
C = (cid:0) P ,Sone,m ,σ (cid:1) (40)
UCI sw(10) one lr a
5Additionally(cid:15)isusedinm l andm ll forpreventingdivision C = (cid:0) P ,Sone,m ,σ (cid:1) (41)
by 0. NPMI sw(10) one nlr a
403

|     |     | Name       |       |     | 20NG    |           | Genomics    | NYT   | RTL-NYT | RTL-Wiki    |         |          | Movie  |     |
| --- | --- | ---------- | ----- | --- | ------- | --------- | ----------- | ----- | ------- | ----------- | ------- | -------- | ------ | --- |
|     |     | Topics     |       |     | 100     |           | 100         | 100   |         | 1095        | 1096    |          | 100    |     |
|     |     | Top        | words |     |         | 10        |             | 10 10 |         | 5           |         | 5        | 5      |     |
|     |     | Documents  |       |     | 19952   |           | 29833       | —     |         | —           | 7838    |          | 108952 |     |
|     |     | Paragraphs |       |     | 155429  |           | 2678088     | —     |         | —           | 319859  | 2136811  |        |     |
|     |     | Sentences  |       |     | 341583  |           | 9744966     | —     |         | —           | 1035265 | 6583202  |        |     |
|     |     | Tokens     |       |     | 2785319 | 114065923 |             | —     |         | — 13679052  |         | 86256415 |        |     |
|     |     | Vocabulary |       |     | 109610  |           | 1640456     | —     |         | —           | 591957  | 1625124  |        |     |
|     |     |            |       |     | Table   |           | 1: Datasets | used  | for     | evaluation. |         |          |        |     |
Thecoherencesdefinedin[7]andtransformedin[16]canbe rankingsarecorrelatedusingPearson’sr. Thus,goodqual-
written as: ityofacoherencemeasureisindicatedbyalargecorrelation
|     |     |     |     |     |     |     |     |     | to human | ratings. |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | -------- | --- | --- | --- | --- |
o n e,m
C one-all =(P bd ,S d ,σ a ) (42) WordcountsandprobabilitiesarederivedfromWikipedia.
a l l
(cid:0) ,Sone,m (cid:1) Incasethecorpus,whichwasusedastrainingdatafortopic
|     |     | C one-any | = P | bd  | d ,σ | a   |     | (43) |     |     |     |     |     |     |
| --- | --- | --------- | --- | --- | ---- | --- | --- | ---- | --- | --- | --- | --- | --- | --- |
any learning, was available, we computed coherence measures a
|     |     |           | (cid:0) | ,Sany,m |      | (cid:1) |     |      |        |            |        |         |                   |     |
| --- | --- | --------- | ------- | ------- | ---- | ------- | --- | ---- | ------ | ---------- | ------ | ------- | ----------------- | --- |
|     |     | C any-any | = P     | bd any  | d ,σ | a       |     | (44) |        |            |        |         |                   |     |
|     |     |           |         |         |      |         |     |      | second | time using | counts | derived | from that corpus. |     |
Shogenji’s [17], Olsson’s [14] and Fitelson’s [8] coherences Duringevaluation,wetestedawiderangeofdifferentpa-
do not define how the probabilities are computed. There- rameter settings. Window sizes varied between [10,300] for
|             |         |             |     |     |             |     |            |     | theslidingand[5,150]forthecontextwindow. |     |     |     |     | Theparam- |
| ----------- | ------- | ----------- | --- | --- | ----------- | --- | ---------- | --- | ---------------------------------------- | --- | --- | --- | --- | --------- |
| fore, these | measure | definitions |     | can | be combined |     | with every |     |                                          |     |     |     |     |           |
estimation6: eterγvariedin{1,2,3}. Overall,ourevaluationcomprisesa
| method | of probability |     |     |     |     |     |     |     |       |           |           |            |                        |     |
| ------ | -------------- | --- | --- | --- | --- | --- | --- | --- | ----- | --------- | --------- | ---------- | ---------------------- | --- |
|        |                |     |     |     |     |     |     |     | total | of 237912 | different | coherences | and parameterizations. |     |
(cid:16) (cid:17) In literature, other evaluation methods has been used as
|     |     | C   | = ·,Sall,m |     | ,σ  |     |     | (45) |     |     |     |     |     |     |
| --- | --- | --- | ---------- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- |
S one ls a well, e.g., humans were asked to classify word sets using
C = (cid:0) ·,Sset,m ,σ (cid:1) (46) different given error types [12]. However, since the data is
|     |     | O   |                    | set | o i        |     |     |      |             |            |     |         |                  |         |
| --- | --- | --- | ------------------ | --- | ---------- | --- | --- | ---- | ----------- | ---------- | --- | ------- | ---------------- | ------- |
|     |     |     |                    |     |            |     |     |      | not freely  | available, | we  | can not | use such methods | for our |
|     |     | C   | = (cid:0) ·,Sone,m |     | ,σ (cid:1) |     |     | (47) |             |            |     |         |                  |         |
|     |     | F   |                    | any | f a        |     |     |      | evaluation. |            |     |         |                  |         |
Using the context-window-based probability estimation A dataset comprises a corpus, topics and human ratings.
P described in section 2, we are able to formulate the Topicshadbeencomputedusingthecorpusandaregivenby
cw
context-vector-based coherences defined in [1] within our wordsetsconsistingofthetopicstopwords. Humanratings
framework7: for topics had been created by presenting these word sets
|     |     |         |     |     |     |         |     |     | tohumanraters. |     | Topicsareratedregardinginterpretability |     |     |     |
| --- | --- | ------- | --- | --- | --- | ------- | --- | --- | -------------- | --- | --------------------------------------- | --- | --- | --- |
|     |     | (cid:0) |     |     |     | (cid:1) |     |     |                |     |                                         |     |     |     |
C = P ,Sone,m˜ ,σ (48) andunderstandabilityusingthreecategories—good,neutral
|     |     | cos     | cw(5)    | one | cos(nlr,γ) | a   |         |      |        |       |     |     |     |     |
| --- | --- | ------- | -------- | --- | ---------- | --- | ------- | ---- | ------ | ----- | --- | --- | --- | --- |
|     |     | (cid:0) |          |     |            |     | (cid:1) |      | or bad | [13]. |     |     |     |     |
|     | C   | = P     | ,Sone,m˜ |     |            | ,σ  |         | (49) |        |       |     |     |     |     |
dice cw(5) one dice(nlr,γ) a The generation of such a dataset is expensive due to the
|     |     | (cid:0) |     |     |     | (cid:1) |     |     |     |     |     |     |     |     |
| --- | --- | ------- | --- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
C = P ,S o n e,m˜ ,σ (50) necessary manual work to create human topic ratings. Re-
|     |     | jac | cw(5) | o n e | jac(nlr,γ) | a   |     |     |     |     |     |     |     |     |
| --- | --- | --- | ----- | ----- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:0) (cid:1) cently, several datasets have been published [1, 6, 10, 16].
|     | C   | = P | ,Sone,m˜ |     |     | ,σ  |     | (51) |     |     |     |     |     |     |
| --- | --- | --- | -------- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- |
cen cw(5) set cos(nlr,γ) a Additionally, the creation of such a dataset is separated
Thisshowsthattheframeworkcancoverallexistingmea- from the topic model used to compute the topics, since the
sures. However, it allows to construct new measures that humans rate just plain word sets without any information
combine the ideas of existing measures. about the topic model [1, 6, 10, 15, 16]. This opens the
|     |     |     |     |     |     |     |     |     | possibility | to reuse     | them     | for evaluation. |                |          |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ------------ | -------- | --------------- | -------------- | -------- |
|     |     |     |     |     |     |     |     |     | The         | 20NG dataset | contains |                 | the well known | 20 News- |
4. EVALUATIONANDDATASETS
|     |     |     |     |     |     |     |     |     | groups | corpus that | consists | of  | Usenet messages | of 20 dif- |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | ----------- | -------- | --- | --------------- | ---------- |
Theevaluationfollowsacommonschemethathasalready ferent groups. The Genomics corpus comprises scientific
been used in [1, 10, 13, 16]. Coherence measures are com- articles of 49 MEDLINE journals and is part of the TREC-
puted for topics given as word sets that have been rated Genomics Track8. Aletras and Stevenson [1] published 100
by humans with respect to understandability. Each mea- rated topics for both dataset, each represented by a set of
|               |     |           |     |            |      |             |     |     | 10topwords. | Further,theypublished100ratedtopicsthat |     |     |     |     |
| ------------- | --- | --------- | --- | ---------- | ---- | ----------- | --- | --- | ----------- | --------------------------------------- | --- | --- | --- | --- |
| sure produces |     | a ranking | of  | the topics | that | is compared |     | to  |             |                                         |     |     |     |     |
therankinginducedbyhumanratings. Following[10],both have been computed using 47229 New York Times articles
|     |     |     |     |     |     |     |     |     | (NYT). | Unfortunately, |     | this corpus | is not available | to us. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | -------------- | --- | ----------- | ---------------- | ------ |
6Sall
is used to formulate Shogenji’s coherence and is de- Chang et al. [6] used two corpora, one comprising New
| one | Sone |     | W(cid:48) |     | W∗  |     | Sset |     |     |     |     |     |     |     |
| --- | ---- | --- | --------- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
fined like but with and swapped. = YorkTimesarticles(RTL-NYT)andtheotherisaWikipedia
| {(W(cid:48),W∗)|W(cid:48),W∗ | all |     |     |     |     |     | set |     |     |     |     |     |     |     |
| ---------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
= W} is used for Olsson’s coherence. subset (RTL-Wiki). A number of 900 topics were created
Note that Sset contains only one single pair. Therefore, for each of these corpora. [10] published human ratings for
set
the aggregation function is the identity function σ i . These these topics. Human raters evaluated word subsets of size
| special | segmentation |     | schemas | are | used | only for | these | two |                                                 |     |     |     |     |     |
| ------- | ------------ | --- | ------- | --- | ---- | -------- | ----- | --- | ----------------------------------------------- | --- | --- | --- | --- | --- |
|         |              |     |         |     |      |          |       |     | fiverandomlyselectedfromthetopwordsofeachtopic. |     |     |     |     | We  |
coherences.
|           |        |      |        |       |       |       |     |     | aggregated | the | ratings | for each | word set. Word | sets with |
| --------- | ------ | ---- | ------ | ----- | ----- | ----- | --- | --- | ---------- | --- | ------- | -------- | -------------- | --------- |
| 7We added | window | size | to the | model | name, | e.g., | P   | for |            |     |         |          |                |           |
cw(5)
| the window               | size      | s = | ±5. The   | context      | window    |     | is only  | used |     |     |     |     |     |     |
| ------------------------ | --------- | --- | --------- | ------------ | --------- | --- | -------- | ---- | --- | --- | --- | --- | --- | --- |
| for indirect             | coherence |     | measures. | For          | represent | all | measures |      |     |     |     |     |     |     |
| mentionedin[1]insteadofm |           |     |           | themeasuresm |           |     | orm      | =    |     |     |     |     |     |     |
|                          |           |     |           | nlr          |           |     | lr       | P    |     |     |     |     |     |     |
P(W(cid:48),W∗) could be used respectively. 8http://ir.ohsu.edu/genomics
404

secnerehoc
Name C C C C C C C
V P UMass one-any UCI NPMI A
S Sone Sone Sone Sone Sone Sone Sone
set pre pre any one one one
P P P P P P P P
sw(110) sw(70) bd bd sw(10) sw(10) cw(5)
M m˜ m m m m m m˜
cos(nlr,1) f lc d lr nlr cos(nlr,1)
Σ σ σ σ σ σ σ σ
a a a a a a a
suproc
gnisu
20NG 0.665 0.756 0.395 0.563 0.312 0.486 0.563
Genomics 0.671 0.652 0.514 0.549 0.624 0.630 0.632
RTL-Wiki 0.627 0.615 0.272 0.545 0.527 0.573 0.542
Movie 0.548 0.549 0.093 0.453 0.473 0.438 0.431
average 0.628 0.643 0.319 0.528 0.484 0.532 0.542
aidepikiW
eht
gnisu
01=
N
20NG 0.859 0.825 0.562 0.822 0.696 0.780 0.739
Genomics 0.773 0.721 0.442 0.452 0.478 0.594 0.530
NYT 0.803 0.757 0.543 0.612 0.783 0.806 0.747
average 0.812 0.768 0.516 0.629 0.652 0.727 0.672
5=
N
RTL-NYT 0.728 0.720 0.106 0.438 0.631 0.678 0.687
RTL-Wiki 0.679 0.645 0.350 0.499 0.558 0.606 0.602
Movie 0.544 0.533 0.143 0.454 0.447 0.452 0.465
average 0.650 0.633 0.200 0.464 0.545 0.579 0.585
average 0.731 0.700 0.358 0.546 0.599 0.653 0.628
Table 2: Coherence measures with strongest correlations with human ratings.
less than three ratings or words with encoding errors are
0.74
removed.9
0.72
The RTL-Wiki corpus is published in bag-of-words for- 0.7
n
m
ba
a
s
t
ed
th
p
a
r
t
o
i
b
s
a
u
b
n
il
s
i
u
ty
ita
es
b
t
l
i
e
m
f
a
o
t
r
io
p
n
a
s
r
.
ag
T
r
h
ap
er
h
e
-
f
,
o
s
r
e
e
n
,
t
w
en
e
c
h
e
a
-
v
o
e
r
r
w
et
in
ri
d
e
o
v
w
ed
-
el
ati o
0
0
.
.
6
6
6
8
the articles in version of May 2009 from Wikipedia history orr 0.64
records. Notallarticlesoftheoriginalcorpuswereavailable c 0.62
0.6
anymore. Therefore,therecreatedcorpusisslightlysmaller
0.58
than the original one.
0 50 100 150 200 250 300
Rosneretal.[16]publishedtheMoviecorpus—aWikipedia
window size
subset—and100ratedtopics. Topicsaregivenassetsoffive
topwords. LiketheRTL-Wikicorpusthiscorpuswasrecre- variants of CV variants of CUCI
ated and is slightly smaller than the original one. variants of CP variants of CNPMI
Table1showsanoverviewofsizesofthedifferentdatasets
Figure 3: The influence of the sliding window’s size
used for evaluation. All corpora as well as the complete
onthecorrelationofvariantsofdifferentcoherences
Wikipedia used as reference corpus are preprocessed using
and human ratings.
lemmatization and stop word removal. Additionally, we re-
moved portal and category articles, redirection and disam-
evaluation of the topic quality is harder, if the number of
biguation pages as well as articles about single years.
top words N is small.
Lookingatalreadyproposedcoherencemeasures(fivemost
rightcolumnsoftable2),ourresultsconfirmthatonaverage
5. RESULTSANDDISCUSSION
UCIcoherenceperformsbetterwithNPMI.Amongalready
Table 2 shows the best performing coherence measures proposedcoherencemeasures,theNPMIshowedbestoverall
with respect to the different datasets.10 performance. Slightlylowercorrelationsareobtainedbythe
The largest correlations for all datasets (except for the bestperformingvector-basedcoherenceofthoseproposedin
Movie dataset) were reached, when the coherence measures [1]. UMass coherence has lower correlations—especially in
reliedonprobabilitiesderivedfromtheWikipediainsteadof cases of small word sets. Shogenji’s (0.034) and Olsson’s
the corpus used for topic learning. We focus our discussion (0.218) coherences (not shown in table 2) have low corre-
on these calculations. lations, while Fitelson’s coherence (0.541) is comparable to
Most correlations computed for topics with 10 top words C proposed in [16].
one−any
are higher than those of topics with 5 top words. Thus, Thebestperformingcoherencemeasure(themostleftcol-
umn) is a new combination found by systematic study of
9TheRTL-Wikidatasetcontains23wordsetswith6words the configuration space of coherence measures. This mea-
andmorethan3ratingsthatwereremovedaswelltoensure sure (C ) combines the indirect cosine measure with the
V
comparability of ratings NPMI and the boolean sliding window. This combination
10Further results can be found in the supplementary mate- has been overlooked so far in the literature. Also, the best
rial. ResultsdifferingtoAletrasandStevenson[1]mightbe
directcoherencemeasure(C )foundbyourstudyisanew
causedbyadifferentpreprocessinganddifferentversionsof P
combination. It combines Fitelson’s confirmation measure
the Wikipedia.
405

Name direct indirect indirect
Name direct
m˜ m˜ m˜
P 0.648 0.664 cos dice jac
bd
P 0.679 0.698 m 0.581 0.619 0.628 0.626
bp c
P 0.664 0.691 m 0.623 0.675 0.676 0.664
bs d
P 0.700 0.731 m 0.700 0.685 0.453 0.539
sw(70) f
P 0.668 0.731 m 0.478 0.582 0.592 0.576
sw(110) j
P — 0.695 m 0.381 0.388 0.380 0.380
cw(50) l
m 0.493 0.374 0.238 0.238
Sany 0.617 0.730 lc
any m 0.574 0.249 0.210 0.205
Sone 0.456 0.728 lj
all m 0.582 0.563 0.472 0.507
Sone 0.648 0.730 ll
any m 0.632 0.714 0.672 0.670
Sone 0.699 0.711 lr
one m 0.172 0.714 0.672 0.670
Sone 0.700 0.711 ls
pre m 0.693 0.731 0.689 0.691
Sone 0.695 0.711 nlr
suc m 0.478 0.582 0.592 0.576
Sone — 0.731 o
set m — 0.575 0.605 0.590
P
σ a 0.700 0.731 m r 0.378 0.605 0.577 0.557
σ 0.468 0.606
g
σ 0.457 0.590 Table4: Bestcorrelationsfortheconfirmationmea-
h
σ 0.659 0.730 sures used directly or combined with an inderect
m
σ 0.482 0.573 confirmation measure.
n
σ 0.648 0.716
q corpus coherence average
σ 0.513 0.670
x left out P S M Σ correlation
Table 3: Best correlations for the probability es- 20NG (P ,Sany,m˜ ,σ ) 0.708
timations, segmentations and aggregations if they sw110 any cos(nlr,1) m
Genomics (P ,Sone,m˜ ,σ ) 0.724
were combined with a direct or indirect confirma- sw70 set cos(nlr,1) a
tion measure. NYT (P sw110 ,S s o e n t e,m˜ cos(nlr,1) ,σ a ) 0.717
RTL-NYT (P ,Sone,m˜ ,σ ) 0.732
with the boolean sliding window. This one is still better sw110 set cos(nlr,1) a
RTL-Wiki (P ,Sone,m˜ ,σ ) 0.741
than published measures. sw110 set cos(nlr,1) a
Amongprobabilityestimationmethods,thebooleanpara- Movie (P ,Sone,m˜ ,σ ) 0.769
sw70 set cos(nlr,1) a
graph, boolean sentence and context window methods per-
Table 5: Coherence measures with the highest aver-
formedbetterthanthebooleandocument(seetable3). The
age correlations if one dataset has been left out.
booleanslidingwindowperformedbest,butthewindowsize
should be larger than proposed in [13]. Figure 3 shows the
three benefit from a combination with an indirect measure,
correlation to human ratings achieved by variants of C ,
V while the correlation of m drops.
C , UCI and NPMI with different window sizes. It shows f
P The small differences in correlation of coherences with a)
thatonlytheC coherencehasaveryhighcorrelationwith
P differentwindowsizesandb)segmenationmethodsthatare
a small window (s=10). The correlation of C and NPMI
V verysimilartoeachother,leadstoalargenumberofcoher-
remainsonahighlevel,whenthewindowsizeislargerthan
ences having a high average correlation that is only slightly
50. The UCI coherence benefits from a larger window size,
lower than the best performing coherence C . Thus, there
too,andreachesitsbestcorrelationats=70. Anexplana- V
are many variants of C that are performing very good as
tionforthegoodperformanceofthebooleanslidingwindow V
long as they use
isthatitimplicitlyrepresentsdistancesbetweenwordtokens
within large documents. Further, large documents that are
• a sliding window with a window size s≥50,
known to have good quality in Wikipedia, are implicitly up
• a segmentation method that takes larger subsets into
weighted because they contain more windows than smaller
account and
documents.
• σ or σ as summarization method.
a m
Amongthesegmentationmethods,ifadirectconfirmation
measure is used the single-word-based segmentation meth- We confirm this by generating leave one out averages by
ods(Sone,SoneandSone)havethehighestandSonehasthe calculating the average using only five of the six datasets.
one pre suc all
worstcorrelations. Thischangeswhenanindirectconfirma- Table5showsthatindependentlyfromthedatasetleftout,
tionmeasureisused. Whileallsegmentationmethodsreach C oroneofitsvariantsfullfillingthepointsaboveachieves
V
averyhighcorrelation,thesingle-word-basedsegmentations thehighestaveragecorrelation. Foreverycoherenceintable
have slightly lower correlations than those that take larger 2, figure 4 shows the six averages. It can be seen that the
subsets into account (Sany, Sone, Sone, Sone). set of averages of C only overlap with the averages of C
any any all set V P
The arithmetic mean is the aggregation with the highest and are clearly higher than those of the other coherences.
correlations. Combinedwithindirectconfirmationmeasures
the median and the quadratic mean created high correla-
6. RUNTIMES
tions, too.
Among the direct confirmation measures, only m , m , Nexttothequalityitisimportanttoknowthecostsofa
f nlr
m andm reachhighercorrelations(seetable4). Thelast certaincoherencemeasure. Therefore,wehaveanalyzedthe
lr d
runtimesofallcoherencemeasures. Forthisexperiment,we
used the 100 topics of the NYT dataset and the Wikipedia
406

|     |     |     |     |     |     |     |      |     |     |               | runtimes | in  | s   |
| --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | ------------- | -------- | --- | --- |
|     |     |     |     |     |     |     | Name |     | |S| |               |          |     |     |
|     |     |     |     |     |     |     |      |     |     | m cos(mnlr,1) |          |     | σ m |
Sone
|     |     |     |     |     |     |     | all  |     | N   |     | 0.002 | <0.001 |     |
| --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | ----- | ------ | --- |
|     |     |     |     |     |     |     | Sone |     | N   |     | 0.002 |        | —   |
set
|     |     |     |     |     |     |     | Sone |     | N·(N−1) |     | 0.002 | <0.001 |     |
| --- | --- | --- | --- | --- | --- | --- | ---- | --- | ------- | --- | ----- | ------ | --- |
|     |     |     |     |     |     |     | pre  |     | 2       |     |       |        |     |
|     |     |     |     |     |     |     | Sone |     | N·(N−1) |     | 0.002 | <0.001 |     |
|     |     |     |     |     |     |     | suc  |     | 2       |     |       |        |     |
Sone
|     |     |     |     |     |     |     |     |     | N ·(N −1) |     | 0.002 |     | 0.001 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | ----- | --- | ----- |
one
|     |     |     |     |     |     |     | Sone |     | ·(2(N−1)−1) |     |       |     |       |
| --- | --- | --- | --- | --- | --- | --- | ---- | --- | ----------- | --- | ----- | --- | ----- |
|     |     |     |     |     |     |     | any  | N   |             |     | 0.140 |     | 0.023 |
N −1(cid:0)(cid:0)N(cid:1)
|     |     |     |     |     |     |     | Sany | (cid:80) | ·(2i−1) | (cid:1) |       |     |       |
| --- | --- | --- | --- | --- | --- | --- | ---- | -------- | ------- | ------- | ----- | --- | ----- |
|     |     |     |     |     |     |     | any  |          |         |         | 1.436 |     | 0.322 |
i
| Figure | 4: The | leave | one | out averages | of the | coher- |     | i=1 |     |     |     |     |     |
| ------ | ------ | ----- | --- | ------------ | ------ | ------ | --- | --- | --- | --- | --- | --- | --- |
ence measures. Table 7: Different segmentation schemes, the num-
|     |     |     |     |     |     |     | ber of | subset | pairs S | they contain | (|S|) | and | exam- |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ | ------- | ------------ | ----- | --- | ----- |
i
Name runtime in s ples of their influence on runtimes of confirmation
|     |     |     |     |       |     |     | measures | and  | aggregations. |              |                 |     |     |
| --- | --- | --- | --- | ----- | --- | --- | -------- | ---- | ------------- | ------------ | --------------- | --- | --- |
|     |     | C V |     | 315.2 |     |     |          |      |               |              |                 |     |     |
|     |     | C P |     | 317.7 |     |     |          |      |               |              |                 |     |     |
|     |     |     |     |       |     |     | used in  | data | exploration   | systems like | TopicExplorer11 |     | [9] |
|     |     | C   |     | 13.7  |     |     |          |      |               |              |                 |     |     |
UMass that use word representations of topics to show the user
|     |     | C   |     | 13.7 |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
one-any
|     |     | C   |     | 356.1 |     |     | anoverviewoflargedocumentcollections. |     |     |     |     | Topicsthatcan- |     |
| --- | --- | --- | --- | ----- | --- | --- | ------------------------------------- | --- | --- | --- | --- | -------------- | --- |
UCI
C 356.1 notbeinterpretedarefilteredoutusingcoherencemeasures.
NPMI
C 301.8 Thus, usability of the system is increased by hiding topics
A
|     |     |     |     |     |     |     | that would | confuse | users. |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ------- | ------ | --- | --- | --- | --- |
Table 6: Runtimes on the NYT dataset and the Asexampletable8showsthefivetopicswithhighestand
Wikipedia as reference corpus. lowestcoherencerespectivelyofatotalof200topicsthatare
|     |     |     |     |     |     |     | computed | by  | Latent Dirichlet | Allocation |     | [3] using | English |
| --- | --- | --- | --- | --- | --- | --- | -------- | --- | ---------------- | ---------- | --- | --------- | ------- |
as reference corpus. Table 6 shows the overall runtimes of Wikipedia. Itclearlyshowsthedifferencebetweenthequal-
thecoherencemeasurestocomputetheresultspresentedin ityofthetopicrepresentationsasbesttopicsallowtoguess
table 2. a general topic while the worst topics are not interpretable.
For theruntimeofacoherencemeasure, themostimpor- However, coherence measures have applications beyond
| tant component |            | is the         | probability | estimation. | The               | fastest |                  |     |                  |              |      |           |          |
| -------------- | ---------- | -------------- | ----------- | ----------- | ----------------- | ------- | ---------------- | --- | ---------------- | ------------ | ---- | --------- | -------- |
|                |            |                |             |             |                   |         | topic models.    |     | First, precision | of key       | word | search    | in docu- |
| one is the     | boolean    | document       |             | that needed | only 13.7s        | to re-  |                  |     |                  |              |      |           |          |
|                |            |                |             |             |                   |         | ment collections |     | can profit       | by filtering | out  | documents | that     |
| trieve all     | neccessary | probabilities. |             | The         | boolean paragraph |         |                  |     |                  |              |      |           |          |
containthequerykeywordsinsomeproximitybutthewords
andthebooleansentencebasedestimationmethodsneeded
|     |     |     |     |     |     |     | are located | in  | nearby but | thematically | different |     | passages. |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ---------- | ------------ | --------- | --- | --------- |
34.4s and 138.8s. Both suffer from the fact that there are The approach would extract a word set for each document
muchmoreparagraphsandsentencesthansingledocuments. that covers the query words as well as the main words of
But they are still faster than the window based approaches the documents passage that contains the query words. Low
sincethereferencecorpuscanbedividedintoparagraphsor quality hits for the query are filtered out by setting a mini-
sentences while preprocessing the corpus. In contrast, both mum threshold for the coherence of the extracted word set.
windowbasedestimationmethodshadthehighestruntimes. Second, coherence can be used to select advertising links
This is caused by the need of retrieving the single positions that fits a web page. The approach is similar as above. A
| of the words | inside | the | documents | to  | check whether | these |     |     |     |     |     |     |     |
| ------------ | ------ | --- | --------- | --- | ------------- | ----- | --- | --- | --- | --- | --- | --- | --- |
wordsetisextractedfromawebpagethatcontainsthemost
| positions   | are inside | the             | same   | window.     | As parameters   | for       |                                   |                        |                    |         |                     |               |         |
| ----------- | ---------- | --------------- | ------ | ----------- | --------------- | --------- | --------------------------------- | ---------------------- | ------------------ | ------- | ------------------- | ------------- | ------- |
|             |            |                 |        |             |                 |           | describingwordsofthepagescontent. |                        |                    |         | Advertisinglinksare |               |         |
| the runtime | of         | all probability |        | calculation | we can identify | a)        |                                   |                        |                    |         |                     |               |         |
|             |            |                 |        |             |                 |           | selected                          | that                   | maximize coherence | of      | the union           | of            | the web |
| the number  | of         | topics,         | b) the | number of   | top words       | per topic |                                   |                        |                    |         |                     |               |         |
|             |            |                 |        |             |                 |           | page’s                            | wordsetwithdescriptive |                    | wordsof | the                 | respectivead. |         |
(N) and c) the size of the reference corpus. On the other Third,coherencecanbeusedtoimproveautomatictrans-
hand, the size of the window does not have an influence on lations of web pages. When using a dictionary to translate
the runtimes. a sentence from a web page into another language, usually
Anotherimportantcomponentisthesegmentation. While ambiguous translations of single words remain. Coherence
the segmentation of a specific topic is very fast, it controls measurescanbeusedselectthemostcoherentcombination
the number of confirmation values that have to be calcu- among the ambiguous translations.
lated. Thus,ithasahighimpactonthetimeneededbythe
| confirmation | measure |     | and the | aggregation | component. | Ta- |     |     |     |     |     |     |     |
| ------------ | ------- | --- | ------- | ----------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
8. CONCLUSION
| ble7showsthenumberofsubsetpairsS |     |     |     |     | thatthedifferent |     |     |     |     |     |     |     |     |
| -------------------------------- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
i
segmentations create and two examples of the influence of We proposed a unifying framework that span the space
this number on the runtime of confirmation measures and of all known coherence measures and allows to combine all
Sone Sany main ideas in the context of coherence quantification. We
| aggregations. |     | It can be | seen | that any | and any | have an |     |     |     |     |     |     |     |
| ------------- | --- | --------- | ---- | -------- | ------- | ------- | --- | --- | --- | --- | --- | --- | --- |
evaluated237912coherencemeasuresonsixdifferentbench-
| exponential | complexity. |     |     |     |     |     |         |             |              |               |         |                |           |
| ----------- | ----------- | --- | --- | --- | --- | --- | ------- | ----------- | ------------ | ------------- | ------- | -------------- | --------- |
|             |             |     |     |     |     |     | marks   | for topic   | coherence—to | the           | best of | our knowledge, |           |
|             |             |     |     |     |     |     | this is | the largest | number       | of benchmarks | used    | for            | topic co- |
7. APPLICATIONS
|     |     |     |     |     |     |     | herences | so far. | We introduced | coherence |     | measures | from |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------- | ------------- | --------- | --- | -------- | ---- |
Coherencemeasurescanbeappliedtoautomaticallyrate
quality of topics computed by topic models. This can be 11http://topicexplorer.informatik.uni-halle.de
407

coherence topic
0.94 company sell corporation own acquire purchase buy business sale owner
0.91 age population household female family census live average median income
0.86 jewish israel jew israeli jerusalem rabbi hebrew palestinian palestine holocaust
0.85 ship navy naval fleet sail vessel crew sink sea submarine
0.83 guitar album track bass drum vocal vocals release personnel list
...
0.35 number code type section key table block set example oth
0.34 group official website member site base oth form consist profile
0.34 part form become history change present create merge forme separate
0.29 know call name several refer oth hunter hunt thompson include
0.27 mark paul heart take read harrison follow become know include
Table 8: The five Wikipedia topics with highest and lowest coherences using best preforming measure C .
V
scientific philosophy that have been not used in the area of [5] L. Bovens and S. Hartmann. Bayesian Epistemology.
topic evaluation and—in the case of Fitelson’s coherence— Oxford University Press, 2003.
showedagoodperformance. Usingourframework,weiden- [6] J.Chang,S.Gerrish,C.Wang,J.L.Boyd-graber,and
tified measures that clearly outperform all coherences pro- D. M. Blei. Reading tea leaves: How humans interpret
posed so far. topic models. In Advances in Neural Information
Inthefuture,anextstepwillbeamoredetailedinvestiga- Processing Systems 22, pages 288–296. 2009.
tionontheslidingwindowandcouldbringupnewprobabil- [7] I. Douven and W. Meijs. Measuring coherence.
ityestimationmethods. Futureworkwillincludetransferof Synthese, 156(3):405–425, 2007.
coherencetootherapplicationsbeyondtopicmodels,which [8] B. Fitelson. A probabilistic theory of coherence.
can be done in a systematic way using the new unifying Analysis, 63(279):194–199, 2003.
framework. Hence, our research agenda may lead to com-
[9] A. Hinneburg, R. Preiss, and R. Schr¨oder.
pletelynewinsightsofthebehavioroftopicmodels. Finally,
Topicexplorer: Exploring document collections with
our open framework enables researchers to measure the im-
topic models. In ECML/PKDD (2), pages 838–841,
pactonacomparablebasisforfieldsofapplicationliketext
2012.
mining, information retrieval and the world wide web. Ad-
[10] J. H. Lau, D. Newman, and T. Baldwin. Machine
ditionally, it will be possible to finally evaluate the reasons
reading tea leaves: Automatically evaluating topic
forspecificbehaviorofstatistics-drivenmodelsanduncover
coherence and topic model quality. In Proc. of the
distinguishing properties of benchmarks.
Europ. Chap. of the Assoc. for Comp. Ling., 2014.
[11] D. Mimno and D. Blei. Bayesian checking for topic
9. ACKNOWLEDGMENTS models. In Proc. of the Conf. on Empirical Methods in
Natural Language Processing, pages 227–237. 2011.
WewanttothankJeyHanLauandJordanBoyd-Graber
for making their data available. A special thanks goes to [12] D.Mimno,H.M.Wallach,E.Talley,M.Leenders,and
NikosAletrasforpublishinghisdataandseveraldiscussions A. McCallum. Optimizing semantic coherence in topic
about his approach. The work of the first author has been models. In Proc. of the Conf. on Empirical Methods in
supported by the ESF and the Free State of Saxony. The Natural Language Processing, pages 262–272. 2011.
work of the last author has been partially [13] D. Newman, J. H. Lau, K. Grieser, and T. Baldwin.
supported by the Klaus Automatic evaluation of topic coherence. In Human
Tschira Foundation. Language Technologies: The 2010 Annual Conference
of the North American Chapter of the Association for
Computational Linguistics, pages 100–108. 2010.
10. REFERENCES
[14] E. Olsson. What is the problem of coherence and
truth? The Jour. of Philosophy, 99(5):246–272, 2002.
[1] N. Aletras and M. Stevenson. Evaluating topic
coherence using distributional semantics. In Proc. of [15] M. R¨oder, M. Speicher, and R. Usbeck. Investigating
the 10th Int. Conf. on Computational Semantics quality raters’ performance using interface evaluation
(IWCS’13), pages 13–22, 2013. methods.InInformatik 2013,pages137–139.GI,2013.
[2] L. Alsumait, D. Barbara´, J. Gentle, and [16] F. Rosner, A. Hinneburg, M. R¨oder, M. Nettling, and
C. Domeniconi. Topic significance ranking of lda A. Both. Evaluating topic coherence measures. CoRR,
generative models. In Proc. of the Europ. Conf. on abs/1403.6397, 2014.
Machine Learning and Knowledge Disc. in Databases: [17] T. Shogenji. Is coherence truth conducive? Analysis,
Part I, ECML PKDD ’09, pages 67–82, 2009. 59(264):338–345, 1999.
[3] D. M. Blei, A. Y. Ng, and M. I. Jordan. Latent [18] K. Stevens, P. Kegelmeyer, D. Andrzejewski, and
dirichlet allocation. Journal of Machine Learning D. Buttler. Exploring topic coherence over many
Research, 3:993–1022, 2003. models and many topics. In Proc. of the 2012 Joint
[4] G.Bouma.Normalized(pointwise)mutualinformation Conf. on Empirical Methods in Natural Language
in collocation extraction. In From Form to Meaning: Processing and Computational Natural Language
Processing Texts Automatically, Proc. of the Biennial Learning, EMNLP-CoNLL ’12, pages 952–961, 2012.
GSCL Conference 2009, pages 31–40, Tu¨bingen, 2009.
408