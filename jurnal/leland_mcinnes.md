UMAP: Uniform Manifold
Approximation and Projection for
Dimension Reduction
Leland McInnes
Tutte Institute for Mathematics and Computing
leland.mcinnes@gmail.com
John Healy
Tutte Institute for Mathematics and Computing
jchealy@gmail.com
James Melville
jlmelville@gmail.com
September 21, 2020
Abstract
UMAP (Uniform Manifold Approximation and Projection) is a novel
manifoldlearningtechniquefordimensionreduction.UMAPisconstructed
fromatheoreticalframeworkbasedinRiemanniangeometryandalgebraic
topology. The result is a practical scalable algorithm that is applicable to
real world data. The UMAP algorithm is competitive with t-SNE for visu-
alizationquality,andarguablypreservesmoreoftheglobalstructurewith
superiorruntimeperformance. Furthermore,UMAPhasnocomputational
restrictionsonembeddingdimension,makingitviableasageneralpurpose
dimensionreductiontechniqueformachinelearning.
1 Introduction
Dimensionreductionplaysanimportantroleindatascience,beingafunda-
mental technique in both visualisation and as pre-processing for machine
1
0202
peS
81
]LM.tats[
3v62430.2081:viXra

| learning.                                           | Dimensionreductiontechniquesarebeingappliedinabroaden- |     |     |     |     |     |     |                |     |
| --------------------------------------------------- | ------------------------------------------------------ | --- | --- | --- | --- | --- | --- | -------------- | --- |
| ingrangeoffieldsandoneverincreasingsizesofdatasets. |                                                        |     |     |     |     |     |     | Itisthusdesir- |     |
abletohaveanalgorithmthatisbothscalabletomassivedataandableto
| copewiththediversityofdataavailable. |           |                                            |     |             | Dimensionreductionalgorithms |     |            |      |           |
| ------------------------------------ | --------- | ------------------------------------------ | --- | ----------- | ---------------------------- | --- | ---------- | ---- | --------- |
| tend to                              | fall into | two categories;                            |     | those       | that seek                    | to  | preserve   | the  | pairwise  |
| distance                             | structure | amongst                                    | all | the data    | samples                      | and | those      | that | favor the |
| preservation                         | of        | local distances                            |     | over global | distance.                    |     | Algorithms |      | such as   |
| PCA[27],                             | MDS[30],  | andSammonmapping[50]fallintotheformercate- |     |             |                              |     |            |      |           |
gorywhilet-SNE[59,58],Isomap[56],LargeVis[54],Laplacianeigenmaps
[6,7]anddiffusionmaps[16]allfallintothelattercategory.
Inthispaperweintroduceanovelmanifoldlearningtechniquefordi-
| mension | reduction. | We  | provide | a sound | mathematical |     | theory |     | grounding |
| ------- | ---------- | --- | ------- | ------- | ------------ | --- | ------ | --- | --------- |
thetechniqueandapracticalscalablealgorithmthatappliestorealworld
data.UMAP(UniformManifoldApproximationandProjection)buildsupon
| mathematical        |     | foundations                                 | related | to  | the work | of Belkin |     | and | Niyogi on |
| ------------------- | --- | ------------------------------------------- | ------- | --- | -------- | --------- | --- | --- | --------- |
| Laplacianeigenmaps. |     | Weseektoaddresstheissueofuniformdatadistri- |         |     |          |           |     |     |           |
butionsonmanifoldsthroughacombinationofRiemanniangeometryand
theworkofDavidSpivak[52]incategorytheoreticapproachestogeomet-
| ricrealizationoffuzzysimplicialsets. |     |               |     |                | t-SNEisthecurrentstate-of-the-art |           |             |                |         |
| ------------------------------------ | --- | ------------- | --- | -------------- | --------------------------------- | --------- | ----------- | -------------- | ------- |
| for dimension                        |     | reduction     | for | visualization. | Our                               | algorithm |             | is competitive |         |
| with t-SNE                           | for | visualization |     | quality and    | arguably                          | preserves |             | more           | of the  |
| global structure                     |     | with superior |     | run time       | performance.                      |           | Furthermore |                | the al- |
gorithmisabletoscaletosignificantlylargerdatasetsizesthanarefeasible
fort-SNE.Finally,UMAPhasnocomputationalrestrictionsonembedding
dimension,makingitviableasageneralpurposedimensionreductiontech-
niqueformachinelearning.
Baseduponpreliminaryreleasesofasoftwareimplementation,UMAP
hasalreadyfoundwidespreaduseinthefieldsofbioinformatics[5,12,17,
| 46, 2, 45, | 15], materials |     | science | [34, 23], | and | machine | learning |     | [14, 20, 21, |
| ---------- | -------------- | --- | ------- | --------- | --- | ------- | -------- | --- | ------------ |
24,19,47]amongothers.
| Thispaperislaidoutasfollows. |     |     |                                            | InSection2wedescribethetheoryun- |     |     |     |     |     |
| ---------------------------- | --- | --- | ------------------------------------------ | -------------------------------- | --- | --- | --- | --- | --- |
| derlyingthealgorithm.        |     |     | Section2isnecessarytounderstandboththethe- |                                  |     |     |     |     |     |
oryunderlyingwhyUMAPworksandthemotivationforthechoicesthat
| where made | in  | developing | the | algorithm. | A reader |     | without | a background |     |
| ---------- | --- | ---------- | --- | ---------- | -------- | --- | ------- | ------------ | --- |
(orinterest)intopologicaldataanalysis,categorytheoryorthetheoretical
underpinningsofUMAPshouldskipoverthissectionandproceeddirectly
toSection3.
Thatbeingsaid,wefeelthatstrongtheoryandmathematicallyjustified
algorithmicdecisionsareofparticularimportanceinthefieldofunsuper-
| visedlearning. |     | Thisis,atleastpartially,duetoplethoraofproposedobjec- |     |     |     |     |     |     |     |
| -------------- | --- | ----------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
2

| tive functions |     | within the | area. | We attempt | to  | highlight | in  | this paper | that |
| -------------- | --- | ---------- | ----- | ---------- | --- | --------- | --- | ---------- | ---- |
UMAPsdesigndecisionswereallgroundedinasolidtheoreticfoundation
andnotderivedthroughexperimentationwithanyparticulartaskfocused
| objectivefunction. |      | Thoughallneighbourhoodbasedmanifoldlearningal- |             |     |            |     |     |         |          |
| ------------------ | ---- | ---------------------------------------------- | ----------- | --- | ---------- | --- | --- | ------- | -------- |
| gorithms           | must | share certain                                  | fundamental |     | components |     | we  | believe | it to be |
advantageousforthesecomponentstobeselectedthroughwellgrounded
| theoretical | decisions. |     | One of | the primary | contributions |     | of  | this paper | is to |
| ----------- | ---------- | --- | ------ | ----------- | ------------- | --- | --- | ---------- | ----- |
reframetheproblemofmanifoldlearninganddimensionreductioninadif-
ferentmathematicallanguageallowingpracitionerstoapplyanewfieldof
mathemtaicstotheproblems.
| In Section |     | 3 we provide | a   | more computational |     |     | description | of  | UMAP. |
| ---------- | --- | ------------ | --- | ------------------ | --- | --- | ----------- | --- | ----- |
Section3shouldprovidereaderslessfamiliarwithtopologicaldataanalysis
withabetterfoundationforunderstandingthetheorydescribedinSection
2. AppendixCcontrastsUMAPagainstthemorefamiliaralgorithmst-SNE
| andLargeVis,describingallthesealgorithmsinsimilarlanguage. |     |     |     |     |     |     |     |     | Thissec- |
| ---------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | -------- |
tionshouldassistreadersalreadyfamiliarwiththosetechniquestoquickly
gainanunderstandingoftheUMAPalgorithmthoughtheywillgrantlittle
insiteintoitstheoreticalunderpinnings.
InSection4wediscussimplementationdetailsoftheUMAPalgorithm.
Thisincludesamoredetailedalgorithmicdescription,anddiscussionofthe
hyper-parametersinvolvedandtheirpracticaleffects.
InSection5weprovidepracticalresultsonrealworlddatasetsaswell
asscalingexperimentstodemonstratethealgorithm’sperformanceinreal
worldscenariosascomparedwithotherdimensionreductionalgorithms.
InSection6wediscussrelativeweakenessesofthealgorithm,andap-
plicationsforwhichUMAPmaynotbethebestchoice.
Finally,inSection7wedetailanumberofpotentialextensionsofUMAP
| that are | made  | possible | by its      | construction | upon | solid   | mathematical |                 | foun- |
| -------- | ----- | -------- | ----------- | ------------ | ---- | ------- | ------------ | --------------- | ----- |
| dations. | These | avenues  | for further | development  |      | include |              | semi-supervised |       |
learning,metriclearningandheterogeneousdataembedding.
| 2 Theoretical |     |     | Foundations |     |     | for | UMAP |     |     |
| ------------- | --- | --- | ----------- | --- | --- | --- | ---- | --- | --- |
ThetheoreticalfoundationsforUMAParelargelybasedinmanifoldtheory
| andtopologicaldataanalysis. |          |             |             | Muchofthetheoryismosteasilyexplained |         |      |            |     |           |
| --------------------------- | -------- | ----------- | ----------- | ------------------------------------ | ------- | ---- | ---------- | --- | --------- |
| in the                      | language | of topology |             | and category                         | theory. |      | Readers    | may | consult   |
| [39], [49]                  | and      | [40] for    | background. | Readers                              |         | more | interested | in  | practical |
computationalaspectsofthealgorithm,andnotnecessarilythetheoretical
| motivation | for | the computations |     | involved, | may | wish | to skip | this | section. |
| ---------- | --- | ---------------- | --- | --------- | --- | ---- | ------- | ---- | -------- |
3

Readers more familiar with traditional machine learning may find the re-
lationshipsbetweenUMAP,t-SNEandLargevizlocatedinAppendixCen-
lightening. Unfortunately,thispurelycomputationalviewfailstoshedany
light upon the reasoning that underlies the algorithmic decisions made in
UMAP.Withoutstrongtheoreticalfoundationstheonlyargumentswhich
can be made about algorithms amount to empirical measures, for which
therearenoclearuniversalchoicesforunsupervisedproblems.
Atahighlevel,UMAPuseslocalmanifoldapproximationsandpatches
togethertheirlocalfuzzysimplicialsetrepresentationstoconstructatopo-
logicalrepresentationofthehighdimensionaldata.Givensomelowdimen-
sionalrepresentationofthedata,asimilarprocesscanbeusedtoconstruct
anequivalenttopologicalrepresentation. UMAPthenoptimizesthelayout
of the data representation in the low dimensional space, to minimize the
cross-entropybetweenthetwotopologicalrepresentations.
The construction of fuzzy topological representations can be broken
down into two problems: approximating a manifold on which the data is
assumed to lie; and constructing a fuzzy simplicial set representation of
the approximated manifold. In explaining the algorithm we will first dis-
cuss the method of approximating the manifold for the source data. Next
we will discuss how to construct a fuzzy simplicial set structure from the
manifold approximation. Finally, we will discuss the construction of the
fuzzysimplicialsetassociatedtoalowdimensionalrepresentation(where
the manifold is simply Rd), and how to optimize the representation with
respecttoourobjectivefunction.
2.1 Uniformdistributionofdataonamanifoldand
geodesic approximation
The first step of our algorithm is to approximate the manifold we assume
the data (approximately) lies on. The manifold may be known apriori (as
simplyRn)ormayneedtobeinferredfromthedata. Supposethemanifold
isnotknowninadvanceandwewishtoapproximategeodesicdistanceon
it. LettheinputdatabeX = {X ,...,X }. AsintheworkofBelkinand
1 N
NiyogionLaplacianeigenmaps[6,7],fortheoreticalreasonsitisbeneficial
toassumethedataisuniformlydistributedonthemanifold,andevenifthat
assumptionisnotmade(e.g[26])resultsareonlyvalidinthelimitofinfinite
data.Inpractice,finiterealworlddataisrarelysonicelybehaved.However,
ifweassumethatthemanifoldhasaRiemannianmetricnotinheritedfrom
theambientspace,wecanfindametricsuchthatthedataisapproximately
uniformlydistributedwithregardtothatmetric.
4

Formally,letMbethemanifoldweassumethedatatolieon,andletg
betheRiemannianmetriconM. Thus,foreachpointp ∈ Mwehaveg ,
p
aninnerproductonthetangentspaceT M.
p
Lemma1. Let(M,g)beaRiemannianmanifoldinanambientRn,andlet
p ∈ M beapoint. Ifg islocallyconstantaboutpinanopenneighbourhood
U suchthatgisaconstantdiagonalmatrixinambientcoordinates,thenina
ballB ⊆ U centeredatpwithvolume
πn/2
withrespecttog,thegeodesic
Γ(n/2+1)
distancefromptoanypointq ∈ B is 1
r
dRn (p,q),whereristheradiusofthe
ballintheambientspaceanddRn istheexistingmetricontheambientspace.
SeeAppendixAofthesupplementarymaterialsforaproofofLemma
1.
IfweassumethedatatobeuniformlydistributedonM(withrespectto
g)then,awayfromanyboundaries,anyballoffixedvolumeshouldcontain
approximatelythesamenumberofpointsofX regardlessofwhereonthe
manifolditiscentered. Givenfinitedataandsmallenoughlocalneighbor-
hoods this crude approximation should be accurate enough even for data
samplesnearmanifoldboundaries. Now,conversely,aballcenteredatX
i
that contains exactly the k-nearest-neighbors of X should have approxi-
i
mately fixed volume regardless of the choice of X ∈ X. Under Lemma 1
i
itfollowsthatwecanapproximategeodesicdistancefromX toitsneigh-
i
borsbynormalisingdistanceswithrespecttothedistancetothek thnearest
neighborofX .
i
In essence, by creating a custom distance for each X , we can ensure
i
thevalidityoftheassumptionofuniformdistributiononthemanifold. The
cost is that we now have an independent notion of distance for each and
every X , and these notions of distance may not be compatible. We have
i
afamilyofdiscretemetricspaces(oneforeachX )thatwewishtomerge
i
into a consistent global structure. This can be done in a natural way by
convertingthemetricspacesintofuzzysimplicialsets.
2.2 Fuzzy topological representation
Wewillusefunctorsbetweentherelevantcategoriestoconvertfrommetric
spaces to fuzzy topological representations. This will provide a means to
merge the incompatible local views of the data. The topological structure
of choice is that of simplicial sets. For more details on simplicial sets we
refer the reader to [25], [40], [48], or [22]. Our approach draws heavily
upon the work of Michael Barr [3] and David Spivak in [52], and many
of the definitions and theorems below are drawn or adapted from those
5

| sources. | Weassumefamiliaritywiththebasicsofcategorytheory. |     |     |     |     |     |     | Foran |
| -------- | ------------------------------------------------- | --- | --- | --- | --- | --- | --- | ----- |
introductiontocategorytheoryreadersmayconsult[39]or[49].
| Tostartwewillreviewthedefinitionsforsimplicialsets.         |     |     |     |     |     |     | Simplicialsets |      |
| ----------------------------------------------------------- | --- | --- | --- | --- | --- | --- | -------------- | ---- |
| provideacombinatorialapproachtothestudyoftopologicalspaces. |     |     |     |     |     |     |                | They |
arerelatedtothesimplernotionofsimplicialcomplexes–whichconstruct
| topological               | spaces | by gluing | together                                 | simple |     | building | blocks | called sim- |
| ------------------------- | ------ | --------- | ---------------------------------------- | ------ | --- | -------- | ------ | ----------- |
| plices–butaremoregeneral. |        |           | Simplicialsetsaremosteasilydefinedpurely |        |     |          |        |             |
abstractlyinthelanguageofcategorytheory.
| Definition | 1.  | The category | ∆ has | as objects |     | the finite | order | sets [n] = |
| ---------- | --- | ------------ | ----- | ---------- | --- | ---------- | ----- | ---------- |
{1,...,n},withmorphimsgivenby(non-strictly)order-preservingmaps.
| Followingstandardcategorytheoreticnotation,∆ |     |     |     |     |     |     | op denotesthecate- |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ------------------ | --- |
gorywiththesameobjectsas∆andmorphismsgivenbythemorphisms
of∆withthedirection(domainandcodomain)reversed.
| Definition2. |     | Asimplicialsetisafunctorfrom∆optoSets,thecategoryof |     |     |     |     |     |     |
| ------------ | --- | --------------------------------------------------- | --- | --- | --- | --- | --- | --- |
sets;thatis,acontravariantfunctorfrom∆toSets.
| GivenasimplicialsetX |     |                                                   | : ∆ op | → Sets,itiscommontodenotetheset |     |     |     |     |
| -------------------- | --- | ------------------------------------------------- | ------ | ------------------------------- | --- | --- | --- | --- |
| X([n])asX            |     | andrefertotheelementsofthesetasthen-simplicesofX. |        |                                 |     |     |     |     |
n
Thesimplestpossibleexamplesofsimplicialsetsarethestandardsimplices
| ∆n,definedastherepresentablefunctorshom |     |     |     |     |     | (·,[n]). | Itfollowsfromthe |     |
| --------------------------------------- | --- | --- | --- | --- | --- | -------- | ---------------- | --- |
∆
Yonedalemmathatthereisanaturalcorrespondencebetweenn-simplices
| of and          | morphisms |          | in              | the category |       | of simplicial |     | sets, and it |
| --------------- | --------- | -------- | --------------- | ------------ | ----- | ------------- | --- | ------------ |
| X               |           | ∆n       | → X             |              |       |               |     |              |
| is often        | helpful   | to think | in these terms. |              | Thus  | for each      |     | we have      |
|                 |           |          |                 |              |       |               | x ∈ | X n          |
| a corresponding |           | morphism | x : ∆n          | →            | X. By | the density   |     | theorem and  |
employingaminorabuseofnotationwethenhave
|     |     |     | colim∆n | ∼   |     |     |     |     |
| --- | --- | --- | ------- | --- | --- | --- | --- | --- |
= X
x∈Xn
| There                 | is a | standard        | covariant functor |             |       |             | mapping  | from       |
| --------------------- | ---- | --------------- | ----------------- | ----------- | ----- | ----------- | -------- | ---------- |
|                       |      |                 |                   |             | |·| : | ∆ →         | Top      |            |
| the category          | ∆    | to the category | of                | topological |       | spaces that | sends    | [n] to the |
| standardn-simplex|∆n| |      |                 | ⊂ Rn+1 definedas  |             |       |             |          |            |
|                       |      | (cid:40)        |                   |             |       |             | (cid:41) |            |
n
|     | |∆n| | (cid:44) |            | Rn+1 | (cid:88) |         |     |     |
| --- | ---- | -------- | ---------- | ---- | -------- | ------- | --- | --- |
|     |      | (t       | ,...,t ) ∈ |      | |        | t = 1,t | ≥ 0 |     |
|     |      | 0        | n          |      |          | i       | i   |     |
i=0
| with the                               | standard | subspace | topology. | If  | X : ∆                    | op → | Sets is | a simplicial |
| -------------------------------------- | -------- | -------- | --------- | --- | ------------------------ | ---- | ------- | ------------ |
| setthenwecanconstructtherealizationofX |          |          |           |     | (denoted|X|)asthecolimit |      |         |              |
|X| = colim|∆n|
x∈Xn
6

and thus associate a topological space with a given simplicial set. Con-
verselygivenatopologicalspaceY wecanconstructanassociatedsimpli-
cialsetS(Y),calledthesingularsetofY,bydefining
S(Y) : [n] (cid:55)→ hom (|∆n|,Y).
Top
Itisastandardresultofclassicalhomotopytheorythattherealizationfunc-
torandsingularsetfunctorsformanadjunction,andprovidethestandard
means of translating between topological spaces and simplicial sets. Our
goal will be to adapt these powerful classical results to the case of finite
metricspaces.
We draw significant inspiration from Spivak, specifically [52], where
heextendstheclassicaltheoryofsingularsetsandtopologicalrealization
to fuzzy singular sets and metric realization. To develop this theory here
wewillfirstoutlineacategoricalpresentationoffuzzysets,dueto[3],that
will make extending classical simplicial sets to fuzzy simplicial sets most
natural.
Classically a fuzzy set [65] is defined in terms of a carrier set A and a
mapµ : A → [0,1]calledthemembershipfunction. Oneistointerpretthe
valueµ(x)forx ∈ AtobethemembershipstrengthofxtothesetA. Thus
membership of a set is no longer a bi-valent true or false property as in
classicalsettheory,butafuzzypropertytakingvaluesintheunitinterval.
Wewishtoformalizethisintermsofcategorytheory.
Let I be the unit interval (0,1] ⊆ R with topology given by intervals
oftheform[0,a)fora ∈ (0,1]. Thecategoryofopensets(withmorphisms
given by inclusions) can be imbued with a Grothendieck topology in the
naturalwayforanyposetcategory.
Definition3. ApresheafP onI isafunctorfromIop toSets. Afuzzyset
isapresheafonI suchthatallmapsP(a ≤ b)areinjections.
Presheaves on I form a category with morphisms given by natural
transformations. We can thus form a category of fuzzy sets by simply re-
strictingtothesub-categoryofpresheavesthatarefuzzysets. Wenotethat
suchpresheavesaretriviallysheavesundertheGrothendiecktopologyon
I. As one might expect, limits (including products) of such sheaves are
welldefined,butcaremustbetakentodefinecolimits(andcoproducts)of
sheaves. To link to the classical approach to fuzzy sets one can think of a
section P([0,a)) as the set of all elements with membership strength at
leasta. Wecannowdefinethecategoryoffuzzysets.
Definition 4. The category Fuzz of fuzzy sets is the full subcategory of
sheavesonI spannedbyfuzzysets.
7

With this categorical presentation in hand, defining fuzzy simplicial
setsissimplyamatterofconsideringpresheavesof∆valuedinthecate-
goryoffuzzysetsratherthanthecategoryofsets.
Definition 5. The category of fuzzy simplicial sets sFuzz is the category
with objects given by functors from ∆op to Fuzz, and morphisms given by
naturaltransformations.
Alternatively,afuzzysimplicialsetcanbeviewedasasheafover∆×I,
where∆isgiventhetrivialtopologyand∆×I hastheproducttopology.
Wewilluse∆n todenotethesheafgivenbytherepresentablefunctorof
<a
theobject([n],[0,a)). Theimportanceofthisfuzzy(sheafified)versionof
simplicialsetsistheirrelationshiptometricspaces. Webeginbyconsider-
ingthelargercategoryofextended-pseudo-metricspaces.
Definition 6. An extended-pseudo-metric space (X,d) is a set X and a
mapd : X ×X → R ∪{∞}suchthat
≥0
1. d(x,y) (cid:62) 0,andx = y impliesd(x,y) = 0;
2. d(x,y) = d(y,x);and
3. d(x,z) (cid:54) d(x,y)+d(y,z)ord(x,z) = ∞.
Thecategoryofextended-pseudo-metricspacesEPMethasasobjectsextended-
pseudo-metricspacesandnon-expansivemapsasmorphisms. Wedenotethe
subcategoryoffiniteextended-pseudo-metricspacesFinEPMet.
Thechoiceofnon-expansivemapsinDefinition6isduetoSpivak,but
wenotethatitcloselymirrorstheworkofCarlssonandMemoliin[13]on
topological methods for clustering as applied to finite metric spaces. This
choiceissignificantsincepureisometriesaretoostrictanddonotprovide
largeenoughHom-sets.
In [52] Spivak constructs a pair of adjoint functors, Real and Sing be-
tweenthecategoriessFuzzandEPMet. Thesefunctorsarethenaturalex-
tensionoftheclassicalrealizationandsingularsetfunctorsfromalgebraic
topology. ThefunctorRealisdefinedintermsofstandardfuzzysimplices
∆n as
<a
(cid:40) n (cid:41)
(cid:88)
Real(∆n ) (cid:44) (t ,...,t ) ∈ Rn+1 | t = −log(a),t ≥ 0
<a 0 n i i
i=0
similarlytotheclassicalrealizationfunctor|·|. ThemetriconReal(∆n )
<a
is simply inherited from Rn+1. A morphism ∆n → ∆m exists only if
<a <b
8

a ≤ b, and is determined by a ∆ morphism σ : [n] → [m]. The action of
Realonsuchamorphismisgivenbythemap
 
log(b) (cid:88) (cid:88) (cid:88)
(x 0 ,x 1 ,...,x n ) (cid:55)→
log(a)
 x i0 , x i0 ,..., x i0 .
i0∈σ−1(0) i0∈σ−1(1) i0∈σ−1(m)
Such a map is clearly non-expansive since 0 ≤ a ≤ b ≤ 1 implies that
log(b)/log(a) ≤ 1.
WethenextendthistoageneralsimplicialsetX viacolimits,defining
Real(X) (cid:44) colim Real(∆n ).
<a
∆n →X
<a
Since the functor Real preserves colimits, it follows that there exists a
right adjointfunctor. Again, analogouslyto the classicalcase, we findthe
rightadjoint,denotedSing,isdefinedforanextendedpseudometricspace
Y intermsofitsactiononthecategory∆×I:
Sing(Y) : ([n],[0,a)) (cid:55)→ hom (Real(∆n ),Y).
EPMet <a
For our case we are only interested in finite metric spaces. To corre-
spond with this we consider the subcategory of bounded fuzzy simplicial
sets Fin-sFuzz. We therefore use the analogous adjoint pair FinReal and
FinSing. Formallywedefinethefinitefuzzyrealizationfunctorasfollows:
Definition 7. Define the functor FinReal : Fin-sFuzz → FinEPMet by
setting
FinReal(∆n ) (cid:44) ({x ,x ,...,x },d ),
<a 1 2 n a
where

−log(a) ifi (cid:54)= j,
d (x ,x ) = .
a i j
0 otherwise
andthendefining
FinReal(X) (cid:44) colim FinReal(∆n ).
<a
∆n →X
<a
SimilartoSpivak’sconstruction,theactionofFinRealonamap∆n →
<a
∆m ,wherea ≤ bdefinedbyσ : ∆n → ∆m,isgivenby
<b
({x ,x ,...,x },d ) (cid:55)→ ({x ,x ,...,x },d ),
1 2 n a σ(1) σ(2) σ(n) b
whichisanon-expansivemapsincea ≤ bimpliesd ≥ d .
a b
SinceFinRealpreservescolimitsitadmitsarightadjoint,thefuzzysin-
gularsetfunctorFinSing. Wecanthendefinethe(finite)fuzzysingularset
functorintermsoftheactionofitsimageon∆×I,analogouslytoSing.
9

Definition8. DefinethefunctorFinSing : FinEPMet → Fin-sFuzzby
FinSing(Y) : ([n],[0,a)) (cid:55)→ hom (FinReal(∆n ),Y).
FinEPMet <a
Wethenhavethefollowingtheorem.
Theorem1. ThefunctorsFinReal : Fin-sFuzz → FinEPMetandFinSing :
FinEPMet → Fin-sFuzzformanadjunctionwithFinRealtheleftadjoint
andFinSingtherightadjoint.
The proof of this is by construction. Appendix B provides a full proof
ofthetheorem.
Withthenecessarytheoreticalbackgroundinplace,themeanstohan-
dlethefamilyofincompatiblemetricspacesdescribedabovebecomesclear.
Each metric space in the family can be translated into a fuzzy simplicial
setviathefuzzysingularsetfunctor,distillingthetopologicalinformation
whilestillretainingmetricinformationinthefuzzystructure. Ironingout
theincompatibilitiesoftheresultingfamilyoffuzzysimplicialsetscanbe
done by simply taking a (fuzzy) union across the entire family. The result
isasinglefuzzysimplicialsetwhichcapturestherelevanttopologicaland
underlyingmetricstructureofthemanifoldM.
Itshouldbenoted,however,thatthefuzzysingularsetfunctorapplies
to extended-pseudo-metric spaces, which are a relaxation of traditional
metric spaces. The results of Lemma 1 only provide accurate approxima-
tions of geodesic distance local to X for distances measured from X –
i i
thegeodesicdistancesbetweenotherpairsofpointswithintheneighbor-
hoodofX arenotwelldefined. Indeferencetothislackofinformationwe
i
definedistancesbetweenX andX intheextended-pseudometricspace
j k
localtoX (wherei (cid:54)= j andi (cid:54)= k)tobeinfinite(localneighborhoodsof
i
X andX willprovidesuitableapproximations).
j k
For real data it is safe to assume that the manifold M is locally con-
nected.Inpracticethiscanberealizedbymeasuringdistanceintheextended-
pseudo-metric space local to X as geodesic distance beyond the nearest
i
neighbor of X . Since this sets the distance to the nearest neighbor to be
i
equal to 0 this is only possible in the more relaxed setting of extended-
pseudo-metricspaces. It ensures, however, that each0-simplex istheface
of some 1-simplex with fuzzy membership strength 1, meaning that the
resulting topological structure derived from the manifold is locally con-
nected. We note that this has a similar practical effect to the truncated
similarity approach of Lee and Verleysen [33], but derives naturally from
theassumptionoflocalconnectivityofthemanifold.
10

Combining all of the above we can define the fuzzy topological repre-
sentationofadataset.
Definition9. LetX = {X ,...,X }beadatasetinRn.Let{(X,d )}
1 N i i=1...N
beafamilyofextended-pseudo-metricspaceswithcommoncarriersetXsuch
that

d (X ,X )−ρ ifi = j ori = k,
 M j k
d (X ,X ) =
i j k
∞ otherwise,
where ρ is the distance to the nearest neighbor of X and d is geodesic
i M
distance on the manifold M, either known apriori, or approximated as per
Lemma1.
ThefuzzytopologicalrepresentationofX is
n
(cid:91)
FinSing((X,d )).
i
i=1
The(fuzzyset)unionprovidesthemeanstomergetogetherthediffer-
ent metric spaces. This provides a single fuzzy simplicial set as the global
representationofthemanifoldformedbypatchingtogetherthemanylocal
representations.
Given the ability to construct such topological structures, either from
aknownmanifold,orbylearningthemetricstructureofthemanifold,we
can perform dimension reduction by simply finding low dimensional rep-
resentationsthatcloselymatchthetopologicalstructureofthesourcedata.
Wenowconsiderthetaskoffindingsuchalowdimensionalrepresentation.
2.3 Optimizing a low dimensional representation
LetY = {Y ,...,Y } ⊆ Rd bealowdimensional(d (cid:28) n)representation
1 N
of X such that Y represents the source data point X . In contrast to the
i i
source data where we want to estimate a manifold on which the data is
uniformlydistributed,atargetmanifoldforY ischosenapriori(usuallythis
will simply be Rd itself, but other choices such as d-spheres or d-tori are
certainlypossible). Thereforeweknowthemanifoldandmanifoldmetric
apriori, andcancomputethefuzzytopologicalrepresentationdirectly. Of
note,westillwanttoincorporatethedistancetothenearestneighborasper
thelocalconnectednessrequirement. Thiscanbeachievedbysupplyinga
parameterthatdefinestheexpecteddistancebetweennearestneighborsin
theembeddedspace.
11

GivenfuzzysimplicialsetrepresentationsofX andY,ameansofcom-
parison is required. If we consider only the 1-skeleton of the fuzzy sim-
plicial sets we can describe each as a fuzzy graph, or, more specifically, a
fuzzysetofedges. Tocomparetwofuzzysetswewillmakeuseoffuzzyset
cross entropy. For these purposes we will revert to classical fuzzy set no-
tation. Thatis,afuzzysetisgivenbyareferencesetAandamembership
strength function µ : A → [0,1]. Comparable fuzzy sets have the same
referenceset. GivenasheafrepresentationP wecantranslatetoclassical
fuzzysetsbysettingA = (cid:83) P([0,a))andµ(x) = sup{a ∈ (0,1] |
a∈(0,1]
x ∈ P([0,a))}.
Definition 10. The cross entropy C of two fuzzy sets (A,µ) and (A,ν) is
definedas
(cid:18) (cid:18) (cid:19) (cid:18) (cid:19)(cid:19)
(cid:88) µ(a) 1−µ(a)
C((A,µ),(A,ν)) (cid:44) µ(a)log +(1−µ(a))log .
ν(a) 1−ν(a)
a∈A
Similartot-SNEwecanoptimizetheembeddingY withrespecttofuzzy
setcrossentropyC byusingstochasticgradientdescent. However,thisre-
quiresadifferentiablefuzzysingularsetfunctor. Iftheexpectedminimum
distance between points is zero the fuzzy singular set functor is differen-
tiableforthesepurposes,howeverforanynon-zerovalueweneedtomake
a differentiable approximation (chosen from a suitable family of differen-
tiablefunctions).
This completes the algorithm: by using manifold approximation and
patchingtogetherlocalfuzzysimplicialsetrepresentationsweconstructa
topologicalrepresentationofthehighdimensionaldata. Wethenoptimize
thelayoutofdatainalowdimensionalspacetominimizetheerrorbetween
thetwotopologicalrepresentations.
Wenotethatinthiscasewerestrictedattentiontocomparisonsofthe
1-skeletonofthefuzzysimplicialsets. Onecanextendthisto(cid:96)-skeletaby
definingacostfunctionC as
(cid:96)
(cid:96)
(cid:88)
C (X,Y) = λ C(X ,Y ),
(cid:96) i i i
i=1
where X denotes the fuzzy set of i-simplices of X and the λ are suit-
i i
ablychosenrealvaluedweights. Whilesuchanapproachwillcapturethe
overall topological structure more accurately, it comes at non-negligible
computationalcostduetotheincreasinglylargenumbersofhigherdimen-
sional simplices. For this reason current implementations restrict to the
1-skeletonatthistime.
12

3 A Computational View of UMAP
TounderstandwhatcomputationstheUMAPalgorithmisactuallymaking
from a practical point of view, a less theoretical and more computational
descriptionmaybehelpfulforthereader. Thisdescriptionofthealgorithm
lacksthemotivationforanumberofthechoicesmade. Forthatmotivation
pleaseseeSection2.
The theoretical description of the algorithm works in terms of fuzzy
simplicialsets. Computationallythisisonlytractablefortheoneskeleton
which can ultimately be described as a weighted graph. This means that,
from a practical computational perspective, UMAP can ultimately be de-
scribed in terms of, construction of, and operations on, weighted graphs.
In particular this situates UMAP in the class of k-neighbour based graph
learningalgorithmssuchasLaplacianEigenmaps,Isomapandt-SNE.
As with other k-neighbour graph based algorithms, UMAP can be de-
scribedintwophases. Inthefirstphaseaparticularweightedk-neighbour
graphisconstructed. Inthesecondphasealowdimensionallayoutofthis
graph is computed. The differences between all algorithms in this class
amount to specific details in how the graph is constructed and how the
layoutiscomputed. ThetheoreticalbasisforUMAPasdescribedinSection
2 provides novel approaches to both of these phases, and provides clear
motivationforthechoicesinvolved.
Finally,sincet-SNEisnotusuallydescribedasagraphbasedalgorithm,
adirectcomparisonofUMAPwitht-SNE,usingthesimilarity/probability
notationcommonlyusedtoexpresstheequationsoft-SNE,isgiveninthe
AppendixC.
In section 2 we made a few basic assumptions about our data. From
these assumptions we made use of category theory to derive the UMAP
algorithms. Thatsaid,allthesederivationsassumetheseaxiomstobetrue.
1. There exists a manifold on which the data would be uniformly dis-
tributed.
2. Theunderlyingmanifoldofinterestislocallyconnected.
3. Preserving the topological structure of this manifold is the primary
goal.
ThetopologicaltheoryofSection2isdrivenbytheseaxioms,particularly
theinterestinmodellingandpreservingtopologicalstructure.Inparticular
Section 2.1 highlights the underlying motivation, in terms of topological
theory,ofrepresentingamanifoldasak-neighbourgraph.
13

As highlighted in Appendix C any algorithm that attempts to use a
mathematicalstructureakintoak-neighbourgraphtoapproximateaman-
ifoldmustfollowasimilarbasicstructure.
• GraphConstruction
1. Constructaweightedk-neighbourgraph
2. Applysometransformontheedgestoambientlocaldistance.
3. Dealwiththeinherentasymmetryofthek-neighbourgraph.
• GraphLayout
1. Defineanobjectivefunctionthatpreservesdesiredcharacteris-
ticsofthisk-neighbourgraph.
2. Findalowdimensionalrepresentationwhichoptimizesthisob-
jectivefunction.
Many dimension reduction algorithms can be broken down into these
stepsbecausetheyarefundamentaltoaparticularclassofsolutions.Choices
foreachstepmustbeeitherchosenthroughtaskorientedexperimentation
or by selecting a set of believable axioms and building strong theoretical
arguments from these. Our belief is that basing our decisions on a strong
foundational theory will allow for a more extensible and generalizable al-
gorithminthelongrun.
Wetheoreticallyjustifyusingthechoiceofusingak-neighbourgraph
torepresentamanifoldinSection2.1. Thechoicesforourkerneltransform
ansymmetrizationfunctioncanbefoundinSection2.2. Finally,thejustifi-
cationsunderlyingourchoicesforourgraphlayoutareoutlinedinSection
2.3.
3.1 Graph Construction
ThefirstphaseofUMAPcanbethoughtofastheconstructionofaweighted
k-neighbour graph. Let X = {x ,...,x } be the input dataset, with a
1 N
metric(ordissimilaritymeasure)d : X×X → R . Givenaninputhyper-
≥0
parameterk,foreachx wecomputetheset{x ,...,x }oftheknearest
i i1 i
k
neighborsofx underthemetricd. Thiscomputationcanbeperformedvia
i
anynearestneighbourorapproximatenearestneighboursearchalgorithm.
ForthepurposesofourUMAPimplemenationweprefertousethenearest
neighbordescentalgorithmof[18].
Foreachx wewilldefineρ andσ . Let
i i i
ρ = min{d(x ,x ) | 1 ≤ j ≤ k,d(x ,x ) > 0},
i i ij i ij
14

andsetσ tobethevaluesuchthat
i
(cid:88) k
exp
(cid:18)−max(0,d(x i ,x ij )−ρ i )(cid:19)
= log (k).
σ 2
i
j=1
Theselectionofρ derivesfromthelocal-connectivityconstraintdescribed
i
inSection2.2. Inparticularitensuresthatx connectstoatleastoneother
i
datapointwithanedgeofweight1;thisisequivalenttotheresultingfuzzy
simplicial set being locally connected at x . In practical terms this signif-
i
icantlyimproves therepresentation onvery highdimensional datawhere
other algorithms such as t-SNE begin to suffer from the curse of dimen-
sionality.
The selection of σ corresponds to (a smoothed) normalisation factor,
i
definingtheRiemannianmetriclocaltothepointx asdescribedinSection
i
2.1.
We can now define a weighted directed graph G¯ = (V,E,w). The
verticesV ofG¯ aresimplythesetX. Wecanthenformthesetofdirected
edges E = {(x ,x ) | 1 ≤ j ≤ k,1 ≤ i ≤ N}, and define the weight
i ij
functionw bysetting
(cid:18)−max(0,d(x ,x )−ρ )(cid:19)
w((x ,x )) = exp
i ij i
.
i ij
σ
i
Foragivenpointx thereexistsaninducedgraphofx andoutgoingedges
i i
incident on x . This graph is the 1-skeleton of the fuzzy simplicial set as-
i
sociated to the metric space local to x where the local metric is defined
i
in terms of ρ and σ . The weight associated to the edge is the member-
i i
ship strength of the corresponding 1-simplex within the fuzzy simplicial
set,andisderivedfromtheadjunctionofTheorem1usingtherightadjoint
(nearest inverse) of the geometric realization of a fuzzy simplicial set. In-
tuitively one can think of the weight of an edge as akin to the probability
that the given edge exists. Section 2 demonstrates why this construction
faithfully captures the topology of the data. Given this set of local graphs
(represented here as a single directed graph) we now require a method to
combinethemintoaunifiedtopologicalrepresentation.Wenotethatwhile
patchingtogetherincompatiblefinitemetricspacesischallenging,byusing
Theorem1toconverttoafuzzysimplicialsetrepresentation,thecombin-
ingoperationbecomesnatural.
Let A be the weighted adjacency matrix of G¯, and consider the sym-
metricmatrix
B = A+A(cid:62)−A◦A(cid:62),
15

where◦istheHadamard(orpointwise)product. Thisformuladerivesfrom
theuseoftheprobabilistict-conormusedinunioningthefuzzysimplicial
sets. If one interprets the value of A as the probability that the directed
ij
edge from x to x exists, then B is the probability that at least one of
i j ij
thetwodirectededges(fromx tox andfromx tox )exists. TheUMAP
i j j i
graphGisthenanundirectedweightedgraphwhoseadjacencymatrixis
givenbyB. Section2explainsthisconstructionintopologicalterms,pro-
viding the justification for why this construction provides an appropriate
fuzzytopologicalrepresentationofthedata–thatis,thisconstructioncap-
turestheunderlyinggeometricstructureofthedatainafaithfulway.
3.2 Graph Layout
In practice UMAP uses a force directed graph layout algorithm in low di-
mensionalspace. Aforcedirectedgraphlayoututilizesofasetofattractive
forcesappliedalongedgesandasetofrepulsiveforcesappliedamongver-
tices.Anyforcedirectedlayoutalgorithmrequiresadescriptionofboththe
attractive and repulsive forces. The algorithm proceeds by iteratively ap-
plyingattractiveandrepulsiveforcesateachedgeorvertex. Thisamounts
to a non-convex optimization problem. Convergence to a local minima is
guaranteed by slowly decreasing the attractive and repulsive forces in a
similarfashiontothatusedinsimulatedannealing.
In UMAP the attractive force between two vertices i and j at coordi-
natesy andy respectively,isdeterminedby:
i j
2(b−1)
−2ab(cid:107)y −y (cid:107)
i j 2 w((x ,x ))(y −y )
1+(cid:107)y −y (cid:107)2 i j i j
i j 2
whereaandbarehyper-parameters.
Repulsiveforcesarecomputedviasamplingduetocomputationalcon-
straints. Thus, whenever an attractive force is applied to an edge, one of
thatedge’sverticesisrepulsedbyasamplingofothervertices. Therepul-
siveforceisgivenby
2b
(1−w((x ,x )))(y −y ).
(cid:0) (cid:15)+(cid:107)y −y (cid:107)2 (cid:1)(cid:0) 1+a(cid:107)y −y (cid:107)2b (cid:1) i j i j
i j 2 i j 2
(cid:15) is a small number to prevent division by zero (0.001 in the current
implementation).
16

Thealgorithmcanbeinitializedrandomlybutinpractice,sincethesym-
metricLaplacianofthegraphGisadiscreteapproximationoftheLaplace-
Beltramioperatorofthemanifold,wecanuseaspectrallayouttoinitialize
theembedding. Thisprovidesbothfasterconvergenceandgreaterstability
withinthealgorithm.
The forces described above are derived from gradients optimising the
edge-wise cross-entropy between the weighted graph G, and an equiva-
lentweightedgraphH constructedfromthepoints{y } . Thatis,we
i i=1..N
areseekingtopositionpointsy suchthattheweightedgraphinducedby
i
those points most closely approximates the graph G, where we measure
thedifferencebetweenweightedgraphsbythetotalcrossentropyoverall
theedgeexistenceprobabilities. SincetheweightedgraphGcapturesthe
topologyofthesourcedata,theequivalentweightedgraphH constructed
fromthepoints{y } matchesthetopologyascloselyastheoptimiza-
i i=1..N
tionallows,andthusprovidesagoodlowdimensionalrepresentationofthe
overalltopologyofthedata.
4 ImplementationandHyper-parameters
Having completed a theoretical description of the approach, we now turn
our attention to the practical realization of this theory. We begin by pro-
viding a more detailed description of the algorithm as implemented, and
then discuss a few implementation specific details. We conclude this sec-
tionwithadiscussionofthehyper-parametersforthealgorithmandtheir
practicaleffects.
4.1 Algorithm description
In overview the UMAP algorithm is relatively straightforward (see Algo-
rithm 1). When performing a fuzzy union over local fuzzy simplicial sets
wehavefounditmosteffectivetoworkwiththeprobabilistict-conorm(as
onewouldexpectiftreatingmembershipstrengthsasaprobabilitythatthe
simplex exists). The individual functions for constructing the local fuzzy
simplicial sets, determining the spectral embedding, and optimizing the
embedding with regard to fuzzy set cross entropy, are described in more
detailbelow.
The inputs to Algorithm 1 are: X, the dataset to have its dimension
reduced; n, the neighborhood size to use for local metric approximation;
d, thedimensionofthetargetreducedspace; min-dist, analgorithmicpa-
17

Algorithm1UMAPalgorithm
functionUMAP(X,n,d,min-dist,n-epochs)
#Constructtherelevantweightedgraph
forallx ∈ X do
fs-set[x]←LocalFuzzySimplicialSet(X,x,n)
top-rep← (cid:83) fs-set[x] #Werecommendtheprobabilistict-conorm
x∈X
#Performoptimizationofthegraphlayout
Y ←SpectralEmbedding(top-rep,d)
Y ←OptimizeEmbedding(top-rep,Y,min-dist,n-epochs)
returnY
rameter controlling the layout; and n-epochs, controlling the amount of
optimizationworktoperform.
Algorithm 2 describes the construction of local fuzzy simplicial sets.
Torepresentfuzzysimplicialsetsweworkwiththefuzzysetimagesof[0]
and[1](i.e. the1-skeleton),whichwedenoteasfs-set andfs-set . Onecan
0 1
workwithhigherordersimplicesaswell, butthecurrentimplementation
doesnot. Wecanconstructthefuzzysimplicialsetlocaltoagivenpointx
byfindingthennearestneighbors,generatingtheappropriatenormalised
distance on the manifold, and then converting the finite metric space to a
simplicialsetviathefunctorFinSing,whichtranslatesintoexponentialof
thenegativedistanceinthiscase.
Rather than directly using the distance to the n th nearest neighbor as
the normalization, we use a smoothed version of knn-distance that fixes
thecardinalityofthefuzzysetof1-simplicestoafixedvalue. Weselected
log (n)forthispurposebasedonempiricalexperiments. Thisisdescribed
2
brieflyinAlgorithm3.
Spectral embedding is performed by considering the 1-skeleton of the
globalfuzzytopologicalrepresentationasaweightedgraphandusingstan-
dard spectral methods on the symmetric normalized Laplacian. This pro-
cessisdescribedinAlgorithm4.
The final major component of UMAP is the optimization of the em-
bedding through minimization of the fuzzy set cross entropy. Recall that
18

Algorithm2Constructingalocalfuzzysimplicialset
functionLocalFuzzySimplicialSet(X,x,n)
knn,knn-dists←ApproxNearestNeighbors(X,x,n)
←knn-dists[1] #Distancetonearestneighbor
ρ
| σ ←SmoothKNNDist(knn-dists,n,ρ) |     | #Smoothapproximatorto |     |     |
| ------------------------------- | --- | --------------------- | --- | --- |
knn-distance
fs-set
← X
0
| fs-set ← {([x,y],0) | | y ∈ X} |     |     |     |
| ------------------- | -------- | --- | --- | --- |
1
∈knndo
forally
d ← max{0,dist(x,y)−ρ}/σ
x,y
| fs-set ← fs-set | ∪ ([x,y],exp(−d | ))  |     |     |
| --------------- | --------------- | --- | --- | --- |
| 1               | 1               | x,y |     |     |
returnfs-set
Algorithm3Computethenormalizingfactorfordistancesσ
functionSmoothKNNDist(knn-dists,n,ρ)
suchthat(cid:80)n
| Binarysearchforσ |     | exp(−(knn-dists | −ρ)/σ) | = log (n) |
| ---------------- | --- | --------------- | ------ | --------- |
|                  |     | i=1             | i      | 2         |
returnσ
Algorithm4Spectralembeddingforinitialization
functionSpectralEmbedding(top-rep,d)
←1-skeletonoftop-repexpressedasaweightedadjacencymatrix
A
D ←degreematrixforthegraphA
L ← D1/2(D−A)D1/2
evec ←EigenvectorsofL(sorted)
| Y ← evec[1..d+1] |     | #0-baseindexingassumed |     |     |
| ---------------- | --- | ---------------------- | --- | --- |
returnY
19

fuzzysetcrossentropy,withrespectgivenmembershipfunctionsµandν,
isgivenby
|                |     |     |          | (cid:18) | (cid:19)     |     | (cid:18) | (cid:19) |
| -------------- | --- | --- | -------- | -------- | ------------ | --- | -------- | -------- |
|                |     |     | (cid:88) | µ(a)     |              |     |          | 1−µ(a)   |
| C((A,µ),(A,ν)) |     | =   | µ(a)log  |          | +(1−µ(a))log |     |          |          |
|                |     |     |          | ν(a)     |              |     |          | 1−ν(a)   |
a∈A
(cid:88)
|     |     | =   | (µ(a)log(µ(a))+(1−µ(a))log(1−µ(a))) |     |     |     |     |     |
| --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- |
a∈A
(cid:88)
|     |     |     | −   | (µ(a)log(ν(a))+(1−µ(a))log(1−ν(a))). |     |     |     |     |
| --- | --- | --- | --- | ------------------------------------ | --- | --- | --- | --- |
a∈A
(1)
| The first   | sum  | depends | only         | on µ which | takes         | fixed values | during | the op-     |
| ----------- | ---- | ------- | ------------ | ---------- | ------------- | ------------ | ------ | ----------- |
| timization, | thus | the     | minimization | of         | cross entropy | depends      |        | only on the |
secondsum,soweseektominimize
(cid:88)
− (µ(a)log(ν(a))+(1−µ(a))log(1−ν(a))).
a∈A
| Following                                           | both         | [54]                                               | and [41],     | we take   | a sampling  | based    | approach       | to the      |
| --------------------------------------------------- | ------------ | -------------------------------------------------- | ------------- | --------- | ----------- | -------- | -------------- | ----------- |
| optimization.                                       |              | Wesample1-simpliceswithprobabilityµ(a)andupdateac- |               |           |             |          |                |             |
| cording                                             | to the       | value                                              | of ν(a),      | which     | handles the | term     | µ(a)log(ν(a)). | The         |
| term                                                |              |                                                    |               | requires  | negative    | sampling | –              | rather than |
| (1                                                  | − µ(a))log(1 |                                                    | − ν(a))       |           |             |          |                |             |
| computing                                           | this         | over                                               | all potential | simplices | we          | randomly | sample         | potential   |
| 1-simplicesandassumethemtobeanegativeexample(i.e.   |              |                                                    |               |           |             |          | withmember-    |             |
| shipstrength0)andupdateaccordingtothevalueof1−ν(a). |              |                                                    |               |           |             |          |                | Incontrast  |
to[54]theaboveformulationprovidesavertexsamplingdistributionof
(cid:80)
1−µ(a)
{a∈A|d0(a)=xi}
|     |     | P(x | ) = |          |     |     |     |     |
| --- | --- | --- | --- | -------- | --- | --- | --- | --- |
|     |     |     | i   | (cid:80) |     |     |     |     |
1−µ(b)
{b∈A|d0(b)(cid:54)=xi}
fornegativesamples,whichcanbereasonablyapproximatedbyauniform
distributionforsufficientlylargedatasets.
Itthereforeonlyremainstofindadifferentiableapproximationtoν(a)
| for a given | 1-simplex |     | so  | that gradient | descent | can | be applied | for opti- |
| ----------- | --------- | --- | --- | ------------- | ------- | --- | ---------- | --------- |
a
| mization.     | Thisisdoneasfollows: |         |     |         |                                 |     |     |     |
| ------------- | -------------------- | ------- | --- | ------- | ------------------------------- | --- | --- | --- |
| Definition11. |                      | DefineΦ | :   | Rd×Rd → | [0,1],asmoothapproximationofthe |     |     |     |
membershipstrengthofa1-simplexbetweentwopointsinRd,as
|     |     |        |     | (cid:16)                       |     | (cid:17)−1 |     |     |
| --- | --- | ------ | --- | ------------------------------ | --- | ---------- | --- | --- |
|     |     | Φ(x,y) |     | = 1+a((cid:107)x−y(cid:107)2)b |     |            | ,   |     |
2
20

whereaandbarechosenbynon-linearleastsquaresfittingagainstthecurve
Rd×Rd
| Ψ : | → [0,1]where |     |     |     |     |     |
| --- | ------------ | --- | --- | --- | --- | --- |
(cid:40)
|        | 1                           |     |             | if(cid:107)x−y(cid:107) | ≤   | min-dist |
| ------ | --------------------------- | --- | ----------- | ----------------------- | --- | -------- |
| Ψ(x,y) | =                           |     |             |                         | 2   | .        |
|        | exp(−((cid:107)x−y(cid:107) |     | −min-dist)) | otherwise               |     |          |
2
| The optimization |     | process | is now executed | by stochastic | gradient | de- |
| ---------------- | --- | ------- | --------------- | ------------- | -------- | --- |
scentasgivenbyAlgorithm5.
Algorithm5Optimizingtheembedding
functionOptimizeEmbedding(top-rep,Y,min-dist,n-epochs)
α ← 1.0
FitΦfromΨdefinedbymin-dist
| fore ← | 1,...,n-epochsdo |     |     |     |     |     |
| ------ | ---------------- | --- | --- | --- | --- | --- |
top-rep
| forall([a,b],p) |     | ∈   | do  |     |     |     |
| --------------- | --- | --- | --- | --- | --- | --- |
1
|     | Random()≤ |                  |     | #Samplesimplexwithprobabilityp |     |     |
| --- | --------- | ---------------- | --- | ------------------------------ | --- | --- |
| if  |           | pthen            |     |                                |     |     |
|     | y ←       | y +α·∇(log(Φ))(y |     | ,y )                           |     |     |
|     | a         | a                |     | a b                            |     |     |
1,...,n-neg-samplesdo
fori ←
c ← randomsamplefromY
|     | y   | ← y +α·∇(log(1−Φ))(y |     | ,y  | )   |     |
| --- | --- | -------------------- | --- | --- | --- | --- |
|     |     | a a                  |     | a   | c   |     |
1.0−e/n-epochs
α ←
returnY
ThiscompletestheUMAPalgorithm.
4.2 Implementation
Practicalimplementationofthisalgorithmrequires(approximate)k-nearest-
neighborcalculationandefficientoptimizationviastochasticgradientde-
scent.
Efficientapproximatek-nearest-neighborcomputationcanbeachieved
| viatheNearest-Neighbor-Descentalgorithmof[18]. |           |           |                                    | Theerrorintrinsicin |     |         |
| ---------------------------------------------- | --------- | --------- | ---------------------------------- | ------------------- | --- | ------- |
| a dimension                                    | reduction | technique | means that                         | such approximation  |     | is more |
| thanadequateforthesepurposes.                  |           |           | Whilenotheoreticalcomplexitybounds |                     |     |         |
21

have been established for Nearest-Neighbor-Descent the authors of the
originalpaperreportanempiricalcomplexityofO(N1.14). Afurtherben-
efitofNearest-Neighbor-Descentisitsgenerality; itworkswithanyvalid
dissimilaritymeasure,andisefficientevenforhighdimensionaldata.
Inoptimizingtheembeddingundertheprovidedobjectivefunction,we
follow work of [54]; making use of probabilistic edge sampling and nega-
tive sampling [41]. This provides a very efficient approximate stochastic
gradient descent algorithm since there is no normalization requirement.
Furthermore,sincethenormalizedLaplacianofthefuzzygraphrepresen-
tationoftheinputdataisadiscreteapproximationoftheLaplace-Betrami
operatorofthemanifold[?,see]]belkin2002laplacian,belkin2003laplacian,
we can provide a suitable initialization for stochastic gradient descent by
using the eigenvectors of the normalized Laplacian. The amount of opti-
mization work required will scale with the number of edges in the fuzzy
graph(assumingafixednegativesamplingrate),resultinginacomplexity
ofO(kN).
Combiningthesetechniquesresultsinhighlyefficientembeddings,which
wewilldiscussinSection5. Theoverallcomplexityisboundedbytheap-
proximatenearestneighborsearchcomplexityand,asmentionedabove,is
empirically approximately O(N1.14). A reference implementation can be
found at https://github.com/lmcinnes/umap, and an R implementa-
tioncanbefoundathttps://github.com/jlmelville/uwot.
Forsimplicitytheseexperimentswerecarriedoutonasinglecorever-
sionofouralgorithm. Itshouldbenotedthatatthetimeofthispublication
thatbothNearest-Neighbour-DescentandSGDhavebeenparallelizedand
thusthepythonreferenceimplementationcanbesignificantlyaccelerated.
Ourintentioninthispaperwastointroducetheunderlyingtheorybehind
our UMAP algorithm and we felt that parallel vs single core discussions
woulddistractfromourintent.
4.3 Hyper-parameters
AsdescribedinAlgorithm1,theUMAPalgorithmtakesfourhyper-parameters:
1. n,thenumberofneighborstoconsiderwhenapproximatingthelocal
metric;
2. d,thetargetembeddingdimension;
3. min-dist, the desired separation between close points in the embed-
dingspace;and
22

4. n-epochs,thenumberoftrainingepochstousewhenoptimizingthe
lowdimensionalrepresentation.
| The effects | of the parameters |            | d and  | n-epochs | are | largely  | self-evident, |         | and    |
| ----------- | ----------------- | ---------- | ------ | -------- | --- | -------- | ------------- | ------- | ------ |
| will not    | be discussed      | in further | detail | here.    | In  | contrast | the           | effects | of the |
numberofneighborsnandofmin-distarelessclear.
Onecaninterpretthenumberofneighborsnasthelocalscaleatwhich
toapproximatethemanifoldasroughlyflat,withthemanifoldestimation
| averaging | over the | neighbors. | Manifold |     | features | that | occur | at  | a smaller |
| --------- | -------- | ---------- | -------- | --- | -------- | ---- | ----- | --- | --------- |
n
scalethanwithinthennearest-neighborsofpointswillbelost,whilelarge
scalemanifoldfeaturesthatcannotbeseenbypatchingtogetherlocallyflat
| charts at | the scale of | nearest-neighbors |     |     | may | not be | well | detected. | Thus |
| --------- | ------------ | ----------------- | --- | --- | --- | ------ | ---- | --------- | ---- |
n
nrepresentssomedegreeoftrade-offbetweenfinegrainedandlargescale
manifoldfeatures—smallervalueswillensuredetailedmanifoldstructure
isaccuratelycaptured(atalossofthe“bigpicture”viewofthemanifold),
whilelargervalueswillcapturelargescalemanifoldstructures,butataloss
offinedetailstructurewhichwillgetaveragedoutinthelocalapproxima-
| tions. With | smaller | n values | the manifold |     | tends | to be | broken | into | many |
| ----------- | ------- | -------- | ------------ | --- | ----- | ----- | ------ | ---- | ---- |
smallconnectedcomponents(careneedstobetakenwiththespectralem-
beddingforinitializationinsuchcases).
| In contrast | min-dist | is a | hyperparameter |     | directly |     | affecting | the | output, |
| ----------- | -------- | ---- | -------------- | --- | -------- | --- | --------- | --- | ------- |
asitcontrolsthefuzzysimplicialsetconstructionfromthelowdimensional
| representation.                                       | It acts | in lieu | of the                                  | distance | to  | the nearest |     | neighbor  | used |
| ----------------------------------------------------- | ------- | ------- | --------------------------------------- | -------- | --- | ----------- | --- | --------- | ---- |
| toensurelocalconnectivity.                            |         |         | Inessencethisdetermineshowcloselypoints |          |     |             |     |           |      |
| canbepackedtogetherinthelowdimensionalrepresentation. |         |         |                                         |          |     |             |     | Lowvalues |      |
onmin-distwillresultinpotentiallydenselypackedregions,butwilllikely
| more faithfully                                      | represent      | the       | manifold | structure. |        | Increasing |                | the       | value of |
| ---------------------------------------------------- | -------------- | --------- | -------- | ---------- | ------ | ---------- | -------------- | --------- | -------- |
| min-dist                                             | will force the | embedding |          | to spread  | points | out        | more,          | assisting | vi-      |
| sualization(andavoidingpotentialoverplottingissues). |                |           |          |            |        |            | Weviewmin-dist |           |          |
asanessentiallyaestheticparameter,governingtheappearanceoftheem-
bedding,andthusismoreimportantwhenusingUMAPforvisualization.
| In Figure  | 1 we provide |          | examples | of the | effects | of     | varying | the | hyper- |
| ---------- | ------------ | -------- | -------- | ------ | ------- | ------ | ------- | --- | ------ |
| parameters | for a toy    | dataset. | The data | is     | uniform | random | samples |     | from a |
3-dimensionalcolor-cube,allowingforeasyvisualizationoftheoriginal3-
dimensionalcoordinatesintheembeddingspacebyusingthecorrespond-
| ing RGB | colour. Since | the data | fills | a 3-dimensional |     | cube | there | is  | no local |
| ------- | ------------- | -------- | ----- | --------------- | --- | ---- | ----- | --- | -------- |
manifoldstructure,andhenceforsuchdataweexpectlargernvaluestobe
| moreuseful. | Lowvalueswillinterpretthenoisefromrandomsamplingas |     |     |     |     |     |     |     |     |
| ----------- | -------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
finescalemanifoldstructure,producingpotentiallyspuriousstructure1.
1SeethediscussionoftheconstellationeffectinSection6
23

Figure1: VariationofUMAPhyperparametersnandmin-distresultindifferent
embeddings. The data is uniform random samples from a 3-dimensional color-
cube, allowing for easy visualization of the original 3-dimensional coordinates
in the embedding space by using the corresponding RGB colour. Low values of
nspuriouslyinterpretstructurefromtherandomsamplingnoise–seeSection6
forfurtherdiscussionofthisphenomena.
24

| In Figure | 2        | we provides |               | examples   | of the | same    | hyperparamter  |           | choices |
| --------- | -------- | ----------- | ------------- | ---------- | ------ | ------- | -------------- | --------- | ------- |
| as Figure | 1, but   | for         | the PenDigits | dataset2.  |        | In this | case           | we expect | small   |
| to medium | n values |             | to be most    | effective, | since  | there   | is significant |           | cluster |
structurenaturallypresentinthedata.Themin-distparameterexpandsout
tightlyclusteredgroups,allowingmoreoftheinternalstructureofdensely
packedclusterstobeseen.
Finally,inFigure3weprovideanequivalentexampleofhyperparame-
| terchoicesfortheMNISTdataset3. |     |     |     | Again,sincethisdatasetisexpectedto |     |     |     |     |     |
| ------------------------------ | --- | --- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
havesignifcantclusterstructureweexpectmediumsizedvaluesofntobe
| most effective. |       | We note    | that      | large values | of     | min-dist | result       | in the  | distinct |
| --------------- | ----- | ---------- | --------- | ------------ | ------ | -------- | ------------ | ------- | -------- |
| clusters        | being | compressed | together, |              | making | the      | distinctions | between | the      |
clusterslessclear.
| 5 Practical |     |     | Efficacy |     |     |     |     |     |     |
| ----------- | --- | --- | -------- | --- | --- | --- | --- | --- | --- |
WhilethestrongmathematicalfoundationsofUMAPwerethemotivation
| for its development, |     |         | the algorithm | must       | ultimately |          | be judged | by          | its prac- |
| -------------------- | --- | ------- | ------------- | ---------- | ---------- | -------- | --------- | ----------- | --------- |
| tical efficacy.      |     | In this | section       | we examine | the        | fidelity | and       | performance | of        |
lowdimensionalembeddingsofmultiplediverserealworlddatasetsunder
UMAP.Thefollowingdatasetswereconsidered:
Pendigits[1,10]isasetof1797grayscaleimagesofdigitsenteredusing
| adigitisertablet. |     | Eachimageisan8x8imagewhichwetreatasasingle64 |     |     |     |     |     |     |     |
| ----------------- | --- | -------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
dimensionalvector,assumedtobeinEuclideanvectorspace.
COIL20[43]isasetof1440greyscaleimagesconsistingof20objectsun-
| der 72 different |     | rotations | spanning | 360 | degrees. |     | Each image | is  | a 128x128 |
| ---------------- | --- | --------- | -------- | --- | -------- | --- | ---------- | --- | --------- |
imagewhichwetreatasasingle16384dimensionalvectorforthepurposes
ofcomputingdistancebetweenimages.
COIL100[44]isasetof7200colourimagesconsistingof100objectsun-
| der 72 different |           | rotations   | spanning | 360      | degrees.     |           | Each image   | consists | of 3     |
| ---------------- | --------- | ----------- | -------- | -------- | ------------ | --------- | ------------ | -------- | -------- |
| 128x128          | intensity | matrices    | (one     | for each | color        | channel). |              | We treat | this as  |
| a single         | 49152     | dimensional | vector   | for      | the purposes |           | of computing |          | distance |
betweenimages.
| Mouse             | scRNA-seq |     | [11] is profiled                            |     | gene expression |     | data | for 20,921 | cells |
| ----------------- | --------- | --- | ------------------------------------------- | --- | --------------- | --- | ---- | ---------- | ----- |
| fromanadultmouse. |           |     | Eachsampleconsistsofavectorof26,774measure- |     |                 |     |      |            |       |
ments.
Statlog(Shuttle)[35]isaNASAdatasetconsistingofvariousdataassoci-
atedtothepositionsofradiatorsinthespaceshuttle,includingatimestamp.
2SeeSection5foradescriptionofthePenDigitsdataset
3Seesection5fordetailsontheMNISTdataset
25

Figure 2: Variation of UMAP hyperparameters n and min-dist result in differ-
ent embeddings. The data is the PenDigits dataset, where each point is an 8x8
grayscaleimageofahand-writtendigit.
26

Figure 3: Variation of UMAP hyperparameters n and min-dist result in differ-
ent embeddings. The data is the MNIST dataset, where each point is an 28x28
grayscaleimageofahand-writtendigit.
27

Thedatasethas58000pointsina9dimensionalfeaturespace.
MNIST [32] is a dataset of 28x28 pixel grayscale images of handwritten
digits. Thereare10digitclasses(0through9)and70000totalimages. This
istreatedas70000different784dimensionalvectors.
F-MNIST[63]orFashionMNISTisadatasetof28x28pixelgrayscaleim-
ages of fashion items (clothing, footwear and bags). There are 10 classes
and 70000 total images. As with MNIST this is treated as 70000 different
784dimensionalvectors.
Flow cytometry [51, 9] is a dataset of flow cytometry measurements of
CDT4cellscomprisedof1,000,000samples,eachwith17measurements.
GoogleNewswordvectors[41]isadatasetof3millionwordsandphrases
derivedfromasampleofGoogleNewsdocumentsandembeddedintoa300
dimensionalspaceviaword2vec.
For all the datasets except GoogleNews we use Euclidean distance be-
tween vectors. For GoogleNews, as per [41], we use cosine distance (or
angulardistanceint-SNEwhichdoessupportnon-metricdistances,incon-
trasttoUMAP).
5.1 QualitativeComparisonofMultipleAlgorithms
Wecompareanumberofalgorithms–UMAP,t-SNE[60,58],LargeVis[54],
Laplacian Eigenmaps [7], and Principal Component Analysis [27]–on the
COIL20[43],MNIST[32],Fashion-MNIST[63],andGoogleNews[41]datasets.
TheIsomapalgorithmwasalsotested,butfailedtocompleteinanyreason-
abletimeforanyofthedatasetslargerthanCOIL20.
The Multicore t-SNE package [57] was used for t-SNE. The reference
implementation [53] was used for LargeVis. The scikit-learn [10] imple-
mentations were used for Laplacian Eigenmaps and PCA. Where possible
we attempted to tune parameters for each algorithm to give good embed-
dings.
Historicallyt-SNEandLargeVishaveofferedadramaticimprovement
infindingandpreservinglocalstructureinthedata. Thiscanbeseenqual-
itatively by comparing their embeddings to those generated by Laplacian
EigenmapsandPCAinFigure4. Weclaimthatthequalityofembeddings
producedbyUMAPiscomparabletot-SNEwhenreducingtotwoorthree
dimensions. For example, Figure 4 shows both UMAP and t-SNE embed-
dings of the COIL20, MNIST, Fashion MNIST, and Google News datasets.
Whilethepreciseembeddingsaredifferent,UMAPdistinguishesthesame
structuresast-SNEandLargeVis.
28

Figure 4: A comparison of several dimension reduction algorithms. We note
that UMAP successfully reflects much of the large scale global structure that is
well represented by Laplacian Eigenmaps and PCA (particularly for MNIST and
Fashion-MNIST), while also preserving the local fine structure similar to t-SNE
andLargeVis.
29

ItcanbearguedthatUMAPhascapturedmoreoftheglobalandtopo-
logicalstructureofthedatasetsthant-SNE[4,62]. Moreoftheloopsinthe
COIL20 dataset are kept intact, including the intertwined loops. Similarly
theglobalrelationshipsamongdifferentdigitsintheMNISTdigitsdataset
are more clearly captured with 1 (red) and 0 (dark red) at far corners of
theembeddingspace,and4,7,9(yellow,sea-green,andviolet)and3,5,8(or-
ange, chartreuse, and blue) separated as distinct clumps of similar digits.
In the Fashion MNIST dataset the distinction between clothing (dark red,
yellow,orange,vermilion)andfootwear(chartreuse,sea-green,andviolet)
ismademoreclear. Finally,whilebotht-SNEandUMAPcapturegroupsof
similar word vectors, the UMAP embedding arguably evidences a clearer
globalstructureamongthevariouswordclusters.
5.2 QuantitativeComparisonofMultipleAlgorithms
We compare UMAP, t-SNE, LargeVis, Laplacian Eigenmaps and PCA em-
beddings with respect to the performance of a k-nearest neighbor clas-
sifier trained on the embedding space for a variety of datasets. The k-
nearestneighborclassifieraccuracyprovidesaclearquantitativemeasure
ofhowwelltheembeddinghaspreservedtheimportantlocalstructureof
the dataset. By varying the hyper-parameter k used in the training we
canalsoconsiderhowstructurepreservationvariesundertransitionfrom
purely local to non-local, to more global structure. The embeddings used
fortrainingthekNNclassifierareforthosedatasetsthatcomewithdefined
traininglabels: PenDigits,COIL-20,Shuttle,MNIST,andFashion-MNIST.
Wedividethedatasetsintotwoclasses:smallerdatasets(PenDigitsand
COIL-20), for which a smaller range of k values makes sense, and larger
datasets, for which much larger values of k are reasonable. For each of
the small datasets a stratified 10-fold cross-validation was used to derive
a set of 10 accuracy scores for each embedding. For the Shuttle dataset a
10-foldcross-validationwasusedduetoconstraintsimposedbyclasssizes
andthestratifiedsampling. ForMNISTandFashion-MNISTa20-foldcross
validationwasused,producing20accuracyscores.
In Table 1 we present the average accuracy across the 10-folds for the
PenDigitsandCOIL-20datasets. UMAPperformsatleastaswellast-SNE
and LargeVis (given the confidence bounds on the accuracy) for k in the
range10to40,butforlargerkvaluesof80and160UMAPhassignificantly
higher accuracy on COIL-20, and shows evidence of higher accuracy on
PenDigits. Figure5providesswarmplotsoftheaccuracyresultsacrossthe
COIL-20andPenDigitsdatasets.
30

InTable2wepresenttheaveragecrossvalidationaccuracyfortheShut-
tle, MNIST and Fashion-MNIST datasets. UMAP performs at least as well
ast-SNEandLargeVis(giventheconfidenceboundsontheaccuracy)fork
intherange100to400ontheShuttleandMNISTdatasets(butnotablyun-
derperformsontheFashion-MNISTdataset),butforlargerk valuesof800
and 3200 UMAP has significantly higher accuracy on the Shuttle dataset,
andshowsevidenceofhigheraccuracyonMNIST.Forkvaluesof1600and
3200 UMAP establishes comparable performance on Fashion-MNIST. Fig-
ure 6 provides swarm plots of the accuracy results across the Shuttle and
MNISTandFashion-MNISTdatasets.
k t-SNE UMAP LargeVis Eigenmaps PCA
02-LIOC
10 0.934 0.921 0.888 0.629 0.667
(±0.115) (±0.075) (±0.092) (±0.153) (±0.179)
20 0.901 0.907 0.870 0.605 0.663
(±0.133) (±0.064) (±0.125) (±0.185) (±0.196)
40 0.857 0.904 0.833 0.578 0.620
(±0.125) (±0.056) (±0.106) (±0.159) (±0.230)
80 0.789 0.899 0.803 0.565 0.531
(±0.118) (±0.058) (±0.100) (±0.119) (±0.294)
160 0.609 0.803 0.616 0.446 0.375
(±0.067) (±0.138) (±0.066) (±0.110) (±0.111)
stigiDneP
10 0.977 0.973 0.966 0.778 0.622
(±0.033) (±0.044) (±0.053) (±0.113) (±0.092)
20 0.973 0.976 0.973 0.778 0.633
(±0.033) (±0.035) (±0.044) (±0.116) (±0.082)
40 0.956 0.954 0.959 0.778 0.636
(±0.064) (±0.060) (±0.066) (±0.112) (±0.078)
80 0.948 0.951 0.949 0.767 0.643
(±0.060) (±0.072) (±0.072) (±0.111) (±0.085)
160 0.949 0.951 0.921 0.747 0.629
(±0.065) (±0.085) (±0.085) (±0.108) (±0.107)
Table 1: kNN Classifier accuracy for varying values of k over the embedding
spaces of COIL-20 and PenDigits datasets. Average accuracy scores are given
over a 10-fold cross-validation for each of PCA, Laplacian Eigenmaps, LargeVis,
t-SNEandUMAP.
As evidenced by this comparison UMAP provides largely comparable
perfomanceinembeddingqualitytot-SNEandLargeVisatlocalscales,but
performsmarkedlybetterthant-SNEorLargeVisatnon-localscales. This
bearsoutthevisualqualitativeassessmentprovidedinSubsection5.1.
5.3 Embedding Stability
Since UMAP makes use of both stochastic approximate nearest neighbor
search, and stochastic gradient descent with negative sampling for opti-
mization,theresultingembeddingisnecessarilydifferentfromruntorun,
and under sub-sampling of the data. This is potentially a concern for a
31

| k           | t-SNE          | UMAP     | LargeVis | Eigenmaps |          | PCA      |
| ----------- | -------------- | -------- | -------- | --------- | -------- | -------- |
| 100         |                | 0.993    | 0.992    | 0.962     |          | 0.833    |
|             | 0.994 (±0.002) | (±0.002) | (±0.003) |           | (±0.004) | (±0.013) |
| 200         |                | 0.990    | 0.987    | 0.957     |          | 0.821    |
|             | 0.992 (±0.002) | (±0.002) | (±0.003) |           | (±0.006) | (±0.007) |
| elttuhS 400 |                | 0.988    | 0.976    | 0.949     |          | 0.815    |
|             | 0.990 (±0.002) | (±0.002) | (±0.003) |           | (±0.006) | (±0.007) |
| 800         | 0.969          | 0.988    | 0.957    | 0.942     |          | 0.804    |
|             | (±0.005)       | (±0.002) | (±0.004) |           | (±0.006) | (±0.003) |
| 1600        | 0.927          | 0.981    | 0.904    | 0.918     |          | 0.792    |
|             | (±0.005)       | (±0.002) | (±0.007) |           | (±0.006) | (±0.003) |
| 3200        | 0.828          | 0.957    | 0.850    | 0.895     |          | 0.786    |
|             | (±0.004)       | (±0.005) | (±0.008) |           | (±0.006) | (±0.001) |
| 100         | 0.967          | 0.967    | 0.962    | 0.668     |          | 0.462    |
|             | (±0.015)       | (±0.014) | (±0.015) |           | (±0.016) | (±0.023) |
| 200         | 0.966          |          | 0.962    | 0.667     |          | 0.467    |
0.967
|           | (±0.015) | (±0.014) | (±0.015) |       | (±0.016) | (±0.023) |
| --------- | -------- | -------- | -------- | ----- | -------- | -------- |
| TSINM 400 | 0.964    |          | 0.961    | 0.664 |          | 0.468    |
0.967
|               | (±0.015) | (±0.014)       | (±0.015) |       | (±0.016) | (±0.024)  |
| ------------- | -------- | -------------- | -------- | ----- | -------- | --------- |
| 800           | 0.963    |                | 0.961    | 0.660 |          | 0.468     |
|               | (±0.016) | 0.967 (±0.014) | (±0.015) |       | (±0.017) | (±0.023)  |
| 1600          | 0.959    |                | 0.947    | 0.651 |          | 0.467     |
|               | (±0.016) | 0.966 (±0.014) | (±0.015) |       | (±0.014) | (±0.0233) |
| 3200          | 0.946    |                | 0.920    | 0.639 |          | 0.459     |
|               | (±0.017) | 0.964 (±0.014) | (±0.017) |       | (±0.017) | (±0.022)  |
| 100           | 0.818    | 0.790          | 0.808    | 0.631 |          | 0.564     |
| TSINM-noihsaF | (±0.012) | (±0.013)       | (±0.014) |       | (±0.010) | (±0.018)  |
| 200           | 0.810    | 0.785          | 0.805    | 0.624 |          | 0.565     |
|               | (±0.013) | (±0.014)       | (±0.013) |       | (±0.013) | (±0.016)  |
| 400           | 0.801    | 0.780          | 0.796    | 0.612 |          | 0.564     |
|               | (±0.013) | (±0.013)       | (±0.013) |       | (±0.011) | (±0.017)  |
| 800           | 0.784    | 0.767          | 0.771    | 0.600 |          | 0.560     |
|               | (±0.011) | (±0.014)       | (±0.014) |       | (±0.012) | (±0.017)  |
| 1600          |          | 0.747          | 0.742    | 0.580 |          | 0.550     |
0.754
|      | (±0.011) | (±0.013) | (±0.013) |       | (±0.014) | (±0.017) |
| ---- | -------- | -------- | -------- | ----- | -------- | -------- |
| 3200 | 0.727    |          | 0.726    | 0.542 |          | 0.533    |
0.730
|     | (±0.011) | (±0.011) | (±0.012) |     | (±0.014) | (±0.017) |
| --- | -------- | -------- | -------- | --- | -------- | -------- |
Table 2: kNN Classifier accuracy for varying values of k over the embedding
spacesofShuttle,MNISTandFashion-MNISTdatasets. Averageaccuracyscores
are given over a 10-fold or 20-fold cross-validation for each of PCA, Laplacian
Eigenmaps,LargeVis,t-SNEandUMAP.
32

Figure 5: kNN Classifier accuracy for varying values of k over the embedding
spaces of COIL-20 and PenDigits datasets. Accuracy scores are given for each
foldofa10-foldcross-validationforeachofPCA,LaplacianEigenmaps,LargeVis,
t-SNEandUMAP.WenotethatUMAPproducescompetitiveaccuracyscoresto
t-SNEandLargeVisformostcases,andoutperformsbotht-SNEandLargeVisfor
largerk valuesonCOIL-20.
variety of uses cases, so establishing some measure of how stable UMAP
embeddingsare,particularlyundersub-sampling,isofinterest. Inthissub-
sectionwecomparethestabilityundersubsamplingofUMAP,LargeVisand
t-SNE(thethreestochasticdimensionreductiontechniquesconsidered).
To measure the stability of an embedding we make use of the nor-
malized Procrustes distance to measure the distance between two poten-
tiallycomparabledistributions. GiventwodatasetsX = {x ,...,x }and
1 N
Y = {y ,...,y } such that x corresponds to y , we can define the Pro-
1 N i i
custes distance between the datasets d (X,Y) in the following manner.
P
Determine Y(cid:48) = {y (cid:48),...,y (cid:48)} the optimal translation, uniform scaling,
1 N
and rotation of Y that minimizes the squared error (cid:80)N (x −y (cid:48))2, and
i=1 i i
define
(cid:118)
(cid:117) N
(cid:117)(cid:88)
d (X,Y) = (cid:116) (x −y (cid:48))2.
P i i
i=1
Since any measure that makes use of distances in the embedding space is
potentially sensitive to the extent or scale of the embedding, we normal-
ize the data before computing the Procrustes distance by dividing by the
average norm of the embedded dataset. In Figure 7 we visualize the re-
sultsofusingProcrustesalignmentofembeddingofsub-samplesforboth
33

Figure 6: kNN Classifier accuracy for varying values of k over the embedding
spaces of Shuttle, MNIST and Fashion-MNIST datasets. Accuracy scores are
given for each fold of a 10-fold cross-validation for Shuttle, and 20-fold cross-
validation for MNIST and Fashion-MNIST, for each of PCA, Laplacian Eigen-
maps, LargeVis, t-SNE and UMAP. UMAP performs better than the other algo-
rithmsforlargek,particularlyontheShuttledataset. ForFashion-MNISTUMAP
providesslightlypooreraccuracythant-SNEandLargeVisatsmallscales,butis
competitiveatlargerk values.
34

(a)UMAP (b)t-SNE
Figure 7: Procrustes based alignment of a 10% subsample (red) against the full
dataset(blue)fortheflowcytometrydatasetforbothUMAPandt-SNE.
UMAPandt-SNE,demonstratinghowProcrustesdistancecanmeasurethe
stabilityoftheoverallstructureoftheembedding.
Givenameasureofdistancebetweendifferentembeddingswecanex-
amine stability under sub-sampling by considering the normalized Pro-
crustes distance between the embedding of a sub-sample, and the corre-
sponding sub-sample of an embedding of the full dataset. As the size of
the sub-sample increases the average distance per point between the sub-
sampledembeddingsshoulddecrease,potentiallytowardsomeasymptote
of maximal agreement under repeated runs. Ideally this asymptotic value
would be zero error, but for stochastic embeddings such as UMAP and t-
SNEthisisnotachievable.
We performed an empirical comparison of algorithms with respect to
stability using the Flow Cytometry dataset due its large size, interesting
structure, and low ambient dimensionality (aiding runtime performance
for t-SNE). We note that for a dataset this large we found it necessary to
increasethedefaultn_itervaluefort-SNEfrom1000to1500toensurebet-
terconvergence. Whilethishadanimpactontheruntime,itsignificantly
improvedtheProcrustesdistanceresultsbyprovidingmorestableandcon-
sistent embeddings. Figure 8 provides a comparison between UMAP and
t-SNE,demonstratingthatUMAPhassignifcantlymorestableresultsthan
35

t-SNE.Inparticular,aftersub-samplingon5%ofthemilliondatapoints,the
perpointerrorforUMAPwasalreadybelowanyvalueachievedbyt-SNE.
5.4 Computational Performance Comparisons
BenchmarksagainsttherealworlddatasetswereperformedonaMacbook
Pro with a 3.1 GHz Intel Core i7 and 8GB of RAM for Table 3, and on a
server with Intel Xeon E5-2697v4 processors and 512GB of RAM for the
largescalebenchmarkinginSubsections5.4.1,5.4.2,and5.4.3.
For t-SNE we chose MulticoreTSNE [57], which we believe to be the
fastestextantimplementationofBarnes-Hutt-SNEatthistime,evenwhen
runinsinglecoremode. ItshouldbenotedthatMulticoreTSNEisaheav-
ily optimized implementation written in C++ based on Van der Maaten’s
bhtsne[58]code.
As a fast alternative approach to t-SNE we also consider the FIt-SNE
algorithm [37]. We used the reference implementation [36], which, like
MulticoreTNSE is an optimized C++ implementation. We also note that
FIt-SNEmakesuseofmultiplecores.
LargeVis [54] was benchmarked using the reference implementation
[53].Itwasrunwithdefaultparametersincludinguseof8threadsonthe4-
coremachine. Theonlyexceptionsweresmalldatasetswhereweexplicitly
set the -samples parameter to n_samples/100 as per the recommended
valuesinthedocumentationofthereferenceimplementation.
TheIsomap[55]andLaplacianEigenmaps[7]implementationsinscikit-
learn[10]wereused. WesuspecttheLaplacianeigenmapsimplementation
maynotbewelloptimizedforlargedatasetsbutdidnotfindabetterper-
formingimplementationthatprovidedcomparablequalityresults. Isomap
failed to complete for the Shuttle, Fashion-MNIST, MNIST and Google-
News datasets, while Laplacian Eigenmaps failed to run for the Google-
Newsdataset.
To allow a broader range of algorithms to run some of the datasets
wheresubsampledorhadtheirdimensionreducedbyPCA.TheFlowCy-
tometry dataset was benchmarked on a 10% sample and the GoogleNews
was subsampled down to 200,000 data points. Finally, the Mouse scRNA
datasetwasreducedto1,000dimensionsviaPCA.
TimingwereperformedfortheCOIL20[43],COIL100[44],Shuttle[35],
MNIST [32], Fashion-MNIST [63], and GoogleNews [41] datasets. Results
can be seen in Table 3. UMAP consistently performs faster than any of
theotheralgorithmsasidefromontheverysmallPendigitsdataset,where
LaplacianEigenmapsandIsomaphaveasmalledge.
36

Figure8: ComparisonofaverageProcustesdistanceperpointfort-SNE,LargeVis
and UMAP over a variety of sizes of subsamples from the full Flow Cytometry
dataset. UMAPsub-sampleembeddingsareveryclosetothefullembeddingeven
for subsamples of 5% of the full dataset, outperforming the results of t-SNE and
LargeVisevenwhentheyusethefullFlowCytometrydataset.
37

|     |           | UMAP |     | FIt-SNE | t-SNE | LargeVis | Eigenmaps |     |     | Isomap |
| --- | --------- | ---- | --- | ------- | ----- | -------- | --------- | --- | --- | ------ |
|     |           |      | 9s  | 48s     | 17s   | 20s      |           |     |     |        |
|     | PenDigits |      |     |         |       |          |           |     | 2s  | 2s     |
(1797x64)
|     |        |     |     | 75s | 22s | 82s |     |     | 47s | 58s |
| --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     | COIL20 |     | 12s |     |     |     |     |     |     |     |
(1440x16384)
|     |         |     |     | 2681s | 810s | 3197s |     | 3268s |     | 3210s |
| --- | ------- | --- | --- | ----- | ---- | ----- | --- | ----- | --- | ----- |
|     | COIL100 |     | 85s |       |      |       |     |       |     |       |
(7200x49152)
|     | scRNA |     | 28s | 131s | 258s | 377s |     |     | 470s | 923s |
| --- | ----- | --- | --- | ---- | ---- | ---- | --- | --- | ---- | ---- |
(21086x1000)
|     | Shuttle |     | 94s | 108s | 714s | 615s |     |     | 133s | –   |
| --- | ------- | --- | --- | ---- | ---- | ---- | --- | --- | ---- | --- |
(58000x9)
|     |       |     |     | 292s | 1450s | 1298s |     | 40709s |     | –   |
| --- | ----- | --- | --- | ---- | ----- | ----- | --- | ------ | --- | --- |
|     | MNIST |     | 87s |      |       |       |     |        |     |     |
(70000x784)
|     |         |     |     | 278s | 934s | 1173s |     | 6356s |     | –   |
| --- | ------- | --- | --- | ---- | ---- | ----- | --- | ----- | --- | --- |
|     | F-MNIST |     | 65s |      |      |       |     |       |     |     |
(70000x784)
|     | Flow |     | 102s | 164s | 1135s | 1127s |     | 30654s |     | –   |
| --- | ---- | --- | ---- | ---- | ----- | ----- | --- | ------ | --- | --- |
(100000x17)
| GoogleNews |     |     | 361s | 652s | 16906s | 5392s |     |     | –   | –   |
| ---------- | --- | --- | ---- | ---- | ------ | ----- | --- | --- | --- | --- |
(200000x300)
Table3: Runtimeofseveraldimensionreductionalgorithmsonvariousdatasets.
To allow a broader range of algorithms to run some of the datasets where sub-
sampled or had their dimension reduced by PCA. The Flow Cytometry dataset
wasbenchmarkedona10%sampleandtheGoogleNewswassubsampleddown
to 200,000 data points. Finally, the Mouse scRNA dataset was reduced to 1,000
dimensionsviaPCA.Thefastestruntimeforeachdatasethasbeenbolded.
38

5.4.1 ScalingwithEmbeddingDimension
UMAPissignificantlymoreperformantthant-SNE4whenembeddinginto
dimensionslargerthan2. Thisisparticularlyimportantwhentheintention
isto usethelow dimensionalrepresentationfor furthermachinelearning
taskssuchasclusteringoranomalydetectionratherthanmerelyforvisu-
alization. ThecomputationperformanceofUMAPisfarmoreefficientthan
t-SNE, even for very small embedding dimensions of 6 or 8 (see Figure 9).
ThisislargelyduetothefactthatUMAPdoesnotrequireglobalnormali-
sation(sinceitrepresentsdataasafuzzytopologicalstructureratherthan
as a probability distribution). This allows the algorithm to work without
the need for space trees —such as the quad-trees and oct-trees that t-SNE
uses [58]—. Such space trees scale exponentially in dimension, resulting
in t-SNE’s relatively poor scaling with respect to embedding dimension.
By contrast, we see that UMAP consistently scales well in embedding di-
mension,makingthealgorithmpracticalforawiderrangeofapplications
beyondvisualization.
5.4.2 ScalingwithAmbientDimension
Throughacombinationofthelocal-connectivityconstraintandtheapprox-
imatenearestneighborsearch,UMAPcanperformeffectivedimensionre-
ductionevenforveryhighdimensionaldata(seeFigure13foranexample
ofUMAPoperatingdirectlyon1.8milliondimensionaldata).Thisstandsin
contrasttomanyothermanifoldlearningtechniques,includingt-SNEand
LargeVis, for which it is generally recommended to reduce the dimension
withPCAbeforeapplyingthesetechniques(see[59]forexample).
To compare runtime performance scaling with respect to the ambient
dimension of the data we chose to use the Mouse scRNA dataset, which
is high dimensional, but is also amenable to the use of PCA to reduce the
dimension of the data as a pre-processing step without losing too much
of the important structure5. We compare the performance of UMAP, FIt-
SNE,MulticoreTSNE,andLargeVisonPCAreductionsoftheMousescRNA
dataset to varying dimensionalities, and on the original dataset, in Figure
10.
Whilealltheimplementationstestedshowasignificantincreaseinrun-
time with increasing dimension, UMAP is dramatically more efficient for
4ComparisonswereperformedagainstMulticoreTSNEasthecurrentimplementationofFIt-
SNEdoesnotsupportembeddingintoanydimensionlargerthan2.
5IncontrasttoCOIL100,onwhichPCAdestroysmuchofthemanifoldstructure
39

(a)AcomparisonofruntimeforUMAP, (b) Detail of scaling for embedding di-
t-SNEandLargeViswithrespecttoem- mension of six or less. We can see that
bedding dimension on the Pen digits UMAPandLargeVisareessentiallyflat.
dataset. Weseethatt-SNEscalesworse Inpracticetheyappeartoscalelinearly,
than exponentially while UMAP and buttheslopeisessentiallyundetectable
LargeVis scale linearly with a slope so atthisscale.
slighttobeundetectableatthisscale.
Figure 9: Scaling performance with respect to embedding dimension of UMAP,
t-SNEandLargeVisonthePendigitsdataset.
40

Figure 10: Runtime performance scaling of UMAP, t-SNE, FIt-SNE and Largevis
with respect to the ambient dimension of the data. As the ambient dimension
increases beyond a few thousand dimensions the computational cost of t-SNE,
FIt-SNE, and LargeVis all increase dramatically, while UMAP continues to per-
formwellintothetens-of-thousandsofdimensions.
41

largeambientdimensions, easilyscalingtorunontheoriginalunreduced
dataset.Theabilitytorunmanifoldlearningonrawsourcedata,ratherthan
dimensionreduceddatathatmayhavelostimportantmanifoldstructurein
thepre-processing,isasignificantadvantage. Thisadvantagecomesfrom
the local connectivity assumption which ensures good topological repre-
sentation of high dimensional data, particularly with smaller numbers of
nearneighbors,andtheefficiencyoftheNN-Descentalgorithmforapprox-
imatenearestneighborsearcheveninhighdimensions.
SinceUMAPscaleswellwithambientdimensionthepythonimplemen-
tationalsosupportsinputinsparsematrixformat,allowingscalingtoex-
tremely high dimensional data, such as the integer data shown in Figures
13and14.
5.4.3 ScalingwiththeNumberofSamples
FordatasetsizeperformancecomparisonswechosetocompareUMAPwith
FIt-SNE [37], a version of t-SNE that uses approximate nearest neighbor
searchandaFourierinterpolationoptimisationapproach; MulticoreTSNE
[57], which we believe to be the fastest extant implementation of Barnes-
Hutt-SNE;andLargeVis[54]. ItshouldbenotedthatFIt-SNE,MulticoreT-
SNE, and LargeVis are all heavily optimized implementations written in
C++. IncontrastourUMAPimplementationwaswritteninPython—mak-
ing use of the numba [31] library for performance. MulticoreTSNE and
LargeVis were run in single threaded mode to make fair comparisons to
oursinglethreadedUMAPimplementation.
WebenchmarkedallfourimplementationsusingsubsamplesoftheGoogle-
Newsdataset. TheresultscanbeseeninFigure11. Thisdemonstratesthat
UMAP has superior scaling performance in comparison to Barnes-Hut t-
SNE, even when Barnes-Hut t-SNE is given multiple cores. Asymptotic
scaling of UMAPis comparable to thatof FIt-SNE (and LargeVis). Onthis
datasetUMAPdemonstratedsomewhatfasterabsoluteperformancecom-
paredtoFIt-SNE,andwasdramaticallyfasterthanLargeVis.
TheUMAPembeddingofthefullGoogleNewsdatasetof3millionword
vectors,asseeninFigure12,wascompletedinaround200minutes,ascom-
pared with several days required for MulticoreTSNE, even using multiple
cores.
ToscaleevenfurtherwewereinspiredbytheworkofJohnWilliamson
on embedding integers [61], as represented by (sparse) binary vectors of
their prime divisibility. This allows the generation of arbitrarily large, ex-
tremelyhighdimensiondatasetsthatstillhavemeaningfulstructuretobe
42

Figure 11: Runtime performance scaling of t-SNE and UMAP on various sized
sub-samples of the full Google News dataset. The lower t-SNE line is the wall
clockruntimeforMulticoret-SNEusing8cores.
43

Figure12: Visualizationofthefull3millionwordvectorsfromtheGoogleNews
datasetasembeddedbyUMAP.
44

explored. In Figures 13 and 14 we show an embedding of 30,000,000 data
samples from an ambient space of approximately 1.8 million dimensions.
This computation took approximately 2 weeks on a large memory SMP.
Note that despite the high ambient dimension, and vast amount of data,
UMAPisstillabletofindanddisplayinterestingstructure. InFigure15we
show local regions of the embedding, demonstrating the fine detail struc-
turethatwascaptured.
6 Weaknesses
WhilewebelieveUMAPtobeaveryeffectivealgorithmforbothvisualiza-
tion and dimension reduction, most algorithms must make trade-offs and
UMAPisnoexception. Inthissectionwewillbrieflydiscussthoseareasor
usecaseswhereUMAPislesseffective,andsuggestpotentialalternatives.
Foranumberofusecasestheinterpretabilityofthereduceddimension
resultsisofcriticalimportance. Similarlytomostnon-lineardimensionre-
duction techniques (including t-SNE and Isomap), UMAP lacks the strong
interpretability of Principal Component Analysis (PCA) and related tech-
niquessuchaNon-NegativeMatrixFactorization(NMF).Inparticularthe
dimensions of the UMAP embedding space have no specific meaning, un-
like PCA where the dimensions are the directions of greatest variance in
thesourcedata.Furthermore,sinceUMAPisbasedonthedistancebetween
observationsratherthanthesourcefeatures,itdoesnothaveanequivalent
of factor loadings that linear techniques such as PCA, or Factor Analysis
can provide. If strong interpretability is critical we therefore recommend
lineartechniquessuchasPCA,NMForpLSA.
One of the core assumptions of UMAP is that there exists manifold
structure in the data. Because of this UMAP can tend to find manifold
structurewithinthenoiseofadataset–similartothewaythehumanmind
finds structured constellations among the stars. As more data is sampled
theamountofstructureevidentfromnoisewilltendtodecreaseandUMAP
becomesmorerobust,howevercaremustbetakenwithsmallsamplesizes
of noisy data, or data with only large scale manifold structure. Detecting
whenaspuriousembeddinghasoccurredisatopicoffurtherresearch.
UMAP is derived from the axiom that local distance is of more im-
portance than long range distances (similar to techniques like t-SNE and
LargeVis). UMAP therefore concerns itself primarily with accurately rep-
resenting local structure. While we believe that UMAP can capture more
global structure than these other techniques, it remains true that if global
45

Figure 13: Visualization of 30,000,000 integers as represented by binary vectors
ofprimedivisibility,coloredbydensityofpoints.
46

Figure 14: Visualization of 30,000,000 integers as represented by binary vectors
ofprimedivisibility,coloredbyintegervalueofthepoint(largervaluesaregreen
oryellow,smallervaluesareblueorpurple).
47

(a)Upperrightspiral (b)Lowerrightspiralandstarbursts
(c)Centralcloud
Figure 15: Zooming in on various regions of the integer embedding reveals fur-
therlayersoffinestructurehavebeenpreserved.
48

structureisofprimaryinterestthenUMAPmaynotbethebestchoicefor
| dimension                                     | reduction.    | Multi-dimensional |        |       | scaling | specifically     |           | seeks     | to pre- |
| --------------------------------------------- | ------------- | ----------------- | ------ | ----- | ------- | ---------------- | --------- | --------- | ------- |
| serve the                                     | full distance | matrix            | of the | data, | and as  | such             | is a good | candidate |         |
| whenallscalesofstructureareofequalimportance. |               |                   |        |       |         | PHATE[42]isagood |           |           |         |
exampleofahybridapproachthatbeginswithlocalstructureinformation
andmakesuseofMDStoattempttopreservelongscaledistancesaswell.It
shouldbenotedthatthesetechniquesaremorecomputationallyintensive
andthusrelyonlandmarkingapproachesforscalability.
ItshouldalsobenotedthatasignificantcontributortoUMAP’srelative
globalstructurepreservationisderivedfromtheLaplacianEigenmapsini-
| tialization(which,inturn,followedfromthetheoreticalfoundations). |         |          |                 |             |         |              |                |             | This |
| ---------------------------------------------------------------- | ------- | -------- | --------------- | ----------- | ------- | ------------ | -------------- | ----------- | ---- |
| was noted                                                        | in, for | example, | [29].           | The authors |         | of that      | paper          | demonstrate |      |
| that t-SNE,                                                      | with    | similar  | initialization, | can         | perform | equivalently |                | to          | UMAP |
| inaparticularmeasureofglobalstructurepreservation.               |         |          |                 |             |         |              | However,theob- |             |      |
jectivefunctionderivedforUMAP(cross-entropy)issignificantlydifferent
fromthatoft-SNE(KL-divergence),inhowitpenalizesfailurestopreserve
non-localandglobalstructure,andisalsoasignificantcontributor6.
Itisworthnotingthat,incombiningthelocalsimplicialsetstructures,
| pure nearest                         | neighbor   | structure     | in  | the high   | dimensional                  |           | space             | is  | not ex- |
| ------------------------------------ | ---------- | ------------- | --- | ---------- | ---------------------------- | --------- | ----------------- | --- | ------- |
| plicitly                             | preserved. | In particular | it  | introduces |                              | so called | ”reverse-nearest- |     |         |
| neighbors”intotheclassicalknn-graph. |            |               |     |            | This,combinedwiththefactthat |           |                   |     |         |
UMAPispreservingtopologyratherthanpuremetricstructures,meanthat
UMAPwillnotperformaswellassomemethodsonqualitymeasuresbased
| on metric | structure | preservation | –   | particularly |     | methods, | such | as  | MDS – |
| --------- | --------- | ------------ | --- | ------------ | --- | -------- | ---- | --- | ----- |
whichareexplicitlydesignedtooptimizemetricstructurepreservation.
UMAPattemptstodiscoveramanifoldonwhichyourdataisuniformly
| distributed. | Ifyouhavestrongconfidenceintheambientdistancesofyour |     |     |     |     |     |     |     |     |
| ------------ | ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
datayoushouldmakeuseofatechniquethatexplicitlyattemptstopreserve
thesedistances.Forexampleifyourdataconsistedofaveryloosestructure
| in one | area of your | ambient | space   | and a | very      | dense | structure | in another |      |
| ------ | ------------ | ------- | ------- | ----- | --------- | ----- | --------- | ---------- | ---- |
| region | region UMAP  | would   | attempt | to    | put these | local | areas     | on an      | even |
footing.
Finally,toimprovethecomputationalefficiencyofthealgorithmanum-
| ber of  | approximations | are   | made.    | This can | have    | an impact |     | on the     | results |
| ------- | -------------- | ----- | -------- | -------- | ------- | --------- | --- | ---------- | ------- |
| of UMAP | for small      | (less | than 500 | samples) | dataset | sizes.    | In  | particular | the     |
useofapproximatenearestneighboralgorithms,andthenegativesampling
| usedinoptimization,canresultinsuboptimalembeddings. |     |     |     |     |     |     | Forthisreason |     |     |
| --------------------------------------------------- | --- | --- | --- | --- | --- | --- | ------------- | --- | --- |
6TheauthorswouldliketothankNikolayOskolkovforhisarticle(tSNEvs. UMAP:Global
Structure)whichdoesanexcellentjobofhighlightingtheseaspectsfromanempiricalandthe-
oreticalbasis.
49

weencourageuserstotakecarewithparticularlysmalldatasets. Aslower
butexactimplementationofUMAPforsmalldatasetsisafutureproject.
7 Future Work
Havingestablishedbothrelevantmathematicaltheoryandaconcreteim-
plementation,therestillremainssignificantscopeforfuturedevelopments
ofUMAP.
A comprehensive empirical study which examines the impact of the
variousalgorithmiccomponents,choices,andhyper-parametersoftheal-
gorithm would be beneficial. While the structure and choices of the algo-
rithmpresentedwerederivedfromourfoundationalmathematicalframe-
work, examining the impacts that these choices have on practical results
wouldbeenlighteningandasignificantcontributiontotheliterature.
Asnotedintheweaknessessectionthereisagreatdealofuncertainty
surrounding the preservation of global structure among the field of man-
ifold learning algorithms. In particular this is hampered by the lack clear
objective measures, or even definitions, of global structure preservation.
While some metrics exist, they are not comprehensive, and are often spe-
cific to various downstream tasks. A systematic study of both metrics of
non-local and global structure preservation, and performance of various
manifoldlearningalgorithmswithrespecttothem,wouldbeofgreatben-
efit. WebelievethiswouldaidinbetterunderstandingUMAP’ssuccessin
variousdownstreamtasks.
MakinguseofthefuzzysimplicialsetrepresentationofdataUMAPcan
potentiallybeextendedtosupport(semi-)superviseddimensionreduction,
anddimensionreductionfordatasetswithheterogeneousdatatypes. Each
datatype(orpredictionvariablesinthesupervisedcase)canbeseenasan
alternative view of the underlying structure, each with a different associ-
atedmetric–forexamplecategoricaldatamayuseJaccardorDicedistance,
whileordinaldatamightuseManhattandistance.Eachviewandmetriccan
beusedtoindependentlygeneratefuzzysimplicialsets,whichcanthenbe
intersected together to create a single fuzzy simplicial set for embedding.
ExtendingUMAPtoworkwithmixeddatatypeswouldvastlyincreasethe
rangeofdatasetstowhichitcanbeapplied.Usecasesfor(semi-)supervised
dimensionreductionincludesemi-supervisedclustering,andinteractivela-
bellingtools.
ThecomputationalframeworkestablishedforUMAPallowsforthepo-
tential development of techniques to add new unseen data points into an
50

| existing  | embedding, | and    | to generate |        | high dimensional |     | representations |             | of  |
| --------- | ---------- | ------ | ----------- | ------ | ---------------- | --- | --------------- | ----------- | --- |
| arbitrary | points     | in the | embedded    | space. | Furthermore,     |     | the             | combination | of  |
supervisionandtheadditionofnewsamplestoanexistingembeddingpro-
| vides avenues    |     | for metric | learning. | The  | addition | of   | new samples  |             | to an ex- |
| ---------------- | --- | ---------- | --------- | ---- | -------- | ---- | ------------ | ----------- | --------- |
| isting embedding |     | would      | allow     | UMAP | to be    | used | as a feature | engineering |           |
toolaspartofageneralmachinelearningpipelineforeitherclusteringor
| classification |     | tasks. Pulling | points | back | to  | the original | high | dimensional |     |
| -------------- | --- | -------------- | ------ | ---- | --- | ------------ | ---- | ----------- | --- |
spacefromtheembeddedspacewouldpotentiallyallowUMAPtobeused
| asagenerativemodelsimilartosomeusecasesforautoencoders. |     |     |     |     |     |     |     |     | Finally, |
| ------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | -------- |
therearemanyusecasesformetriclearning;see[64]or[8]forexample.
Therealsoremainssignificantscopetodeveloptechniquestobothde-
tectandmitigateagainstpotentiallyspuriousembeddings,particularlyfor
| small data  | cases. | The addition |                 | of such | techniques |           | would    | make | UMAP far |
| ----------- | ------ | ------------ | --------------- | ------- | ---------- | --------- | -------- | ---- | -------- |
| more robust |        | as a tool    | for exploratory |         | data       | analysis, | a common |      | use case |
whenreducingtotwodimensionsforvisualizationpurposes.
Experimentalversionsofsomeofthisworkarealreadyavailableinthe
referencedimplementations.
8 Conclusions
Wehavedevelopedageneralpurposedimensionreductiontechniquethat
| is grounded    |      | in strong                                           | mathematical    |                  | foundations. |      | The     | algorithm     | imple-   |
| -------------- | ---- | --------------------------------------------------- | --------------- | ---------------- | ------------ | ---- | ------- | ------------- | -------- |
| menting        | this | technique                                           | is demonstrably |                  | faster       | than | t-SNE   | and           | provides |
| betterscaling. |      | Thisallowsustogeneratehighqualityembeddingsoflarger |                 |                  |              |      |         |               |          |
| data sets      | than | had previously                                      |                 | been attainable. |              | The  | use and | effectiveness |          |
ofUMAPinvariousscientificfieldsdemonstratesthestrengthofthealgo-
rithm.
TheauthorswouldliketothankColinWeir,Rick
Acknowledgements
Jardine,BrendanFong,DavidSpivakandDmitryKobakfordiscussionand
usefulcommentaryonvariousdraftsofthispaper.
| A Proof |     | of Lemma |     | 1   |     |     |     |     |     |
| ------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
Let(M,g)beaRiemannianmanifoldinanambientRn,andlet
Lemma1.
| p ∈ M | beapoint. | Ifg | islocallyconstantaboutpinanopenneighbourhood |     |     |     |     |     |     |
| ----- | --------- | --- | -------------------------------------------- | --- | --- | --- | --- | --- | --- |
U suchthatgisaconstantdiagonalmatrixinambientcoordinates,thenina
πn/2
| ballB ⊆ | U centeredatpwithvolume |     |     |     |     | withrespecttog,thegeodesic |     |     |     |
| ------- | ----------------------- | --- | --- | --- | --- | -------------------------- | --- | --- | --- |
Γ(n/2+1)
51

1
| distancefromptoanypointq |     |     |     | ∈ B is | dRn | (p,q),whereristheradiusofthe |     |     |     |
| ------------------------ | --- | --- | --- | ------ | --- | ---------------------------- | --- | --- | --- |
r
| ballintheambientspaceanddRn |                           |           |     | istheexistingmetricontheambientspace. |                  |     |         |         |          |
| --------------------------- | ------------------------- | --------- | --- | ------------------------------------- | ---------------- | --- | ------- | ------- | -------- |
| Proof.                      | Let                       | x1,...,xn | be  | the coordinate                        | system           |     | for the | ambient | space. A |
| ballB                       | inMunderRiemannianmetricg |           |     |                                       | hasvolumegivenby |     |         |         |          |
(cid:90)
(cid:112) det(g)dx1∧···∧dxn.
B
andhence(cid:112)
| IfB                                     | iscontainedinU,theng |           |             | isconstantinB |     |                   |        | det(g)iscon- |     |
| --------------------------------------- | -------------------- | --------- | ----------- | ------------- | --- | ----------------- | ------ | ------------ | --- |
| stantandcanbebroughtoutsidetheintegral. |                      |           |             |               |     | Thus,thevolumeofB |        |              | is  |
|                                         |                      |           | (cid:90)    |               |     |                   | πn/2rn |              |     |
|                                         |                      | (cid:112) |             |               |     | (cid:112)         |        |              |     |
|                                         |                      | det(g)    | dx1∧...∧dxn |               | =   | det(g)            |        | ,            |     |
Γ(n/2+1)
B
| wherer      |     | istheradiusoftheballintheambientRn. |                              |     |     |     | Ifwefixthevolumeof |     |     |
| ----------- | --- | ----------------------------------- | ---------------------------- | --- | --- | --- | ------------------ | --- | --- |
| theballtobe |     | πn/2                                | wearriveattherequirementthat |     |     |     |                    |     |     |
Γ(n/2+1)
1
|     |     |     |     | det(g) | =   | .   |     |     |     |
| --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- |
r2n
| Now,sinceg |     | isassumedtobediagonalwithconstantentrieswecansolve |     |     |     |     |     |     |     |
| ---------- | --- | -------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
forg itselfas

|     |     |     |     | 1   | ifi | = j, |     |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- |
r2
(2)
|                                               |     |     |     | g ij = |           |     | .   |               |     |
| --------------------------------------------- | --- | --- | --- | ------ | --------- | --- | --- | ------------- | --- |
|                                               |     |     |     | 0     | otherwise |     |     |               |     |
| ThegeodesicdistanceonMundergfromptoq(wherep,q |     |     |     |        |           |     |     | ∈ B)isdefined |     |
as
(cid:90)
|     |     |     |     | b (cid:112) |                   |     |     |     |     |
| --- | --- | --- | --- | ----------- | ----------------- | --- | --- | --- | --- |
|     |     |     |     | inf         | g(c˙(t),c˙(t))dt, |     |     |     |     |
c∈C
a
| where |      | is the class   | of  | smooth curves        |     | on   | such that |            | and     |
| ----- | ---- | -------------- | --- | -------------------- | --- | ---- | --------- | ---------- | ------- |
|       | C    |                |     |                      | c   | M    |           | c(a)       | = p     |
| c(b)  | = q, | and c˙ denotes |     | the first derivative |     | of c | on M.     | Given that | g is as |
definedin(2)weseethatthiscanbesimplifiedto
(cid:90) b
|     |     |     |     | 1   | (cid:112)                        |     |     |     |     |
| --- | --- | --- | --- | --- | -------------------------------- | --- | --- | --- | --- |
|     |     |     |     | inf | (cid:104) c˙(t),c˙(t)(cid:105)dt |     |     |     |     |
r c∈C
a
(cid:90)
|     |     |     |     | 1 b |                                          |     |     |     | (3) |
| --- | --- | --- | --- | --- | ---------------------------------------- | --- | --- | --- | --- |
|     |     |     | =   | inf | (cid:104)(cid:107)c˙(t),c˙(t)(cid:107)dt |     |     |     |     |
r c∈C
a
1
= dRn (p,q).
r
52

| B         | ProofthatFinRealandFinSing |                    |                                                    |     |             |                      | areadjoint |     |     |     |
| --------- | -------------------------- | ------------------ | -------------------------------------------------- | --- | ----------- | -------------------- | ---------- | --- | --- | --- |
| Theorem2. |                            | ThefunctorsFinReal |                                                    |     | : Fin-sFuzz | → FinEPMetandFinSing |            |     |     | :   |
| FinEPMet  |                            | →                  | Fin-sFuzzformanadjunctionwithFinRealtheleftadjoint |     |             |                      |            |     |     |     |
andFinSingtherightadjoint.
| Proof.             | The | adjunction | is              | evident | by construction, |            | but can    | be made | more |     |
| ------------------ | --- | ---------- | --------------- | ------- | ---------------- | ---------- | ---------- | ------- | ---- | --- |
| explicitasfollows. |     |            | DefineafunctorF |         |                  |            | FinEPMetby |         |      |     |
|                    |     |            |                 |         | : ∆×I            | →          |            |         |      |     |
|                    |     |            | F([n],[0,a))    |         | = ({x ,x         | ,...,x },d | ),         |         |      |     |
|                    |     |            |                 |         | 1 2              | n          | a          |         |      |     |
where

|                                  |            |     |               |     | −log(a)      | ifi (cid:54)=     | j,  |     |     |     |
| -------------------------------- | ---------- | --- | ------------- | --- | ------------- | ----------------- | --- | --- | --- | --- |
|                                  |            |     | d (x ,x       | ) = |               |                   | .   |     |     |     |
|                                  |            |     | a i           | j   |               |                   |     |     |     |     |
|                                  |            |     |               |     | 0            | otherwise         |     |     |     |     |
| NowFinSingcanbedefinedintermsofF |            |     |               |     |               | as                |     |     |     |     |
|                                  | FinSing(Y) |     | : ([n],[0,a)) |     | (cid:55)→ hom | (F([n],[0,a)),Y). |     |     |     |     |
FinEPMet
| where            | the | face       | maps                                           | are given | by pre-composition |          | with           | Fdi, | and sim- |     |
| ---------------- | --- | ---------- | ---------------------------------------------- | --------- | ------------------ | -------- | -------------- | ---- | -------- | --- |
|                  |     |            | d i                                            |           |                    |          |                |      |          |     |
| ilarly           | for | degeneracy | maps,                                          | at        | any given          | value of | a. Furthermore |      | post-    |     |
| compositionwithF |     |            | level-wiseforeachadefinesmapsoffuzzysimplicial |           |                    |          |                |      |          |     |
setsmakingFinSingafunctor.
|     | We now | construct | FinReal |     | as the left | Kan extension |     | of F along |     | the |
| --- | ------ | --------- | ------- | --- | ----------- | ------------- | --- | ---------- | --- | --- |
Yonedaembedding:
Fin(cid:56)(cid:56) -sFuzz
|     |     |     |     | y   |     | FinReal |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------- | --- | --- | --- | --- |
(cid:43) (cid:11)
(cid:40)(cid:40)
(cid:47)(cid:47)
|     |     |     | ∆×I |     |     | FinEPMet |     |     |     |     |
| --- | --- | --- | --- | --- | --- | -------- | --- | --- | --- | --- |
F
ExplicitlythisresultsinadefinitionofFinRealatafuzzysimplicialsetX
asacolimit:
|     |     |     | FinReal(X) |     | = colim | F([n]). |     |     |     |     |
| --- | --- | --- | ---------- | --- | ------- | ------- | --- | --- | --- | --- |
y([n],[0,a))→X
Further,itfollowsfromtheYonedalemmathatFinReal(∆n ) ∼ = F([n],[0,a)),
<a
| and                                                        | hence | this | definition | as a | left Kan extension | agrees | with | Definition |       | 7,  |
| ---------------------------------------------------------- | ----- | ---- | ---------- | ---- | ------------------ | ------ | ---- | ---------- | ----- | --- |
| andthedefinitionofFinSingaboveagreeswiththatofDefinition8. |       |      |            |      |                    |        |      |            | Tosee |     |
thatFinRealandFinSingareadjointwenotethat
|     |           | (∆n |              |     | ∼ FinSing(Y)n |     |                  |     |     |     |
| --- | --------- | --- | ------------ | --- | ------------- | --- | ---------------- | --- | --- | --- |
| hom | Fin-sFuzz |     | ,FinSing(Y)) |     | =             |     |                  |     |     |     |
|     |           |     | <a           |     |               | <a  |                  |     |     |     |
|     |           |     |              |     | = hom         |     | (F([n],[0,a)),Y) |     |     |     |
FinEPMet
|     |     |     |     |     | ∼ = hom  |     | (FinReal(∆n |     | ),Y)). |     |
| --- | --- | --- | --- | --- | -------- | --- | ----------- | --- | ------ | --- |
|     |     |     |     |     | FinEPMet |     |             | <a  |        |     |
(4)
53

The first isomorphism follows from the Yoneda lemma, the equality is by
construction,andthefinalisomorphismfollowsbyanotherapplicationof
theYonedalemma. Sinceeverysimplicialsetcanbecanonicallyexpressed
asacolimitofstandardsimplicesandFinRealcommuteswithcolimits(as
it was definedvia a colimit formula), itfollows thatFinRealis completely
determined by its image on standard simplices. As a result the isomor-
phismofequation(4)extendstotherequiredisomorphismdemonstrating
theadjunction.
C From t-SNE to UMAP
As an aid to implementation of UMAP and to illuminate the algorithmic
similarities with t-SNE and LargeVis, here we review the main equations
usedinthosemethods,andthenpresenttheequivalentUMAPexpressions
inanotationwhichmaybemorefamiliartousersofthoseothermethods.
In what follows we are concerned with defining similarities between
two objects i and j in the high dimensional input space X and low di-
mensional embedded space Y. These are normalized and symmetrized in
various ways. In a typical implementation, these pair-wise quantities are
stored and manipulated as (potentially sparse) matrices. Quantities with
the subscript ij are symmetric, i.e. v = v . Extending the conditional
ij ji
probabilitynotationusedint-SNE,j | iindicatesanasymmetricsimilarity,
i.e. v (cid:54)= v .
j|i i|j
t-SNEdefinesinputprobabilitiesinthreestages. First,foreachpairof
points,iandj,inX,apair-wisesimilarity,v ,iscalculated,Gaussianwith
ij
respecttotheEuclideandistancebetweenx andx :
i j
v = exp(−(cid:107)x −x (cid:107)2/2σ2) (5)
j|i i j 2 i
whereσ2 isthevarianceoftheGaussian.
i
Second, the similarities are converted into N conditional probability
distributionsbynormalization:
v
p = j|i (6)
j|i (cid:80) v
k(cid:54)=i k|i
σ ischosenbysearchingforavaluesuchthattheperplexityoftheproba-
i
bilitydistributionp matchesauser-specifiedvalue.
·|i
Third,theseprobabilitydistributionsaresymmetrizedandthenfurther
normalizedovertheentirematrixofvaluestogiveajointprobabilitydis-
tribution:
54

p +p
p = j|i i|j (7)
ij
2N
Wenotethatthisisaheuristicdefinitionandnotinaccordancewithstan-
dardrelationshipbetweenconditionalandjointprobabilitiesthatwouldbe
expectedunderprobabilitysemanticsusuallyusedtodescribet-SNE.
Similarities between pairs of points in the output space Y are defined
using a Student t-distribution with one degree of freedom on the squared
Euclideandistance:
(cid:16) (cid:17)−1
w = 1+(cid:107)y −y (cid:107)2 (8)
ij i j 2
followedbythematrix-wisenormalization,toformq :
ij
w
q = ij (9)
ij (cid:80)
w
k(cid:54)=l kl
Thet-SNEcostistheKullback-Leiblerdivergencebetweenthetwoproba-
bilitydistributions:
C = (cid:88) p log p ij (10)
t−SNE ij
q
ij
i(cid:54)=j
thiscanbeexpandedintoconstantandnon-constantcontributions:
(cid:88)
C = p logp −p logq (11)
t−SNE ij ij ij ij
i(cid:54)=j
Becausebothp andq requirecalculationsoverallpairsofpoints,im-
ij ij
provingtheefficiencyoft-SNEalgorithmshasinvolvedseparatestrategies
forapproximatingthesequantities. Similaritiesinthehighdimensionsare
effectively zero outside of the nearest neighbors of each point due to the
calibrationofthep valuestoreproduceadesiredperplexity.Thereforean
j|i
approximationusedinBarnes-Hutt-SNEistoonlycalculatev fornnear-
j|i
estneighborsofi,wherenisamultipleoftheuser-selectedperplexityand
toassumev = 0forallotherj. Becausethelowdimensionalcoordinates
j|i
change with each iteration, a different approach is used to approximate
q . InBarnes-Hutt-SNEandrelatedmethodsthisusuallyinvolvesgroup-
ij
ing together points whose contributions can be approximated as a single
point.
A further heuristic algorithm optimization technique employed by t-
SNEimplementationsistheuseofearlyexaggerationwhere,forsomenum-
berofinitialiterations,thep aremultipliedbysomeconstantgreaterthan
ij
55

1.0 (usually 12.0). In theoretical analyses of t-SNE such as [38] results are
obtained only under an early exaggeration regimen with either large con-
stant(oforderofthenumberofsamples),orinthelimitofinfiniteexagger-
ation. Furtherpaperssuchas[37],and[28],suggesttheoptionofusingex-
aggerationforalliterationsratherthanjustearlyones,anddemonstratethe
utilityofthis. Theeffectivenessoftheseanalysesandpracticalapproaches
suggeststhatKL-divergenceasameasurebetweenprobabilitydistributions
isnotwhatmakesthet-SNEalgorithmwork,since,underexaggeration,the
p are manifestly not a probability distribution. This is another example
ij
of the probability semantics used to describe t-SNE are primarily descrip-
tive rather than foundational. None the less, t-SNE is highly effective and
clearlyproducesusefulresultsonaverywidevarietyoftasks.
LargeVis uses a similar approach to Barnes-Hut t-SNE when approxi-
matingp ,butfurtherimprovesefficiencybyonlyrequiringapproximate
ij
nearest neighbors for each point. For the low dimensional coordinates,
it abandons normalization of w entirely. Rather than use the Kullback-
ij
Leibler divergence, it optimizes a likelihood function, and hence is maxi-
mized,notminimized:
(cid:88) (cid:88)
C = p logw +γ log(1−w ) (12)
LV ij ij ij
i(cid:54)=j i(cid:54)=j
p and w are defined as in Barnes-Hut t-SNE (apart from the use of
ij ij
approximatenearestneighborsforp ,andthefactthat,inimplementation,
ij
LargeVisdoesnotnormalizethep byN)andγ isauser-chosenpositive
ij
constantwhichweightsthestrengthofthetherepulsivecontributions(sec-
ondterm)relativetotheattractivecontribution(firstterm). Notealsothat
thefirsttermresemblestheoptimizablepartoftheKullback-Leiblerdiver-
gencebutusingw insteadofq .Abandoningcalculationofq isacrucial
ij ij ij
change,becausetheLargeViscostfunctionisamenabletooptimizationvia
stochasticgradientdescent.
Ignoring specific definitions of v and w , the UMAP cost function,
ij ij
thecrossentropy,is:
(cid:18) (cid:19) (cid:18) (cid:19)
C = (cid:88) v log v ij +(1−v )log 1−v ij (13)
UMAP ij ij
w 1−w
ij ij
i(cid:54)=j
LiketheKullback-Leiblerdivergence,thiscanbearrangedintotwocon-
stantcontributions(thosecontainingv only)andtwooptimizablecontri-
ij
butions(containingw ):
ij
56

(cid:88)
|          | C    |         | =            | v logv | +(1−v       |      | )log(1−v      | )         |            |
| -------- | ---- | ------- | ------------ | ------ | ----------- | ---- | ------------- | --------- | ---------- |
|          |      | UMAP    |              | ij     | ij          | ij   |               | ij        |            |
|          |      |         | i(cid:54)=j  |        |             |      |               |           | (14)       |
|          |      |         | −v           | logw   | −(1−v       |      | )log(1−w      | )         |            |
|          |      |         |              | ij     | ij          | ij   |               | ij        |            |
| Ignoring |      | the two | constant     | terms, | the         | UMAP | cost function |           | has a very |
| similar  | form | to that | of LargeVis, |        | but without | a    | term          | to weight | the re-    |
γ
pulsivecomponentofthecostfunction,andwithoutrequiringmatrix-wise
| normalizationinthehighdimensionalspace. |     |     |     |     |     | ThecostfunctionforUMAP |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | ---------------------- | --- | --- | --- |
canthereforebeoptimized(inthiscase,minimized)withstochasticgradi-
entdescentinthesamewayasLargeVis.
AlthoughtheabovediscussionplacesUMAPinthesamefamilyofmeth-
| odsast-SNEandLargeVis,itdoesnotusethesamedefinitionsforv |     |     |     |     |     |     |     |     | and |
| -------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ij
. Usingthenotationestablishedabove,wenowprovidetheequivalent
w ij
| expressionsfortheUMAPsimilarities. |     |                                                     |     |     | Inthehighdimensionalspace, |     |     |     | the |
| ---------------------------------- | --- | --------------------------------------------------- | --- | --- | -------------------------- | --- | --- | --- | --- |
| similaritiesv                      |     | arethelocalfuzzysimplicialsetmemberships,basedonthe |     |     |                            |     |     |     |     |
j|i
smoothnearestneighborsdistances:
|                  |     |     | v =                                          | exp[(−d(x | ,x  | )−ρ | )/σ ] |     | (15) |
| ---------------- | --- | --- | -------------------------------------------- | --------- | --- | --- | ----- | --- | ---- |
|                  |     |     | j|i                                          |           | i   | j   | i i   |     |      |
| AswithLargeVis,v |     |     | iscalculatedonlyfornapproximatenearestneigh- |           |     |     |       |     |      |
j|i
| bors and                               | v   | = 0 for | all other                                   | j.  | d(x ,x | ) is the | distance           | between | x and |
| -------------------------------------- | --- | ------- | ------------------------------------------- | --- | ------ | -------- | ------------------ | ------- | ----- |
|                                        | j|i |         |                                             |     | i      | j        |                    |         | i     |
| ,whichUMAPdoesnotrequiretobeEuclidean. |     |         |                                             |     |        |          | isthedistancetothe |         |       |
| x j                                    |     |         |                                             |     |        |          | ρ i                |         |       |
| nearestneighborofi.                    |     |         | σ isthenormalizingfactor,whichischosenbyAl- |     |        |          |                    |         |       |
i
gorithm3andplaysasimilarroletotheperplexity-basedcalibrationofσ
i
| int-SNE.Calculationofv |     |     |     | withEquation15correspondstoAlgorithm2. |     |     |     |     |     |
| ---------------------- | --- | --- | --- | -------------------------------------- | --- | --- | --- | --- | --- |
j|i
Symmetrizationiscarriedoutbyfuzzysetunionusingtheprobabilistic
t-conormandcanbeexpressedas:
|                                                    |     |     |      | (cid:0) |     | (cid:1) |     |              | (16) |
| -------------------------------------------------- | --- | --- | ---- | ------- | --- | ------- | --- | ------------ | ---- |
|                                                    |     |     | v ij | = v     | +v  | −v v    |     |              |      |
|                                                    |     |     |      | j|i     | i|j | j|i     | i|j |              |      |
| Equation16correspondstoformingtop-repinAlgorithm1. |     |     |      |         |     |         |     | Unliket-SNE, |      |
furthernormalizationisnotcarriedout.
Thelowdimensionalsimilaritiesaregivenby:
|       |       |                    |     | (cid:16)      |     |             | (cid:17)−1    |     |             |
| ----- | ----- | ------------------ | --- | ------------- | --- | ----------- | ------------- | --- | ----------- |
|       |       |                    |     |               |     | (cid:107)2b |               |     | (17)        |
|       |       |                    | w = | 1+a(cid:107)y |     | −y          |               |     |             |
|       |       |                    | ij  |               | i   | j 2         |               |     |             |
| where | a and | b are user-defined |     | positive      |     | values.     | The procedure |     | for finding |
themisgiveninDefinition11.Useofthisprocedurewiththedefaultvalues
| intheUMAPimplementationresultsina |     |                                                |     |     |     | 1.929andb |     | 0.7915. | Setting |
| --------------------------------- | --- | ---------------------------------------------- | --- | --- | --- | --------- | --- | ------- | ------- |
|                                   |     |                                                |     |     |     | ≈         |     | ≈       |         |
| a = 1andb                         | =   | 1resultsintheStudentt-distributionusedint-SNE. |     |     |     |           |     |         |         |
57

References
| [1] EAlpaydinandFevziAlimoglu.                         |     |           |                                   |     | Pen-basedrecognitionofhandwrit- |     |                 |            |     |
| ------------------------------------------------------ | --- | --------- | --------------------------------- | --- | ------------------------------- | --- | --------------- | ---------- | --- |
| ten digits                                             |     | data set. | university                        |     | of california,                  |     | irvine. Machine | Learning   |     |
| Repository.Irvine:                                     |     |           | UniversityofCalifornia,4(2),1998. |     |                                 |     |                 |            |     |
| [2] FrederikOtzenBagger,SavvasKinalis,andNicolasRapin. |     |           |                                   |     |                                 |     |                 | Bloodspot: |     |
adatabaseofhealthyandmalignanthaematopoiesisupdatedwithpu-
rifiedandsinglecellmrnasequencingprofiles.NucleicAcidsResearch,
2018.
| [3] MichaelBarr. |     | Fuzzysettheoryandtopostheory. |     |     |     |     | Canad.Math.Bull, |     |     |
| ---------------- | --- | ----------------------------- | --- | --- | --- | --- | ---------------- | --- | --- |
29(4):501–508,1986.
| [4] Etienne                                   | Becht,     |             | Charles-Antoine                                  |          | Dutertre,       |           | Immanuel    | W.H.            | Kwok,  |
| --------------------------------------------- | ---------- | ----------- | ------------------------------------------------ | -------- | --------------- | --------- | ----------- | --------------- | ------ |
| Lai Guan                                      |            | Ng, Florent |                                                  | Ginhoux, | and             | Evan      | W Newell.   | Evaluation      | of     |
| umapasanalternativetot-sneforsingle-celldata. |            |             |                                                  |          |                 |           |             | bioRxiv,2018.   |        |
| [5] Etienne                                   | Becht,     |             | Leland                                           | McInnes, |                 | John      | Healy,      | Charles-Antoine |        |
| Dutertre,                                     | Immanuel   |             | WH                                               | Kwok,    | Lai             | Guan      | Ng, Florent | Ginhoux,        | and    |
| EvanWNewell.                                  |            |             | Dimensionalityreductionforvisualizingsingle-cell |          |                 |           |             |                 |        |
| datausingumap.                                |            |             | Naturebiotechnology,37(1):38,2019.               |          |                 |           |             |                 |        |
| [6] Mikhail                                   | Belkin     |             | and Partha                                       | Niyogi.  |                 | Laplacian | eigenmaps   | and             | spec-  |
| tral                                          | techniques |             | for embedding                                    |          | and clustering. |           | In          |                 |        |
|                                               |            |             |                                                  |          |                 |           | Advances    | in              | neural |
informationprocessingsystems,pages585–591,2002.
| [7] Mikhail | Belkin    |     | and Partha | Niyogi. |                 | Laplacian | eigenmaps | for          | dimen- |
| ----------- | --------- | --- | ---------- | ------- | --------------- | --------- | --------- | ------------ | ------ |
| sionality   | reduction |     | and        | data    | representation. |           |           | computation, |        |
Neural
15(6):1373–1396,2003.
| [8] Aure´lien                                     | Bellet, |     | Amaury | Habrard, | and | Marc | Sebban. | A survey      | on  |
| ------------------------------------------------- | ------- | --- | ------ | -------- | --- | ---- | ------- | ------------- | --- |
| metriclearningforfeaturevectorsandstructureddata. |         |     |        |          |     |      |         | arXivpreprint |     |
arXiv:1306.6709,2013.
| [9] Tess  | Brodie, | Elena    |            | Brenna, | and | Federica | Sallusto. | Omip-018:        |     |
| --------- | ------- | -------- | ---------- | ------- | --- | -------- | --------- | ---------------- | --- |
| Chemokine |         | receptor | expression |         | on  | human    | t helper  | cells. Cytometry |     |
PartA,83(6):530–532,2013.
| [10] Lars | Buitinck, | Gilles |         | Louppe, | Mathieu | Blondel, | Fabian | Pedregosa,    |     |
| --------- | --------- | ------ | ------- | ------- | ------- | -------- | ------ | ------------- | --- |
| Andreas   | Mueller,  |        | Olivier | Grisel, | Vlad    | Niculae, | Peter  | Prettenhofer, |     |
AlexandreGramfort,JaquesGrobler,RobertLayton,JakeVanderPlas,
ArnaudJoly,BrianHolt,andGae¨lVaroquaux.APIdesignformachine
| learningsoftware: |           |     | experiencesfromthescikit-learnproject. |     |          |        |             | InECML    |     |
| ----------------- | --------- | --- | -------------------------------------- | --- | -------- | ------ | ----------- | --------- | --- |
| PKDD              | Workshop: |     | Languages                              |     | for Data | Mining | and Machine | Learning, |     |
pages108–122,2013.
58

| [11] JohnNCampbell,                     |              |     | EvanZMacosko,  |        | HenningFenselau, |     |                    | TuneHPers, |      |
| --------------------------------------- | ------------ | --- | -------------- | ------ | ---------------- | --- | ------------------ | ---------- | ---- |
| AnnaLyubetskaya,                        |              |     | DanielleTenen, |        | MelissaGoldman,  |     |                    | AnneMJVer- |      |
| stegen,JonMResch,StevenAMcCarroll,etal. |              |     |                |        |                  |     | Amolecularcensusof |            |      |
| arcuate                                 | hypothalamus |     | and            | median | eminence         |     | cell types.        | Nature     | neu- |
roscience,20(3):484,2017.
[12] JunyueCao,MalteSpielmann,XiaojieQiu,XingfanHuang,DanielM
| Ibrahim,                       | Andrew      |             | J Hill, | Fan Zhang,    | Stefan             |              | Mundlos,        | Lena           | Chris-     |
| ------------------------------ | ----------- | ----------- | ------- | ------------- | ------------------ | ------------ | --------------- | -------------- | ---------- |
| tiansen,                       | Frank       | J Steemers, |         | et al.        | The single-cell    |              | transcriptional |                | land-      |
| scapeofmammalianorganogenesis. |             |             |         |               | Nature,page1,2019. |              |                 |                |            |
| [13] Gunnar                    | Carlsson    |             | and     | Facundo       | Me´moli.           |              | Classifying     |                | clustering |
| schemes.                       |             |             |         |               |                    | Mathematics, |                 | 13(2):221–252, |            |
|                                | Foundations |             | of      | Computational |                    |              |                 |                |            |
2013.
| [14] Shan | Carter, | Zan   | Armstrong, |     | Ludwig     |        | Schubert, |          | Ian John- |
| --------- | ------- | ----- | ---------- | --- | ---------- | ------ | --------- | -------- | --------- |
| son,      | and     | Chris | Olah.      |     | Activation | atlas. |           | Distill, | 2019.     |
https://distill.pub/2019/activation-atlas.
| [15] Brian | Clark,    | Genevieve |               | Stein-O’Brien, |               | Fion       | Shiau,  | Gabrielle     | Can-   |
| ---------- | --------- | --------- | ------------- | -------------- | ------------- | ---------- | ------- | ------------- | ------ |
| non,       | Emily     | Davis,    | Thomas        | Sherman,       | Fatemeh       |            | Rajaii, | Rebecca       | James- |
| Esposito,  | Richard   |           | Gronostajski, |                | Elana Fertig, |            | et al.  | Comprehensive |        |
| analysis   | ofretinal |           | development   |                | at singlecell | resolution |         | identifies    | nfi    |
factorsasessentialformitoticexitandspecificationoflate-borncells.
bioRxiv,page378950,2018.
| [16] RonaldRCoifmanandSte´phaneLafon. |     |     |     |     |     | Diffusionmaps. |     |     |     |
| ------------------------------------- | --- | --- | --- | --- | --- | -------------- | --- | --- | --- |
Appliedand
computationalharmonicanalysis,21(1):5–30,2006.
[17] AlexDiaz-Papkovich,LukeAnderson-Trocme,andSimonGravel.Re-
| vealing | multi-scale |     | population |     | structure | in large | cohorts. |     | bioRxiv, |
| ------- | ----------- | --- | ---------- | --- | --------- | -------- | -------- | --- | -------- |
page423632,2018.
| [18] Wei | Dong,        | Charikar      | Moses,      | and        | Kai Li.    | Efficient | k-nearest |                | neighbor |
| -------- | ------------ | ------------- | ----------- | ---------- | ---------- | --------- | --------- | -------------- | -------- |
| graph    | construction |               | for generic |            | similarity | measures. |           | In Proceedings |          |
|          |              |               |             |            |            |           |           | Web, WWW       | ’11,     |
| of       | the 20th     | International |             | Conference | on         | World     | Wide      |                |          |
pages577–586,NewYork,NY,USA,2011.ACM.
| [19] Carlos         | Escolano,         | Marta |                                     | R Costa-jussa`, |     | and Jose´ | AR             | Fonollosa. | (self- |
| ------------------- | ----------------- | ----- | ----------------------------------- | --------------- | --- | --------- | -------------- | ---------- | ------ |
| attentive)          | autoencoder-based |       |                                     | universal       |     | language  | representation |            | for    |
| machinetranslation. |                   |       | arXivpreprintarXiv:1810.06351,2018. |                 |     |           |                |            |        |
[20] MateusEspadoto,NinaSTHirata,andAlexandruCTelea.Deeplearn-
| ing | multidimensional |     | projections. |     |       |          |     | arXiv:1902.07958, |     |
| --- | ---------------- | --- | ------------ | --- | ----- | -------- | --- | ----------------- | --- |
|     |                  |     |              |     | arXiv | preprint |     |                   |     |
2019.
59

[21] Mateus Espadoto, Francisco Caio M Rodrigues, and Alexandru C
Telea. Visualanalyticsofmultidimensionalprojectionsforconstruct-
ingclassifierdecisionboundarymaps.
[22] Greg Friedman et al. Survey article: an elementary illustrated intro-
duction to simplicial sets. Rocky Mountain Journal of Mathematics,
42(2):353–423,2012.
[23] LukasFuhrimann,VahidMoosavi,PatrickOleOhlbrock,andPierluigi
Dacunto. Data-driven design: Exploring new structural forms using
machinelearningandgraphicstatics. arXivpreprintarXiv:1809.08660,
2018.
[24] BenoitGaujac,IlyaFeige,andDavidBarber.Gaussianmixturemodels
withwassersteindistance. arXivpreprintarXiv:1806.04465,2018.
[25] Paul G Goerss and John F Jardine. Simplicial homotopy theory.
SpringerScience&BusinessMedia,2009.
[26] Matthias Hein, Jean-Yves Audibert, and Ulrike von Luxburg. Graph
laplacians and their convergence on random neighborhood graphs.
JournalofMachineLearningResearch,8(Jun):1325–1368,2007.
[27] Harold Hotelling. Analysis of a complex of statistical variables into
principal components. Journal of educational psychology, 24(6):417,
1933.
[28] DmitryKobakandPhilippBerens.Theartofusingt-sneforsingle-cell
transcriptomics. Naturecommunications,10(1):1–14,2019.
[29] Dmitry Kobak and George C Linderman. Umap does not preserve
globalstructureanybetterthant-snewhenusingthesameinitializa-
tion. bioRxiv,2019.
[30] J.B.Kruskal. Multidimensionalscalingbyoptimizinggoodnessoffit
toanonmetrichypothesis. Psychometrika,29(1):1–27,Mar1964.
[31] SiuKwanLam,AntoinePitrou,andStanleySeibert. Numba: Allvm-
based python jit compiler. In Proceedings of the Second Workshop on
the LLVM Compiler Infrastructure in HPC, LLVM ’15, pages 7:1–7:6,
NewYork,NY,USA,2015.ACM.
[32] YannLecunandCorinnaCortes. TheMNISTdatabaseofhandwritten
digits.
[33] JohnALeeandMichelVerleysen. Shift-invariantsimilaritiescircum-
vent distance concentration in stochastic neighbor embedding and
variants. ProcediaComputerScience,4:538–547,2011.
60

[34] Xin Li, Ondrej E Dyck, Mark P Oxley, Andrew R Lupini, Leland
McInnes, John Healy, Stephen Jesse, and Sergei V Kalinin. Mani-
foldlearningoffour-dimensionalscanningtransmissionelectronmi-
croscopy. npjComputationalMaterials,5(1):5,2019.
[35] M.Lichman. UCImachinelearningrepository,2013.
[36] George Linderman. Fit-sne. https://github.com/KlugerLab/
FIt-SNE,2018.
[37] George C Linderman, Manas Rachh, Jeremy G Hoskins, Stefan
Steinerberger,andYuvalKluger. Efficientalgorithmsfort-distributed
stochasticneighborhoodembedding. arXivpreprintarXiv:1712.09005,
2017.
[38] GeorgeCLindermanandStefanSteinerberger. Clusteringwitht-sne,
provably. SIAMJournalonMathematicsofDataScience,1(2):313–332,
2019.
[39] Saunders Mac Lane. Categories for the working mathematician, vol-
ume5. SpringerScience&BusinessMedia,2013.
[40] JPeterMay. Simplicialobjectsinalgebraictopology, volume11. Uni-
versityofChicagoPress,1992.
[41] Tomas Mikolov, Ilya Sutskever, Kai Chen, Greg S Corrado, and Jeff
Dean. Distributed representations of words and phrases and their
compositionality. In Advances in neural information processing sys-
tems,pages3111–3119,2013.
[42] KevinRMoon,DavidvanDijk,ZhengWang,ScottGigante,DanielB
Burkhardt, William S Chen, Kristina Yim, Antonia van den Elzen,
Matthew J Hirn, Ronald R Coifman, et al. Visualizing structure and
transitionsinhigh-dimensionalbiologicaldata. Naturebiotechnology,
37(12):1482–1492,2019.
[43] SameerA.Nene,ShreeK.Nayar,andHiroshiMurase.Columbiaobject
imagelibrary(coil-20. Technicalreport,1996.
[44] Sameer A. Nene, Shree K. Nayar, and Hiroshi Murase. object image
library(coil-100. Technicalreport,1996.
[45] KarolynAOetjen,KatherineELindblad,MeghaliGoswami,GegeGui,
PradeepKDagur,CatherineLai,LauraWDillon,JPhilipMcCoy,and
ChristopherSHourigan. Humanbonemarrowassessmentbysingle
cell rna sequencing, mass cytometry and flow cytometry. bioRxiv,
2018.
61

[46] Jong-Eun Park, Krzysztof Polanski, Kerstin Meyer, and Sarah A Te-
ichmann. Fast batch alignment of single cell transcriptomes unifies
multiplemousecellatlasesintoanintegratedlandscape.bioRxiv,page
397042,2018.
[47] JoseDanielGallegoPosada. Simplicialautoencoders. 2018.
[48] Emily Riehl. A leisurely introduction to simplicial sets. Unpublished
expository article available online at http://www. math. harvard. edu/˜
eriehl,2011.
[49] EmilyRiehl. Categorytheoryincontext. CourierDoverPublications,
2017.
[50] John W Sammon. A nonlinear mapping for data structure analysis.
IEEETransactionsoncomputers,100(5):401–409,1969.
[51] Josef Spidlen, Karin Breuer, Chad Rosenberg, Nikesh Kotecha, and
RyanRBrinkman. Flowrepository: Aresourceofannotatedflowcy-
tometrydatasetsassociatedwithpeer-reviewedpublications. Cytom-
etryPartA,81(9):727–731,2012.
[52] David I Spivak. Metric realization of fuzzy simplicial sets. Self pub-
lishednotes,2012.
[53] JianTang. Largevis. https://github.com/lferry007/LargeVis,
2016.
[54] Jian Tang, Jingzhou Liu, Ming Zhang, and Qiaozhu Mei. Visualizing
large-scaleandhigh-dimensionaldata.InProceedingsofthe25thInter-
nationalConferenceonWorldWideWeb,pages287–297.International
WorldWideWebConferencesSteeringCommittee,2016.
[55] Joshua B. Tenenbaum. Mapping a manifold of perceptual observa-
tions.InM.I.Jordan,M.J.Kearns,andS.A.Solla,editors,Advancesin
Neural Information Processing Systems 10, pages 682–688. MIT Press,
1998.
[56] Joshua B Tenenbaum, Vin De Silva, and John C Langford. A global
geometricframeworkfornonlineardimensionalityreduction.science,
290(5500):2319–2323,2000.
[57] Dmitry Ulyanov. Multicore-tsne. https://github.com/
DmitryUlyanov/Multicore-TSNE,2016.
[58] Laurens van der Maaten. Accelerating t-sne using tree-based algo-
rithms. Journalofmachinelearningresearch,15(1):3221–3245,2014.
62

| [59] LaurensvanderMaatenandGeoffreyHinton. |                                                         |         |         |      | Visualizingdatausing |     |     |
| ------------------------------------------ | ------------------------------------------------------- | ------- | ------- | ---- | -------------------- | --- | --- |
| t-sne.                                     | Journalofmachinelearningresearch,9(Nov):2579–2605,2008. |         |         |      |                      |     |     |
| [60] LaurensvanderMaatenandGeoffreyHinton. |                                                         |         |         |      | Visualizingdatausing |     |     |
| t-SNE.                                     | JournalofMachineLearningResearch,9:2579–2605,2008.      |         |         |      |                      |     |     |
| [61] John                                  | Williamson.                                             | What do | numbers | look | like?                |     |     |
https://johnhw.
github.io/umap_primes/index.md.html,2018.
[62] DuoduoWu,JoeYeong,GraceTan,MarionChevrier,JoshLoh,Tony
| Lim,                                                  | and Jinmiao              | Chen. Comparison |         | between     | umap           | and  | t-sne for   |
| ----------------------------------------------------- | ------------------------ | ---------------- | ------- | ----------- | -------------- | ---- | ----------- |
| multiplex-immunofluorescence                          |                          |                  | derived | single-cell |                | data | from tissue |
| sections.                                             | bioRxiv,page549659,2019. |                  |         |             |                |      |             |
| [63] HanXiao,KashifRasul,andRolandVollgraf.           |                          |                  |         |             | Fashion-mnist: |      | anovel      |
| imagedatasetforbenchmarkingmachinelearningalgorithms. |                          |                  |         |             |                |      | CoRR,       |
abs/1708.07747,2017.
| [64] Liu Yang | and Rong                            | Jin. Distance | metric | learning: |     | A comprehensive |     |
| ------------- | ----------------------------------- | ------------- | ------ | --------- | --- | --------------- | --- |
| survey.       | MichiganStateUniversiy,2(2):4,2006. |               |        |           |     |                 |     |
[65] LoftiAZadeh.Informationandcontrol.Fuzzysets,8(3):338–353,1965.
63