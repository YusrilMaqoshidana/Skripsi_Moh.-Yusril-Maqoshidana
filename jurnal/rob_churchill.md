The Evolution of Topic Modeling
ROBCHURCHILLandLISASINGH,GeorgetownUniversity
Topicmodelshavebeenappliedtoeverythingfrombookstonewspaperstosocialmediapostsinaneffortto
identifythemostprevalentthemesofatextcorpus.Weprovideanin-depthanalysisofunsupervisedtopic
modelsfromtheirinceptiontotoday.Wetracetheoriginsofdifferenttypesofcontemporarytopicmodels,
beginninginthe1990s,andwecomparetheirproposedalgorithms,aswellastheirdifferentevaluationap-
proaches.Throughout,wealsodescribesettingsinwhichtopicmodelshaveworkedwellandareaswhere
newresearchisneeded,settingthestageforthenextgenerationoftopicmodels.
CCSConcepts:•Generalandreference→Surveysandoverviews;•Computingmethodologies→
Modelingmethodologies;Machinelearningalgorithms;
Additional Key Words and Phrases: Topic modeling, social media, online topic modeling, temporal topic
modeling
ACMReferenceformat:
RobChurchillandLisaSingh.2022.TheEvolutionofTopicModeling.ACMComput.Surv.54,10s,Article215
(November2022),35pages.
https://doi.org/10.1145/3507900
1 INTRODUCTION
Understanding the core themes associated with a document collection is a fundamental task in
today’s information era. Topic models are a class of unsupervised machine learning techniques
designedforthistask.Theycancompressacorpusofthousandsofdocumentsintoashortsum-
marythatcapturesthemostprevalentsubjectspresentinthecorpus.Theshortsummarytakes
theformoftopics,orsetsofrelatedwords,henceatopicmodel.Wedefineatopicmodeltobean
unsupervisedmathematicalmodelthattakesasinputasetofdocumentsD andreturnsasetof
topicsT thatrepresentthecontentofD inanaccurateandcoherentmanner.
Figure1showsanexampleofthekindofinput(left),theoutput(center),andtheusage(right)
one would expect when employing topic modeling. One inputs documents. The topic modeling
algorithmreturnsasetofthemes/topicspertainingtothosedocuments.Somealgorithmsalsore-
turnaweightordegreeofrelevanceforeachwordinthetopic.Thedocumentsinthecollection
canthenbelabeledwiththesetopics,allowinguserstounderstandtheimportanceofthetopicin
eachdocumentandinthecollectionasawhole.TheexampledocumentsinFigure1areallbooks
setinmagicalormedievalworlds,andassuch,thefourtopicsreturnedhavetodowithrelevant
ThisworkwassupportedbytheMassiveDataInstitute(MDI)atGeorgetownUniversity,andthroughgrantsprovidedby
theNationalScienceFoundation(#1934925and#1934494).
Authors’ address: R. Churchill and L. Singh, Georgetown University; emails: rjc111@georgetown.edu, lisa.singh@
georgetown.edu.
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalorclassroomuseisgrantedwithoutfee
providedthatcopiesarenotmadeordistributedforprofitorcommercialadvantageandthatcopiesbearthisnoticeand
thefullcitationonthefirstpage.CopyrightsforcomponentsofthisworkownedbyothersthanACMmustbehonored.
Abstractingwithcreditispermitted.Tocopyotherwise,orrepublish,topostonserversortoredistributetolists,requires
priorspecificpermissionand/orafee.Requestpermissionsfrompermissions@acm.org.
©2022AssociationforComputingMachinery.
0360-0300/2022/11-ART215$15.00
https://doi.org/10.1145/3507900
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.
215

215:2 R.ChurchillandL.Singh
Fig.1. AnExampleInputandOutputofaTopicModel.Topiclabelssuchas“magic”and“travel”arenot
normallyassignedbytopicmodelsbutareincludedhereforclarity.
magicalthemesdescribedinthesebooks.Atopicmodelidentifiesthemesbyidentifyingrepeated
patternsofwordsandgroupingthesepatternsofwordsintotopicsthatreflectthecontentofthe
documents.Itisnotunusualforsometopicstocontainthesamewords(like“fairy”intheexam-
ple).Intuitively,topicsthatarecoherent,areinterpretable,andhaveasmallnumberofoverlapping
wordsareconsideredhigherquality.TopicsdonotusuallycomewithlabelsastheydoinFigure1.
These topic labels were added to make it easier to understand the distribution of the identified
setsofwordsindocuments,i.e.,thedocument-topicdistributions.Thislackofaproperlabelcan
maketheirresultsverydifficultforhumanstointerpretiftopicsarenotcoherent—containingsets
ofwordsthatintuitivelyseemtobelongtogether.Originallydesignedtoclassifydocumentslike
books, research papers, and news articles, seminal topic models rely on the predictable and fre-
quentrepetitionofpatternsofwordsacrossthedocumentcollectioninordertoproduceaccurate
andcoherentmodels.Inotherwords,themorepredictablethepatterns,thebetterthequalityof
thetopicsgeneratedbydifferenttopicmodels.
Topicmodelshavebeenutilizedacrossmanydisciplinestounderstanddifferenttypesoftexts,
from tweets to books. Researchers have applied topic modeling to understand themes from his-
toricnewspapers[55,90].Sleemanetal.[71]incorporatedtopicsmodelsintheiranalysisofthe
evolutionofclimatechangeliterature.JockersandMimnousedtopicmodelingtoidentifythemes
in19th-centuryliterature[34].Ryanetal.[66]usedtopicmodelsinasemi-iterativeapproachto
discerning the most popular parenting topics on Twitter, while Bode et al. [11] employ a simi-
larapproachfor understandingthe2016USpresidentialelectionusing newspapers,tweets,and
open-endedsurveys.
Topicmodelscanalsobeincorporatedwithotherlearningmodelstoincreasepredictivepower
andinterpretability.Singhetal.[70]usetopicsasinputintohierarchicalBayesianmodelstohelp
predictforcedmigrationofdisplacedpersons.Topicmodelshavealsobeenadaptedtohelppre-
dicttheeffectsofgeneticvariants[3].Theyhavebeenusedtogeneratetagsforcontenttagging
systems [37], to organize online recommendation systems [1], and to explain latent factors that
lead to recommendations [65]. They have also been employed to improve sentiment analysis in
text[35,46].Topicmodelsareausefultoolininformationretrieval,aidinginqueryexpansionand
documentsmoothing[92,93].Whatshouldbeapparentfromtheseexamplesisthattopicmodels
arebeingusedbroadly,bothasafinalresultandasafeatureintootherpredictivemodels.
As the number of applications of topic modeling increases, it has become clear that not all
topicmodelingalgorithmsarewellsuitedforalltypesoftext.Ryanetal.’s[66]useofaniterative
manually aided topic modeling approach to get an acceptable set of topics on social media data
is indicative of the continued failure of topic models in that area. However, Sleeman et al. [71]
demonstratewithscientificarticlesjusthowpowerfultopicmodelscanbe.Thisleadsustostrive
forthatkindofpowerandaccuracyinlower-qualitytextlikesocialmediaposts.Traditionalbooks
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:3
andscientificarticleshavecertaintypesofdiscerniblepatternsofwords,whilesocialmediaposts
mayhaveverydifferentones.Inthisnewworld,socialmediapostsareanewtypeofdocumentand
topic models can be important for understanding the themes of this online conversation. These
new types of documents come with their own challenges. 1. Document length: Instead of well-
editedbooksandarticles,manytextdocumentsareshort,uneditedsocialmediapostscontaining
veryfewwords.InthecaseofTwitter,tweetsarerestrictedto280characters.2.Sparsity:Instead
oftextsconsistingofthousandsofcarefullyeditedwordsandphrases,socialmediapostscontain
afewdozenhastilytypedwordsthatarenotgrammatically consistent,oftenaccompaniedbya
hashtagandaURL.Socialmediadatahasavocabularythatiscontinuallyevolving.Newwords
andhashtagsarecreatedconstantly.Postscontainingmultiplelanguagesarenotuncommon,and
abbreviations are the norm. Reinforced word co-occurrence patterns within social media posts
simplydonotexistattheratethattheydoinlongertexts.Thislackofstrongwordco-occurrence
can result in noisy, incoherent topics when topic models not designed for sparse, short text are
used with social media data. 3. Volume: Instead of the thousands of books and research papers
being published every year, there are millions of social media posts generated every day. Many
of the original topic models were built on statistical models supported by intractable inference
problemsthatrequirerelaxationjusttobefeasibleforthousandsofdocuments.4.RateofChange:
Insteadofinformationbeingpublishedonayearly,quarterly,monthly,orevenweeklybasis,social
mediafacilitatesthepublishingofinformationinrealtime.Thismeansthatthesubjectoftoday
was probably not that of yesterday, and will likely not be that of tomorrow. Given these new
challenges,atopicmodelbuiltforsocialmediadatashouldbecapableofthefollowing:(1)building
modelsinsparsedomainswithlowwordcofrequencies,(2)consideringthetemporaldimension
andadaptingtopicswithtimeinmind,and(3)filteringnoiseefficientlytoproducecoherenttopics.
Duetothevarietyofdocumenttypes,nosingletopicmodelcanbeexpectedtoperformthebest
ineverysetting.Thisistheperfecttimetolookatthelandscapeoftopicmodelsandassesswhich
arebestforthenewtypesofdocumentsandwherethereisstillaneedforimprovement.Foreach
topicmodel,wewillhighlightthestrengthsandweaknessesofthemodel,aswellasthechallenges
addressed.Thissurveytakesatimeline-likeapproachandlooksattheevolutionofunsupervised
topicmodelsinanefforttotracetheoriginsofdifferentaspectsofcurrentstate-of-the-arttopic
models. We compare topic models based on their methodology; whether they are designed for
static,temporal,oronlinedocumentcollections;thelengthofdocumenttheyaredesignedfor;the
data they have been tested on; and the metrics used to evaluate them. Table 1 provides a quick
reference for every model examined in this article. For each model, the table indicates the base
methodology of each model, whether it was designed for a specific setting, and whether it was
designed for short (social media) or long (papers, articles) documents. Most topic models were
designed for static datasets, but some were designed for online, temporal, or multiple settings.
Whiletheoldermodelsweredesignedpriortobiginnovationsinnaturallanguageprocessing
(NLP),theNLP-aidedcolumnshowsjusthowmanynewermodelshaveoptedtotakeadvantage
of these new methods. In the last two columns, we delineate between long and short document
types.Whilemanyofthesemodelscanbeusedinpracticeonalltypesofdocuments,weindicate
herewhichtypesofdocumentsthesemodelsweredesignedforandtestedonintheirrespective
papers.
Wealsodiscusstheevolutionoftheevaluationoftopicmodels,whichhasbeenlargelyincon-
sistentoverthehistoryoftopicmodels.Topicmodelingisasubjectivetask,leavingmuchofthe
determination of the quality of topic models up to the humans who use topic models. Because
evaluationisnotdoneconsistentlyforthistask,webeginoursurveybypresentingtheprevalent
evaluationmetricsinSection2.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

| 215:4 |         |                                        |     |     | R.ChurchillandL.Singh |     |     |
| ----- | ------- | -------------------------------------- | --- | --- | --------------------- | --- | --- |
|       | Table1. | TopicModelDesignCharacteristicsbyModel |     |     |                       |     |     |
TopicModelComparison
|     |     | Methodology |     |     | DesignedFor | DocumentType |     |
| --- | --- | ----------- | --- | --- | ----------- | ------------ | --- |
Model Generative GraphBased MatrixBased NLPAided Static Online Temporal Short Long
| LSI[23]       |     |     | x   |     | x   |     | x   |
| ------------- | --- | --- | --- | --- | --- | --- | --- |
| pLSI[30]      | x   |     |     |     | x   |     | x   |
| DMM[57]       | x   |     |     |     | x   |     | x   |
| LDA[8]        | x   |     |     |     | x   |     | x   |
| HDP[74]       | x   |     |     |     | x   |     | x   |
| CTM[40]       | x   |     |     |     | x   |     | x   |
| DTM[7]        | x   |     |     |     |     | x   | x   |
| TOT[86]       | x   |     |     |     |     | x   | x   |
| SWB[15]       | x   |     |     |     | x   |     | x   |
| OnlineLDA[4]  | x   |     |     |     | x x |     | x   |
| OnlineLDA[29] | x   |     |     |     | x x |     | x   |
| OnlineHDP[83] | x   |     |     |     | x x |     | x   |
| MTTM[52]      | x   |     |     |     |     | x   | x   |
| cDTM[82]      | x   |     |     |     |     | x   | x   |
| NMF[69]       |     |     | x   |     | x   |     | x   |
| NMF[36]       |     |     | x   |     |     | x x | x   |
| NMF[89]       |     |     | x   |     | x   | x   |     |
| ETM[13]       |     | x   |     |     |     | x x |     |
| TS[22]        |     | x   |     |     | x   | x   |     |
| TFM[21]       |     | x   |     |     | x   | x x |     |
| PTM[18]       |     | x   |     |     | x   | x   |     |
| BTM[88]       | x   |     |     | x   | x   | x   | x   |
| SATM[62]      | x   |     |     | x   | x   | x   |     |
| LF-DMM[56]    | x   |     |     | x   | x   | x   |     |
| LF-LDA[56]    | x   |     |     | x   | x   | x   |     |
| NVDM[49]      | x   |     |     | x   | x   |     | x   |
| lda2vec[51]   | x   |     |     | x   | x   | x   |     |
| ETM[60]       | x   |     |     | x   | x   | x   |     |
| GSDMM[94]     | x   |     |     |     | x   |     | x   |
| GPUDMM[42]    | x   |     |     | x   | x   | x   |     |
| GPUPDMM[42]   | x   |     |     | x   | x   | x   |     |
| DREx[6]       | x   |     |     | x   | x   |     | x   |
| CSTM[44]      | x   |     |     | x   | x   |     | x   |
| WELDA[12]     | x   |     |     | x   | x   |     | x   |
| LapDMM[45]    | x   |     |     | x   | x   | x   |     |
| CluWords[78]  |     |     | x   | x   | x   | x   |     |
| CluHTM[79]    |     |     | x   | x   | x   | x   |     |
| ETM[25]       | x   |     |     | x   | x   |     | x   |
| D-ETM[26]     | x   |     |     | x   |     | x   | x   |
| TND[20]       | x   |     |     | x   | x   | x   |     |
Orderedbyappearanceinthissurvey.
Wethenbeginthehistoryoftopicmodelsatthebirthofunsupervisedtopicmodelsandtheir
earlyvariants(Section3).Figure2depictstheevolutionoftopicmodelsfrominceptionupuntil
the incorporation of more modern language models such as word embedding spaces into topic
modelsandincludestopicmodelsfromSections3and4.Wedescribesomeclassicalapproachesto
onlineandtemporaltopicmodels(Section4)andmovethroughtimeinordertounderstandhow
wearriveatwherewearetoday(Section5)andwhatthereisstilltobedoneinordertocreate
accurate topic models (Section 6). Figure 3 depicts the evolution of topic models from the intro-
ductionofWord2VecwordembeddingstothepresentandincludestopicmodelsfromSection5.
Intotal,wecompareover30topicmodels.Whileanumberofsupervised,semi-supervised,and
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:5
Fig.2. ATimelineofTopicModelsfromInceptiontotheintroductionofModernTechniques.
Fig.3. ATimelineofTopicModelsfromtheintroductionofWord2VectoPresent.
topic models with knowledge have been proposed, this article focuses on unsupervised models
since they are more prevalent for large datasets. We briefly discuss other variants at the end of
Section5.3.Ultimately,ourgoalistoprovideinsightandintuitionaboutthebasicsofhoweach
topic model is designed and the strengths and weaknesses of the different topic modeling algo-
rithmsgiventhechanginglandscapeofmoderndocuments.Lastly,wediscusspresent-daytopic
modelingandwhatwebelieveareareasthatstillneedattention.
2 EVALUATIONMETHODS
An important part of topic modeling is evaluation, both datasets and evaluation metrics. Tradi-
tionally,newspaperandresearchpapersservedasthepopularsourcesoflabeleddatasetsfortopic
modelevaluation.TheTwentyNewsgroupsdataset[41]isbyfarthemostpopularavailabledataset
for evaluating topic models. It contains just over 22,000 newspaper articles labeled with topics
fromasetof20differenttopics.OthernewspaperarticlesourcessuchastheNewYorkTimesand
theAssociatedPressmadeforgoodlabeleddatasetssinceeacharticlewasassociatedwithspecific
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:6 R.ChurchillandL.Singh
topicsbythenewspaper.Researchconferencesandjournals,suchastheNeuralInformationPro-
cessingSystems(NIPS) ConferenceandthejournalScience,werealsolabeledbyauthors.Since
researchhasmovedtowardevaluatingtopicmodelsonsocialmediadata,dataprivacyconcerns
havelimitedthesharingoftheselabeleddatasets.However,Twitterallowsresearcherstodown-
loadpostsandmanytopicmodelsarebeingtestedonsubsetsofthesedata.
Intherestofthissection,wedescribesomeofthemorepopularevaluationmethodsfortopic
models.Differentgroupshaveconductedresearchontheeffectivenessofcertainevaluationmeth-
ods [14, 54, 81]. We focus on those methods used by more than one approach we present and
organizethemintothreegeneralcategories:evaluationofcoverage,evaluationofcoherence,and
qualitativeevaluation.
2.1 Coverage
Coverage refers to how well the concepts in the document collection are represented. Coverage
canbedividedintotwotypesofcoverage,topiccoverageanddocumentcoverage.Topiccoverage
measures assess how representative the topics themselves are, i.e., are the topics in a document
collectionidentifiedbythemodel.Themostprevalenttopiccoveragemeasureistopicrecall.Topic
recallisthefractionofground-truthtopicsrecoveredbythetopicmodel.
Document coverage measures evaluate how well documents are represented by topics. Topic
modelaccuracyisatypicalmeasureforevaluatingdocumentcoverage.Itisdefinedasthefraction
ofdocumentsthatareaccuratelylabeledbythetopicmodel.Inordertoevaluatetopicrecalland
accuracy,ground-truthtopicsmustbeavailable.Aswillbeseen,topicrecallisusedmoresparingly
thantopicaccuracy.
Whenafullsetofground-truthtopicsarenotreadilyavailable,othermetricsareused.Purity
is the accuracy of the model if documents are always assigned the dominant topic. This metric
attemptstopenalizemodelsthatassignalargenumberoflow-probabilitytopicstodocuments,as
opposedtoamodelthatassignsahighprobabilitytoasingletopicacrossthedocumentcollection.
Anotherwaytomeasureconvergenceistocomparetopicsacrosstopicmodels.KL-Divergence
isusedtoshowhowanewmodel’sprobabilitydistributionovertopicsdiffersfromthatofabase-
linetopicmodel.KL-Divergenceistheexpectationofthelogdifferencebetweentheunderlying
probability distributions of the topic models [38]. Instead of relying on ground-truth topic sets,
KL-Divergence allows one to compare the topic set of a new model to a previously established
state-of-the-artmodel.
Allofthecoveragemethodsdescribedsofarrequire,tosomedegree,priorknowledgetopics,
eitherin theform of ground-truth topicsor in theform of a state-of-the-arttopicmodel’s topic
distribution.In1999,Hofmanntookadifferentapproachwhenheintroducedperplexity [30].In-
stead of relying on ground-truth data to compute topic or document coverage, perplexity is a
probabilistic measure of how well a model can predict a held-out sample of documents. It is a
waytocompareprobabilistictopicmodels.Moreprecisely,perplexityistheaveragenegativelog-
likelihood of held-out documents. A lower perplexity means that the topic model does a better
jobofmappingtheheld-outdocumentstothetheoreticaldistributionofwordsinthedocuments,
therebyhavingbetterdocumentcoverage.Othershaveusedthelog-likelihoodofheld-outdocu-
ments(notnegated)asanevaluationmethod.Itshouldbenotedthatitisdebatedwhetherornot
perplexityisareasonableevaluationmethodfordeterminingtopicquality.Changandcolleagues
showedthatperplexityandhumanjudgmentwerenotwellcorrelated[14].
2.2 Coherence
While coverage is an important measure for high-quality topics, by itself, coverage is not suffi-
cientforguaranteeingindividualtopicquality.Tocombatthepotentialfornoisyandunintelligible
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:7
topics,authorsturntowhatwecallcoherenceevaluationmethods.Thesemethodsattempttodis-
cerntheusefulnessofindividualtopicsandofwordsinindividualtopics.
Many of the earlier works took a classic approach to coherence evaluation—precision. Given
ground-truth topics and the top words from each approximated topic, a precision score can be
calculatedbytakingthefractionofwordsfromeachapproximatedtopicthatfallsintothebest-
fittingground-truthtopic.
Aswewillsee,coherenceevaluationmethodswerelargelyabandonedaftersomeoftheinitial
topicmodelswereintroduced.Onlyrecentlyhascoherenceresurfacedasanimportantcomponent
oftopicmodelevaluation.Themostcommoncoherencemetricispointwisemutualinforma-
tion(PMI).TherearemanydifferentvariantsofPMI,butatitscore,PMIattemptstomeasurethe
closenessofwordsineachtopicbasedontheirrelativecofrequencieswitheachother.Itspopular-
ityhasincreasedbecauseunlikeprecision,noground-truthtopicsetisrequiredtocalculatePMI.
Anumberofothercoherencemeasureshavebeenusedtoevaluatetopicmodels.C ,asdefinedby
V
Röderetal.[64],isacombinationofcosinesimilarityandnormalizedPMIunderaBooleansliding
window.Itattemptstocaptureproximitybetweenwordsaswellasthemutualinformationand
vectorsimilarity.
Diversity isanevaluationmethodthatattemptstoaccountforwordoverlapintopics[25].Ifa
modelcannotdecidewhichtopicawordbelongsto,itmayassignitwithreasonablyhighproba-
bilitytomultipletopics.Thismakesatopicsetlesscoherent.Topicdiversityisthepercentageof
uniquewordsinthetopicset,consideringthetop-k wordsofeachtopic.LikePMI,diversitydoes
notrequireknowledgeofground-truthtopics.Methodssimilartotopicdiversityhaveappeared
underdifferentnamesovertheyears,includingtopicuniqueness[53]andtopicoverlap[21].
Adjusted Rand Index (ARI) measures the agreement of topic-document classifications. For
a pair of documents, either they should or should not be clustered together based on some sim-
ilarity measure. The Rand Index calculates the percentage of document pairs that are correctly
placedtogetherorcorrectlynotplacedtogether.ARIcorrectstheRandIndexforchance.ARIis
mostcommonlyusedwhenthetopic-documentlabelsareknown,sothatthesimilaritymeasure
is whetherthedocumentsactually belong to thesame topic. However, ARI could also employ a
similaritymeasurethatdoesnotrelyonground-truthlabels.
Signal-to-Noise Ratio (SNR), similar to precision, uses ground-truth topics to compare the
number of correct and incorrect topic words in each approximated topic. A high SNR indicates
morecoherenttopics,whilealowSNRindicateshighvolumesofnoiseandthereforelesscoherent
topics.Finally,wordintrusion,definedbyChangetal.[14],isahuman-judgedcoherencemethod
thatconsistsofgivingahumansixwords,fivefromthesametopicandonethatdoesnotbelong
inthetopic.Ifhumanscanconsistentlypickwhichworddoesnotbelong,thenthetopicmodelis
judgedtobemorecoherent.
2.3 Qualitative
Whiledifferentcoverageandcoherencemetricsgiveusinsightintothequalityoftopicmodels,hu-
manevaluationscaptureinsightsthatquantitativeanalysiscannot,includingevaluatingmultiple
criteriasimultaneouslyandlookingatthetopicsusinga“commonsense”lens.Assuch,coverage
andcoherenceevaluationsinandofthemselvesareinsufficientjudgesofatopicmodel.Aquali-
tativeevaluationofatopicmodelisanyevaluationthatdisplaysthetopicsproducedbyamodel
forreaderstoassessthemselves[8].Qualitativeevaluationconsistsofpresentingtopicsgenerated
during the experiments to human evaluators. In some cases, a qualitative evaluation is used to
compareasingletopicacrossallthemodelstested.Forexample,ahumanevaluatormaybegiven
atopic(orsetoftopics)outputbymultiplemodelsandaskedwhichoneseemstocapturethetopic
thebest.Qualitativeanalysescanalsobeusedtoshowthediversityofanentiretopicsetgenerated
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:8 R.ChurchillandL.Singh
bythenewmodel.Forexample,ahumanevaluatormaybeaskedtoidentifytopicsthataremost
similarormostdifferentfromaspecifictopic.Inthecaseofsometemporalmodels,aqualitative
analysisshowstopicsalongwithwhentheyaremostprevalentalongatimescale.Thesecanthen
be mapped to relevant events to show the evolution of each topic. A qualitative evaluation of a
topic model is used to portray what math and statistics often cannot: human understandability.
A qualitative analysis can be misleading if authors choose to display only a small subset of the
besttopics.However,awell-donequalitativeanalysiscanbeveryvaluableifithelpsresearchers
better understand the quality of topics generated and/or how a new model’s topics might differ
frombaselinemodels.
2.4 EvaluationMappingtoProposedModels
Table2showswhichmodelsusedwhichevaluationmethodsfortheirexperiments.Table2con-
tainsonlytheevaluationmethodsthatweredefinedandusedinmorethanonepaperexaminedin
thissurvey.Manymoreevaluationmethodshavebeenusedinthepasttodemonstratethequality
oftopicmodels.Whileourlistisnotexhaustive,itdoesshowatrendinmethodsovertime.Cov-
erage and coherence methods have waxed and waned in popularity throughout the years, with
perplexity falling in favor of pointwise mutual information. The qualitative evaluation has be-
comejustasnecessaryasagoodquantitativeevaluationforportrayingtopicmodelquality.Other
evaluationmethodsfindahomehereandthere,butPMIandqualitativeevaluationhavebecome
commonpractice.
3 EARLYTOPICMODELS(1990–2006)
3.1 PrecursorstoTopicModels:LatentSemanticIndexing
Topicmodelscantracetheiroriginsbackto1990,aswecanseeinFigure2.Intheirarticle“Index-
ingbyLatentSemanticAnalysis,”Deerwesteretal.describedhowonecoulduselatentsemantic
analysis to automatically index and retrieve documents from large databases [23]. The authors
deviseamodelcalledLatentSemanticIndexing(LSI).
Givenavocabulary,asetofdocumentscanberepresentedbyaword-documentmatrix,where
eachdocumentisavectorthesizeofthevocabulary,andeachentryinthevectoristhefrequencyof
therelativevocabularywordinthedocument.LSItakestheword-documentmatrixandperforms
asingularvaluedecomposition(SVD)toreducethedimensionalityonthedocumentsideofthe
matrixbutretainthemeaningfulnessofthewords.Indoingso,LSIcreatedthefirsttopicsetsfrom
documents.ThesetopicswerevectorsofwordfrequenciesthatwerederivedusingSVDandcould
becomparedtothespecificwordfrequencyvectorsofindividualdocumentsinordertoclassify
thedocumentsintotopics.Notably,LSIdefineswhatwillcometobeknownasthebag-of-words
model.Thebag-of-wordsmodelisoblivioustotheorderingofwordsinadocument;itcaresonly
aboutthefrequencyofwords.
In1999,ThomasHofmannkickedoffwhatturnedouttobethefieldoftopicmodeling.Hofmann
introducedProbabilisticLatentSemanticIndexing(pLSI),inanattempttoproducemorecon-
sistently accurate results in domain-specific documents than LSI [30]. Hofmann never actually
referstotopicsinhispaper,callingthemfactorsinstead.ByreplacingtheSVDwithagenerative
datamodel,calledanaspectmodel inthepaper,hewasabletouseanexpectationmaximization
algorithmtotrainthemodel.InsteadoftopicsbeingtheresultofanSVD,thetopicswereaprob-
abilisticmixtureofwordsbasedontheirjointprobabilitieswithdocuments.
3.2 DMMandLDA:TheFirstTopicModels
3.2.1 DMM. Originally interested in improving the accuracy of text classifiers that until
then had used labeled data to classify text, in 2000, Nigam et al. set out to determine how to
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

| TheEvolutionofTopicModeling |     |                                            |     |     |     | 215:9 |
| --------------------------- | --- | ------------------------------------------ | --- | --- | --- | ----- |
|                             |     | Table2. TopicModelEvaluationMethodsbyModel |     |     |     |       |
EvaluationMethodPrevalence
|     |     | Coverage |     |     | Coherence | Qualitative |
| --- | --- | -------- | --- | --- | --------- | ----------- |
Model Recall Accuracy LL Perplexity KLD Purity Precision PMI Diversity ARI Qualitative
| LSI[23]       | x   |     |     |     | x   |     |
| ------------- | --- | --- | --- | --- | --- | --- |
| pLSI[30]      |     |     | x   |     | x   |     |
| DMM[57]       | x   |     |     |     | x   |     |
| LDA[8]        |     |     | x   |     |     | x   |
| HDP[74]       |     |     | x   |     |     | x   |
| CTM[40]       |     | x   | x   |     |     | x   |
| DTM[7]        |     | x   |     |     |     | x   |
| TOT[86]       |     | x   | x   |     |     | x   |
| SWB[15]       |     |     | x   |     | x   | x   |
| OnlineLDA[4]  |     |     |     |     | x   | x   |
| OnlineLDA[29] |     |     | x   |     |     |     |
| OnlineHDP[83] |     | x   |     |     |     | x   |
| MTTM[52]      |     |     | x   |     |     | x   |
| cDTM[82]      |     |     | x   |     |     | x   |
| NMF[69]       |     | x   |     |     |     |     |
| NMF[36]       | x   | x   |     |     | x   |     |
| NMF[89]       |     | x   |     |     | x   | x x |
| ETM[13]       |     |     |     |     |     | x   |
| TS[22]        |     | x   |     |     |     |     |
| TFM[21]       | x   | x   |     |     | x   | x   |
| PTM[18]       |     |     |     |     | x x | x   |
| BTM[88]       |     |     |     | x   | x   | x x |
| SATM[62]      |     | x   |     | x   | x   |     |
| LF-DMM[56]    |     |     |     | x   | x   | x   |
| LF-LDA[56]    |     |     |     | x   | x   | x   |
| NVDM[49]      | x   | x   | x x |     | x x | x   |
| lda2vec[51]   |     |     |     |     |     | x   |
| PTM[97]       | x   | x   |     |     | x   | x   |
| ETM[60]       |     |     |     |     | x   | x   |
| GSDMM[94]     |     |     |     |     | x   | x   |
| GPUDMM[42]    |     | x   |     |     | x   |     |
| GPUPDMM[42]   |     | x   |     |     | x   |     |
| DREx[6]       | x   |     |     |     | x x | x   |
| CSTM[44]      |     | x   |     | x   | x   | x   |
| WELDA[12]     |     |     |     |     | x   | x   |
| LapDMM[45]    |     | x   |     |     | x   |     |
| CluWords[78]  |     |     |     |     | x   | x   |
| CluHTM[79]    |     |     |     |     | x   |     |
| ETM[25]       |     |     |     |     | x x | x   |
| D-ETM[26]     |     |     |     |     | x x | x   |
| TND[20]       | x   |     |     |     | x x | x   |
Orderedbyappearanceinthissurvey.
incorporate unlabeled data into text classification [57]. They would again use expectation maxi-
mizationalongwithagenerativemodel,buttheyaddedtheDirichletdistributiontotheconversa-
tion.TheDirichletdistributionisthemultivariategeneralizationoftheBetadistribution.Instead
ofusingjustαandβtodefineitsdistribution(asintheBetadistribution),theDirichletdistribution
isdefinedwithrespecttok,wherek canbeviewedasthenumberofdimensionsassociatedwith
theDirichlet.Together,thesedimensionsareusedtoformaprobabilitydistributionthatisnormal-
izedusingα.TheDirichletdistributionisidealfortopicmodelingbecauseeachtopiccanbecastas
oneofthesekdimensionsinthedistribution.Intuitively,eachofthektopicshasitsownprobabil-
ityofappearinggiventhedistributionandobserveddocument.Intheiralgorithm,adocumentis
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:10 R.ChurchillandL.Singh
Fig.4. LDAGraphicalModel(PlateNotation).
sampled by one topic and generated according to that topic based on a prior distribution repre-
sentedbyaDirichletdistribution.Theirexperimentsshowthatwhileinsomecasestheirmodel
improvesresultsoverlabeleddataby30%,themodelcanhurtperformanceinothercases.While
originallynotframedasatopicmodel,thismodelwouldcometobeknowninthetopicmodeling
literatureastheDirichletMultinomialMixture(DMM)andthemixtureofunigramsmodel.
3.2.2 LDA. Thetermtopicmodelwascoinedin2001byBleietal.whentheyproposedLatent
DirichletAllocation(LDA)[8,9].TheauthorsidentifiedproblemswiththepLSImodel,includ-
ingthelargenumberofparametersneededtofine-tunepLSIandtheinabilityofonetoquerythe
pLSImodelwithnewunseendocuments.Furthermore,theauthorsofLDAmadeakeyobservation
thatenabledthemtobemoresuccessfulinfindingaccuratetopics:documentsarenotgenerated
accordingtoonlyonetopic.
LDAborrowsfromtheideasofpLSI[30]andcreatesitsowngenerativemodel,thistimebased
on the use of the Dirichlet distribution [57]. It uses the same bag-of-words model as pLSI and
the same document-term matrix defined by pLSI. The key innovation of LDA over DMM and
pLSI is that LDA does not sample one topic per document. Instead, it samples a distribution of
topics for a document, allowing a document to be probabilistically generated from many topics.
LDA’sgoalistofindtheparametersofatopic-worddistributionthatmaximizesthelikelihoodof
documentsinthedatasetoverk topics.Eachdocumenthasatopicdistributionspecifictoitthat
is proportional to the probability of each of its words in the topic-word distribution. LDA uses
expectationmaximizationtotrainitsmodelandhastwomainparametersasidefromk:α andβ.
α correspondstotopics-per-documentratio.Settingα higherresultsinmoretopicsperdocument.
β correspondstowords-per-topicratio.Settingβ lowerresultsinfewerwordspertopic.Foraset
ofM documentsD,thegenerativeprocessofLDAworksasfollows:
Ford ∈D:
(1) RandomlydrawthenumberofwordsN ford.
(2) Randomlydrawthetopicdistributionθ fromtheDirichletdistribution,conditionedonthe
parameterα.
(3) Foreachwordw ,0 ≤i < N:
i
(a) Drawatopicz fromθ.
i
(b) Drawawordw basedontheprobabilityofw giventhetopicz andconditionedonthe
i i i
parameterβ.
Figure4showsthegraphicalrepresentationofLDAusingthenotationabove.
TheauthorsshowthatLDAperformsbetterintermsofperplexitythanpLSI.Themaindatasetis
acorpusof16,000newspaperarticlesfromtheAssociatedPress,containingavocabularyof23,075
terms.Theauthorsidentifyaproblemoftermsparsity,writing,“thelargevocabularysizethatis
characteristicofmanydocumentcorporacreatesseriousproblemsofsparsity.Anewdocumentis
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:11
verylikelytocontainwordsthatdidnotappearinanyofthedocumentsinatrainingcorpus”[9].
TheauthorsattempttoaccountforthisbyusingLaplacesmoothing,essentiallyassigningsome
verylowprobabilitytoeverywordsothatitcanbeclassifiedbythemodel.Theproblemofsparsity
persistsalltheseyearslaterinevenmoreextremefashionduetothevastamountofslangandlack
ofstructureinsocialmediaposts,open-endedsurveyresponses,andothershorttexts.
LDAisstillsynonymouswithtopicmodeling,andmanyothermodelstothisdayarevariations
ofthismodelthatwasoriginallyconceived20yearsago.LDAhasmanyvariationsandhasbeen
appliedtomanydifferenttasksinandaroundthenaturallanguageprocessingrealm.Jelodaretal.
takeanin-depthlookatLDAanditsvariantsintheirsurveyofLDA-basedtopicmodels[33].
3.3 EarlyLDAVariants
IntheyearsafterdesigningLDA,researchersbegantoimproveuponthismodelinordertosolve
someproblemsnotaddressedbyLDA,includingtheselectionofk,thetopicindependenceassump-
tion,andthedynamicnatureoftopics.
3.3.1 HierarchicalDirichletProcess. OneproblemwithLDAisthatithasaparameter,k,repre-
sentingthenumberoftopicsthatshouldbesampled,thatneedstobespecified.Thiswasaproblem
becausemostpeopledonotknowhowmanytopicsanunexploreddatasetcontained.Theprocess
offindingtherightkforanewdatasetwastedious,requiringusersofLDAtotestusingnumerous
settingsofk,manuallyevaluatingtheresultsaftereachiteration.Tehetal.introducedtheHier-
archicalDirichletProcess(HDP),anon-parametricadaptationofLDAthatapproximatesthe
parameterk usingaprobabilisticmodel[74].
In HDP, the Dirichlet processes representing topic distributions are distributed according to
another Dirichlet process. Essentially, not only are topics sampled probabilistically, but also the
numberoftopicsisalsosampledprobabilistically.HDPstillallowsforthefine-tuningofα andβ
inthesamewaythatLDAdoes,butthekvalueischosenprobabilisticallysoastotakethetedious
processoutoftheuser’shands.DuetotheextralayerofDirichletprocesses,HDPisevenmore
intractabletocomputeprecisely.Theauthorsreplacethedeterministicexpectationmaximization
algorithmfromLDAwithaGibbssamplertoimproveitsefficiency.
Intheirexperiments,theauthorsshowthatHDPprovidestopicsetswithconsistentlylowper-
plexityforanematodebiologyabstractdataset(5,838abstracts)andaNIPSarticlesdataset(1,447
articles).
3.3.2 CorrelatedTopicModels. AnotherlimitationofLDAisthatitassumesindependenceon
topics, where in the real world, topics are often correlated with each other. For instance, topics
aboutweatherandsailingareprobablymorecorrelatedthantopicsaboutweatherandvideogames.
LaffertyandBleiintroduceacorrelatedtopicmodel(CTM)toaddressthisissue[40].
The key difference between CTM and LDA is that in CTM, the authors replace the Dirichlet
distribution with a logistic normal distribution and add a covariance matrix between topics to
modelcorrelation.ThegenerativeprocessisidenticaltothatofLDA;theonlythingthatchanges
is the distribution from which topic probabilities are drawn. The assumption that exists with a
Dirichletdistribution—thattopicsareindependentofeachother—isnotnecessaryinCTM,since
thecovariancematrixofthelogisticnormaldistributionprovidesameasureofhowclosetopics
aretoeachother.Thisallowsforthemodeltopicknotonlywordsbasedontopicsthataredrawn
fromtheobserveddocumentbutalsotopicsthatarecorrelatedwiththeprobabletopics.
Todemonstratetheeffectivenessoftheirapproach,theauthorsperformtopicmodelingonarti-
clesfromthejournalScience.ThedomainofSciencearticlesisspreadacrossmanyfieldsofstudy,
butintuitivelythereshouldbesomecorrelationovermanyofthesefields.Again,theauthorsuse
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:12 R.ChurchillandL.Singh
perplexityastheirevaluationmethod.TheauthorsshowthattheCTMisabletomaintainstrong
performanceevenasthenumberoftopicsgrows,whereasLDAfallsoffataround30topics.
3.3.3 DynamicTopicModels. LDAcapturesthetopicsofastaticdatasetatonemomentintime,
butitdoesnotcapturetheevolutionoftopicsacrosstime.BleiandLaffertycreatethefirsttemporal
topicmodel,calledDynamicTopicModel(DTM),withthegoalofcapturingtopicevolution[7].
Atemporaltopicmodel isatopicmodelthataddsatime-basedcomponenttotopics.Insteadofa
topicconsistingofasetofwords,atemporaltopicmodelproducestopicsthatconsistofasetof
wordsandatimestamportimerange.Asimpletemporaltopicmodelcouldseparatedocuments
intoarangeofdatesandperformmodelingoneachsubsetofdocumentsinturn.
TheauthorsagainusethejournalScience,whichhasbeenpublishedcontinuouslysince1880.
Astechnologyandtheknowledgeofhumanshaveadvanced,sotoohavethetopicscoveredinthe
journal,sotheauthorshypothesizethatifDTMisagoodmodel,itshouldbeabletocapturethe
evolutionoftopicsthroughoutthehistoryofScience,visualizingthebirthanddeathoftopics.
Tocreatethedynamictopicmodel,theauthorssliceadatasetintotimeperiods,whereinonlya
giventimeperioddocumentsareexchangeable.TheauthorsreplacetheDirichletdistributionof
topicswithasequenceofGaussiandistributions,eachofwhichrepresentsthetopicdistribution
foradifferenttimeslice.TheauthorsreplacetheDirichletpriorα withaGaussianpriorγ ineach
time period. The authors state that their Gaussian distributions are an extension of the logistic
normal distribution to deal with time series data. The approach that the authors use is not so
muchatemporaltopicmodelasitisaseriesoftopicmodelstiedtogetherinsequence.Thetopic
distributionandγ priorarepassedontothenexttimeperiodasastartingpoint.Thetopicsfor
timeslicet areconditionedonthetopicsfromtimeslicet −1andbythedocumentsintimeslice
t.Thisleadstotopicsthatseeminglyevolvethroughtime,appearingastheybecomerelevantand
disappearingastheylosepopularity.
The authors show how topics related to Darwin and Einstein spike as each become famous
fortheirworkandslowlydieoutastimepasseson.Anotherexamplethattheypointoutinthe
paper is the topic about the moon, which is moderately popular throughout the late 1800s and
early 1900s, but which spikes during the space race of the Cold War. The authors further show
theabilityofDTMtopredictfuturetopicsgivenitscurrenttopicdistribution.Theycomparethis
predictive power to the approach of chaining LDA through the same time slices and show that
DTMisfarmoreaccuratewhentaskedwithpredictingfuturetopics.
In2006,WangandMcCallumproposedatemporaltopicmodelbasedonLDAthatworksona
continuous-timemodel[86].Theadvantageofthisapproach,calledTopicsoverTime(TOT),is
thateventsarenotuniformlydistributedovertime,souniformlydistributedtimeepochsdonot
fully capture the evolution of topics over time. TOT models time alongside word co-occurrence
in order to capture time-sensitive events, such as different wars and the rise of technology. The
continuousdistributionovertimeallowsfortheusertonotspecifythelengthofanepoch,instead
relyingonthealgorithmtofindsignificantwordco-occurrencesoverrelevanttimeperiods.
Wang and McCallum mostly provide a qualitative analysis of their topic model but perform
asmallquantitativeanalysisoftheirmodelcomparedtoLDA,wheretheyuseKL-divergenceto
showthatTOTproducesslightlymoredistincttopicsthanLDA.TheytestedTOTonthreedifferent
datasets,onecontaining208presidentialStateoftheUnionaddresses,onecontaining13,300emails
betweencomputerscienceresearchers,andthefinalconsistingof2,326researchpapersfromthe
NIPSconferencebetween1987and2003.
DTMandTOTrepresentthefirstattemptsatapplyingLDAinatemporalfashioninorderto
capturetheevolutionoftopics.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:13
3.4 TopicModelsConsideringBackgroundNoise
In2006,Chemuduguntaetal.[15]proposedatopicmodel,SWB,thatincorporatedtwosecondary
distributionstocapturespecialwords(specifictoadocument)andbackgroundwords(whatwe
would call noise words). The goal of the proposed method is to capture the difference between
genericdocuments,highlyspecificdocuments,andthoseinbetween.Intheory,thisshouldpro-
ducedocumentsthataretruetotheapproximatedtopicsbutthatalsovaryinspecificityasisthe
caseintherealworld.TheyuseLDA[9]asthebasisoftheirmodelandinsertthespecialwords
andbackgroundwordsdistributionsdirectlyintothescheme.Theauthorsproposeusingarandom
variabletoactasaswitch,whichdeterminesifthenextwordinadocumentisgeneratedfromthe
specialwordsdistribution,thebackgrounddistribution,orthechosentopic.Theswitchvariableis
sampledfromadocument-specificmultinomialconditionedonaDirichletprior,sothateverydoc-
umentisindividuallytailored.Thespecialwordsdistributionissampledfromadocument-specific
multinomialconditionedonanotherDirichletprior,suchthateachdocumenthasitsownsetof
specialwords.Thebackgroundwordsdistributionissampledfromadataset-specificmultinomial
conditioned on another Dirichlet prior. This final distribution is dataset-wide so that commonly
usedwordscanbeidentifiedacrossalldocuments.
Intheirexperiments,theauthorsshowtheeffectivenessofthebackgrounddistributiononfour
differentdatasetsandcomparetheirmodelvariantstoLDAusingperplexityandprecision.The
fourdatasetsusedintheexperimentsareofunspecifiedsizebutconsistofNIPSarticles,Associ-
atedPressarticles,U.S.Patents,andFederalRegisterarticles,respectively.Theauthorsshowthat
theirmodelvariantsbeatLDAintermsofperplexityandbeatLDA[9]andLSI[23]intermsofpre-
cisionwhentaskedwithretrievingdocumentscontainingatleastonequeryword(adownstream
informationretrievaltask).Theauthorsuseanewspaperdatasetconsistingof3,104articlesabout
EnronfromtheNewYorkTimestoperformaqualitativeanalysis,highlightingtopicwords,special
words,andbackgroundwords.
Whiletheauthorsclearlyintendedtheirmodelbeusedforinformationretrievalpurposes,their
proposalisthefirstrealattempttofilternoisewordsfromtopics.Webelievethattheywereahead
oftheirtimeinthisregard.Aswewillsee,identifyingandfilteringnoiseintopicmodelsbecomes
crucialasthetypeofdocumentsthatwecareabouttransitionsfromlong,well-editeddocuments
toshort,noisyones.
3.5 ComputationalComplexityofGenerativeModels
TheearlyimplementationsofLDAanditsdescendantswereverycomputationallyexpensive.Son-
tagandRoyprovedthecomplexityboundsofgenerativetopicmodels[73].Theyshowedthatif
a document is generated by a mixture of the entire topic set, inference is NP-Hard. However, if
adocumentisgeneratedbyaconstantnumberoftopicsstrictlysmallerthank,inferencecanbe
solvedinO(N4),whereN isthenumberofdocumentsinthedataset.Thesecomplexityboundsse-
verelylimithowfasttopicscanbeapproximatedinsomeofthemostpopulartopicmodels.While
approximationalgorithmsdoexist,improvingtheefficiencyofgenerativetopicmodelsisstillan
importantresearchdirection.
4 TEMPORALANDONLINETOPICMODELS(2006–2011)
4.1 TemporalTopicModels
AsdiscussedinSection3,by2006,BleiandLafferty[7],aswellasWangandMcCallum[86],had
alreadybeenexperimentingwithwaysofdetectingtopicsastheyriseandfalloverthecourseof
time.Whiletheirapproacheswererelativelysuccessful,theywerecomputationallycostly.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:14 R.ChurchillandL.Singh
In2007,Nallapatietal.proposedanewgenerativemodel,MTTM,toimproveontheDynamic
Topic Model’s temporal aspect [52]. The authors replace LDA’s multinomial distribution over
wordswithaPoissondistributionoverthewords.Foreachwordineachepoch,anexpectedfre-
quencyineachtopiciskeptintheformofaPoissonmean.Theauthorsrepresenteachtopicasa
vectorofPoissonmeans,whichallowsfortheevolutionoftopicsovertimeepochstobemonitored
moreefficiently.TheauthorsshowthatMTTMworksinahierarchicalmanner,startingwiththe
smallest time epochs and building up into bigger and bigger epochs. This hierarchical structure
allowsforusersto“zoomin”oncertaintimeperiodsforaparticulartopic.
In 2008, Wang et al. proposed cDTM [82], a continuous version of the DTM. In it, as in TOT,
cDTMdoesnotrequiretimetobediscretized,optingforacontinuousdistributionthatislesscom-
putationallyintensivethantheoriginalDTM.Theauthorsfirstprobabilisticallyselectatimeframe
foreachtopicbeforeinferringtheworddistribution.Thisapproachallowsforfasterinferenceof
amorefine-grainedtimelineoftopics.
In2009,Iwataetal.proposedTopicTrackingModel(TTM)[32],amodelcreatedforanalyz-
ingconsumerpurchasebehaviorone-commercewebsites.ItborrowstheideaofpassingDirichlet
priors to future time periods from DTM [7] but changes how it occurs. The authors attempt to
modeltheitemsthatauserbuysateachtimeperiodastopics,inordertoinformfuturetimepe-
riodsofitemslikelytobeboughttogether.Intheabstractconceptoftopicmodels,usersintheir
schemerepresentdocuments,andtheitemsthatauserbuysrepresentindividualwordsinadocu-
ment.Becauseitwasdesignedtotrackthetrendsofconsumers,theypassuser-specificpriorsinto
futuretimeperiods.WhereasinDTMthetopicdistributionandglobalγ priorarepassedontothe
next time period, TTM passes on the topic distribution and a specific distribution for each user
representingtheirinterests,i.e.,theirfrequentlyusedwords.Thiseffectivelyallowsthemodelto
tracknotonlytheevolutionoftopicsthroughouttimebutalsotheindividualevolutionofusers
throughouttime.Theauthorsalsoallowfor“long-termdependencies”tobepassedon,wherein-
steadofjustpassingthetopicdistributionandinterestsfromtheprevioustimeperiod,thoseofthe
pastLtimeperiodsarepassedalong.Thesedependenciesareincludedwiththeacknowledgment
thatusers’futureinterestsarenotsolelyderivedfromthemostrecenttimeperiod.
TheauthorstestTTMagainstvariationsofLDAontwodatasetsoftransactions.Thedatasets
containtransactionsfrommovieandcartoondownloadingwebsites,respectively.Theformercon-
tains 70,122 users, and the latter contains 143,212 users. To show the capabilities of TTM, they
showtheN-bestaccuracyofTTMandthebaselinemodels,whichmeasuresthepercentagethat
purchased items are contained in the set of N-highest-probability items. The accuracies of the
movie dataset are low for every model, but TTM beats all LDA variants on both datasets. The
authors also show that TTM’s runtime is much faster than the slowest LDA variant, and only
30%to40%slowerthanthefastestLDAvariants(includingBanerjeeandBasu’sversionofonline
LDA[4]).
This is a novel implementation of a topic model in a temporal setting, and although it moves
awayfromthetraditionaluseoftopicmodelsondocuments,itpresentsaframeworkforworking
with dynamic topic models. If we view each post in a Reddit thread as a transaction, then this
approachcouldbeafoundationfortemporalmodelinginsocialmediadata.
4.2 OnlineTopicModels
Theseearlymodelsalsoreliedonafixedvocabularythatwasdeterminedduringinitializationof
themodel.However,therearetimeswhennewdocumentsareaddedthatcontainsomenewwords.
In this section, we explore how LDA and HDP were transformed from the original batch-based
Bayesian inference to online versions that require fewer computations, and allow for additional
vocabularytobeaddedafterinitialization. Thiscanoccurifthedatasetistoolarge toload into
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:15
memoryallatonce,orifthedatasetisbeingcontinuouslygenerated(streamingsetting),suchas
fromastreamingAPIorRSSfeed.
4.2.1 FasterTopicModelInference. In2008,Porteousetal.introducedafasterimplementation
ofaGibbssamplerforLDAthatwasuptoeighttimesfasterthantheoriginal[59].Themaincon-
tributionofPorteousetal.isthatinsteadofinferringadocument’sprobabilityofbeinginevery
topic, they infer only the probability of a document being in a few of the most likely topics for
thatdocument.Thissavesalotofinferencetimeinlargedatasets,andtheauthorsshowthatin
two large datasetswith large numbersof topics, thetop 20 topicsfor a given document explain
about90%ofthatdocument.Theauthorstestedtheirmodelsonfourdatasets.Thefirstcontained
1,500papersfromtheNIPSconference,thesecondcontained39,861emailsfromEnron,thethird
contained 300,000 news articles from the New York Times, and the final contained 8,200,000 ab-
stractsfromPubMed.Theauthorsshowthatonthesmallerdatasets,thespeedupoftheirmodel
isconsiderableoverLDA,butthattheeffectisdiminishedinthelargerdatasets.
In2009,Yaoetal.describedmultipleapproachestomakingtheinferenceofLDAfasterwhile
retaining accuracy[91]. The authorsintroducethree different variations of Gibbs sampling that
improveoverallinferencespeed.Allmethodsassumethatinferenceisbeingperformedonsmaller
chunksofdata,addingmorechunksineachiteration.Thefirstmethodresamplesalltopicsover
alldocuments(newandold)ineachiteration.ThisisfasterthannormalGibbssamplingbecauseit
issteadilyincreasingthenumberofdocumentsperiterationinsteadofinferringtheentiredataset
everyiteration.Thesecondmethodresamplestopicsonlyfornewdocuments.Thisismuchfaster
thanthepreviousmethod,becauseitfixesthetopicassignmentsofpreviouslyseendocuments.It
usesthosetopicassignmentsastrainingdataforassignmentsoftopicstofuturedocuments.The
thirdmethodisanonlineversionofGibbssampling,whichindependentlyprocesseseachdocu-
ment.Thetopic-worddistributionuseddrawsonlyfromthecurrentdocumentandthetraining
data.TheyalsoproposealogisticregressionclassifierandNaiveBayesclassifierasothermeansof
performinginference.Theauthorsperformexperimentsonrelativelysmalldatasets(1,740NIPS
papersand51,616paperabstracts).YaoandcolleaguesshowthattheonlineversionsoftheirGibbs
sampler converge much faster than the traditional Gibbs samplers on these small datasets. Al-
though their versions are faster, the authors note that each individual iteration of inference is
muchlongerthanthoseofthetraditionalGibbssamplers.
4.2.2 Online LDA. In 2007, Banerjee and Basu [4] wrote a short survey of topic models for
textstreams.Theyimplementbatchandonlinetopicmodelsandpresentthefirstonlinescheme
forLDA.Theirapproachisstraightforward,runningLDA[9]onsmallbatchesofdocumentsina
sliding-windowformat.ThetopicdistributionandDirichletpriorsareinitializedforthenextbatch
usingtheapproximationsfromthepreviousbatch.Theauthorsshowthattheirversionofonline
LDAismuchfasterthanthebatchversion.Theyalsotesttheirmodelsusingnormalizedpointwise
mutualinformation,theearliestoccurrencethatwehaveseenofitsuseintopicmodelevaluation.
They use the full Twenty Newsgroups dataset [41], which contains approximately 20,000 news
articles,andfivesmallsubsetsofthedatasettotestthemodels.
In 2010, Hoffman et al. developed an online variational Bayes (VB) algorithm to allow for
faster inference of topics using LDA [29]. The authors created the online VB algorithm by com-
puting an approximate expectation step based on the current observed document and the prior
topic-worddistribution.Theauthorscomputetheapproximatedistribution,assumingthattheen-
tirecorpusconsistsofthisonedocument.Theythenadjustthetruetopic-worddistributiontoa
weightedaveragebetweenthepreviousdistributionandtheapproximateddistribution.Thisnew
online version relies only on the current observed document and the approximated topic-word
distributionfromallpreviouslyobserveddocuments.Inimplementation,insteadofobservingone
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:16 R.ChurchillandL.Singh
documentatatime,theauthorsobserve“mini-batches,”orsmallcollectionsofahandfulofdocu-
ments.Thisallowsformoreaccurate,butstillfast,inferenceoftopics.
Intheirexperiments,theauthorsshowthatincreasingbatchsizefrom1upto256documents
resultsinbetteraccuracyintermsofperplexity.Theauthorsshowthatonacorpusof3.3million
Wikipedia articles, it took 3 days to complete, with about half of that time devoted to the infer-
ence(preprocessingaccountedfortheotherhalf).Theynotethatevenoneiterationofthebatch
version of the algorithm would have taken many days to complete. The authors do not provide
specificationsforthemachinethatexperimentswereperformedon,soitisnotpossibletosayhow
longsuchexperimentswouldtaketoday.However,forthesakeofcomparisonbetweenonlineand
batchLDA,itseemssafetosaythatonlineisconsiderablyfaster.
4.2.3 OnlineHDP. In2011,Wangetal.[83]developedanonlinevariationalBayesalgorithm
forHDP.Theauthorsapplythesameapproach,usingmini-batchesofdocumentstoproduceap-
proximationsoftheexpectationstepoftheexpectationmaximizationalgorithm.
Due to HDP’s inherently more complex computational nature (it infers the number of topics
aswell),theauthorsusedmuchsmallerdatasetsintheirevaluationoftheironlineHDPvariant.
The authors showed results for 352,549 Nature articles and 82,519 PNAS documents. Wang and
colleaguesnotethattraditionalHDPcanonlyberunonbatchesof20,000documentsduetotime
constraints.TheauthorschangetheexperimentsetupfromthatofonlineLDA,choosingtorun
eachmodelfor6hours,insteadofrunningmodelstoconvergenceorcompletion.Theyshowthat
onlineHDPproducesahigheraccuracyafter6hoursofsimulation.Likeintheexperimentsfor
onlineLDA,Wangetal.donotprovidemachinespecificationsfortheirexperiments.Assuming
allmodelswererunonthesamecalibermachine,onlineHDPoutperformsonlineLDAandbatch
HDPsignificantlyonthetwotestdatasets.
Whiletheseonlinealgorithmsareanimportantstepintheevolutionoftopicmodels,theyare
stilllimitedbythenumberofdocumentstheycanhandle.Inthemodernageofsocialmedia,where
millionsofdocumentsareproducedeveryhour,theseonlinemethodsmaynotbefastenough.
5 MODERNTOPICMODELS(2011–PRESENT)
Inthelast20years,thedocumentsthatweinputintotopicmodelshavechangedfarmoredras-
tically than the topic models themselves. At the turn of the century, we input scientific articles,
books,andnewspaperarticles.Now,weinputsocialmediapostsincludingtweets,blogposts,Red-
ditposts,andothershorttexts.Topicmodelingresearchhasevolvedtoaddresstheproblemsthat
arisewhenattemptingtoinfertopicsonthesenewtypesofdata.Thereareafewnewapproaches,
butmanyoftheoldmathematicalcomponentsfrom20yearsagoarestilltheacceptedbestprac-
tices.Ineachofthefollowingsubsections,thefirstmodelistheseminalmodelforthecategoryof
models,andweexplainitindepth,followedbydescriptionsofothermodelsinthecategory.
Figures2and3depictthebiggerdevelopmentsintopicmodeling’s30-yearhistory.Inthissec-
tion,wecoverthemostrecentdevelopmentsthathaveimpactedthefieldoftopicmodeling—the
applicationoftopicmodelstosocialmediadata,theinventionofWord2Vecandotherwordem-
beddingmodels,andtheincorporationofnovelnaturallanguageprocessingtechniquesintotopic
models.
5.1 Non-negativeMatrixFactorization
Non-negativematrixfactorization(NMF)isamathematicalprocessinwhichamatrixofnon-
negativevaluesisfactorizedintotwonewmatricessuchthattheproductofthetwonewmatrices
isequaltotheoriginal.Liketheinferenceofgenerativemodels,NMFisknowntobeNP-Hard[77].
Thetwo-factormatriceshaveamuchsmallerdimensionalitythantheoriginalmatrix.Inthecase
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:17
oftopicmodeling,thelargematrixisthedocument-wordmatrix.Inotherwords,thelargematrix
isthesetofdocuments,whereeachdocumentisrepresentedasavectorofwords.Thetwosmaller
matricesthatNMFfactorsthelargematrixintoarethetopic-wordmatrixandtopic-documentma-
trix.Thistopic-wordmatrixcanbeinterpretedasatopicdistributionoverwords,andtopicscan
be derived from it by choosing the highest-weighted words for each topic. Likewise, the topic-
documentmatrixcanbeinterpretedasatopicdistributionoverdocuments,andeachdocument’s
individualtopicdistributioncanbederivedfromthismatrix.Ak valuerepresentingthenumber
oftopicsdesiredbytheuserdecidesthefinaldimensionalityofthesmallermatrices.Ifthereare
DdocumentsandV wordsinthevocabulary,thelargematrixwillbeofsizeDxV,andthesmaller
matriceswillbeofsizekxV andDxk,respectively.Thesetupoftheproblemissimple,butsolving
itexactlyisintractable,soanapproximationalgorithmisused.NMFworksbyminimizinganerror
functionbetweentheoriginalmatrixandtheproductofthetwo-factormatrices.Non-negativema-
trixfactorizationhasbeenshowntobemathematicallyequivalenttopLSI(describedinSection3)
whenusingKL-divergenceastheerrorfunction[27].
In2006,Shahnazetal.demonstratedNMF’scapabilitiesasatopicmodel[69].Theauthorsuse
asparseencodingofthedocument-termmatrixtosavememoryandrunthealgorithmmoreef-
ficiently. The experiments consisted of two datasets, one with 21,578 Reuters news articles, and
theothercontaining7,919transcriptsfromdifferentnewssources.Theauthorslimittheirexperi-
mentstodocumentspre-labeledwithasingletopic.Inthefirstdataset,theaccuracyofthemodel
rangesfrom96%whentheylabeldocumentsusingonlytwotopicsto54%whenlabeling20topics.
Theseconddatasetrangesfrom99%accuracyat2topicsto80%at20topics.Theauthorsattribute
thedisparityinperformancetothebroadtopiclabelsintheReutersdataset.
In2011,Kasiviswanathanetal.publishedatemporalmodelthatusedNMFasitsbasis[36].While
NMFwasnotdesignedspecificallyforastreamingsetting,theauthorsusedNMFondocuments
in each epoch in order to produce sets of emerging topics. Emerging topics are temporal topics
thatarereceivingmoreattention,i.e.,rising.Theauthorstestedtheiralgorithmonasetof9,394
documents,andontheTwentyNewsgroupsdataset,consistingof18,774newsarticles.Insteadof
othertopicmodels,theauthorscomparedtheirmodelagainstclusteringalgorithms.Theauthors
orderthedocumentsnotbydatebutbypre-labeledtopicandintroducedocumentsinorderoftheir
clusters,withsomeoverlapineachepoch.Whilethemodelitselfisunsupervised,theorderingof
thedocumentsintheirexperimentsconstitutessomelevelofsupervision.Inmostsettings,data
are not generated in order of their pre-labeled topic. This potentially gives an unfair accuracy
advantagetothemodel.Aftertestingonthetwopre-labeleddatasets,theauthorsalsotesttheir
modelonasetof5,199tweetsabouttheperformanceofIBM’sWatsononJeopardy.Theauthors
ranthemodelon2weeks’worthoftweetsleadinguptotheairingoftheshow(8,434tweets)as
abaselineforfindingemergingtopics.
In 2013, Yan et al. took a new perspective of the NMF approach [89]. Instead of attempting
todetecttopicsusingadocument-termmatrix,theyemployatermcorrelationmatrixinorderto
detecttopicsinshorttexts.Theyarguethatwordco-occurrencewithindocumentsisnotadequate
fordetectingtopicsinshorttextsduetothelowfrequencyofwordswithinthesedocuments,and
thatthetruenatureoftopicsinthesetextscanbecapturedbyanalyzingthecorrelationbetween
wordsthemselves.Insteadofbuildingamatrixofdocumentswithwordcounts,theauthorsbuild
a matrix of words with positive pointwise mutual information scores (positive to maintain non-
negativefactorization).TheauthorsemployNMFonthismatrixinordertolearnthetopicsdirectly
fromwordcorrelationsratherthanfromdocumentcorrelations.Theauthorstesttheiralgorithm
onthreedatasetsconsistingof4,520tweets,2,630newsarticletitles,and36,219onlinequestions,
respectively. The authors compared their algorithm to LDA and other implementations of NMF
fortopicmodeling.Theauthorsevaluatetopicsetsbasedonpurity,normalizedPMI,andARI.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:18 R.ChurchillandL.Singh
NMF and its variants are a dimensionality reduction approach to topic modeling. In environ-
mentswherenoiseispervasive,dimensionalityreductionmethodsthatareabletoremovenoise
andextractfeaturesfromsparsehigh-dimensionalspacesmaybepromising.
5.2 Graph-basedModels
Recently,someworkhasfocusedonfindingtopicsusinggraph-basedapproaches.Whenbuilding
thegraph,wordsaregenerallynodesandtheirco-occurrenceisrepresentedasaweightededge.
Thebasicintuitionisthatwordsintightlyconnectedcommunitiesrepresenttopics.
An early implementation of a graph-based topic model is that of Cataldi et al. [13], a model
designed to detect emerging topics. In their model, the authors employ a directed graph, where
eachnodeisaword,andeachedgeisaweightedco-occurrenceoftwowords.Edgesaredirected
becausetheweightcanbedifferentineachdirection.Edgeweightingiscalculatedbasedonthe
co-occurrencefrequencyofawordpair,relativetothetotalfrequencyofthewordatthesourceof
theedge.Awordwithveryhighfrequencybutmanyco-occurringwordsislikelytohavelower
outgoingedgeweightsthanonewithalowerfrequencybutfewerco-occurringwords.
The graph is created for each time epoch in sequence, and the frequency of words in each
epochissavedforthefutureepochs.Oncethegraphhasbeencreated,alocalizededgepruningis
performed,removinglower-weightedges.Duetothenecessityofpruningedges,thisalgorithm
mustiteratethroughalledgesinthegraph.Thenumberofpossibleedgesis
|V|(|V|−1),where|V|is
2
thenumberofwordsinthevocabulary,sothecomplexityofthealgorithmisO(|V|2),althoughdue
tographsparsity,theruntimeisusuallymuchfaster.Topicsaredetectedonthisgraphbyrunning
a depth-first search (DFS) out from a set of “emerging terms.” To compute emerging terms in
each epoch, frequencies from previous epochs are compared to current frequencies. Words are
chosenasemergingtermsiffrequencyhasincreasedsignificantly.Fromeachtermreachedduring
theDFS,anewDFSisrun.IfaDFSreachestheoriginalemergingterm,thenthetermisaddedto
atopiccontainingtheemergingterm.Thisprocessalsoguaranteesthatnotwotopicswillinclude
the same term, resulting in zero topic overlap. This double-DFS approach to finding topics in a
directedgraphensuresthatanytwowordsincludedinthesametopicarestronglyconnectedto
eachother,atleastthroughsomechainofotherstronglyconnectedwords.
The authors show their results on a generic Twitter dataset containing more than 3 million
tweetsover2weeksin2010.Whiletheydonotcomparetheiraccuracytoothertopicmodels,they
showtopicsthatarerecoveredthroughoutthe2-weekperiod.Theirtopicsaresmall(fourwords
each),butthereisnoanalysisthatshowswhethertheapproachcapturesallemergingtopicsor
justahandfulofthebiggest.
In 2016, Arruda et al. designed a static topic model, topic segmentation (TS), based on an
undirectedgraphwithnounsandverbsasnodes,connectedbyco-occurrence[22].Theauthors
describethreedifferentwaystocomputeco-occurrence,basedonadjacencyofwords,paragraph
co-occurrence, and an approach that compares co-occurrences to a baseline frequency. The au-
thorsemploytheLouvainmodularityalgorithmtodetectcommunitiesofconnectedwordsintheir
graph[10].ThecomplexityofthemodularityalgorithmisO(nloдn).Givenasubsetofnodesina
graph,theLouvainmodularityalgorithmcomparesthenumberofinternaledges(betweennodes
in the subset) to the number of outgoing edges (between a node in the subset and a node not
inthesubset).Ahigher-than-expectedratioofinternaledgestooutgoingedgesindicatesahigh
modularityscore.Ahighmodularityscore,intheapproachdesignedbyArrudaetal.,indicatesa
probabletopicrepresentedinthegraph.Theauthorscreatedtheirowndataset,consistingof200
documentsbuiltfromparagraphsextractedfromWikipediaarticlesrevolvingaroundpre-chosen
topics.Theauthorscomparetheirapproachtoclusteringmethodsinsteadoftopicmodels.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:19
In2018,Churchilletal.[21]designedtheTopicFlowModel(TFM),withthegoalofreducing
noiseintopicsinatemporalsettingandtrackingtheevolutionoftopics.Theauthorsemployeda
similardirectedgraphstructureasCataldietal.[13].Forthesamereasonsas[13],thecomplexity
ofTFMisO(|V|2).Insteadofperformingalocaledgepruningmethod,theauthorsincludeanedge
onlyiftheweightmeetsaglobalthreshold.Thisresultsinfeweredgesinthegraph,whichallows
forfastermodeling.Theauthorsalsointroducethenotionofdomain-specificfloodwords.Flood
wordsarewordsthatappearindocumentsacrossadomainand,likestopwords,donotaddcontext
tothetopics.Forexample,ifweweretryingtounderstandCOVID-19-relevanttopics,“COVID-19”
wouldbeineverytopic,makingitafloodword.Toaccountforfloodwords,theauthorsintroduce
anupperboundforwordfrequencywhendetectingemergingterms.Athirdparametercaptures
theindividualchangeinfrequencyovertimeforpossibleemergingterms.WhileCatadietal.[13]
traversedthegraphusingaDFSinordertofindtopics,Churchilletal.[21]usedabreadth-first
search(BFS)andlimitedthedistanceofthesearch.Whilethismoreeffectivelyfiltersoutnoisier
emergingtermsfromtopics,moreparametersneedtobetuned.
Theauthorsusetheemergingtopicsdetectedateachtimeepochtotracktopicsthroughtime.
Inadditiontotheemergingtermsdetectedateachepoch,TFMseekstoconfirmthecontinuing
existence of previous topics. If a previous topic can be recovered in the current epoch, it is in-
cludedinitsnewstate.Inthismanner,theevolutionofatopiccanbetrackedfromemergenceto
disappearance.Intheirexperiments,theauthorsusedasmallsyntheticdatasetconsistingof500
documents randomly generated, consisting of seven topics and seven time periods, and varying
levels of flood words. The authors also tested their model at larger scale, using a set of 280,000
tweetsaboutthe2016U.S.presidentialelection,andasetof14,000newspaperarticlesaboutthe
sametopic.Precision,recall,andsignal-to-noiseratiowereusedtoevaluateTFM.Usingground-
truth-labeledtopics,TFMwasfoundtobebetteratdetectingtopicsinatemporalsettingthanthe
baselines.
In2020,ChurchillandSinghproposedanothergraph-basedtopicmodel,thePercolation-based
TopicModel(PTM)[18],fordetectingtopicsinnoisydatasets.Theirapproachconsistedofincre-
mentallystrippingnoiseawayfromthegraph,leavingsmalltopickernelscontaininglittletono
noise.ChurchillandSinghrelaxedthecliquepercolationproblem1 toallowforsubgraphs(topic
kernelsintheircase)tobegroupedtogether.Intheirexperiments,theauthorsusedlarge,domain-
specificTwitterdatasetsconsistingofmorethan750,000tweetsperdataset.Theauthorsusedtopic
diversityandtopiccoherence(NPMI)toevaluatethequantitativequalityoftheirmodels,showing
competitivescorestothebestmodels.Aqualitativeanalysiscomparestheirmodelstostate-of-the-
artmodelsintermsofinterpretabilityandnoise.Duetohavingtoiteratethroughalledgesineach
round of decomposition, with the possibility of having to perform |V| rounds of decomposition,
thecomplexityofPTMisO(|V|3),where|V|isthenumberofwordsinthevocabulary.
Graph-basedapproachesaddanewperspectivetotopicmodeling,takingadifferentdirection
fromtheearliergenerativemodels.Theydonotassumeknowledgeoftheunderlyingtopicdistri-
bution,sotheymorereadilyfindtopicsofvaryingsize.Insomesense,theycanbemoreadaptive
than generative models, allowing for either a global or local topic discovery. However, if flood
wordsarenotwellmanaged,thegraphstructurecanbeverycostlytotraverse.
5.3 MixingTraditionalTopicModelswithModernNLPMethods
In recent years, there has been a shift toward incorporating more sophisticatedNLP techniques
intotopicmodels.WhiletopicmodelscanbeviewedasNLPmodels,hereweconsiderhowother
1Cliquepercolationisawayofclusteringsize-kcliquesinagraph.Itconsistsofgroupingtwosize-kcliquesiftheyshare
k-1nodes.Thisprocessisrepeatedforallpairsofsize-kcliques.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:20 R.ChurchillandL.Singh
NLP models augment traditional topic models. In contrast to early models such as LDA, which
arestatisticalmodels,thesenewapproachesleveragepriorknowledgeofnaturallanguageinthe
form of other pre-trained NLP models in order to improve the coherence and accuracy of the
unsupervisedtopicmodel.Figure3outlinesafewofthemostnotablecontributionsdiscussedin
thissection.
ThemostpopularformofmodernNLPmodelthathasbeenincorporatedintotopicmodelsis
wordembeddingspaces.AsurveyofwordembeddingsbyAlmeidaandXexeo[2]givesanin-depth
accountoftheirdevelopment.Here,wefocusontheinceptionoflarge-scalewordembeddingsto
providecontextforthetopicmodelsthatfollow.In2003,Bengioetal.describedhowaneuralmodel
could be used to learn a distributed representation for words [5]. They named these distributed
representationswordfeaturevectors,whichhavecometobeknownaswordembeddings.In2013,
Mikolovetal.introducedamodelcalledWord2Vecforcreatingwordembeddingsthatwereboth
fast to compute and accurate [50]. They showed how their word vectors could be used to find
semanticallysimilarwords.Thissimplicitylendsanaturalhandtotopicmodels,whicharetasked
withfindinggroupsofsemanticallysimilarwordsthatrepresentatopic.
5.3.1 BitermTopicModel. InthesameyearthatMikolovandcolleaguesintroducedimproved
word embeddings [50], Yan et al. released the biterm topic model (BTM) [88]. Designed for
short texts such as tweets and other social media posts, the BTM attempts to model the word
co-occurrence patterns present in a dataset instead of document-level patterns. This approach
makessenseinthecontextofshorttextsbecausedocument-levelpatternsarehardertotrackin
documentsthatcontainonlyasmallnumberofwords.Theauthorsextractwordpairsthatoccur
inthesamedocumentandperforminferenceonthewordpairsinsteadofthedocuments.Biterms,
astheycallwordpairs,aregeneratedbasedonatopic-worddistribution.Theirgenerativeprocess
isdependentnotondocuments,butonthesebiterms.Toapproximatethebitermdistribution,the
authorsemployaGibbssamplingalgorithmnotunlikethatofLDAorDMM,whereeachbiterm
isgeneratedbysometopicwithsomeprobability.
YanandcolleaguesshowthatiterationsofBTMusingGibbssamplingtakesignificantlylonger
thanthoseofLDAsincethesetofbitermscanbesignificantlylargerthanthesetofdocuments.
Ontheotherhand,BTMrequireslessmemoryduetotheactualsizeofeachbitermcomparedto
thatofeachdocument.TheauthorsperformedexperimentsontheTweets2011collection,which
contains4.2milliontweetswithavocabularyof98,857words.Theyalsouseadatasetofquestions
fromBaidu,aChineseQ&Awebsite,containingover648,000questions.Theauthorsshowthaton
bothdatasets,theirmodeloutperformsLDAintermsofcoherenceandclassificationaccuracy.
5.3.2 Self-aggregatingTopicModel. In2015,Quanetal.introducedtheSelf-aggregatingTopic
Model(SATM)toattempttoimprovetopicmodelingonshorttexts[62].Theauthorsidentifythe
problemofshorttextslackingadequatewordco-occurrenceforuseintraditionaltopicmodelsand
attempttosolveitbyaggregatingshorttextsintolongertextsthatarebettersuitedforuseinLDA.
Intheirmodel,theauthorsemployatwo-stepprocess,runningLDAonthedatasetofshorttexts,
andusingtheoutputtopicstoprobabilisticallygeneratelongerpseudo-texts.Apseudo-textisan
aggregation of shorter documents into a single longer document for the purposes of increasing
wordco-occurrence.Forinstance,twosimilardocuments,“MedicalFacts:Coronavirusmakesyour
teethfallout”and“MedicalFacts:Coronavirusisthenumberonecauseofcavitiesandrootcanals”
couldbecombinedintoapseudo-text“MedicalFacts:CoronavirusmakesyourteethfalloutMedical
Facts:Coronavirusisthenumberonecauseofcavitiesandrootcanals.”2Thesepseudo-textsareused
2These“facts”arenottrue.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:21
togenerateshorttextsnippetsthatrepresenttopics,suchthateachsnippetisgeneratedaccording
toonepseudo-text.Thesetextsnippetsarethenoutputastopics.
Theauthorstesttheirmodelon1,740NIPSpapersand88,120questionsfromYahooAnswers.
TheyuseaPMIscoretoevaluatethecoherenceoftheirmodelcomparedtoasetofhand-labeled,
goldstandardtopicsforeachdataset.SATMachievesahigherpurityscorethanLDA,DMM,and
BTM,butnocomparisonintermsofcoherencebetweenSATMandthebaselinesisoffered.
5.3.3 LatentFeatureLDAandLatentFeatureDMM. In2015,Nguyenetal.[56]proposedusing
word embedding spaces (latent features) in conjunction with traditional topic models LDA and
DMM.Theyreplacethetopic-worddistributionofLDAandDMMwithatwo-componentmixture
ofatopic-worddistributionandalatentfeaturecomponent.WhatthismeansisthatLF-LDAand
LF-DMMretainthestructureoftheirtraditionalcounterparts,whileaddinglatentfeaturevectors
foreachwordinthedistribution.Ingeneratingawordforadocument,thewordischoseneither
fromthedrawntopicorfromthelatentfeaturevectorofthetopic,inessenceexpandingthepool
ofwordstobechosenbyallowingwordssimilartothetopicinthelatentfeaturespacetobeadded
aswell.Becauseoftheaddedlatentfeaturespace,theauthorsexpecttheirmodelstoperformwell
ondatasetswherethereislittledataabouttopic-worddistributions,i.e.,shorttexts.
The authors test their model on different variants of the Twenty Newsgroups dataset [41]
containing 18,820 documents (variants contained 1,794 and 400 documents, respectively), the
TagMyNewsdataset[80]containing32,597documents,andaTwittercorpuscontaining2,520doc-
uments.TheyuseNPMItoevaluatethequalityoftheirmodelsusingWord2Vec[50]andGloVe[58]
asthelatentfeaturespaces.TheyshowthatatleastoneoftheirmodelsbeatvanillaLDAinterms
of NPMI and purity on each dataset. A qualitative analysis shows how their model successfully
groupstogethertopicsoveriterations.
5.3.4 NeuralVariationalDocumentModel. Whilenottechnicallydesignedtobeatopicmodel,
Miaoetal.createdtheNeuralVariationalDocumentModel(NVDM)in2016tomodeldocu-
ments[49].ThegoalofNVDMistocreatea“continuoussemanticlatentvariableforeachdocu-
ment.”TheNVDMisanunsupervisedgenerativemodelthatusesaneuralnetworktoperforma
multinomial logisticregressiononthedocumentset,resultinginwhatisessentiallyawordem-
beddingvectorforeachdocument.TheauthorstestedtheirmodelagainstLDAandotherneural
documentclassifiersontheTwentyNewsgroupsdatasetandasetofReutersnewspaperarticles
consistingof804,414articles.Theauthorsuseperplexityastheironlyevaluationmetricfortopic
qualityandshowthattheperplexityoftheirmodelislowerthanthatofthebaselinemodels.
5.3.5 lda2vec. In2016,Moodycreatedamodelcalledlda2vec,withthegoalofdirectlyincorpo-
ratingtheWord2VecmodelintotheclassicLDAmodel[51].lda2vecalterstheWord2Vecmodel
tocreatedocumentvectorsaswellaswordvectors.Documentvectorsallowthemeasurementof
similaritybetweendocuments,andbetweendocumentsandwordsorphrases.Eachtopicisavec-
torinthesamespaceasthewordanddocumentvectors,calculatedbysummingtheprobability
of each document belonging to that topic. The resulting topic vector can be compared to word
vectors to find the most similar words to the topic. The author shows that this approach works
wellonHackerNewscomments,containing66,000shorttexts,aswellastheTwentyNewsgroup
dataset,containing11,313documents.Moodydoesnotofferanycomparisonofthemodeltoother
state-of-the-arttopicmodels,insteadoptingtoshowexampletopicsdiscoveredbylda2veconeach
dataset.
5.3.6 Pseudo-document-based Topic Model (PTM). In 2016, Zuo et al. proposed the Pseudo-
document-based Topic Model (PTM) [97] as an improvement on the Self-Aggregating Topic
Model[62].PTMassumesthatshorttextsaregeneratedfromlongerpseudo-documents.Foreach
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:22 R.ChurchillandL.Singh
shorttextobserved,alatentpseudo-textisdrawnfromthedistributionofpseudo-documents.A
topic is then drawn from the topic distribution of the pseudo-text as opposed to the short text,
andthattopicisusedtogeneratethenextwordintheshorttext.Theauthors’hypothesisisthat
by condensing many short texts into a single pseudo-document, the word co-occurrence matrix
is condensed, leading to a more accurate approximation of topics. The authors claim that their
generativeprocessissignificantlyfasterthanthetwo-stepprocessofSATMowingtothefactthat
theirprocessisasinglestepinwhichasinglepseudo-documentisusedtogenerateadocument.
The authors also propose a variant of their model, SPTM, to account for sparsity by adding the
“SpikeandSlab”prior[31]tothetopicdistributionofpseudo-documents.
The authors test their model on four datasets: a news dataset consisting of 29,200 articles, a
DBLPdatasetconsistingof55,290researchpapertitlesfromsixresearchareas,aquestionsdataset
consistingof142,690questionsfromaChinesequestion-and-answerwebsite,andaTwitterdataset
consistingof182,671tweetslabeledwithcategories.Theauthorsuseprecision,recall,andf-score
to evaluate their models, as well as a PMI-based coherence score. The authors perform a short
qualitativeanalysisofPTMonDBLP,showinghowthemostprobabletopicsinapseudo-topiccan
beexplainedbythecontentofthepseudo-topic.TheauthorsshowthatPTMorSPTMoutperforms
LDA,SATM,andotherbaselinemodelsonalldatasetsexceptforTwitter.
5.3.7 Embedding-based Topic Model. In 2016, Qiang et al. introduced an embedding-based
topicmodel(ETM)forperformingtopicmodelingonshorttextswiththehelpofwordembedding
vectors [60]. Using the Word2Vec framework created by Mikolov et al. [50], the authors create
a new distance metric, called the Word Mover’s Distance (WMD), to measure the difference
betweendocumentsgiventhewordembeddingvectorsoftheircomponentwords.TheWMD,an
adaptation of the Earth Mover’s Distance, computes the minimum distance between each word
inonedocumenttoitsclosestneighborintheotherdocument.TheauthorscomputetheWMD
betweendocumentsandthenaggregateshortdocumentsintolongerpseudo-textsusingK-means
clustering,withtheWMDasthedistancemetric.TheauthorsrunLDAonthepseudo-textstoget
topicassignmentsforeachpseudo-textandwordinthevocabulary.TheycreateaMarkovRandom
Field (manifested as an undirected graph), and for each pair of words with a sufficiently small
WMD,theycreateanedgeinthegraphbetweenthetwowordnodes,representingtheirshared
topicassignment.Then,foreachpseudo-text,thereisanundirectedgraphconsistingofthenodes
referringtothewordsinthepseudo-text.Wordsaredrawnfromamultinomialdistributiongiven
theirWMDandpseudo-text.Asaresult,similarwordsthatappearinthesamepseudo-textwill
haveahighprobabilityofbeingplacedinthesametopic,whilesimilarwordsthatdonotappear
inthesamepseudo-textwillnot.
The authors tested their model against multiple state-of-the-art models on two datasets, con-
sisting of 16 million tweets and 6,974 news articles, respectively. They find that their approach
improves on the coherence of other models. While the example topics that the authors display
showlessnoisethanothermodels,theircomparisonisonasmallsetofonlyfourtopics.
5.3.8 GibbsSamplingDMM. In2014,inanefforttomoreeffectivelymodeltopicsonshorttext,
YinandWang[94]revivedtheDMMcreatednearly15yearsearlierbyNigametal.[57].Yinand
WangalteredtheoriginalDMMbyproposingaGibbssamplingalgorithmthatimprovedonthe
scalabilityofDMM.DMMnaturallylendsitselftomodelingshorttextsbecauseofitsassumption
that every document is generated from a single topic. In short texts such as social media, there
isoftennotenoughspacetoreferencemultipletopicseffectively,soamodelsuchasLDAmight
endupconvergingtoapointwhereitfindsthatmostdocumentsaregeneratedinlargepartbya
singletopicorerroneouslyfindsthatdocumentsaregeneratedbymanytopics,leadingtonoisy
and inaccurate topics. Yin and Wang perform experiments on DMM using 11,109 news articles
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:23
from Google News, as well as 2,472 pre-labeled tweets from TREC. The authors compare their
modeltoclusteringalgorithmsinsteadoftopicmodels.Despitethesmallchangetotheoriginal
model,thisnewlookatanoldmodelpavedthewayforothermoreadvancedvariantsofDMM.
5.3.9 GPUDMMandGPUPDMM. In2016,Lietal.introducedGeneralizedPolyaUrnDirich-
letMultinomialMixture(GPUDMM),anothertopicmodelthatincorporatedwordembeddings
into a classic model, although in a completely different manner than Moody [42]. GPUDMM at-
temptstobringtogethersemanticallyrelatedwordsintothesametopicusingtheGPUmodel.In
the Gibbs sampling model, when a word is sampled, it is added back to the chosen topic. In the
GPU model, when a word is sampled, a copy of similar words as well as the original word are
added back to the chosen topic. This results in groups of similar words all being pushed to the
topofatopictogether,producingtopicsthatcontainmorecoherentsetsofwords.Thesimilarity
of words in the GPU model is decided by their word embedding distance. So, in comparison to
lda2vec,whichreliescompletelyontheWord2Vecembeddingmodeltocreatetopics,GPUDMM
augmentsthetraditionalDMMmodelwithbetterwordsbasedonthewordvectorsimilarities.In
terms of the DMM part of the model, the authors borrow directly from Yin et al.’s GSDMM. To
incorporatetheGPUmodelintoDMM,theauthorsemployaprobabilisticsamplingstrategyinan
attempttoonlyreinforcethosewordsthatareverysimilartothesampledtopic.
To account for the possibility of documents being generated by more than a single topic, the
authorsalsointroducetheGPUPDMMmodel.ThisvariantofGPUDMMreplacestheDMMwitha
Poisson-basedDMM,whichallowsforoneormoretopicstogenerateadocument.Thedifference
betweenPDMMandLDAisthatPDMMlimitsthenumberoftopicsthatcangenerateadocument
based on a Poisson distribution, whereas LDA allows for all topics to contribute to generation
with some probability. Aside from the difference in the number of topics allowed to generate a
document,GPUDMMandGPUPDMMareidentical.
Li and colleagues show results for two different short text datasets, with 12,265 and 179,042
documents,respectively.Intheirexperiments,theyshowthattheirtopicsaremorecoherentthan
thosegeneratedbyDMMandotherstate-of-the-artmodelsthatincorporatewordembeddings.
5.3.10 Distributed Representation-based Expansion (DREx). In 2017, Bicalho et al. proposed a
frameworkforexpandingshorttextsusingwordembeddings[6].Givenawordembeddingspace
andadocument,thedocumentcanbeexpandedbyfindingtheclosestngramsintheembedding
spacetoeachngramcontainedinthedocument.Foreachcandidatengram,ifitissufficientlyclose
tothengraminthedocument,thecandidatewordisaddedtothedocument.Thisprocessstops
whennocandidatewordsremain,orwhenthedocumentsizelimitisreached(60inthearticle).
Theauthorstesttheirframeworkonsevenshorttextdatasets,includingfourTwitterdatasets,
two news datasets, and one web search snippet dataset, ranging in size from 1,001 documents
to 70,707 documents. They show that by expanding using Distributed Representation-based
Expansion(DREx),documentscanincreaseinsizefromsingledigitstobetween20and60words
(becausethelimitis60).TheauthorsuseNPMI,precision,andrecalltocomparetheperformance
ofmodelswithandwithoutDREx,andfindthatDRExwithGloVe[58]wordembeddingsperforms
bestthroughoutalldatasets.TestingDRExwithLDA[9],LF-LDA[56],andBTM[88],theauthors
showthatDREximprovesallresults.
5.3.11 CommonSemanticsTopicModel. In2018,Lietal.proposedtheCommonSemantics
TopicModel(CSTM)[44]tofilternoisefromtopicsinsocialmediadatasets.BasedonDMM[57]
(whattheauthorscallmixtureofunigramsmodel),theauthorsadd“commontopics”tothemix.
Adocumentcanbegeneratedfromasingle“functiontopic”(atraditionaltopic)andfromtheset
of common topics. Common topics are designed to capture words that appear across all topics.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:24 R.ChurchillandL.Singh
Givenk topics,C aredefinedtobecommontopics,andK arefunctiontopics.Foreachdocument,
afunctiontopicz issampledfromK,andthenforeachword,atopicisdrawnfromthemixture
d
ofC∪z andthewordisdrawnfromthechosentopic.
d
Theauthorstesttheirmodelsonthreedatasets,oneconsistingof12,340websearchsnippets,
one consisting of 179,022 questions from a Chinese Q&A website, and the final consisting of
2,000,000tweets.TheytestedagainstbaselinemodelsincludingSATM[62],BTM[88],DMM[57],
and DREx+LDA [6]. A qualitative analysis of the tweets dataset shows the identified common
wordsgroupedintothecommontopics.CSTMproducesmorecoherenttopicsthanthebaseline
models (based on NPMI) and performs competitively on classification accuracy and purity. The
authors also show the effect of changing the number of common topics on coherence for each
dataset. The coherence of topics increases up to about five common topics and decreases as the
numberofcommontopicsincreasesfurther.
5.3.12 Word Embedding LDA. In 2018, Bunk and Krestel proposed a model called WELDA, a
combination of word embeddings (WEs) and LDA [12]. In their paper, Bunk and Krestel find
thatwordembeddingsandtopicmodelsdonothaveahighnaturalcorrelationintermsofwhich
wordstheyfindtobesimilar.Theyfindthatintermsofjudgingwordsimilarity,wordembeddings
arefarsuperiortoLDA.Withthisinmind,theysetouttocombinewordembeddingswithLDA
inordertocreateamorecoherenttopicmodel.
Theauthorsuseapre-trainedembeddingmodelastheirembeddingspaceandperformaslightly
alteredversionofLDA’sgenerativealgorithmtofindtopics.Insteadofjustbeinggiventhetopic-
worddistributionsforeachtopic,anembeddedtopicdistributionisgivenaswell.Theembedded
topicdistributionisasetofwordsthatareclosestintheembeddingspacetothetopwordsofa
giventopic.Usingthisembeddingspace,foreachobservedwordinadocument,acoinisflipped
withsomesuccessprobabilityλ.Ifthiscoinflipissuccessful,thentheobservedwordisreplacedin
thedocumentwiththenearestneighbortotheobservedwordintheembeddedtopicdistribution.
Thereplacedwordissampledinsteadoftheactualobservedword.Thisresultsinthetopwordsfor
eachtopicmovingclosertogetherintheembeddingspace,helpingtopicsbecomemorecoherent.
Fortheirexperiments,theauthorstestedontheTwentyNewsgroupsdatasetandNIPSdataset,
which contain 11,295 and 1,740 documents, respectively. The authors note the small size of the
datasetsbutmentionthatotherattemptsatwordembeddingtopicmodelsstillstruggletoprocess
thesedatasets.TheauthorsuseC asdefinedbyRöderetal.[64]andwordintrusionasdefinedby
V
Changetal.[14].TheauthorsfoundthatthewordintrusionscoresforWELDAwerehigherthan
LDAandslightlyhigherthanorcomparabletootherbaselinemodelsthatusedwordembeddings.
TheauthorsalsofoundthatthecoherenceofWELDAwasmuchbetterthanLDAandbetterthan
orcomparabletootherbaselinemodels.
5.3.13 LaplacianDMM. In2019,Lietal.adaptedDMMtobettersuitshorttexts,andproposed
LaplacianDMM(LapDMM)[45].Whiletheynotethattheassumptionofonetopicperdocument
alreadysuitsDMMtoshorttexts,theyincorporatevariationalmanifoldregularizationinorderto
preservethelocalneighborhoodstructureofshorttexts.Manifoldregularizationinthecontextof
topicmodelingaddstheconstraintthattopicrepresentationsofdocumentpairsshouldbesimilar
to each other if they are nearest neighbors in document manifolds. In order to find the nearest
neighbors of documents, a graph is constructed prior to training LapDMM that measures docu-
mentdistances.TheLaplacianmatrixofthegraphcanthenbeusedasaconstraintonthetopic
assignmentofdocuments,toensurethatdocumentsassignedtothesametopichavewordsinsim-
ilarneighborhoodsinthegraph.Theauthorsusewordembeddings(specificallyWord2Vec[50])
and the Word Mover’s Distance [39] to compute the distance between documents. Using word
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:25
embeddingsinsteadofdirecttermdistancesallowsonetocomparedocumentswithnowordsin
common.
The authors test their model variants against DMM [94], GPU-DMM [42], BTM [88], and an
aggregationmodelsimilartoSATM[62].Theyusethreedatasets,aTRECquestiondatasetconsist-
ingof5,952documents,awebsearchsnippetsdatasetconsistingof12,340documents,andaStack
Overflowdatasetconsistingof20,000questiontitles.UsingNPMIandaccuracy(thetopicofeach
documentwaslabeled),theauthorsshowedthattheirmodelperformedbetterorcompetitivelyon
alldatasets.TheyalsoshowedthatLapDMMwasmoreaccurateinclassifyingdocumentsoneach
dataset. The authors note that the construction of the document graph can be time-consuming,
especiallyforlargedatasets.
5.3.14 CluWords and CluHTM. In 2019, Viegas et al. proposed a topic model that leveraged
clustersofwordsandTF-IDFtogeneratetopics[78].Themodelrevolvesaroundthenotionofa
CluWord,whichisaclusterofwordsgivenanembeddingspace.WordsbelongtothesameClu-
Word if their cosine similarity in the embedding space is greater than some threshold α. Once
CluWordsforeachwordinthevocabularyhavebeencomputed,eachwordineachdocumentis
replaced by its CluWord. The TF-IDF of the CluWords is then computed to filter out very com-
mon and rare CluWords. The authors use CluWord representations of documents with NMF to
produce a topic set. The authors test their model on 12 small datasets (909 to 22,384 documents
each), against a number of baseline models including LDA [9], BTM [88], GPUDMM [42], and
ETM[60],andfindthattheirmodel’scoherenceoutperformsthebaselines.
In2020,Viegasetal.proposedamodelbasedonCluWordsandNMFcalledCluHTMtoperform
hierarchicaltopicmodeling[79].ThemodelisinitializedinthesamemannerasCluWords[78],
but once the initial set of topics is approximated, instead of finding CluWords and performing
modelingontheentiredataset,itrecursivelyfocusesonlyonthedocumentsbelongingtoasingle
topicatatime.Thisrepeatedprocessresultsinahierarchyoftopicswhereeachsetoftopicsone
rungdowncorrespondstooneoftheoriginaltopicsandsoon.TheauthorstestCluHTMonthe
samedatasetsasintheCluWordspaper,thistimetestingagainstotherhierarchicalmodels.They
findthatinmostdatasets,CluHTMoutperformstheothermodelsintermsofcoherence.
5.3.15 EmbeddedTopicModelandDynamicEmbeddedTopicModel. In2019,Diengetal.intro-
duced another version of a topic model assisted by word embeddings [25]. In their model, also
namedETM,wordsandtopicsarebothrepresentedbyavectorinanembeddingspace.Because
topicsandwordsareprojectedontothesameembeddingspace,wordscanbeplacedintotopics
probabilisticallybasedonhowcloseawordvectoristothetopicvector.Thegenerativeprocess
describedissimilartothatofLDA,whereforeachdocument,atopicisdrawnaccordingtoaprob-
abilitydistribution.InthecaseofLDA,thatdistributionistheDirichlet.InthecaseofETM,that
distributionisthelogistic-normal distribution,inordertofacilitateeasierreparameterizationin
theinferencealgorithm.Then,foreachword,atopicassignmentisdrawn.Finally,theobserved
wordisdrawn,inembeddingform,fromtheassignedtopic.Inthisway,thewordsaredrawnfrom
theircontext(theembeddings),insteadoffromthewordsthatareclosetotheminthegivendocu-
ment.TheETMmodelisfitusinganeuralnetworkwiththegoalofmaximizingthelogmarginal
likelihoodofobserveddocuments.
ETMcanbeusedwithorwithoutpretrainedembeddings,andinthecaseofpretrainedembed-
dings,itwillassignwordsintheembeddingspacetotopicseveniftheydonotoccurinthecorpus.
Thiscouldbeparticularlyusefulinsparsedatasetslikedomain-specificTwitterdata,wherethere
isalimitedvocabularyandlittlewordco-occurrencereinforcement.
The authors compare their model to LDA and NVDM. They test their model on the Twenty
Newsgroupdatasetandadatasetofover1.8millionnewsarticlesfromtheNewYorkTimes.They
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:26 R.ChurchillandL.Singh
useahybridevaluationmetric,topicquality,whichisthenormalizedproductofthetopiccoher-
ence(normalizedPMI)andtopicdiversity.TheauthorsfindthatETMwithpretrainedembeddings
performedbestonTwentyNewsgroups,consistentlyoutperformingothermethods.OntheNew
YorkTimesdataset,othermodelscatchuptoit,withamuchcloserspreadintermsofinterpretabil-
ityandpredictivepower.However,itstilloutperformstheothermodels.Theauthorsalsoshow
thatETMisrobusttostopwords.Ifstopwordsareleftinthedocuments,itfindsafewstopword
topics,butstopwordsdonotinfiltrateothertopicsasisthecasewithmanyothertopicmodels.
Alsoin2019,Diengetal.designedtheDynamicEmbeddedTopicModel(D-ETM)fortempo-
raltopicmodelingassistedbywordembeddings[26].AvariantoftheETMthattheyfirstdesigned,
D-ETMaddsatime-varyingaspecttothemodel.Thedifferenceinthemodel’sgenerativeprocess
isthatthegenerationisrunforeachtimestep,suchthattherearektopicsineachtimestep,stillall
projectedontoanembeddingspace.Wordembeddingsarenottimedependentinthismodel,soit
ispossiblethattopicsfromanearliertimestepcouldpickupwordsthatappearonlyindocuments
in later time steps. This helps for continuity of topicsthrough time steps but may be a problem
whenjudgingtheaccuracyofatopicatagiventime.
The authors test their model on three temporal datasets, including ACL abstracts (8,936 doc-
uments), articles from the journal Science (13,894 documents), and United Nations (UN) general
debates (196,290 documents). They tested against two dynamic versions of LDA (D-LDA and D-
LDA-REP).Theauthorsusetopiccoherence,topicdiversity,andtopicqualityandfindthatinthe
UNandSciencedatasets,D-ETMbeatsD-LDAontopicdiversityandqualitybutlosesintermsof
coherence.Inthesmallestdataset,ACL,D-ETMperformsthebestacrossallmetrics.Theauthors
alsofindthatD-ETMbeatsD-LDAontwoofthreedatasetsintermsofperplexity.
5.3.16 Topic Modeling with BERT. In 2020, Thompson and Mimno [76] proposed using the
language model BERT [24] to produce topics. The authors use k-means to cluster tokens ob-
served in the dataset based on their contextual vectors drawn from BERT. BERT is a language
modeloriginallyproposedin2018thatisacontextualwordembeddingspace.Itisabidirectional
model,meaningthatitswordembeddingsconsiderboththeleft-andright-sidecontext[24].This
differs from previous models such as GloVe and Word2Vec, which are context-free embedding
spaceswithasingleembeddingrepresentationforeachword.Itexcelsacrosstheboardontradi-
tionalNLPtasks.Theauthorsproposedifferentmodelvariantsbasedondifferentvariantsofthe
BERTmodel.Intheirexperiments,theauthorsemploythreedatasets,includinga1,000-document
Wikipedia dataset, a 5,300-document dataset consisting of U.S. Supreme Court opinions, and a
25,000-documentdatasetconsistingofAmazonproductreviews.Theauthorstesttheirmodelvari-
antsagainstLDAusingPMI-basedtopiccoherenceanddiversity(whichtheycallexclusivity).The
authors show that for any given metric, at least one of their model variants outperforms LDA;
however,nomodelconsistentlyoutperformsLDAoneverymetric.Inaqualitativeanalysis,the
authorsshowhowtheirmodelsaremoresyntacticallyawareintheirclusteringsthanLDA.
5.3.17 Topic-NoiseModels. In2021,ChurchillandSinghproposedanewtypeoftopicmodel,
topic-noise models, that jointly approximates topic and noise distributions [20]. Their model,
Topic-NoiseDiscriminator(TND),usesaBetadistributiontodecidewhetheranobservedword
belongs in a topic or in the noise distribution. If a word is determined to be a noise word, TND
samplesthenearestwordsinanembeddingspaceandaddsthemtothenoisedistributionaswell.
Thisfortifiesthenoisedistribution,resultinginstrongerandmoreaccuratenoisefiltering.Theau-
thorscombineTNDandLDAtocreateNoiselessLDA(NLDA),anensembledtopic-noisemodel.
NLDA uses the noise distribution of TND and the topic distribution of LDA to generate topics,
againusingtheBetadistributiontodeterminewhetherawordisnoiseoratopicword.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:27
TheauthorstestTNDandNLDAontheTwentyNewsgroupsdataset[41],aswellasadataset
containing 1 million tweets about the Covid-19 pandemic and a dataset containing 1.4 million
tweetsaboutthe2020U.S.elections.ComparingtoLDA,DMM,GPUDMM,andCSTMusingtopic
coherence,diversity,andnoisepenetrationmetrics,theauthorsshowthatNLDAperformsbetter
on social media data, especially in terms of coherence. The authors also conduct a qualitative
analysisthatshowstheinterpretabilityoftopicsgeneratedbytopic-noisemodelsusingexample
topicsandhumanjudgments.
NLP-aided topic models have evolved in the past 8 years, mostly due to the innovation of
Word2Vec in 2013. The best of these models incorporate word embeddings in some smart way,
nottowhollyreplaceclassictopicmodelframeworks,buttohelpreducethesparsityoftheword
co-occurrencespace.Wordembeddingsanddeep-learninglanguagemodelslikeBERTarenotsuit-
abletotopicmodelingthemselves,duetotheirdifferenceinobjectivefromtopicmodels.Instead
oftryingtoproduceasetofwordsrelatedtoatopic,wordembeddingsattempttoclusterwords
basedontheircontextualsimilarities.LanguagemodelslikeBERTaretrainedtoproducecoher-
entsentencesandsyntax,whichisnotrequiredintopicsandcansometimesleadtolesscoherent
topics.Despitetheirdifferenceinobjectivefromtopicmodels,thesemodelshavebeenshownto
beusefulfortopicaugmentation.AsshownbyDiengetal.in2019andbyChurchillandSinghin
2021,thesemodelscontinuetogetmoreaccurate,andtheevaluationmetricscontinuetoevolve,
honinginonimportantaspectsoftopicmodelsindifferentscenarios.
5.4 Meta-dataAugmented,Supervised,andReinforcement-Learning-basedModels
Whilethescopeofthissurveyisfocusedspecificallyonunsupervisedtopicmodels,wedescribea
fewseminalworksformeta-dataaugmented,supervised,andreinforcement-learning-basedtopic
models that have begun to appear in recent years. This section is not exhaustive, but rather an
introductionintothemainapproachesintheseareas.
In2011,Zhaoetal.proposedTwitter-LDA[95]asameansofproducingbettertopicsonTwitter
data. Their model worked by aggregating tweets into larger documents by user. These pseudo-
documentsarethenfedintoanLDA-basedmodelthatassumesadifferenttopicdistributionfor
eachuser.ThisapproachhasshownpromisingqualityonTwitterdata,butitrequiresmeta-data
(namely,theuserwhosenteachtweet).Italsorequirestheabilitytogobackandrecovertheentire
tweetsetofeachuserinthedataset,whichcanbeimpracticalforlargerdatasets.In2014,Sasakiet
al.proposedahybridmodelofTwitter-LDA[95]andTopicTrackingModel(TTM)[32]called
Twitter-TTM[67].ItessentiallyinsertedTwitter-LDA’sgenerativemodelintotheTTMtemporal
frameworktoproduceatemporalmodelthatworkswellonTwitterdata,giventhemeta-dataand
extrausertweetsetsrequiredbyTwitter-LDA.TheauthorsshowthatTwitter-TTMismuchbetter
ontheirTwitterdatasetthanLDA,Twitter-LDA,andTTMintermsofperplexity.
Themaindifferencebetweensupervisedandunsupervisedmodelsisthattheformerrelieson
documentspre-labeledwithtopics,orpre-labeledtopics,inordertodetecttopicsandlabelunseen
documents.Asaresult,supervisedtopicmodelsarelesspopularbecauseoftherelianceonlabeled
data,whichistime-consumingtocreateanddifficulttofind.
AnearlysupervisedtopicmodelisMDK-LDA[17].Ituseduser-definedsetsofrelatedwords
drawnfromtopicsinotherdomainsinordertogeneratetopicsonanewdataset.Eachtopicisa
mixtureofthesepre-definedsetsofwords,anddocumentsaredrawnfromtopics,aswellasthe
mostrelatedwordsinthevocabularytothosetopics.AsupervisedHierarchicalTopicModelingap-
proachusessupervisionintheformofalabeledtopichierarchytoallowforamoreaccuratehierar-
chicaltopicstructure[47](thisapproachusesagraphstructureasopposedtoneuralnetworks).In
2019,theAdversarial-neuralTopicModel(ATM)[85]usedagenerativeadversarialnetwork
(GAN)toapproximatetopicsthroughreinforcementlearning.ATMtranslateseachdocumentinto
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:28 R.ChurchillandL.Singh
TF-IDFvectorsandaskstheGANtoapproximateDirichletpriorssuchthatitcanrecreatethedoc-
ument with high accuracy. GANs are neural networks that contain a generator neural network
andadiscriminatorneuralnetwork.Thegeneratoristaskedwithcreatinganacceptablefakever-
sionof the documentand presentedwith both thetrueand fakedocument; thediscriminator is
tasked with guessing which is the fake document. The authors believe that the GAN can learn
whicharethemostimportantwordsinthedatasetandlearnpatternsintheirappearanceinsimi-
lardocuments.TheauthorstestATMonadatasetcontainingjustunder100,000NewYorkTimes
articles,anencyclopediadatasetcontaining29,762documents,andaneventsdatasetcontaining
20,199newsarticlesfromMay2014.Theauthorsusecoherenceandaqualitativeanalysistoshow
thatATMoutperformsLDAandotherbaselinesinthesedatasets.
In2020,anotherreinforcementlearningalgorithm,BidirectionalAdversarialTopicModel
(BAT) [84], was proposed to build on ATM. Instead of just the generator network and discrimi-
natornetwork,athirdcomponentoftheframeworkwasadded:theencoder.Theencodertakesa
V-dimensionaldocumentrepresentation(whereVisthesizeofthedocument)andconvertsitto
aK-dimensionaltopicdistribution(whereKisthenumberoftopics).Now,insteadofjusthaving
toverifythatthedocumentissimilartotherealdocument,thediscriminatoristaskedwithevalu-
atingthepairofthegenerateddocumentanditssimultaneouslygeneratedtopicdistribution.The
datasetsthattheytestonarerelativelysmallanddonotcontainshorttexts,buttheircoherence
resultsonthosedatasetsarestrong.
In 2021, Gui et al. introduced another neural topic model with reinforcement learning [28]
(VTMRL).Thisnewmodelleveragestopiccoherencewithinthemodelitself,usingthecoherence
scoreandwhattheauthorscalltopicoverlap(similartotheinverseoftopicdiversity)asthereward
forreinforcementlearning.Atopicwithhighcoherenceandlowtopicoverlapwillbereinforced
asagoodtopic,whiletheoppositewillbepunishedwithalowreward.Thisineffectallowsthe
modeltooptimizefortopiccoherenceanddiversity.TheauthorstestontheTwentyNewsgroups
andaNIPSdataset.Alsoin2021,Zhaoetal.introducedanotherneuraltopicmodelthatincorpo-
rateswordembeddingvectorsandentityvectorsintothemodel[96](VAETM).Wordvectorshave
beenincorporatedinbothneuralandunsupervisedtopicmodels.However,theinclusionofentity
vectors(whichmapawordtoasetofknownentitiesthatrepresenttopics,concepts,orobjects)
alongwithwordvectorsisanotherexampleoftheaddedvalueofmeta-dataandoutsideknowledge
basesforgeneratingtopicmodels.TheauthorstestontheTwentyNewsgroupsdataset,aswellas
twootherdatasets(25,000and96,000documents,respectively).WhilebothVTMRLandVAETM
testondatasetsthatarenotshorttextsorsocialmediadata,theirapproachesshowatrendtoward
incorporating outside knowledge like known entity vectors and improving topic generation by
employingNLPtechniquesandmodelsthathavebeensuccessfulforotherlearningtasks.
5.5 Model-agnosticImprovementstoTopicModeling
Whileourfocushasbeenonimprovementstotopicmodelingalgorithmsinparticular,wepause
tomentionthatthereareotherimportantdevelopmentswithregardtotopicmodelingmoregen-
erallythatcansignificantlyimpacttheperformanceoftopicmodels. Therehasbeensignificant
effortinunderstandingtheeffectsoftextpreprocessingontopicmodelingperformance.Schofield
etal.analyzedtheeffectsontopicsofremovingstopwords,findingasignficantimprovementin
LDA’sperformancewhenstopwordswereremoved[68].ChurchillandSinghcreatedapreprocess-
ingpipeline(textPrep)designedfortopicmodelinginanefforttostandardizepreprocessingand
provideasinglewaytoaccessbothbasicandmoresophisticatedpreprocessingmethods[19].
Therehavebeenconcertedeffortstowardmakingcurrenttopicmodelsmoreefficient.MALLET
LDA[48]wasoriginallyimplementedbyMcCallumin2002buthassincebeenmaintained,opti-
mized,andparallelizedbyDavidMimnoandmanyothers.SmolaandNarayanamurthyproposed
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:29
Fig.5. Anexampleofthevarietyindocuments.
anotherparallelarchitectureforgenerativetopicmodelsin2010[72].Otherparallelarchitectures
havebeenproposedforgenerativemodelsaswell[16,75].ResearchershaveadaptedLDAtorun
on GPUs in order to model larger datasets [43, 87]. Řehůřek and Sojka created Gensim in 2010,
a Python library containing the most extensive set of topic modeling tools, increasing access to
topicmodelingforusersofalllevelsofproficiencyincodingandtopicmodeling[63].
6 TOPICMODELINGTODAYANDTOMORROW
Inthissurvey,wehavetracedtheevolutionoftopicmodelsfromtheirinceptionuptothepresent.
Inthissection,wediscussthecurrentstateoftopicmodeling,andourintuitionaboutthecriteria
researchersshouldconsiderwhenselectingatopicmodelfordifferentsettings.
Thankstotheproliferationoftheinternetandsocialmedia,therearefarmoretypesandstylesof
textdatainexistencetodaythanwhentopicmodelswereinvented.Socialmediawebsitessuchas
Facebook,Twitter,andRedditproducemillionsofshorttextdocumentseveryday.Figure5shows
the variety in modern-day documents. Document length and quality, as well as dataset volume,
vocabularysize,andsparsity,areallsignificantfactorsthatcontributetothisvariability.Itisthis
variabilityoffactorsthathasledtothecreationofsomanydifferenttypesoftopicmodels.
Givenallofthetopicmodelsthatexist,itisdifficulttosaythatanyonemodelwouldperform
best on a hypothetical dataset. Figure 6 provides the main factors to consider when choosing a
topicmodel.Theoverarchingthemeofthesefactorsfocusesonunderstandingthepropertiesof
the data. The most important factor is the data source. When we want a model that is going to
producegoodtopicsoutofthebox,itisimportanttocomparethedatasetweareusingandthe
datasetsthatwereusedintheoriginalexperimentsonthespecificmodel.Forexample,ifweare
attemptingtoinfertopicsonaTwitterdatasetandweareconsideringtwoshorttexttopicmodels,
wewouldleantowardtheonewhoseauthorstestonTwitterdatasetsintheirpaper.Wemustalso
considerthesizeofourdataset.It’snotuncommontoseeapromisingmodelfailbecauseitcannot
scalefromthesmallerdatasetsitwastestedontolargerdatasets,containingmillionsofdocuments.
AnNLP-aidedtopicmodelmayperformverywellonsmallerdatasetsbutmaybetoocomplexto
scaletolargerdatasets.Otherunforeseenproblemscanbeavoidedifresearcherstakeintoaccount
thelength,noiselevels,andsparsityofdocuments.Thevarietyofdocumenttypeshasresultedina
fieldoftopicmodelsoptimizedfordifferentlengths,noiselevels,andwordco-occurrencedensities.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:30 R.ChurchillandL.Singh
Fig.6. Factorstoconsiderwhenchoosingatopicmodel.
Whereasthesewerenotalwaysfactorsofgreatconcernduetothehomogeneityofdocuments,this
newvarietyhasmadethemfarmoreimportant.Ifresearchershaveaspecificsettinginmindsuch
astemporaltopicmodelingoronlinetopicmodeling,thenumberofoptionsismuchsmaller,and
itislikelythataniterativeprocesswillbenecessarytodeterminethebestmodel.
Still,givenalltheempiricalinvestigation,thereareafewtakeawayswithregardtospecificmeth-
ods.LDA[9]andNMF[69]aregoodgeneral-purposetopicmodels.LDA(specificallytheMALLET
implementation[48])canstrugglewithnoisefiltrationbutcanbeusedinasemi-supervisediter-
ativemannertoproduceagoodground-truthsetoftopicsinthosecases[66].NMF[69]isstilla
popularchoiceoftopicmodelaswell.ItiscommontoseeitusedasanalternativetoLDAwhen
researchersareuncertainaboutthecharacteristicsoftheirdata.
Whendatasetsconsistofshorttexts,considermodelssuchasSATM[62],ETM[60],orothers
that were designed specifically for short texts. When noise is an issue, such as in social media
datasets, there are a number of options including TND and NLDA [20], PTM [18], CSTM [44],
WELDA[12],andothermodelsdesignedwithnoiseinmind.Graph-basedmodelssuchasthose
proposedbyCataldietal.[13]andArrudaetal.[22]performwellintheirrespectiveniches.
Finally,anotheroverlookedquestionwhenchoosingatopicmodelisthetaskthatwewishtouse
ourtopicmodelfor.Inthepast,textclassificationwasbyandlargethemostcommondownstream
taskassignedtotopicmodels.Now,weseeuseoftopicmodelsinallsortsofareas,includingsocial
science[11,66]andotherfieldswherehumansaredirectlyinterpretingtopicsorusingthesetopics
asexplanatoryvariableswithinmoretraditionalstatisticalanalyzes.Giventhenewrolethattopic
modelsareplayingacrossdisciplines,asafield,weneedtocontinuetoimproveourintuitionabout
thestrengthsandweaknessesofdifferenttopicmodelsindifferentsettings.
Agoodapproachistorunasuiteoftopicmodelsonanewdataset,takingtheresultsofthebest
model.Qiangetal.[61]publishedalibraryofshorttexttopicmodelsthatcaneasilybeusedin
suchaway.Itincludesimplementationsof10ofthetopicmodelsinthissurvey,manyofwhich
we have used in our own research when conducting experiments on our own models. In terms
ofevaluatingtopicmodelingresults,webelievethathavingatleastonemethodfromeachofthe
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:31
largercategoriesofevaluationisessential.Coverage,coherence,andqualitativemethodsareall
important,butnoonetopicmodelevaluationistrulycompletebyitself.
Althoughtopicmodelshavecomefarandimprovedgreatlyoverthepastthreedecades,they
arestillnotperfect.Manynewertopicmodelsstillsufferfromnoisepollutionintopics,andmany
morearenotscalabletothesizeofmoderndatasets.Furthermore,thereareveryfewtopicmodels
designedtomodelonatemporalaspect.Alloftheseissuesareimportantfacetsofamoderntopic
model,giventhenoisepresentinandlargescaleofsocialmediadatasets.Theissueoftemporal
topicmodelingisalsopertinentgiventhespeedwithwhichtopicsonaplatformcanchange.Solv-
ingtheseissues,whichcomedowntointerpretabilityandspeed,wouldprovideagreatbenefitto
theusersoftopicmodels.Onlineandtemporaltopicmodels,andtopicmodelsrobusttothenoiseof
socialmedia,arewhatweshouldstrivetoproducegoingforward.Finally,unsupervisedtopicmod-
elshavelimitations.Wetouchedonmeta-dataaugmented,supervised,andreinforcementlearning
topicmodelsattheendofSection5.Asmachinelearningbecomesmoreandmorepowerfuland
betterunderstood,itislikelythatwewillseemoreandmoreofthesetypesoftopicmodels.How-
ever, duetothegrowing size ofdatasets,itmay notalwaysbe feasibleto traincomputationally
expensivemodelssuchassupervisedandreinforcementlearningmodels.Semi-supervisedmodels
maybeanimportantfuturedirectionthatbalancesthecomputationalcostandthecostoflabeling
trainingdata.Topicmodelsarealsolikelytobecomeusefulforgeneratingfeaturesfordifferent
machinelearningandNLPtasks.Wearealreadybeginningtoseethisforlearningofcomplexdy-
namicslikeforcedmigration[70].Otherpossibleapplicationsincludeunderstandingconversation
dynamicstodetectmaliciousgroupsofusersinsocialmedianetworks,identificationofdifferent
typesofmisinformation,andcomparisonsofdifferenttypesofdocumentcollections(newspaper
andsocialmediaasanexample).Theseareallpromisingdirectionsthatcanfurtherincreasethe
impactoftopicmodels.
7 CONCLUSION
This survey describes how topic models have evolved in many directions since their inception.
The evolution has been driven in large part by the evolution of the data that researchers want
to understand. As the structure and volume of data has changed, the limitations of classic topic
modelshavebeenexposed.Newtopicmodelshavebeendesignedtoaccountforthepervasiveness
ofinformal,conversationaltextthatisinherentlynoisy,short,andunstructured.Thesemodelsare
not always new asmuch asthey arerediscoveriesof older models, suchas in thecaseof DMM.
Eventoday,manyofthebestmodelsareadaptationsofLDAtoaccountforthesemodernproblems.
Wehaveseenhowgraph-basedapproacheshavebeenusedincertainsettingsinordertoreduce
noiseandfindsubsetsoftopics(likeemergingtopics),butthesemodelsdonotfindthefulltopic
setandcannotperformthesamedocumentclassificationasgenerativemodels.Wehaveseenhow
non-negative matrix factorization can play the part of a topic model, efficiently approximating
factormatricesthatrepresenttopics.Wehaveseenhowrelativelysimplenaturallanguagetools
such as word embedding vector spaces can significantly improve the performance of old topic
modelsondifferenttypesoftext,withlittleadditionalcomputationaloverhead.
Despitealloftheseinnovations,mostoftheresearchintopicmodelshasbeeninthedirection
ofstaticmodels.Eveninthecaseofmanytemporalmodels,suchasDynamicTopicModelandDy-
namicEmbeddedTopicModel,thereisanassumptionthattheentiredatasetisknownbeforehand.
Onlinelearninghasbeenincorporatedintosomemodelsinordertofacilitatefasterinference,but
thecurrentstateoftheartisstillnotdesignedforbuildingmodelsusingmillionsofstreamingdoc-
umentsonatemporaldimension.Topicmodelsarealsonotdesignedformulti-lingualsituations.
It is not uncommon for social media posts, reviews, emails, and other informal texts to contain
multiple languages. Understanding how to identify and incorporate these multi-lingual cues is
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:32 R.ChurchillandL.Singh
alsoanimportantfuturedirection.Ingeneral,astextbecomesmoreinformal,multi-lingual,multi-
modal,andnoisy,futuretopicmodelsmustbeoptimizedfortheseconstraints.Finally,giventhe
newemphasisonalgorithmicbias,itisalsotimetolookatwhichmodelsgeneratetopicsthatper-
petuatebiasthatexistinthelanguageandwhichonescompensateforthesedifferences.Toward
thatend,topicmodelingfairnessisanotherareathatneedsmoreattention.Whilethehistoryof
topicmodelingisrich,aneedexistsforcontinuedadvancesinthisresearcharea.
REFERENCES
[1] DeepakAgarwalandBee-ChungChen.2010.fLDA:MatrixfactorizationthroughlatentDirichletallocation.InInter-
nationalConferenceonWebSearchandDataMining(WSDM’10).91–100.
[2] FelipeAlmeidaandGeraldoXexéo.2019.WordEmbeddings:ASurvey.arXiv:cs.CL/1901.09069
[3] DanielBackenroth,ZihuaiHe,KrzysztofKiryluk,ValentinaBoeva,LynnPethukova,EktaKhurana,AngelaChristiano,
JosephD.Buxbaum,andIulianaIonita-Laza.2018.FUN-LDA:AlatentDirichletallocationmodelforpredictingtissue-
specificfunctionaleffectsofnoncodingvariation:methodsandapplications.AmericanJournalofHumanGenetics102,
5(2018),920–942.
[4] ArindamBanerjeeandSugatoBasu.2007.Topicmodelsovertextstreams:Astudyofbatchandonlineunsupervised
learning.InSIAMInternationalConferenceonDataMining(SDM’07).431–436.
[5] YoshuaBengio,RéjeanDucharme,PascalVincent,andChristianJauvin.2003.Aneuralprobabilisticlanguagemodel.
JournalofMachineLearningResearch3,(Feb.2003),1137–1155.
[6] PauloBicalho,MarceloPita,GabrielPedrosa,AnisioLacerda,andGiseleL.Pappa.2017.Ageneralframeworkto
expandshorttextfortopicmodeling.InformationSciences393(2017),66–81.
[7] DavidM.BleiandJohnD.Lafferty.2006.Dynamictopicmodels.InInternationalConferenceonMachineLearning
(ICML’06).113–120.
[8] DavidM.Blei,AndrewY.Ng,andMichaelI.Jordan.2002.LatentDirichletallocation.InAdvancesinNeuralInformation
ProcessingSystems(NIPS’02),T.G.Dietterich,S.Becker,andZ.Ghahramani(Eds.).601–608.
[9] DavidM.Blei,AndrewY.Ng,andMichaelI.Jordan.2003.LatentDirichletallocation.JournalofMachineLearning
Research3(March2003),993–1022.
[10] VincentD.Blondel,JeanloupGuillaume,RenaudLambiotte,andEtienneLefebvre.2008.Fastunfoldingofcommuni-
tiesinlargenetworks.JournalofStatisticalMechanics:TheoryandExperiment10(2008),P10008.
[11] Leticia Bode, Ceren Budak, Jonathan M. Ladd, Frank Newport, Josh Pasek, Lisa O. Singh, Stuart N. Soroka, and
MichaelW.Traugott.2020.WordsThatMatter:HowtheNewsandSocialMediaShapedthe2016PresidentialCampaign.
BrookingsInstitutionPress.
[12] StefanBunkandRalfKrestel.2018.Welda:Enhancingtopicmodelsbyincorporatinglocalwordcontext.InACM/IEEE
onJointConferenceonDigitalLibraries.293–302.
[13] MarioCataldi,LuigiDiCaro,andClaudioSchifanella.2010.EmergingtopicdetectiononTwitterbasedontemporal
andsocialtermsevaluation.InKDDWorkshoponMultimediaDataMining.
[14] JonathanChang,JordanBoyd-Graber,ChongWang,SeanGerrish,andDavidM.Blei.2009.Readingtealeaves:How
humansinterprettopicmodels.InAdvancesinNeuralInformationProcessingSystems(NIPS’09).
[15] ChaitanyaChemudugunta,PadhraicSmyth,andMarkSteyvers.2007.Modelinggeneralandspecificaspectsofdocu-
mentswithaprobabilistictopicmodel.InAdvancesinNeuralInformationProcessingSystems(NIPS’07).
[16] JianfeiChen,JunZhu,JieLu,andShixiaLiu.2018.Scalabletrainingofhierarchicaltopicmodels.VLDBEndowment
11,7(2018),826–839.
[17] ZhiyuanChen,ArjunMukherjee,BingLiu,MeichunHsu,MaluCastellanos,andRiddhimanGhosh.2013.Leveraging
multi-domainpriorknowledgeintopicmodels.InInternationalJointConferenceonArtificialIntelligence.
[18] RobChurchillandLisaSingh.2020.Percolation-basedtopicmodelingfortweets.InKDDWorkshoponIssuesofSenti-
mentDiscoveryandOpinionMining(WISDOM’20).
[19] RobChurchillandLisaSingh.2021.textPrep:Atextpreprocessingtoolkitfortopicmodelingonsocialmediadata.In
TheDATAConference.
[20] RobChurchillandLisaSingh.2021.Topic-noisemodels:Modelingtopicandnoisedistributionsinsocialmediapost
collections.InInternationalConferenceonDataMining(ICDM’21).
[21] RobChurchill,LisaSingh,andChristoKirov.2018.Atemporaltopicmodelfornoisymediums.InPacific-AsiaCon-
ferenceonKnowledgeDiscoveryandDataMining(PAKDD’18).
[22] HenriqueFerrazdeArruda,LucianodaFontouraCosta,andDiegoR.Amancio.2016.Topicsegmentationviacom-
munitydetectionincomplexnetworks.Chaos26(2016),063120.
[23] ScottDeerwester,SusanT.Dumais,GeorgeW.Furnas,ThomasK.Landauer,andRichardHarshman.1990.Indexing
bylatentsemanticanalysis.JournaloftheAmericanSocietyforInformationScience41,6(1990),391–407.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:33
[24] JacobDevlin,Ming-WeiChang,KentonLee,andKristinaToutanova.2018.Bert:Pre-trainingofdeepbidirectional
transformersforlanguageunderstanding.arXivpreprintarXiv:1810.04805(2018).
[25] AdjiB.Dieng,FranciscoJ.R.Ruiz,andDavidM.Blei.2019.Topicmodelinginembeddingspaces.arXivpreprint
arXiv:1907.04907(2019).
[26] AdjiB.Dieng,FranciscoJ.R.Ruiz,andDavidM.Blei.2019.Thedynamicembeddedtopicmodel.CoRR(2019).
[27] ChrisDing,TaoLi,andWeiPeng.2008.Ontheequivalencebetweennon-negativematrixfactorizationandproba-
bilisticlatentsemanticindexing.ComputationalStatistics&DataAnalysis52,8(2008),3913–3927.
[28] LinGui,JiaLeng,GabrielePergola,YuZhou,RuifengXu,andYulanHe.2019.Neuraltopicmodelwithreinforcement
learning.InConferenceonEmpiricalMethodsinNaturalLanguageProcessingandtheInternationalJointConferenceon
NaturalLanguageProcessing(EMNLP-IJCNLP’19).3478–3483.
[29] MatthewHoffman,FrancisR.Bach,andDavidM.Blei.2010.OnlinelearningforlatentDirichletallocation.InAdvances
inNeuralInformationProcessingSystems(NIPS’10).856–864.
[30] ThomasHofmann.1999.Probabilisticlatentsemanticindexing.InSIGIRConferenceonResearchandDevelopmentin
InformationRetrieval.50–57.
[31] HemantIshwaranandJ.SunilRao.2005.Spikeandslabvariableselection:FrequentistandBayesianstrategies.Annals
ofStatistics33,2(2005),730–773.
[32] TomoharuIwata,ShinjiWatanabe,TakeshiYamada,andNaonoriUeda.2009.Topictrackingmodelforanalyzing
consumerpurchasebehavior.InInternationalJointConferenceonArtificialIntelligence.Citeseer.
[33] HamedJelodar,YongliWang,ChiYuan,XiaFeng,XiahuiJiang,YanchaoLi,andLiangZhao.2019.LatentDirichlet
allocation(LDA)andtopicmodeling:Models,applications,asurvey.MultimediaToolsandApplications78,11(2019),
15169–15211.
[34] MatthewL.JockersandDavidMimno.2013.Significantthemesin19th-centuryliterature.Poetics41,6(2013),750–769.
[35] G.Kaminkaetal.2016.Ajointmodelforsentiment-awaretopicdetectiononsocialmedia.InEuropeanConferenceon
ArtificialIntelligence.338.
[36] ShivaPrasadKasiviswanathan,PremMelville,ArindamBanerjee,andVikasSindhwani.2011.Emergingtopicdetec-
tionusingdictionarylearning.InInternationalConferenceonInformationandKnowledgeManagement(CIKM’11).
[37] RalfKrestel,PeterFankhauser,andWolfgangNejdl.2009.LatentDirichletallocationfortagrecommendation.InACM
ConferenceonRecommenderSystems.61–68.
[38] SolomonKullbackandRichardA.Leibler.1951.Oninformationandsufficiency.AnnalsofMathematicalStatistics22,
1(1951),79–86.
[39] MattKusner,YuSun,NicholasKolkin,andKilianWeinberger.2015.Fromwordembeddingstodocumentdistances.
InInternationalConferenceonMachineLearning(ICML’15).957–966.
[40] JohnD.LaffertyandDavidM.Blei.2006.Correlatedtopicmodels.InAdvancesinNeuralInformationProcessingSystems
(NIPS’06).147–154.
[41] KenLang.1995.20NewsgroupsDataset.http://people.csail.mit.edu/jrennie/20Newsgroups/.
[42] ChenliangLi,HaoranWang,ZhiqianZhang,AixinSun,andZongyangMa.2016.Topicmodelingforshorttextswith
auxiliarywordembeddings.InSIGIRConferenceonResearchandDevelopmentinInformationRetrieval.165–174.
[43] KaiweiLi,JianfeiChen,WenguangChen,andJunZhu.2017.Saberlda:Sparsity-awarelearningoftopicmodelson
gpus.ACMSIGPLANNotices52,4(2017),497–509.
[44] XimingLi,YueWang,AngZhang,ChangchunLi,JinjinChi,andJihongOuyang.2018.Filteringoutthenoiseinshort
texttopicmodeling.InformationSciences456(2018),83–96.
[45] XimingLi,JiaojiaoZhang,andJihongOuyang.2019.Dirichletmultinomialmixturewithvariationalmanifoldregu-
larization:Topicmodelingovershorttexts.InAAAIConferenceonArtificialIntelligence,Vol.33.7884–7891.
[46] ChenghuaLinandYulanHe.2009.Jointsentiment/topicmodelforsentimentanalysis.InInternationalConferenceon
InformationandKnowledgeManagement(CIKM’09).375–384.
[47] QingqingLong,YilunJin,GuojieSong,YiLi,andWeiLin.2020.Graphstructural-topicneuralnetwork.InInternational
ConferenceonKnowledgeDiscovery&DataMining(KDD’20).1065–1073.
[48] AndrewKachitesMcCallum.2002.MALLET:Amachinelearningforlanguagetoolkit.http://mallet.cs.umass.edu.
[49] YishuMiao,LeiYu,andPhilBlunsom.2016.Neuralvariationalinferencefortextprocessing.InInternationalConfer-
enceonMachineLearning(ICML’16),Vol.48.1727–1736.
[50] TomasMikolov,IlyaSutskever,KaiChen,GregS.Corrado,andJeffDean.2013.Distributedrepresentationsofwords
andphrasesandtheircompositionality.InAdvancesinNeuralInformationProcessingSystems(NIPS’13).3111–3119.
[51] ChristopherE.Moody.2016.MixingDirichlettopicmodelsandwordembeddingstomakelda2vec.CoRR(2016).
[52] RameshM.Nallapati,SusanDitmore,JohnD.Lafferty,andKinUng.2007.Multiscaletopictomography.InInterna-
tionalConferenceonKnowledgeDiscovery&DataMining(KDD’07).520–529.
[53] FengNan,RanDing,RameshNallapati,andBingXiang.2019.TopicmodelingwithWassersteinautoencoders.arXiv
preprintarXiv:1907.12374(2019).
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

215:34 R.ChurchillandL.Singh
[54] DavidNewman,YounNoh,EdmundTalley,SarvnazKarimi,andTimothyBaldwin.2010.Evaluatingtopicmodelsfor
digitallibraries.InJointConferenceonDigitalLibraries.215–224.
[55] DavidJ.NewmanandSharonBlock.2006.Probabilistictopicdecompositionofaneighteenth-centuryAmericannews-
paper.JournaloftheAmericanSocietyforInformationScienceandTechnology57,6(2006),753–767.
[56] DatQuocNguyen,RichardBillingsley,LanDu,andMarkJohnson.2015.Improvingtopicmodelswithlatentfeature
wordrepresentations.AssociationforComputationalLinguistics(ACL)3(2015),299–313.
[57] KamalNigam,AndrewKachitesMcCallum,SebastianThrun,andTomMitchell.2000.Textclassificationfromlabeled
andunlabeleddocumentsusingEM.MachineLearning39,2–3(2000),103–134.
[58] JeffreyPennington,RichardSocher,andChristopherD.Manning.2014.GloVe:Globalvectorsforwordrepresentation.
InEmpiricalMethodsinNaturalLanguageProcessing(EMNLP’14).1532–1543.
[59] IanPorteous,DavidNewman,AlexanderIhler,ArthurAsuncion,PadhraicSmyth,andMaxWelling.2008.Fastcol-
lapsedGibbssamplingforlatentDirichletallocation.InInternationalConferenceonKnowledgeDiscovery&Data
Mining(KDD’08).569–577.
[60] JipengQiang,PingChen,TongWang,andXindongWu.2016.Topicmodelingovershorttextsbyincorporatingword
embeddings.CoRR(2016).
[61] JipengQiang,QianZhenyu,YunLi,YunhaoYuan,andXindongWu.2019.Shorttexttopicmodelingtechniques,
applications,andperformance:Asurvey.arXivpreprintarXiv:1904.07695(2019).
[62] Xiaojun Quan, Chunyu Kit, Yong Ge, and Sinno Jialin Pan. 2015. Short and sparse text topic modeling via self-
aggregation.InInternationalJointConferenceonArtificialIntelligence.
[63] RadimŘehůřekandPetrSojka.2010.Softwareframeworkfortopicmodellingwithlargecorpora.InLREC2010Work-
shoponNewChallengesforNLPFrameworks.45–50.
[64] MichaelRöder,AndreasBoth,andAlexanderHinneburg.2015.Exploringthespaceoftopiccoherencemeasures.In
InternationalConferenceonWebSearchandDataMining(WSDM’15).399–408.
[65] MarcoRossetti,FabioStella,andMarkusZanker.2013.Towardsexplaininglatentfactorswithtopicmodelsincollab-
orativerecommendersystems.InInternationalWorkshoponDatabaseandExpertSystemsApplications.162–167.
[66] R.Ryan,P.E.Davis-Kean,L.Bode,JKruger,Z.Mneimneh,andL.Singh.2020.ThenewDr.Spock:Analyzinginfor-
mationprovidedbyparenting-focusedTwitteraccounts.UnpublishedPaperunderReview.DOI:10.31234/osf.io/n3teh
[67] KentaroSasaki,TomohiroYoshikawa,andTakeshiFuruhashi.2014.OnlinetopicmodelforTwitterconsideringdynam-
icsofuserinterestsandtopictrends.InConferenceonEmpiricalMethodsinNaturalLanguageProcessing(EMNLP’14).
1977–1985.
[68] AlexandraSchofield,MånsMagnusson,andDavidMimno.2017.Pullingoutthestops:Rethinkingstopwordremoval
fortopicmodels.InConferenceoftheEuropeanChapteroftheAssociationforComputationalLinguistics(EACL’17),
Vol.2.432–436.
[69] FarialShahnaz,MichaelW.Berry,V.PaulPauca,andRobertJ.Plemmons.2006.Documentclusteringusingnonneg-
ativematrixfactorization.InformationProcessingManagement42,2(March2006),373–386.
[70] LisaSingh,LailaWahedi,YanchenWang,YifangWei,ChristoKirov,SusanMartin,KatharineDonato,YaguangLiu,
andKornraphopKawintiranon.2019.Blendingnoisysocialmediasignalswithtraditionalmovementvariablesto
predictforcedmigration.InInternationalConferenceonKnowledgeDiscovery&DataMining(KDD’19).1975–1983.
[71] JenniferSleeman,MiltonHalem,TimFinin,MarkCane,etal.2016.Modelingtheevolutionofclimatechangeassess-
mentresearchusingdynamictopicmodelsandcross-domaindivergencemaps.InAAAISpringSymposiumonAIfor
SocialGood.
[72] AlexanderSmolaandShravanNarayanamurthy.2010.Anarchitectureforparalleltopicmodels.VLDBEndowment3,
1–2(2010),703–710.
[73] DavidSontagandDanielM.Roy.2009.Complexityofinferenceintopicmodels.InAdvancesinNeuralInformation
Processing:WorkshoponApplicationsforTopicModels:TextandBeyond.
[74] YeeWhyeTeh,MichaelI.Jordan,MatthewJ.Beal,andDavidM.Blei.2006.HierarchicalDirichletprocesses.Journal
ofAmericanStatisticalAssociation101,476(2006),1566–1581.
[75] AlexanderTerenin,MånsMagnusson,LeifJonsson,andDavidDraper.2018.PolyaurnlatentDirichletallocation:A
doublysparsemassivelyparallelsampler.IEEETransactionsonPatternAnalysisandMachineIntelligence41,7(2018),
1709–1719.
[76] LaureThompsonandDavidMimno.2020.Topicmodelingwithcontextualizedwordrepresentationclusters.arXiv
preprintarXiv:2010.12626(2020).
[77] StephenA.Vavasis.2010.Onthecomplexityofnonnegativematrixfactorization.SIAMJournalonOptimization20,3
(2010),1364–1377.
[78] FelipeViegas,SérgioCanuto,ChristianGomes,WashingtonLuiz,ThiersonRosa,SabirRibas,LeonardoRocha,and
MarcosAndréGonçalves.2019.CluWords:Exploitingsemanticwordclusteringrepresentationforenhancedtopic
modeling.InInternationalConferenceonWebSearchandDataMining(WSDM’19).753–761.
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.

TheEvolutionofTopicModeling 215:35
[79] FelipeViegas,WashingtonCunha,ChristianGomes,AntônioPereira,LeonardoRocha,andMarcosGoncalves.2020.
Cluhtm-semantichierarchicaltopicmodelingbasedoncluwords.AssociationforComputationalLinguistics(ACL).
8138–8150.
[80] DanieleVitale,PaoloFerragina,andUgoScaiella.2012.Classificationofshorttextsbydeployingtopicalannotations.
InEuropeanConferenceonInformationRetrieval(ECIR’12).376–387.
[81] HannaM.Wallach,IainMurray,RuslanSalakhutdinov,andDavidMimno.2009.Evaluationmethodsfortopicmodels.
InInternationalConferenceonMachineLearning(ICML’09).1105–1112.
[82] ChongWang,DavidM.Blei,andDavidHeckerman.2012.Continuoustimedynamictopicmodels.arXivpreprint
arXiv:1206.3298.
[83] ChongWang,JohnPaisley,andDavidBlei.2011.OnlinevariationalinferenceforthehierarchicalDirichletprocess.
InInternationalConferenceonArtificialIntelligenceandStatistics.752–760.
[84] RuiWang,XuemengHu,DeyuZhou,YulanHe,YuxuanXiong,ChenchenYe,andHaiyangXu.2020.Neuraltopic
modelingwithbidirectionaladversarialtraining.arXivpreprintarXiv:2004.12331(2020).
[85] RuiWang,DeyuZhou,andYulanHe.2019.ATM:Adversarial-neuraltopicmodel.InformationProcessing&Manage-
ment56,6(2019),102098.
[86] XueruiWangandAndrewMcCallum.2006.Topicsovertime:Anon-Markovcontinuous-timemodeloftopicaltrends.
InInternationalConferenceonKnowledgeDiscovery&DataMining(KDD’06).
[87] XiaolongXie,YunLiang,XiuhongLi,andWeiTan.2019.CuLDA_CGS:Solvinglarge-scaleLDAproblemsonGPUs.
InSymposiumonPrinciplesandPracticeofParallelProgramming.435–436.
[88] XiaohuiYan,JiafengGuo,YanyanLan,andXueqiCheng.2013.Abitermtopicmodelforshorttexts.InTheWeb
Conference(WWW’13).1445–1456.
[89] XiaohuiYan,JiafengGuo,ShenghuaLiu,XueqiCheng,andYanfengWang.2013.Learningtopicsinshorttextsbynon-
negativematrixfactorizationontermcorrelationmatrix.InSIAMInternationalConferenceonDataMining(SDM’13).
[90] Tze-IYang,AndrewTorget,andRadaMihalcea.2011.Topicmodelingonhistoricalnewspapers.InACL-HLTWorkshop
onLanguageTechnologyforCulturalHeritage,SocialSciences,andHumanities.96–104.
[91] LiminYao,DavidMimno,andAndrewMcCallum.2009.Efficientmethodsfortopicmodelinferenceonstreaming
documentcollections.InInternationalConferenceonKnowledgeDiscovery&DataMining(KDD’09).
[92] XingYiandJamesAllan.2008.Evaluatingtopicmodelsforinformationretrieval.InInternationalConferenceonInfor-
mationandKnowledgeManagement(CIKM’08).1431–1432.
[93] XingYiandJamesAllan.2009.Acomparativestudyofutilizingtopicmodelsforinformationretrieval.InEuropean
ConferenceonInformationRetrieval(ECIR’09).29–41.
[94] JianhuaYinandJianyongWang.2014.ADirichletmultinomialmixturemodel-basedapproachforshorttextclustering.
InInternationalConferenceonKnowledgeDiscovery&DataMining(KDD’14).ACM,233–242.
[95] WayneXinZhao,JingJiang,JianshuWeng,JingHe,Ee-PengLim,HongfeiYan,andXiaomingLi.2011.Comparing
Twitterandtraditionalmediausingtopicmodels.InEuropeanConferenceonInformationRetrieval(ECIR’11).
[96] XiaoweiZhao,DeqingWang,ZhengyangZhao,WeiLiu,ChenweiLu,andFuzhenZhuang.2021.Aneuraltopicmodel
withwordvectorsandentityvectorsforshorttexts.InformationProcessing&Management58,2(2021),102455.
[97] YuanZuo,JunjieWu,HuiZhang,HaoLin,FeiWang,KeXu,andHuiXiong.2016.Topicmodelingofshorttexts:A
pseudo-documentview.InInternationalConferenceonKnowledgeDiscovery&DataMining(KDD’16).2105–2114.
Received3July2020;revised7November2021;accepted20December2021
ACMComputingSurveys,Vol.54,No.10s,Article215.Publicationdate:November2022.