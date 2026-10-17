Inter and Intra Topic Structure Learning with Word Embeddings
|     |     |     | HeZhao1 | LanDu1 | WrayBuntine1 |     | MingyaunZhou2 |     |     |     |     |     |
| --- | --- | --- | ------- | ------ | ------------ | --- | ------------- | --- | --- | --- | --- | --- |
Abstract
|     |     |     |     |     |     |     | Table1. | Examplelocaltopicswithtop10words |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | -------------------------------- | --- | --- | --- | --- |
Oneimportanttaskoftopicmodelingfortextanal- journalsciencebiologyresearchjournals
1
ysisisinterpretability. Bydiscoveringstructured internationalcellpsychologyscientificbioinformatics
topicsoneisabletoyieldimprovedinterpretabil-
fitnesspianoguitarswimmingviolin
2
ity as well as modeling accuracy. In this paper, weightliftinglessonstrainingswimweight
weproposeanoveltopicmodelwithadeepstruc- taylorprinceswiftwilliam
3
jovibonwomangalapilljon
turethatexploresbothinter-topicandintra-topic
structuresinformedbywordembeddings. Specifi- sanautotheftgrandandreas
4
cally,ourmodeldiscoversintertopicstructuresin mobilegtagamerockstardecember
theformoftopichierarchiesanddiscoversintra
| topicstructuresintheformofsub-topics,eachof |     |     |     |     |     | interpretability. |     |     |     |     |     |     |
| ------------------------------------------- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- |
whichisinformedbywordembeddingsandcap-
|     |     |     |     |     |     | One | popular | direction | to explore | topic | structure | is using |
| --- | --- | --- | --- | --- | --- | --- | ------- | --------- | ---------- | ----- | --------- | -------- |
turesafine-grainedthematicaspectofanormal
thehierarchical/deeprepresentationoftextdata,suchasthe
topic.Extensiveexperimentsdemonstratethatour
nestedhierarchicalDirichletprocess(nHDP)(Paisleyetal.,
modelachievesthestate-of-the-artperformance
2015),DeepPoissonFactorAnalysis(DPFA)(Ganetal.,
| in terms | of perplexity, |           | document | classification, |         |                       |           |        |                             |     |       |               |
| -------- | -------------- | --------- | -------- | --------------- | ------- | --------------------- | --------- | ------ | --------------------------- | --- | ----- | ------------- |
|          |                |           |          |                 |         | 2015),                | and Gamma | Belief | Network                     |     | (GBN) | (Zhou et al., |
| and      | topic quality. | Moreover, |          | with topic      | hierar- |                       |           |        |                             |     |       |               |
|          |                |           |          |                 |         | 2016;Congetal.,2017). |           |        | Ingeneral,thesemodelsassume |     |       |               |
chiesandsub-topics,thetopicsdiscoveredinour
|     |     |     |     |     |     | that | topics in | the higher | layers | of  | a hierarchy | are more |
| --- | --- | --- | --- | --- | --- | ---- | --------- | ---------- | ------ | --- | ----------- | -------- |
modelaremoreinterpretable,providinganillumi-
|     |     |     |     |     |     | general/abstractthanthoseinthelowerlayers. |     |     |     |     |     | Therefore, |
| --- | --- | --- | --- | --- | --- | ------------------------------------------ | --- | --- | --- | --- | --- | ---------- |
natingmeanstounderstandtextdata.
byrevealinghierarchicalcorrelationsbetweentopics,topic
hierarchiesprovideanintuitivewaytounderstandtextdata.
1.Introduction
|     |     |     |     |     |     | In addition | to  | topic hierarchies, |     | we  | are also | interested in |
| --- | --- | --- | --- | --- | --- | ----------- | --- | ------------------ | --- | --- | -------- | ------------- |
analyzingthefine-grainedthematicstructurewithineachin-
Significantresearchefforthasbeendevotedtodeveloping
|          |               |               |     |               |       | dividualtopic. |     | Asweknow,inconventionalmodels,topics |     |     |     |     |
| -------- | ------------- | ------------- | --- | ------------- | ----- | -------------- | --- | ------------------------------------ | --- | --- | --- | --- |
| advanced | text analysis | technologies. |     | Probabilistic | topic |                |     |                                      |     |     |     |     |
arediscoveredlocallyfromthewordco-occurrencesina
modelssuchasLatentDirichletAllocation(LDA),arepop-
|     |     |     |     |     |     | corpus. | Sowereferthosetopicsaslocaltopics. |     |     |     |     | Duetothe |
| --- | --- | --- | --- | --- | --- | ------- | ---------------------------------- | --- | --- | --- | --- | -------- |
ularapproachesforthistask,whichdiscoverlatenttopics
limitationofthecontextofatargetcorpus,somelocaltopics
| from text | collections. | One | preferred | property | of proba- |     |     |     |     |     |     |     |
| --------- | ------------ | --- | --------- | -------- | --------- | --- | --- | --- | --- | --- | --- | --- |
maybehardtointerpretbecauseofthefollowingtwoef-
| bilistic topic | models | is interpretability: |     | one | can explain |     |     |     |     |     |     |     |
| -------------- | ------ | -------------------- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
fects: (1)Theycanmixthewordswhichco-occurlocallyin
| that a document | is  | composed | of topics | and a | topic is de- |     |     |     |     |     |     |     |
| --------------- | --- | -------- | --------- | ----- | ------------ | --- | --- | --- | --- | --- | --- | --- |
thetargetcorpusbutarelesssemanticallyrelatedingeneral;
| scribedbywords. | Althoughwidelyused,mostvariations |     |     |     |     |           |        |     |              |     |                |        |
| --------------- | --------------------------------- | --- | --- | --- | --- | --------- | ------ | --- | ------------ | --- | -------------- | ------ |
|                 |                                   |     |     |     |     | (2) Local | topics | can | be dominated |     | by specialized | words, |
ofstandardvanillatopicmodels(e.g.,LDA)assumetopics
|                 |     |       |        |                  |       | whicharelessinterpretablewithoutextraknowledge. |     |     |     |     |     | For |
| --------------- | --- | ----- | ------ | ---------------- | ----- | ----------------------------------------------- | --- | --- | --- | --- | --- | --- |
| are independent | and | there | are no | structures among | them. |                                                 |     |     |     |     |     |     |
example,weshowfourexampletopicsofourexperiments
Thislimitsthosemodels’abilitytoexploreanyhierarchical
|                     |     |                                    |     |     |     | inTable1,wherewecansee: |     |     |     | Topic1iscomposedofthe |     |     |
| ------------------- | --- | ---------------------------------- | --- | --- | --- | ----------------------- | --- | --- | --- | --------------------- | --- | --- |
| thematicstructures. |     | Therefore,itisinterestingtodevelop |     |     |     |                         |     |     |     |                       |     |     |
wordsfromboththe“scientificpublication”and“biology”
| a model | that is capable | of  | exploring | topic structures | and |     |     |     |     |     |     |     |
| ------- | --------------- | --- | --------- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
aspects;Topic2isamixtureof“sports”and“music”;Topics
yieldsnotonlyimprovedmodelingaccuracybutalsobetter
3and4areveryspecifictopicsabout“singer”and“video
1FacultyofInformationTechnology,MonashUniversity,Aus- game”respectively.Wehumansareabletounderstandthose
tralia2McCombsSchoolofBusiness,UniversityofTexasatAustin. localtopicsintheabovewaybecauseweareequippedwith
Correspondenceto:LanDu<lan.du@monash.edu>,Mingyuan the global semantics of the words, making us go beyond
Zhou<mingyuan.zhou@mccombs.utexas.edu>. the local context of the target corpus. Therefore, we are
|             | 35th   |               |     |            |            | motivatedtoproposeamodelwhichisabletoautomatically |     |     |     |     |     |     |
| ----------- | ------ | ------------- | --- | ---------- | ---------- | -------------------------------------------------- | --- | --- | --- | --- | --- | --- |
| Proceedings | of the | International |     | Conference | on Machine |                                                    |     |     |     |     |     |     |
analyzethefine-grainedthematicstructuresoflocaltopics,
Learning,Stockholm,Sweden,PMLR80,2018.Copyright2018
furtherimprovingtheinterpretabilityoftopicmodeling.
bytheauthor(s).

WEDTM
Fortunately,wordembeddingssuchasGloVe(Pennington tively. PoissonFactorAnalysis(PFA)(Zhouetal.,2012)
et al., 2014), word2vec (Mikolov et al., 2013), and Fast- isanonnegativematrixfactorizationmodelwithPoisson
Text(Bojanowskietal.,2017)canbeusedasanaccessible link,whichisapopularalternativetoLDA,fortopicmodel-
source of global semantic information for topic models. ing. ThedetailsofthecloserelationshipsbetweenPFAand
Learnedfromlargecorpora,wordembeddingsencodethe LDAcanbefoundinZhou(2018). Thereareseveraldeep
semanticsofwordswiththeirlocationsinaspace,where extensionstoPFAfordocuments,suchasDPFA(Ganetal.,
morerelatedwordsareclosertoeachother. Forexamplein 2015),DPFM(Henaoetal.,2015),andGBN(Zhouetal.,
Topic1,accordingtothedistancesofwordembeddings,the 2016). Amongthem,GBNfactorizesthefactorscorema-
words“biology, cell, psychology, bioinformatics”should trix(topicweightsofdocuments)inPFAwithnonnegative
be in one cluster and “journal, science, research, interna- gamma-distributedhiddenunitsconnectedbytheweights
tional,scientific”shouldbeintheother.Therefore,ifatopic drawnfromtheDirichletdistribution. Fromamodelingper-
modelcanleveragetheinformationinwordembeddings,it spective,GBNisrelatedtoPAM,whileGBNassumesthere
maydiscoverthefine-grainedthematicstructuresoflocal isacorpus-leveltopichierarchysharedbyallthedocuments.
topics. Furthermore,ithasbeendemonstratedthatconven- AsreportedbyCongetal.(2017),GBNoutperformsother
tionaltopicmodelssufferfromdatasparsity, resultingin hierarchical models including nHDP, DPFA, and DPFM.
alargeperformancedegradationonsomeshorterinternet- Despitehavingtheattractiveproperties,thesedeepmodels
generateddocumentsliketweets,productreviews,andnews barelyconsiderintratopicstructuresorthesparsityissue
headlines (Zuo et al., 2016; Zhao et al., 2017c). In this associatedwithinternet-generatedcorpora.
case, wordembeddingscanalsoserveascomplementary
Wordembeddingtopicmodels: Recently,thereisagrow-
informationtoalleviatethesparsityissueintopicmodels.
inginterestinapplyingwordembeddingstotopicmodels,
In this paper, we propose a novel deep structured especiallyforsparsedata.Forexample,WF-LDA(Petterson
topic model, named the Word Embeddings Deep Topic etal.,2010)extendsLDAtomodelwordfeatureswiththe
Model,WEDTM1,whichimprovestheinterpretabilityof logistic-normaltransform,wherewordembeddingsareused
topic models by discovering topic hierarchies (i.e., inter aswordfeaturesinZhaoetal.(2017b). LF-LDA(Nguyen
topicstructure)andfine-grainedinterpretationsoflocaltop- etal.,2015)integrateswordembeddingsintoLDAbyre-
ics(i.e., intratopicstructure). Specifically, theproposed placing the topic-word Dirichlet multinomial component
modeladaptsamulti-layerGammaBeliefNetworkwhich withamixtureofaDirichletmultinomialcomponentand
generates deep representations of topics as well as docu- awordembeddingcomponent. Duetothenon-conjugacy
ments. Moreover, WEDTM is able to split a local topic inWF-LDAandLF-LDA,partoftheinferencehastobe
into a set of sub-topics, each of which captures one fine- donebyMAPoptimization. Insteadofgeneratingtokens,
grained thematic aspect of the local topic, in a way that GaussianLDA(GLDA)(Dasetal.,2015)directlygener-
eachsub-topicisinformedbywordembeddings. WEDTM ateswordembeddingswiththeGaussiandistribution. The
has the following key properties: (1) Better interpretabil- modelproposedinXunetal.(2017)furtherextendsGLDA
itywithtopichierarchiesandsub-topicsinformedbyword by modeling topic correlations. MetaLDA (Zhao et al.,
embeddings. (2)Thestate-of-the-artperplexity,document 2017c;2018a)isaconjugatetopicmodelthatincorporates
classification,andtopiccoherenceperformance,especially both document and word meta information. However, in
forsparsetextdata. (3)AstraightforwardGibbssampling MetaLDA,wordembeddingshavetobebinarized,which
algorithm facilitated by fully local conjugacy under data canloseusefulinformation. WEI-FTM(Zhaoetal.,2017b)
augmentation. isafocusedtopicmodelwhereatopicfocusesonasubsetof
words,informedbywordembeddings. Toourknowledge,
topichierarchiesandsub-topicsarenotconsideredinmost
2.RelatedWork
oftheexistingwordembeddingmodels.
Deep/hierarchicaltopicmodels: Severalapproacheshave
been developed to learn hierarchical representations of 3.TheProposedModel
documents and topics. The Pachinko Allocation model
(PAM)(Li&McCallum,2006)assumesthetopicstructure Based on the PFA framework, WEDTM is a hierarchical
is modeled by a directed acyclic graph (DAG), which is model with two major components: one for discovering
documentspecific. nCRP(Bleietal.,2010)modelstopic the inter topic hierarchies and the other for discovering
hierarchiesbyintroducingatreestructurepriorconstructed intra topic structures (i.e., sub-topics) informed by word
withmultipleCRPs. Paisleyetal.(2015);Kimetal.(2012); embeddings. The two components are connected by the
Ahmedetal.(2013)furtherextendnCRPbyeithersoftening bottom-layertopics,detailedasfollows. Assumethateach
itsconstraintsorapplyingittodifferentproblemsrespec- documentj ispresentedasawordcountvectorx(1) ∈NV,
j 0
where V is the size of the vocabulary; the pre-trained L
1https://github.com/ethanhezhao/WEDTM

WEDTM
dimensional real-valued embeddings for each word v ∈ representationofdocumentj andφ(2) ∈RK1 modelsthe
{1,··· ,V}arestoredinaL-dimensionalvectorf ∈RL. correlationsbetweentopick andal k l 2 thefirs + t-layertopics.
v 2
NowweconsiderWEDTMwithT hiddenlayers,wherethe Notethatstrictlyspeaking,k isnota“real”topicasitis
2
t-thlayeriswithK topicsandk istheindexofeachtopic. notadistributionoverwords. Butitcanbeinterpretedwith
t t
Inthebottomlayer(t=1),thereareK 1 (local)topics,each wordsbyΦ(1)φ(2). Byrepeatingthisconstruction,weare
ofwhichisassociatedwithS sub-topics. Toassistclarity, abletobuildade k e 2 pstructuretodiscovertopichierarchies.
wesplitthegenerativeprocessofthemodelintothreeparts,
Now we explain how sub-topics are discovered for the
shownasfollows:
bottom-layertopicswiththehelpofwordembeddings.First
 (cid:104) (cid:105)
 θ j (1) ∼Gam Φ(2)θ j (2),p( j 2)/(1−p( j 2)) , o
p
f
ar
a
a
l
m
l,
e
W
ter
E
s
D
β
TM
∈
ap
R
p
V
lie
f
s
or
in
e
d
a
i
c
v
h
id
b
u
o
a
t
l
to
a
m
sy
-
m
la
m
ye
e
r
tr
(
i
l
c
oc
D
al
i
)
ri
t
c
o
h
p
le
ic
t
Generating φ(1) ∼Dir(β ), k1 +
documents x( k 1 1 ) ∼Pois (cid:16) Φ k1 (1)θ(1) (cid:17) , φ( k 1 1 ). Wefurtherconstructβ vk1 = (cid:80)S s β v < k s 1 >,whereβ v < k s 1 >
j j modelshowstronglywordvisassociatedwithsub-topics
  θ
··
j (
·
T) ∼Gam
(cid:16)
(cid:16) r,1/c( j T+1) (cid:17) ,
(cid:17)
i d
is
n im
g
lo
a
e c
m
n a s
m
l io t
a
o n p
d
a i l
i
c
s
s
t
u k
ri
b 1
b
. -
u
t F o
te
o p
d
r i
,
c e
i
e a
ts
m ch
s
b
c
e s
a
u d
le
b d - i
p
n to
a
g
r
p :
a
i
m
w cs
e k
<
t
,
1 e
s w >
r
e
is
∈ in
c
R
o
tr
n
L o
s
d .
tr
u A
u
c s
c
e
t
β
e
a
v d
< n
k
s
b 1
L >
y
-
Inter θ(t) ∼Gam Φ(t+1)θ(t+1),1/c(t+1) (t<T), thedotproductoftheembeddingsofsub-topicsandword
structure j j j

φ
··
(
k
·
t
t
) ∼Dir(η
0
1)(t>1),
T
v
h
th
e
r
b
o
a
u
s
g
i
h
ci
t
d
h
e
e
a
e
o
x
f
po
o
n
u
e
r
n
m
ti
o
a
d
l
e
fu
l
n
is
ct
s
i
u
o
m
n.
marizedasfollows:

w<s> ∼N [0,diag(1/σ<s>)],
Intra
α
k
<
k
1
1
s> ∼Gam(
(cid:16)
α
0
<s>/S,1/c<
0
s>
(cid:17)
),
1. I
la
n
y
t
e
e
r
r
)
m
t
s
op
o
i
f
c
s
i
u
s
b
a
-
s
to
so
p
c
ic
i
s
a
,
te
w
d
e
w
a
i
s
t
s
h
um
se
e
ve
e
r
a
a
c
l
h
su
(l
b
o
-
c
t
a
o
l
p
,
i
b
c
o
s,
tt
i
o
n
m
a
-
structure β β v < k s 1 >
:=
∼
(cid:80)
Ga
S
m
β<
α
s>
k < 1
,
s>,ef v (cid:62)w k < 1 s> , w
lo
a
c
y
al
t
t
h
o
a
p
t
ic
th
v
e
ia
su
a
b
s
-
u
t
m
op
m
ic
o
s
d
c
e
o
l
n
(Z
tr
h
ib
o
u
u
t
,
e
2
t
0
o
16
th
).
e
T
p
h
r
e
io
re
r
f
o
o
f
re
t
,
h
i
e
f
vk1 s vk1 aworddominatesinoneormoresub-topics,itislikely
thatthewordwillstilldominateinthelocaltopic.With
where(t)istheindexofthelayerthatavariablebelongsto
thisconstruction,asub-topicisexpectedtocaptureone
and<s>istheindexofsub-topics. Tocompletethemodel,
fine-grainedthematicaspectofthelocaltopicandeach
weimposethefollowingpriorsonthelatentvariables:
sub-topic can be directly interpreted with words via
β<s> ∈RV.
r
kT
∼Gam(γ
0
/K
T
,1/c
0
), k1 +
γ ∼Gam(a ,1/b ),p(t) ∼Beta(a ,b ), 2. Toleveragewordembeddingstoinformthelearning
0 0 0 j 0 0
ofsub-topics,weintroducethesub-topicembedding
c( j t) ∼Gam(e 0 ,1/f 0 ),α 0 <s> ∼Gam(e 0 ,1/f 0 ), foreachofthem,w<s>,whichdirectlyinteractswith
c< 0 s> ∼Gam(e 0 ,1/f 0 ),σ l <s> ∼Gam(a 0 ,1/b 0 ). the word embeddin k g 1 s. Therefore, sub-topic embed-
dings are learned with both the local context of the
Wefirsttakealookatthebottomlayerofthemodel,i.e.,
targetcorpusandtheglobalinformationofwordem-
theprocessofgeneratingthedocuments,whichfollowsa
beddings. According to our model construction, the
PFA framework. In this part, WEDTM models the word
probabilitydensityfunctionofβ istheconvolution
countsx(
j
1)inadocumentbyaPoisson(Pois)distribution
ofScovariance-dependentgamm
v
a
k1
distributions(Zhou,
andfactorizesthePoissonparametersintoaproductofthe 2016). Therefore,ifthesub-topicembeddingsofsand
factorloadingsΦ(1) ∈RV×K1 andhiddenunitsθ(1). θ(1) word embeddings of v are close, the dot product of
+ j j
isthefirst-layerlatentrepresentation(unnormalizedtopic themwillbelarge,givingalargeexpectationofβ<s>.
vk1
weights) of document j, each element of which is drawn Thelargeexpectationmeansthatvhasalargeweight
Φ f f r r o o (1 m m ), a a φ g ( k D 1 1 a ) i m r ∈ i m ch R a le V + ( t G i ( s a D m th ir ) e ) d w d i i s o s t r t r d r i i b d b u i u t s t i t i o r o i n b n 2 u . . ti T W on h e e o t f k h t 1 e o - n p th i e c c x k o p 1 l l u , a m d in r n a t w h o n e f i t lo n o c s t a h u l e b t - o l t o p o c i p c a i . l c t s op o i f c’ k s . p F r i i n o a r ll β y v , k β 1 v < , k i s 1 n > fo f r u m rt i h n e g r φ co ( v 1 n k ) 1 tri o b f u t t h e e s
componentfordiscoveringintertopichierarchies,whichis
similartothestructureofGBN(Zhouetal.,2016). Specif- 3. It is also noteworthy the special case of WEDTM,
ically, the shape parameter of θ(1) is factorized into θ(2) where S = 1, meaning that there are no sub-topics
j j
andeachlocaltopick isassociatedwithonetopicem-
andΦ(2) ∈RK1×K2,whereθ(2)isthesecond-layerlatent 1
+ j beddingvectorw . Consequently,inWEDTM,there
k1
2Thefirstandsecondparametersofthegammadistributionare arethreelatentvariablescapturingtheweightsbetween
theshapeandscalerespectively. thewordsandlocaltopick 1 : eF(cid:62)wk1 (F ∈ RL×V is

WEDTM
theembeddingsofallthewords),β ,andφ(1),each Sample α<s>. We first sample g<s> ∼
ofwhichisavectoroverwords. Itis k i 1 nterestin k g 1 toana- CRT (cid:0) h<s>, k α<s>(cid:1) ,then: vk1
lyzetheconnectionsanddifferencesofthem. eF(cid:62)wk1
vk1 k1
i e th s F e t (cid:62) h g w e lo k p 1 b r a i i o l s r s t e h o m e f a c β n lo k t 1 i s c e , s i w t n h f o o n il r e e m t β a o t k i t 1 o h n e is , w w t o h h r e i d l p e e r m φ io ( b r 1 e ) o d f i d s φ i t n h ( k g 1 e 1 s ) , c . i l S . o e s o . - , α k < 1 s> ∼ c< 0 s G > a + m( lo α g 0 < (cid:16) s> 1 / + S e + π v < g k s 1 · < > k s 1 l > og ,1 q ) k 1 1 (cid:17) . (3)
k1
est one to the data, i.e., the local document context Itisnoteworthythatthehierarchicalconstructiononα<s>is
of the target corpus. Therefore, unlike conventional
k1
closelyrelatedtothegamma-negativebinomialprocessand
topic models with φ(1) only, the three variables of canbeconsideredasa(truncated)gammaprocess(Zhou&
k1
WEDTMgivethreedifferentviewstothesametopic, Carin,2015;Zhou,2016)withanintrinsicshrinkagemech-
from global to local, respectively. We qualitatively anismonS. Itmeansthatthemodelisabletoautomatically
showthisinterestingcomparisoninSection5.4. learnthenumberofeffectivesub-topics.
4. Thelastbutnotleast,wordembeddingsinWEDTM Samplew<s>.
k1
can be viewed to serve as the prior/complementary
w<s> ∼N(µ<s>,Σ<s>),
informationtoassistthelearningofthewholemodel, k1 k1 k1
whichisimportantespeciallyforsparsedata. µ<s> =
k1
4.Inference Σ< k1 s> (cid:34) (cid:88) V
v
(cid:32) h< vk s 1 >− 2 α k < 1 s> −ω v < k s 1 >loglog q 1 k1 (cid:33) f v (cid:35) ,
Unlikemanyotherwordembeddingstopicmodels,thefully (cid:34) V (cid:35)−1
(cid:88)
localconjugacyofWEDTMfacilitatesthederivationofan Σ<s> = diag(1/σ<s>)+ ω<s>f (f )(cid:62) ,(4)
k1 vk1 v v
effective Gibbs sampling algorithm. As the sampling for v
thelatentvariablesintheprocessofgeneratingdocuments
(cid:16) (cid:17)
andmodelingintertopicstructurearesimilartoGBN,the where ω<s> ∼ PG h<s>+α<s>,π<s>+loglog 1
detailscanbefoundinZhouetal.(2016). Herewefocus andPGd
v
e
k
n
1
otesthePo´ly
v
a
k1
gamma
k1
distrib
v
u
k
t
1
ion(Polsone
q
t
k1
al.,
onthesamplingofthelatentvariablesformodelingintra 2013). TosamplefromPG,weuseanaccurateandefficient
topicstructure. approximatesamplerinZhou(2016).
AssumethatsampledbyEq.(28)inAppendixBofZhou Omittedderivations,details,andtheoverallalgorithmare
etal.(2016),thelatentcountforthebottom-layerlocaltop- inthesupplementarymaterials.
icsarex(1) ,whichcountshowmanywordsvindocument
vjk1
j areallocatedwithlocaltopick .
1 5.Experiments
Sampleβ<s>. Wefirstsample: WeevaluatetheproposedWEDTMbycomparingitwith
vk1 several recent advances including deep topic models and
(cid:32) (cid:33) wordembeddingtopicmodels. Theexperimentswerecon-
β<1> β<S>
(cid:0) h<1>,··· ,h<S>(cid:1) ∼Mult h , vk1 ,··· , vk1 , ductedonfourreal-worlddatasetsincludingbothregular
vk1 vk1 vk1 β vk1 β vk1 andsparsetexts. Wereportperplexity,documentclassifica-
(1) tionaccuracy,andtopiccoherencescores. Wealsoqualita-
tivelyanalyzethetopichierarchiesandsub-topics.
(cid:16) (cid:17)
where h ∼ CRT x(1) ,β (Zhou & Carin, 2015;
vk1 v·k1 vk1
5.1.ExperimentalSettings
Zhaoetal.,2017a),andx(1) := (cid:80) x(1) 3. Then:
v·k1 j vjk1
Intheexperiments,weusedaregulartextdataset(20NG)
Gam(α<s>+h<s>,1) andthreesparsetextdatasets(WS,TMN,Twitter),thede-
β<s> ∼ k1 vk1 , (2) tailsofwhichareasfollows: 1. 20NG,20Newsgroup,con-
vk1 e−π v < k s 1 > +log qk 1
1
sistsof18,774articleswith20categories. FollowingZhou
etal.(2016), weusedthe2000mostfrequenttermsafter
whereq ∼Beta(β ,x(1) )(Zhaoetal.,2018b)andwe removingstopwords. Theaveragedocumentlengthis76.
k1 ·k1 ··k1
2. WS, Web Snippets, contains 12,237 web search snip-
defineπ<s> :=f(cid:62)w<s>.
vk1 v k1 petswith8categories,usedbyLietal.(2016);Zhaoetal.
3Wehereafteruse·ofadimensiontodenotethesumoverthat (2017c;b). Thevocabularycontains10,052tokensandthere
dimension. are15wordsinonesnippetonaverage. 3. TMN,TagMy

WEDTM
|     |       |     |     |        |     | (c)Twitter |     |     |     | (d)20NG |     |     |
| --- | ----- | --- | --- | ------ | --- | ---------- | --- | --- | --- | ------- | --- | --- |
|     | (a)WS |     |     | (b)TMN |     |            |     |     |     |         |     |     |
| 50  |       |     | 50  |        | 10  |            |     |     | 20  |         |     |     |
0
| 0   |     |     | 0   |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
10
|     |     |     | -50 |     | -10 |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
-50
|     |     |     | -100 |     | -20 |     |     |     | 0   |     |     |     |
| --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
-100
-30
-150
| W       | E D T M - 1 G B N - | 1 M e t | a LD A  |     |        |     |     |     | -10     |     |     |     |
| ------- | ------------------- | ------- | ------- | --- | ------ | --- | --- | --- | ------- | --- | --- | --- |
| -150    |                     |         | -200    |     | -40    |     |     |     |         |     |     |     |
| W       | E D T M - 2 G B N - | 2 W E   | I -F TM |     |        |     |     |     |         |     |     |     |
| WEDTM-3 | GBN-3               |         |         |     |        |     |     |     |         |     |     |     |
| -200    |                     |         | -250    |     | -50    |     |     |     | -20     |     |     |     |
| 50      | 100                 |         | 200 50  | 100 | 200 50 |     | 100 |     | 200 100 |     | 200 | 400 |
GBN-1:704,595,548 GBN-1:1498,1299,1190 GBN-1:461,349,305 GBN-1:631,522,479
|      | (e)WS |     |      | (f)TMN |     | (g)Twitter |     |     |     | (h)20NG |     |     |
| ---- | ----- | --- | ---- | ------ | --- | ---------- | --- | --- | --- | ------- | --- | --- |
| 100  |       |     | 200  |        | 50  |            |     |     | 5   |         |     |     |
| 0    |       |     |      |        |     |            |     |     | 0   |         |     |     |
|      |       |     | 0    |        | 0   |            |     |     |     |         |     |     |
| -100 |       |     |      |        |     |            |     |     | -5  |         |     |     |
| -200 |       |     | -200 |        |     |            |     |     |     |         |     |     |
|      |       |     |      |        | -50 |            |     |     | -10 |         |     |     |
-300
-400
-15
| -400 | WEDTM-1 GBN-1 |     | MetaLDA |     | -100 |     |     |     |     |     |     |     |
| ---- | ------------- | --- | ------- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
|      |               |     | -600    |     |      |     |     |     | -20 |     |     |     |
| -500 | WEDTM-2 GBN-2 |     | WEI-FTM |     |      |     |     |     |     |     |     |     |
|      | WEDTM-3 GBN-3 |     |         |     |      |     |     |     |     |     |     |     |
| -600 |               |     | -800    |     | -150 |     |     |     | -25 |     |     |     |
20% 40% 60% 80% 20% 40% 60% 80% 20% 40% 60% 80% 20% 40% 60% 80%
GBN-1:1786,994,728,595 GBN-1:3140,1925,1495,1299 GBN-1:699,446,382,349 GBN-1:704,595,549,522
Figure1.(a)-(d):Relativeper-heldout-wordperplexity6(thelowerthebetter)withthevariedK 1 andfixedproportion(80%)oftraining
wordsofeachdocument.(e)-(h):Relativeper-heldout-wordperplexity6withthevariedproportionoftrainingwordsofeachdocument
andfixedK (100onWS,TMN,andTwitter;200for20NG).Theerrorbarsindicatethestandarddeviationsof5randomtrials.The
1
numberattachedtoWEDTMandGBNindicatesthenumberoflayers(i.e.,T)used.
News,consistsof32,597RSSnewssnippetsfromTagMy 2016). Therefore,weconsideredthethreeabovecompeti-
| Newswith7categories,usedbyNguyenetal.(2015);Zhao |                                       |     |     |     | torstoWEDTM. |     |         |       |     |          |      |          |
| ------------------------------------------------ | ------------------------------------- | --- | --- | --- | ------------ | --- | ------- | ----- | --- | -------- | ---- | -------- |
| etal.(2017c;b).                                  | Eachsnippetcontainsatitleandashortde- |     |     |     |              |     |         |       |     |          |      |          |
|                                                  |                                       |     |     |     | Originally   |     | MetaLDA | (when | no  | document | meta | informa- |
scription. Thereare13,370tokensinthevocabularyandthe
|                              |     |     |                         |     | tion                                       | is provided) |     | and WEI-FTM |     | follow | the LDA | frame- |
| ---------------------------- | --- | --- | ----------------------- | --- | ------------------------------------------ | ------------ | --- | ----------- | --- | ------ | ------- | ------ |
| averagelengthofasnippetis18. |     |     | 4. Twitter,wasextracted |     |                                            |              |     |             |     |        |         |        |
|                              |     |     |                         |     | work,wherethetopicdistributionfordocumentj |              |     |             |     |        |         | isθ ∼  |
j
in2011and2012microblogtracksatTextREtrievalCon-
|     |     |     |     |     | Dir(α | 0 1) | and α 0 | is a hyperparameter |     | (usuallyset |     | to 0.1). |
| --- | --- | --- | --- | --- | ----- | ---- | ------- | ------------------- | --- | ----------- | --- | -------- |
ference(TREC)4andpreprocessedinYin&Wang(2014).
|                           |     |     |                          |     | For | a fair    | comparison, |     | we replaced    |     | this part | with the |
| ------------------------- | --- | --- | ------------------------ | --- | --- | --------- | ----------- | --- | -------------- | --- | --------- | -------- |
| Ithas11,109tweetsintotal. |     |     | Thevocabularysizeis6,344 |     |     |           |             |     |                |     |           |          |
|                           |     |     |                          |     | PFA | framework | with        | the | gamma-negative |     | binomial  | pro-     |
andatweetcontains21wordsonaverage.
|     |     |     |     |     | cess | (Zhou | & Carin, | 2015), | which | is equivalent |     | to GBN |
| --- | --- | --- | --- | --- | ---- | ----- | -------- | ------ | ----- | ------------- | --- | ------ |
WecomparedWEDTMwith: 1. GBN(Zhouetal.,2016), whenT =1andcloselyrelatedtothehierarchicalDirichlet
thestate-of-the-artdeeptopicmodel. 2. MetaLDA(Zhao ProcessLDA(HDPLDA)(Tehetal.,2012).
etal.,2017c;2018a),thestate-of-the-arttopicmodelwith
|     |     |     |     |     | For | all the | models, | we used | 50-dimensional |     | GloVe | word |
| --- | --- | --- | --- | --- | --- | ------- | ------- | ------- | -------------- | --- | ----- | ---- |
binarymetainformationaboutdocumentand/orword.Word
Wikipedia5.
|     |     |     |     |     | embeddings |     | pre-trained |     | on  |     | Except | for Met- |
| --- | --- | --- | --- | --- | ---------- | --- | ----------- | --- | --- | --- | ------ | -------- |
embeddingsneedtobebinarizedbeforeusedinthemodel.3.
aLDA,wherewefollowedthepapertobinarisetheword
WEI-FTM(Zhaoetal.,2017b),thestate-of-the-artfocused
embeddings,theotherthreemodelsusedtheoriginalreal-
topicmodelthatincorporatesreal-valuedwordembeddings.
|     |     |     |     |     | valuedembeddings. |     |     | Thehyperparametersettingsweused |     |     |     |     |
| --- | --- | --- | --- | --- | ----------------- | --- | --- | ------------------------------- | --- | --- | --- | --- |
ItisnoteworthythatGBNwasreported(Congetal.,2017) for WEDTM and GBN are a = b = 0.01,e = f =
|     |     |     |     |     |     |     |     |     | 0   | 0   |     | 0 0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
to have better performance than other deep (hierarchi- 1.0,η 0 =0.05. ForMetaLDAandWEI-FTM,wecollected
cal) topic models such as nHDP (Paisley et al., 2015), 1000 MCMC samples after 1000 burnins; for GBN and
DPFA(Ganetal.,2015),andDPFM(Henaoetal.,2015). WEDTM,wecollected1000forT =1and500forT >1
MetaLDAandWEI-FTMwerereportedtoperformbetter MCMCsamplesafter1000forT = 1and500forT > 1
than other word embedding topic models including WF- burnins,toestimatetheposteriormean. Duetotheshrink-
LDA(Pettersonetal.,2010)andGPUDMM(Lietal.,2016) ageeffectofWEDTMonS,discussedinSection4,weset
as well as short text topic models like PTM (Zuo et al., S =5whichislargeenoughforallthetopics.
4http://trec.nist.gov/data/microblog.html 5https://nlp.stanford.edu/projects/glove/

WEDTM
(c)20NG
|     |     |         | (a)WS |         |     | (b)TMN |     |     |     |     |     |
| --- | --- | ------- | ----- | ------- | --- | ------ | --- | --- | --- | --- | --- |
|     | 20  |         |       |         | 10  |        |     | 5   |     |     |     |
|     |     | WEDTM-1 | GBN-1 | MetaLDA |     |        |     |     |     |     |     |
|     |     | WEDTM-2 | GBN-2 | WEI-FTM | 8   |        |     | 4   |     |     |     |
15
|     |     | WEDTM-3 | GBN-3 |     | 6   |     |     | 3   |     |     |     |
| --- | --- | ------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
10
|     |     |     |     |     | 4   |     |     | 2   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     | 2   |     |     | 1   |     |     |     |
5
|     |     |     |     |     | 0   |     |     | 0   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0
|     |     |     |     |     | -2      |     |     | -1     |     |     |     |
| --- | --- | --- | --- | --- | ------- | --- | --- | ------ | --- | --- | --- |
|     | -5  |     |     |     | -4      |     |     | -2     |     |     |     |
|     | 20% | 40% |     | 60% | 80% 20% | 40% | 60% | 80%20% | 40% | 60% | 80% |
GBN-1:66.6,80.9,83.1,82.2 GBN-1:72.0,77.9,78.8,79.4 GBN-1:64.5,68.3,69.6,69.9
Figure2.Relativedocumentclassificationaccuracy6(%)onWS,TMN,and20NGwiththevariedproportionoftrainingwordsofeach
trainingdocument.TheresultswithK =100onWSandTMN,K =200on20NGarereported.
|     |       |          |         | 1          |         |        | 1   |         |            |     |     |
| --- | ----- | -------- | ------- | ---------- | ------- | ------ | --- | ------- | ---------- | --- | --- |
|     |       |          | (a)WS   |            |         | (b)TMN |     |         | (c)Twitter |     |     |
|     | 0.08  |          |         |            | 0.1     |        |     | 0.1     |            |     |     |
|     | 0.06  |          |         |            | 0.08    |        |     | 0.08    |            |     |     |
|     | 0.04  |          |         |            | 0.06    |        |     | 0.06    |            |     |     |
|     | 0.02  |          |         |            | 0.04    |        |     | 0.04    |            |     |     |
|     |       | 0        |         |            | 0.02    |        |     | 0.02    |            |     |     |
|     | -0.02 |          |         |            | 0       |        |     |         | 0          |     |     |
|     | -0.04 | WEDTM    | GBN     | WEI-FTM    | -0.02   |        |     | -0.02   |            |     |     |
|     |       | WEDTM-te | MetaLDA | WEI-FTM-te |         |        |     |         |            |     |     |
|     | -0.06 |          |         |            | -0.04   |        |     | -0.04   |            |     |     |
|     | 20%   |          | 40%     | 60%        | 80% 20% | 40%    | 60% | 80% 20% | 40%        | 60% | 80% |
Figure3.Topiccoherence(NPMI,thehigherthebetter)onWS,TMN,andTwitterwiththevariedproportionoftrainingwordsofeach
document.TheresultswithK 1 =100arereported.ForWEDTMandWEI-FTM,thetopwordsofatopicaregeneratedbyrankingthe
worddistributionandthedotproductoftopicandwordembeddings(denoted“-te”).
5.2.Perplexity dings as well, the proposed WEDTM outperforms them
|     |     |     |     |     |     |     | significantly. | PerhapsthewaythatWEDTMincorporates |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------------- | ---------------------------------- | --- | --- | --- |
Perplexityisameasurethatiswidelyused(Wallachetal.,
wordembeddingsismoreeffective.
2009)toevaluatethemodelingaccuracyoftopicmodels.
Herewerandomlychoseacertainproportionoftheword
5.3.DocumentClassification
tokensineachdocumentastrainingandusedtheremain-
| ingonestocalculateper-heldout-wordperplexity. |     |     |     |     | Figure1 |     |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | ------- | --- | --- | --- | --- | --- | --- |
Weconsiderthemulti-classclassificationtaskforpredict-
showstherelativeperplexity6
resultsofallthemodelson ingthecategoriesfortestdocumentstoevaluatethequality
all the datasets, where we varied the number of bottom- ofthelatentdocumentrepresentation(unnormalizedtopic
layertopicsaswellastheproportionoftrainingwords. The models.7
|     |     |     |     |     |     |     | weights) | extracted | by these |     | In this experiment, |
| --- | --- | --- | --- | --- | --- | --- | -------- | --------- | -------- | --- | ------------------- |
proposed WEDTM performs significantly better than the followingZhouetal.(2016), weranthetopicmodelson
others, especially on sparse data. There are several inter- thetrainingdocumentsandtrainedaL
2 regularizedlogistic
estingremarksoftheresults: (1)Theperplexityadvantage regressionusingtheLIBLINEARpackage(Fanetal.,2008)
ofWEDTMoverGBNbecomesobviouswhenthecorpus withthelatentrepresentationθ(1)
|                                                 |     |     |     |     |     |     |     |     |     |     | asfeatures. Aftertrain- |
| ----------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------------------- |
| becomessparse(e.g.,WS/TMN/TwitterV.S.20NGand20% |     |     |     |     |     |     |     |     |     | j   |                         |
ing,weusedthetrainedtopicmodelstoextractthelatent
V.S.80%trainingwords). Itshowsthatusingwordembed- representationsofthetestdocumentsandthetrainedlogistic
| dings as | the prior | information | benefits | the | model. | (2) In |                                   |     |     |     |                      |
| -------- | --------- | ----------- | -------- | --- | ------ | ------ | --------------------------------- | --- | --- | --- | -------------------- |
|          |           |             |          |     |        |        | regressiontopredictthecategories. |     |     |     | Forallthedatasets,we |
general, increasingthedepthofthemodelleadstobetter randomly selected 80% documents for training and used
| perplexity. | However,whenthedataaretoosparse(e.g. |         |                  |     |       | WS  |                            |     |     |                         |     |
| ----------- | ------------------------------------ | ------- | ---------------- | --- | ----- | --- | -------------------------- | --- | --- | ----------------------- | --- |
|             |                                      |         |                  |     |       |     | theremaining20%fortesting. |     |     | Figure2showstherelative |     |
| with 20%    | training                             | words), | the single-layer |     | WEDTM | and |                            |     |     |                         |     |
documentclassificationaccuracy6resultsforallthemodels.
GBNperformbetterthantheirmulti-layercounterparts. (3) Itcanbeobservedthatwithwordembeddings, WEDTM
AlthoughMetaLDAandWEI-FTMleveragewordembed-
outperformsGBNsignificantly,thebestonTMNand20NG,
|     |     |     |     |     |     |     | andthesecond-bestonWS.Again, |     |     |     | weseeasimilarphe- |
| --- | --- | --- | --- | --- | --- | --- | ---------------------------- | --- | --- | --- | ----------------- |
6WesubtractedthescoreofGBNwithonlyonelayer(GBN-1)
| fromthescoreofeachmodel. |     |     | Thelinesplotthedifferences. |     |     | So  |     |     |     |     |     |
| ------------------------ | --- | --- | --------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
7TheresultsofTwitterarenotreportedbecauseeachdocument
GBN-1isthehorizontallineon“0”.TheabsolutescoreofGBN-1
ofitisassociatedwithmultiplecategories.
isgivenbeloweachfigure.

WEDTM
nomenon: wordembeddingshelpmoreonthesparserdata localinterpretationofWEDTM’stopicsisstillconsiderably
andincreasingthenetworkdepthimprovestheaccuracy. morecoherentthanthoseinGBN.
5.4.TopicCoherence Demonstrationofsub-topics: InFigure4,Weshowthe
sub-topicsdiscoveredbyWEDTMforthetopicsusedasex-
Topiccoherenceisanotherpopularevaluationoftopicmod-
|          |     |                 |         |           |     |          | amplesatthebeginningofthepaper(Table1). |     |     |     | Itcanbeob- |
| -------- | --- | --------------- | ------- | --------- | --- | -------- | --------------------------------------- | --- | --- | --- | ---------- |
| els (Zuo | et  | al., 2016; Zhao | et al., | 2017b;b). | It  | measures |                                         |     |     |     |            |
servedthattheintratopicstructureswithsub-topicsclearly
thesemanticcoherenceinthemostsignificantwords(top
|                 |     |                                  |     |     |     |     | help to | explain the | local topics. | For example, | WEDTM |
| --------------- | --- | -------------------------------- | --- | --- | --- | --- | ------- | ----------- | ------------- | ------------ | ----- |
| words)inatopic. |     | HereweusedtheNormalizedPointwise |     |     |     |     |         |             |               |              |       |
successfullysplitsTopic1intosub-topicsrelatedto“jour-
MutualInformation(NPMI)(Aletras&Stevenson,2013;
nal”and“biology,”andTopic2into“music”and“sports”.
Lauetal.,2014)tocalculatetopiccoherencescoreofthe
Moreover,withthehelpofwordembeddings,WEDTMdis-
top10wordsofeachtopicandreporttheaveragescoreof
allthetopics.8 coversgeneralsub-topicsforspecifictopics. Forexample,
|     |     |     |     |     |     |     | Topic 3 | and 4 are | more interpretable | with | the sub-topics |
| --- | --- | --- | --- | --- | --- | --- | ------- | --------- | ------------------ | ---- | -------------- |
Tocomparewiththeothermodels,inthisexperiment,we of“singer”and“game”respectively. Theexperimentalso
set S = 1 for WEDTM. Recall that in WEDTM, from empiricallydemonstratestheshrinkagemechanismofthe
global to local, there are three ways to interpret a topic. model: formosttopics,theeffectivesub-topicsarelessthan
|     |     |     |     | eF(cid:62)wk1 |     | andφ( 1 ). | themaximumnumberS |     | =5. |     |     |
| --- | --- | --- | --- | ------------- | --- | ---------- | ----------------- | --- | --- | --- | --- |
HereweevaluateNPMIfortwoofthem:
|     |     |     |     |     |     | k 1 |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Figure3showstheNPMIscoresforallthemodelsonWS,
TMN, and Twitter. It is not surprising to see that the top Demonstrationoftopichierarchies: Figure5showsan
words generated by eF(cid:62)wk1 in WEDTM always gain the examplethatjointlydemonstratestheinterandintrastruc-
highest NPMI scores, meaning that the topics are more tures of WEDTM. The tree is a cluster of topics related
coherent. ThisisbecausethetopicembeddingsinWEDTM to“health,”wherethetopichierarchiesarediscoveredby
directlyinteractwithwordembeddings. Moreover, ifwe ranking{Φ(t)} ,theleafnodesarethetopicsinthebottom
t
justcomparethetopicsgeneratedbyφ(1),WEDTMalso layer,andeachbottom-layertopicisassociatedwithaset
k
|       |      |                 |      | 1        |            |      | ofsub-topics. | InWEDTM,theintertopicstructuresarere- |     |     |     |
| ----- | ---- | --------------- | ---- | -------- | ---------- | ---- | ------------- | ------------------------------------- | --- | --- | --- |
| gives | more | coherent topics | than | the ot h | er models. | This |               |                                       |     |     |     |
vealedintheformoftopichierarchieswhiletheintratopic
| demonstrates |     | that the proposed | model | is  | able to | discover |     |     |     |     |     |
| ------------ | --- | ----------------- | ----- | --- | ------- | -------- | --- | --- | --- | --- | --- |
moreinterpretabletopics. structuresarerevealedintheformofsub-topics.Combining
thetwokindsoftopicstructuresinthiswaygivesabetter
5.5.QualitativeAnalysis viewofthetargetcorpus,whichmayfurtherbenefitother
textanalysistasks.
AsoneofthemostappealingpropertiesofWEDTMisits
interpretability,weconductedtheextensivequalitativeeval-
6.Conclusion
uationofthequalityofthetopicsdiscoveredbyWEDTM,
| including | topic | embeddings, | sub-topics, |     | and topic | hierar- |                |     |               |        |              |
| --------- | ----- | ----------- | ----------- | --- | --------- | ------- | -------------- | --- | ------------- | ------ | ------------ |
|           |       |             |             |     |           |         | In this paper, | we  | have proposed | WEDTM, | a deep topic |
chies. Morequalitativeanalysisincludingtopichierarchy model that leverages word embeddings to discover inter
visualizationandsyntheticdocumentgenerationisshown topicstructureswithtopichierarchiesandintratopicstruc-
inthesupplementarymaterials.
|     |     |     |     |     |     |     | tureswithsub-topics. |     | Moreover, | withtheintroductionto |     |
| --- | --- | --- | --- | --- | --- | --- | -------------------- | --- | --------- | --------------------- | --- |
sub-topicembeddings,eachsub-topiccanbeinformedby
|               |     |          |             |     |                |     | the global                                     | information | in word | embeddings, | so as to dis- |
| ------------- | --- | -------- | ----------- | --- | -------------- | --- | ---------------------------------------------- | ----------- | ------- | ----------- | ------------- |
| Demonstration |     | of topic | embeddings: |     | We demonstrate |     |                                                |             |         |             |               |
|               |     |          |             |     |                |     | coverafine-grainedthematicaspectofalocaltopic. |             |         |             | With          |
thatWEDTMdiscoversmorecoherenttopicsbycomparing
topicembeddings,WEDTMprovidesdifferentviewstoa
| withthoseofGBNinTable2. |     |     | HerewesetS |     | =1aswell. |     |     |     |     |     |     |
| ----------------------- | --- | --- | ---------- | --- | --------- | --- | --- | --- | --- | --- | --- |
topic,fromglobaltolocal,whichfurtherimprovestheinter-
Thisdemonstrationfurtherexplainsthenumericalresultsin
|     |     |     |     |     |     |     | pretabilityofthemodel. |     | Asafullyconjugatemodel,thein- |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------------- | --- | ----------------------------- | --- | --- |
Figure3. Itisalsointerestingtocomparethelocalinterpre-
tation(φ(1))andglobalinterpretation(topicembeddings) ferenceofWEDTMcanbedonebyastraightforwardGibbs
|        | k    |                 |     |          |     |           | sampling | algorithm. | Extensive | experiments | have shown |
| ------ | ---- | --------------- | --- | -------- | --- | --------- | -------- | ---------- | --------- | ----------- | ---------- |
| of the | same | topic in WEDTM. | For | example, | in  | the fifth |          |            |           |             |            |
thatWEDTMachievesthestate-of-the-artperformanceon
| set, | the local | interpretation | (5.b) | is about | “networks | and |                                                    |     |     |     |       |
| ---- | --------- | -------------- | ----- | -------- | --------- | --- | -------------------------------------------------- | --- | --- | --- | ----- |
|      |           |                |       |          |           |     | perplexity,documentclassification,andtopicquality. |     |     |     | Inad- |
security,”whiletheglobalinterpretation(5.c)generalizesit
dition,withtopichierarchies,sub-topics,andtopicembed-
| withmoregeneralwordsrelatedto“communications.” |     |     |     |     |     | We  |     |     |     |     |     |
| ---------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
dings,themodelcandiscovermoreinterpretablestructured
| can | also observe | that although | the | local | interpretation | of  |     |     |     |     |     |
| --- | ------------ | ------------- | --- | ----- | -------------- | --- | --- | --- | --- | --- | --- |
topics,whichhelpstogetbetterunderstandingsoftextdata.
WEDTMisnotasclosetowordembeddingsastheglobal
Giventhelocalconjugacy,itispossibletoderivemorescal-
interpretation,asinformedbytheglobalinterpretation,the
ableinferencealgorithmsforWEDTM,suchasstochastic
8WeusedthePalmettopackagewithalargeWikipediadump variationalinferenceandstochasticgradientMCMC,which
tocomputeNPMI(http://palmetto.aksw.org). isagoodsubjectforfuturework.

WEDTM
Table2.Top10wordsoffivesetsofexampletopicsontheWSdataset.Eachsetcontainsthetopwordsof3topics:topic‘a’isgenerated
byφ(
k
1)inGBN-3;topic‘b’isgeneratedbyφ(
k
1)inWEDTM-3;topic‘c’isgeneratedbyeF(cid:62)wk1 inWEDTM-3.Topic‘a’and‘b’are
matchedbytheHellingerdistanceofφ(1).Topic‘b’and‘c’aredifferentwaysofinterpretingonetopicinWEDTM.
k
Topic Index Top10words NPMI
a enginecarbuyinghomedieselsellingfuelautomobileviolinjet -0.055
1 b enginemotordieselfuelgasolinejetelectricenginesgastechnology 0.202
c enginedieselenginesgasolinesteamelectricfuelpropulsionmotorscombustion 0.224
a partylabordemocraticpoliticalsocialistmovementunionsocialnewsaustralian 0.168
2 b partypoliticalcommunistdemocraticsocialistlaborrepublicanpartiesconservativeleader 0.188
c partydemocraticcommunistlabourliberalsocialistconservativeoppositionelectionsrepublican 0.219
a cancerlungtobaccointelligenceartificialinformationhealthsymptomssmokingtreatment -0.006
3 b cancerlungtobaccoinformationhealthsmokingtreatmentgovresearchsymptoms 0.050
c cancerbreastdiabetespulmonarycancerspatientsasthmacardiovascularcholesterolobesity 0.050
a oscaracademyawardsswimmingawardwinnersswimoscarsnominationspicture 0.020
4 b artawardsoscaracademygallerymuseumsurrealismsculpturepicassoarts 0.076
c paintingsawardsawardartmuseumgallerysculpturepaintingpicassoportrait 0.087
a securitycomputernetworknuclearweaponsnetworkingspamvirusspywarenational 0.059
5 b securitynetworkwirelessaccessnetworksspamspywarenetworkingnationalcomputer 0.061
c wirelessinternetnetworksdevicesphonebroadbandusersnetworkwi-fiproviders 0.143
taylor san
b i i n p o t r s s j i s e e b o n y c j c r s i o u f c i o n c i e o e e h u r e l a n r n o a n o r m l t t n a l g r i c l i o c o fi a a l y e s h n c g l t i a y c l s p e i d n p e r s o j s f e u s o j r c o c o c - o s b u i r r u u i e e m e c e l r m i r n n i a s v n n e a t a h i e r c i a e t t c fi l y e n i e s l w o h c s t n s e d n i n b a n t i n e e o m b r g o u r t e g b i d e o o e t r s e i e o i c o l l n s e e o n c h s l c e o a c h g e c n i t u p g r i n i t i o e c c c i l l y c o l a i a n s h o n l r l c o g a e g y ry y p i m n e t e a h e n zr t ur a o h - n na m r b t o e c e e a u s a la m r j v t r o mm is i a n i o g a e l i n i ys t w s i a t c e l a e d w s e w l t e w r i g p fi v s g a i s m e u i t i w h i a o s n n i i t g m o i t n l e l i m i a i n n h n o f s i r t g n t s s i n g g k e g p s f v g p e t v y t u i i e a r u i o i n b a o i i n t n n i l d o t n i a l o n i a g o e n a o r r s r s s s r r d c s o e w w t n b w g fi i r x n d a o i t o l e m e n o d i i r x t n r i k e v o i g m c i o i o n e s o n i h n s i u g s s r g n t e i t n g g o c v o l e l i g r mt u es l de r r l r e t x b a l ai a n i o g n uc a s ns to g t g a r h y s o d yk s l r e s d w p w w s g b r i j j i l o w i o h a n l o n i v n i a l t i n c t a f e i e m t e r a c s u s c m o b i s s n d n i r n a o n a i o u i g g e g n n c n w s h i n n e e g g d i d t c c g r r t e r p a o d s r g s c m d i a s i n j n o a t o u i n r a n c w g n v e e c e n g e i g s n e t s t r s i r s c d a r e m o g g n c a t c r h g a d o e u a k e t m r b m s t a n e o f i t t e l d a b a e s e r r p n r l a r s o a v e i s e g n e e n r y l e e l i a t a s r d e g e r a s m t s r a i i a n i e n s o o o s e t d e s a i n i n e d o o d l n a c m n a o m n s n a n a t i t s h d v o d d r t u a i u e e r b n l n t c e d c r o f i e u t l s a k e s e a s s s r y
1 2 3 4
Figure4.Thesub-topics(red)oftheexampletopics(blue). Largerfontsizeindicateslargerweight( (cid:80)V β<s>)ofasub-topictothe
v vk
localtopic.WesetS =5andtrimmedoffthesub-topicswithextremesmallweights.
47 health cancer information gov disease
healthy nutrition diet medical hiv
4 health cancer information gov healthy 33 hiv aids system respiratory prevention 21 theoretical edu models hypotheses cgi
nutrition disease diet medical heart epidemic infection hepatitis organism living model reasoning abstract hypothesis framework
1 information
4 c p m a s o e b c b t r s n t a m o t o l o b o i n e c l m p r k c i g b w l c y l e e c s s c v m m c m a i a k d o o i r g fl u n i r e l t l r e e t o o l s i n o a e s n d d o l i i d o t d n m c e n n g e r s wa p s a s w n b s t e b c r h o e t u o o t o l oi o i r w n sc r mp i r gel hl gy d s l e e s t o n re s o s h n p e l c w o n i o e a n o a u l e m w i g k m r n r b c s e c s e e h e s in w f i n o p o b p b e w m t r a n o e a o m b g l o e a r i g o s n n a e k b i e k i l e e s t t s i e o t n g d s d b k u i u ac r e f l h im ou it d m t s y i o a cl o e t m w l a w b - i h n b n t po a a eu- a o g t sr s r xr r o o s d i e ie t e e k s s s s s s a u du n i tm i s s r v h r e e ca i oe l o p r il l a n n t e arx r d u r i g i k i a it a f c c m a a sh n ol t e e i vr d e in 5 n d m f h c o u i h e a s e r h g d t e m a e n r d e i o i e a l a c t i t a a v i c t r h e o s l t t a t y i e r n h o l n i n d n p d m f c i o h u a s i a f c s e r e o e t t m a e n r i d a o e a i r a c t i a l d e n s i c t e o s h t e a t i e r n s o s l n c h n c o v d c o ua i d b a f i tl eh a tl aei e l cr e o t d t i ms i s a t t t u r i l y ts i o r i ei t m e y n yn r o l r p o e e i h r s n s r 3 s e p e p g f y p 6 a v i e p d e a s i e i c r a d e t c n a n e h t t i s m i i e i t t s o m i t o v i i s o m i n s c r n y r p e d i h r d s n h s e i e p s i f p u s a v e p e h e e i m e i c r a d a i c a a v n t t a i s s i e i s t t o t e o n i i e s o n s s r n y dis a c a s h a m m h n s r sn uc c ss l c e i adm t n c oe n w m dl e c b r les 1 2 h h f r r y e y a a m p t m p a b h m o e o o s s c e o t e d o d t t g h o d h r w u n e i a e r e e e i l o c s n s l s t t r e g i i k c s s a l u m n t m a d h e a t t h g e e m t o h n s h e r r o l e t a o s p e e u o r m l t w i e c o y d a r r i u i t r s a t y c n e i y h c l i t a a d s s i a c l r i n l a g l m s s a u t y h t p p h m e h e q p s e j s o m y r u u y t m t s r s s l e l r e e t i a r k m t i t r n i y c g a
Figure5.Oneexamplesub-treeofthetopichierarchydiscoveredbyWEDTMontheWSdatasetwithK = 50andS = 5. The
1
tree is generated in the same way to Zhou et al. (2016). A line from node k at layer t to node k at layer t−1 indicates that
t t−1
φ(t) >1.5/K anditswidthindicatesthevalueofφ(t) (i.e.topiccorrelationstrength).Theoutsideborderofthetextboxis
kt−1kt t−1 kt−1kt
coloredasorange,blue,orblackifthenodeisatlayerthree,two,orone,respectively.Fortheleafnodes,sub-topicsareshowninthe
samewaytoFigure4.

WEDTM
References Nguyen, D. Q., Billingsley, R., Du, L., and Johnson, M.
Improvingtopicmodelswithlatentfeaturewordrepre-
| Ahmed,A.,Hong,L.,andSmola,A. |     |              |                               | NestedChineserestau- |     |     |                                 |                      |           |                      |     |        |
| ---------------------------- | --- | ------------ | ----------------------------- | -------------------- | --- | --- | ------------------------------- | -------------------- | --------- | -------------------- | --- | ------ |
|                              |     |              |                               |                      |     |     | sentations.                     | TACL,3:299–313,2015. |           |                      |     |        |
| rantfranchiseprocess:        |     |              | Applicationstousertrackingand |                      |     |     |                                 |                      |           |                      |     |        |
| documentmodeling.            |     | InICML,2013. |                               |                      |     |     |                                 |                      |           |                      |     |        |
|                              |     |              |                               |                      |     |     | Paisley,                        | J., Wang, C.,        | Blei, D., | and Jordan,          | M.  | Nested |
|                              |     |              |                               |                      |     |     | hierarchicalDirichletprocesses. |                      |           | TPAMI,37(2):256–270, |     |        |
| Aletras,N.andStevenson,M.    |     |              | Evaluatingtopiccoherence      |                      |     |     |                                 |                      |           |                      |     |        |
2015.
| using | distributional | semantics. |     | In Proc. | of  | the 10th In- |     |     |     |     |     |     |
| ----- | -------------- | ---------- | --- | -------- | --- | ------------ | --- | --- | --- | --- | --- | --- |
ternationalConferenceonComputationalSemantics,pp. Pennington,J.,Socher,R.,andManning,C. GloVe: Global
13–22,2013.
|     |     |     |     |     |     |     | vectorsforwordrepresentation. |     |     | InEMNLP,pp.1532– |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------- | --- | --- | ---------------- | --- | --- |
1543,2014.
| Blei,D.,Griffiths,T.,andJordan,M. |     |     |     | ThenestedChinese |     |     |     |     |     |     |     |     |
| --------------------------------- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
restaurantprocessandBayesiannonparametricinference Petterson,J.,Buntine,W.,Narayanamurthy,S.M.,Caetano,
| oftopichierarchies. |     | JournaloftheACM(JACM),57(2): |     |     |     |     |                    |                           |                                |     |     |     |
| ------------------- | --- | ---------------------------- | --- | --- | --- | --- | ------------------ | ------------------------- | ------------------------------ | --- | --- | --- |
|                     |     |                              |     |     |     |     | T.S.,andSmola,A.J. |                           | WordfeaturesforLatentDirichlet |     |     |     |
| 7,2010.             |     |                              |     |     |     |     | Allocation.        | InNIPS,pp.1921–1929,2010. |                                |     |     |     |
Bojanowski,P.,Grave,E.,Joulin,A.,andMikolov,T. En- Polson, N., Scott, J., and Windle, J. Bayesian inference
richingwordvectorswithsubwordinformation. TACL,5: forlogisticmodelsusingPo´lya–Gammalatentvariables.
135–146,2017.
JournaloftheAmericanStatisticalAssociation,108(504):
1339–1349,2013.
| Cong, Y., | Chen, B., | Liu, | H., and | Zhou, | M.  | Deep latent |     |     |     |     |     |     |
| --------- | --------- | ---- | ------- | ----- | --- | ----------- | --- | --- | --- | --- | --- | --- |
Dirichletallocationwithtopic-layer-adaptivestochastic Teh,Y.W.,Jordan,M.,Beal,M.,andBlei,D. Hierarchical
gradient Riemannian MCMC. In ICML, pp. 864–873, Dirichletprocesses. JournaloftheAmericanStatistical
| 2017. |     |     |     |     |     |     | Association,101(476):1566–1581,2012. |     |     |     |     |     |
| ----- | --- | --- | --- | --- | --- | --- | ------------------------------------ | --- | --- | --- | --- | --- |
Das,R.,Zaheer,M.,andDyer,C. GaussianLDAfortopic Wallach,H.M.,Mimno,D.M.,andMcCallum,A. Rethink-
models with word embeddings. In ACL, pp. 795–804, ingLDA:Whypriorsmatter. InNIPS,pp.1973–1981,
2015.
2009.
Fan,R.-E.,Chang,K.-W.,Hsieh,C.-J.,Wang,X.-R.,and
|     |     |     |     |     |     |     | Xun, G., | Li, Y., Zhao, | W. X., Gao, | J., and | Zhang, | A. A |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------------- | ----------- | ------- | ------ | ---- |
Lin,C.-J. LIBLINEAR:Alibraryforlargelinearclassifi- correlatedtopicmodelusingwordembeddings. InIJCAI,
| cation. | JMLR,9:1871–1874,2008. |     |     |     |     |     | pp.4207–4213,2017. |     |     |     |     |     |
| ------- | ---------------------- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- |
Gan, Z., Chen, C., Henao, R., Carlson, D., and Carin, L. Yin,J.andWang,J.ADirichletmultinomialmixturemodel-
ScalabledeepPoissonfactoranalysisfortopicmodeling. basedapproachforshorttextclustering. InSIGKDD,pp.
| InICML,pp.1823–1832,2015. |     |     |     |     |     |     | 233–242.ACM,2014. |     |     |     |     |     |
| ------------------------- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- |
Henao, R., Gan, Z., Lu, J., and Carin, L. Deep Poisson Zhao, H., Du, L., and Buntine, W. Leveraging node at-
| factormodeling. |     | InNIPS,pp.2800–2808,2015. |     |     |     |     |          |                |            |       |          |     |
| --------------- | --- | ------------------------- | --- | --- | --- | --- | -------- | -------------- | ---------- | ----- | -------- | --- |
|                 |     |                           |     |     |     |     | tributes | for incomplete | relational | data. | In ICML, | pp. |
4072–4081,2017a.
| Kim,J.H.,Kim,D.,Kim,S.,andOh,A. |     |     |     |     | Modelingtopic |     |     |     |     |     |     |     |
| ------------------------------- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- |
hierarchieswiththerecursiveChineserestaurantprocess. Zhao, H., Du, L., and Buntine, W. A word embeddings
InCIKM,pp.783–792.ACM,2012. informedfocusedtopicmodel. InACML,pp.423–438,
2017b.
| Lau,J.H.,Newman,D.,andBaldwin,T. |     |     |     |     | Machinereading |     |     |     |     |     |     |     |
| -------------------------------- | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | --- | --- |
tealeaves: Automaticallyevaluatingtopiccoherenceand Zhao,H.,Du,L.,Buntine,W.,andLiu,G. MetaLDA:A
topicmodelquality. InEACL,pp.530–539,2014. topicmodelthatefficientlyincorporatesmetainformation.
InICDM,pp.635–644,2017c.
| Li, C., Wang, | H., | Zhang, | Z., Sun, | A., | and Ma, | Z. Topic |     |     |     |     |     |     |
| ------------- | --- | ------ | -------- | --- | ------- | -------- | --- | --- | --- | --- | --- | --- |
modelingforshorttextswithauxiliarywordembeddings.
|     |     |     |     |     |     |     | Zhao, H., | Du, L., Buntine, | W., | and Liu, | G. Leveraging |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ---------------- | --- | -------- | ------------- | --- |
InSIGIR,pp.165–174,2016. externalinformationintopicmodelling. Knowledgeand
InformationSystems,pp.1–33,2018a.
| Li, W. | and McCallum, | A.  | Pachinko |     | allocation: | DAG- |     |     |     |     |     |     |
| ------ | ------------- | --- | -------- | --- | ----------- | ---- | --- | --- | --- | --- | --- | --- |
structuredmixturemodelsoftopiccorrelations. InICML, Zhao,H.,Rai,P.,Du,L.,andBuntine,W. Bayesianmulti-
pp.577–584,2006. labellearningwithsparsefeaturesandlabels,andlabel
|          |                |     |       |              |     |            | co-occurrences. | InAISTATS,pp.1943–1951,2018b. |     |     |     |     |
| -------- | -------------- | --- | ----- | ------------ | --- | ---------- | --------------- | ----------------------------- | --- | --- | --- | --- |
| Mikolov, | T., Sutskever, | I., | Chen, | K., Corrado, |     | G. S., and |                 |                               |     |     |     |     |
Dean,J. Distributedrepresentationsofwordsandphrases Zhou,M. Softplusregressionsandconvexpolytopes. arXiv
andtheircompositionally. InNIPS,pp.3111–3119,2013. preprintarXiv:1608.06383,2016.

WEDTM
| Zhou,M. NonparametricBayesiannegativebinomialfactor |                              |     |       |
| --------------------------------------------------- | ---------------------------- | --- | ----- |
| analysis. BayesianAnalysis,2018.                    |                              |     |       |
| Zhou,M.andCarin,L.                                  | Negativebinomialprocesscount |     |       |
| andmixturemodeling.                                 | TPAMI,37(2):307–320,2015.    |     |       |
| Zhou,M.,Hannah,L.,Dunson,D.B.,andCarin,L.           |                              |     | Beta- |
| negativebinomialprocessandPoissonfactoranalysis.    |                              |     | In    |
AISTATS,pp.1462–1471,2012.
| Zhou, M., Cong, | Y., and Chen,           | B. Augmentable | gamma |
| --------------- | ----------------------- | -------------- | ----- |
| beliefnetworks. | JMLR,17(163):1–44,2016. |                |       |
Zuo,Y.,Wu,J.,Zhang,H.,Lin,H.,Wang,F.,Xu,K.,and
| Xiong, H. | Topic modeling | of short texts: | A pseudo- |
| --------- | -------------- | --------------- | --------- |
InSIGKDD,pp.2105–2114,2016.
documentview.