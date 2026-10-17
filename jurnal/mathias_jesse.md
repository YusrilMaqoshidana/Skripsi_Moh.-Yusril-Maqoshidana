UserModelingandUser-AdaptedInteraction(2023)33:769–802
https://doi.org/10.1007/s11257-022-09351-w
Intra-listsimilarityandhumandiversityperceptionsof
recommendations:thedetailsmatter
Mathias Jesse1·Christine Bauer2·Dietmar Jannach1
Received:20June2022/Acceptedinrevisedform:13November2022/Publishedonline:12December2022
©TheAuthor(s)2022
Abstract
Thediversityofthegenerateditemsuggestionscanbeanimportantqualityfactorofa
recommendersystem.Inofflineexperiments,diversityiscommonlyassessedwiththe
helpoftheintra-listsimilarity(ILS)measure,whichisdefinedastheaveragepairwise
similarityoftheitemsinalist.Thesimilarityofeachpairofitemsisoftendetermined
basedondomain-specificmeta-data,e.g.,moviegenres.Whilethisapproachiscom-
mon in the literature, it in most cases remains open if a particular implementation
oftheILSmeasureisactuallyavalidproxyforthehumandiversityperceptionina
given application. With this work, we address this research gap and investigate the
correlationofdifferentILSimplementationswithhumanperceptionsinthedomains
of movie and recipe recommendation. We conducted several user studies involving
over 500 participants. Our results indicate that the particularities of the ILS metric
implementationmatter.WhilewefoundthattheILSmetriccanbeagoodproxyfor
human perceptions, it turns out that it is important to individually validate the used
ILSmetricimplementationforagivenapplication.Onamoregenerallevel,ourwork
pointstoacertainlevelofoversimplificationinrecommendersystemsresearchwhen
it comes to the design of computational proxies for human quality perceptions and
thuscallsformoreresearchregardingthevalidationofthecorrespondingmetrics.
Keywords Recommendersystems·Diversityperception·Intra-listsimilarity·
Metricvalidation·Userstudy
B
DietmarJannach
dietmar.jannach@aau.at
MathiasJesse
mathias.jesse@aau.at
ChristineBauer
c.bauer@uu.nl
1 UniversityofKlagenfurt,KlagenfurtamWörthersee,Austria
2 UtrechtUniversity,Utrecht,Netherlands
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

770 M.Jesseetal.
1 Introduction
The main task of a recommender system is to surface items that are relevant for
users in their current context. However, it is well known that in many cases, being
accurateintermsofpredictingwhichitemsarerelevantmaynotbeenough(McNee
et al. 2006). One established additional quality criterion that is important in many
application domains is that of diversity. Non-diverse recommendation lists may not
only appear monotone to users, but they may also lead to limited discovery if they
only cover a limited part of the available catalog, e.g., only movies from the most
preferred genre. Therefore, various algorithmic approaches were proposed over the
years to ensure a certain level of diversity in the recommendations, see Kaminskas
andBridge(2016)andKunaverandPožrl(2017)forrelatedsurveys.
Asdiversitymaybeconsideredasubjectiveconcept,severaluserstudiesfocusedon
understandinginwhichwaystheperceiveddiversityofasetofrecommendationsmay
affectotherqualityfactorssuchasperceivedaccuracy(Puetal.2011;Ekstrandetal.
2014;Willemsenetal.2016;Nilashietal.2016).However,probablyamuchlarger
numberofpublicationsondiversityusesofflineexperimentsasaresearchmethodol-
ogy and therefore relyon objective, computational metrics to quantify the extent of
diversityofagivenrecommendationlist.Averycommonapproachtoquantifyalist’s
diversity is to consider the pairwise similarities of the items. Early proposals were
made over 20 years ago in the context of retrieval-based and conversational recom-
menders (Bradley and Smyth 2001; McGinty and Smyth 2003). Soon after, Ziegler
et al. (2005) popularized this approach under the term intra-list similarity (ILS) in
theirearlyworkontopicdiversificationinabookrecommendationsetting.
Technically,theILSofaset P of(recommended)itemsisdefinedinZiegleretal.
(2005)asfollows:
(cid:2) (cid:2)
sim(p ,p )
ILS(P)= pi ∈P pj ∈P,pi (cid:3)=pj i j (1)
2
wheresimisanarbitraryfunctionthatreturnsasimilarityscorefortwoitems.Often,
thescoreisstandardizedtoliein[−1,1]or[0,1].NotethatinZiegleretal.(2005)
thesumofthepairwisesimilaritiesisdividedbytwo.Reportingtheaveragepairwise
similarity,asdoneinearlierinBradleyandSmyth(2001),ishowevermorecommon
today, and the denominator in this case would be the number of comparisons, i.e.,
(|P|(|P|−1))/2.
One important aspect of the technical formulation of the ILS metric is that the
orderoftheelementsinalistdoesnotmatter.ThesameILSvaluewillbereturned
when all similar items are dispersed across the list or when they are clustered, e.g.,
at the beginning or end of the list.1 Another feature of the ILS metric definition is
that it is generic in a sense that is not tailored to a particular application setting.
Dependingonaspecificapplication,anysuitablesimilarityfunctioncanbeplugged
in.Ziegleretal.(2005)usedAmazon’sbooktaxonomytodiversifytheresultsoftheir
recommender.Laterworksreliedonvariousothertypesof(meta-)data,forexample,
1 Geetal.(2012)reportedsomeindicationsthatthesimilarityperceptionofusersmaypossiblydependon
thepositionsoftheitems.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 771
movie genres (Vargas et al. 2012), food ingredients (Hauptmann et al. 2021), artist
similaritybasedonsocialtags(Jannachetal.2017),orlatenttopicmodelsfromthe
users’interactions(Shietal.2012).
Inmanyworksondiversityinrecommendation,therationaleforusingaparticular
similarityfunctionishowevernotdiscussedindepth,anditmightsimplybebasedon
theavailabilityofitemmeta-data.Inthisregard,wemaythereforefaceanoversim-
plificationintermsoftheselectionandoperationalizationofdiversitymetrics.Most
workscomewithoutanevaluationoftheselecteddiversitymetric—neitherforaspe-
cificapplicationnoracrosssettingsordomains.Instead,itissimplyassumed—often
withoutevidenceortheoreticalunderpinning—thatthechosencomputationalmetric
isalignedwithhumanperceptions.Moreover,whilemanypublishedworksmayshow
thataparticulardiversity-awarealgorithmhasaneffectonthechosenILSmetric,it
isoftenunclearifthealgorithmwouldactuallyimpacttheusers’diversityperception.
Understandingtheusers’perceptionishoweverimportantbecauseitmaysignificantly
affectthequalityperceptionoftherecommendersystemandthebehavioralintentions
ofusers,asmentionedabove(Puetal.2011;Ekstrandetal.2014;Willemsenetal.
2016;Nilashietal.2016).
In this work, we address this largely open research gap and investigate to what
extentdifferentILSmetricimplementationsaresuitableproxiesforthediversityper-
ception of users. For that purpose, we conducted a number of user studies in two
applicationdomains,involvingover500participants.Inthesestudies,wepresented
theparticipantswithrecommendationliststhathaddifferentdiversitylevelsaccord-
ingtoaparticularILSmetric,andwethencontrastedtheILS-baseddiversityvalues
withtheparticipants’self-reporteddiversityperceptions.Ourstudiesledtotwomain
insights.First,wefindthatILScanbeavalidproxyforuser-perceiveddiversity.Inboth
applicationdomains,wefoundametricimplementationthatcorrelatedwellwithuser
perceptions.Second,however,wefoundthattheparticularitiesmatter:usingdifferent
metricimplementationsfordiversificationresultsinvaryingdiversityperceptions,and
whatworkswellinonedomaindoesnotnecessarilyworkwellinanother.Overall,our
workthereforeconfirmsourconjectureregardingacertainlevelofoversimplification
inourresearchpracticeswhenitcomestostudyingdiversity-awarerecommendation
algorithms.Correspondingly,moreresearchseemstobeneededsothatfutureresearch
inthisareacanbuildonvalidatedmetrics.
Theremainderofthepaperisorganizedasfollows.Afterdiscussingpreviousworks
inSect.2,wedescribethedetailsofouruserstudiesinSect.3.Theresultsarepresented
anddiscussedinSect.4.Weconcludeourworkwithasummaryofthemainfindings
andanoutlookonfutureresearchinSect.5.
2 Relatedwork
The main concepts of interest in our study are diversity metrics for recommenda-
tion lists and the diversity perceptions of humans. In terms of terminology, let us
note upfront that “similarity” and “diversity” are often considered to be inversely
relatedconceptsintheliteratureandthatthetermsaresometimesusedinanalmost
interchangeable manner. Technically, as mentioned above, the diversity of a list is
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

772 M.Jesseetal.
commonlycomputedasamathematicalinverseofametricthatisbasedonsimilarity.
In user-centric evaluations, by comparison, both questions related to the perceived
similarityandtheperceiveddiversityaresometimesusedtoassessthediversityofa
list,e.g.,inPuetal.(2011).
Inthefollowingsections,wefirstpresentrelatedworkonintra-listsimilarity(ILS),
whichisthecentralmetricinourwork,anddiscussothersimilaritymetricsusedin
recommendersystemsresearch(Sect.2.1).Thereafter,wereviewpreviousworksthat
studied human perceptions of similarity and diversity. First, we discuss works that
focusonthesimilarityperceptionofitempairs(Sect.2.2);subsequently,wepresent
relatedworkthatfocusesonthediversityperceptionoflistsofitems(Sect.2.3).
Overall, our present work is different from the discussed prior works in that we
aimtovalidatewhethercommonlyusedmetricstoassessthediversityoflistsofitems
are indeed valid proxies of human perceptions. For that purpose, we investigate to
what extent the particularities of the specific implementation of ILS matter for two
importantapplicationdomains.
2.1 Intra-listsimilarityandotherdiversitymetrics
ILSisprobablythemostcommonlyusedmetrictocapturediversityinrecommender
systemsintheliterature(Duetal.2021).Asdescribedearlier,ILSisbasedonpairwise
similaritycomparisons,andahigherILSscoredenotesalowerlevelofdiversity.Other
namesforILSareintra-listdiversity(Vargasetal.2014;MauroandArdissono2019)
orintra-listdistance(Linetal.2020).
ThegenericILSdefinitionprovidestheflexibilitytopluginanysuitablesimilarity
function. In the literature, a variety of similarity functions was used for different
applications, using different types of content information or meta-data. Kaminskas
andBridge(2016)pointoutthatthereisnoguaranteethatlistswithahigh-ILSmetric
valuearealsoperceivedashighlysimilar.Whenusingaparticularimplementationof
theILSmetric,itisinprinciple necessary tovalidate thatitisindeed agood proxy
foruserperceptions.Thisvalidationis,however,rarelydoneandourpresentresearch
addressesthisquestionfortwoILSimplementations.
Wenotethat—besidesILS—alsovariousothermetricsareusedtocapturediver-
sityinrecommenderresearch.KunaverandPožrl(2017)provideadetailedliterature
review of diversity metrics. However, it turns out that several of these metrics are
variationsorextensionsofeachother,whichmeansonlyasmallnumberofdistinct
metricsareactuallyusedintheliterature.
Anexampleofanapproachtocaptureaquitedifferentconceptofdiversityistouse
theGinicoefficient.TheGinicoefficientisameasureofdistributionalinequalityand
is,forexample,usedineconomicstocaptureincomeinequality.Inthecontextofrec-
ommendersystems,thecoefficientcanbeusedtomeasurehowoftenindividualitems
arerecommended(andsubsequentlymorelikelypurchased).Ifarecommendersystem
makes the same item suggestions to everyone, the distribution will be very skewed,
leading to a high Gini coefficient and a concentration bias on a few items (Fleder
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 773
andHosanagar2007)2.DifferentlyfromtheILSmetric,diversityassessmentsbased
ontheGiniindexarenotbasedontheanalysisofindividuallists,butonhowoften
individualitemsappearinrecommendationlistsacrossusers,whichiswhyitiscalled
“aggregatediversity”inAdomaviciusandKwon(2012).Questionsofaggregatediver-
sity,concentrationbiases,andrelatedconceptsofcoverage—seeJannachetal.(2015)
foranin-depthanalysis—arenotthefocusofourpresentwork,whichaimstostudy
humandiversityperceptionsatthelevelofindividuallists.
In many research works on recommendation diversity, the goal is to balance the
typicaltrade-offbetweenaccuracy(relevance)anddiversitymetrics,seeZhengand
Wang(2022)andJannach(2022)forrelatedsurveysonmulti-objectiverecommender
systems.Analternativetosuchapproachesistodesignevaluationmetricsthatcom-
bine various aspects, including accuracy, diversity, or novelty in a single metric.
In the area of information retrieval, Clarke et al. (2008) for example proposed to
consider various such aspects when computing the nDCG (Normalized Discounted
CumulativeGain)ofanitemranking.Lateron,similarideaswereproposedforrec-
ommendationproblems—e.g.,inVargas(2011)andVargasandCastells(2011)—to
designrelevance-awarebeyond-accuracymetrics.Technically,suchmetricsarehow-
ever again often based on the ILS metric. In our present work, we focus on human
diversityperceptionsindependentoftheindividualrelevanceoftheitemsforagiven
user.
Overall,whilethereviewbyKunaverandPožrl(2017)showsthatthereareseveral
alternativeapproachestocomputationallyassessingthedifferentnotionsofdiversity,
theILSisthemostfrequentlyusedmetricintheliterature,andwethereforeuseitas
thebasisforourresearch.
2.2 Assessingthesimilarityperceptionofitempairs
In the context of recommender systems, similarity functions play a central role in
different ways. In content-based recommendation approaches in general, similarity
functions serve as the basis to assess the match between a given item and a user’s
past preferences (de Gemmis et al. 2015). Also, similarity functions are commonly
amaincomponentthatdeterminestheitemrankingfortheproblemsofsimilar-item
recommendation (Brovman etal.2016) and next-item recommendation (Zeng etal.
2019). Moreover, similarity functions are typically the foundation of diversification
approaches(KunaverandPožrl2017;Ziegleretal.2005;VargasandCastells2011;
Chenetal.2013),wherethegoalistomatchtheusers’diversityneedsortosupport
theirexplorationefforts(TsaiandBrusilovsky2018).
For all such purposes, it is important that the chosen similarity function reflects
userperception,anaspectthatusuallyhastobevalidatedthroughcorrespondinguser
studies,see,e.g.,Ekstrandetal.(2014).Inthefollowing,wereviewworksthatstudied
userperceptionsbasedonpairwiseitemsimilarityjudgments.
In Colucci et al. (2016), participants judged the similarity of movies in pairwise
comparisonsusingabinaryjudgment(yes–no).For62%oftheevaluationpairs,there
2 TheHerfindahlindexisusedasanalternativemeasureofconcentrationbiases,forinstance,inAdomavi-
ciusandKwon(2012).
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

774 M.Jesseetal.
was complete consensus among the participants. Yet, these human judgments were
only partly aligned with the output of three algorithmic similarity functions (with
the highest precision value being only .55). Building on this dataset, Wang et al.
(2017)designedtwocontent-basedrecommendationapproaches,whereoneconsid-
ered human perceptions in the recommendation process whereas the other did not.
Theirexperimentsshowedthatusersindeedpreferredtherecommendationsthatcon-
sideredthehumansimilarityjudgments.TheresultsbyColuccietal.(2016)andWang
etal.(2017)indicatethathumanslargelyagreeintheirsimilarityperceptionsofitem
pairs, while these perceptions are not aligned with algorithmic similarity functions.
Further,theirworksdemonstratethatdifferentsimilarityfunctionsresultindiscrep-
anciesbetweenobjectivesimilaritymeasuresandhumanperception.Differentlyfrom
theirworks,whichfocusonpairwiseitemsimilarities,ourworkfocusesontheper-
ceptionofentirelistsandthecorrespondencewiththeILSmeasure.
ThemoviedomainwasalsothefocusoftheworkbyYaoandHarper(2018).Intheir
work,theauthors evaluated similarityscoringalgorithms intermsof howwellthey
reflecttheusers’perceptions.Tothisend,studyparticipantshadtoratethesimilarity
of movie pairs which were selected with six different similarity scoring algorithms
spanningarangeofactivity-andcontent-basedapproaches.Theresultssuggestthat
content-basedapproachestodefiningthesimilarityofmoviesbestreflecttheusers’
perceptionofsimilarity.
TrattnerandJannach(2019)studiedinmoredepthhowspecificitemfeatures(e.g.,
title,plot,movieposter)—whenusedinacontent-basedsimilarityfunction—correlate
withthesimilarityofitemsasperceived byusers.DifferentlyfromYaoandHarper
(2018),theirstudydesignrequiredparticipantstocompareareferencemoviewitha
listofmovies.Thesimilaritymeasurebasedontagsreflecteduserperceptionswell,
which was also shown in Yao and Harper (2018). Moreover, capturing similarity in
the latent space using matrix factorization proved to be particularly powerful as it
did not only reflect user perceptions well but was also the approach that led to the
highest usefulness scores in terms of the participants’ interest in trying out a movie
recommendation.Inourpresentwork,wethereforerelyonlatentitemrepresentations
whencomparingitemsintwoofourstudies.Moreover,asthisapproachisdomain-
independent,itallowsustomakeacross-domaincomparison.
Human similarity judgments were also central to the work by Lee (2010) in the
musicdomain.Intheirwork,theauthorscollectedhumanjudgmentsonhow“musi-
callysimilar”pairsofsongswereviaAmazon’sMechanicalTurkplatform,andthey
thencomparedthosejudgmentswithagroundtruthofexpertjudgments.Onemain
findingoftheirworkwasthatcrowdsourcing—asalsodoneinourpresentstudy—can
be considered a reliable source for music similarity judgments. Some earlier work
in the music domain (Ellis et al. 2002), however, indicated that finding a computa-
tional metric that gives “reasonable agreement” with the human judgments can be
challenging.AndDownieetal.(2007)foundthatprovidingparticipantswithasim-
ilarity definition (here: “musically similar” or “melodically similar”) influences the
similarityjudgments.
In the food and recipe domains, van Pinxteren et al. (2011) employed a card-
sorting approach to identify ingredients, preparation techniques, cuisine, meal type,
andpreparationtimeasthemostrelevantcharacteristicsthatdeterminethesimilarity
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 775
of recipes. In Trattner and Jannach (2019), recommendations based on the recipe
instructions,title,andingredientlists,aswellasacombinedmodel,ledtothehighest
similarityperception.Inoneofourstudiesintherecipedomain,we,therefore,also
relyonacombinedapproachwhereweconsideringredientsandcookinginstructions
asitemmeta-data.
Finally,inthenewsdomain,Starkeetal.(2021)comparedseveralsimilarityfunc-
tions(basedontitle,bodytext,imagefeatures)andconcludedthatusingthearticles’
bodytextforcapturingsimilaritybetweennewsarticlescomesclosesttothehuman
similarityperception.Yet,inthisdomain,thesimilarityfunctionswereoverallshown
tobemuchweakerthanintherecipeandthemoviedomain.Thus,theysuggesttouse
otherfeaturesthanbodytextonlyincasetheusedsimilarityfunctionisspecifically
adapted thenews domain. Their cross-domain comparison suggests thatintermsof
capturingsimilarity,thenewsdomainisclosertothemoviethantherecipedomain;
although in general the news domain may require similarity functions that are less
“taste-related”thanintherecipeandmoviedomains.
2.3 Assessingthediversityperceptionofitemlists
Whileseveralworkshaveaddressedsimilarityperception,onlyafewhavespecifically
addressedthediversityperceptionoflists.Inthemusicdomain(specifically,electronic
music), for example, Porcaro et al. (2022) found that instrument and samples, sub-
genreorsub-style,tempo,andmoodstronglyinfluencewhattracklistswereconsidered
diverse. On the artist level, the artists’ origin and nationality, gender, and skin tone
were considered key factors for diverse music lists. They also found that the used
metricsreflectthediversityperceptionsparticularlywellforparticipantscomingfrom
Westernandeducatedsocietiesandintheagerangebetween18and35years.
Although primarily studying similarity perception, Trattner and Jannach (2019)
also address how similarity perception relates to diversity perception—specifically,
theperceptionoflistdiversity.Forboththemovieandrecipedomain,theitemfea-
turesdeterminingperceivedlistdiversitywerefoundtobesimilartothosedetermining
perceivedsimilarity.Formovies,thematrixfactorization-basedapproachwasapar-
ticularlyusefulapproachtocaptureusers’perceptionoflistdiversity.Similarly,title,
movieposter,plot,andgenrewereusefulfeaturesinacontent-basedapproach.Inthe
recipedomain,theimageofthedishasthebasisforthesimilarityfunctionreflected
theusers’listdiversityperceptionbest,followedbytitle,instructions,andtheingredi-
entslist.WhiletheworkofTrattnerandJannach(2019)andourpresentworkaddress
related topics and adopt similar research methodology, there are stark differences
betweenthetwoworks.TrattnerandJannach(2019)aimedtofindwaystoconstruct
similar-itemrecommendationsinareliableway.Specifically,theyinvestigatewhich
itemfeatures determinetheperceived similarityofagiven pairof items.Our work,
incontrast,aimstovalidateifcommonlyusedmetricsforlistsofitemsaresuitable
proxiesforhumanperceptions.
Overall,theexaminedpriorworkindicatesthatnotallsimilarityfunctionscorrelate
equallywellwiththesimilarityperceptionsofusers.Thus,thefindingsintheliterature
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

776 M.Jesseetal.
support the hypothesis investigated in our present work that the specifics of how a
similaritymetricisimplementedmatter.
3 Experimentaldesign
GoalsofStudiesWerecallthatthegoalofourresearchistoassessandvalidatetowhat
extent different ILS metrics correlate with the users’ perception of diversity in two
popularapplicationdomainsofrecommendersystems,movies,andrecipes.Further,
basedontheobservationsbyGeetal.(2011),weinvestigatewhethertheitems’order
withinalistimpactstheusers’perceptions.
Overview of Studies Overall, we conducted four complementary studies to address
these aspects. Essentially, in each of the studies, the participants were shown rec-
ommendation lists with different levels of ILS and asked to report their diversity
perceptions.Specifically,westudiedtheusers’perceptionswhen(i)latentitemrep-
resentationswereusedtocompareitemsandwhen(ii)application-specificsimilarity
measureswereapplied.Forboth,weexecutedthestudiesinthedomainsofmovies
and recipes. Figure 1 shows an overview of our four studies: Study-1 movies and
Study-1 rely on latent item vectors and involve nine different list types with
recipes
varyingILSlevelsanditemordersasourmanipulatedvariables. Study-2 movies and
Study-2 use domain-specific ILS metrics. In this second set of studies, we
recipes
focusonlyonvaryingtheILSlevels(low,mid,high),whichleadstothreelisttypes
perdomain.Inallstudies,eachlistshowntouserscontainedsevenitems.Weconsid-
eredlargerlistsizestobecognitivelytoochallengingforstudyparticipants,cf.Miller
(1956),JensenandLisman(1996).
Fig.1 Overviewofthestudies
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 777
In our experiment, we employ a mixed design. Each participant rated three lists,
whichconstitutesthewithin-subjectelementofthedesign.Whileallparticipantsrated
threelists,theselectionofthelistswasrandomizedand,thus,thesetoflistsvaried
acrossparticipants,whichconstitutesabetween-subjectselementofourdesign.
Subsidiary Research Questions While the main focus of our work is validating the
ILS metric, we also designed the studies to answer relevant subsidiary questions.
First, we addressed whether the familiarity of items influences the perception of a
list.SimilartoPorcaroetal.(2022),wheredomainknowledgeplayedaroleindiver-
sityperception, participants without background knowledge regarding a specific set
ofitemsmightperceivethelistdifferently(e.g.,morediverse)thanparticipantswith
more knowledge. Second, we addressed whether different diversity levels impacted
theparticipants’decisionprocesses,e.g.,intermsoftheirperceivedchoicedifficulty
orchoiceconfidence,cf.Puetal.(2011),Ekstrandetal.(2014).Third,weinvestigated
ifthepopularityoftheitemshadanyimpactontheperceptionofthelists.Asobserved
inotherworks(e.g.,Abdollahpourietal.2019),recommendersystemsmayfacethe
problem of popularity bias, which could eventually alter the way users perceive the
quality of the recommendations. Fourth, we checked for any gender-specific differ-
encesintheresponsesoftheparticipants.Lastly,wealsoexploredwhatwouldhappen
ifparticipantswerepresentedwithonlyonepairofverydissimilaritems,compared
topresentinganentirelistwithhighdiversity.
3.1 Creatingdiverserecommendationlists
CreatingListswithVariedDiversityLevelsTocreaterecommendationlistsofdifferent
diversity levels, we followed an approach which is both repeatable and as free as
possible from potential researcher bias. The general idea of our approach is to first
createasetofkrecommendationlistsforarandomlyselectedsetofusersfromagiven
datasetusingamatrixfactorizationapproach.3 Then,wecomputetheILSvaluesof
theserecommendationliststoobtainanestimateofthedistributionoftheILSvalues
foragivendataset.4
Basedonthisapproximateddistribution,wethenselectthreelistsoftheksampled
ones, which we then consider as representations of being of low, medium, and high
diversity.Inourcase,wesimplyusedthelistswiththelowestILSandthehighestILS
toserveasrepresentativesforalow-ILSandahigh-ILSlist,respectively.Todetermine
amid-ILSrepresentativelist,wecomputedthemeanofthejustdiscussedhighestand
lowestILSvalues.Then,wepickedtheonerecommendationlistfromthetensamples,
whichwasclosesttothismeanILSvalue.
Inadditiontothesethreelists,wedesignedtwomorespeciallistsforourexperi-
mentsforeachdomain.
3 Wenotethatmatrixfactorizationstillisahighlyeffectivemethodforthispurpose(Rendleetal.2020).
Technically,weusedthesvdmethodimplementedinthenumpyPythonlibrary.Wedeterminedtheoptimal
numberoflatentfactorsforeachdatasetusinggridsearch.Weshareallcodeonlineathttps://github.com/
ladychb/ils_study.
4 Inourexperiments,weusedk=10sampledlists.Infutureworks,alargervalueforkmaybeexplored
inordertoobtainacloserapproximationofthedistribution.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

778 M.Jesseetal.
Table1 Overviewofhowrecommendationlistsofincreasingsimilaritywerecreated
Abbr. Listtitle Description
reclow-ILS Recommendation-based(low-ILS) This list is created by choosing ten
randomusersandcreatingtop-Nrec-
ommendationsusingmatrixfactoriza-
tion.Wethenselectthelistwiththe
lowestILS
recmid-ILS Recommendation-based(mid-ILS) Createdlikereclow-ILS,butweselect
thelistwithamediumILS
rechigh-ILS Recommendation-based(high-ILS) Createdlikereclow-ILS,butweselect
thelistwiththehighestILS
popsim Popular&Similar Wecreatethislistbyrandomlyselect-
ing one of the top 20 items in the
datasetandfindingthesixmostsimi-
laritemsinthetop-Nitems.Theorder
oftheresultinglistwasrandomized
upp UpperBound Alistofrelatedfilmsinafranchise
in the movie domain (“Batman”); a
setofmanuallyselectedverysimilar
muffinrecipesinthefooddomain
– Thefirstofthem,whichwecallpopsim,wascreatedbyrandomlypickingoneof
the20mostpopularitemsineachdatasetandthendeterminingtheirmostsimilar
itemsamongthe100mostpopularitems.Wecreatedthislisttostudythediversity
perceptionofliststhatcontainpopularsimilaritems,which—atleastinthemovie
domain—are also often items that users are familiar with. We note that popular
itemrecommendationsarecommonlyusedasasimplebaselineinresearchworks.
Avalidationofthisbaselineapproachisthereforeaparticularlyusefulreference
pointforworksonrecommendersystemsalgorithms.
– Thesecondlist,whichwenamedupp,servesasaproxyforanupperboundfor
ILS values that we may realistically observe in practice. In the movie domain,
we selected a collection of sequels for this purpose (“Batman”); in the recipe
domain,wemanuallypickedasetofhighlysimilarrecipesformuffins.Withupp,
wecreatedlistswithasetofitemswithaclose-to-maximumILSvalue.
ThisprocessgivesusfivelistswithdifferentlevelsfortheILSvalues.Anoverview
oftheselistsisgiveninTable1.
Intermsoftechnicaldetails,wereliedontwopublicdatasetsinourexperiments
thatcontainuser-itemratingsandmeta-data,MovieLens-25M5forthemoviedomain
andtheFoodRecSysdataset6 forrecipes.WeconsideredtwowaysofcomputingILS
valuesforthecreatedlists:
– Adomain-independentapproach:Giventheinsightsfromearlierresearch(Trat-
tner and Jannach 2019; Yao and Harper 2018), we measured the ILS of a set of
recommendationsbasedonthecosinesimilarityoflatentitemvectors(or:embed-
5 https://grouplens.org/datasets/movielens/25m.
6 https://www.kaggle.com/datasets/elisaxxygao/foodrecsysv1.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 779
Table2 Overviewofhowrecommendationlistswithdifferentorderswerecreated
| Abbr.  | Listtitle         | Description |                          |
| ------ | ----------------- | ----------- | ------------------------ |
| recmin | Recommendation-   | From the    | Recommendation-based     |
|        | based (mid-ILS,   | (mid-ILS)   | list, we randomly select |
|        | minimize similar- | one item.   | Based on this reference  |
|        | ityofneighbors)   | item, we    | choose the least similar |
|        |                   | item and    | put it next. We continue |
thisprocessuntilallsevenitemsare
placed.
| recmax | Recommendation-  | Similar to                      | recmin, but this time we |
| ------ | ---------------- | ------------------------------- | ------------------------ |
|        | based (mid-ILS,  | placetheitemswiththehighestsim- |                          |
|        | maximizesimilar- | ilaritynexttoeachother          |                          |
ityofneighbors)
| popsimmin | Popular & Simi-  | Identicaltorecminwiththedifference |     |
| --------- | ---------------- | ---------------------------------- | --- |
|           | lar(minimizesim- | thatweusepopsimasthebaselist       |     |
ilarity of neigh-
bors)
| popsimmax | Popular & Sim- | Identicaltorecmin,exceptthatweuse |     |
| --------- | -------------- | --------------------------------- | --- |
|           | ilar (maximize | popsimasthebaselist               |     |
similarity of
neighbors)
dings)ofthelistelements.Weobtainedthelatentvectorsdirectlyfromtheused
matrixfactorizationmodel.
– A domain-specific approach: In this case, we used item meta-data—genre for
moviesandrecipedescriptionsfortherecipes—tocomputethesimilaritybetween
items.Moredetailsforeachdomainaregivenlaterbelow.
CreatingListswithVariedItemOrderingsTostudypotentialeffectsoftheitemorder,
wecreatedfouradditionallists.Twooftheselistswerepermutationsofrec mid-ILS and
twowerepermutationsofpopsim.Ourrationaleforcreatingthepermutationswasto
add(a)alistvariationwheretheneighboringitemsareassimilaraspossible(rec
max
and popsim max ), and (b), a variation where the neighboring items are dissimilar
(rec and popsim ).Ourhypothesisisthatclustersofsimilaritems(e.g.,atthe
| min | min |     |     |
| --- | --- | --- | --- |
beginning of a list) may make a set of recommendations appear more similar than
when the items are dispersed over the list; see also Ge et al. (2012). Technically,
to build these lists that either maximize the similarity of neighbors or minimize the
similarityofneighbors,werandomlypickedoneitemofthebaselistandthenadded
the remaining items iteratively in a way that either the most similar or least similar
itemwasappendedtothelist.Inthebeginning,therandomlyselecteditemisusedasa
referenceandthesimilaritytoalltheotheritemsiscalculated.Thisprocessisrepeated
withthelatestappendeditemasthenewreferenceuntilallitemshavebeenplacedin
thelist.Table2providesanoverviewofthesefouradditionallistswithdifferentitem
orders.
Overall, this process left us with nine different lists, where the first five were
designedtorepresentlistsofdifferentILSlevels,andwherethelastfourwerevaria-
tionsoftwoofthelistsforwhichwechangedtheitemorderings.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

780 M.Jesseetal.
Fig.2 Experimentprocess
3.2 Experimentflowanddetails
Tasks for Participants The tasks for the participants—as outlined in Fig. 2—were
identicalinallfourstudies.Afterreadingtheinstructionsandafterinformedconsent,
eachparticipantwasshownthreelistsofrecommendations,allfromthesamedomain.
Foreachoftheselists,participantshadthentoselectoneitemtowatch(movies)or
tryout(recipes)next.Inaddition,theyhadtospecifytheirfamiliaritylevelforeachof
theshownitems7,whichallowsustoanalyzeifitemfamiliarityhasaneffectonuser
perception.Moreover,sixquestionsregardingthesimilarity/diversityperceptionand
the choice experience were asked before the participants could move on to the next
list.TheexactquestionsforthemoviedomainareshowninTable3andfortherecipe
domainintheAppendix.
After providing feedback on the three lists, participants were shown a pair of
“extreme”itemsfromoneoftherecommendationlists,i.e.,twoitemswiththelowest
pairwise similarity. Again, participants had to express their similarity/diversity per-
ceptionforthispair.Withthisadditionalquestion,ourgoalistoassesstowhatextent
thediversityperceptionofthepairofextremesiscorrelatedwiththatofanentirelist.
Next,tounderstandwhatmakesalistdiverseforparticipantsinagivendomain,
we asked them to explain in free text what criteria they used to assess the diversity
ofalistofmoviesandrecipes,respectively.Afterthisstep,participantshadtorank
pre-definedcriteria8asdoneinTrattnerandJannach(2019).Finally,weaskeddemo-
graphicquestionsinthepost-taskquestionnaire(agegroup,gender,domainexpertise).
Setup of the Individual Studies The studies in the first phase were identical except
for the domain. The same is true for the second phase. The difference between the
two study phases lies (i) in the type of the used ILS metric and (ii) in the set of the
examinedlistsfromTables1and2.
– Phase 1: In Phase 1, the similarity of items was based on latent item vectors
asmentionedabove.Participantswereassignedthreelistsfromallninetypesas
presentedinTables1and2inarandomizedprocess.Toavoidthattoosimilarlists
werepresentedtooneparticipant,whichmaybiastheirperceptions,weensured
thateveryparticipantreceivedexactlyonerecommendation-basedlist(rec ,
mid-ILS
rec , or rec ) and exactly one homogeneous list (popsim, popsim , or
min max min
popsim ). For each of these two list types (i.e., recommendation-based and
max
7 Forthemoviedomain,theoptionswere“neverheardof,”“haveheardof,”“haveseenit.”Theoptions
fortherecipedomainweresimilar:“thetypeofrecipeisnewtome,”“Ihavepreparedasimilardish,”“I
havepreparedthisdish.”
8 Inthemoviedomain,thesevencriteriaweregenre,actors,coverimage,plot,runtime,title,andrelease
year.Intherecipedomain,theeightcriteriaweretitle,nutrients,recipeimage,ingredients,cuisine,cooking
duration,reviews,andinstructions.Participantswerenotforcedtorankallcriteria.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 781
tsilhcaerofsmetieriannoitseuQ
3elbaT
epyT
sucoF
noitseuQ
elacstrekiLtniop-5
ytisreviD
esrevideratsilsihtnidetneserpseivomehT
)ytisrevid(1Q
elacstrekiLtniop-5
ytisreviD
yteiravhcirareffotsilsihtnidetneserpseivomehT
)yteirav(2Q
elacstrekiLtniop-5
ytisreviD
rehtohcaeotralimiseratsilsihtnidetneserpseivomehT
)ytiralimis(3Q
elacstrekiLtniop-5
ssenisaEeciohC
ysaesawhctawoteivomtxenehtgnitceleS
)ssenisaeeciohc(4Q
elacstrekiLtniop-5
ecnedfinoCeciohC
txenhctawotdetcelesIeivomehtekillliwItnedfinocmaI
)ecnedfinoceciohc(5Q
srewsnadenfied-erP
snoitpodoogfo.oN
…deniatnoctsilehT
)snoitpodoogfo.on(6Q
,.g.e,selbatrehtonidnaerehstcepsaehtfosemanehtesuylnoew,ytiverbroF.ytisreviddeviecrepgnidrager,.g.e,snoitpecrepresunoerewsnoitseuqehttahtetoneW
”dekilItahtnoitpoon“”,noitpodoogenoyltcaxe“”,noitpodoogenonahterom“erew6QrofsnoitpoehT.ytisrevid
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

782 M.Jesseetal.
homogeneous),onelistisselectedrandomlyforeachparticipant.Therefore,we
areabletocompare,acrossmultipleparticipants,iftheorderofitems,onaverage,
makesadifferenceonthehumanperception.
– Phase 2: In Phase 2, the ILS metric was based on meta-data: we used genre
overlap for the movie domain, as done, e.g., by Vargas et al. (2014), and cosine
similarityoftheLatentDirichletAllocation(LDA)embeddingsofingredientsand
cookingdirectionsasdonebyHauptmannetal.(2021).Werecallthatwepurposely
selectdifferenttypesofmeta-dataforeachdomain. Usingthesedifferentmetric
implementations,ourgoalistoassessthediversityperceptionswhentheILSmetric
isbasedoncommonlyusedmeta-data.Aswestudiedpotentialordereffectsalready
inPhase1,weonlyconsiderthethreerecommendation-basedlistswithvarying
diversitylevelsinPhase2.
3.3 Participants
WerecruitedcrowdworkersasparticipantsthroughAmazon’sMechanicalTurkplat-
form. To ensure high-quality responses, we only invited crowdworkers who had an
approvalrateofatleast99%andwhohadalreadysuccessfullycompletedmorethan
500tasks.Asanothermeasuretoincreasethereliabilityoftheresponses,weincluded
twoattentionchecksinthequestionnaires,andwefilteredoutthosecrowdworkerswho
didnotworkcarefullyandmissedthesechecks.Onaverage,theparticipantsneeded
9minutesforthetaskandreceivedapaymentof1.5$–2$onsuccessfulcompletion.
Overall, 791 participants completed the study, of which 531 were considered
reliable after the attention check. The number of participants per study were
223 for Study-1 movies , 195 for Study-1 recipes , 55 for Study-2 movies and 58 for
Study-2 . We recruited a smaller number of participants for Phase 2 because
recipes
weconsideredfewerlistsinthisphase.Fromallstudyparticipants,around60%were
male and almost 40% were female. Three participants identified themselves with a
differentgender.Themajorityoftheparticipantswerebetween26and35yearsold
(41%).
Participantswhowereinvolvedinthestudiesinthemoviedomain(Study-1 movies ,
Study-2 movies )anaveragereportedthemselvestobequiteengagedinmovies,andwe
foundnodifferencebetweenthestudypopulationsinthatrespect.Specifically,when
participantswereaskedabouttheirinterestinmovies,theiraverageresponseswhere
3.86(SD =0.98)inStudy-1 movies and3.87(SD =1.00)inStudy-2 movies .
Looking at the participants’ cooking behavior and preferences, we also observe
that participants in both study phases were very similar. Around two-thirds of the
participantsineachphasereportedcookingatleastfourtimesperweek.Almost70%
ofparticipantsinbothphaseshadnorestrictionsineatingbehavior,around17%were
vegetarians,6%werevegans,andabout8%mentionedrestrictionsforotherreasons
including religious ones, gluten intolerance, and allergies. We note here that none
of the participants with such restrictions provided negative feedback regarding our
selectionofrecipes;andallofthemstatedthattheyfoundatleastonerecipeinthe
listthattheyliked.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

| Intra-listsimilarityandhumandiversityperceptions... |     |     | 783 |
| --------------------------------------------------- | --- | --- | --- |
Table4 ILSvaluesforStudy
|     | List | Movies | Recipes |
| --- | ---- | ------ | ------- |
Phase1,usinglatentitem
| vectors | reclow-ILS  | 0.37 | 0.38 |
| ------- | ----------- | ---- | ---- |
|         | recmid-ILS  | 0.41 | 0.41 |
|         | rechigh-ILS | 0.46 | 0.44 |
|         | popsim      | 0.41 | 0.35 |
|         | upp         | 0.51 | 0.46 |
|         | recmin      | 0.41 | 0.41 |
|         | recmax      | 0.41 | 0.41 |
|         | popsimmin   | 0.41 | 0.35 |
|         | popsimmax   | 0.41 | 0.35 |
4 Results
Inthissection,wediscusstheresultsofourstudieswithrespecttothegivenresearch
questions.
4.1 RQ1:CorrespondenceofILSandhumandiversityperception
4.1.1 ResultsforPhase1:usinglatentitemrepresentations
InPhase1,weusedlatentitemrepresentationsasthebasisforcomparingitemswith
the cosine similarity measure. The computed ILS metric values for the movies and
recipedomainsareshowninTable4.Generally,weobservethattherangeofobtained
ILSvaluesisnottoolarge(from0.35to0.51).Forthemoviedomain,theILSvalueof
therec andpopsim listswereincidentallyverysimilar(around0.41).Those
mid-ILS
listsinwhichonlytheorderwaschanged(i.e.,rec min andrec max ; popsim min and
popsim )haveofcourseidenticalILSvalues.
max
The highest ILS value, as expected, is obtained for the upp lists, which consist
of hand-picked items that are assumed to be very similar. The lowest similarity in
the movie domain is found for therec low-ILS list. In the recipe domain, the lowest
similarity—andthushighestdiversity—isobservedforthepopsim
listconsistingof
popular items. This may appear a bit surprising because the list was constructed by
addingitemssimilartoarandomlyselectedpopularreferenceitem.However,aswe
limited the set of candidate items for this list to the 100 most popular items, the
overall ILS value remained comparably low. This confirms previous findings that
the recommendation of the most popular items in some domains can lead to quite
diversifiedlists(e.g.,Ribeiroetal.2015;Vargasetal.2014).
Table5andFig.3showtheaverageresponsesforthequestionsonthesubjective
perceptions for Study-1 movies , ordered by the values for Q1 on diversity. Looking
attheresponsesforQ1,weobservethattherankingofthelistsroughlyfollowsthe
patternsfortheILSmetricreportedinTable4.Ontopofthelist,wefindrec ,
low-ILS
rec mid-ILS ,andrec max ,wherethelatterisareorderedversionofrec mid-ILS tomax-
imizethesimilarityofneighboringelements.Thus,listswithlowILSvaluesleadto
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

784 M.Jesseetal.
Table5 ResultsforStudy-1movies(movies,9lists);numbersshowaverageresponsesandstandarddevi-
ations
List ILS Q1 Q2 Q3 Q4 Q5
Diversity Variety Similarity Choiceeasiness Choiceconfidence
recmax 0.41 4.14(0.90) 4.11(0.90) 2.61(1.31) 3.76(1.10) 4.26(0.88)
recmid-ILS 0.41 4.12(0.83) 4.03(1.05) 2.84(1.24) 4.14(0.88) 4.27(0.71)
reclow-ILS 0.37 4.05(1.00) 4.14(1.00) 2.59(1.35) 3.78(1.04) 4.18(0.84)
recmin 0.41 3.94(0.79) 4.01(0.74) 2.97(1.20) 4.03(0.96) 4.12(0.99)
popsim 0.41 3.86(0.96) 3.82(1.11) 3.15(1.27) 3.65(1.18) 4.04(0.99)
popsimmax 0.41 3.76(0.91) 3.82(0.95) 2.91(1.09) 3.75(1.07) 4.14(0.86)
popsimmin 0.41 3.75(0.88) 3.75(0.97) 3.04(1.12) 3.78(1.13) 4.13(0.82)
rechigh-ILS 0.46 3.17(1.14) 3.24(1.22) 3.68(1.02) 3.96(0.96) 4.32(0.90)
upp 0.51 2.37(1.32) 2.60(1.49) 4.43(0.93) 3.77(1.12) 4.15(1.10)
Fig.3 AverageresponsesinStudy-1movies(movies,9lists)
high diversity perceptions. At the bottom end of the list, we find upp, as expected,
andalsorec ,whichhasahighILSvalue.Generally,wethereforefoundthat
high-ILS
the ILSvalue of a listand theusers’ perceptions are wellaligned inthis study. The
SpearmancorrelationcoefficientsbetweentheILSwithsubjectiveperceptionswere
−0.39fordiversity,0.37forvariety,and0.44forsimilarity,whichcorrespondstoa
mediumcorrelation.Allcorrelationsweresignificantwith p <.001.Theanswersto
questionsQ2(variety)andQ3(similarity)arealsopositivelyandnegativelycorrelated
withdiversity,whichisalsoexpected.
AKruskal–Wallistest9 revealedsignificantdifferencesforthevariablesdiversity,
variety,andsimilaritywithallpvaluessmallerthan.001.Nosignificantdifferencewas
observedatthesignificancelevelα =.05forchoiceeasinessandchoiceconfidence.
9 Aseveryparticipantgavefeedbacktothreelists,thesethreeassessmentsperparticipantmightpossibly
becorrelated,whichwouldnotmeetthetestassumptionthattheobservationsareindependent.Toassessif
thisproblemexists,wefittwotypesofregressionmodelsforeachvariable.Oneregressionassumedthat
allobservationswereindependent;theotherwasamixed-effectsmodelthatconsideredthehierarchical
(user-level)structureinthedata.Inthemixed-effectsmodel,wedidnotobserveahighinterclasscorrela-
tioncoefficient.Moreover,theobtainedregressioncoefficientsforbothmodelswerealmostidentical.We
thereforeconcludethattheparticipant-relatedeffectsareminimal,andusingtheKruskal–Wallistestas
wellasWilcoxontestsfortheposthocanalysesisappropriate.Thesameanalysiswasperformedforthe
otherthreestudies.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 785
Forchoiceeasiness,wehoweverobservesometendencythatselectingfromthelists
with popular items (e.g., popsim) and with high similarity (e.g., rec ) was
high-ILS
perceivedtobemoredifficult;with p =.06,theoveralldifferencesaccordingtothe
Kruskal–Wallistestwereonlysignificantwithanαlevelof.10.10
WethenperformedaposthocanalysiswithWilcoxon’ssignedranktest,inwhich
wemadepairwisecomparisons.Bonferronicorrectionwasappliedtothealphalevelto
accountappropriatelyforthesemultiplecomparisons.Theobservationsfordiversity,
variety,andsimilarityareoftensimilarandweonlyreportselectedresultsfordiversity
here.11
Looking at the obtained numbers, we found that the diversity perception of a
list of movie sequels (upp) and the recommendation list with the highest ILS value
(rec ) was significantly lower than for all other lists. Interestingly, while we
high-ILS
found that the difference between rec and rec was significant, the
high-ILS mid-ILS
differencebetweenrec mid-ILS andrec low-ILS wasapparentlynotnoticedbythepar-
ticipants.Theresponsesobtainedforthepopsim listwerenotsignificantlydifferent
fromtheotherlists(exceptforthesequelsintheupplist).
Table6showstheresultfortherecipedomaininPhase1,i.e.,againusinglatent
item vectors as a basis for the similarity computations and ordered by the values
forQ1ondiversity.12Inlinewiththemoviedomain,aKruskal–Wallistestindicated
significantdifferencesfordiversity,variety,andsimilarity,andnodifferenceforchoice
easinessandchoiceconfidence.Lookingattheresultsoftheposthoctests,however,
thedifferencesbetweenthevarioustreatmentgroups,i.e.,listsofdifferentdiversity
levels,arequitesmallandstatisticallynot significant.Anexceptionisthemanually
constructedupplist,whichishowevernota“natural”recommendationlistbutservesas
anupperboundinourstudy.Notably,thedifferencebetweenthenaturallistrec low-ILS ,
rec , and rec are not significant for diversity, variety and similarity.
mid-ILS high-ILS
In other words, differently from Study-1 movies , the ILS metric in Study-1 recipes
cannot be considered a reliable proxy for user perceptions. This suggests that the
particular choice of how the ILS metric is implemented matters, and what works in
oneapplicationmightnotworkwellinanother.
4.1.2 ResultsforPhase2:usingdomain-specificmeta-data
Next,welookattheresultsobtainedinPhase2,whereweusedapplication-specific
meta-data to determine the similarity between two items and thus compute the ILS
metric. Table 7 and Fig. 4 show the results for the movie domain, where we used
genreinformationwhencomparingmovies.Recallthatweonlyinvestigatedthreelists
(rec low-ILS ,rec mid-ILS ,andrec high-ILS )inthisphase,astheotherresearchquestions
regardingtheitemordering,canbeansweredwiththeresultsobtainedinPhase1.The
results in Table 7 show a trend in terms of diversity, variety, and similarity, but the
differencesaretoosmalltoreachstatisticalsignificanceaccordingtoaKruskal–Wallis
10 WeappliedKruskal–WallistestbecausetheprerequisitesforapplyingANOVAwerenotfulfilled.
11 ThedetailedstatisticscanbefoundintheAppendix.
12 SeeFig.5inAppendixforavisualrepresentationofthedata.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

786 M.Jesseetal.
Table6 ResultsforStudy-1recipes(recipes,9lists);numbersshowaverageresponsesandstandarddevi-
ations
List ILS Q1 Q2 Q3 Q4 Q5
Diversity Variety Similarity Choiceeasiness Choiceconfidence
reclow-ILS 0.38 4.31(0.63) 4.33(0.68) 2.87(1.44) 3.96(1.07) 4.33(0.74)
rechigh-ILS 0.44 4.22(0.57) 4.26(0.66) 2.82(1.32) 3.96(1.14) 4.21(0.66)
recmin 0.41 4.16(0.76) 4.27(0.80) 2.98(1.28) 4.17(1.14) 4.33(0.60)
popsimmin 0.35 4.16(0.76) 4.27(0.80) 2.98(1.28) 4.17(1.14) 4.33(0.60)
recmid-ILS 0.41 4.16(0.72) 4.23(0.77) 2.53(1.21) 3.86(0.81) 4.27(0.65)
recmax 0.41 4.05(0.62) 3.95(0.81) 2.88(1.21) 3.79(1.07) 4.25(0.70)
popsimmax 0.35 4.05(0.62) 3.95(0.81) 2.88(1.21) 3.79(1.07) 4.25(0.70)
popsim 0.35 3.80(0.92) 3.77(0.96) 3.28(1.13) 4.02(0.96) 4.17(0.98)
upp 0.48 2.37(1.22) 2.68(1.46) 4.19(0.90) 3.65(1.04) 3.95(0.89)
Table 7 Results for Study-2movies (movies, 3 Lists); numbers show average responses and standard
deviations
List Q1 Q2 Q3 Q4 Q5
Diversity Variety Similarity Choiceeasiness Choiceconfidence
reclow-ILS 4.09(0.61) 4.20(0.68) 2.64(1.12) 3.95(0.92) 4.35(0.75)
recmid-ILS 4.11(0.57) 4.07(0.77) 2.75(1.09) 3.98(0.87) 4.31(0.74)
rechigh-ILS 3.82(0.89) 3.84(0.90) 2.96(1.12) 3.69(0.98) 4.20(0.80)
Fig.4 AverageresponsesinStudy-2movies(movies,3lists)
testwithα = .05.13 Asimilartrendcanbeobservedforchoiceeasiness,wherethe
difficultyseemstoincreasewhenthelistislessdiverse.Butagain,thedifferencesare
notstatisticallysignificantatthe.05thresholdlevel(p =.15).Overall,theresultsfor
diversity,variety,andsimilarityin Study-2 movies arenot alignedwiththeresultsin
Study-1 movies ,wherewecouldobserveadifferenceinuserperceptions.
Table8finallyshowstheoutcomesforStudy-2 ,wherethesimilaritybetween
recipes
recipes was based on comparing embeddings of the recipe ingredients and cook-
13 Thepvaluesareatabout.12fordiversity,.10forvariety,and.29forsimilarity.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

| Intra-listsimilarityandhumandiversityperceptions... |     |     |     |     |     |     |     | 787 |
| --------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
Table 8 Results for Study-2recipes (recipes, 3 Lists); numbers show average responses and standard
deviations
| List | Q1        | Q2      |     | Q3         |     | Q4             | Q5               |     |
| ---- | --------- | ------- | --- | ---------- | --- | -------------- | ---------------- | --- |
|      | Diversity | Variety |     | Similarity |     | Choiceeasiness | Choiceconfidence |     |
reclow-ILS 4.02(0.64) 4.07(0.78) 3.27(1.26) 3.73(0.86) 4.10(0.62)
recmid-ILS 4.03(0.65) 4.07(0.76) 3.14(1.23) 3.73(0.94) 4.15(0.70)
rechigh-ILS 3.46(1.00) 3.49(1.05) 4.00(0.74) 3.95(0.77) 4.10(0.63)
Table9 Summaryofmainstudyoutcomes(RQ1)
| Study |     | Similaritybasedon… |     |     |     |     | Diversity | perceptions |
| ----- | --- | ------------------ | --- | --- | --- | --- | --------- | ----------- |
significantlydifferent?
| Study-1movies  |     | Latentitemvectors            |     |     |     |     | Yes |     |
| -------------- | --- | ---------------------------- | --- | --- | --- | --- | --- | --- |
| Study-1recipes |     | Latentitemvectors            |     |     |     |     | No  |     |
| Study-2movies  |     | Application-specificfeatures |     |     |     |     | No  |     |
| Study-2recipes |     | Application-specificfeatures |     |     |     |     | Yes |     |
ingdirections.14 AKruskal–Wallistestindicatedsignificantdifferencesfordiversity
| = .001), |         | =   | .003), |            |     | < .001). |          |            |
| -------- | ------- | --- | ------ | ---------- | --- | -------- | -------- | ---------- |
| (p       | variety | (p  | and    | similarity | (p  |          | Post hoc | tests then |
revealed significant differences (with p < .002 after Bonferroni correction) for all
| three variables | when | comparing | (a) | rec     | vs. | rec      | and (b) | rec     |
| --------------- | ---- | --------- | --- | ------- | --- | -------- | ------- | ------- |
|                 |      |           |     | low-ILS |     | high-ILS |         | mid-ILS |
.15 vs. rec high-ILS This stands in contrast to Study-1 recipes , where we could not
observe statistically significant differences. Again, therefore, these results confirm
thattheparticularitiesofhowtheILSmetricisimplementedcanmakeadifference.
Table9summarizesourstudyoutcomesinthecontextofRQ1.Usinglatentitem
vectors for similarity assessments worked well for the movie domain but not for
recipes.Thesimilaritymetricsbasedonapplication-specificfeatures,incontrast,only
workedwellfortherecipedomainbutnotformovies.
Next,weanalyzedoursubsidiaryresearchquestions.First,astheitems’popular-
ity could potentially bias the users’ diversity perception, we explored if there is a
corresponding correlation. Second, we explored potential gender differences in the
participants’ responses. For instance, Knijnenburg et al. (2011) highlight a possible
effectofgenderontheperceptionofthequalityandvarietyofrecommendations.
Toanswerthefirstquestion,wecalculatedthepopularitylevelofeachlisttoanalyze
potential correlations between the popularity of the items in a list and the diversity
perceptionofalist.Tothisend,wedefinedthepopularitylevelofalistasthemean
ofthenumberofratingsoftheitemsinalist;anoverviewofthepopularitylevelscan
befoundinTable21forthemoviedomainandTable22fortherecipedomain,both
intheAppendix.
14 SeeFig.6inAppendixforavisualrepresentationofthedata.
15
Again,however,theuserperceptionsinthesethreedimensionswerenotsignificantwhencomparing
thereclow-ILSandrecmid-ILSconditions,similartowhatwasobservedinStudy-1movies.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

788 M.Jesseetal.
WethencomputedtheSpearmanrankcorrelationcoefficienttoassesstherelation-
shipbetweenlistpopularityanddiversityperception.Forbothdomains,wefoundthe
correlationtobenotstatisticallysignificantatthechosenthreshold(α =.05).The p
valuesforthemoviedomainwere p = .23andfortherecipedomain p = .95.We
therefore have no evidence that the popularity level of a list strongly influences the
users’diversityperceptionsinourstudy.
To address the second side question, we investigated if there are gender-related
differencesintheparticipants’responses16 Astheprerequisitesforat-testwerenot
fulfilled17,weusedaWilcoxontest.AllresultsoftheWilcoxontestaresummarized
in Table 20 in the Appendix. The Wilcoxon test revealed no statistically significant
difference in the means for male and female respondents for any of our variables
(withα = .05).Therefore,wefoundnoindicationforsignificantdifferencesinhow
differentgendersperceivedtherecommendationsthatwereprovidedtothem.
4.2 RQ2:Impactofitemorderonuserperceptions
ApreviousstudyGeetal.(2012)suggestedthattheorderoftheitemsina(diversified)
list may impact user perceptions. As described above, our study therefore involves
permutedversionsofthepopsimandrec listsinwhichthesimilaritybetween
mid-ILS
neighboring elements was either minimized or maximized. Minimization leads to
clusters of similar items, whereas maximization makes sure that similar items are
moredispersedacrossthelist.
The post hoc analysis of the relevant pairs in the sets {popsim, popsim ,
min
popsim }and{rec ,rec ,rec }revealednosignificantdifferencesin
max mid-ILS min max
termsofdiversity,variety,andsimilarity,bothinStudy-1 movies andinStudy-1 recipes .
Allpvaluesinthesepairwisecomparisonwereactuallycloseto1.Thus,ourstudiesdo
notprovideanyevidencethattheorderoftheelementsimpactedtheusers’diversity,
variety,andlistsimilarityperceptions.
However,wecannotruleoutthatordereffects,asreportedinGeetal.(2012),may
existingeneral.ComparedtothestudybyGeetal.(2012),whereparticipantshadto
assessthediversityofalistoftwelveitems,thenumberofitemsintherecommendation
listwaslimitedtosevenitemsinourcase.Thismayhaveimpactedtheoutcomesof
our study. Also,Geet al.(2012) reliedon manually diversified lists(e.g.,including
severalanimationmoviesintoalistthatwaslabeledtobeactionmovies),whichwere
probablymore“extreme”intermsofthediversityofthelistelements.Moreover,in
some of their treatments, these diverse elements (e.g., all animation movies in the
action movie list) were manually bulked together at the top or bottom of the lists,
or manually dispersed across the list. This may have also led to stronger effects of
theorderingsthanweobservedinourstudy.Overall,wethereforebelievethatmore
studiesareneededtoassesstheeffectsofitemplacementsonuserperceptions.
16 Forthisanalysis,weonlyconsideredmaleandfemaleparticipantsbecauseoursampleincludedonly
oneparticipantwhoidentifiedasbeingnon-binaryandtwowhopreferredtonottoindicatetheirgender.
17 Shapiro–Wilktestsindicatedthattheresponsesforallvariablesdeviatedsignificantlyfromanormal
distribution.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 789
Regarding the questions of choice easiness and choice confidence, no significant
differenceswerefound—neitherinStudy-1 movies norinStudy-1 recipes ,asdiscussed
above. This is in some way aligned with the results of Ge et al. (2012), where no
significant impact on user satisfaction was found when the order of the items was
changed. From the results shown in Tables 5 and 6, we can observe a slight trend
in terms of choice easiness for the natural recommendation lists. In both studies,
choiceeasinessisconsistentlyhigherwhensimilaritemsarenotclusteredtogether,
i.e., choices are easier forrec than forrec . These differences were however
min max
notfoundtobesignificant.Forthepermutationsofthepopsimlists,whichconsistof
ratherpopularitems,thistrendwasnotobserved.
Asforthelastanalysesinthiscontext,rememberthatweaskedstudyparticipants
toratethesimilarityofthetwomostdissimilaritems(intermsofthegivenILSmetric)
aftertheyhadassessedanentirelistofrecommendations.Thisadditionalmeasurement
serves two purposes. First, it helps us assess if participants were consistent in their
assessments.Iftheyareconsistent,thesimilarityassessmentfortheextremeitempair
should be lower than the one for the entire list. Second, if this is the case, it would
also support that the design principle of the ILS metric, which is based on pairwise
comparisonsofallitems,isvalid.Ifthesimilarityassessmentoftheextremepairwould
beverysimilartotheassessmentfortheentirelist,thenthesimilarityperceptionofthe
participantsmightbemainlyguidedbytheextremesandnotbythelistinitsentirety.
As an example for an extreme pair, we asked participants who saw and assessed
the rec list to judge the similarity of the list’s extreme items “Avatar” and
mid-ILS
“Harry Potter and the Order of the Phoenix.” In the recipe domain, an example of
an extreme pair is “Award Winning Soft Chocolate Chip Cookies” and “Orzo with
Parmesan and Basil.” Overall, there were four such pairs in the movie domain and
four pairs in the recipe domain.18 The results were consistent for all eight pairs in
that the similarity assessments of the individual pairs were lower than those of the
listsinwhichtheywerecontained.Thenumbersobtainedforpairsofmoviesandthe
lists that contained these pairs are shown in Table 10. The differences between the
pairandlistassessmentswereevenstrongerfortherecipedomain.19Weassumethat
thisisthecasebecausetheprovidedlistsoftencontainedrecipesforlargelydifferent
typesofdishes,e.g.,maindishesanddesserts.Overall,however,wefindthat(a)the
participantsareconsistentintheirassessmentandthat(b)theusersactuallyconsider
morethantheextremepointsinalistwhentheyjudgethediversity(or:similarity)of
alist.
4.3 RQ3:Criteriathatdeterminesimilarityassessments
Withthisresearchquestion,ourgoalistoobtainabetterunderstandingofhowusers
assessthesimilaritiesofitemsinthetwoexamineddomains.Inapracticalapplication,
suchanunderstandingisimportanttoappropriatelydesignasuitablesimilarityfunc-
tionthatmaythenbeusedintheILScomputation.Inourexperimentflowdescribed
inFig.2,participantshadtoaccomplishtwoadditionaltasksaftertheyhadassessed
18 Rememberthattherewerethreerecommendation-basedlistsandoneconsistingofpopularmovies.
19 ThedetaileddatafortherecipedomainareprovidedintheAppendix.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

| 790 |     |     | M.Jesseetal. |
| --- | --- | --- | ------------ |
Table10 Assessmentofthemostdissimilaritemsandtheentirelist(i.e.,recmid-ILS)inthemoviedomain
| Pairassessment  |                    |            | Containinglist |
| --------------- | ------------------ | ---------- | -------------- |
| Movie1          | Movie2             | Sim.(SD)   | Sim.(SD)       |
| Avatar          | HarryPotterand…    | 2.70(1.20) | 2.84(1.24)     |
| Inception       | LordoftheRings…    | 2.35(0.97) | 2.84(1.24)     |
| TheAvengers     | MonstersInc.       | 2.25(1.23) | 2.84(1.24)     |
| LordoftheRings… | 2001:ASpaceOdyssey | 2.14(1.15) | 2.84(1.24)     |
Table11 Mostfrequentcodesinfree-textresponsesregardingthecriteriathatdeterminemoviesimilarities
| Code                                              |     | Percentageofappearance |     |
| ------------------------------------------------- | --- | ---------------------- | --- |
| Genre(including,e.g.,topics)                      |     | 28                     |     |
| Plot(including,e.g.,story)                        |     | 15                     |     |
| Theme(including,e.g.,setting,timeperiodofmovie)   |     | 9                      |     |
| Targetgroup(including,e.g.,age)                   |     | 6                      |     |
| People(including,e.g.,actors,characters)          |     | 6                      |     |
| Style(including,e.g.,animation,visualeffects)     |     | 6                      |     |
| Production(including,e.g.,director,budget,awards) |     | 6                      |     |
| Mood(including,e.g.,pacing,emotionalimpact)       |     | 4                      |     |
thediversityofagivenlistandthesimilarityoftheextremepairinthislist.First,they
were asked to state, in free text, according to which criteria they have assessed the
diversityofthegivenlists.Second,theywereaskedtorankupto7(moviedomain)
or8(recipedomain)pre-definedrankingcriteria.
In a first step, we performed a qualitative analysis of the free-text responses. We
appliedabottom-upcodingapproach(Saldana2015),wherewefirstidentifiedalarger
setofcodes/tagsintheparticipants’responsesandwherewethenmergedrelatedtags.
Overall,498wordsweretaggedinthefree-textresponsesinthemoviestudies.The
mostfrequentaggregatedcodesforthemoviedomainareshowninTable11.20
Thegenreofthemoviewasthebyfarmostfrequentlymentioneddecisioncriterion
bytheparticipants,anditwasmentionedalmosttwiceasoftenasthesecond-ranked
aspect, the plot. Interestingly, aspects related to movie poster, the title, music, and
soundeffectsorproductionyearwereonlyveryrarelymentioned.
The pre-defined list of criteria which participants had to rank after their free-
text responses included a number of meta-data elements that are commonly found
inresearchdatasetsinthemoviedomain.Toaggregatetheobtainedincompleterank-
ings,weusedtheBordacountrankaggregationmethodBlack(1958).Inthismethod,
anitematthefirstplaceofalistofnelementsreceivesn−1points,thesecondplace
givesn−2points,etc.TheobtainedrankingisshowninTable12.
Weobservethatthetoptwopositions(genre,plot)areidenticaltothoseextracted
fromthefree-textresponsesbytheparticipants.Severalofthesubsequentcodesfrom
20
TheaggregatedcodesfortherecipedomaincanbefoundintheAppendix.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 791
Table12 Bordacount
Criterion Bordacount
pre-definedcriteriaforassessing
moviesimilarities
Genre 3800
Plot 3437
Actors 3261
Title 3033
Image 2920
ReleaseYear 2871
Runtime 2652
thefree-textinput(e.g.,theme,targetgroup,mood)werenotpartofourpre-defined
list,whichisbasedoncommonmeta-datafrommovieratingdatasets.Thissuggests
that it might be helpful to include alternative information sources when computing
similarities in this domain. In particular, user provided content in the form of tags
appearedtobepromisinginthepast(Vigetal.2009;TrattnerandJannach2019).
Interestingly,whilethegenrewasconsideredasthemaincriteriontoassessitem
similarityinthemoviedomain,buildingtheILSmetricongenreinformationalone
may be too limited, as indicated by the findings from Study-2 movies . In our genre-
basedapproach,weusedtheJaccardindexasadistancemeasure.Whilewecannot
ruleoutotherwaysofcomputingsimilaritiesbasedongenres,thestudybyTrattner
andJannach(2019)suggestedthatusinganLDA-basedcomparisonmaynotbemore
effectiveeither.
TheBordacountrankingofthepre-definedcriteriaintherecipedomainisshown
in Table 13.21 The most important criterion, according to the participants, is the
ingredients, which are also one of the two pieces of information that we used in
ourapplication-specificsimilaritymeasureintherecipedomain.Thisisalsoinline
withtheobservationsinTrattnerandJannach(2019)whereingredients(aswellasthe
imageofthedish)werehighlyranked.NotehoweverthatTrattnerandJannach(2019)
foundthatcookingdirectionswerealsoveryhighlycorrelatedwithhumansimilarity
perceptionsandthatimages—althoughtheywereself-reportedbyparticipantstobe
very decisive—did not correlate to a similar extent with the perceptions in reality.
Therefore,wereliedbothoningredientsanddirectionswhendesigningasimilarity
functioninourstudy,whichintheendturnedouttobeindicativeofthesimilarityas
perceivedbyusers.
Overall,wearguethatitisimportanttofirstinvestigate,foreachapplicationdomain,
whattheparticularfactorsarethatdeterminethediversityperceptionofusers.Inthe
caseofrecipes,webuiltinpriorresearchbyTrattnerandJannach(2019)andcombined
those features that were found to be good predictors of perceived similarities in a
large-scaleuserstudy.Forthemoviedomain,incontrast,wereliedongenresasthe
onlyfeatureinthesimilarityfunction,asthisisacommonapproachintheliterature.
ConsideringtheimportancerankinginTable12,itseemsadvisabletocombinegenre
informationwithotherfeatures,inparticularwithplotsummaries.Aninvestigationof
21 Theabsolutevaluesarehigherintherecipedomaincomparedtothemoviedomainbecausetherewere
morepre-definedcriteria.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

| 792 |     | M.Jesseetal. |
| --- | --- | ------------ |
Table13 Bordacount
|     | Criterion | Bordacount |
| --- | --------- | ---------- |
pre-definedcriteriaforassessing
| recipesimilarities | Ingredients     | 7185 |
| ------------------ | --------------- | ---- |
|                    | Cuisine         | 6447 |
|                    | Image           | 6364 |
|                    | Nutrients       | 5778 |
|                    | Instructions    | 5650 |
|                    | Cookingduration | 5520 |
|                    | Reviews         | 4937 |
whichcombinationoffeaturesismostpredictiveofthediversityperceptionbyusers
inthemoviedomainishoweverbeyondthescopeofourpresentwork,whichaimsto
validatetypicalsimilaritymeasuresfromtheliterature.
Lastly,wealsoinvestigatedtheeffectsofdomainknowledgeonthediversityper-
ceptionofalist.BasedonpriorresearchconductedbyPorcaroetal.(2022),wemight
assumethatparticipantswithdifferinglevelsofbackgroundknowledgemayperceive
alistofitemsdifferently.Ontheonehand,userswithmorebackgroundknowledge
mightfindmoreaspectsinwhichitemsaredifferent.Ontheotherhand,ifusersknow
nothingabout,forexample,amovie,theymightthinkallmoviesofthatsamegenre
aresimilaratahigherlevel.
To study if such effects exist, we analyzed if there is a correlation between the
expressed diversity perception of participants and their level of familiarity with the
itemsinalist.Technically,todeterminethefamiliaritylevelofalist,wecountedfor
howmanyitemsinthelisttheparticipantexpressedatleastsomeleveloffamiliarity,
i.e.,whentheitemwasnotentirelyunknown.Interestingly,theanalysisindicatedno
correlationbetweenthediversityperceptionofalistandtheparticipants’familiarity
<.10).
withtheitems(r
5 Conclusionsandfuturework
Overall,ourresearchindicatesthattheILSmeasurecanindeedbeagoodproxyfor
humandiversityperceptions.Thedetailsofhowthemetricisactuallyimplementedcan
howevermatter,andaspecificmetricthereforehastobevalidatedinagivendomain
andapplication,e.g.,beforealgorithmicdiversificationtechniquesareapplied.With
these results, our work narrows an important research gap in the literature, where
researchersoftenimplicitlyassume,withoutvalidation,thattheirusedILSmetric—
whichislikelydesignedbasedonlyonintuition—wouldbeareliableproxyforhuman
diversityperceptions.
Onelimitationofourresearch,sofar,isthatwecannotprovidegeneralguidelines
regardinghowtodesignasimilaritymetricforagivendomain.Ourfindingsseemto
suggestthatinthecaseofmeta-data-basedapproaches,itmaybehelpfultorelyon
morethanoneitemfeature(e.g.,genreandplotoringredientsandcookingdirections).
As our studies were limited to two domains and on two particular ways of creating
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 793
similarityfunctionsbasedonmeta-data,thisindicationisnottoostrongyetandneeds
moreresearchinthefuture.
Apotentialthreattothevalidityofourstudiesmaybeseenintherepresentativesand
thereliabilityoftheparticipants.Inparticular,inthemoviedomain,manyparticipants
declared themselves to be almost movie enthusiasts. It therefore remains open to
investigationinthefutureifthefindingsobtainedinourpresentstudywouldgeneralize
toaparticipantpopulationthatislessengagedintheapplicationdomain.Regarding
thereliabilityoftheparticipants,weimplementedanumberofmeasurestoensurethat
wecantrustthattheresponsesarereliable,e.g.,byonlyadmittingcrowdworkerswith
goodpastperformanceandbyimplementingattentionchecksintheonlinestudies.
In terms of future works, it may be interesting to further investigate the effects
ofgenderonthediversityperceptionofrecommendationlistsinmoredepth.While
ourworkprovidednoevidencefordifferencesinhowdifferentgendersperceivethe
recommendation lists, other works suggest that there, in fact, may be a difference
(Knijnenburgetal.2011).Furthermore,itisimportanttoexpandourresearchtoother
frequentlyusedcomputationalmetrics,whichhavenotbeenvalidatedtoasufficient
extent yet. First of all, this includes common “beyond-accuracy” quality metrics, in
particularnoveltyorserendipity.Forinstance,likefordiversity,anumberofresearch
worksintroducenoveltymetrics.Often,suchnoveltymetricsarebasedonitempopu-
larity(VargasandCastells2011).However,formostofthesemetrics,itremainstobe
shownthattheyaresuitableproxiesforuserperceptions.Differentfromdiversity—as
investigated in our present work—the assessment of the novelty of a set of recom-
mended items has to be done relative to what a particular user already knows. This
addsadditionalcomplexitytothedesignofcorrespondinguserstudies.
In the last few years, also questions of fairness have gained increased research
interest in the area of recommender systems and in machine learning in general.
In that context, it was recently observed by Deldjoo et al. (2022) that the majority
of currently published research is based on non-validated assumptions and metrics.
Formanyoftheseworks,itthereforeremainsopenthatthedescribedcomputational
fairnessgoalscorrespondtowhatuserswouldconsiderfairorunfair.
Acknowledgements WethankMartijnC.Willemsenforhisfeedbackonthestatisticalanalyses.
Funding OpenaccessfundingprovidedbyUniversityofKlagenfurt.
OpenAccess ThisarticleislicensedunderaCreativeCommonsAttribution4.0InternationalLicense,which
permitsuse,sharing,adaptation,distributionandreproductioninanymediumorformat,aslongasyougive
appropriatecredittotheoriginalauthor(s)andthesource,providealinktotheCreativeCommonslicence,
andindicateifchangesweremade.Theimagesorotherthirdpartymaterialinthisarticleareincluded
inthearticle’sCreativeCommonslicence,unlessindicatedotherwiseinacreditlinetothematerial.If
materialisnotincludedinthearticle’sCreativeCommonslicenceandyourintendeduseisnotpermitted
bystatutoryregulationorexceedsthepermitteduse,youwillneedtoobtainpermissiondirectlyfromthe
copyrightholder.Toviewacopyofthislicence,visithttp://creativecommons.org/licenses/by/4.0/.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

794 M.Jesseetal.
Appendix:Additionalmaterial
Inthisappendix,weprovideadditionaldetailedmaterial,includingthequestionnaire
items for the recipe domain (Table 14), the participants’ assessments of the most
dissimilaritemsintherecipedomain(Table15),codingresultsfortherecipedomain
(Table16),theresultsofthestatisticalsignificancetests(pairwisecomparisons)forthe
moviestudyinPhase1(Tables17,18,19),theresultsonthegenderdifferencesinall
studies(Table20),thepopularitylevelsofitemsforbothdomains(Tables21,22),and
thedistributionofhumanresponsesforallstudies(Tables23,24,25,26).Furthermore,
we provide additional figures for the average responses of Study-1 (Table 5)
recipes
and Study-2 (Table6).
recipes
Table14 Questionnaireitemsforeachlistintherecipedomains
Question Focus Type
Q1(diversity) Therecipes Diversity 5-pointLikertscale
presentedinthis
listarediverse
Q2(variety) Therecipes Diversity 5-pointLikertscale
presentedinthis
listofferarich
variety
Q3(similarity) Therecipes Diversity 5-pointLikertscale
presentedinthis
listaresimilarto
eachother
Q4(choiceeasiness) Selectingarecipe ChoiceEasiness 5-pointLikertscale
waseasy
Q5(choiceconfidence) IamconfidentI ChoiceConfidence 5-pointLikertscale
willlikethe
recipeIselected
towatchnext
Q6(no.ofgoodoptions) Thelistcontained… No.ofgoodoptions Pre-definedanswers
TheoptionsforQ6were“morethanonegoodoption,”“exactlyonegoodoption,”“nooptionthatIliked”
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 795
Fig.5 AverageresponsesinStudy-1recipes(recipes,9lists)
Table15 Assessmentofmostdissimilarrecipesandtheentirelist(i.e.,recmid-ILS)
Pairassessment Containinglist
| Recipe1 | Recipe2 | Sim.(SD) Sim.(SD) |
| ------- | ------- | ----------------- |
2.00(1.46) 2.53(1.21)
AwardWinningSoftChocolateChipCookies OrzowithParmesanandBasil
BananaCrumbMuffins BroiledTilapiaParmesan 1.77(1.45) 2.53(1.21)
2.31(1.23) 2.53(1.21)
| DeliciousHamandPotatoSoup | BroiledTilapiaParmesan |     |
| ------------------------- | ---------------------- | --- |
FluffyPancakes CranberryPistachioBiscotti 2.26(1.16) 2.53(1.21)
Table16 Mostfrequentcodesinfree-textresponsesregardingthecriteriathatdeterminerecipesimilarities
| Code                                               |     | Percentageofappearance |
| -------------------------------------------------- | --- | ---------------------- |
| Ingredients(including,e.g.,mainingredient)         |     | 29                     |
| Category(including,e.g.,course,type)               |     | 27                     |
| Flavor(including,e.g.,taste,spiciness)             |     | 11                     |
| Cookingprocess(including,e.g.,directions,duration) |     | 10                     |
| Cuisine(including,e.g.,origin)                     |     | 9                      |
| Familiarity(including,e.g.,knowledge)              |     | 5                      |
| Nutrition(including,e.g.,proteins,healthiness)     |     | 4                      |
Firstimpression(including,e.g.,image,title)
4
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

| 796 |     |     |     |     | M.Jesseetal. |
| --- | --- | --- | --- | --- | ------------ |
Table17 PairwiseWilcoxontestwithBonferronicorrectionforStudy-1movies(movies,9lists);numbers
showthepvalueforeachpairwisecomparisonondiversity
List upp reclow-ILS recmid-ILS rechigh-ILS popsim recmin recmax popsimmin
<.001
reclow-ILS
| recmid-ILS | <.001 1    |       |     |     |     |
| ---------- | ---------- | ----- | --- | --- | --- |
|            | <.01 <.001 | <.001 |     |     |     |
rechigh-ILS
| popsim    | <.001 .826 | 1   | <.01  |     |       |
| --------- | ---------- | --- | ----- | --- | ----- |
|           | <.001 .88  |     | .001  |     |       |
| recmin    |            | 1   |       | 1   |       |
| recmax    | <.001 1    | 1   | <.001 | 1 1 |       |
|           | <.001 .02  | .31 | .046  |     | .21   |
| popsimmin |            |     |       | 1 1 |       |
| popsimmax | <.001 .048 | .54 | .04   | 1 1 | .40 1 |
Significantresults(p<.05)areprintedinboldface
Table18 PairwiseWilcoxontestwithBonferronicorrectionforStudy-1movies(movies,9lists);numbers
showthepvalueforeachpairwisecomparisononvariety
List upp reclow-ILS recmid-ILS rechigh-ILS popsim recmin recmax popsimmin
<.001
reclow-ILS
| recmid-ILS | <.001 1 |     |     |     |     |
| ---------- | ------- | --- | --- | --- | --- |
.149 <.001 .002
rechigh-ILS
| popsim    | <.001 .43  | 1   | .14   |     |     |
| --------- | ---------- | --- | ----- | --- | --- |
|           | <.001 .44  |     | .003  |     |     |
| recmin    |            | 1   |       | 1   |     |
| recmax    | <.001 1    | 1   | <.001 | 1 1 |     |
|           | <.001 .008 |     | .33   |     |     |
| popsimmin |            | 1   |       | 1 1 | 1   |
| popsimmax | <.001 .033 | 1   | .12   | 1 1 | 1 1 |
Significantresults(p<.05)areprintedinboldface
Table19 PairwiseWilcoxontestwithBonferronicorrectionforStudy-1movies(movies,9lists);numbers
showthepvalueforeachpairwisecomparisononsimilarity
List upp reclow-ILS recmid-ILS rechigh-ILS popsim recmin recmax popsimmin
<.001
reclow-ILS
| recmid-ILS | <.001 .23   |       |     |     |     |
| ---------- | ----------- | ----- | --- | --- | --- |
|            | <.001 <.001 | <.001 |     |     |     |
rechigh-ILS
| popsim    | <.001 .003 | 1   | .44   |     |     |
| --------- | ---------- | --- | ----- | --- | --- |
|           | <.001 .03  |     | .01   |     |     |
| recmin    |            | 1   |       | 1   |     |
| recmax    | <.001 1    | 1   | <.001 | 1 1 |     |
|           | <.001 .004 |     | .02   |     |     |
| popsimmin |            | 1   |       | 1 1 | 1   |
| popsimmax | <.001 .02  | 1   | <.001 | 1 1 | 1 1 |
Significantresults(p<.05)areprintedinboldface
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 797
Table20 PairwiseWilcoxontestwithBonferronicorrectionforallstudieswithα =.05;numbersshow
thepvalueforeachpairwisecomparisononthegender
Study Diversity Variety Similarity Choiceeasiness Choiceconfidence
.08 .22 .07 .90 .73
Study-1movies
| Study-1recipes | .86 .12 | .56 | .08 | .21 |
| -------------- | ------- | --- | --- | --- |
.34 .29 .46 .10 .29
Study-2movies
| Study-2recipes | .24 .43 | .87 | .53 | .11 |
| -------------- | ------- | --- | --- | --- |
Table21 AveragenumberofratingsforthelistsinStudy-1movies andthecorrespondingdiversityper-
ception
| List | Averagenumberofratingsforlist |     |     | Diversityperception |
| ---- | ----------------------------- | --- | --- | ------------------- |
| upp  | 15978                         |     |     | 2.37                |
3.82
| popsim     | 45174 |     |     |      |
| ---------- | ----- | --- | --- | ---- |
| reclow-ILS | 26939 |     |     | 4.05 |
3.92
| recmid-ILS  | 29984 |     |     |      |
| ----------- | ----- | --- | --- | ---- |
| rechigh-ILS | 46622 |     |     | 3.17 |
Weusedthemeanofpopsim, popsimmax,and popsimmin forthefinaldiversityperceptionrating.The
samewasdoneforrecmid-ILS
Table22 AveragenumberofratingsforthelistsinStudy-1recipes andthecorrespondingdiversityper-
ception
| List        | Averagenumberofratingsforlist |     |     | Diversityperception |
| ----------- | ----------------------------- | --- | --- | ------------------- |
| upp         | 106                           |     |     | 2.37                |
| popsim      | 58                            |     |     | 3.82                |
| reclow-ILS  | 5183                          |     |     | 4.31                |
| recmid-ILS  | 6769                          |     |     | 4.12                |
| rechigh-ILS | 5385                          |     |     | 4.22                |
Weusedthemeanofpopsim, popsimmax,and popsimmin forthefinaldiversityperceptionrating.The
samewasdoneforrecmid-ILS
Fig.6 AverageresponsesinStudy-2recipes(recipes,3lists)
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

798 M.Jesseetal.
Table23 DistributionofhumanresponsesforeachlistinStudy-1movies
| List        | Male | Female | Other(non-binary/undisclosed) |
| ----------- | ---- | ------ | ----------------------------- |
| upp         | 39   | 36     | 0                             |
| reclow-ILS  | 43   | 29     | 0                             |
| recmid-ILS  | 47   | 27     | 0                             |
| rechigh-ILS | 50   | 26     | 0                             |
| popsim      | 44   | 27     | 0                             |
| recmin      | 38   | 30     | 0                             |
| recmax      | 47   | 34     | 0                             |
| popsimmin   | 39   | 37     | 0                             |
| popsimmax   | 49   | 27     | 0                             |
Eachparticipantreceivedthreedifferentlists,hencethedifferentnumberofresponsesperlist;theresponses
aresplitbygender
Table24 DistributionofhumanresponsesforeachlistinStudy-1recipes
| List        | Male | Female | Other(non-binary/undisclosed) |
| ----------- | ---- | ------ | ----------------------------- |
| upp         | 33   | 24     | 2                             |
| reclow-ILS  | 38   | 30     | 0                             |
| recmid-ILS  | 32   | 28     | 0                             |
| rechigh-ILS | 44   | 24     | 0                             |
| popsim      | 40   | 24     | 1                             |
| recmin      | 39   | 22     | 1                             |
| recmax      | 44   | 28     | 1                             |
| popsimmin   | 39   | 32     | 0                             |
| popsimmax   | 36   | 22     | 1                             |
Eachparticipantreceivedthreedifferentlists,hencethedifferentnumberofresponsesperlist;theresponses
aresplitbygender
Table25 DistributionofhumanresponsesforeachlistinStudy-2movies
| List        | Male | Female | Other(non-binary/undisclosed) |
| ----------- | ---- | ------ | ----------------------------- |
| reclow-ILS  | 33   | 21     | 1                             |
| recmid-ILS  | 33   | 21     | 1                             |
| rechigh-ILS | 33   | 21     | 1                             |
Each participant received three different lists, hence all lists have the same amount of responses; the
responsesaresplitbygender
Table26 DistributionofhumanresponsesforeachlistinStudy-2recipes
| List        | Male | Female | Other(non-binary/undisclosed) |
| ----------- | ---- | ------ | ----------------------------- |
| reclow-ILS  | 38   | 20     | 0                             |
| recmid-ILS  | 38   | 20     | 0                             |
| rechigh-ILS | 38   | 20     | 0                             |
Each participant received three different lists, hence all lists have the same amount of responses; the
responsesaresplitbygender
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 799
References
Abdollahpouri, H., Burke, R., Mobasher, B.: Managing popularity bias in recommender systems with
personalizedre-ranking,pp.1–6.ArXiv,arXiv:1901.07555(2019)
Adomavicius,G.,Kwon,Y.:Improvingaggregaterecommendationdiversityusingranking-basedtech-
niques.IEEETrans.Knowl.DataEng.24(5),896–911(2012).https://doi.org/10.1109/TKDE.2011.
15
Black,D.:TheTheoryofCommitteesandElections.Springer,NewYork(1958)
Bradley,K.,Smyth,B.:Improvingrecommendationdiversity.In:TwelfthIrishConferenceonArtificial
IntelligenceandCognitiveScience,pp.85–94(2001)
Brovman,Y.M.,Jacob,M.,Srinivasan,N.,Neola,S.,Galron,D.,Snyder,R.,Wang,P.:Optimizingsimilar
itemrecommendationsinasemi-structuredmarketplacetomaximizeconversion.In:Proceedingsof
the10thACMConferenceonRecommenderSystems,pp.199–202(2016).https://doi.org/10.1145/
2959100.2959166
Chen,L.,Wu,W.,He,L.:Howpersonalityinfluencesusers’needsforrecommendationdiversity?In:CHI
’13ExtendedAbstractsonHumanFactorsinComputingSystems,pp.829–834(2013).https://doi.
org/10.1145/2468356.2468505
Clarke,C.L.,Kolla,M.,Cormack,G.V.,Vechtomova,O.,Ashkan,A.,Büttcher,S.,MacKinnon,I.:Novelty
anddiversityininformationretrievalevaluation.In:Proceedingsofthe31stAnnualInternational
ACMSIGIRConferenceonResearchandDevelopmentinInformationRetrieval,pp.659–666(2008).
https://doi.org/10.1145/1390334.1390446
Colucci,L.,Doshi,P.,Lee,K.L.,Liang,J.,Lin,Y.,Vashishtha,I.,Zhang,J.,Jude,A.:Evaluatingitem-item
similarityalgorithmsformovies.In:Proceedingsofthe2016CHIConferenceExtendedAbstracts
onHumanFactorsinComputingSystems,pp.2141–2147(2016).https://doi.org/10.1145/2851581.
2892362
deGemmis,M.,Lops,P.,Musto,C.,Narducci,F.,Semeraro,G.:Semantics-awarecontent-basedrecom-
mendersystems.In:RecommenderSystemsHandbook,pp.119–159(2015).https://doi.org/10.1007/
978-1-4899-7637-6_4
Deldjoo,Y.,Jannach,D.,Bellogin,A.,Difonzo,A.,Zanzonelli,D.:Asurveyofresearchonfairrecommender
systems(2022).https://doi.org/10.48550/ARXIV.2205.11127
Downie,J.S.,Lee,J.H.,Gruzd,A.A.,Jones,M.C.:Towardanunderstandingofsimilarityjudgmentsfor
musicdigitallibraryevaluation.In:Proceedingsofthe7thACM/IEEE-CSJointConferenceonDigital
Libraries,pp.307–308(2007).https://doi.org/10.1145/1255175.1255235
Du,Y.,Ranwez,S.,Sutton-Charani,N.,Ranwez,V.:Isdiversityoptimizationalwayssuitable?Toward
abetterunderstandingofdiversitywithinrecommendationapproaches.Inf.Process.Manag.58(6),
102721(2021).https://doi.org/10.1016/j.ipm.2021.102721
Ekstrand, M.D., Harper, F.M., Willemsen, M.C., Konstan, J.A.: User perception of differences in rec-
ommenderalgorithms.In:Proceedingsofthe8thACMConferenceonRecommenderSystems,pp.
161–168(2014).https://doi.org/10.1145/2645710.2645737
Ellis,D.P.,Whitman,B.,Berenzweig,A.,Lawrence,S.:Thequestforgroundtruthinmusicalartistsim-
ilarity.In:Proceedingsofthe3rdInternationalConferenceonMusicInformationRetrieval(2002).
https://ismir2002.ismir.net/proceedings/02-FP05-4.pdf
Fleder,D.M.,Hosanagar,K.:Recommendersystemsandtheirimpactonsalesdiversity.In:Proceedings
ofthe8thACMConferenceonElectronicCommerce,pp.192–199(2007).https://doi.org/10.1145/
1250910.1250939
Ge,M.,Gedikli,F.,Jannach,D.:Placinghigh-diversityitemsintop-nrecommendationlists.In:Proceedings
oftheWorkshoponIntelligentTechniquesforWebPersonalizationandRecommenderSystems(ITWP
2011atIJCAI2011)(2011)
Ge,M.,Jannach,D.,Gedikli,F.,Hepp,M.:Effectsoftheplacementofdiverseitemsinrecommendationlists.
In:14thInternationalConferenceonEnterpriseInformationSystems,pp.201–208(2012).https://doi.
org/10.5220/0003974802010208
Hauptmann,H.,Leipold,N.,Madenach,M.,Wintergerst,M.,Lurz,M.,Groh,G.,Böhm,M.,Gedrich,
K.,Krcmar,H.:Effectsandchallengesofusinganutritionassistancesystem:resultsofalong-term
mixed-methodstudy.In:UserModelingandUser-AdaptedInteraction(2021).https://doi.org/10.1007/
s11257-021-09301-y
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

800 M.Jesseetal.
Jannach, D., Kamehkhosh, I., Lerche, L.: Leveraging multi-dimensional user models for personalized
next-trackmusicrecommendation.In:ProceedingsoftheSymposiumonAppliedComputing,pp.
1635–1642(2017).https://doi.org/10.1145/3019612.3019756
Jannach, D.: Multi-objective recommendation: Overview and challenges. In: Proceedings of the 2nd
Workshop on Multi-Objective Recommender Systems co-located with 16th ACM Conference on
RecommenderSystems(RecSys2022).arXiv:2210.10309(2022)
Jannach,D.,Lerche,L.,Kamehkhosh,I.,Jugovac,M.:Whatrecommendersrecommend:ananalysisof
recommendationbiasesandpossiblecountermeasures.UserModel.UserAdapt.Interact.25(5),427–
491(2015).https://doi.org/10.1007/s11257-015-9165-3
Jensen,O.,Lisman,J.E.:Novellistsof7+/-2knownitemscanbereliablystoredinanoscillatoryshort-term
memorynetwork:interactionwithlong-termmemory.Learn.Mem.3(2–3),257–263(1996).https://
doi.org/10.1101/lm.3.2-3.257
Kaminskas,M.,Bridge,D.:Diversity,serendipity,novelty,andcoverage:asurveyandempiricalanalysisof
beyond-accuracyobjectivesinrecommendersystems.ACMTransInteractIntellSyst(2016).https://
doi.org/10.1145/2926720
Knijnenburg,B.P.,Willemsen,M.C.,Kobsa,A.:Apragmaticproceduretosupporttheuser-centriceval-
uationofrecommendersystems.In:ProceedingsoftheFifthACMConferenceonRecommender
Systems,pp.321–324(2011).https://doi.org/10.1145/2043932.2043993
Kunaver,M.,Požrl,T.:Diversityinrecommendersystems—asurvey.Knowl.BasedSyst.123,154–162
(2017).https://doi.org/10.1016/j.knosys.2017.02.009
Lee,J.H.:Crowdsourcingmusicsimilarityjudgmentsusingmechanicalturk.In:Proceedingsofthe11th
InternationalSocietyforMusicInformationRetrievalConference,pp.183–188(2010)
Lin,K.,Sonboli,N.,Mobasher,B.,Burke,R.:Calibrationincollaborativefilteringrecommendersystems:a
user-centeredanalysis.In:Proceedingsofthe31stACMConferenceonHypertextandSocialMedia,
pp.197–206,(2020)https://doi.org/10.1145/3372923.3404793
Mauro,N.,Ardissono,L.:Extendingatag-basedcollaborativerecommenderwithco-occurringinformation
interests.In:Proceedingsofthe27thACMConferenceonUserModeling,AdaptationandPersonal-
ization,pp.181–190(2019).https://doi.org/10.1145/3320435.3320458
McGinty,L.,Smyth,B.:Ontheroleofdiversityinconversationalrecommendersystems.In:Case-Based
ReasoningResearchandDevelopment,pp.276–290(2003).https://doi.org/10.1007/3-540-45006-
8_23
McNee,S.M.,Riedl,J.,Konstan,J.A.:Beingaccurateisnotenough:Howaccuracymetricshavehurt
recommendersystems.In:CHI’06ExtendedAbstractsonHumanFactorsinComputingSystems,
pp.1097–1101(2006).https://doi.org/10.1145/1125451.1125659
Miller,G.A.:Themagicalnumberseven:plusorminustwo:Somelimitsonourcapacityforprocessing
information.Psychol.Rev.63(2),81–97(1956).https://doi.org/10.1037/h0043158
Nilashi,M.,Jannach,D.,BinIbrahim,O.,Esfahani,M.D.,Ahmadi,H.:Recommendationquality,trans-
parency,andwebsitequalityfortrust-buildinginrecommendationagents.Electron.Commer.Res.
Appl.19,70–84(2016).https://doi.org/10.1016/j.elerap.2016.09.003
Porcaro,L.,Gómez,E.,Castillo,C.:Perceptionsofdiversityinelectronicmusic:Theimpactoflistener,
artist,andtrackcharacteristics.Proc.ACMHum.Comput.Interact.(2022)https://doi.org/10.1145/
3512956
Pu,P.,Chen,L.,Hu,R.:Auser-centricevaluationframeworkforrecommendersystems.In:Proceedingsof
theFifthACMConferenceonRecommenderSystems,pp.157–164(2011).https://doi.org/10.1145/
2043932.2043962
Rendle,S.,Krichene,W.,Zhang,L.,Anderson,J.:Neuralcollaborativefilteringvs.matrixfactorization
revisited.In:Proceedingsofthe14thACMConferenceonRecommenderSystems,RecSys’20,pp.
240–248(2020).https://doi.org/10.1145/3383313.3412488
Ribeiro,M.T.,Ziviani,N.,Moura,E.S.D.,Hata,I.,Lacerda,A.,Veloso,A.:Multiobjectivepareto-efficient
approachesforrecommendersystems.ACMTrans.Intell.Syst.Technol.(2015)https://doi.org/10.
1145/2629350
Saldana,J.:TheCodingManualforQualitativeResearchers,3rdedn.SagePublications,London(2015)
Shi,Y.,Zhao,X.,Wang,J.,Larson,M.,Hanjalic,A.:Adaptivediversificationofrecommendationresultsvia
latentfactorportfolio.In:Proceedingsofthe35thInternationalACMSIGIRConferenceonResearch
and Development in Information Retrieval, pp. 175–184 (2012). https://doi.org/10.1145/2348283.
2348310
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Intra-listsimilarityandhumandiversityperceptions... 801
Starke, A.D., Øverhaug, S., Trattner, C.: Predicting feature-based similarity in the news domain using
humanjudgments.In:Proceedingsofthe9thInternationalWorkshoponNewsRecommendationand
Analytics(2021)
Trattner,C.,Jannach,D.:Learningtorecommendsimilaritemsfromhumanjudgements.UserModel.User
Adapt.Interact.30,1–49(2019).https://doi.org/10.1007/s11257-019-09245-4
Tsai,C.H.,Brusilovsky,P.:Beyondtherankedlist:User-drivenexplorationanddiversificationofsocial
recommendation.In:23rdInternationalConferenceonIntelligentUserInterfaces,pp.239–250(2018).
https://doi.org/10.1145/3172944.3172959
vanPinxteren,Y.,Geleijnse,G.,Kamsteeg,P.:Derivingarecipesimilaritymeasureforrecommending
healthfulmeals.In:Proceedingsofthe16thInternationalConferenceonIntelligentUserInterfaces,
pp.105–114(2011).https://doi.org/10.1145/1943403.1943422
Vargas,S.,Baltrunas,L.,Karatzoglou,A.,Castells,P.:Coverage,redundancyandsize-awarenessingenre
diversityforrecommendersystems.In:Proceedingsofthe8thACMConferenceonRecommender
Systems,pp.209–216(2014).https://doi.org/10.1145/2645710.2645743
Vargas, S., Castells, P., Vallet, D.: Explicit relevance models in intent-oriented information retrieval
diversification.In:Proceedingsofthe35thInternationalACMSIGIRConferenceonResearchand
DevelopmentinInformationRetrieval,pp.75–84(2012).https://doi.org/10.1145/2348283.2348297
Vargas,S.,Castells,P.:Rankandrelevanceinnoveltyanddiversitymetricsforrecommendersystems.In:
ProceedingsoftheFifthACMConferenceonRecommenderSystems,pp.109–116(2011).https://
doi.org/10.1145/2043932.2043955
Vargas,S.:Newapproachestodiversityandnoveltyinrecommendersystems.In:FourthBCS-IRSGSympo-
siumonFutureDirectionsinInformationAccess,pp.8–13(2011).https://doi.org/10.5555/2227322.
2227324
Vig,J.,Sen,S.,Riedl,J.:Tagsplanations:Explainingrecommendationsusingtags.In:Proceedingsofthe
14thInternationalConferenceonIntelligentUserInterfaces,pp.47–56(2009).https://doi.org/10.
1145/1502650.1502661
Wang,C.,Agrawal,A.,Li,X.,Makkad,T.,Veljee,E.,Mengshoel,O.,Jude,A.:Content-basedtop-nrecom-
mendationswithperceivedsimilarity.In:Proceedingsofthe2017IEEEInternationalConferenceon
Systems,Man,andCybernetics,pp.1052–1057(2017).https://doi.org/10.1109/SMC.2017.8122750
Willemsen,M.C.,Graus,M.P.,Knijnenburg,B.P.:Understandingtheroleoflatentfeaturediversification
onchoicedifficultyandsatisfaction.UserModel.UserAdapt.Interact.26(4),347–389(2016).https://
doi.org/10.1007/s11257-016-9178-6
Yao,Y.,Harper,F.M.:Judgingsimilarity:auser-centricstudyofrelateditemrecommendations.In:Pro-
ceedingsofthe12thACMConferenceonRecommenderSystems,pp.288–296(2018).https://doi.
org/10.1145/3240323.3240351
Zeng,Z.,Lin,J.,Li,L.,Pan,W.,Ming,Z.:Next-itemrecommendationviacollaborativefilteringwith
bidirectionalitemsimilarity.ACMTrans.Inf.Syst.(2019).https://doi.org/10.1145/3366172
Zheng,Y.,Wang,D.X.:Asurveyofrecommendersystemswithmulti-objectiveoptimization.Neurocom-
puting474,141–153(2022).https://doi.org/10.1016/j.neucom.2021.11.041
Ziegler,C.N.,McNee,S.M.,Konstan.J.A.,Lausen,G.:Improvingrecommendationliststhroughtopic
diversification.In:Proceedingsofthe14thInternationalConferenceonWorldWideWeb,pp.22–32
(2005).https://doi.org/10.1145/1060745.1060754
Publisher’sNote SpringerNatureremainsneutralwithregardtojurisdictionalclaimsinpublishedmaps
andinstitutionalaffiliations.
MathiasJesseisadoctoralcandidateinComputerScienceintheDigitalAgeResearchCenter(D!ARC)
atUniversityofKlagenfurt,Austria.HereceivedhisMScdegreefromthesameuniversityinInformation
Management.Hisresearchisfocusedonpersuasiverecommendersystems.
ChristineBauerisanAssistantProfessoratUtrechtUniversity,TheNetherlands.Herresearchactivities
centeroninteractiveintelligentsystems.Centralthemesinherresearcharecontextandcontext–adaptivity.
Coreinterestsinhercurrentresearchactivitiesarefairnessandmulti-methodevaluations.Shehasco-
authoredmorethan100publications,threeofthemawardedasbestresearchpaperandonereceivedan
awardofexcellence.Sheholdsfiveawardsasbestoroutstandingreviewer.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

802 M.Jesseetal.
DietmarJannachisaProfessorofComputerScienceatUniversityofKlagenfurt,Austria.Hehasworked
ondifferentareasofartificialintelligence,includingrecommendersystems,model-baseddiagnosis,and
knowledge-based systems. He is the leading author of a textbook on recommender systems and has
authoredmorethanhundredresearchpapers,focusingontheapplicationofartificialintelligencetech-
nologytopracticalproblems.
123
Content courtesy of Springer Nature, terms of use apply. Rights reserved.

Terms and Conditions
Springer Nature journal content, brought to you courtesy of Springer Nature Customer Service Center
G mbH (“Springer Nature”).
Springer Nature supports a reasonable amount of sharing of research papers by authors, subscribers
and authorised users (“Users”), for small-scale personal, non-commercial use provided that all
copyright, trade and service marks and other proprietary notices are maintained. By accessing,
sharing, receiving or otherwise using the Springer Nature journal content you agree to these terms of
use (“Terms”). For these purposes, Springer Nature considers academic use (by researchers and
s tudents) to be non-commercial.
These Terms are supplementary and will apply in addition to any applicable website terms and
conditions, a relevant site licence or a personal subscription. These Terms will prevail over any
conflict or ambiguity with regards to the relevant terms, a site licence or a personal subscription (to
the extent of the conflict or ambiguity only). For Creative Commons-licensed articles, the terms of
t he Creative Commons license used will apply.
We collect and use personal data to provide access to the Springer Nature journal content. We may
also use these personal data internally within ResearchGate and Springer Nature and as agreed share
it, in an anonymised way, for purposes of tracking, analysis and reporting. We will not otherwise
disclose your personal data outside the ResearchGate or the Springer Nature group of companies
u nless we have your permission as detailed in the Privacy Policy.
While Users may use the Springer Nature journal content for small scale, personal non-commercial
u se, it is important to note that Users may not:
1.use such content for the purpose of providing other users with access on a regular or large scale
basis or as a means to circumvent access control;
2.use such content where to do so would be considered a criminal or statutory offence in any
jurisdiction, or gives rise to civil liability, or is otherwise unlawful;
3.falsely or misleadingly imply or suggest endorsement, approval , sponsorship, or association
unless explicitly agreed to by Springer Nature in writing;
4.use bots or other automated methods to access the content or redirect messages
5.override any security feature or exclusionary protocol; or
6.share the content in order to create substitute for Springer Nature products or services or a
systematic database of Springer Nature journal content.
In line with the restriction against commercial use, Springer Nature does not permit the creation of a
product or service that creates revenue, royalties, rent or income from our content or its inclusion as
part of a paid for service or for other commercial gain. Springer Nature journal content cannot be
used for inter-library loans and librarians may not upload Springer Nature journal content on a large
s cale into their, or any other, institutional repository.
These terms of use are reviewed regularly and may be amended at any time. Springer Nature is not
obligated to publish any information or content on this website and may remove it or features or
functionality at our sole discretion, at any time with or without notice. Springer Nature may revoke
this licence to you at any time and remove access to any copies of the Springer Nature journal content
w hich have been saved.
To the fullest extent permitted by law, Springer Nature makes no warranties, representations or
guarantees to Users, either express or implied with respect to the Springer nature journal content and
all parties disclaim and waive any implied warranties or warranties imposed by law, including
m erchantability or fitness for any particular purpose.
Please note that these rights do not automatically extend to content, data or other material published
b y Springer Nature that may be licensed from third parties.
If you would like to use or distribute our Springer Nature journal content to a wider audience or on a
regular basis or in any other manner not expressly permitted by these Terms, please contact Springer
N ature at
onlineservice@springernature.com