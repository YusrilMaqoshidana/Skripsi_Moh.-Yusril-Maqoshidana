Received10July2024,accepted20August2024,dateofpublication22August2024,dateofcurrentversion2September2024.
DigitalObjectIdentifier10.1109/ACCESS.2024.3447894
From Colonial Legacies to Linguistic Inclusion:
A BERTopic Enhanced Bibliometric Insight
Into Global South Higher Education
SOUMYAJYOTIBANERJEE ANDARITRAPAN ,(Member,IEEE)
InternationalManagementInstituteatBhubaneswar,Bhubaneswar,Odisha751003,India
Correspondingauthor:AritraPan(aritra.pan360@gmail.com)
ABSTRACT The present study is a comprehensive three-tiered empirical framework that investigates the
processesoflinguisticdiversityanddecolonizationwithinthehighereducationsystemsoftheGlobalSouth.
It provides a novel complementary application of ARM for Topic Recommender Systems and explores
the evolving landscape of scholarly discourse on language justice and educational reform by mapping
the findings from Bibliometric Co-occurrence Analysis with LDA and BERTopic modelling respectively.
Bibliometric Co-occurrence Analysis was employed to produce seminal relationships between key terms
from the extant scholarly literature that subsequently leads to a detailed thematic review. Successive
applications of LDA and BERTopic modelling generated a comprehensive thematic analysis that detailed
the trends in academic discourse on inclusivity, multilingualism, translanguaging and decolonization of
higher education curriculum. Furthermore, by the innovative use of ARM based on author keywords, this
studyrevealedmoreintricateassociationsandpatternsamongresearchtopics,givingimportantinsightsinto
future avenues of research. The analysis was based on data entirely retrieved from the Scopus database.
It shows the consensus around the need for reform of language policies in higher education, as well as
thetransformativepotentialforadvancedcomputationaltechniquesinanalyzingacademicnarratives.The
findingsfromourmethodologicalexploration,demonstratethenecessityofpolicyreforminhighereducation
concerning linguistic pluralism and dismantling colonial legacies. This study extends the conversation
around the complexities of decolonisation, linguistic equity and justice in higher education in the Global
Southandbeyond.
INDEX TERMS BERTopic modelling, educational technology, global south, higher education policy,
linguisticdecolonization,multilingualism.
I. INTRODUCTION post-conflict, would entail dealing with a host of factors
UnitedNations2030Agendasetsqualityeducationasoneof rangingfrominfrastructurestoteachingpersonnel’straining
its key goals for the realization of sustainable development andsocietalsupport[3],[4].
worldwide.TheUNinsiststhatqualityeducationisinclusive Thecorefactorthatoverburdensqualityhighereducation
andequitablegiventhatitprovidestherighttolifelonglearn- in the post-colonial societies depends highly on the overde-
ing [1], [2]. Quality higher education (henceforth referred pendence of the Western education models and medium of
toasHE)ishinderedbyseveralfactors.Literaturesuggests instruction [5]. The impact of historical colonialism on the
thatthisformofassuringqualityeducationinanegalitarian contemporarystateofHEinpost-colonialsocieties—likethe
way, especially within the setting of a post-pandemic and Indian and African continents—is emerging as a growing
cause of concern [6], [7]. This helps to provide a greater
The associate editor coordinating the review of this manuscript and insightintopostcolonialchallengeswitheducationalideolo-
approvingitforpublicationwasBijuIssac . gies through the inspection of ideological influences such
2024TheAuthors.ThisworkislicensedunderaCreativeCommonsAttribution-NonCommercial-NoDerivatives4.0License.
117418 Formoreinformation,seehttps://creativecommons.org/licenses/by-nc-nd/4.0/ VOLUME12,2024

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
as gender on HE. A major contribution to these restrictions Adejunmobi[19],forinstance,hasproposedlinguistictrans-
is colonial language dependence and vernacular language lationasameanstocounterlanguageinjustice.Hepointsout
ignorance.Furthermore,highereducation’sdecolonizingdis- thatitcanfacilitateanenvironmentthatfostersdiversity,both
course, especially in its curriculum focus, shares some of linguisticandsocio-economic.Diversityandinclusioncanbe
the cultural and material implications with relation to the enhanced by participatory design. It is necessary, therefore,
colonialism and empire, in close relations to the need to that HE systems in postcolonial societies be grounded in
decolonizethematerialaspectsofcolonizationanddecoloni- language justice, and an equitable environment, in which
sationinhighereducationinstitutions[6]. one has access to formal knowledge in one’s vernacular
The dominance of English in higher education (HE) in [20],[21],[22].
postcolonialsocietiesintheGlobalSouthistheoutcomeof In Africa, the process of decolonisation of HE is compli-
a powerful legacy of colonialism and contemporary global cated and involves uprooting Eurocentric values entrenched
control over the English language [8]. South Africa serves in the academia [1]. Since the official end of apartheid
as a prime example of the ‘‘colonial wound’’ caused by in 1994, the knowledge systems and curriculum in the
the dominance of English in HE, which leads to feelings universities across South Africa are still steeped in colo-
of linguistic and social inferiority among students [1], [9]. nial worldviews [5]. The current Eurocentric curricula is
Calls have been made to intellectualize and internationalize in urgent need of a total rethinking, reframing, and recon-
AfricanlanguagesatAfricanuniversitiesintheglobalcontext stitution to position South Africa and Africa at the core
as a way forward for addressing the issues of equity and of teaching, learning, and research. Academics have drawn
development[10],[11].ThehistoryofIndianHE,alongwith attention to the need to reconsider the decolonisation of
the influence of political policies, has traced an alternative higher education within broader societal shifts, such as the
internationalizationtrajectory[12],[13].TheuseofEnglish COVID-19 pandemic [14], with Naicker [23] underscores
in East Asian HE has also been examined to reveal wider thepandemic’spotentialto‘‘sustainanimportantplankfrom
geopolitics relating to language dominance. This illustrates which to re-imagine the decolonisation of higher education
theassociationofsociopoliticalandhistoricalforcesatplay in South Africa’’ as it proves to reflect the continuing reso-
withinpostcolonialsocieties. nanceandadaptabilityofthedecolonisationdiscourse.This
The significance of language justice in HE in the signalsamorenuancedandfullerunderstandingofthepro-
Global South has been studied extensively. Docrat and cess of decolonisation, extending beyond the curriculum to
Kaschula[14],forexample,exploredthelinksbetweenlan- rethink the epistemological and theoretical bases for HE in
guagetransformationanddecolonisationwithintheHEand Africa[24].
legal systems of South Africa. They advocate the use of Decolonising HE naturally involves the inclusion of ver-
nativeAfricantonguesinthejudiciaryofthecountry.Inhis nacular as a fundamental constituent of its efforts in the
work Rajendram [15] studied the hurdles faced by inter- GlobalSouth.DecolonisationofHEcurriculaandtheinclu-
national students (especially from the Global South) who sion of native languages or knowledge systems is complicit
migratetoCanadianuniversitiesforhigherstudies.Hespeaks with various complexities [6]. Studies onmultilingual prac-
aboutbiasedinstitutionallanguagepoliciesandcontendsfor tices in HE, such as LaDousa et al. [25] discussion of the
translanguaging as a basic criterion that Western universi- ‘languagedness’, reveal the possibility of including indige-
ties must ensure before onboarding international students. nous languages in academics. Also, within postcolonial
Tarisayi[16]speaksabouttheneedtodevelopAI-basedtools societies newer strategies of including vernaculars in HE
for language acquisition, which are relevant to the target ought to be implemented [26], [27]. In Africa, for exam-
users’ culture in the Global South. Decolonising HE in the ple, processes like translanguaging and multilingualism are
Global South is urgent and should focus on the dissocia- aimed to build linguistic diversity and equity in HE [28],
tionofinstitutionsfromremnantcolonialpractices.Thiscan [29]. Multilingualism allows for better student comprehen-
take place through pedagogical transformations and strong sionbyreflectinganation’slinguisticandcultural[30],[31].
institute-communityconnect[1].Indigenouslanguagesofthe Asapolicyinstrumenttranslanguagingandmultilingualism
AfricancontinentfaceseriouschallengesinHEandresearch provides agency to both teachers and learners, eliminates
settings due to the overt dominance of colonial languages, socio-ethnic-linguistic discrimination, and promotes inclu-
thus making the continuous marginalisation of native lan- sivity[32],[33],[28].
guages indefensible [16], [17]. The aforementioned studies Theexistingresearchhasextensivelyexploredthedimen-
point out the essentiality of language justice and decoloni- sions of inclusivity and quality in African HE, revealing
sation efforts in Global South HE. They also give useful criticalinsightsandlayingthegroundworkforfutureexplo-
recommendationsthatserveasusefulindicatorsinthepursuit ration.Differentapproachesemphasizingculturalrelevance,
oflinguisticequalityandinclusivity. a capabilities approach, and rethinking the curriculum have
Language justice in HE needs addressing from varying beenmadebytheaforementionedauthors.Movingforward,
perspectives such as linguistic inequalities, stakeholder par- thefocusshouldshifttowarddesigningpracticalstrategiesfor
ticipation,andovercomingcoloniallanguagehangover[18]. inclusivity, researching the impact of digital education, and
VOLUME12,2024 117419

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE1. Bibliographicdataretrievalprocess.
further destabilizing colonial legacies within curricula. The Using established bibliometric procedures, 1408 articles
evolvingAfricanHElandscapesdemandscontinuedresearch were stratified and assessed to satisfy the selection criteria
todealwithdynamicchallengesandopportunities. neededtoyield992articlesincludedinthestudy.Thereview
Thisresearchhasreviewedrelatedliteratureinanattempt was conducted following the PRISMA protocol (Table 1)
to offer a research terrain within the domain of Equity which provides a comprehensive guideline for conducting
and Language Justice in Higher Education with special on systematicreviewsandmeta-analysesinatransparent,repro-
AfricanHE.Astheresearchprogresses,theauthorsarguethat ducible, and comprehensive process [38], [39] [40]. The
thebibliometricanalysisandtopicmodellingservetoachieve searchyieldedatotalof1408piecesofliterature.Thesearch
thefollowingresearchobjectives: strategy followed multiple inclusion and exclusion criteria.
AfterfilteringthrougharticlesinEnglish,thecollectionwas
1. ChartthetrendsofresearchinthefieldofEquity,Justice,
|     |     |     |     |     |     | narrowed | down to 1066 | articles. | Through | further | manual |
| --- | --- | --- | --- | --- | --- | -------- | ------------ | --------- | ------- | ------- | ------ |
andLanguageJusticeinHigherEducation.
|            |            |            |        |     |         | checking | for relevancy,  | we identified |            | 992 key  | articles that |
| ---------- | ---------- | ---------- | ------ | --- | ------- | -------- | --------------- | ------------- | ---------- | -------- | ------------- |
| 2. Uncover | the unique | underlying | themes | of  | current |          |                 |               |            |          |               |
|            |            |            |        |     |         | became   | the focal point | of our        | study. The | analysis | spanned       |
researchtrendsonEquity,Justice,andLanguageJustice
|           |                     |        |                 |          |        | content     | topics, including     | basic | bibliometrics, |            | topic mod- |
| --------- | ------------------- | ------ | --------------- | -------- | ------ | ----------- | --------------------- | ----- | -------------- | ---------- | ---------- |
| in Higher | Education           | by way | of bibliometric |          | map-   |             |                       |       |                |            |            |
|           |                     |        |                 |          |        | elling, and | topic recommendation, |       | covering       | literature | from       |
| ping      | and topic modelling | using  | large           | language | models |             |                       |       |                |            |            |
theperiodof1996toJanuary2024.Theanalysismethodslike
(LLM).
|     |     |     |     |     |     | bibliometric | co-occurrence | analysis, | LDA | topic | modelling |
| --- | --- | --- | --- | --- | --- | ------------ | ------------- | --------- | --- | ----- | --------- |
3. UsetheTopicRecommenderSystemstosuggestdirec-
|     |     |     |     |     |     | (topicmodels | package | in R v0.2.14), |     | BERTopic | (v0.16.0) |
| --- | --- | --- | --- | --- | --- | ------------ | ------- | -------------- | --- | -------- | --------- |
tionsandtopicsoffutureresearchinEquity,Justice,and
modelling(usingPythoninGoogleColab),andtopicrecom-
LanguageJusticeinHigherEducation.
mendersystemusingassociationrulemining(arulespackage
inRv1.7-6).
II. DATAANDMETHODOLOGY In basic bibliometric analysis from Table 2 using R
Thisresearchmethodologyisamajordeparturefromthepast programming v4.3.3 (RStudio GUI), we have found a
methodologies[34],[35]inHE,socialjustice,decolonisation total of 992 documents to be part of this paper from
etc. This research advances the use of bibliometric analysis 562sources.Atotalof1929authorsareinvolved,including
in the incorporation of the cutting-edge transformer-based 464single-authoreddocuments,withanaveragecitationrate
largepre-trainedlanguagemodels[36],[37].Weutilizedthe of9.277perdocument.Fromtheannualscientificproduction
|     |     |     |     |     |     | chart (Fig. | 1), we can see | a steep | growth | in the | number of |
| --- | --- | --- | --- | --- | --- | ----------- | -------------- | ------- | ------ | ------ | --------- |
Scopusdatabaseasitoffersthelargestcollectionofabstract
andcitationdatabaseofpeer-reviewedliterature.Weentered publicationsinluxuryfashionmarketinginrecentyears.
| search terms | like ‘‘equity,’’ | ‘‘social | justice,’’ | ‘‘inclusion,’’ |     |     |     |     |     |     |     |
| ------------ | ---------------- | -------- | ---------- | -------------- | --- | --- | --- | --- | --- | --- | --- |
‘‘belonging,’’‘‘translanguaging,’’‘‘co-creation,’’‘‘decoloni-
sation,’’ ‘‘decolonisation’’ and ‘‘postcoloni∗’’ in combina- A. EMPIRICALDESIGN
tion with two group of keywords: first set of education Thisflowchartillustratestheprocessoftopicextractionand
(‘‘higher education,’’ ‘‘university,’’ ‘‘university education,’’ recommendationfrombibliometricdata,specificallysourced
‘‘college education’’ and ‘‘tertiary education’’) and second from Scopus. The flowchart is organized into several key
set of geography (‘‘india,’’ ‘‘south africa,’’ ‘‘africa,’’ ‘‘south steps and analytical processes to derive insights and themes
| asia,’’ ‘‘south | east asia’’ | and ‘‘asia’’), | to access | bibliometric |     | fromthedata. |     |     |     |     |     |
| --------------- | ----------- | -------------- | --------- | ------------ | --- | ------------ | --- | --- | --- | --- | --- |
data using ‘TITLE-ABS-KEY’ search function in Scopus This flowchart in Fig. 2 unpacks the process of how bib-
database. This was done to limit the responses to coun- liometric data collected from Scopus becomes topic insight
tries belonging to the Global South [1], and also those that suggestions about important areas of the new technology
wereerstwhileimperialcolonies;nowpostcolonialsocieties, space. It maps out each step and the analytical procedures
such as the Indian subcontinent and several nations from that werefollowed touncover the insightsand themesfrom
| Africa[6]. |     |     |     |     |     | thedatathatwasgathered. |     |     |     |     |               |
| ---------- | --- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | ------------- |
| 117420     |     |     |     |     |     |                         |     |     |     |     | VOLUME12,2024 |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE2. Descriptiveanalyticsofbibliometricdata.
| FIGURE1. | Annualscientificproduction. |     |     |     |     |     |     |     |     |     |
| -------- | --------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
1. Data Source – Scopus Bibliometric: The process starts b. Untokenised Abstracts: This pathway deals with
withthe992bibliometricrecords’bibliometricdatacol- theraw,untokenisedabstractsfromthebibliometric
| lectedfromScopus.Thisisconsideredthefoundational |     |     |     |     |     | data. |     |     |     |     |
| ------------------------------------------------ | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- |
datasetfortheanalysisthatfollows.Astandardcleaning 3. AnalysisPathways:
| procedure | was further | followed | which | included: | tok- |     |     |     |     |     |
| --------- | ----------- | -------- | ----- | --------- | ---- | --- | --- | --- | --- | --- |
a. FromAuthorKeywords:
enization,filteringoutstopwordsandspecialstopwords,
|           |                   |       |         |          |     | i. Association | Rule | Mining: | This | step involves |
| --------- | ----------------- | ----- | ------- | -------- | --- | -------------- | ---- | ------- | ---- | ------------- |
| filtering | out punctuations, | lower | casing, | removing | all |                |      |         |      |               |
applyingassociationruleminingtechniques[39]
| specialty | punctuation | outside | of default | ones | etc. This |        |        |          |             |          |
| --------- | ----------- | ------- | ---------- | ---- | --------- | ------ | ------ | -------- | ----------- | -------- |
|           |             |         |            |      |           | to the | author | keywords | to identify | patterns |
wasperformedonthesourcedatasetsofbothLDAand
|     |     |     |     |     |     | or co-occurrences |     | among | the terms. | After fil- |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | ----- | ---------- | ---------- |
BERTopicmodels.
|                      |     |                  |     |              |        | tering out      | redundant |             | rules and | statistically |
| -------------------- | --- | ---------------- | --- | ------------ | ------ | --------------- | --------- | ----------- | --------- | ------------- |
| 2. Data Segregation: |     | The bibliometric |     | data is then | segre- |                 |           |             |           |               |
|                      |     |                  |     |              |        | non-significant |           | rules using | Fisher’s  | exact test,   |
gatedintotwomainpathwaysforanalysis:
|     |     |     |     |     |     | significant | rules | were checked | against | domain |
| --- | --- | --- | --- | --- | --- | ----------- | ----- | ------------ | ------- | ------ |
a. Author Keywords: This pathway focuses on knowledgetoreportonlyrelevantrules.
analysingthekeywordsprovidedbytheauthorsof ii. Patterns / Co-occurrences: The outcome of the
thebibliometricdata. associationrulemining,highlightthesignificant
| VOLUME12,2024 |     |     |     |     |     |     |     |     |     | 117421 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
FIGURE2. Empiricaldesign.
patternsorco-occurrenceswithintheauthorkey- similar documents into topics based on their
words. The recommended topics co-occurring BERT embeddings. In post-processing, several
with a selected topic gives an insight that how steps are performed to improve the quality and
topics are correlated to each other. This is a relevance of the topics identified by BERTopic.
unique way of understating co-occurrence of Apartfromrefinementsteptoremovenoisydoc-
keywords(orresearchtopics)witheachotherto uments, similar topics were consolidated based
giveresearchersanideaaboutpossibleresearch oncoherenceandexclusivitymeasures.Thepro-
connectionsbetweenkeywords. cessingincludesfollowingsub-steps:
b. TopicModelling: 1. c–TF–IDF: A custom Term Frequency-Inverse
i. BibliometricCo-occurrenceAnalysis:Thisanal- DocumentFrequencyanalysistailoredfortopic
ysis[41]identifiesco-occurringtermswithinthe modelling[44].
bibliometricdatatounderstandtherelationships 2. Vectorization by Sentence Transformer: Con-
betweendifferenttopics. verts text data into numerical vectors using
ii. LDA Topic Modelling: Latent Dirichlet Allo- sentence transformers [45] for better semantic
cation (LDA) is used for topic modelling [42], understanding.
extractingthemesortopicsfromtheuntokenised 3. Dimension Reduction – UMAP: Applies the
abstracts.ItwasfurthertunedusingK-foldCross Uniform Manifold Approximation and Projec-
Validation for different number of topics (2 to tion (UMAP) [46] technique for dimension
20) for selection of optimal number of topics reduction, also aiding in the visualization and
usingElbowmethodaswellascoherencescore clusteringoftopics.
(highestvalue). 4. Clustering–HDBSCAN:HierarchicalDensity-
iii. BERTopic Topic Modelling: BERTopic is a Based Spatial Clustering of Applications with
topicmodellingalgorithmthatusesBERT(Bidi- Noise (HDBSCAN) was then used to per-
rectional Encoder Representations from Trans- formclusteringonthereduced-dimensionaldata,
formers) embeddings to represent text docu- whichwassuccessfulinidentifyingdistincttop-
ments [43]. BERTopic is known for showing ics[47].
superior performance over other traditional and 5. Tuning:TheBERTopicwastunedondefaultval-
deep learning-based topic modelling methods. uesforUMAPandHDBSCAN.Aniterativetun-
ItusesHDBSCANclusteringapproachtogroup ingapproachwastakenforadjustingparameters
117422 VOLUME12,2024

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
byobservingimpactonresults.However,given A. RESEARCHTHEMES
the sample size, tuning set of parameters were AsisevidentfromTable3,thetopicsgeneratedbyLDAtopic
restrictedtolimitedoptions. modellingaregreaterinnumberthanthosegeneratedbyBib-
4. ThemeMapping: liometricCo-occurrenceAnalysis.LDAtopicmodellingwas
a. The topics generated by Bibliometric Co- abletoproducemoreprecisetopics.Consequently,thetopics
occurrenceAnalysisandLDATopicModelling generatedbyBERTopicarestillgreaterinnumberthanthose
aremappedagainsteachotherforidentification produced by LDA and Co-occurrence Analysis. BERTopic
ofcommonandexclusivetopics. was able to give topics with greater precision and accuracy.
b. ThefinalBERTopicAnalysisyields‘‘Topicsby IfwecomparethetopicsbetweenLDA(e.g.‘‘Decolonisation
BERT’’ which were mapped against identified & African Studies’’) and BERTopic, we see that BERTopic
topics from co-occurrence analysis and LDA givesusmultipletopicswithinthetopicgivenbyLDA.This
topicmodelling. enhances the perspective of the researcher and presents an
opportunity to study individually essential fields within a
5. ResearchThemes:
largerdomain.Thus,BERTopicsremainsthemostpotenttool
a. In the final block, topics generated by BERTopic,
forextractingsignificanttopicsfromextantresearch.Using
and their clustering helped in identifying six
BERTopics, we proposed broad research themes in Table 4
research themes. These themes were named with
whichwediscussedindetail.
the help of the domain experts. This section pro-
videsacomprehensiveoverviewofthemainthemes
and insights derived from the entire analysis pro-
B. THEME1:TRANSFORMATIVEEDUCATIONINTHE
cess which presents potential areas of interest for
GLOBALSOUTH
researchwithinthedomain.
Basedonouranalysis,theprominentkeywordsthatcameup
The flowchart acts like a step-by-step process to extract are decolonisation, curriculum, South African, teacher edu-
topics and insights from bibliometric data. Furthermore, cation and pedagogical strategies etc. An important issue in
the results from analysis present the themes of research theGlobalSouthistheconceptoftransformativeeducational
andpotentialresearchtopicrecommendations.Thisincludes paradigms. In the process of decolonizing educational cur-
using both old bibliometric analysis and new text mining ricula[50],observedthatSouthAfricanactivismandsocial
waystolearnfromhiddenpatternsinbibliometricdatafrom movements have emerged as an important terrain through
Scopustogetmeaningfulinsights. whicheducationalnarrativesarere-constructedglobally.This
isimportantgiventhatintheGlobalSouth,highereducation
III. RESULTS isfacedwithnumerouschallengesandopportunities,among
In our analysis 6 topics were extracted using Bibliomet- them the invention of multilingual and translingual peda-
ric Co-occurrence analysis (Fig. 3), 10 using LDA topic gogicalpractices[51]whichinturnempowertheprivileged
modellingand36usingBERTopicmodelling(Fig.5).LDA place of creative expression and student creativity within
optimal topic selection is decided using Elbow method as a decolonized education system, offering new frontiers for
showninFig.4.Fig.5visualizesaninter-topicdistancemap, thediscussionofAfricanhighereducation[35].Thistheme
revealing six distinct clusters of topics given the distance asks us to consider these as inseparable in the context of
between data points [48]. This visualization reinforces the howeducationalsystemsshapesocialstructuresandthecall
clarityandseparatenessofthesethemesinformofgroupof for educational research to interrupt, disrupt, and reconfig-
topics. Quality check helps to identify the validity and reli- ure social and educational structures so that students’ lives
ability of topics generated from topic modelling algorithms are worth writing and reading about. Topics like nurturing
such as Latent Dirichlet Allocation (LDA) and BERTopic. a critical feminist praxis that is inclusive, exploring queer
Coherencescoresprovideamethodforquantifyingthequal- pedagogies,andadecolonialcritiqueofdevelopmentinrela-
ityoftopicsthatareproducedbyalgorithmsbyindicatingto tion to higher education and society thread gender, race,
whatdegreethewordsineachtopicco-occurinameaningful and social justice in such a way that it is not erased but
way [49]. As such, they allow us to determine the perfor- rather addresses issues from outside the norms of higher
manceofLDAaswellasBERTopic.Usingafixedchoiceof educationandequitypolicies[1].Acallismadeforteacher
10topics,theLDAmodelreturnsacoherencescoreof0.094, educationthatincludesareconfigurationofthepedagogical
whereastheBERTopicmodelisabletoachieveasignificantly to accommodate the diverse needs of students and ensure
superiorcoherencescoreof0.496.Ahighercoherencescore equitableaccesstoqualityeducationforall[10].Thisispart
signifiesthatthemodelismoreeffectiveinidentifyingcohe- ofanevenwiderepistemologicaltransformationandspeaks
sive and interpretable topics. This comparison underscores tore-imaginingworldviews,exchanginglinearandEurocen-
the BERTopic model’s enhanced effectiveness in creating tric views for those centered on decolonisation, inclusivity,
moremeaningfulandcoherenttopicclusterscomparedtothe and social justice as the agenda for education in the Global
traditionalLDAmodel. South[6].
VOLUME12,2024 117423

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
| FIGURE3. | Bibliometricco-occurrenceanalysis.                                    |     |     |     |     |     |     |     |
| -------- | --------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
| FIGURE4. | Latentdirichletallocation(LDA)optimaltopicsselectionusingelbowmethod. |     |     |     |     |     |     |     |
C. THEME2:DECOLONISATION,EDUCATION,AND Ubuntuphilosophy,whichaccentuatescommunalvaluesand
CULTURALTRANSFORMATIONINAFRICA interconnectedness as counter-narratives to the legacy of
|             |                  |           |                  | coloniality [53]. | Decolonisation | of HE in | Africa is one | that |
| ----------- | ---------------- | --------- | ---------------- | ----------------- | -------------- | -------- | ------------- | ---- |
| Reimagining | higher education | in Africa | as a vehicle for |                   |                |          |               |      |
decolonisation and African cultural transformation is piv- compels the reclaiming of epistemic knowledge in Africa,
otal within this research theme. Major keywords appearing challenging western epistemic hegemony and arguing for
underthisthemeincludedecolonisation,Africanfilmstudies, an educational curriculum that speaks to the reality and
African colonial studies, French influence, Ubuntu philos- knowledge systems of Africa [35]. So too, does it provide
|               |                      |           |            | into theological | and religious | HE and their | contribution | to  |
| ------------- | -------------------- | --------- | ---------- | ---------------- | ------------- | ------------ | ------------ | --- |
| ophy, African | education, Epistemic | knowledge | in Africa, |                  |               |              |              |     |
theology, and religious education insights amongst others. the decolonisation project and cultural transformation in
Within the landscape of Africa, HE decolonisation, edu- Africa [54]. The decolonisation of African studies and HE
cation, and African cultural transformation are significant commandsboththecultivationofvernacularresearchandstu-
topics of exploration [50]. Such as, African film studies dentengagementasmajordriversoftransformativechange.
as a lens to understand the broader cultural narrative and The research theme marked in our analysis elucidates the
the persistent colonial legacy, with a specific emphasis critical import of a reimagining of HE in Africa as the
on the French influence on African colonial studies [52]. vehicle for decolonizing and cultural transformation. It is
| 117424 |     |     |     |     |     |     | VOLUME12,2024 |     |
| ------ | --- | --- | --- | --- | --- | --- | ------------- | --- |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
|     |     | FIGURE5. |     | BERTopicmappingoftopics. |     |     |     |     |     |     |     |
| --- | --- | -------- | --- | ------------------------ | --- | --- | --- | --- | --- | --- | --- |
advocacy for an educational paradigm deeply engaged with postcolonialspace[6],andwheretheLGBTQ+community
African epistemologies, philosophies, and realities, aiming adds another, unique dimension to the conversation [56].
for a future grounded in cultural sovereignty, social justice, Althoughnotanobviousdomainoftheinclusionandsocial
andsustainabledevelopment. justice movement, Asian politics and international relations
|     |     |     |     |     |     |     | offers more | than enough | evidence | of the | close alignment |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | -------- | ------ | --------------- |
betweenpoliticaldynamicsandeducationalreform,andany
D. THEME3:INCLUSIVITYANDSOCIALJUSTICEIN
|     |     |     |     |     |     |     | critical analysis | of the | inclusion | of learners | within the HE |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | ------ | --------- | ----------- | ------------- |
EDUCATIONINASIA
|             |          |         |             |              |            |              | sector should | also incorporate |         | dominant formations | of gen-     |
| ----------- | -------- | ------- | ----------- | ------------ | ---------- | ------------ | ------------- | ---------------- | ------- | ------------------- | ----------- |
| The primary | keywords |         | identified  | under        | this theme | included     |               |                  |         |                     |             |
|             |          |         |             |              |            |              | der, race,    | and social       | justice | at the HE level     | in an Asian |
| HE in       | India,   | migrant | and refugee | experiences, |            | multicultur- |               |                  |         |                     |             |
utopia[56].Thisthemethusmapsaninternationalterrainas
| alism | and diasporic | identities, |     | Asian | histories | and interna- |     |     |     |     |     |
| ----- | ------------- | ----------- | --- | ----- | --------- | ------------ | --- | --- | --- | --- | --- |
wellasacross-disciplinaryonewherewecanre-imaginean
| tional | relations, | gender | studies | in HE, | social | implications, |     |     |     |     |     |
| ------ | ---------- | ------ | ------- | ------ | ------ | ------------- | --- | --- | --- | --- | --- |
LGBTQ+ equality-driven,culturallyemergent,andcriticallydistinctive
|     | studies | and | rights, | and more. | Significant | discus- |     |     |     |     |     |
| --- | ------- | --- | ------- | --------- | ----------- | ------- | --- | --- | --- | --- | --- |
HEgalaxy.
| sion in    | the Asian | context | —          | with its | postcolonial | societies   |     |     |     |     |     |
| ---------- | --------- | ------- | ---------- | -------- | ------------ | ----------- | --- | --- | --- | --- | --- |
| — includes | inclusion |         | and social | justice  | [6]          | and how the |     |     |     |     |     |
experiences of migrants and refugees, for instance, have E. THEME4:TRANSFORMINGHIGHEREDUCATION
transformedtheeducationallandscapefornewgenerationsin Ouranalysisunveiledtwomajorkeywordsunderthistheme,
Asia,andtheattendantcomplexitiesofcontemporarymulti- viz.,privatizationandeducationtrendsinKerala,andquality
culturalismanddiasporicidentities[55]anditsintersections inHE.ThisthemeextendsthediscussionfromTheme3and
with educational practices and policies with wide-ranging consolidates the focus to the state of HE in the Indian sub-
impactsonstudentexperiencesacrossthecontinent. continent. HE in India continues to cope with the colonial
Inclusivity in HE is also salient in the context of gender, linguistic legacy dominated by English [6]. The narrative
andhowitofferskeyinsightsintohowinstitutionsandindi- of transformation of the system of Indian HE has largely
vidualscanunderstandandaddressgenderdisparitieswithin beenoneofprivatization.Forexample,privatizationandHE
HE [1], even as we consider the struggles and successes trend in Kerala, India, serve as a case study to understand
for Muslim women’s higher education across India — an the implications of privatization in HE globally. The trend
example of how sometimes overlooked female bodies may towardsprivatizationofHEinIndiapresentsbothchallenges
defendtheirrightstohighereducationandlivingintheAsian and opportunities for ensuring quality in higher education,
| VOLUME12,2024 |     |     |     |     |     |     |     |     |     |     | 117425 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE3. Topicsgeneratedbybibliometricco-occurrenceanalysis,LDAtopicmodellingandbertopicmodelling.
117426 VOLUME12,2024

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE3. (Continued.)Topicsgeneratedbybibliometricco-occurrenceanalysis,LDAtopicmodellingandbertopicmodelling.
whichiscrucialforstakeholdersintheeducationsector[57]. studentsandeducators.Keyamongthemistheproliferation
PrivatisationofHEalsohassocialramifications,infostering ofdigitallibrariesrunbyspecificAIappsandwebsites[59].
social equity and justice. It can help in identifying effective Digtal libraries increase the width of learning capabili-
strategiesandframeworkstopromoteinclusivityandfairness ties in response to the challenge of the Pandemic. COVID
in educational access and outcomes [56]. Privatisation can 19severelyaffectedteacher-studentperformance,especially
further the process of inclusive teacher education which is inHEsettings,leadingtostress,andanxietyinacademia[14].
fundamentalincreatingenvironmentsconducivetolearning Innovative educational practices can mitigate these issues,
forallstudents,regardlessoftheirsocio-economic,cultural, thereby improving academic outcomes and student well-
orpersonalbackgrounds.Thismayleadtotheholistictrans- being [16]. Also, in the post-Pandemic scenario integrating
formationofHEinstitutions.Thistransformationshouldaim healthcareresearchandmedicalinnovationsintoHEcurric-
not only to achieve academic excellence and operational ula has become essential, to equip students with the skills
efficiency but also to promote social justice, equity, and andknowledgerequiredtoaddresscontemporaryhealthchal-
inclusivity[58]. lenges[60].
The present research themes underscore the significance
F. THEME5:INNOVATIONSANDCHALLENGESIN of educational research and student engagement in driving
EDUCATION innovation within HE, especially in creating environments
Theme 5 has the following keywords as per our analy- thatencourageactiveparticipationandcriticalthinking.
sis, the COVID pandemic’s impact on sense of belonging,
librarylearningandstudentstudies,digitalliteracyandonline G. THEME6:INCLUSIVEANDENGAGING
learning, performance, stress, and anxiety in academia, and EDUCATIONALPRACTICES
clinicalandmedicalhealthstudies.ThePandemicimpacted Based on our analysis the principal keywords that emerged
students’senseofbelonging;theshiftfromofflinetoonline under this research theme are Education for Students with
learning HE environments challenged and restructured stu- Disabilities, and Inclusive Education Practices. A key com-
dent engagement and community-building dynamics in a ponentofinclusionamongHEinstitutions,especiallyinthe
significant manner [14]. In wake of the digital literacy and Global South, is the education of students with disabilities.
online learning has become important. Innovative pedagog- There is an urgent need to explore innovative strategies and
ical strategies could enhance digital competencies among interventions designed to dismantle barriers to learning and
VOLUME12,2024 117427

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE4. ThemesgeneratedbyclusteringoftopicsextractedusingBERTopic.
117428 VOLUME12,2024

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE4. (Continued.)ThemesgeneratedbyclusteringoftopicsextractedusingBERTopic.
ensuringequitableaccesstoeducationalopportunitiesforall confidence, and lift across rules indicate a rich web of rela-
students[61].InclusionpracticesinHEnotonlymeetsessen- tionshipstobeunpackedforthoseinterestedinthesetopics.
Asanexample,thestrongassociationbetween‘‘colonialism,
| tial educational | needs | but | also foster | a sense | of belonging |     |     |     |     |     |     |     |     |     |
| ---------------- | ----- | --- | ----------- | ------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
andcommunityamongstudents.Inadditiontoleadingtoan postcolonialism’’ and ‘‘neocolonialism’’ (lift = 496.500)
increasededucationalexperience,thebenefitsandvaluesof implies a deeply entangled literature, perhaps reflective of
adopting inclusive educational pedagogies in HE should be a critical interrogation of both historical and contempo-
viewed as a strategy for a more effective educational prac- rarycolonialisms.Incontrast,therule‘‘transformation’’and
tice,studentengagement,andengagedlearningenvironment, ‘‘highereducation’’(lift=2.486)underscoresarelationship
with a view to enhancing academic success and personal that might be more intuitive or broadly findable in the lit-
developmentforthemanystudentswithdiverseneeds[35]. erature, symptomatic of ongoing debates about the role of
Universities and colleges are required to be responsive to educationinsocialtransformation.
| a diverse | population | of  | students. | The paper | provided | case |     |     |     |     |     |     |     |     |
| --------- | ---------- | --- | --------- | --------- | -------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
studiesandexamplesofHEIsthathaveincorporatedinclusive
|     |     |     |     |     |     |     | I. THEMATICCONTINUITIES |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- | --- | --- |
teachingmethodologies,resultingintheenhancementofaca- Rules which reflect the strong interrelations between
demicpracticeandamoreinclusivestudentexperience[61].
|     |     |     |     |     |     |     | ‘‘arts-based |     | inquiry’’ | and ‘‘methods |     | of  | inquiry’’ | and |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | --------- | ------------- | --- | --- | --------- | --- |
InHE,asineducationmorebroadly,therehasbeenacall between ‘‘colonialism, postcolonialism’’ and ‘‘neocolo-
to action for the implementation of inclusive and engaging nialism’’ respectively indicate thematic continuities within
| educational | practices. | This | is a | theme | that evidences | the |            |     |               |           |               |     |     |            |
| ----------- | ---------- | ---- | ---- | ----- | -------------- | --- | ---------- | --- | ------------- | --------- | ------------- | --- | --- | ---------- |
|             |            |      |      |       |                |     | particular |     | fields. These | rules are | characterized |     | by  | relatively |
importanceofhighereducation’sdeepengagementwith,and high confidence scores, which imply that a strong con-
| holistic | adoption | of inclusive | practices |     | in relation | to HE. |         |      |                 |     |                |     |        |       |
| -------- | -------- | ------------ | --------- | --- | ----------- | ------ | ------- | ---- | --------------- | --- | -------------- | --- | ------ | ----- |
|          |          |              |           |     |             |        | ceptual | link | remains between |     | the discussion |     | of one | theme |
It calls for collective action in relation to the creation of and another. This may be particularly useful in guiding
learningenvironmentsthatareaccessible,fair,andengageall researcherstoexplorethedepthofthesethemesasitsuggests
students,particularlythosewithdisabilities.Thisaddsmore
|     |     |     |     |     |     |     | a strong | scholarly | consensus |     | and | a greatly | foundational |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | --------- | --------- | --- | --- | --------- | ------------ | --- |
depthtothediscussionsonequityineducationandcallsfor relationshipbetweentheconcepts.
| a paradigm | shift | in HE | by embracing | different | languages, |     |     |     |     |     |     |     |     |     |
| ---------- | ----- | ----- | ------------ | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
viewpointsandexperiences.
|     |     |     |     |     |     |     | J. INTERDISCIPLINARYBRIDGES |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------------- | --- | --- | --- | --- | --- | --- | --- |
Severalrulesunderscoretheinterdisciplinarynatureofmod-
ernacademicinquiry.Forinstance,theassociationof‘‘central
H. TOPICRECOMMENDERSYSTEMS
asia,gender’’with‘‘Tajikistan’’andsimilarly,‘‘centralasia,
| The association |     | rules in | Table 5 | indicate | some intriguing |     |     |     |     |     |     |     |     |     |
| --------------- | --- | -------- | ------- | -------- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
relationships between academic research topics, illustrating highereducation’’with‘‘Tajikistan,’’reflectspecificregional
|             |                |     |             |          |         | =   | studies | intersecting | with | broader | thematic |     | areas | like gen- |
| ----------- | -------------- | --- | ----------- | -------- | ------- | --- | ------- | ------------ | ---- | ------- | -------- | --- | ----- | --------- |
| the utility | of association |     | rule mining | (minimum | support |     |         |              |      |         |          |     |       |           |
0.002,minimumconfidence=0.1)touncovercomplexpat- derstudiesandeducation[1].Theseassociations,supported
ternswithinscholarlyliteratureusingauthorkeywords.Each by perfect confidence scores, may reveal regional case
|                 |     |             |              |     |          |           | studies | that | are pivotal | in the | broader | discourse |     | of these |
| --------------- | --- | ----------- | ------------ | --- | -------- | --------- | ------- | ---- | ----------- | ------ | ------- | --------- | --- | -------- |
| rule represents | a   | directional | relationship |     | from the | left-hand |         |      |             |        |         |           |     |          |
side (LHS) to the right-hand side (RHS), providing insight thematicareas,suggestingfruitfulareasforcross-disciplinary
|          |             |        |                |     |           |       | research. | Yet | another example |     | can be | the cross | disciplinary |     |
| -------- | ----------- | ------ | -------------- | --- | --------- | ----- | --------- | --- | --------------- | --- | ------ | --------- | ------------ | --- |
| into the | way certain | topics | are associated |     | with each | other |           |     |                 |     |        |           |              |     |
conceptually. association between ‘‘global south’’, ‘‘social justice’’ and
The relevance of these rules goes beyond mere statistical ‘‘global citizenship education.’’ The concept of decolonis-
|     |     |     |     |     |     |     | ing | HE in | the Global South | should, |     | according | to  | this rule, |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | ---------------- | ------- | --- | --------- | --- | ---------- |
association,sheddinglightonthematiccontinuities,interdis-
ciplinary bridges, and evolving discourses within academia. incorporate discussions on educating the demographic in
|               |        |             |                |        |               |          | the       | Global | South about | its extended |     | international |     | commu- |
| ------------- | ------ | ----------- | -------------- | ------ | ------------- | -------- | --------- | ------ | ----------- | ------------ | --- | ------------- | --- | ------ |
| These data    | offer  | a number    | of interesting |        | insights      | into the |           |        |             |              |     |               |     |        |
| way research  | themes | are         | connected.     | This   | is suggestive | of       | nity[62]. |        |             |              |     |               |     |        |
| the potential | for    | association | rule           | mining | to uncover    | signifi- |           |        |             |              |     |               |     |        |
cant patterns that are not necessarily immediately obvious, K. EVOLVINGDISCOURSES
aiding the synthesis of literature and the identification of The table also captures evolving discourses within the
novel research directions. The varying levels of support, academia, particularly in rapidly developing fields. The
| VOLUME12,2024 |     |     |     |     |     |     |     |     |     |     |     |     |     | 117429 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
TABLE5. Topicrecommendersystem.
discussion of ‘‘narrative, social justice’’ and ‘‘performative spokenwordorvisualartifactthroughwhichmeaningiscon-
text’’withahighreach,asindicatedbyMüller[63],moves veyed and through which a specific message or positioning
us to a fresh approach to social justice research, one which emerges[63].Here,individualsandgroupsdisruptdominant
pays attention to narrative and performance in activism and narratives,contestoppressivenorms,andcatalyzecommuni-
scholarship. Narratives are powerful carriers of lived expe- tiesintheconstructionofalternativenarrativesofandvisions
|               |             |             |                    | for more | just and inclusive | societies. | In HE, narratives | and |
| ------------- | ----------- | ----------- | ------------------ | -------- | ------------------ | ---------- | ----------------- | --- |
| rience, tools | that enable | individuals | and groups to give |          |                    |            |                   |     |
voice to their muted knowledge, and challenge ideologies performativetextsrepresentimmersiveexperientiallearning
of domination, including newer iterations of colonialism, opportunitiesthatimmersestudentsinthecreation,represen-
for instance [6]. Performative text refers to any written or tation, and interpretation of narratives through performative
| 117430 |     |     |     |     |     |     | VOLUME12,2024 |     |
| ------ | --- | --- | --- | --- | --- | --- | ------------- | --- |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
acts, for instance, in English courses at the postsecondary Theresultsofthepresentstudyprovideadetailedanalysis
level, as is attested by Giroux and Shannon [64] in their of the aforementioned themes around decolonization, and
whirlwind tour of recent developments in this area. When languagejusticeinGlobalSouthHE.
narratives and performative texts are woven into the fabric The analysis revealed an evolving literature emphasizing
of HE, educators create transformative experiences that cut the urgency to decolonize HE within postcolonial societies
acrossdisciplinesanddeveloptheessentialskillstodealwith andpromotelinguisticinclusion.Theseresearchtrendsalign
navigatinganincreasinglyinterconnectedanddiverseworld. withatheoreticalframeworkthatsuggestsdecolonizationof
|     |     |     |     |     |     |     |     | HE and language |     | justice | as vital | components |     | for achieving |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ------- | -------- | ---------- | --- | ------------- | --- |
academicequity.Thegrowingattentiononsuchthemesindi-
L. METHODOLOGICALINSIGHTS
catesapositiveshifttowardsaddressingthecolonialpractices
| This combination |     | of  | concepts | suggests |     | methodological |     |     |     |     |     |     |     |     |     |
| ---------------- | --- | --- | -------- | -------- | --- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
thatstillpersistinvariousHEsystems.
| insights. | A lift | of 496.500 |     | between | the terms | ‘‘arts-based |     |            |        |            |     |         |          |     |      |
| --------- | ------ | ---------- | --- | ------- | --------- | ------------ | --- | ---------- | ------ | ---------- | --- | ------- | -------- | --- | ---- |
|           |        |            |     |         |           |              |     | The unique | themes | identified |     | through | BERTopic |     | mod- |
inquiry’’and‘‘methodsofinquiry’’,forexample,suggeststhe
|     |     |     |     |     |     |     |     | elling, underscore |     | the intricate | nature | of  | the decolonization |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | ------------- | ------ | --- | ------------------ | --- | --- |
closeassociationandlikelyunderexploredorhighlyspecific
|                |          |            |         |             |         |      |          | discourse.     | These   | identified | themes     | suggest    |               | that achieving |     |
| -------------- | -------- | ---------- | ------- | ----------- | ------- | ---- | -------- | -------------- | ------- | ---------- | ---------- | ---------- | ------------- | -------------- | --- |
| methodological |          | approaches |         | that might  | each    | rule | a number |                |         |            |            |            |               |                |     |
|                |          |            |         |             |         |      |          | language       | justice | in HE      | cannot     | be limited |               | to changes     | in  |
| of different   | research |            | niches. | Researchers | further |      | from the |                |         |            |            |            |               |                |     |
|                |          |            |         |             |         |      |          | the curriculum | but     | must       | also cover | greater    | institutional |                | and |
boundariesofagivenfieldmighttrustthisinsighttoidentify
|     |     |     |     |     |     |     |     | sociocultural | dynamics. |     | The theoretical |     | underpinnings |     | of  |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --------- | --- | --------------- | --- | ------------- | --- | --- |
under-utilizedmethodologicalapproachesthatcouldredefine
|     |     |     |     |     |     |     |     | postcoloniality | that | advocates | for | a wholesome |     | approach | of  |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | ---- | --------- | --- | ----------- | --- | -------- | --- |
theirpracticeandthusthefrontiersoftheirholisticcontribu-
|     |     |     |     |     |     |     |     | undoing | entrenched | colonial | legacies |     | is reflected | in  | these |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | -------- | -------- | --- | ------------ | --- | ----- |
tiontoknowledge.
findings.
| The relationship  |     | is         | as fascinating |         | as the           | possibilities | for   |                     |           |         |        |         |             |          |      |
| ----------------- | --- | ---------- | -------------- | ------- | ---------------- | ------------- | ----- | ------------------- | --------- | ------- | ------ | ------- | ----------- | -------- | ---- |
|                   |     |            |                |         |                  |               |       | Also, as            | mentioned | earlier | the    | topic   | recommender |          | sys- |
| future use-cases. |     | Arts-based |                | inquiry | is a challenging |               | cate- |                     |           |         |        |         |             |          |      |
|                   |     |            |                |         |                  |               |       | tem and association |           | rule    | mining | provide | vital       | insights | into |
gory.Theunderlyingconceptsdescribeanapproachaligned
|         |           |            |          |            |                |     |        | possible           | avenues | for future | research.     |     | For               | example, | the |
| ------- | --------- | ---------- | -------- | ---------- | -------------- | --- | ------ | ------------------ | ------- | ---------- | ------------- | --- | ----------------- | -------- | --- |
| to arts | practice, | as         | they are | used       | to communicate |     | and    |                    |         |            |               |     |                   |          |     |
|         |           |            |          |            |                |     |        | strong correlation |         | between    | ‘‘colonialism |     | postcolonialism’’ |          |     |
| explore | human     | experience |          | [65]. This | is somewhere   |     | after, |                    |         |            |               |     |                   |          |     |
and‘‘neocolonialism’’indicatesthepotentialneedtoinvesti-
| but not | entirely | unlike, | traditional |     | methodologies. |     | These |     |     |     |     |     |     |     |     |
| ------- | -------- | ------- | ----------- | --- | -------------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
gatecurrentformsofcolonialinfluenceupontheHEsystems
| too explore | human       | phenomena |               | and | create knowledge. |     | That     |                 |                     |     |             |             |      |               |       |
| ----------- | ----------- | --------- | ------------- | --- | ----------------- | --- | -------- | --------------- | ------------------- | --- | ----------- | ----------- | ---- | ------------- | ----- |
|             |             |           |               |     |                   |     |          | of postcolonial | societies.          |     | This aligns | well        | with | the theoreti- |       |
| includes    | the sensory |           | and emotional |     | dimension         | of  | scholar- |                 |                     |     |             |             |      |               |       |
|             |             |           |               |     |                   |     |          | cal insight     | that decolonization |     | is          | a continual |      | process       | which |
shipthatarts-basedinquirychampions.Thisexaminationand
requiresconstantvigilance,attentionandadaptation.
| interpretation | of  | human | phenomena, |     | including | the | practices |     |     |     |     |     |     |     |     |
| -------------- | --- | ----- | ---------- | --- | --------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
Thefindingswhenperceivedthroughthelensofpostcolo-
| surrounding | forcibly |     | displaced | peoples, | would | be  | further |     |     |     |     |     |     |     |     |
| ----------- | -------- | --- | --------- | -------- | ----- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
nialtheoryandlanguageequityinHE,divulgetheinterplay
| enriched | by an | exploration |     | and interpretation |     | of arts-based |     |     |     |     |     |     |     |     |     |
| -------- | ----- | ----------- | --- | ------------------ | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ofhistoricalinheritanceandthemodernacademia.Addition-
| inquiry. | It would | not | replace | traditional | methodologies, |     | but |     |     |     |     |     |     |     |     |
| -------- | -------- | --- | ------- | ----------- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ally,theemphasisonmultilingualismasatooltoaccomplish
| package | together | their | insights | into | a more | comprehensive |     |     |     |     |     |     |     |     |     |
| ------- | -------- | ----- | -------- | ---- | ------ | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
theurgentinclusionofindigenouslanguagesalsoalignswith
understandingoftheirsubjects.
thetheoreticalassertionthatactualdecolonizationnecessar-
ilyinvolvesimplementinglinguisticequityandempowering
| M. IMPLICATIONSFORRESEARCHANDEDUCATION |     |     |     |     |     |     |     | marginalizedvoices. |     |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ------------------- | --- | --- | --- | --- | --- | --- | --- |
Variables with lower lift scores are still significant but This also highlights the crucial areas where HE systems
suggest more established or broadly acknowledged connec- in the Global South should focus their efforts to promote
tionswithintheacademicdiscourse,suchas‘‘learning’’and languageequity,justice,andinclusion.
‘‘teaching.’’Thesemoreintuitiveassociations,then,arewell
positioned to inform curriculum development, pedagogical IV. DISCUSSIONANDPOLICYIMPLICATIONS
strategies, and the broader educational discourse by high- ThisstudyemphasizestheurgencyofpolicyreforminGlobal
lighting areas of consensus or foundational knowledge that South HE. It is necessary to eradicate colonial linguistic
underpinacademicdisciplines. scars and ensure language justice, inclusivity and equity
Insum,thesignificanceoftheseassociationrulesistheir in the academia within postcolonial societies. The preva-
ability to map the intellectual landscape of contemporary lenceofcoloniallanguagesintheirHEsystemsperpetuates
research, specifying the co-occurrence of topics as well as socio-cultural exclusion of native speaking students. Thus,
thedepthoftheirinterrelation.Thisprovidesaroadmapfor HE in these nations needs to be more inclusive, and policy
navigatingdialoguesthatareincreasinglycomplex,identify- makersneedtodeliberateseveralessentialaspects.
ingliterature-ladenpolesfromwhichscholarsmightproffer Firstly, transforming HE requires immediate execution
contributions in the form of knowledge and/or method, and of decolonial practices within the curricula. This naturally
suggesting new lines of flight for projects that creatively necessitatesdismantlingWesternhegemonicepistemologies
crosscutdisciplines,methodologies,andthematicareasinan andhermeneutics.Policymakersshouldconsidertransform-
eraofknowledgeproductionthatseemsincreasinglydefined ing the HE curricula to officially include native languages
bysuchbordercrossings. andknowledgesystems,inordertopromotediversitywithin
| VOLUME12,2024 |     |     |     |     |     |     |     |     |     |     |     |     |     |     | 117431 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
academic discourse [1]. A total overhaul of the course socio-culturalcontexts[6].Thiscanbeachievedbyinitiatives
content is required, along with major revisions of reading like multilingual documentation and archiving, vernacu-
and reference materials, teaching methodologies and didac- lar support services, and campaigns for linguistic diversity
tic approaches, to make certain of meeting the goals of withincampuses.Policiessuchasthese,ifimplementedprag-
decolonisation.Suchpolicymeasureswouldensureacademic matically,couldencouragemultilingualismandinclusionin
democratisation. It would make HE more inclusive, acces- academicspaces[35].
sible,andpracticaltostudentsfromvarioussocio-linguistic Along with public policy initiatives the academia also
environments [66]. Inclusivity can be increased greatly by needs to facilitate the process. Research and development
propagating ‘‘vernacular’’ knowledge(s) within HE institu- on translanguaging, multilingualism in the classroom, ped-
tions, which could consequently become spaces for ‘‘the agogical innovations, the efficacy of training programmes,
innumerablediversitiesofhumanthoughtandculture’’[61]. among others, are essential to the overall improvement of
Secondly, a major component of the language justice HEsystems.Researchshouldnecessarilybeinterdisciplinary
projectisthepromotionofmultilingualismwithinHE.Mul- andcollaborative.Itshouldfacilitateeasyexchangeofideas
tilingualism establishes the natural linguistic diversity of amongmultiplestakeholdersintheacademiaandshouldalso
students as an asset. Therefore, policy makers should focus provide access to knowledge repositories [23]. Publicly or
oncreatingatranslanguagingenvironment,whichaugments privatelyfundedjointresearchandconsultancyprojectscan
the development of cognitive ability, student engagement shedlightonanyessentialemergentphenomenon,bestprac-
and subsequent academic scores [67]. The multilingual tices,andcreativesolutions.Collaborativeresearchbetween
approachisalsobeneficialtowardsenhancingsocio-cultural academia and industry can also lead to the development of
collaborationamongstudents.Thiscouldcontributetotheir newertechnologiescustomisedtomeetthespecificlinguistic
psychological aptitude and well-being as well [15]. For this needsofnativestudentsinHEsetups.Transnationalresearch
to happen policies should focus on developing modern aca- canalsoadvancetheunderstandingthemethodsofmeeting
demic infrastructure and should introduce extensive teacher languagejusticeinHE,byallowingabird’sviewperspective
trainingprogrammes. intomultifarioustranslanguagingstrategiesbeingemployed
Thirdly, a significant part of the infrastructure should elsewhere[69].Itcanleadtobestpracticesinpedagogy,and
include modern tools, AI and language technologies. The trainingmethodsinHE.Internationalresearchcanalsostim-
incorporation of such technologies, like language learning ulateconsensusonvernacularrights,diversityandinclusivity
and translation aps, tools for creative etc., help in creating withinacademicspaces[70].
a multifaceted academic and research environment within Whilethepolicyrecommendationsinthestudyareaimed
HE institutions. Technology can effectively bridge the gap atfosteringlinguisticequityinHE,itisnonethelessnecessary
betweenstudentswhohavebenefitedfromaforeignlanguage to acknowledge the potential challenges that could hinder
exposure and those that have not [59]. Policy makers thus, theirimplementation.Addressingsuchproblemsandoffering
needtoincentiviseandsponsorHEinstitutionstoincorporate relevantsolutionswillundoubtedlyaugmenttheoperational
AI tools and language technologies within their pedagogy. effectivenessoftherecommendationsinthereal-world.
The integration of modern educational technology has the A significant challenge is of course could be the lack of
potentialtototallytransformtheHElandscapesintheGlobal institutional willingness to adopt an overhauled format of
South. academic instruction. This may be due to an indifference
Fourthly, incorporating multilingualism within the HE towardstheproblemorthedearthofresourcestoaddressit.
ecosystem automatically requires teachers and facilitators Anentirelyrevisedcurricula,andtheinclusionofindigenous
who are adept at multilingual instruction. Policy makers languagesystemsrequiressubstantialtime,capitalandeffort.
must ensure and fund comprehensive teacher training pro- Anotherobstaclecouldbeincorporatingamultilingualism
grammes in order to create educators equipped with the frameworkwithinHE.Inpostcolonialsocietiesthepredom-
necessary skills to handle a multilingual environment in inance of colonial languages such as English delimit the
theirclassrooms.Suchprogrammesshouldincludemodules availability of instructional materials in native languages.
dealingwithdiversityandinclusivitytraining,translanguag- Additionally, there is a significant probability of a scarcity
ing and multilingual practices [68]. Also, teaching-learning ofqualifiedmultilingualeducators.
and additional reading materials should be made in various Yet another vital challenge is posed by technology. Inte-
indigenouslanguages.Public-privatepartnershipsandinvest- grating state-of-the-art technologies, such as AI-based lan-
mentintheseprogrammescansafeguardtheacademicneeds guagelearningintotheGlobalSouthHElandscapewillprove
of students in the long run, by developing inclusive, and daunting.Thismaybeduetohurdlesconcerninginfrastruc-
diverseacademicenvironments. ture,capitalexpenditureanddigitalliteracy.
Furthermore,publicpoliciesshouldincentivisethedevel- Overcoming such challenges would necessitate a multi-
opmentofmultilingualpolicies.HEsystemsinpostcolonial prongedapproachinpolicymaking,stakeholderengagement,
countries can develop pragmatic frameworks for the use of technological innovation and teacher training. Conducting
various languages within institutional administration, and training workshops to educate HE faculty and staff could
117432 VOLUME12,2024

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
prove extremely beneficial. They must be made aware of quantitative analyses involved in this research allowed for
the benefits of decolonized curricula. The policymakers in-depthanalysesofthebibliometricdata,makingitbroadly
should begin with pilot programmes that incorporate native representativeoftheacademicliterature,itisalsoclearthat
indigenous knowledge systems and languages, and gradu- theydonotnecessarilyreflectthecomplexlivedexperiences
ally spread out based on stakeholder feedback. In order to of linguistic minorities in higher education. Further qual-
defeat the challenged HE institutions in the Global South itative and/or ethnographic research should be undertaken
mustseekfundingopportunitiesfromgovernmentalandnon- to flesh out these preliminary findings. The study limited
governmental organizations. International collaboration and its analysis to articles retrieved from the Scopus database
sharing best practices would also be beneficial. Along with alone,whichmighthaveleftoutsimilarsignificantresearch
this educational material must be developed in indigenous in the domain from other databases (Web of Science etc.).
languagesandeducatorsshouldbetrainedinthem. An important limitation is the linguistic similarity of the
By proactively addressing these potential challenges HE analyzed texts. Since the study mainly focuses on publica-
institutionsintheGlobalSouthcanrationallyhopetoachieve tions in English, it disregards potentially valuable research
amoreequitable,inclusive,andsocio-culturallyrootededu- inotherlanguages.Thismayhaveledtosingledimensional
cationalsystem. perspective to capture educational practices and policies,
Overall,policymakersintheGlobalSouthhavetheoppor- eventually leading towards exclusion of different linguistic
tunity to dismantle redundant colonial HE models and and cultural contexts. Also, the study presupposed that the
technologiesandpavethewayforamoresocio-linguistically trends and patterns identified by the analyses would remain
andsocio-culturallynuanced,equitable,diverseandinclusive stableovertime,geographiesandcultures.Thisassumption
HElandscape.HEtransformationanddecolonisationinpost- might inadvertently overlook the evolution of educational
colonialsocietiesareconsistentwiththeUNSDGsandcan policiesandpractices,whichmaylimittheuniversalapplica-
contributetoamorejustsociety. bility of the findings. The authors suggest expanding future
researchinthisfieldbyincludingmoredatasourcesthatare
V. CONCLUSION diverseaswellasmultiplelanguagesalongsidemoredetailed
The research presented here offers a significant addition to qualitativeanalyses.
agrowingbodyofworkthatischallengingtheexclusionary Future research can be expanded to include other (non-
forcesthatshapehighereducation,particularlyintheGlobal English) language-based literature as well as multiple bib-
South,throughthelensoflanguagejustice.Byilluminating liometric databases (Web of Science, Google Scholar etc.)
the intricate ways in which linguistic diversity, educational to capture diverse perspectives as sole reliance on a single
policies, and colonial legacies intersect, it reminds us of database(Scopusinthisstudy)couldintroduceanunforeseen
the necessity of radically rethinking educational systems to selectionbiasbecauseofitsuniquecoverage,indexingcrite-
embracelinguisticpluralismandfostertrulyinclusivespaces ria,andgeographicrepresentation.Thiscanhelptogainmore
of learning [68]. Ultimately, in synthesising this discussion, generalizabilityofthefuturefindings.Qualitativemethodolo-
this research argues for a reimagined project of higher edu- giescanfurtherprovideadditionalexposuretoexperiencesby
cation,onethatplaceslanguagejusticeatitscoreandseeks linguistic minorities. Longitudinal as well as cross-cultural
tonurtureaneducationalsystemthatvaluesandbuildsfrom studies can put light onto a dynamic and comprehensive
our many languages. The pursuit of such an educational understanding of educational policies and colonial legacies.
endeavour will depend significantly on the commitment of Additionally,exploringdecolonialpractices,integratingtech-
scholars, educators, and policymakers working in unison to nology,andfocusingontheuniquechallengesintheGlobal
radically rethink educational policy and practice. The path South will help create more inclusive and equitable educa-
ahead is long, and it is strewn with the legacy of colonial tionalsystems.
practicesineducationandthemurkywatersofadecolonial
project. But as clear as the legacy of colonialism is in the ACKNOWLEDGMENT
current university systems it is indeed possible to envision Theauthorswouldliketothankalltheanonymousreviewers
a world of academia beyond the colonial [6]. Collaborative fortheirinsightfulcomments.
effortsthatcentredecolonialpraxisinhighereducationmay
wellproduceamoreinclusiveandequitableacademicworld AUTHORCONTRIBUTIONS
within which to marvel at and nurture the intellectual tradi- Aritra Pan and Soumyajyoti Banerjee: conceptualization,
tionsofallofourlanguages. validation, formal analysis, data curation, writing—original
It is important to acknowledge the limitations of this draftpreparation,andwriting—reviewandediting;andAritra
study. The use of specific bibliometric databases runs the Pan:methodology,software,andvisualization.Soumyajyoti
risk of excluding a tradition of valuable non-English and BanerjeeandAritraPanhavereadandagreedtothepublished
grey literature research published in languages other than versionofthemanuscript.
English and in non-academic domains, which could have
widenedthescopeofdiscussiontoincludevariousperspec- CONFLICTSOFINTEREST
tivesfromunderrepresentedregions.Additionally,whilethe Theauthorsdeclarenoconflictsofinterest.
VOLUME12,2024 117433

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
DECLARATIONOFGENERATIVEAIANDAI-ASSISTED [16] K. S. Tarisayi, ‘‘ChatGPT use in universities in South Africa through
|     |     |     |     |     |     |     | a socio-technical |     | lens,’’ | Cogent | Educ., | vol. 11, | no. 1, | Jan. 2024, |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ------- | ------ | ------ | -------- | ------ | ---------- |
TECHNOLOGIESINTHEWRITINGPROCESS
Art.no.2295654,doi:10.1080/2331186x.2023.2295654.
| During   | the preparation |        | of this  | work | the author(s)  | used |                     |     |                  |        |              |           |         |           |
| -------- | --------------- | ------ | -------- | ---- | -------------- | ---- | ------------------- | --- | ---------------- | ------ | ------------ | --------- | ------- | --------- |
|          |                 |        |          |      |                |      | [17] K. Behari-Leak |     | and G.           | Mokou, | ‘‘Disrupting | metaphors | of      | colonial- |
| OpenAI’s | ChatGPT         | (v3.5) | in order | to   | do the English | lan- |                     |     |                  |        |              |           |         |           |
|          |                 |        |          |      |                |      | ity to mediate      |     | social inclusion | in     | the global   | south,’’  | Int. J. | Academic  |
Develop.,vol.24,no.2,pp.135–147,Apr.2019,doi:10.1080/1360144x.
| guage editing | and | grammatical |     | errors checking | to  | improve |     |     |     |     |     |     |     |     |
| ------------- | --- | ----------- | --- | --------------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
2019.1594236.
| the readability | of  | the article. | After | using | this tool/service, |     |                                                                  |     |     |     |     |     |     |     |
| --------------- | --- | ------------ | ----- | ----- | ------------------ | --- | ---------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
|                 |     |              |       |       |                    |     | [18] S.N.Fongwa,‘‘Towardsanexpandeddiscourseongraduateoutcomesin |     |     |     |     |     |     |     |
theauthor(s)reviewedandeditedthecontentasneededand
SouthAfrica,’’Educ.Change,vol.22,no.3,pp.1–23,Nov.2018,doi:
take(s) full responsibility for the content of the publication. 10.25159/1947-9417/3337.
|             |         |      |      |         |                 |     | [19] M. Adejunmobi, |          | ‘‘Translation | and         | postcolonial | identity:   | African        | writ- |
| ----------- | ------- | ---- | ---- | ------- | --------------- | --- | ------------------- | -------- | ------------- | ----------- | ------------ | ----------- | -------------- | ----- |
| The authors | declare | that | they | have no | known competing |     |                     |          |               |             |              |             |                |       |
|             |         |      |      |         |                 |     | ing and             | European | languages,’’  | Translator, |              | vol. 4, no. | 2, pp.163–181, |       |
financial interests or personal relationships that could have Jan.1998,doi:10.1080/13556509.1998.10799018.
appearedtoinfluencetheworkreportedinthispaper. [20] M. R. Wawrzynski and P. Garton, ‘‘Language and the cocurriculum:
Theneedfordecolonizingout-of-classroomexperiences,’’HigherEduc.,
vol.87,no.2,pp.453–469,Mar.2023,doi:10.1007/s10734-023-01016-w.
REFERENCES [21] S. Hasnain and S. Halder, ‘‘Task-based language teaching approach
|             |         |            |            |            |               |     | for improving |     | speaking | fluency: | Case study | of  | trainee | teachers in |
| ----------- | ------- | ---------- | ---------- | ---------- | ------------- | --- | ------------- | --- | -------- | -------- | ---------- | --- | ------- | ----------- |
| [1] M. Nel, | J. Hay, | T. Bekker, | C. Beyers, | N. Pylman, | G. Alexander, | and |               |     |          |          |            |     |         |             |
WestBengal,’’WorldFutures,vol.79,nos.7–8,pp.747–775,Aug.2023,
S.Matoti,‘‘Exploringtheperceptionsoflecturersandfinalyearstudents
doi:10.1080/02604027.2021.1996189.
abouttheinfusionofinclusionininitialteachereducationprogrammesin [22] M. M. Chidsey, ‘‘The language medium ‘divide’: Ideologies of Hindi-
SouthAfrica,’’FrontiersEduc.,vol.8,Mar.2023,Art.no.1024054,doi:
Englishuseatfourall-girls’‘publicschools’inNorthIndia,’’Int.J.Sociol.
10.3389/feduc.2023.1024054.
Lang.,vol.2018,no.253,pp.27–53,Mar.2018,doi:0.1515/ijsl-2018-
[2] A.V.ChisinguiandN.Costa,‘‘Teachereducationandsustainabledevelop-
0022.
mentgoals:Acasestudywithfuturebiologyteachersinanangolanhigher
|     |     |     |     |     |     |     | [23] A. Naicker, | ‘‘Sustaining |     | opportunities | and | mutual | partiality | through |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | ------------ | --- | ------------- | --- | ------ | ---------- | ------- |
educationinstitution,’’Sustainability,vol.12,no.8,p.3344,Apr.2020, collaborative online international learning in South Africa,’’ Pol-
doi:10.3390/su12083344. icy Futures Educ., vol. 22, no. 3, pp.327–336, May 2023, doi:
[3] S. Akoojee, S. Nkomo, and S. Nkomo, ‘‘Access and quality in South 10.1177/14782103231176359.
Africanhighereducation:Thetwinchallengesoftransformation,’’South
|      |           |             |         |                |      |            | [24] N. Alexander, |     | An Ordinary | Country: | Issues | in the | Transition | From |
| ---- | --------- | ----------- | ------- | -------------- | ---- | ---------- | ------------------ | --- | ----------- | -------- | ------ | ------ | ---------- | ---- |
| Afr. | J. Higher | Educ., vol. | 21, no. | 3, pp.385–399, | Feb. | 2008, doi: |                    |     |             |          |        |        |            |      |
ApartheidtoDemocracyinSouthAfrica.NewYork,NY,USA:Berghahn
| 10.4314/sajhe.v21i3.25712. |     |     |     |     |     |     | Books,2003. |     |     |     |     |     |     |     |
| -------------------------- | --- | --- | --- | --- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
[4] M.Pascoe,O.Mahura,andK.Rossouw,‘‘Transcribingandtransforming: [25] C. LaDousa, C. P. Davis, and N. Choksi, ‘‘Postcolonial language ide-
Towardsinclusive,multilingualchildspeechtrainingforSouthAfrican ologies: Indian students reflect on mother tongue and English,’’ J.
speech-language therapy students,’’ Folia Phoniatrica et Logopaedica, Linguistic Anthropol., vol. 32, no. 3, pp.607–628, Aug. 2022, doi:
vol.72,no.2,pp.108–119,Apr.2020,doi:10.1159/000499427.
10.1111/jola.12378.
[5] A.deMeloandL.M.Lima,‘‘Consideringcurriculumchange:Thecasefor [26] B.E.AntiaandC.Dyers,‘‘Epistemologicalaccessthroughlecturemate-
PortugueseasanadditionallanguageinSouthAfricanhighereducation,’’ rialsinmultiplemodesandlanguagevarieties:Theroleofideologiesand
J. Educ., vol. 2020, no. 79, pp.385–399, 2020. [Online]. Available: multilingualliteracypracticesinstudentevaluationsofsuchmaterialsata
https://www.scielo.org.za/scielo.php?script=sci_arttext&pid=S2520- SouthAfricanUniversity,’’Lang.Policy,vol.15,pp.525–545,Nov.2016,
| 98682020000200006 |     |            |             |        |        |            | doi:10.1007/s10993-015-9389-4.                                     |     |     |     |     |     |     |     |
| ----------------- | --- | ---------- | ----------- | ------ | ------ | ---------- | ------------------------------------------------------------------ | --- | --- | --- | --- | --- | --- | --- |
|                   |     |            |             |        |        |            | [27] F.M.PhakaandD.Ovid,‘‘Lifesciencesreadingmaterialinvernacular: |     |     |     |     |     |     |     |
| [6] T. Makhanya   | and | S. Zibane, | ‘‘Students’ | voices | on how | indigenous |                                                                    |     |     |     |     |     |     |     |
languages are disfavoured in South African higher education,’’ Lang. Lessonsfromdevelopingabilingual(IsiZuluandEnglish)bookonSouth
Matters, vol. 51, no. 1, pp.22–37, Jan. 2020, doi: 10.1080/10228195. Africanfrogs,’’CurrentIssuesLang.Planning,vol.23,no.1,pp.96–111,
| 2020.1711533. |     |     |     |     |     |     | Jan.2022,doi:10.1080/14664208.2021.1936397. |     |     |     |     |     |     |     |
| ------------- | --- | --- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
[7] D. P. Lawrence and E. M. Mutua, ‘‘Dialogs and solidarity among the [28] M.NakhoodaandM.I.J.Paxton,‘‘Atranslanguagepedagogytopro-
|     |     |     |     |     |     |     | mote biotechnology |     | concept | engagement |     | and academic | literacy | in a |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | ------- | ---------- | --- | ------------ | -------- | ---- |
sages:BimalKrishnaMatilalandHenryOderaOruka’sadvocacyforthe
philosophicalrationalityofnon-westerncultures,’’J.DharmaStud.,vol.2, linguistically-diverse university context,’’ Crit. Stud. Teaching Learn.,
no.2,pp.153–162,Mar.2020,doi:10.1007/s42240-019-00057-8. vol.9,no.SI,pp.38–55,2021,doi:10.14426/cristal.v9isi.339.
[8] G.B.MalambeandC.Harford,‘‘RaisingtheprofileofsiSwatiasanational [29] O.J.Mbhalati,‘‘Access,equityandredress:Towardsasustainablefunding
language,’’J.Contemp.Afr.Stud.,vol.41,no.2,pp.167–182,Apr.2023, frameworkforpublicuniversitiesinSouthAfrica,’’Rev.Educ.,vol.12,
no.1,p.e3449,Jan.2024.
doi:10.1080/02589001.2021.2014423.
|                |       |               |          |         |                      |     | [30] D.Balosa,‘‘Existentialsociolinguisticsandexistentialjustice:Addressing |          |        |                 |                  |     |          |        |
| -------------- | ----- | ------------- | -------- | ------- | -------------------- | --- | --------------------------------------------------------------------------- | -------- | ------ | --------------- | ---------------- | --- | -------- | ------ |
| [9] S. Sparks, | ‘‘The | peculiarities | of South | African | history: Thompsonian |     |                                                                             |          |        |                 |                  |     |          |        |
|                |       |               |          |         |                      |     | minority                                                                    | language | issues | in multilingual | societies,’’Int. |     | J. Lang. | Stud., |
socialhistoryandthelimitsofcolonialism,’’SocialHist.,vol.45,no.4,
pp.440–452,Oct.2020,doi:10.1080/03071022.2020.1812300. vol.18,no.2,pp.35–62,Apr.2024,doi:10.5281/zenodo.10475254.
[10] P.ChimbundeandM.Kgari-Masondo,‘‘ThedecolonisationofAfrican [31] O.García,‘‘Decolonizingforeign,second,heritage,andfirstlanguages:
Implicationsforeducation,’’inDecolonizingForeignLanguageEduca-
languages:InsightsfromSouthernAfrica,’’Lang.Matters,vol.53,no.3,
tion,D.Macedo,Ed.,NewYork,NY,USA:Routledge,2019,pp.152–168.
pp.5–24,Sep.2022,doi:10.1080/10228195.2022.2138957.
|     |     |     |     |     |     |     | [32] N. Klapwijk | and | C. Van | der Walt, | ‘‘English-plus |     | multilingualism | as  |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ------ | --------- | -------------- | --- | --------------- | --- |
[11] R.N.Madadzhe,‘‘UsingAfricanlanguagesatuniversitiesinSouthAfrica:
|     |     |     |     |     |     |     | the new | linguistic | capital? | Implications |     | of university | students’ | atti- |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | -------- | ------------ | --- | ------------- | --------- | ----- |
Thestrugglecontinues,’’StellenboschPapersLinguisticsPlus,vol.58,
|     |     |     |     |     |     |     | tudes towards | languages |     | of instruction | in  | a multilingual | environment,’’ |     |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --------- | --- | -------------- | --- | -------------- | -------------- | --- |
no.1,pp.205–218,Dec.2019,doi:10.5842/58-0-843.
|     |     |     |     |     |     |     | J. Lang., | Identity | Educ., | vol. 15, | no. 2, | pp.67–82, | Mar. | 2016, doi: |
| --- | --- | --- | --- | --- | --- | --- | --------- | -------- | ------ | -------- | ------ | --------- | ---- | ---------- |
[12] M. Jordaan and N. Mennega, ‘‘Community partners’ experiences of 10.1080/15348458.2015.1137475.
highereducationservice-learninginacommunityengagementmodule,’’ [33] E.Kotzé,‘‘Theemergenceofafavourablepolicylandscape,’’inMultilin-
J.Appl.Res.HigherEduc.,vol.14,no.1,pp.394–408,Mar.2021,doi:
gualUniversitiesinSouthAfrica:ReflectingSocietyinHigherEducation,
10.1108/jarhe-09-2020-0327.
A.deKlerk,Ed.,Stellenbosch,SouthAfrica:SunMedia,2014,pp.15–27.
[13] J.Dyson,‘‘Rethinkingeducationasacontradictoryresource:Girls’educa-
|     |     |     |     |     |     |     | [34] P. Pineda | and S. | Mishra, | ‘‘The semantics |     | of diversity | in higher | educa- |
| --- | --- | --- | --- | --- | --- | --- | -------------- | ------ | ------- | --------------- | --- | ------------ | --------- | ------ |
tionintheIndianHimalayas,’’Geoforum,vol.103,pp.66–74,Jul.2019, tion: Differences between the global north and global south,’’ Higher
doi:10.1016/j.geoforum.2019.03.021. Educ.,vol.85,no.4,pp.865–886,Apr.2023,doi:10.1007/s10734-022-
| [14] Z.DocratandR.H.Kaschula,TransformativePowerofLanguagePolicies |     |     |     |     |     |     | 00870-4. |     |     |     |     |     |     |     |
| ------------------------------------------------------------------ | --- | --- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
inHigherEducation:FromPostcolonialToKnowledgeSocietiesinAfrica. [35] A. Adefila, R. V. Teixeira, L. Morini, M. L. T. Garcia,
NewYork,NY,USA:CambridgeUniv.Press,2020.
T.M.Z.G.F.Delboni,G.Spolander,andM.Khalil-Babatunde,‘‘Higher
[15] S.Rajendram,‘‘Translanguagingasanagentivepedagogyformultilingual education decolonisation: #Whose voices and their geographical
learners:Affordancesandconstraints,’’Int.J.Multilingualism,vol.20, locations?’’Globalisation,SocietiesEduc.,vol.20,no.3,pp.262–276,
no.2,pp.595–622,Apr.2023,doi:10.1080/14790718.2021.1898619. May2022,doi:10.1080/14767724.2021.1887724.
| 117434 |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME12,2024 |     |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- |

S.Banerjee,A.Pan:FromColonialLegaciestoLinguisticInclusion
[36] A.AbuzayedandH.Al-Khalifa,‘‘BERTforArabictopicmodeling:An [58] F.Qamar,‘‘Self-financedprivateuniversitiesinIndia:Genesis,growthand
experimentalstudyonBERTopictechnique,’’Proc.Comput.Sci.,vol.189, policyimplications,’’J.HigherEduc.PolicyLeadershipStud.,vol.2,no.2,
pp.191–194,Jan.2021,doi:10.1016/j.procs.2021.05.096. pp.69–81,Jun.2021,doi:10.52547/johepal.2.2.69.
[37] J. W. Goodell, S. Kumar, W. M. Lim, and D. Pattnaik, ‘‘Artifi- [59] A.Lusigi,‘‘Highereducation,technology,andequityinAfrica,’’NewRev.
cial intelligence and machine learning in finance: Identifying foun- Inf. Netw., vol. 24, no. 1, pp.1–16, Jan. 2019, doi: 10.1080/13614576.
2019.1608576.
| dations, | themes, | and research | clusters | from | bibliometric | analysis,’’ | J.  |     |     |     |     |     |     |     |     |
| -------- | ------- | ------------ | -------- | ---- | ------------ | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Behav. Experim. Finance, vol. 32, Dec. 2021, Art.no.100577, doi: [60] P. Ford-Jones and T. Daly, ‘‘Volunteers’ experiences delivering a
10.1016/j.jbef.2021.100577. community-universitychronicdiseasehealthawarenessprogramforSouth
[38] M. J. Page et al., ‘‘The PRISMA 2020 statement: An updated guide- Asianolderadults,’’J.CommunityHealth,vol.42,no.6,pp.1148–1155,
lineforreportingsystematicreviews,’’Int.J.Surg.,vol.88,Apr.2021, May2017,doi:10.1007/s10900-017-0364-1.
|     |     |     |     |     |     |     |     | [61] O. Mutanga, |     | ‘‘Inclusion of | students | with disabilities |     | in South | African |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | -------------- | -------- | ----------------- | --- | -------- | ------- |
Art.no.105906,doi:10.1016/j.ijsu.2021.105906.
|                  |     |             |        |        |          |             |       | higher | education,’’ | Int. J. | Disability, | Develop. | Educ., | vol. 65, | no. 2, |
| ---------------- | --- | ----------- | ------ | ------ | -------- | ----------- | ----- | ------ | ------------ | ------- | ----------- | -------- | ------ | -------- | ------ |
| [39] R. Agrawal, | T.  | Imieliłski, | and A. | Swami, | ‘‘Mining | association | rules |        |              |         |             |          |        |          |        |
pp.229–242,Sep.2017,doi:10.1080/1034912x.2017.1368460.
betweensetsofitemsinlargedatabases,’’ACMSIGMODRec.,vol.22,
no.2,pp.207–216,Jun.1993,doi:10.1145/170036.170072. [62] B.VanHaute,‘‘ThecontemporarySouthAfricanartistasglobalcitizen,’’
[40] D.Pattnaik,S.Kumar,andA.Vashishtha,‘‘Researchontradecredit—A Int. J. Afr. Renaissance Stud. Multi-, Inter-Transdisciplinarity, vol. 17,
no.1,pp.110–124,Jan.2022,doi:10.1080/18186874.2022.2039876.
systematicreviewandbibliometricanalysis,’’QualitativeRes.Financial
|     |     |     |     |     |     |     |     | [63] M.Müller,‘‘Littleweknowofeachother,’’CulturalStud.Crit.Methodol., |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
Markets,vol.12,no.4,pp.367–390,Jun.2020,doi:10.1108/qrfm-09-
vol.19,no.1,pp.39–42,Jan.2018,doi:10.1177/1532708617750991.
2019-0103.
|                 |       |           |       |         |               |        |        | [64] H.A.GirouxandP.Shannon,EducationandCulturalStudies:Towarda |     |     |     |     |     |     |     |
| --------------- | ----- | --------- | ----- | ------- | ------------- | ------ | ------ | --------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
| [41] M. Callon, | J.-P. | Courtial, | W. A. | Turner, | and S. Bauin, | ‘‘From | trans- |                                                                 |     |     |     |     |     |     |     |
PerformativePractice.NewYork,NY,USA:Routledge,2013.
| lations | to problematic | networks: |     | An introduction |     | to co-word | analy- |     |     |     |     |     |     |     |     |
| ------- | -------------- | --------- | --- | --------------- | --- | ---------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
sis,’’ Social Sci. Inf., vol. 22, no. 2, pp.191–235, Mar. 1983, doi: [65] E. Oliveira and J. Vearey, ‘‘The seductive nature of participatory
research:Reflectingonmorethanadecadeofworkwithmarginalized
10.1177/053901883022002003.
migrantsinSouthAfrica,’’MigrationLett.,vol.17,no.2,pp.219–228,
[42] D.M.Blei,A.Y.Ng,andM.I.Jordan,‘‘LatentDirichletallocation,’’J.
Apr.2020.[Online].Available:https://migrationletters.com/index.php/ml/
Mach.Learn.Res.,vol.3,pp.993–1022,Jan.2002.
article/view/785
[43] M.Grootendorst.(2020).BERTopic:LeveragingBERTandC-TF-IDFto
|     |     |     |     |     |     |     |     | [66] I. Mekoa, | ‘‘Challenges | facing | higher | education | in  | South Africa | : A |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | ------------ | ------ | ------ | --------- | --- | ------------ | --- |
CreateEasilyInterpretableTopics.Zenodo. changefromapartheideducationtodemocraticeducation,’’Afr.Renais-
[44] G.SaltonandC.Buckley,‘‘Term-weightingapproachesinautomatictext sance, vol. 15, no. 2, pp.227–246, Jun. 2018, doi: 10.31920/2516-
retrieval,’’Inf.Process.Manage.,vol.24,no.5,pp.513–523,Jan.1988,
5305/2018/v15n2a11.
doi:10.1016/0306-4573(88)90021-0.
|                 |     |              |                  |     |          |            |     | [67] B. Brock-Utne, |     | ‘‘Researching | language | and | culture in | Africa | using an |
| --------------- | --- | ------------ | ---------------- | --- | -------- | ---------- | --- | ------------------- | --- | ------------- | -------- | --- | ---------- | ------ | -------- |
| [45] N. Reimers | and | I. Gurevych, | ‘‘Sentence-BERT: |     | Sentence | embeddings |     |                     |     |               |          |     |            |        |          |
autoethnographicapproach,’’Int.Rev.Educ.,vol.64,no.6,pp.713–735,
using Siamese BERT-networks,’’ in Proc. Conf. Empirical Methods Sep.2018,doi:10.1007/s11159-018-9746-6.
Natural Lang. Process. 9th Int. Joint Conf. Natural Lang. Process. [68] K.E.Colley,‘‘TeachereducationinanglophoneWestAfrica:Doespolicy
(EMNLP-IJCNLP),HongKong,2019,pp.3982–3992. matchpractice?’’Annu.Rev.ComparativeInt.Educ.,vol.25,pp.201–233,
[46] L.McInnes,J.Healy,andJ.Melville,‘‘UMAP:Uniformmanifoldapprox- Aug.2014,doi:10.1108/S1479-367920140000025015.
imationandprojectionfordimensionreduction,’’2018,arXiv:1802.03426.
|     |     |     |     |     |     |     |     | [69] F.M.OkwaroandP.W.Geissler,‘‘In/dependentcollaborations:Percep- |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
[47] R.J.G.B.Campello,D.Moulavi,andJ.Sander,‘‘Density-basedclustering tionsandexperiencesofAfricanscientistsintransnationalHIVresearch,’’
basedonhierarchicaldensityestimates,’’inProc.17thPacific–AsiaConf. Med. Anthropol. Quart., vol. 29, no. 4, pp.492–511, Dec. 2015, doi:
Knowl.DiscoveryDataMining(PAKDD),2013,pp.160–172. 10.1111/maq.12206.
[48] A. Sharma, N. P. Rana, and R. Nunkoo, ‘‘Fifty years of information [70] P.Narismulu,‘‘Aheuristicforanalysingandteachingliteraturedealing
management research: A conceptual structure analysis using structural with the challenges of social justice,’’Teaching Higher Educ., vol. 18,
no.7,pp.784–796,Oct.2013,doi:10.1080/13562517.2013.836098.
topicmodeling,’’Int.J.Inf.Manage.,vol.58,Jun.2021,Art.no.102316,
doi:10.1016/j.ijinfomgt.2021.102316.
| [49] M. Röder, | A. Both,    | and | A. Hinneburg, | ‘‘Exploring |            | the space  | of topic |     |     |             |     |          |          |     |           |
| -------------- | ----------- | --- | ------------- | ----------- | ---------- | ---------- | -------- | --- | --- | ----------- | --- | -------- | -------- | --- | --------- |
|                |             |     |               |             |            |            |          |     |     | SOUMYAJYOTI |     | BANERJEE | received |     | the Ph.D. |
| coherence      | measures,’’ | in  | Proc. 8th     | ACM         | Int. Conf. | Web Search | Data     |     |     |             |     |          |          |     |           |
degreeinEnglishfromIndianInstituteofTech-
Mining,NewYork,NY,USA,Feb.2015,pp.399–408.
nology(ISM)Dhanbad.Heiscurrentlyworking
[50] M.McAteerandL.Wood,‘‘Decolonisingknowledge:Enactingthecivic
asanAssistantProfessorwithIMIBhubaneswar.
roleoftheuniversityinacommunity-basedproject,’’SouthAfr.J.Educ.,
|     |     |     |     |     |     |     |     |     |     | He has | previously | worked | at Indian | Institute | of  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | ---------- | ------ | --------- | --------- | --- |
vol.38,no.4,pp.1–10,Nov.2018,doi:10.15700/saje.v38n4a1662.
|                    |     |     |           |                   |     |      |            |     |     | Management |     | (IIM) Bodh | Gaya, | Haldia | Institute |
| ------------------ | --- | --- | --------- | ----------------- | --- | ---- | ---------- | --- | --- | ---------- | --- | ---------- | ----- | ------ | --------- |
| [51] R. Tsokalidou | and | E.  | Skourtou, | ‘‘Translanguaging |     | as a | culturally |     |     |            |     |            |       |        |           |
sustaining pedagogical approach: Bi/multilingual educators’ perspec- of Technology, and Indian Institute of Manage-
tives,’’ in Inclusion, Education and Translanguaging. Inklusion Und ment (IIM) Indore. He has more than 13 years
Bildung in Migrationsgesellschaften. Wiesbaden, Germany: Springer, of experience teaching business communication,
2020,pp.219–235. technicalcommunication,businessethics,sustain-
[52] R.Armes,PostcolonialImages:StudiesinNorthAfricanFilm.Blooming- able development, and personality development; and allied courses to
ton,IN,USA:IndianaUniv.Press,2005. undergraduateandpostgraduatestudentsofreputedmanagementandtech-
| [53] R.N.ShanyananaandY.Waghid,‘‘Reconceptualizingubuntuasinclu- |     |     |     |     |     |     |     | nicalinstitutions. |     |     |     |     |     |     |     |
| ---------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- |
sioninAfricanhighereducation:Towardsequalizationofvoice,’’Knowl.
Cultures,vol.4,pp.104–120,Jan.2016.
ARITRAPAN(Member,IEEE)iscurrentlywork-
[54] N.M.Hadebe,‘‘Commodification,decolonisationandtheologicaledu-
|        |            |         |            |     |         |                |     |     |     | ing as | an Assistant |     | Professor | of information |     |
| ------ | ---------- | ------- | ---------- | --- | ------- | -------------- | --- | --- | --- | ------ | ------------ | --- | --------- | -------------- | --- |
| cation | in Africa: | Renewed | challenges | for | African | theologians,’’ | HTS |     |     |        |              |     |           |                |     |
systemswiththeInternationalManagementInsti-
TeologieseStud./TheologicalStud.,vol.73,no.3,pp.1–10,Feb.2017,doi:
10.4102/hts.v73i3.4550. tute (IMI) Bhubaneshwar. Prior to joining IMI,
[55] S. Ahmed, ‘‘Collective feelings,’’ Theory, Culture Soc., vol. 21, no. 2, he was associated with IIM Bodh Gaya, as an
pp.25–42,Apr.2004,doi:10.1177/0263276404042133. Assistant Professor of IT systems and analytics.
Hehasexperienceofworkinginseveralpremiere
| [56] C. Arun-Pina, | ‘‘Homonegative |     | labyrinth | of  | representational | distortions: |     |     |     |     |     |     |     |     |     |
| ------------------ | -------------- | --- | --------- | --- | ---------------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
managementinstituteslikeIFMRGSB,KreaUni-
| Planning | im/possibilities |     | for higher | education | LGBTQ+ | students | in  |     |     |     |     |     |     |     |     |
| -------- | ---------------- | --- | ---------- | --------- | ------ | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
versity,andInstituteofManagementTechnology,
Mumbai,’’UrbanPlanning,vol.8,no.2,pp.150–163,Mar.2023,doi:
Ghaziabad.Hisresearchinterestsincludeanalytics
10.17645/up.v8i2.6311.
|            |           |            |     |       |         |              |        | in the dimensions |     | of financial | markets, | strategic | consulting, | cost-growth |     |
| ---------- | --------- | ---------- | --- | ----- | ------- | ------------ | ------ | ----------------- | --- | ------------ | -------- | --------- | ----------- | ----------- | --- |
| [57] P. M. | Nimmi, P. | V. Mathew, | and | W. E. | Donald, | ‘‘Additional | skills |                   |     |              |          |           |             |             |     |
acquisition programme (ASAP) project: The case of an employability strategy,clientprofiling,andhealthcareandsocialsciencesusingpredictive
enhancement initiative in India,’’ J. Int. Educ. Bus., vol. 15, no. 2, modelingandresearchskills.
pp.393–405,May2022,doi:10.1108/jieb-10-2021-0094.
| VOLUME12,2024 |     |     |     |     |     |     |     |     |     |     |     |     |     |     | 117435 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |