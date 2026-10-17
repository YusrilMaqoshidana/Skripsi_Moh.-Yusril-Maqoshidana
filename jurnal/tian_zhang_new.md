DataMiningandKnowledgeDiscovery,1,141–182(1997)
(cid:176)c 1997KluwerAcademicPublishers.ManufacturedinTheNetherlands.
BIRCH: A New Data Clustering Algorithm and Its
Applications
TIANZHANG zhang@cs.wisc.edu
RAGHURAMAKRISHNAN raghu@cs.wisc.edu
MIRONLIVNY miron@cs.wisc.edu
ComputerSciencesDepartment,UniversityofWisconsin,Madison,WI53706,U.S.A.
Editor:UsamaFayyad
ReceivedAugust20,1996;RevisedMarch18,1997;AcceptedMarch26,1997
Abstract.Dataclusteringisanimportanttechniqueforexploratorydataanalysis,andhasbeenstudiedforseveral
years.Ithasbeenshowntobeusefulinmanypracticaldomainssuchasdataclassificationandimageprocessing.
Recently,therehasbeenagrowingemphasisonexploratoryanalysisofverylargedatasetstodiscoveruseful
patternsand/orcorrelationsamongattributes. Thisiscalleddatamining,anddataclusteringisregardedasa
particularbranch.Howeverexistingdataclusteringmethodsdonotadequatelyaddresstheproblemofprocessing
largedatasetswithalimitedamountofresources(e.g.,memoryandcpucycles).Soasthedatasetsizeincreases,
theydonotscaleupwellintermsofmemoryrequirement,runningtime,andresultquality.
Inthispaper,anefficientandscalabledataclusteringmethodisproposed,basedonanewin-memorydata
structurecalledCF-tree,whichservesasanin-memorysummaryofthedatadistribution.Wehaveimplemented
itinasystemcalledBIRCH(BalancedIterativeReducingandClusteringusingHierarchies),andstudieditsper-
formanceextensivelyintermsofmemoryrequirements,runningtime,clusteringquality,stabilityandscalability;
wealsocompareitwithotheravailablemethods.Finally,BIRCHisappliedtosolvetworeal-lifeproblems:one
isbuildinganiterativeandinteractivepixelclassificationtool,andtheotherisgeneratingtheinitialcodebookfor
imagecompression.
Keywords:VeryLargeDatabases,DataClustering,IncrementalAlgorithm,DataClassificationandCompression
1. Introduction
Inthispaper,dataclusteringreferstotheproblemofdividingNdatapointsintoKgroupsso
astominimizeanintra-group‘difference’metric,suchasthesumofthesquareddistances
fromtheclustercenters. Givenaverylargesetofmultidimensionaldatapoints, thedata
spaceisusuallynotuniformlyoccupiedbythedatapoints. Throughdataclustering,onecan
identifysparseandcrowdedregions,andhencediscovertheoveralldistributionpatternsor
thecorrelationsamongdataattributes. Thisinformationmaybeusedtoguidetheapplication
ofmorerigorousdataanalysisprocedures. Itisaproblemwithmanypracticalapplications
andhasbeenstudiedformanyyears. Manyclusteringmethodshavebeendevelopedand
appliedtovariousdomains,includingdataclassificationandimagecompression(Lee,1981,
DubesandJain,1980). However,itisalsoaverydifficultsubjectbecausetheoretically,it
isanonconvex,discreteoptimization(KaugfmanandRousseeuw,1990)problem. Dueto
anabundanceoflocalminima,thereistypicallynowaytofindagloballyminimalsolution

142 ZHANG,RAMAKRISHNANANDLIVNY
withouttryingallpossiblepartitions. Usually,thisisinfeasibleexceptwhenNandKare
extremelysmall.
In this paper, we add the following database-oriented constraints to the problem, moti-
vatedbyourdesiretoclusterverylargedatasets: Theamountofmemoryavailableislimited
(typically,muchsmallerthanthedatasetsize)whereasthedatasetcanbearbitrarilylarge,
andtheI/Ocostinvolvedinclusteringthedatasetshouldbeminimized. Wepresentaclus-
teringalgorithmcalledBIRCHanddemonstratethatitisespeciallysuitableforclustering
very large datasets. BIRCH deals with large datasets by first generating a more compact
summarythatretainsasmuchdistributioninformationaspossible,andthenclusteringthe
datasummaryinsteadoftheoriginaldataset. ItsI/Ocostislinearwiththethedatasetsize:
asinglescanofthedatasetyieldsagoodclustering,andoneormoreadditionalpassescan
(optionally)beusedtoimprovethequalityfurther.
By evaluating BIRCH’s running time, memory usage, clustering quality, stability and
scalability,aswellascomparingitwithotherexistingalgorithms,wearguethatBIRCHis
thebestavailableclusteringmethodforhandlingverylargedatasets. WenotethatBIRCH
actuallycomplementsotherclusteringalgorithmsbyvirtueofthefactthatdifferentcluster-
ingalgorithmscanbeappliedtothesummaryproducedbyBIRCH.BIRCH’sarchitecture
alsooffersopportunitiesforparallelandconcurrentclustering,anditispossibletointerac-
tivelyanddynamicallytunetheperformancebasedonknowledgegainedaboutthedataset
overthecourseoftheexecution.
Therestofthepaperisorganizedasfollows. Section2surveysrelatedwork, andthen
explainsthecontributionsandlimitationsofBIRCH.Section3presentssomebackground
materialneededfordiscussingdataclusteringinBIRCH.Section4introducestheclustering
feature(CF)conceptandtheCF-treedatastructure,whicharecentraltoBIRCH.Thedetails
oftheBIRCHdataclusteringalgorithmaredescribedinSection5. Theperformancestudyof
BIRCH,CLARANSandKMEANSonsyntheticdatasetsispresentedinSection6. Section
7 presents two applications of BIRCH, which are also intended to show how BIRCH,
CLARANS and KMEANS perform on some real datasets. Finally our conclusions and
directionsforfutureresearcharepresentedinSection8.
2. PreviousWorkandBIRCH
DataclusteringhasbeenstudiedintheMachineLearning(Cheeseman,etal.,1988,Fisher,
1987, Fisher, 1995, Gennari, Langley and Fisher, 1989, Lebowitz, 1987), Statistics
(DudaandHart,1973, DubesandJain,1980, Lee,1981, Murtagh,1983), and Database
(Ester,KriegelandXu,1995a,Ester,KriegelandXu,1995b,NgandHan,1994)commu-
nitieswithdifferentmethodsanddifferentemphases.
2.1. Probability-BasedClustering
PreviousdataclusteringworkinMachineLearningisusuallyreferredtoasunsupervised
conceptuallearning(Cheeseman,etal.,1988,Fisher,1987,Gennari,LangleyandFisher,
1989,Lebowitz,1987). Theyconcentrateonincrementalapproachesthatacceptinstances

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 143
one at a time, and do not extensively reprocess previously encountered instances while
incorporatinganewconcept. Concept(orcluster)formationisaccomplishedbytop-down
‘sorting’, with each new instance directed through a hierarchy whose nodes are formed
gradually,andrepresentconcepts. Theyareusuallyprobability-basedapproaches,i.e.,(1)
they use probabilistic measurements (e.g., category utility as discussed in (Fisher,1987,
Gennari,LangleyandFisher,1989))formakingdecisions;and(2)theyrepresentconcepts
(orclusters)withprobabilisticdescriptions.
Forexample,COBWEB(Fisher,1987)proceedsasfollows. Toinsertanewinstanceinto
thehierarchy,itstartsfromtheroot,andconsidersfourchoicesateachlevelasitdescends
thehierarchy: (1)recursivelyincorporatingtheinstanceintoanexistingnode,(2)creating
anewnodefortheinstance,(3)mergingtwonodestohosttheinstance,and(4)splitting
anexistingnodetohosttheinstance. Thechoicethatresultsinthehighestcategoryutility
scoreisselected. COBWEBhasthefollowinglimitations:
† Itistargetedforhandlingdiscreteattributesandthecategoryutilitymeasurementused
isveryexpensivetocompute. Tocomputethecategoryutilityscores,adiscreteproba-
bilitydistributionisstoredineachnodeforeachindividualattribute. COBWEBmakes
theassumptionthatprobabilitydistributionsonseparateattributesarestatisticallyin-
dependent,andignorescorrelationsamongattributes. Updatingandstoringaconcept
isveryexpensive,especiallyiftheattributeshavealargenumberofvalues. COBWEB
dealsonlywithdiscreteattributes,andforacontinuousattribute,onehastodividethe
attributevaluesintoranges,or‘discretize’theattributeinadvance.
† All instances ever encountered are retained as terminal nodes in the hierarchy. For
verylargedatasets,storingandmanipulatingsuchalargehierarchyisinfeasible. Ithas
alsobeenshownthatthiskindoflargehierarchytendsto‘overfit’thedata. Arelated
problemisthatthishierarchyisnotkeptwidth-balancedorheight-balanced. Sointhe
caseofskewedinputdata,thismaycauseperformancetodegrade.
AnothersystemcalledCLASSIT(Gennari,LangleyandFisher,1989)isverysimilarto
COBWEB,withthefollowingmaindifferences. (1)Itonlydealswithcontinuous(orreal-
valued)attributes(incontrasttodiscreteattributesinCOBWEB).(2)Itstoresacontinuous
normal distribution (i.e., mean and standard deviation) for each individual attribute in a
node,incontrasttoadiscreteprobabilitydistributioninCOBWEB.(3)Asitclassifiesanew
instance,itcanhaltatsomehigher-levelnodeiftheinstanceis‘similarenough’tothenode,
whereasCOBWEBalwaysdescendstoaterminalnode. (4)Itmodifiesthecategoryutility
measurement to be an integral over continuous attributes, instead of a sum over discrete
attributesasinCOBWEB.
The disadvantages of using an expensive metric and generating large, unbalanced tree
structures clearly apply to CLASSIT as well as COBWEB, and make it unsuitable for
workingdirectlywithlargedatasets.

144 ZHANG,RAMAKRISHNANANDLIVNY
2.2. Distance-Based
MostdataclusteringalgorithmsinStatisticsaredistance-basedapproaches. Thatis,(1)they
assumethatthereisadistancemeasurementbetweenanytwoinstances(ordatapoints),and
thatthismeasurementcanbeusedformakingsimilaritydecisions;and(2)theyrepresent
clustersbysomekindof‘center’measure.
There are two categories of clustering algorithms (KaugfmanandRousseeuw,1990):
Partitioning Clustering and Hierarchical Clustering. Partitioning Clustering (PC)
(DudaandHart,1973,KaugfmanandRousseeuw,1990)startswithaninitialpartition,then
triesallpossiblemovingorswappingofdatapointsfromonegrouptoanotheriteratively
to optimize the objective measurement function. Each cluster is represented either by
the centroid of the cluster (KMEANS), or by one object centrally located in the cluster
(KMEDOIDS).Itguaranteesconvergencetoalocalminimum,butthequalityofthelocal
minimum is very sensitive to the initial partition, and the worst case time complexity is
exponential. HierarchicalClustering(HC)(DudaandHart,1973,Murtagh,1983)doesnot
trytofindthe‘best’clusters,insteaditkeepsmerging(agglomerativeHC)theclosestpair,
orsplitting(divisiveHC)thefarthestpair, ofobjectstoformclusters. Withareasonable
distancemeasurement,thebesttimecomplexityofapracticalHCalgorithmisO(N2).
Insummary, theseapproachesassumethatalldatapointsaregiveninadvanceandcan
bestoredinmemoryandscannedfrequently(non-incremental). Theytotallyorpartially
ignorethefactthatnotalldatapointsinthedatasetareequallyimportantforpurposesof
clustering, i.e., that data points which are close and dense can be considered collectively
insteadofindividually. Theyareglobalorsemi-globalmethodsatthegranularityofdata
points. That is, for each clustering decision, they inspect all data points or all currently
existing clusters equally no matter how close or far away they are, and they use global
measurements, which require scanning all data points or all currently existing clusters.
Hencenoneofthemcanscaleuplinearlywithstablequality.
Data clustering has been recognized as a useful spatial data mining method recently.
(NgandHan,1994)presentsCLARANS,whichisaKMEDOIDSalgorithmbutwithran-
domizedpartialsearchstrategy,andsuggeststhatCLARANSout-performsthetraditional
KMEDOIDSalgorithms. TheclusteringprocessinCLARANSisformalizedassearching
agraphinwhicheachnodeisaK-partitionrepresentedbyK medoids,andtwonodesare
neighborsiftheyonlydifferbyonemedoid. CLARANSstartswitharandomlyselected
node. For the current node, it checks at most maxneighbor neighbors randomly, and if
a better neighbor is found, it moves to the neighbor and continues; otherwise it records
the current node as a local minimum, and restarts with a new randomly selected node to
search for another local minimum. CLARANS stops after numlocal local minima have
beenfound,andreturnsthebestofthese. CLARANSsuffersfromthesamedrawbacksas
theKMEDOIDSmethodwithrespecttoefficiency. Inaddition,itmaynotfindareallocal
minimumduetotherandomsearchtrimmingcontrolledbymaxneighbor.
The R-tree (Guttman,1984) (or variants such as R⁄-tree (Beckmann,etal.,1990)) is a
populardynamicmulti-dimensionalspatialindexstructurethathasexistedinthedatabase
communityformorethanadecade. BasedonspatiallocalityinR⁄-trees(avariationofR-
trees),(Ester,KriegelandXu,1995a)and(Ester,KriegelandXu,1995b)proposefocusing

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 145
techniquestoimproveCLARANS’sabilitytodealwithverylargedatasetsthatmayreside
ondisksby(1)clusteringasampleofthedatasetthatisdrawnfromeachR⁄-treedatapage;
and(2)focusingonrelevantdatapointsfordistanceandqualityupdates. Theirexperiments
showthatthetimeisimprovedbutwithasmalllossofquality.
2.3. ContributionsandLimitationsofBIRCH
The CF-tree structure introduced in this paper is strongly influenced by balanced tree-
structuredindexessuchasB-treesandR-Trees. Itisalsoinfluencedbytheincrementaland
hierarchical themes of COBWEB as well as COBWEB’s use of splitting and merging to
alleviatethepotentialsensitivitytoinputdataordering. Currently, BIRCHcanonlydeal
with metric attributes (similar to the kind of attributes that KMEANS and CLASSIT can
handle). Ametricattributeisonewhosevaluescanberepresentedbyexplicitcoordinates
inanEuclideanspace.
Incontrasttoearlierwork,animportantcontributionofBIRCHistheformulationofthe
clusteringprobleminawaythatisappropriateforverylargedatasetsbymakingthetimeand
memoryconstraintsexplicit. AnothercontributionisthatBIRCHexploitstheobservation
that the data space is usually not uniformly occupied, and hence not every data point is
equallyimportantforclusteringpurposes. SoBIRCHtreatsadenseregionofpoints(ora
subclusters)collectivelybystoringacompactsummarization(‘clusteringfeature’,which
isdiscussedinSection4.1). BIRCHtherebyreducestheproblemofclusteringtheoriginal
data points into one of clustering the set of summaries, which is much smaller than the
originaldataset.
The summaries generated by BIRCH reflect the natural closeness of data, allow for
the computation of the distance-based measurements (defined in Section 3), and can be
maintained efficiently and incrementally. Although we only use them for computing the
distances, we note that they are also sufficient for computing the probability-based mea-
surementssuchasmean,standarddeviationandcategoryutilityusedinCLASSIT.
Comparedwithpriordistance-basedalgorithms,BIRCHisincrementalinthesensethat
clustering decisions are made without scanning all data points or all currently existing
clusters. IfweomittheoptionalPhase4(Section5),BIRCHisanincrementalmethodthat
doesnotrequirethewholedatasetinadvance,andonlyscansthedatasetonce.
Comparedwithpriorprobability-basedalgorithms,BIRCHtriestomakethebestuseof
the available memory to derive the finest possible subclusters (to ensure accuracy) while
minimizingI/Ocosts(toensureefficiency)byorganizingtheclusteringandreducingprocess
using an in-memory balanced tree structure of bounded size. Finally BIRCH does not
assumethattheprobabilitydistributionsonseparateattributesareindependent.
3. Background
Assumingthatthereadersarefamiliarwiththeterminologyofvectorspaces,webeginby
definingcentroid,radiusanddiameterforacluster. GivenN d-dimensionaldatapointsin

| 146       |             |     |                                                   |     | ZHANG,RAMAKRISHNANANDLIVNY |     |     |     |     |
| --------- | ----------- | --- | ------------------------------------------------- | --- | -------------------------- | --- | --- | --- | --- |
|           | fX~ gwherei |     | 1;2;:::;N,thecentroidX~0,radiusRanddiameterDofthe |     |                            |     |     |     |     |
| acluster: |             |     | =                                                 |     |                            |     |     |     |     |
i
clusteraredefinedas:
P
|      |     | N X~  |     |     |     |     |     |     |     |
| ---- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
| X~0= |     | i=1 i |     |     |     |     |     |     |     |
(1)
N
P
|     |     | N (X~ ¡X~0)2 |     |     |     |     |     |     |     |
| --- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
|     |     | i=1 i        | )1  |     |     |     |     |     |     |
| R=( |     |              | 2   |     |     |     |     |     | (2) |
N
|     | P   | P         |         |      |     |     |     |     |     |
| --- | --- | --------- | ------- | ---- | --- | --- | --- | --- | --- |
|     |     | N N       | (X~ ¡X~ | )2   |     |     |     |     |     |
|     |     | i=1 j = 1 | i       | j )1 |     |     |     |     |     |
| D   | =(  |           |         | 2    |     |     |     |     | (3) |
|     |     | N ( N     | ¡1 )    |      |     |     |     |     |     |
Ristheaveragedistancefrommemberpointstothecentroid. Distheaveragepairwise
distancewithinacluster. Theyaretwoalternativemeasuresofthetightnessofthecluster
around the centroid. Next, between two clusters, we define five alternative distances for
measuringtheircloseness.
|     |     |     |     | X~0 | andX~0 |     |     |     |     |
| --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- |
Giventhecentroidsoftwoclusters: ,thecentroidEuclideandistanceD0
|     |     |     |     |     | 1 2 |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
andcentroidManhattandistanceD1ofthetwoclustersaredefinedas:
| D0=((X~0 |     | ¡X~0 | )2)1 |     |     |     |     |     |     |
| -------- | --- | ---- | ---- | --- | --- | --- | --- | --- | --- |
|          |     | 1    | 2 2  |     |     |     |     |     | (4) |
Xd
|         |     |      |         | (i)¡X~0 | (i)j |     |     |     |     |
| ------- | --- | ---- | ------- | ------- | ---- | --- | --- | --- | --- |
| D1=jX~0 |     | ¡X~0 | j= jX~0 |         |      |     |     |     | (5) |
|         |     | 1    | 2       | 1       | 2    |     |     |     |     |
i=1
|     |     |     |     |     | fX~ gwherei |     |     |     |     |
| --- | --- | --- | --- | --- | ----------- | --- | --- | --- | --- |
GivenN d-dimensionaldatapointsinacluster: i = 1;2;:::;N , andN
|     | 1   |     |     |     |     |     |     | 1   | 2   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
datapointsinanothercluster: fX~ gwherej =N +1;N +2;:::;N +N ,theaverage
|     |     |     | j   |     | 1 1 |     | 1   | 2   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
inter-cluster distance D2, average intra-cluster distance D3 and variance increase
distanceD4ofthetwoclustersaredefinedas:
|     | P   | P          |                |          |     |     |     |     |     |
| --- | --- | ---------- | -------------- | -------- | --- | --- | --- | --- | --- |
|     |     | N N        | + N            |          |     |     |     |     |     |
|     |     | 1          | 1 2 (X~ i ¡X~  | j)2      |     |     |     |     |     |
| D2= | (   | i= 1 j=    | N 1 + 1        | )1       |     |     |     |     | (6) |
|     |     | N1N2       |                |          | 2   |     |     |     |     |
|     | P   | P          |                |          |     |     |     |     |     |
|     |     | N 1 +N 2   | N 1 + N 2 (X ~ | ¡ X~ j)2 |     |     |     |     |     |
|     |     |            |                | i        | )1  |     |     |     |     |
| D3= | (   | i= 1       | j = 1          | ¡        | 2   |     |     |     | (7) |
|     |     | ( N 1+ N2) | ( N 1 + N 2    | 1)       |     |     |     |     |     |
P
|     |     |       | P     |          | N +N         |     |          |        |     |
| --- | --- | ----- | ----- | -------- | ------------ | --- | -------- | ------ | --- |
|     |     |       | N     | 1+ N2(X~ | ¡ 1 2 X~     |     |          |        |     |
| D4= |     |       | (     |          | l= 1         | l)2 |          |        |     |
|     |     |       | k=    | 1        | k N + N      | P   |          |        |     |
|     |     |       | P     |          | 1 2          |     |          |        |     |
|     |     | P     | N     |          | P            | N 1 | + N 2 X~ |        |     |
|     | ¡   | N (X~ | ¡ 1   | X~ l)2¡  | N + N (X~ ¡  |     |          | l )2)1 |     |
|     |     | 1     | l = 1 |          | 1 2          | l=  | N 1 + 1  | 2      | (8) |
|     |     | i= 1  | i N 1 |          | j= N 1 + 1 j |     | N 2      |        |     |
D3isactuallyD ofthemergedcluster. Forthesakeofclarity, wetreatX~0, R andD
aspropertiesofasinglecluster,andD0,D1,D2,D3andD4aspropertiesbetweentwo
clustersandstatethemseparately.

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 147
Followingaretwoalternativeclusteringqualitymeasurements: weightedaveragecluster
radiussquareQ1(orR„),andweightedaverageclusterdiametersquareQ2(orD„).
P
K n R2
Q1= Pi=1 i i (9)
K n
i=1 i
P
K n (n ¡1)D2
Q2= Pi=1 i i i (10)
K n (n ¡1)
i=1 i i
Wecanoptionallypre-processdatabyweightingand/orshiftingthedataalongdifferent
dimensionswithoutaffectingtherelativeplacementofdatapoints(ThatisifpointAisto
theleftofpointB,thenafterweightingandshifting,pointAisstilltotheleftofpointB.).
Forexample,tonormalizethedata,onecanshiftitbythemeanvaluealongeachdimension,
andthenweightitbytheinverseofthestandarddeviationoneachdimension. Ingeneral,
suchdatapre-processingisadebatablesemanticissue. Ononehand,itavoidsbiasescaused
bysomedimensions. Forexample,thedimensionswithlargespreaddominatethedistance
calculationsintheclusteringprocess. Ontheotherhand,itisinappropriateifthespreadis
indeedduetonaturaldifferencesofclusters. Sincepre-processingthedatainsuchamanner
isorthogonaltotheclusteringalgorithmitself,wewillassumethattheuserisresponsible
forsuchpre-processing,andnotconsideritfurther.
4. ClusteringFeatureandCF-tree
BIRCHsummarizesadatasetintoasetofsubclusterstoreducethescaleoftheclustering
problem. Inthissection,wewillanswerthefollowingquestionsaboutthesummarization
usedinBIRCH:
1. Howmuchinformationshouldbekeptforeachsubcluster?
2. Howistheinformationaboutsubclustersorganized?
3. Howefficientlyistheorganizationmaintained?
4.1. ClusteringFeature(CF)
AClusteringFeature(CF)entryisatriplesummarizingtheinformationthatwemaintain
aboutasubclusterofdatapoints.
CF Definition : Given N d-dimensional data points in a cluster: fX~ g where i =
i
1;2;:::;N,theClusteringFeature(CF)entryoftheclusterisdefinedasatriple: CF=
(N;L~S;SS), where N is the number of data points in the cluster, L~S is the linear sum
P
oftheN datapoints, i.e., N X~ , andSS isthesquaresumoftheN datapoints, i.e.,
P i=1 i
N X~ 2 .
i=1 i

148 ZHANG,RAMAKRISHNANANDLIVNY
CFRepresentativityTheorem : GiventheCFentriesofsubclusters,allthemeasurements
definedinSection3canbecomputedaccurately.
CFAdditivityTheorem : AssumethatCF =(N ;L~S ;SS ),andCF =(N ;L~S ;
1 1 1 1 2 2 2
SS ) aretheCFentriesoftwodisjointsubclusters. ThentheCFentryofthesubcluster
2
thatisformedbymergingthetwodisjointsubclustersis:
CF +CF =(N +N ;L~S +L~S ;SS +SS ) (11)
1 2 1 2 1 2 1 2
The theorem’s proof consists of conventional vector space algebra (Zhang,1996). Ac-
cordingtotheCFdefinitionandtheCFrepresentativitytheorem, onecanthinkofasub-
clusterasasetofdatapoints,andtheCFentrystoredasasummary. ThisCFentryisnot
onlycompactbecauseitstoresmuchlessthanallthedatapointsinthesubcluster,itisalso
accuratebecauseitissufficientforcalculatingallthemeasurements(asdefinedinSection
3)thatweneedformakingclusteringdecisionsinBIRCH.AccordingtotheCFadditiv-
itytheorem,theCFentriescanbestoredandcalculatedincrementallyandconsistentlyas
subclustersaremergedornewdatapointsareinserted.
4.2. CF-tree
ACF-treeisaheight-balancedtreewithtwoparameters: branchingfactor(B fornonleaf
nodeandLforleafnode)andthresholdT. EachnonleafnodecontainsatmostBentriesof
theform[CF ;child ],wherei=1;2;:::;B,‘child ’isapointertoitsi-thchildnode,and
i i i
CF istheCFentryofthesubclusterrepresentedbythischild. Soanonleafnoderepresents
i
asubclustermadeupofallthesubclustersrepresentedbyitsentries. Aleafnodecontainsat
mostLentries,andeachentryisaCF.Inaddition,eachleafnodehastwopointers,‘prev’
and‘next’,whichareusedtochainallleafnodestogetherforefficientscans. Aleafnode
alsorepresentsasubclustermadeupofallthesubclustersrepresentedbyitsentries. But
allentriesinaleafnodemustsatisfyathresholdrequirement,withrespecttoathreshold
valueT:thediameter(alternatively,theradius)ofeachleafentryhastobelessthanT.
ThetreesizeisafunctionofT. ThelargerT is,thesmallerthetreeis. Werequireanode
tofitinapageofsizeP,whereP isaparameterofBIRCH.Oncethedimensiondofthe
dataspaceisgiven,thesizesofleafandnonleafentriesareknown,andthenB andLare
determinedbyP. SoP canbevariedforperformancetuning.
SuchaCF-treewillbebuiltdynamicallyasnewdataobjectsareinserted. Itisusedto
guideanewinsertionintothecorrectsubclusterforclusteringpurposesjustasaB+-treeis
usedtoguideanewinsertionintothecorrectpositionforsortingpurposes. Howeverthe
CF-treeisaverycompactrepresentationofthedatasetbecauseeachentryinaleafnodeis
notasingledatapointbutasubcluster(whichabsorbsasmanydatapointsasthespecific
thresholdvalueallows).

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 149
4.3. InsertionAlgorithm
We now present the algorithm for inserting a CF entry ‘Ent’ (a single data point or a
subcluster)intoaCF-tree.
1. Identifyingtheappropriateleaf: Startingfromtheroot,recursivelydescendtheCF-tree
bychoosingtheclosestchildnodeaccordingtoachosendistancemetric: D0,D1,D2,D3
orD4asdefinedinSection3.
2. Modifyingtheleaf: Uponreachingaleafnode,findtheclosestleafentry,sayL ,and
i
thentestwhetherL can‘absorb’‘Ent’withoutviolatingthethresholdcondition. (That
i
is,theclustermergedwith‘Ent’andL mustsatisfythethresholdcondition. Notethat
i
theCFentryofthenewclustercanbecomputedfromtheCFentriesforL and‘Ent’.)
i
Ifso,updatetheCFentryforL toreflectthis. Ifnot,addanewentryfor‘Ent’tothe
i
leaf. Ifthereisspaceontheleafforthisnewentrytofitin,wearedone,otherwisewe
mustsplittheleafnode. Nodesplittingisdonebychoosingthefarthestpairofentries
asseeds,andredistributingtheremainingentriesbasedontheclosestcriteria.
3. Modifyingthepathtotheleaf: Afterinserting‘Ent’intoaleaf, updatetheCFinfor-
mation for each nonleaf entry on the path to the leaf. In the absence of a split, this
simplyinvolvesupdatingexistingCFentriestoreflecttheadditionof‘Ent’. Aleafsplit
requires us to insert a new nonleaf entry into the parent node, to describe the newly
createdleaf. Iftheparenthasspaceforthisentry,atallhigherlevels,weonlyneedto
updatetheCFentriestoreflecttheadditionof‘Ent’. Ingeneral,however,wemayhave
tosplittheparentaswell,andsoonuptotheroot. Iftherootissplit,thetreeheight
increasesbyone.
4. A Merging Refinement: Splits are caused by the page size, which is independent of
theclusteringpropertiesofthedata. Inthepresenceofskeweddatainputorder,this
canaffecttheclusteringquality,andalsoreducespaceutilization. Asimpleadditional
mergingstepoftenhelpsamelioratetheseproblems: Supposethatthereisaleafsplit,
andthepropagationofthissplitstopsatsomenonleafnodeN ,i.e.,N canaccommo-
j j
datetheadditionalentryresultingfromthesplit. WenowscannodeN tofindthetwo
j
closestentries. Iftheyarenotthepaircorrespondingtothesplit,wetrytomergethem
andthecorrespondingtwochildnodes. Iftherearemoreentriesinthetwochildnodes
than one page can hold, we split the merging result again. During the resplitting, in
caseoneoftheseedsattractsenoughmergedentriestofillapage,wejustputtherestof
theentrieswiththeotherseed. Insummary,ifthemergedentriesfitonasinglepage,
we free a node (page) for later use and create space for one more entry in node N ,
j
therebyincreasingspaceutilizationandpostponingfuturesplits;otherwiseweimprove
thedistributionofentriesintheclosesttwochildren.
TheabovestepsworktogethertodynamicallyadjusttheCF-treetoreduceitssensitivityto
thedatainputordering.

150 ZHANG,RAMAKRISHNANANDLIVNY
4.4. Anomalies
Since each node can only hold a limited number of entries due to its fixed size, it does
notalwayscorrespondtoanaturalcluster. Occasionally,twosubclustersthatshouldhave
beeninoneclusteraresplitacrossnodes. Dependingupontheorderofdatainputandthe
degreeofskew,itisalsopossiblethattwosubclustersthatshouldnotbeinoneclusterare
keptinthesamenode. Thisinfrequentbutundesirableanomalycausedbynodesizelimit
(Anomaly1)willbeaddressedwithaglobalclusteringalgorithmdiscussedinSection5.
Anotherundesirableartifactisthatifthesamedatapointisinsertedtwice,butatdifferent
times, the two copies might be entered into two distinct leaf entries. In other words,
occasionally with a skewed input order, a point might enter a leaf entry that it should
nothaveentered(Anomaly2). Thisproblemwillbeaddressedwitharefiningalgorithm
discussedinSection5.
4.5. RebuildingAlgorithm
WenowdiscusshowtorebuildtheCF-treebyincreasingthethresholdiftheCF-treesize
limitisexceededasdatapointsareinserted. Assumethatt isaCF-treeofthresholdT .
i i
Itsheightish,anditssize(numberofnodes)isS . GivenT ‚ T ,wewanttouseall
i i+1 i
theleafentriesoft torebuildaCF-tree,t ,ofthresholdT suchthatthesizeoft
i i+1 i+1 i+1
shouldnotbelargerthanS .
i
AssumethatwithineachnodeofCF-treet ,theentriesarelabeledcontiguouslyfrom0
i
ton ¡1, wheren isthenumberofentriesinthatnode. Thenapathfromanentryin
k k
theroot(Level1)toaleafnode(Levelh)canbeuniquelyrepresentedby(i 1 ;i 2 ;:::;i h¡1 ),
wherei ;j =1;:::;h¡1isthelabelofthej-thlevelentryonthatpath. Sonaturally,path
j
(i(1);i(1);:::;i(1) )isbefore(or<)path(i(2);i(2);:::;i(2) )ifi(1) =i(2),...,i(1) =i(2) ,
1 2 h¡1 1 2 h¡1 1 1 j¡1 j¡1
and i(1) < i(2)(0 • j • h ¡ 1). It is obvious that each leaf node corresponds to a
j j
path,sincewearedealingwithtreestructures,andwewilljustuse‘path’and‘leafnode’
interchangeablyfromnowon.
TheideaoftherebuildingalgorithmisillustratedinFigure1. Withthenaturalpathorder
definedabove,itscansandfreestheoldtree,pathbypath,andatthesametime,createsthe
new tree path by path. The new tree starts with NULL, and ‘OldCurrentPath’ is initially
theleftmostpathintheoldtree.
1. Create the corresponding ‘NewCurrentPath’ in the new tree: Copy the nodes along
‘OldCurrentPath’intheoldtreeintothenewtreeasthe(current)rightmostpath;call
this‘NewCurrentPath’.
2. Insertleafentriesin‘OldCurrentPath’tothenewtree: Withthenewthreshold,each
leaf entry in ‘OldCurrentPath’ is tested against the new tree to see if it can either be
absorbed by an existing leaf entry, or fit in as a new leaf entry without splitting,
in the ‘NewClosestPath’ that is found top-down with the closest criteria in the new
tree. If yes and ‘NewClosestPath’ is before ‘NewCurrentPath’, then it is inserted to
‘NewClosestPath’,anddeletedfromtheleafnodein‘NewCurrentPath’.

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 151
Old Tree New Tree
Freed Created
OldCurrentPath NewClosestPath NewCurrentPath
Figure1.RebuildingCF-tree
3. Freespacein‘OldCurrentPath’and‘NewCurrentPath’: Onceallleafentriesin‘Old-
CurrentPath’areprocessed,thenodesalong‘OldCurrentPath’canbedeletedfromthe
oldtree. Itisalsolikelythatsomenodesalong‘NewCurrentPath’areemptybecause
leaf entries that originally corresponded to this path have been ‘pushed forward’. In
thiscasetheemptynodescanbedeletedfromthenewtree.
4. Processthenextpathintheoldtree: ‘OldCurrentPath’issettothenextpathintheold
treeiftherestillexistsone,andtheabovestepsarerepeated.
Fromtherebuildingsteps,itisclearthatallleafentriesintheoldtreearere-insertedinto
thenewtree,butthenewtreecanneverbecomelargerthantheoldtree. Sinceonlynodes
correspondingto‘OldCurrentPath’and‘NewCurrentPath’needtoexistsimultaneouslyin
bothtrees,themaximumextraspaceneededforthetreetransformationish(heightofthe
oldtree)pages. SobyincreasingthethresholdvalueT,wecanrebuildasmallerCF-tree
with a very limited amount of extra memory. The following theorem summarizes these
observations.
ReducibilityTheorem : AssumewerebuildCF-treet ofthresholdT fromCF-tree
i+1 i+1
t ofthresholdT bytheabovealgorithm,andletS andS bethesizesoft andt
i i i i+1 i i+1
respectively. IfT ‚ T ,thenS • S ,andthetransformationfromt tot needs
i+1 i i+1 i i i+1
atmosthextrapagesofmemory,wherehistheheightoft .
i
5. TheBIRCHClusteringAlgorithm
Figure 2 presents the overview of BIRCH. It consists of four phases: (1) Loading, (2)
OptionalCondensing,(3)GlobalClustering,and(4)OptionalRefining.
ThemaintaskofPhase1istoscanalldataandbuildaninitialin-memoryCF-treeusing
thegivenamountofmemoryandrecyclingspaceondisk. ThisCF-treetriestoreflectthe
clusteringinformationofthedatasetinasmuchdetailaspossiblesubjecttothememory
limits. Withcrowdeddatapointsgroupedintosubclusters,andsparsedatapointsremoved
asoutliers, thisphasecreatesanin-memorysummaryofthedata. MoredetailsofPhase

152 ZHANG,RAMAKRISHNANANDLIVNY
Data
Phase1: Load into memory by building a CF tree
Initial CF tree
Phase 2 (optional): Condense into desirable range
by building a smaller CF tree
smaller CF tree
Phase 3: Global Clustering
Good Clusters
Phase 4: (optional and off line) : Cluster Refining
Better Clusters
Figure2.BIRCHOverview
1willbediscussedinSection5.1. AfterPhase1,subsequentcomputationsinlaterphases
willbe: (1)fastbecause(a)noI/Ooperationsareneeded,and(b)theproblemofclustering
the original data is reduced to a smaller problem of clustering the subclusters in the leaf
entries; (2)accuratebecause (a) outliers can be eliminated, and (b)the remaining datais
describedatthefinestgranularitythatcanbeachievedgiventheavailablememory;(3)less
order sensitive because the leaf entries of the initial tree form an input order containing
betterdatalocalitycomparedwiththearbitraryoriginaldatainputorder.
Oncealltheclusteringinformationisloadedintothein-memoryCF-tree,wecanusean
existingglobalorsemi-globalalgorithminPhase3toclusteralltheleafentriesacrossthe
boundariesofdifferentnodes. ThiswaywecanovercomeAnomaly1,(Section4.4)which
causestheCF-treenodestobeunfaithfultotheactualclustersinthedata. Weobservethat
existingclusteringalgorithms(e.g.,HC,KMEANSandCLARANS)thatworkwithaset
ofdatapointscanbereadilyadaptedtoworkwithasetofsubclusters,eachdescribedby
itsCFentry.
Weadaptedanagglomerativehierarchicalclusteringalgorithmbasedonthedescription
in (Olson,1993). It is applied to the subclusters represented by their CF entries. It has
a complexity of O(m2), where m is the number of subclusters. If the distance metric
satisfiesthereducibilityproperty(Olson,1993)1,itproducesexactresults;otherwiseitstill
providesaverygoodapproximatealgorithm. Inourcase,D2andD4satisfythereducibility
propertyandtheyaretheidealmetricsforusingthisalgorithm. Besides,ithastheflexibility
ofallowingtheusertoexploredifferentnumberofclusters(K),ordifferentdiameter(or

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 153
radius)thresholdsforclusters(T)basedontheformedhierarchywithoutre-scanningthe
dataorre-clusteringthesubclusters.
Phase2isanoptionalphase. Withexperimentation,wehaveobservedthattheglobalor
semi-global clustering methods that we adapt in Phase 3 have different input size ranges
within which they perform well in terms of both speed and quality. For example, if we
choosetoadaptCLARANSinPhase3,weknowthatCLARANSperformsprettywellfora
setoflessthan5000dataobjects. Thatisbecausewithinthatrange,frequentdatascanning
isacceptableandgettingtrappedataverybadlocalminimalduetothepartialsearchingis
notverylikely. SopotentiallythereisagapbetweenthesizeofPhase1resultsandthebest
performancerangeofthePhase3algorithmweselect. Phase2servesasacushionbetween
Phase 1 and Phase 3 and bridges this gap: we scan the leaf entries in the initial CF-tree
to rebuild a smaller CF-tree, while removing more outliers and grouping more crowded
subclustersintolargerones.
AfterPhase3,weobtainasetofclustersthatcapturesthemajordistributionpatternsin
the data. However, minor and localized inaccuracies might exist because of (1) the rare
misplacementproblem(Anomaly2inSection4.4),and(2)thefactthatPhase3isapplied
on a coarse summary of the data. Phase 4 is optional and entails the cost of additional
passesoverthedatatocorrectthoseinaccuraciesandrefinetheclustersfurther. Notethat
uptothispoint,theoriginaldatahasonlybeenscannedonce,althoughthetreemayhave
beenrebuiltmultipletimes.
Phase4usesthecentroidsoftheclustersproducedbyPhase3asseeds,andredistributes
thedatapointstoitsclosestseedtoobtainasetofnewclusters. Notonlydoesthisallow
pointsbelongingtoaclustertomigrate, butalsoitensuresthatallcopiesofagivendata
pointgotothesamecluster. Phase4canbeextendedwithadditionalpassesifdesiredby
theuser,andithasbeenprovedtoconvergetoaminimum(GershoandGray,1992). Asa
bonus,duringthispass,eachdatapointcanbelabeledwiththeclusterthatitbelongsto,if
wewishtoidentifythedatapointsineachcluster. Phase4alsoprovidesuswiththeoption
ofdiscardingoutliers. Thatis,apointwhichistoofarfromitsclosestseedcanbetreated
asanoutlierandnotincludedintheresult.
5.1. Phase1Revisited
Figure 3 shows the details of Phase 1. It starts with an initial threshold value, scans the
data,andinsertspointsintothetree. Ifitrunsoutofmemorybeforeitfinishesscanningthe
data,itincreasesthethresholdvalue,andrebuildsanew,smallerCF-tree,byre-inserting
theleafentriesoftheoldCF-treeintothenewCF-tree. Afteralltheoldleafentrieshave
beenre-inserted,thescanningofthedata(andinsertionintothenewCF-tree)isresumed
fromthepointatwhichitwasinterrupted.
5.1.1. ThresholdHeuristic
A good choice of threshold value can greatly reduce the number of rebuilds. Since the
initialthresholdvalueT isincreaseddynamically,wecanadjustforitsbeingtoolow. But
0

154 ZHANG,RAMAKRISHNANANDLIVNY
Start CF tree t1 of Initial T
Continue scanning data and insert to t1
Out of memory Finish scanning data
Result?
(1) Increase T.
(2) Rebuild CF tree t2 of new T from CF tree t1:
if a leaf entry of t1 is potential outlier and disk space available,
write to disk; otherwise use it to rebuild t2.
(3) t 1 <- t2.
otherwise Out of disk space
Result?
Re-absorb potential outliers into t1
Re-absorb potential outliers into t1
Figure3.FlowChartofPhase1
iftheinitialT istoohigh,wewillobtainalessdetailedCF-treethanisfeasiblewiththe
0
availablememory. SoT shouldbesetconservatively. BIRCHsetsittozerobydefault;a
0
knowledgeableusercouldchangethis.
SupposethatT turnsouttobetoosmall,andwesubsequentlyrunoutofmemoryafter
i
N datapointshavebeenscanned. Basedontheportionofthedatathatwehavescanned
i
and the CF-tree that we have built up so far, we try to estimate the next threshold value
T . This estimation is a difficult problem, and a full solution is beyond the scope of
i+1
thispaper. Currently,weusethefollowingmemory-utilizationorientedheuristicapproach:
IfthecurrentCF-treeoccupiesallthememory, weincreasethethresholdvaluetobethe
average of the distances between all the ‘nearest pairs’ of leaf entries. So on average,
approximatelytwoleafentrieswillbemergedintoonewiththenewthresholdvalue. For
efficiency reasons, the distance of each ‘nearest pair’ of leaf entries is approximated by
searchingonlywithinthesameleafnodelocally(insteadofsearchingalltheleafentries
globally). WiththeCF-treeinsertionalgorithm,itisverylikelythatthenearestneighbor
ofaleafentryiswithinthesameleafnodeasthatleafentryis.
There are several advantages of estimating the threshold value this way: (1) the new
CF-tree, whichisrebuiltfromthecurrentCF-tree, willoccupyapproximatelyhalfofthe
memory,leavingtheotherhalfforaccommodatingadditionalincomingdatapoints. Sono
matter how the incoming data is distributed or is input, the memory utilization is always

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 155
maintainedapproximatelyat50%;and(2)onlythedistributionoftheseendata,whichis
stored in the current CF-tree, is needed in the estimation. However, more sophisticated
solutionstothethresholdestimationproblemshouldbestudiedinthefuture.
5.1.2. Outlier-HandlingOption
Optionally, wecanallocateR bytesofdiskspaceforhandlingoutliers. Outliersareleaf
entriesoflowdensitythatarejudgedtobeunimportantwithrespecttotheoverallclustering
pattern. WhenwerebuildtheCF-treebyre-insertingtheoldleafentries,thesizeofthenew
CF-tree is reduced in two ways. First, we increase the threshold value, thereby allowing
each leaf entry to ‘absorb’ more points. Second, we treat some leaf entries as potential
outliersandwritethemouttodisk. Anoldleafentryisconsideredtobeapotentialoutlier
ifithas‘farfewer’datapointsthantheaverage. ‘Farfewer’isofcourseanotherheuristic.
Periodically,thediskspacemayrunout,andthepotentialoutliersarescannedtocheck
iftheycanbere-absorbedintothecurrenttreewithoutcausingthetreetogrowinsize;an
increaseinthethresholdvalueorachangeinthedistributionduetothenewdatareadaftera
potentialoutlieriswrittenoutcouldwellmeanthatthepotentialoutliernolongerqualifies
asanoutlier. Whenalldatahasbeenscanned,thepotentialoutliersleftintheoutlierdisk
spacemustbescannedtoverifyiftheyareindeedoutliers. Ifapotentialoutliercannotbe
absorbedatthislastchance,itisverylikelyarealoutlierandshouldberemoved.
Note that the entire cycle — insufficient memory triggering a rebuilding of the tree,
insufficient disk space triggering a re-absorbing of outliers, etc. — could be repeated
severaltimesbeforethedatasetisfullyscanned. Thiseffortmustbeconsideredinaddition
tothecostofscanningthedatainordertoassessthecostofPhase1accurately.
5.1.3. Delay-SplitOption
Whenwerunoutofmainmemory,itmaywellbethecasethatstillmoredatapointscan
fitinthecurrentCF-treewithoutchangingthethreshold. However,someofthedatapoints
thatwereadmayrequireustosplitanodeintheCF-tree, Asimpleideaistowritesuch
datapointstodiskinamannersimilartohowoutliersarewritten,andtoproceedreading
thedatauntilwerunoutofdiskspaceaswell. Theadvantageofthisapproachisthatin
general,moredatapointscanfitinthetreebeforewehavetorebuild.
5.2. MemoryManagement
WehaveobservedthattheamountofmemoryneededforBIRCHtofindagoodclustering
fromagivendatasetisdeterminednotbythedatasetsize,butbythedatadistribution. On
theotherhand,theamountofmemoryavailabletoBIRCHisdeterminedbythecomputing
system. Soitisverylikelythatthememoryneededandthememoryavailabledonotmatch.
Ifthememoryavailableislessthanthememoryneeded,thenBIRCHcantraderunning
timeformemory. Specifically,inPhases1through3,ittriestousealltheavailablememory

156 ZHANG,RAMAKRISHNANANDLIVNY
togeneratethesubclustersthatisasfineasthememoryallows,butinPhase4,byrefining
the clustering a few more passes, it can compensate for the inaccuracies caused by the
coarsenessduetoinsufficientmemoryinPhases1.
If the memory available is more than the memory needed, then BIRCH can cluster the
givendatasetonmultiplecombinationsofattributesconcurrentlywhilesharingthesame
scan of the dataset. So the total available memory will be divided and allocated to the
clustering process of each combination of attributes accordingly. This gives the user the
chanceofexploringthesamedatasetfrommultipleperspectivesconcurrentlyiftheavailable
resourcesallowthis.
6. PerformanceStudies
6.1. Analysis
FirstweanalyzethecpucostofPhase1. GiventhememoryisM bytesandeachpageisP
bytes,themaximumsizeofthetreeis M. Toinsertapoint,weneedtofollowapathfrom
P
roottoleaf,touchingabout1+log M nodes. AteachnodewemustexamineBentries,
B P
lookingforthe‘closest’one;thecostperentryisproportionaltothedimensiond. Sothe
costforinsertingalldatapointsisO(d⁄N ⁄B(1+log M)). Incasewemustrebuild
B P
thetree,letC ⁄dbetheCFentrysizewhereCissomeconstantmappingdimensioninto
CF entry size. There are at most M leaf entries to re-insert, so the cost of re-inserting
C⁄d
leafentriesisO(d⁄ M ⁄B(1+log M)). Thenumberoftimeswehavetore-buildthe
C⁄d B P
treedependsuponourthresholdheuristic. Currently,itisaboutlog N ,wherethevalue2
2 N0
arisesfromthefactthatwealwaysbringthetreesizedowntoabouthalfsize,andN isthe
0
numberofdatapointsloadedintomemorywiththresholdT . SothetotalcpucostofPhase
0
1isO(d⁄N ⁄B(1+log M)+log N ⁄d⁄ M ⁄B(1+log M)). SinceB equals
B P 2 N0 C⁄d B P
P ,thetotalcpucostofPhase1canbefurtherrewrittenasO(N ⁄ P(1+log M)+
C⁄d C C P ⁄d P
log N ⁄ M ⁄ P(1+log M))TheanalysisofPhase2cpucostissimilar,andhence
2 N0 C⁄d C C P ⁄d P
omitted.
AsforI/O,wescanthedataonceinPhase1andnotatallinPhase2. Withtheoutlier-
handlingandsplit-delayingoptionson,thereissomecostassociatedwithwritingoutoutlier
entriestodiskandreadingthembackduringarebuilt. Consideringthattheamountofdisk
availableforoutlier-handlingandsplit-delayingisnottoomuch, andthatthereareabout
log N rebuilds, the I/O cost of Phase 1 is not significantly different from the cost of
2 N0
readinginjusttheoriginaldataset.
ThereisnoI/OinPhase3. SincetheinputtoPhase3isbounded,thecpucostofPhase
3 is therefore bounded by a constant that depends upon the maximum input size range
andtheglobalalgorithmchosenforthisphase. Basedontheaboveanalysis—whichis
actuallyratherpessimisticforB,numberofleafentriesandthetreesizeinthelightofour
experimentalresults—thecostofPhases1,2and3shouldscaleuplinearlywithN.
Phase4scansthedatasetagainandputseachdatapointintothepropercluster;thetime
taken is proportional to N ⁄K. However using the newest nearest neighbor techniques
proposed in (Huang,etal.,1992), for each of the N data point, instead of looking all K

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 157
Table1.DataGenerationParametersandTheirValuesorRangesExperimented
Parameter ValuesorRanges
Dimensiond 2..50
Pattern grid,sine,random
NumberofclustersK 4..256
nl(Lowern) 0..2500
nh(Highern) 50..p2500
rl(Lowerr) 0p.. p50
rh(Higherr) 2.. 50
Distancemultiplierkg 4(gridonly)
Numberofcyclesnc 4(sineonly)
Noiseratern(%) 0..10
Inputordero randomized,ordered
clustercenterstofindthenearestone, itonlylooksthoseclustercentersthatarearound
thedatapoint. Thisway,Phase4canbeimprovedquiteabit.
6.2. SyntheticDatasetGenerator
TostudythesensitivityofBIRCHtothecharacteristicsofawiderangeofinputdatasets,
wehaveusedacollectionofsyntheticdatasets. Thesyntheticdatagenerationiscontrolled
byasetofparametersthataresummarizedinTable1.
EachdatasetconsistsofKclustersofd-dimensionaldatapoints. Aclusterischaracterized
bythenumberofdatapointsinit(n),itsradius(r),anditscenter(c). nisintherange[n ,n ],
l h
andr isintherange[r ,r ]. (Notethatwhenn = n thenumberofpointsisfixed,and
l h l h
whenr =r theradiusisfixed.) Onceplaced,theclusterscoverarangeofvaluesineach
l h
dimension. Werefertotheserangesasthe‘overview’ofthedataset.
Thelocationofthecenterofeachclusterisdeterminedbythepatternparameter. Three
patterns—grid,sine,andrandom—arecurrentlysuppoprtedbypthegenerator. Whenthe
grid pattern is used, the cluster centers are placed on a K £ K grid. The distance
betweenthecentersofneighboringclustersonthesamerow/columniscontrolledbyk ,
p g
andissettok
g
(rl+
2
rh). Thisleadstoanoverviewof[0, Kk
g
rl+
2
rh]onbothdimensions.
Thesinepatternplacestheclustercentersonacurveofsinefunction. TheK clustersare
dividedinton groups,eachofwhichisplacedonadifferentcycleofthesinefunction. The
c
xlocationofthecenterofclusteriis2…iwhereastheylocationis K⁄sine(2…i=(K)). The
nc nc
overviewofasinedatasetistherefore[0,2…K]and[¡K,+K]onthexandy directions
nc nc
respectively. Therandompatternplacestheclustercentersrandomly. Theoverviewofthe
datasetis[0,K]onbothdimensionssincethethexandylocationsofthecentersareboth
randomlydistributedwithintherange[0,K].
Oncethecharacteristicsofeachclusteraredetermined,thedatapointsfortheclusterare
generatedaccordingtoad-dimensionalindependentnormaldistributionwhosemeanisthe
center c, and whose variance in each dimension is r2 . Note that due to the properties of
d
anormaldistribution,themaximumdistancebetweenapointintheclusterandthecenter
is unbounded. In other words, a point may be arbitrarily far from the cluster to which it

| 158 |     | ZHANG,RAMAKRISHNANANDLIVNY |     |
| --- | --- | -------------------------- | --- |
Table2.BIRCHParametersandTheirDefaultValues
| Scope  | Parameter        |     | DefaultValue    |
| ------ | ---------------- | --- | --------------- |
| Global | Memory(M)        |     | 5%ofdatasetsize |
|        | Disk(R)          |     | 20%M            |
|        | Distancedef.     |     | D2              |
|        | Qualitydef.      |     | D„              |
|        | Thresholddef.    |     | thresholdforD   |
| Phase1 | Initialthreshold |     | 0.0             |
|        | Delay-split      |     | on              |
|        | Pagesize(P)      |     | 1024bytes       |
|        | Outlier-handling |     | off             |
| Phase3 | Inputrange       |     | 1000            |
|        | Algorithm        |     | AdaptedHC       |
| Phase4 | Refinementpass   |     | 1               |
|        | Discard-outlier  |     | off             |
‘belongs’,accordingtothedatagenerationalgorithm. Soadatapointthatbelongstocluster
A may be closer to the center of cluster B than to the center of A, and we refer to such
pointsas‘outsiders’.
In addition to the clustered data points, noise in the form of data points uniformly dis-
tributedthroughouttheoverviewofthedatasetcanbeaddedtothedataset. Theparameter
r controlsthepercentageofdatapointsinthedatasetthatareconsiderednoise.
n
The placement of the data points in the dataset is controlled by the order parameter
o. When the randomized option is used, the data points of all clusters and the noise are
randomized throughout the entire dataset. Whereas when the ordered option is selected,
thedatapointsofaclusterareplacedtogether,theclustersareplacedintheordertheyare
generated,andthenoiseisplacedattheend.
6.3. ParametersandDefaultSetting
BIRCHiscapableofworkingundervarioussettings. Table2liststheparametersofBIRCH,
their effecting scopes and their default values. Unless specified explicitly otherwise, an
experimentisconductedunderthisdefaultsetting.
M was selected to be about 5% of the dataset size in the base workload used in our
experiments. Since disk space (R) is just used for outliers, we assume that R < M and
setR = 20%ofM. Theexperimentsontheeffectsofthe5distancemetricsinthefirst3
phases(Section6.6)indicatethat(1)usingD3inPhases1and2resultsinamuchhigher
endingthreshold, andhenceproducesclustersofpoorerquality; (2)however, thereisno
distinctiveperformancedifferenceamongtheothers. WethereforedecidedtochooseD2
asdefault. FollowingStatisticstradition,wechose‘weightedaveragediameter’(denoted
| asD„)asthequalitymetric. | ThesmallerD„ | is,thebetterthequalityis. |     |
| ------------------------ | ------------ | ------------------------- | --- |
Thethresholdisdefinedasathresholdforclusterdiameter. InPhase1,theinitialthreshold
issetto0,thedefaultvalue. Basedonastudyofhowpagesizeaffectsperformance(Section
6.6),weselectedP =1024. Thedelay-splitoptionisusedforbuildingmorecompactCF-
trees. Theoutlier-handlingoptionisnotused,forsimplicity.

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 159
Table3.DatasetsUsedasBaseWorkload
DS GeneratorSetting D„ int
1 d=2;gridp;K=100;nl=nh=1000,
rl=rh= 2;kg =4;rn=0%;o=randomized 2.00
2 d=2;sinep;K=100;nl=nh=1000,
rl=rh= 2;nc=4;rn=0%;o=randomized 2.00
3 d=2;random;K=100;nl=0;nh=2000,
rl=0;rh=4;rn=rn=0%;o=randomized 4.18
In Phase 3, most global algorithms can handle a few thousand objects well. So we set
theinputrangetobe1000asadefault. WehavechosentheadaptedHCalgorithmtouse
here. WedecidedtoletPhase4refinetheclustersonlyoncewithitsdiscard-outlieroption
off,sothatalldatapointswillbecountedinthequalitymeasurementforfaircomparisons
withothermethods.
6.4. BaseWorkloadPerformance
ThefirstsetofexperimentswastoevaluatetheabilityofBIRCHtoclusterlargedatasets
ofvariouspatternsandinputorders. Allthetimesarepresentedinsecondsinthispaper.
Three 2-dimensional synthetic datasets, one for each pattern, were used; 2-dimensional
datasetswerechoseninpartbecausetheyareeasytovisualize. Table3presentsthedata
generationsettingsforthem. TheweightedaveragediametersoftheintendedclustersD„
int
arealsoincludedinthetableasroughqualityindicationsofthedatasets. Notethatfrom
nowon,werefertotheclustersgeneratedbythegeneratorasthe‘intendedclusters’,and
theclustersidentifiedbyBIRCHas‘BIRCHclusters’.
Figure 4 visualizes the intended clusters of DS1 by plotting a cluster as a circle whose
centeristhecentroid,radiusistheclusterradius,andlabelisthenumberofpointsinthe
cluster. TheBIRCHclustersofDS1arepresentedinFigure7. WeobservethattheBIRCH
clustersareverysimilartotheintendedclustersintermsoflocation,numberofpoints,and
radii. Themaximumandaveragedistancebetweenthecentroidsofanintendedclusterand
itscorrespondingBIRCHclusterare0.17and0.07respectively. Thenumberofpointsina
BIRCHclusterisnomorethan5%differentfromthecorrespondingintendedcluster. The
radiioftheBIRCHclusters(rangingfrom1.25to1.40withanaverageof1.32)areclose
to, those of the intended clusters (1.41). Note that all the BIRCH radii are smaller than
the intended radii. This is because BIRCH assigns the ‘outsiders’ of an intended cluster
to a proper BIRCH cluster. Similar conclusions can be reached by analyzing the visual
presentationsoftheintendedclustersandBIRCHclustersforDS2(Figure510).
As summarized in Table 4, it took BIRCH less than 15 seconds (on a DEC Pentium-
prostationrunningSolaris)tocluster100,000datapointsofeachdataset,whichincludes
2 scans of the dataset (about 1.16 seconds for one scan of ASCII file from disk). The
pattern of the dataset had almost no impact on the clustering time. Table 4 also presents
theperformanceresultsforthreeadditionaldatasets—DS1o, DS2oandDS3o—which
correspondtoDS1,DS2andDS3,respectivelyexceptthattheparameteroofthegenerator

| 160 |     | ZHANG,RAMAKRISHNANANDLIVNY |     |
| --- | --- | -------------------------- | --- |
Figure4.IntendedClustersofDS1
Figure5.IntendedClustersofDS2
Table4.BIRCHPerformanceonBaseWorkloadwithrespecttoTime,D„,InputOrderand#ScanofData
| DS Time | D„ #Scan | D Time  | D„ #Scan |
| ------- | -------- | ------- | -------- |
| 1 11.5  | 1.87 2   | 1o 13.6 | 1.87 2   |
| 2 10.7  | 1.99 2   | 2o 12.1 | 1.99 2   |
| 3 11.4  | 3.95 2   | 3o 12.2 | 3.99 2   |
is set to ordered. As demonstrated in Table 4, changing the order of the data points had
almostnoimpactontheperformanceofBIRCH.
6.5. ComparisonsofBIRCH,CLARANSandKMEANS

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 161
Figure6.IntendedClustersofDS3
Figure7.BIRCHClustersofDS1
Table5.CLARANSPerformanceonBaseWorkloadwithrespecttoTime,D„,InputOrderand#ScanofData
| DS Time | D„ #Scan  | DS Time | D„ #Scan  |
| ------- | --------- | ------- | --------- |
| 1 932   | 2.10 3307 | 1o 794  | 2.11 2854 |
| 2 758   | 2.63 2661 | 2o 816  | 2.31 2933 |
| 3 835   | 3.39 2959 | 3o 934  | 3.28 3369 |
Table6.KMEANSPerformanceonBaseWorkloadwithrespecttoTime,D„,InputOrderand#ScanofData
|         | D„       |         | D„       |
| ------- | -------- | ------- | -------- |
| DS Time | #Scan    | DS Time | #Scan    |
| 1 43.9  | 2.09 289 | 1o 33.8 | 1.97 197 |
| 2 13.2  | 4.43 51  | 2o 12.7 | 4.20 29  |
| 3 32.9  | 3.66 187 | 3o 36.0 | 4.35 241 |

162 ZHANG,RAMAKRISHNANANDLIVNY
Figure8.CLARANSClustersofDS1
Inthisexperiment,wecomparetheperformanceofBIRCH,CLARANSandKMEANSon
thebaseworkload. Firstofall,inCLARANSandKMEANS,thememoryisassumedto
belargeenoughtoholdthewholedatasetaswellassomeotherlinearsizeassistingdata
structures. SotheyneedmuchmorememorythanBIRCHdoes. (Clearly,thisassumption
greatlyfavorsthesetwoalgorithmsintermsoftherunningtimecomparison!) Second,the
CLARANSimplementationwasprovidedbyRaymondNg,andtheKMEANSimplemen-
tationwasdonebyusbasedonthealgorithmpresentedin(HartiganandWong,1979),with
theinitialseedsselectedrandomly. WehaveobservedthattheperformancesofCLARANS
and KMEANS are very sensitive to the random number generator used. A bad random
numbergenerator,suchastheUNIX‘rand()’usedintheoriginalcodeofCLARANS,can
generate random numbers that are not really random but sensitive to the data order, and
hencemakeCLARANSandKMEANS’sperformanceextremelyunstablewiththedifferent
input orders. So to avoid this problem, we have replaced ‘rand()’ with a more elaborate
randomnumbergenerator. Third,inorderforCLARANStostopafteranacceptablerun-
ningtime,wesetitsmaxneighborvaluetobethelargerof50(insteadof250)and1.25%
ofK(N-K),butnomorethan100(newlyenforcedupperlimitrecommendedbyNg). Its
numlocalvalueisstill2,asin(NgandHan,1994).
Figure 8 and 9 visualize the CLARANS and KMEANS clusters for DS1. Comparing
themwiththeintendedclustersforDS1,weobservethat: (1)Thepatternofthelocationof
theclustercentersisdistorted. (2)ThenumberofdatapointsinaCLARANSorKMEANS
clustercanbeasmanyas40%differentfromthenumberintheintendedcluster. (3)The
radiiofCLARANSclustersvarieslargelyfrom1.15to1.94withanaverageof1.44(larger
thanthoseoftheintendedclusters,1.41). TheradiiofKMEANSclustersvarieslargelyfrom
0.99to2.02withanaverageof1.38(largerthanthoseofBIRCHclusters,1.32). Similar
behavior can be observed in the visualization of CLARANS and KMEANS clusters for
DS2.
Tables5and6summarizetheperformanceofCLARANSandKMEANS.Forallthree
datasetsofthebaseworkload,(1)Theyscanthedatasetfrequently. WhenrunningCLARANS

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 163
Figure9.KMEANSClustersofDS1
Figure10.BIRCHClustersofDS2
and KMEANS experiments, all data are loaded into memory, only the first scan is from
ASCIIfileondisk,andtheremainingscansareinmemory. Consideringthetimeneededfor
eachscanondisk(1.16secondsperscan),CLARANSandKMEANSaremuchslowerthan
BIRCHandtheirrunningtimesaremoresensitivetothepatternsofthedataset. (2)The
D„ valuesfortheCLARANSandKMEANSclustersarelargerthanthosefortheBIRCH
clustersforDS1andDS2. Thatmeanseventhroughtheyspentalotoftimesearchingfora
localminimalpartition,thepartitionmaynotbeasgoodasthenon-minimalpartitionfound
byBIRCH.(3)TheresultsforDS1o,DS2o,andDS3oshowthatifthedatapointsareinput
indifferentorders,thetimeandqualityofCLARANSandKMEANSclusterswillchange.
In conclusion, for the base workload, BIRCH uses much less memory, scans data only
twice,butrunsfaster,isbetteratescapingfrominferiorlocallyminimalpartitions,andless
order-sensitivecomparedwithCLARANSandKMEANS.

164 ZHANG,RAMAKRISHNANANDLIVNY
Figure11.CLARANSClustersofDS2
Figure12.KMEANSClustersofDS2
6.6. SensitivitytoParameters
WestudiedthesensitivityofBIRCH’sperformancetoseveralparameters. Duetolackof
space,weonlypresentsomemajorconclusions.
Initialthreshold: (1)BIRCH’sperformanceisstableaslongastheinitialthresholdis
notexcessivelyhighwithrespecttothedataset. (2)T =0:0workswellwithalittleextra
0
runningtime. (3)IfauserdoesknowagoodT ,thenshe/hecanberewardedbysavingup
0
to10%ofthetime.
Page Size P: In Phase 1, smaller (larger) P tends to decrease (increase) the running
time, requires higher (lower) ending threshold, produces less (more) but ‘coarser (finer)’
leaf entries, and hence degrades (improves) the quality. However, with the refinement in
Phase 4, the experiments suggest that for P = 256 to 4096, although the qualities at the
endofPhase3aredifferent,thefinalqualitiesaftertherefinementarealmostthesame.

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 165
Figure13.BIRCHClustersofDS3
Figure14.CLARANSClustersofDS3
OutlierOptions: BIRCHwastestedon‘noisy’datasetswithalltheoutlieroptionson,
andoff. Theresultsshowthatwithalltheoutlieroptionson,BIRCHisnotslowerbutfaster,
andatthesametime,itsqualityismuchbetter.
Memory Size: In Phase 1, as memory size (or the maximum tree size) increases, (1)
therunningtimeincreasesbecauseofprocessingalargertreeperrebuild,butonlyslightly
becauseitisdoneinmemory;(2)morebutfinersubclustersaregeneratedtofeedthenext
phase, and hence this results in better quality; (3) the inaccuracy caused by insufficient
memory can be compensated to some extent by Phase 4 refinements. In other words,
BIRCHcantradeoffmemoryversustimetoachievesimilarfinalquality.
6.7. Scalability

| 166 |     | ZHANG,RAMAKRISHNANANDLIVNY |     |
| --- | --- | -------------------------- | --- |
Table7.QualityStabilitywithrespecttoIncreasingNumberofPointsperCluster
| DS  | ninn2[nl::nh] | N   | D„=D„ |
| --- | ------------- | --- | ----- |
int
| 1   | 50..50     | 5000   | 1.87/1.99 |
| --- | ---------- | ------ | --------- |
|     | 100..100   | 10000  | 1.92/2.01 |
|     | 250..250   | 25000  | 1.87/1.99 |
|     | 500..500   | 50000  | 1.86/1.98 |
|     | 750..750   | 75000  | 1.88/2.00 |
|     | 1000..1000 | 100000 | 1.87/2.00 |
|     | 2500..2500 | 250000 | 1.88/2.00 |
| 2   | 50..50     | 5000   | 1.98/1.98 |
|     | 100..100   | 10000  | 2.00/2.00 |
|     | 250..250   | 25000  | 2.00/2.00 |
|     | 500..500   | 50000  | 2.00/2.00 |
|     | 750..750   | 75000  | 1.99/1.99 |
|     | 1000..1000 | 100000 | 1.99/2.00 |
|     | 2500..2500 | 250000 | 1.99/1.99 |
| 3   | 0..100     | 5000   | 4.08/4.42 |
|     | 0..200     | 10000  | 4.30/4.78 |
|     | 0..500     | 25000  | 4.21/4.65 |
|     | 0..1000    | 50000  | 4.00/4.27 |
|     | 0..1500    | 75000  | 3.74/4.22 |
|     | 0..2000    | 100000 | 3.95/4.18 |
|     | 0..5000    | 250000 | 4.23/4.52 |
Table8.QualityStabilitywithrespecttoIncreasingNumberofClusters
| DS  | K   | N   | D„=D„ |
| --- | --- | --- | ----- |
int
| 1   | 16  | 16000  | 2.32/2.00 |
| --- | --- | ------ | --------- |
|     | 36  | 36000  | 1.98/2.00 |
|     | 64  | 64000  | 1.93/1.99 |
|     | 100 | 100000 | 1.87/2.00 |
|     | 144 | 144000 | 1.87/1.99 |
|     | 196 | 196000 | 1.87/2.00 |
|     | 256 | 256000 | 1.87/2.00 |
| 2   | 4   | 4000   | 1.98/1.99 |
|     | 40  | 40000  | 1.99/1.99 |
|     | 100 | 100000 | 1.99/2.00 |
|     | 120 | 120000 | 2.00/2.00 |
|     | 160 | 160000 | 2.00/2.00 |
|     | 200 | 200000 | 1.99/1.99 |
|     | 240 | 240000 | 1.99/1.99 |
| 3   | 5   | 5000   | 5.57/6.43 |
|     | 50  | 50000  | 4.10/4.52 |
|     | 75  | 75000  | 4.04/4.76 |
|     | 100 | 100000 | 3.95/4.18 |
|     | 150 | 150000 | 4.21/4.26 |
|     | 200 | 200000 | 5.22/4.49 |
|     | 250 | 250000 | 5.52/4.48 |

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 167
Figure15.KMEANSClustersofDS3
30
25
20
15
10
5
0
0 50000 100000 150000 200000 250000
)sdnoces(
emiT
gninnuR
DS1: Phase1-3
DS2: Phase1-3
DS3: Phase1-3
DS1: Phase1-4
DS2: Phase1-4
DS3: Phase1-4
N
Figure16.TimeScalabilitywithrespecttoIncreasingNumberofPointsperCluster
ThreedistinctwaysofincreasingthedatasetsizewereusedtotestthescalabilityofBIRCH.
IncreasingtheNumberofPointsperCluster(n): ForeachofDS1,DS2andDS3,we
createdarangeofdatasetsbykeepingthegeneratorsettingsthesameexceptforchanging
n andn tochangen,andhenceN. SinceN doesnotgrowtoofarfromthatofthebase
l h
workload,wedecidedtousethesameamountofmemoryforthesescalingexperimentsas
weusedforthebaseworkload. Thisenablesustoestimateforeachpattern,givenafixed
amount of memory, how large a dataset BIRCH can cluster while maintaining its stable

| 168 |     |     | ZHANG,RAMAKRISHNANANDLIVNY |     |     |
| --- | --- | --- | -------------------------- | --- | --- |
35
DS1: Phase1-3
DS2: Phase1-3
30
| )sdnoces( emiT gninnuR |     |     | DS3: Phase1-3 |     |     |
| ---------------------- | --- | --- | ------------- | --- | --- |
DS1: Phase1-4
25
DS2: Phase1-4
DS3: Phase1-4;
20
15
10
5
0
|     | 0 50000 | 100000 | 150000 | 200000 | 250000 |
| --- | ------- | ------ | ------ | ------ | ------ |
N
Figure17.TimeScalabilitywithrespecttoIncreasingNumberofClusters
Table9.QualityisStablewithrespecttoIncreasingDimension
| DS  |     | d(dimension) |     |     | D„=D„ |
| --- | --- | ------------ | --- | --- | ----- |
int
| 1   |     | 2   |     |     | 1.87/1.99   |
| --- | --- | --- | --- | --- | ----------- |
|     |     | 10  |     |     | 4.68/4.46   |
|     |     | 20  |     |     | 6.52/6.31   |
|     |     | 30  |     |     | 7.87/7.74   |
|     |     | 40  |     |     | 8.97/8.93   |
|     |     | 50  |     |     | 10.08/9.99  |
| 2   |     | 2   |     |     | 1.99/1.99   |
|     |     | 10  |     |     | 4.46/4.46   |
|     |     | 20  |     |     | 6.31/6.31   |
|     |     | 30  |     |     | 7.74/7.74   |
|     |     | 40  |     |     | 8.93/8.93   |
|     |     | 50  |     |     | 10.02/9.99  |
| 3   |     | 2   |     |     | 3.95/4.28   |
|     |     | 10  |     |     | 11.96/9.62  |
|     |     | 20  |     |     | 17.11/13.62 |
|     |     | 30  |     |     | 20.76/16.70 |
|     |     | 40  |     |     | 25.34/19.28 |
|     |     | 50  |     |     | 26.64/21.56 |
qualities. Based on the performance analysis in 6.1, with M, P, d, K fixed, and only N
growing,therunningtimeshouldscaleuplinearlywithN.
Followingaretheexperimentalresults. Withallthreepatternsofdatasets,theirrunning
timesforthefirst3phases,aswellasforall4phasesareplottedagainstthedatasetsizeN

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 169
70
60
50
40
30
20
10
0
0 5 10 15 20 25 30 35 40 45 50
)sdnoces(
emiT
gninnuR
DS1:Phase1-3
DS1:Phase1-4
DS2:Phase1-3
DS2:Phase1-4
DS3:Phase1-3
DS3:Phase1-4
Dimension
Figure18.TimeScalabilitywithrespecttoIncreasingDimension
inFigure16. Onecanobservethatforallthreepatternsofdatasets: (1)Thefirst3phases,
aswellasall4phasesindeedscaleuplinearlywithrespecttoN. (2)Therunningtimesfor
thefirst3phasesgrowsimilarlyforallthreepatterns. (3)Theimproved‘nearestneighbor’
algorithmusedinPhase4isslightlysensitivetoinputdatapatterns. Itworksbestforthe
sinepatternbecausethereareusuallylessclustercentersaroundadatapointinthatpattern.
Table7providesthecorrespondingqualityvaluesoftheintendedclusters(D„ )andof
int
BIRCHclusters(D„)asnandN increaseforallthreepatterns. Itisshownfromthetable
thatwiththesameamountofmemory,forawiderangeofnandN,thequalityofBIRCH
clusters (indicated by D„) is consistently close to (or better than, due to the correction of
‘outsiders’)thatoftheintendedclusters(indicatedbyD„ ).
act
IncreasingtheNumberofClusters(K):ForeachofDS1, DS2andDS3, wecreatea
rangeofdatasetsbykeepingthegeneratorsettingsthesameexceptforchangingK toN.
Again,sinceKdoesnotgrowtoofarfromthatofthebaseworkload,wedecidedtousethe
sameamountofmemoryforthesescalingexperimentsasweusedforthebaseworkload.
Therunningtimeforthefirst3phases, aswellasforall4phasesareplottedagainstthe
datasetsizeN inFigure17. (1)Again,thefirst3phasesareconfirmedtoscaleuplinearly
withrespecttoN forallthreepatterns. (2)Therunningtimesforall4phasesarelinear
in N, but have slightly different slopes for the three different patterns of datasets. More
specifically,forthegridpatterntheslopeisthelargest,andforthesinepattern,theslope
is the smallest. This is due to the fact that K and N are growing at the same time, and
thecomplexityofPhase4isO(K ⁄N)(notlineartoN)intheworstcase. Althoughwe
havetriedtoimprovethePhase4refiningalgorithmusingthe‘nearestneighbor’techniques

170 ZHANG,RAMAKRISHNANANDLIVNY
proposedin(Huang,etal.,1992),andthisimprovementperformsverywellandbringsthe
timecomplexityO(N ⁄K)downtobealmostlinearwithrespecttoN,thelinearslopeis
sensitive to the distribution patterns of data. In our case, for the grid pattern, since there
areusuallymoreclustercentersaroundadatapoint,itneedsmoretimetofindthenearest
one;whereasforthesinepattern,sincethereareusuallylessclustercentersaroundadata
point,itneedslesstimetofindthenearestone;therandompatternishenceinthemiddle.
Asforqualitystability,Table8showsthatwiththesameamountofmemory,forawide
range of K and N, the quality of BIRCH clusters (indicated by D„) is again consistently
closeto(orbetterthan)thatoftheintendedclusters(indicatedbyD„ ).
int
Increasing the Dimension (d): For each of DS1, DS2 and DS3, we create a range of
datasetsbykeepingthegeneratorsettingsthesameexceptforchangingthedimension(d)
from2to50tochangethedatasetsize. Inthisexperiment,theamountofmemoryusedfor
eachdatasetisscaledupbasedonthedatasetsize(5%ofthedatasetsize). Withallthree
patterns of datasets, their running times for the first 3 phases, as well as for all 4 phases
are plotted against the dimension in Figure 18. We observe that the running time curves
deviateslightlyfromlinearasthedimensionandthecorrespondingmemoryincrease. This
is caused by the following fact: with M (a constant amount of memory), the memory
0
correspondingtoagivend-dimensionaldatasetisscaledupasM ⁄d. Now,ifNandPare
0
constant,asthedimensionincreasesthetimecomplexitywillscaleupas1+log M0 ⁄d
C P ⁄d P
accordingtotheanalysisinSection6.1. Thatis, asthedimensionandmemoryincrease,
firsttheCF-treesizeincreases;secondthebranchingfactordecreasesandcausestheCF-
treeheighttoincrease. Soforalargerd,incorporatinganewdatapointgoesthroughmore
levels on a larger CF-tree, and hence needs more time. The interesting thing is that by
tuningP,onecanmakethescalingcurvessublinearorsuperlinear, andinthiscase, with
P=1024bytes,thecurvesareslightlysuperlinear.
Asforqualitystability,Table9showsthatforawiderangeofd,thequalityofBIRCH
clusters (indicated by D„) are once again consistently close to (or better than) that of the
intendedclusters(indicatedbyD„ ).
int
7. BIRCHApplications
In this section, we would like to show (1) how a clustering system like BIRCH can be
usedtohelpsolvereal-worldproblems,and(2)howBIRCH,CLARANSandKMEANS
performonsomerealdatasets.
7.1. InteractiveandIterativePixelClassification
The first application is motivated by the MVI (Multiband Vegetation Imager) technique
developedin(KucharikandNorman,1996,Kucharik,etal.,1996). TheMVIisthecombi-
nationofacharge-coupleddevice(CCD)camera,afilterexchangemechanism,andlaptop
computer used to capture rapid, successive images of plant canopies in two wavelength
bands. Oneimageistakeninthevisiblewavelengthband,andtheotherinthenear-infrared
band. Thepurposeofusingtwowavelengthbandsistoallowforidentificationofdifferent

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 171
Data
Subset of Data
Each Pixel:
Data Preparation: (X,Y,VIS,NIR)
Feature Selection and Weighting
Clustering with BIRCH USER
Data Filtering
Visualizing with DEVISE
Figure19.PixelClassificationToolwithBIRCHandDEVISEIntegrated
canopy components such as sunlit and shaded leaf area, sunlit and shaded branch area,
clouds, and blue sky for studying plant canopy architecture. This is important to many
fieldsincludingecology,forestry,meteorology,andotheragriculturalsciences. Themain
useofBIRCHistohelpclassifypixelsintheMVIimagesbyperformingclustering,and
experimentingwithdifferentfeatureselectionandweightingchoices.
To do that, we integrated BIRCH with the DEVISE (Cheng, Livny and Ramakrishnan,
1995)datavisualizationsystem,asshowninFigure19,toformauser-friendly,interactive
anditerativepixelclassificationtool. Asdataisreadin,(1)itisconvertedintothedesired
format; (2) interesting features are selected and weighted by the user interactively; (3)
BIRCHisusedforclusteringthedatainthespaceoftheselectedandweightedfeatures;
(4)relevantresultssuchastheclustersaswellastheircorrespondingdataarevisualizedby
DEVISEtoenabletheusertolookfor‘patterns’ortoevaluate‘qualities’;(5)withfeedback
obtainedfromthevisualizations,theusermaychoosetofilteroutasubsetofthedatawhich
correspondstosomeclusters,and/orre-adjustthefeatureselectionandweightingforfurther
clusteringandvisualization. Theiterationwiththeabovefivemajorstepscanberepeated,
andthehistoryofinteractioncanbemaintainedandmanipulatedasatreestructurewhich
allowstheusertodecidewhatpartofresultstokeep,wheretoproceedortobacktrack.
FollowingisanexampleofusingthistooltohelpseparatepixelsinaMVIimage. Figure
20isaMVIimagewhichcontainstwosimilarimagesoftreeswiththeskyasbackground.
The top picture is taken in the near-infrared band (NIR image), and the bottom one is
takeninthevisiblewavelengthband(VISimage). Eachimagecontains490x990pixels
after ‘cutting’ the noisy frames. Each pixel can be represented by a tuple with schema
(x;y;nir;vis), where x and y are the coordinates of the pixel, and nir and vis are the
correspondingbrightnessvaluesintheNIRimageandtheVISimagerespectively.

172 ZHANG,RAMAKRISHNANANDLIVNY
Figure20.TheimagestakeninNIRandVIS
Westartthefirstiterationwiththenumberofclusterssetto2,inthehopeoffindingtwo
clusterscorrespondingtothetreesandthesky. Itiseasytonoticethatthetreesandthesky
arebetterdifferentiatedintheVISimagethanintheNIRimage. Sotheweightassigned
tovisis10timesmorethantheweightassignedtonir. ThenBIRCHisinvokedunderthe
defaultsettingstodotheclusteringwhichtakesatotalof50seconds(includingtwoscans
oftheVISandNIRvaluesfromanASCIIfileondiskinPhase1andPhase4; eachscan
takes about 4.5 seconds). Figure 21 is the DEVISE visualization of the clusters obtained
afterthefirstiteration(top: wherex-axisisforweightedvis, y-axisisforweightednir,
eachclusterisplottedasacirclewiththecentroidasthecenterandthestandarddeviation

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 173
Figure21.1stRun:SeparateTreeandSky
astheradius)aswellasthecorrespondingpartsoftheimage(bottom: wherex-axisisfor
thexcoordinatesofpixelsandy-axisisfortheycoordinatesofpixels).
Visually,bycomparisonwiththeoriginalimages,onecanseethatthetwoclustersform
asatisfactoryclassificationofthetreesandthesky. Ingeneral,itmaytakeafewiterations
fortheusertoidentifyagoodsetofweightsthatachievessuchaclassification. However,
theimportantpointisthatonceasetofgoodweightsarefoundfromoneimagepair,they
canbeusedforclassifyingseveralotherimagepairstakenunderthesameconditions(the
samekindoftree,thesameweatherconditions,aboutthesametimeinaday),andthepixel
classificationtaskbecomesautomatic,withoutfurtherhumanintervention.

174 ZHANG,RAMAKRISHNANANDLIVNY
Figure22.2ndRun:SeparateBranches,ShadowsandSunlitLeaves
Intheseconditeration,thepartofthedatathatcorrespondstothetreesisfilteredoutfor
furtherclustering. Thenumberofclustersissetat3inthehopeoffindingthreeclusters
whichcorrespondtobranches,shadowsandsunlitleaves. Onecanobservefromtheoriginal
images that the branches, shadows and sunlit leaves are easier to tell apart from the NIR
imagethanfromtheVISimage. Sowenowweightnir 10timesheavierthanvis. This
time, with the same amount of memory, but a smaller set of data (263401 tuples versus
485100tuples),theclusteringcanbedoneatamuchfinergranularity,whichshouldresult
inbetterquality. IttakesBIRCHatotalof29.08seconds(includingtwoscansofthesubset
ofVISandNIRvaluesfromanASCIIfileondisk). Figure22showstheclustersafterthe
seconditerationaswellasthecorrespondingpartsoftheimage.

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 175
Table10.BIRCH,CLARANS,KMEANSonPixelClassification
Method Image1:N=485100,K=2 Image2:N=485100,K=5
Time D„ #Scan Time D„ #Scan
BIRCH 50 0.5085 2 53 0.6269 2
CLARANS 368 0.5061 330 642 0.6292 523
KMEANS 8.3 0.5015 5 30 0.6090 48
WeusedtwoverydifferentMVIimagepairstocomparehowBIRCH,CLARANSand
KMEANSperformrelativetoeachother. Table10summarizestheresults. ForBIRCH,
thememoryusedisonly5%ofthedatasetsize,whereasforCLARANSandKMEANS,the
wholedatasetaswellasrelatedsecondarydatastructuresareallinmemory. Forbothcases,
BIRCH,CLARANSandKMEANShavealmostthesamequality. Thequalityobtainedby
CLARANSandKMEANSisslightlybetterthanthatobtainedbyBIRCH.Toexplainthis,
one should notice that (1) CLARANS and KMEANS are doing ‘hill-climbing’ and they
stop only after they reach some ‘optimal’ clustering; (2) in this application, N is not too
big,Kanddareextremelysmall,andthepixeldistributionintermsofVISandNIRvalues
is very simple in modality, so the ‘hill’ that they climb tends to be simple too. Very bad
local optimal solutions do not prevail, and CLARANS and KMEANS can usually reach
aprettygoodclusteringinthe‘hill’. BIRCHstopsafterscanningthedatasetonlytwice,
anditreachesaclusteringalmostasgoodasthoseoptimalonesfoundbyCLARANSand
KMEANSwithalotofadditionaldatascans. BIRCH’srunningtimeisnotsensitivetothe
differentMVIimagepairswhereasforCLARANSandKMEANS,theirrunningtimeand
datascannumbersareverysensitivetothedatasetsthemselves.
7.2. CodebookGeneralizationinImageCompression
Digitalimagecompression(Kou,1995)isthetechnologyofreducingimagedatatosave
storage space and transmission bandwidth. Vector quantization (GershoandGray,1992)
isawidelyusedimagecompression/decompressiontechniquewhichoperatesonblocksof
pixelsinsteadofpixelsforbetterefficiency. Invectorquantization, theoriginalimageis
firstdecomposedintosmallrectangularblocks,andeachblockisrepresentedasavector.
GivenacodebookofsizeK,itcontainsKcodewordsthatarevectorsservingasseedsto
attractothervectorsbaseduponthenearestneighborcriterion. Eachvectorisencodedwith
the codebook, i.e., finding its nearest codeword from the codebook, and later is decoded
withthesamecodebook,i.e.,usingitsnearestcodewordinthecodebookasitsvalue.
Given the training vectors (from the training image) and the desired codebook size
(i.e., number of codewords), the main problem of vector quantization is how to gener-
atethecodebook. AcommonlyusedcodebookgeneratingalgorithmistheLBGalgorithm
(Linde,BuzoandGray,1980). LBG is just KMEANS except for two specific modifica-
tionsthatmustbemadeforuseinimagecompression: (1)Toavoidgettingstuckatabad
local optimal LBG starts with an initial codebook of size 1 (instead of the desired size),
and proceeds by refining and splitting the codebook iteratively. (2) If empty cells (i.e.,

176 ZHANG,RAMAKRISHNANANDLIVNY
Table11.BIRCH,CLARANSandLBGonImageCompression
Method Lena Baboon
Time #Scans Distortion Entropy Time #Scan Distortion Entropy
BIRCH 15 9 712 6.70 17 8 5097 7.15
CLARANS 2222 8146 693 7.43 2111 7651 5070 7.70
LBG 19 46 719 7.38 31 42 5155 7.73
codewordsthatattractnovectors)inthecodebookarefoundduringtherefinement,ithas
astrategyoffillingtheemptycellsviasplitting.
Inalittlemoredetail:
1. LBG uses the GLA (or KMEANS with empty cell filling strategy) algorithm
(GershoandGray,1992)tofindthe‘optimal’codebookofcurrentsize.
2. Ifitreachesthedesiredcodebooksize, thenitstops; otherwiseitdoublesthecurrent
codebook size, perturbs and splits the current ‘optimal’ codebook and goes to the
previousstep.
The above LBG algorithm invokes many extra scans of the training vectors during the
codebookoptimizationsatallthecodebooksizelevelsbeforereachingthedesiredcodebook
sizelevel;yet,ofcourse,itcannotcompletelyescapefromlocallyoptimalsolutions.
WithBIRCHclusteringthetrainingvectors,weknowthatfromthefirst3phases,witha
singlescanofthetrainingvectors,theclustersobtainedgenerallycapturethemajorvector
distributionpatternsandonlyhaveminorinaccuracies. SoinPhase3,ifwesetthenumber
of clusters directly as the desired codebook size, and use the centroids of the obtained
clustersastheinitialcodebook,thenwecanfeedthemtoGLAforfurtheroptimization. So,
incontrastwithLBG,(1)theinitialcodebookfromthefirst3phasesofBIRCHisnotlikely
toleadtoabadlocallyoptimalcodebook;(2)usingBIRCHtogeneratethecodebookwill
involvefewerscansofthetrainingvectors.
Wehaveusedtwodifferentimages: LenaandBaboon(eachwith512x512pixels)asexam-
plestocompareBIRCH,CLARANSandLBG’sperformancesintermsoftherunningtime,
numberofscansofthedataset,distortionandentropy(Kou,1995,RabbaniandJones,1991)
onhighdimensional(d=16)realdatasets. Firstthetrainingvectorsarederivedbyblocking
theimageinto4x4blocks(d=16),andthedesiredcodebooksizeissetto256. Distortion
is defined as the sum of squares of Euclidean distances from all training vectors to their
nearestcodewords. Itisawidelyusedqualitymeasurement,andsmallerdistortionvalues
implybetterqualities. Entropyistheaveragenumberofbitsneededforencodingatraining
vector,solowerentropymeansbettercompression.
Table11summarizestheperformanceresults. Timeisthetotaltimetogeneratetheinitial
codebook of the desired size (256) and then use GLA algorithm to refine the codebook.
#Scansdenotesthetotalnumberofscansofthedatasetinordertoreachthefinalcodebook.
DistortionandEntropyareobtainedbycompressingtheimagesusingthefinalcodebook.
Onecanseethatforbothimages,(1)forallfouraspectslistedinthetable,usingBIRCH
togeneratetheinitialcodebookisconsistentlybetterthanusingCLARANSorusingLBG;
(2)forrunningtime,datascansandentropy,usingBIRCHissignificantlybetterthanusing

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 177
Figure23.LenaCompressedwithBIRCHCodebook
Figure24.LenaCompressedwithCLARANSCodebook
CLARANS.ForCLARANS,itsrunningtimeismuchlongerthanthatofBIRCH,whereas
itsfinalcodebookisonlyslightlybetterthanthatobtainedthroughBIRCH(andisbetter
only in terms of distortion). Readers can look at the compressed images in Figure 23
through28foreasyvisualqualitycomparisons.
8. SummaryandFutureResearch
BIRCH provides a clustering method for very large datasets. It makes a large clustering
problemtractablebyconcentratingondenselyoccupiedportions,andcreatingacompact
summary. It utilizes measurements that capture the natural closeness of data and can be
stored and updated incrementally in a height-balanced tree. BIRCH can work with any
given amount of memory, and the I/O complexity is a little more than one scan of data.

178 ZHANG,RAMAKRISHNANANDLIVNY
Figure25.LenaCompressedwithLBGCodebook
Figure26.BaboonCompressedwithBIRCHCodebook

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 179
Figure27.BaboonCompressedwithCLARANSCodebook
Figure28.BaboonCompressedwithLBGCodebook

180 ZHANG,RAMAKRISHNANANDLIVNY
Experimentally, BIRCH is shown to perform very well on several large datasets, and is
significantlysuperiortoCLARANSandKMEANSintermsofquality,speed,stabilityand
scalabilityoverall.
Properparametersettingandfurthergeneralizationaretwoimportanttopicstoexplore
inthefuture. Additionalissuesincludeotherheuristicmethodsforincreasingthethresh-
old dynamically, how to handle non-metric attributes, other threshold requirements and
relatedinsertion,rebuildingalgorithms,andclusteringconfidencemeasurements. Anim-
portantdirectionforfurtherstudyishowtomakeuseoftheclusteringinformationobtained
fromBIRCHtohelpsolveproblemssuchasstorageoptimization,datapartitionandindex
construction.
Notes
1. The reducibility property requires that if for clusters i, j, k, and some distance value (cid:181): d(i;j) < (cid:181),
d(i;k)>(cid:181),d(j;k)>(cid:181),thenforthemergedclusteri+j,d(i+j;k)>(cid:181).
References
Beckmann,Norbert,Kriegel,Hans-Peter,Schneider,RalfandSeegerBernhard,TheR⁄-tree: AnEfficientand
RobustAccessMethodforPointsandRectangles,Proc.ofACMSIGMODInt.Conf.onManagementofData,
322-331,1990.
Cheeseman,Peter,Kelly,James,Self,Matthew,etal.,AutoClass: ABayesianClassificationSystem,Proc. of
the5thInt.Conf.onMachineLearning,MorganKaufman,Jun.1988.
Cheng,Michael,Livny,MironandRamakrishnan,Raghu,VisualAnalysisofStreamData,Proc. ofIS&T/SPIE
Conf.onVisualDataExplorationandAnalysis,SanJose,CA,Feb.1995.
Duda,RichardandHartPeterE.,PatternClassificationandSceneAnalysis,Wiley,1973.
Dubes,R.andJain,A.K.,ClusteringMethodologiesinExploratoryDataAnalysis,AdvancesinComputers,Edited
byM.C.Yovits,Vol.19,AcademicPress,NewYork,1980.
Ester, Martin, Kriegel, Hans-Peter and Xu, Xiaowei, A Database Interface for Clustering in Large Spatial
Databases,Proc.of1stInt.Conf.onKnowledgeDiscoveryandDataMining,1995a.
Ester,Martin,Kriegel,Hans-PeterandXu,Xiaowei,KnowledgeDiscoveryinLargeSpatialDatabases:Focusing
TechniquesforEfficientClassIdentification,Proc.of4thInt.SymposiumonLargeSpatialDatabases,Portland,
Maine,U.S.A.,1995b.
Feigenbaum,E.A.andSimon,H.,EPAM-likemodelsofrecognitionandlearning,CognitiveScience,vol.8,1984,
305-336.
Fisher,DouglasH.,KnowledgeAcquisitionviaIncrementalConceptualClustering,MachineLearning,2(2),1987
Fisher,DouglasH.,IterativeOptimizationandSimplificationofHierarchicalClusterings,TechnicalReportCS-
95-01,Dept.ofComputerScience,VanderbiltUniversity,Nashville,TN37235,1995.
Gersho,A.andGray,R.,Vectorquantizationandsignalcompression,Boston,Ma.:KluwerAcademicPublishers,
1992.
Gennari,JohnH.,Langley,PatandFisher,Douglas,ModelsofIncrementalConceptFormation,ArtificialIntelli-
gence,vol.40,1989,11-61.
Guttman,A.,R-trees: adynamicindexstructureforspatialsearching,Proc. ACMSIGMODInt. Conf. on
ManagementofData,47-57,1984.
Huang,C.,Bi,Q.,Stiles,G.andHarris,R.,FastFullSearchEquivalentEncodingAlgorithmsforImageCom-
pressionUsingVectorQuantization,IEEETrans.onImageProcessing,vol.1,no.3,July,1992.
Hartigan,J.A.andWong,M.A.,AK-MeansClusteringAlgorithm,Appl.Statist.,vol.28,no.1,1979.
Kaufman,LeonardandRousseeuw,PeterJ.,FindingGroupsinData-AnIntroductiontoClusterAnalysis,Wiley
SeriesinProbabilityandMathematicalStatistics,1990.

BIRCH:ANEWDATACLUSTERINGALGORITHMANDITSAPPLICATIONS 181
Kucharik,C.J.andNorman,J.M.,MeasuringCanopyArchitecturewithaMultibandVegetationImager(MVI)
Proc. ofthe22ndconf. onAgriculturalandForestMeteorology,AmericanMeteorologicalSocietyannual
meeting,Atlanta,GA,Jan28-Feb2,1996.
Kucharik,C.J.,Norman,J.M.,Murdock,L.M.andGower,S.T.,CharacterizingCanopynon-randomnesswith
aMultibandVegetationImager(MVI),SubmittedtoJournalofGeophysicalResearch,toappearintheBoreal
Ecosystem-AtmosphereStudy(BOREAS)specialissue,1996.
Kou,Weidong,DigitalImageCompressionAlgorithmsandStandards,KluwerAcademicPublishers,1995.
Linde,Y.,Buzo,A.andGray,R.M.,AnAlgorithmforVectorQuantizationDesign,IEEETrans.onCommunica-
tions,vol.28,no.1,1980.
Lebowitz,Michael,ExperimentswithIncrementalConceptFormation:UNIMEM,MachineLearning,1987.
Lee, R.C.T., Clustering analysis and its applications, Advances in Information Systems Science, Edited by
J.T.Toum,Vol.8,pp.169-292,PlenumPress,NewYork,1981.
Murtagh,F.,ASurveyofRecentAdvancesinHierarchicalClusteringAlgorithms,TheComputerJournal,1983.
Ng,RaymondT.andHan,Jiawei,EfficientandEffectiveClusteringMethodsforSpatialDataMining,Proc. of
VLDB,1994.
Olson,ClarkF.,ParallelAlgorithmsforHierarchicalClustering,TechnicalReport,ComputerScienceDivision,
Univ.ofCaliforniaatBerkeley,Dec.,1993.
Rabbani, MajidandJones, PaulW.DigitalImageCompressionTechniques, SPIEOpticalEngineeringPress,
1991.
Zhang,Tian,Ramakrishnan,RaghuandLivny,Miron,BIRCH:AnEfficientDataClusteringMethodforVery
LargeDatabases,TechnicalReport,ComputerSciencesDept.,Univ.ofWisconsin-Madison,1995.
Zhang,Tian,DataClusteringforVeryLargeDatasetsPlusApplications,Dissertation,ComputerSciencesDept.
atUniv.ofWisconsin-Madison,1996.
TianZhangreceivedherPh.D.fromtheComputerSciencesDepartmentatUniversityofWisconsin
-Madisonin1997. NowsheisanadvisorysoftwareengineerworkingintheDataManagement
ArchitectureandTechnologyDepartmentatIBMSantaTeresaLaboratory. Herresearchinterests
includedatamininganddatavisualization,patternrecognition,rule-basedandcost-basedquery
optimization,multi-dimensionalindexstructures,heterogeneousdatabasesanddatawarehousing.
RaghuRamakrishnanisanassociateprofessorofComputerScienceatUniversityof
Wisconsin-Madison,wherehehasbeenonthefacultysince1987,whenhereceivedhisPh.D.from
UniversityofTexas-Austin. Hisresearchinterestsareintheareasofdatabasequerylanguages
(includinglogic-basedlanguages,languagesfornon-traditionaldatasuchassequencesandimages,
anddataminingapplications),databaseintegrationandvisualization. Heistherecipientofa
PackardFoundationfellowship,anNSFPYIaward,andanIBMFacultyDevelopmentAward. Heis
ontheeditorialboardsofTheAIReview,J.Constraints,J.DataMiningandKnowledgeDiscovery,
J.IntelligentInformationSystemsandJ.LogicProgramming,andwasthedatabaseareaeditorof
theCRCPressHandbookofComputerScience. Hehaseditedacollectionofarticles,‘Applications
ofLogicDatabases’,publishedbyKluwer,andistheauthorofadatabasetextbook‘Database
ManagementSystems,’publishedbyMcGraw-Hill. Hehasalsoservedontheprogramcommittees
ofseveralconferencesinthedatabaseandlogicprogrammingareas,includingIEEEData
Engineering,ICLP,AAAIKnowledgeandDataDiscovery,ACMPODS,ACMSIGMOD,and
VLDB.HisresearchhasbeensupportedbygrantsfromNASA,NSF,ORD,thePackardFoundation
andseveralcompanies(DEC,HP,IBM,Tandem,Xerox).
MironLivnyisaprofessorofComputerSciencesattheUniversityofWisconsin-Madison,where
hehasbeenafacultysince1984,whenhereceivedhisPh.DfromtheWeizmannInstituteofScience

182 ZHANG,RAMAKRISHNANANDLIVNY
inIsrael. Hisresearchinterestsareintheareasofresourceanddatamanagementtoolsandpolicies
forcentralizedanddistributedsystems(includingreal-timesystems)anddataexplorationand
visualizationenvironments. HeistherecipientofIBM,DEC,andBoeingFacultyawardsandhas
servedontheprogramcommitteesofdatabase,scheduling,andperformanceevaluationconferences
andworkshops. HisresearchhasbeensupportedbygrantsfromNASA,NSF,ORD,NIH,NLMand
severalcompanies(Sun,DEC,IBM,Boeing,Microsoft).