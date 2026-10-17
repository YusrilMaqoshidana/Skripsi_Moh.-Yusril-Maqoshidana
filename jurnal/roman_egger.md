METHODS
published:06May2022
doi:10.3389/fsoc.2022.886498
A Topic Modeling Comparison
Between LDA, NMF, Top2Vec, and
BERTopic to Demystify Twitter Posts
RomanEgger1andJoanneYu2*
1InnovationandManagementinTourism,SalzburgUniversityofAppliedSciences,Salzburg,Austria,2Departmentof
TourismandServiceManagement,ModulUniversityVienna,Vienna,Austria
Therichnessofsocialmediadatahasopenedanewavenueforsocialscienceresearchto
gaininsightsintohumanbehaviorsandexperiences.Inparticular,emergingdata-driven
approaches relying on topic models provide entirely new perspectives on interpreting
social phenomena. However, the short, text-heavy, and unstructured nature of social
media content often leads to methodological challenges in both data collection and
analysis. In order to bridge the developing field of computational science and empirical
social research, this study aims to evaluate the performance of four topic modeling
techniques; namely latent Dirichlet allocation (LDA), non-negative matrix factorization
(NMF), Top2Vec, and BERTopic. In view of the interplay between human relations and
Editedby: digital media, this research takes Twitter posts as the reference point and assesses
DimitriPrandner, the performance of different algorithms concerning their strengths and weaknesses in
JohannesKeplerUniversityof
a social science context. Based on certain details during the analytical procedures and
Linz,Austria
on quality issues, this research sheds light on the efficacy of using BERTopic and NMF
Reviewedby:
TobiasWolbring, toanalyzeTwitterdata.
UniversityofErlangen
Nuremberg,Germany Keywords:topicmodel,machinelearning,LDA,Top2Vec,BERTopic,NMF,Twitter,covidtravel
RubenBach,
UniversityofMannheim,Germany
INTRODUCTION
*Correspondence:
JoanneYu
joanne.yu@modul.ac.at With its limitless availability of constantly growing datasets and simultaneous increase in
computingpower,theeraofdigitaltransformationhasbroughtaboutthepotentialtoaltersocial
Specialtysection: science (Lazer and Radford, 2017). These massive volumes of data assemble digital footprints
Thisarticlewassubmittedto andcapturecumulativehumanactivities,bothindividuallyandcollectively(BocciaArtierietal.,
SociologicalTheory, 2021). As such, the rise of big data in the twenty-first century has prompted a demand for
asectionofthejournal advancedanalytictechniquessuchasmachinelearning,naturallanguageprocessing(NLP),and
FrontiersinSociology
topic modeling in order to uncover patterns and relations embedded in the data, reduce the
Received:28February2022 dimensionality of data, and forecast future outcomes more effectively (Elragal and Klischewski,
Accepted:19April2022 2017).Inparticular,theuseoftopicmodelinginsocialscience[e.g.,conventionalmodelssuchas
Published:06May2022
Dirichletallocation(LDA)andnon-negativematrixfactorization(NMF)]hassoaredinpopularity
Citation: acrossvariousdomainsinthepastyears(Maieretal.,2018;Chenetal.,2019).Thesetechniquesrely
EggerRandYuJ(2022)ATopic onstatisticalmodelingtoextracttopicalpatternswithinacollectionoftexts(EggerandYu,2021).
ModelingComparisonBetweenLDA,
Forinstance,sinceasemanticrelationshipexistsbetweentermslike“apple,”“pear,”and“mango,”
NMF,Top2Vec,andBERTopicto
theycouldbeformedunderatopiccalled“fruit”inatextcorpus(i.e.,acollectionofdocuments).
DemystifyTwitterPosts.
Front.Sociol.7:886498. Typically,documentscontainmixedmembership,whichmeansthatamixtureoftopicsexistsin
doi:10.3389/fsoc.2022.886498 thecorpus(Maieretal.,2018).
FrontiersinSociology|www.frontiersin.org 1 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
To unfold the complex nature of social phenomena, topic 2021), yet the validity and quality of the findings based on
modelsactasabridgebetweensocialscienceand(un)structured suchintuitionremainquestionable.Onecommonmisconception
analysis, different methods of reasoning, and big data analytics that may skew results is the use of default hyperparameter
(Hannigan et al., 2019) due to their explorative character settings. Although the importance of model tuning has been
(Albalawi et al., 2020). In social science, implications of big frequentlyacknowledged(Zhouetal.,2017),littleguidancecan
data can range from macro-level analyses (e.g., social structure befoundwhenanalyzingsocialmediadatainsocialscience.In
and human behavior) to micro-level analyses (e.g., individual addition, another barrier that hinders knowledge generation in
relationshipsandaspectsofdailyactivities).Basedonobserved socialsciencecontextsistheapplicationofmoretraditionaland
phenomena and experiences, examples can be noted from a commonly-adoptedalgorithms(Blairetal.,2020).Forexample,
growing amount of literature analyzing the news (Chen et al., despite the popularity of LDA, the reliability and validity of
2019),onlinereviews(Bietal.,2019),andsocialmediacontent resultshavebeencriticizedsincemodelevaluationisleftbehind
(YuandEgger,2021),amongstothers.Yet,whilethediscussion (EggerandYu,2021).
of big data in social science mainly circles around the critical Consequently, some social scientists have initiated a call to
perspective of the subject, the application itself is hardly ever conduct more interdisciplinary research and evaluate model
deliberated. Although big data seems exceptionally promising, performance based on other new and emerging techniques
data is always preconfigured through beliefs and values, and (Reisenbichler and Reutterer, 2019; Albalawi et al., 2020; Egger
numerous challenges must be acknowledged as every step in and Yu, 2021). Appertaining to the insufficient knowledge of
big data analysis depends on various decisive criteria, such as newlydevelopedalgorithmsthatcouldbetterhandlethenature
theselectionofparameters,theevaluationofpartialresults,and of social media data in social science, this study thus aims to
the actual interpretations thereof (Lupton, 2015). With recent evaluate and compare the performance of four topic modeling
advancement in the NLP field, emerging modeling techniques techniques, namely, LDA, NMF, Top2Vec, and BERTopic.
suchasBERTopic(Grootendorst,2022)andTop2Vec(Angelov, Specifically, LDA is a generative statistical model, NMF uses a
2020) further complicate the process of big data analytics, linearalgebraapproachfortopicextraction,andBERTopicand
pressing the need to evaluate the performance of different Top2Vecuseanembeddingapproach.Bybridgingthediscipline
algorithms.Additionally,whilesocialscientistsareinterestedin of data science with social science, reviews of the strengths,
theory-basedassumptionsandtheirimplications,datascientists and weaknesses of different tools are valuable to support
focus on discovering new patterns (Cai and Zhou, 2016) that applied social scientists in choosing appropriate methods. This
appeartobeirrationalduetotheirlimitedexplanatorypowerfor research sheds light on the capabilities of alternative solutions
socialphenomena(McFarlandetal.,2016). that can facilitate social science scholars in coping with any
Social media has opened an entirely new path for social methodologicalissueswhenaddressingbigdata.
scienceresearch,especiallywhenitcomestotheoverlapbetween
human relations and technology. In this respect, the value of
user-generatedcontentonsocialmediaplatformshasbeenwell- LITERATURE REVIEW
established and acknowledged since their rich and subjective
Making Sense of Social Media Using
information allows for favorable computational analysis (Hu,
2012).Forinstance,recentresearchexploredthesocialdynamics Machine Learning Models
ofsportingeventsbasedonFacebookcomments(Moreauetal., With the omnipresent use of technologies, human
2021), while another study disclosed the social semiotics of communicationhastranscendedtimeandspace,bothlocallyand
different attractions using Instagram content (Arefieva et al., globally(JoubertandCostas,2019).Amongthevarioustypesof
2021). Scholars have also used Twitter posts related to the communicationtools,socialmediastandsoutasavitalmedium
COVID-19pandemictoconstructindividual’sreactions(Boccia in mediating and facilitating interactions between social actors
Artieri et al., 2021). From an epistemological viewpoint, what (Murthy, 2012). As social media portrays human behavior and
is common among these data-driven approaches is that they interactions, social scientists have proceeded with data mining
providebrand-newperspectivesoninterpretingaphenomenon (BocciaArtierietal.,2021)andusingNLPandmachinelearning
and have the possibility to revamp state-of-the-art knowledge approaches. In order to understand the vast numbers of posts
(Simseketal.,2019).Afterall,manyaspectsofsocialscienceand sharedonsocialmedia,NLPcancomprehendhumanlanguages,
socialmediaintertwineinonewayoranother;whiletheformer as programmed for machines, to make predictions based on
concernshumaninteraction,thelatterescalatesitsessencetoa theobservedsocialphenomena(Hanniganetal.,2019).Onthe
muchbroaderandglobalscale. other side, machine learning, as a part of artificial intelligence,
Nevertheless, despite the prominence of social media in refers to computational methods using existing databases (i.e.,
today’s society, posts are often text-heavy and unstructured, thetrainingdata)tobuildandtrainamodelforpredictionand
therebycomplicatingtheprocessofdataanalysis(EggerandYu, better decision making (Zhou et al., 2017). The advantages of
2021).Suchmethodologicalchallengesareparticularlysalientfor opening new horizons for sociological consideration through
thoselackingprogrammingknowledgeandskills(Kraskaetal., advanced data analytics can be witnessed in manifold contexts,
2013). Certainly, recent advancements in visual programming including business, healthcare, education, and, more generally,
software have enabled researchers to analyze social media data the role of social activities in developing scientific knowledge
in a coding-free manner using topic modeling (Yu and Egger, (Yangetal.,2020).
FrontiersinSociology|www.frontiersin.org 2 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
Previous research has underlined that the digital revolution increase the complexity for algorithms to make sense of digital
presents dynamics in exchange networks (Joubert and Costas, interaction. Common challenges arise from using compound
2019)andimpliesone’sself-perception(Murthy,2012).Examples words, acronyms, and ungrammatical sentences (Ariffin and
can be seen from microblogging sites such as Twitter, Tiun, 2020). Despite the productive and unexpressed nature of
accumulatingover200milliondailyactiveusers.Associalmedia compoundwordstheyoftencomplicatecomputationalanalysis
transformsinteractionsintorelationships,andthoseinteractions (Krishna et al., 2016). Other difficulties emerge when data are
evolve into experiences (Witkemper et al., 2012), continuous meaningless (i.e., noisy data) or when there are many gaps
status updates are seen and valued as self-production (Murthy, presentinthedata(i.e.,sparsedata;Kasperiunieneetal.,2020).
2012) and, thus, allow scientists to assess perspectives from the In order to effectively extract features from a large corpus
public’s point of view (Joubert and Costas, 2019). For instance, of text data, numerous text mining approaches have been
in infodemiology, Xue et al. (2020) applied machine learning introduced (Li et al., 2019), among which topic modeling
models to monitor public responses in relation to the COVID- serves as the most frequently adopted technique (Hong and
19discussionandconcernsonTwitter.Likewise,inthehighly- Davison, 2010). In a nutshell, a topic model is a form of
dynamic tourism industry, Lu and Zheng (2021) were able to statistical modeling used in machine learning and NLP, as
track public opinions toward cruise ships during the COVID- discussed earlier, that identifies hidden topical patterns within
19 pandemic based on collected tweets. Furthermore, unlike a collection of texts (Guo et al., 2017). Those viewed as
most networking platforms built upon existing friendships, the the most established, go-to techniques include LDA, latent
retweetfunctioncandisseminateinformationmuchfaster(Park semantic analysis (LSA), and probabilistic LSA (Albalawi et al.,
etal.,2016),therebymakingTwitteranidealmediumforsocial 2020). More recently, however, newly developed algorithms
scienceresearch. such as NMF, Corex, Top2Vec, and BERTopic have also
Yet, regardless of which social media platform, theorization received,andarecontinuingtoattract,increasingattentionfrom
remains an integral part (Müller et al., 2016) of the emerging researchers (Obadimu et al., 2019; Sánchez-Franco and Rey-
subject of big data in social science. Although some scholars Moreno,2022).Inthesocialsciences,topicmodelshaveformerly
believethatbigdatacan,andshould,befreeoftheoryaltogether been applied to, for example, discover consumers’ implicit
(Anderson,2008;Kitchin,2014),itseemsimprobabletointerpret preferences(Vuetal.,2019;Eggeretal.,2022),identifysemantic
results without a sufficient understanding of the social sciences structures on Instagram (Egger and Yu, 2021), and improve
(Mazanec, 2020). Nevertheless, methodological challenges recommendationsystems(ShafqatandByun,2020).Despitethe
often present themselves in parallel with epistemological robustnessoftopicmodelingalgorithms,existingliteraturerelies
developments. For instance, because algorithms are unable to primarily on one single model, with LDA being the dominant
structurefreetext,datapreprocessingstepsthatrequirecomplex method (Gallagher et al., 2017) and is typically viewed as the
decision-makingskills,suchascleaning,transformation,feature standardapproach.
extraction, and vectorization, lay the foundation for further RegardlessofthepopularityofLDAwithinthesocialscience
analysis (Albalawi et al., 2020). Though social scientists have branch, its efficacy in analyzing social media data has been
the ability to preprocess the datasets, issues may arise in the highly criticized (Egger and Yu, 2021; Sánchez-Franco and
followingstepsinvolvingmodelevaluationandhyperparameter Rey-Moreno, 2022). In the case of Twitter data, Jaradat and
tuning(Blairetal.,2020).Forthemostpart,thesechallengescan Matskin (2019) argue that, while multiple topics can coexist
betracedbacktothenatureofsocialmediacontentitself,which in a document, LDA tends to neglect co-occurrence relations.
primarilyconsistsofshort,concise,text-heavy,andunstructured Likewise, other researchers emphasize that noisy and sparse
formats(Albalawietal.,2020). datasets are unsuitable for LDA (Chen et al., 2019) due to
a lack of features for statistical learning (Cai et al., 2018).
Consequently, researchers have reinforced the value of newly
Topic Modeling as a Solution to Cope With
developedalgorithmsasalternativessincetheyoftenoutperform
Unstructured Text Data LDA,especiallywhenanalyzingshorttextdataonsocialmedia
Ashumanlanguageisanadaptivemultilevelsystem,textlength, (Egger, 2022b). Albeit new approaches have emerged and
syntactic complexity, and semantic plausibility have long been have been adopted to reveal novel insights, their innovative
considered focal points in both psychology and linguistics advantages (unintentionally) lower the significance of model
(BradleyandMeeds,2002).Togetherwiththeinterplaybetween evaluation. Evidence can be taken from social media research,
technologyandmodernization,theirimpacthasalsoextendedto to which applying evaluation techniques is yet to become
socialmedia.Forinstance,scholarshavepointedoutthatshorter mainstream (Reisenbichler and Reutterer, 2019). Furthermore,
posts typically lead to a higher engagement rate on Facebook because models would be optimized in extracting any slight
(Sabateetal.,2014),potentiallybecauseconcisemessagesreduce variant of a topic, depending on the purpose of the algorithm,
theamountofcognitiveeffortneededforinformationprocessing theresultsmightbeskewedinaspecificdirection.Theseissues
(Sheetal.,2022).Acrossthevariousavailabletypesofplatforms, furtherhighlighttheunreliabilityofconcentratingsolelyonone
Twitter, in particular, restricts each post to a maximum of single topic model and, thereby, also strengthening the value
280 characters (Queiroz, 2018), and although these short and and need to compare differing algorithms (Reisenbichler and
unstructured posts conform with social media practice, they Reutterer,2019;Albalawietal.,2020;EggerandYu,2021).
FrontiersinSociology|www.frontiersin.org 3 May2022|Volume7|Article886498

| EggerandYu |     |         |     |     |     |     |     |     |     |     |     | ATopicModelingComparison |     |     |
| ---------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------------------ | --- | --- |
| MATERIALS  | AND | METHODS |     |     |     |     |     |     |     |     |     |                          |     |     |
withanefficientresourcetoobtainanexplicitrepresentationof
adocument.
Intrigued by the complexity of short-text social media data, In this research, to pinpoint optimal values for the three
the goal of this research is to compare different types of topic hyperparametersrequiredforLDA,agridsearchwasperformed
modelingalgorithmsinordertooffernewinsightsandsolutions
|     |     |     |     |     |     |     |     | for the | number | of topics | (K) as | well as | for beta | and alpha. |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ------ | --------- | ------ | ------- | -------- | ---------- |
tosocialscientistsinterestedininvestigatinghumaninteractions. The higher the beta, the more words the topics consist of;
Compared to other platforms, Twitter features concise posts, likewise, the higher the alpha, the more diverse the topics are.
| with a maximum |     | of 280 | characters | per | tweet, | that | can be |     |     |     |     |     |     |     |
| -------------- | --- | ------ | ---------- | --- | ------ | ---- | ------ | --- | --- | --- | --- | --- | --- | --- |
Thesearchforanoptimalnumberoftopicsstartedwitharange
| identified | via specific | hashtags |     | (Queiroz, | 2018). | The | use of |          |        |        |         |         |           |             |
| ---------- | ------------ | -------- | --- | --------- | ------ | --- | ------ | -------- | ------ | ------ | ------- | ------- | --------- | ----------- |
|            |              |          |     |           |        |     |        | from two | to 15, | with a | step of | one. In | the first | step of the |
hashtagsthusstreamlinestheinformationsearchprocessbased learning process, K was pre-defined, and the search for beta
on users’ interests. Seeing the potential of social media in and alpha was applied accordingly. During the process, only
| enhancing | crisis communication |     |     | (Femenia-Serra |     | et al., | 2022), |     |     |     |     |     |     |     |
| --------- | -------------------- | --- | --- | -------------- | --- | ------- | ------ | --- | --- | --- | --- | --- | --- | --- |
onehyperparametervaried,andtheotherremainedunchanged
this study makes use of Twitter posts related to travel and the untilreachingthehighestcoherencescore.Thecoherencescore,
COVID-19pandemicasreferencepointsfortheevaluationofthe referring to the quality of the extracted topics, presented itself
fourabove-mentionedtopicmodels(i.e.,LDA,NMF,Top2Vec,
|     |     |     |     |     |     |     |     | for 14 topics | with | a value | of 0.52. | The grid | search | then yielded |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | ---- | ------- | -------- | -------- | ------ | ------------ |
and BERTopic). The detailed implementation process of this asymmetricdistributionwithavalueof0.91forbothalphaand
studyproceededasbelow. beta. Finally, to facilitate a clear interpretation of the extracted
|     |     |     |     |     |     |     |     | information | from | a fitted | LDA | topic model, | pyLDAvis | was |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ---- | -------- | --- | ------------ | -------- | --- |
Data Collection and Preprocessing usedtogenerateanintertropicaldistancemap(Islam,2019).A
|                 |          |           |               |          |      |           |           | screenshot  | of the         | statistical | proximity     | of the | topics    | can be seen |
| --------------- | -------- | --------- | ------------- | -------- | ---- | --------- | --------- | ----------- | -------------- | ----------- | ------------- | ------ | --------- | ----------- |
| Data collection | was      | conducted | in            | November | 2021 | by        | using the |             |                |             |               |        |           |             |
|                 |          |           |               |          |      |           |           | in Figure1. | An interactive |             | visualization | is     | available | at https:// |
| data extraction | software | tool      | Phantombuster |          | and  | searching | for       |             |                |             |               |        |           |             |
tinyurl.com/frontiers-TM.
| the terms   | #covidtravel | as      | well as     | the combination |     |          | of #covid |     |     |     |     |     |     |     |
| ----------- | ------------ | ------- | ----------- | --------------- | --- | -------- | --------- | --- | --- | --- | --- | --- | --- | --- |
| and #travel | to fetch     | tweets. | The initial | datasets        |     | included | a total   |     |     |     |     |     |     |     |
Model2:Non-negativeMatrixFactorization
| of 50,000 | tweets posted |     | in English; | however, |     | after | cleaning |     |     |     |     |     |     |     |
| --------- | ------------- | --- | ----------- | -------- | --- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- |
the data and removing duplicate posts, the final datasets IncontrasttoLDA,NMFisadecompositional,non-probabilistic
algorithmusingmatrixfactorizationandbelongstothegroupof
consistedof31,800uniquetweets.Afterthat,thedataunderwent
|               |          |     |          |        |          |     |           | linear-algebraic | algorithms |     | (Egger, | 2022b). | NMF | works on TF- |
| ------------- | -------- | --- | -------- | ------ | -------- | --- | --------- | ---------------- | ---------- | --- | ------- | ------- | --- | ------------ |
| preprocessing | in which | all | mentions | (e.g., | @users), |     | hashtags, |                  |            |     |         |         |     |              |
IDFtransformeddatabybreakingdownamatrixintotwolower-
unknownsigns,andemojiswereremoved.Itisimportanttonote
rankingmatrices(Obadimuetal.,2019).Specifically,TF-IDFis
that,uptothispoint,originalsentenceswereusedforBERTopic
|             |             |      |            |           |     |              |          | a measure     | to evaluate | the          | importance | of a     | word | in a collection |
| ----------- | ----------- | ---- | ---------- | --------- | --- | ------------ | -------- | ------------- | ----------- | ------------ | ---------- | -------- | ---- | --------------- |
| and Top2Vec | since       | both | algorithms | rely      | on  | an embedding |          |               |             |              |            |          |      |                 |
|             |             |      |            |           |     |              |          | of documents. | As          | demonstrated | in         | Figure2, | NMF  | decomposes      |
| approach,   | and keeping | the  | original   | structure | of  | the text     | is vital |               |             |              |            |          |      |                 |
fortransformermodels. its input, which is a term-document matrix (A), into a product
|              |         |       |          |         |     |         |      | of a terms-topics |         | matrix | (W) and    | a topics-documents |       | matrix       |
| ------------ | ------- | ----- | -------- | ------- | --- | ------- | ---- | ----------------- | ------- | ------ | ---------- | ------------------ | ----- | ------------ |
| On the       | other   | hand, | the data | for     | LDA | and NMF | was  |                   |         |        |            |                    |       |              |
|              |         |       |          |         |     |         |      | (H) (Chen         | et al., | 2019). | The values | of W               | and H | are modified |
| preprocessed | further | using | NLP      | modules | in  | Python. | More |                   |         |        |            |                    |       |              |
iteratively,wheretheformercontainsthebasisvectors,andthe
precisely,stopwordswereexcluded,irrelevanttext(e.g.,numbers,
lattercontainsthecorrespondingweights(Chenetal.,2019).Itis
| abbreviations, | and | unknown | characters) |     | was | removed, | and |     |     |     |     |     |     |     |
| -------------- | --- | ------- | ----------- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
necessarythatallentriesofWandHarenon-negative;otherwise,
tokenizationwasperformed.Followingthisstep,stemmingand
theinterpretationoftopicswithnegativevalueswouldbedifficult
| lemmatization | were | then conducted. |     | The | former | process | used |     |     |     |     |     |     |     |
| ------------- | ---- | --------------- | --- | --- | ------ | ------- | ---- | --- | --- | --- | --- | --- | --- | --- |
PorterStemmertoremovesuffixesfromwords(e.g.,investigating (LeeandSeung,1999).
|                  |         |     |        |      |         |            |     | Since | NMF requires | the | data | to be preprocessed, |     | necessary |
| ---------------- | ------- | --- | ------ | ---- | ------- | ---------- | --- | ----- | ------------ | --- | ---- | ------------------- | --- | --------- |
| to investigate), | whereas | the | latter | used | WordNet | Lemmatizer |     |       |              |     |      |                     |     |           |
stepstobeperformedbeforehandincludeaclassicalNLPpipeline
| to remove | inflectional | endings |     | and to | return | a word | to its |             |         |         |              |     |          |          |
| --------- | ------------ | ------- | --- | ------ | ------ | ------ | ------ | ----------- | ------- | ------- | ------------ | --- | -------- | -------- |
|           |              |         |     |        |        |        |        | containing, | amongst | others, | lowercasing, |     | stopword | removal, |
baseform(e.g.,investigatingtoinvestigate).Lastly,thetextwas
|     |     |     |     |     |     |     |     | lemmatizing | or stemming |     | as well | as punctuation |     | and number |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | --- | ------- | -------------- | --- | ---------- |
convertedintotermfrequency-inversedocumentfrequency(TF-
|     |     |     |     |     |     |     |     | removal | (Egger, 2022b). |     | For this study, | an  | open-source | Python |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | --------------- | --- | --------------- | --- | ----------- | ------ |
IDF)weightforinformationretrievalbasedontheimportanceof
library,Gensim,wasused(Islam,2019)toestimatetheoptimal
akeyword.
numberoftopics.Bycomputingthehighestcoherencescore,10
topicscouldbeidentified.
| Implementation                   |     | of  | Topic | Models |     |     |     |                |     |     |     |     |     |     |
| -------------------------------- | --- | --- | ----- | ------ | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | --- |
| Model1:LatentDirichletAllocation |     |     |       |        |     |     |     | Model3:Top2Vec |     |     |     |     |     |     |
LDA,themostpopulartopicmodelingtechnique,isagenerative Top2Vec (Angelov, 2020) is a comparatively new algorithm
probabilistic model for discrete datasets such as text corpora that uses word embeddings. That is, the vectorization of text
(Blair et al., 2020). It is considered a three-level hierarchical data makes it possible to locate semantically similar words,
Bayesian model, where each collection item is represented as a sentences,ordocumentswithinspatialproximity(Egger,2022a).
finite mixture over an underlying set of topics, and each topic For example, words like “mom” and “dad” should be closer
is represented as an infinite mixture over a collection of topic thanwordslike“mom”and“apple.”Inthisstudy,apretrained
probabilities. Hence, as the number of topics need not be pre- embedding models, the Universal Sentence Encoder, was used
defined(Maieretal.,2018),applyingLDAprovidesresearchers to create word and document embeddings. Since word vectors
FrontiersinSociology|www.frontiersin.org 4 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
FIGURE1|VisualinspectionofLDA.
| Finally, | the centroid | of  | the document | vectors | in  | the original |
| -------- | ------------ | --- | ------------ | ------- | --- | ------------ |
dimensionwascalculatedforeachdensearea,correspondingto
thetopicvector.
| Notably, | because | words | that | appear in | multiple | documents |
| -------- | ------- | ----- | ---- | --------- | -------- | --------- |
cannotbeassignedtoonesingledocument,theywererecognized
| by HDBSCAN        |     | as noise.   | Therefore, | Top2Vec         | does  | not require    |
| ----------------- | --- | ----------- | ---------- | --------------- | ----- | -------------- |
| any preprocessing |     | (e.g.,      | stopwords  | removal),       |       | or stemming    |
| and lemmatization |     | (Ma         | et al.,    | 2021; Thielmann |       | et al., 2021). |
| To conclude       |     | this model, | Top2Vec    | automatically   |       | provided       |
| information       | on  | the number  | of         | topics, topic   | size, | and words      |
representingthetopics.
FIGURE2|IntuitionofNMF.Source:Egger(2022b).
Model4:BERTopic
that emerge closest to the document vectors seem to best BERTopic (Grootendorst, 2020) builds upon the mechanisms
describe the topic of the document, the number of documents of Top2Vec; hence, they are similar in terms of algorithmic
that can be grouped together represents the number of topics structure.Asthenamesuggests,BERTisused asanembedder,
(Hendryetal.,2021). and BERTopic provides document embedding extraction, with
However, since the vector space usually tends to be sparse a sentence-transformers model for more than 50 languages.
(including mostly zero values), a dimension reduction was Similarly, BERTopic also supports UMAP for dimension
performedbeforedensityclustering.Byusinguniformmanifold reduction and HDBSCAN for document clustering. The main
approximation and projection (UMAP), the dimensions were difference between Top2Vec is the application of a class-
reduced to the extent that hierarchical density-based spatial based term frequency inverse document frequency (c-TF-IDF)
clusteringofapplicationswithnoise(HDBSCAN)couldbeused algorithm, which compares the importance of terms within a
to identify dense regions in the documents (Angelov, 2020). cluster and creates term representation (Sánchez-Franco and
FrontiersinSociology|www.frontiersin.org 5 May2022|Volume7|Article886498

| EggerandYu |     |     |     |     |     |           |         |       |     |              | ATopicModelingComparison |     |           |
| ---------- | --- | --- | --- | --- | --- | --------- | ------- | ----- | --- | ------------ | ------------------------ | --- | --------- |
|            |     |     |     |     |     | (Hannigan | et al., | 2019) | and | researchers’ | domain                   |     | knowledge |
(EggerandYu,2022).
Inthefollowingsection,acomparisonoftheobtainedresults
|     |     |     |     |     |     | will be | divided | into two | parts, | according | to  | the nature | of the |
| --- | --- | --- | --- | --- | --- | ------- | ------- | -------- | ------ | --------- | --- | ---------- | ------ |
algorithm:(1)LDAandNMFand(2)Top2VecandBERTopic.
|     |     |     |     |     |     | The latter | highlights |                | the term | search   | function | as     | one of the |
| --- | --- | --- | --- | --- | --- | ---------- | ---------- | -------------- | -------- | -------- | -------- | ------ | ---------- |
|     |     |     |     |     |     | pros of    | using a    | guided/seeding |          | approach | to delve | deeper | into a     |
specifictopic.
|     |     |     |     |     |     | Comparison |           | of          | LDA         | and NMF   |            |        |            |
| --- | --- | --- | --- | --- | --- | ---------- | --------- | ----------- | ----------- | --------- | ---------- | ------ | ---------- |
|     |     |     |     |     |     | Table1     | provides  | an overview |             | of the 14 | identified | topics | in the     |
|     |     |     |     |     |     | LDA model  | and       | the 10      | topics      | from      | NMF. Names |        | were given |
|     |     |     |     |     |     | based on   | the terms | that        | contributed |           | the most   | to     | a topic in |
referencetotheirTF-IDFweights.Overall,severalaspectspoint
|     |     |     |     |     |     | to common | themes,    | such | as  | expectations | toward     | government   |     |
| --- | --- | --- | --- | --- | --- | --------- | ---------- | ---- | --- | ------------ | ---------- | ------------ | --- |
|     |     |     |     |     |     | response, | discussion | on   | R   | values,      | and travel | restrictions | in  |
(t)
differentcountries.Taking“governmentresponse”asanexample,
tweetsseemtofocusonpeople’sexpectationstowardtheWhite
|     |     |     |     |     |     | House (e.g., | #whcovidresponse) |     |     | and | the US | president | (#potus, |
| --- | --- | --- | --- | --- | --- | ------------ | ----------------- | --- | --- | --- | ------ | --------- | -------- |
#vp).Althoughbothmodelsrefertothechancetoreunitewith
|     |     |     |     |     |     | their loved      | ones   | (e.g.,          | #loveisnottourism), |          | LDA,            | in         | particular, |
| --- | --- | --- | --- | --- | --- | ---------------- | ------ | --------------- | ------------------- | -------- | --------------- | ---------- | ----------- |
|     |     |     |     |     |     | points out       | how    | the COVID-19    |                     | pandemic | has             | influenced | the         |
|     |     |     |     |     |     | Diversity        | Visa   | Program         | (e.g.,              | #dv2021) | application.    |            | Likewise,   |
|     |     |     |     |     |     | while both       | models | disclose        |                     | Twitter  | users’ opinions |            | on travel   |
|     |     |     |     |     |     | ban restrictions |        | and quarantine, |                     | the      | LDA results     | appear     | to be       |
moregeographicallyoriented.Forinstance,whendiscussingthe
FIGURE3|BERTopic’sinteractiveintertopicdistancemap. reproductionnumber,Europeancountries,India,andtheUKare
|     |     |     |     |     |     | more frequently |        | mentioned. |          | On the | other hand, | England    | and    |
| --- | --- | --- | --- | --- | --- | --------------- | ------ | ---------- | -------- | ------ | ----------- | ---------- | ------ |
|     |     |     |     |     |     | Scotland        | appear | to be      | the main | focal  | point       | concerning | travel |
restrictions,andasfortweetsrelatedtoquarantine,LDAreveals
Rey-Moreno,2022).Thismeansthatthehigherthevalueisfor
issuessurroundingtheAustralianborder.
aterm,themorerepresentativeitisofitstopic.
|           |         |             |         |      |             | Still, | inspiteof | LDAperforming |     | seeminglybetterup |     |     | tothis |
| --------- | ------- | ----------- | ------- | ---- | ----------- | ------ | --------- | ------------- | --- | ----------------- | --- | --- | ------ |
| BERTopic, | similar | to Top2Vec, | differs | from | LDA because |        |           |               |     |                   |     |     |        |
point,themodelproducesmoreuniversalandirrelevanttopics
| it provides | continuous | rather | than | discrete | topic modeling |     |     |     |     |     |     |     |     |
| ----------- | ---------- | ------ | ---- | -------- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- |
that,atthesametime,barelyofferanymeaningfulimplications.
(Alcoforadoetal.,2022).Thestochasticnatureofthemodelthus
|     |     |     |     |     |     | This can | be evidenced |     | from | the final | four | LDA topics | listed |
| --- | --- | --- | --- | --- | --- | -------- | ------------ | --- | ---- | --------- | ---- | ---------- | ------ |
leadstodifferentresultswithrepeatedmodeling.Oncethemodel
|     |     |     |     |     |     | in Table1, | which, | based | on  | the keywords, |     | center | on travel |
| --- | --- | --- | --- | --- | --- | ---------- | ------ | ----- | --- | ------------- | --- | ------ | --------- |
iscomputed,researcherscanoutputthemostimportanttopics.
|     |     |     |     |     |     | and COVID-19 |     | on a | broader | level. Therefore, |     | despite | the fact |
| --- | --- | --- | --- | --- | --- | ------------ | --- | ---- | ------- | ----------------- | --- | ------- | -------- |
Notably,Topic0withacountof−1willalwaysrepresentoutliers
|     |     |     |     |     |     | that only | a few | NMF | topics | contain | country-specific |     | terms |
| --- | --- | --- | --- | --- | --- | --------- | ----- | --- | ------ | ------- | ---------------- | --- | ----- |
andshouldnotbeconsideredanyfurther.Researcherscanalso
|     |     |     |     |     |     | (e.g., New | Zealand, | India, | and | the UK), | its | value | should not |
| --- | --- | --- | --- | --- | --- | ---------- | -------- | ------ | --- | -------- | --- | ----- | ---------- |
searchforakeywordandreceivethemostimportanttopicsbased
|                     |       |          |           |                 |            | be underestimated. |         | Due      | to a | clear distinction |               | between | all the   |
| ------------------- | ----- | -------- | --------- | --------------- | ---------- | ------------------ | ------- | -------- | ---- | ----------------- | ------------- | ------- | --------- |
| on their similarity | score | along    | with      | the possibility | to inspect |                    |         |          |      |                   |               |         |           |
|                     |       |          |           |                 |            | identified         | topics  | in the   | NMF  | model,            | this research |         | concludes |
| individual topics   | based | on their | keywords. | Ultimately,     | in order   |                    |         |          |      |                   |               |         |           |
|                     |       |          |           |                 |            | that the           | results | obtained | from | NMF               | are more      | in      | line with |
tobetteranalyzethepotentiallylargearrayoftopics,BERTopic
|                       |     |            |          |     |                | human | judgment, | thereby | outperforming |     | LDA | in general. | Yet, |
| --------------------- | --- | ---------- | -------- | --- | -------------- | ----- | --------- | ------- | ------------- | --- | --- | ----------- | ---- |
| offers an interactive |     | intertopic | distance | map | for inspecting |       |           |         |               |     |     |             |      |
asmentionedabove,sincetopicextractionwithLDAandNMF
individualtopics(Grootendorst,2020).AsillustratedinFigure3,
|                 |          |     |            |         |               | relies primarily |     | on hyperparameters, |     |     | most | of the | results are |
| --------------- | -------- | --- | ---------- | ------- | ------------- | ---------------- | --- | ------------------- | --- | --- | ---- | ------ | ----------- |
| once an initial | overview | of  | the topics | becomes | available, an |                  |     |                     |     |     |      |        |             |
withinexpectation.Asbothmodels,however,donotallowforan
automatedtopicreductioncanbeperformedagain.
in-depthunderstandingofthephenomenon,thenextsectionwill
focusonthetopicmodelsthatuseembeddingrepresentations.
RESULTS
|     |     |     |     |     |     | Comparison |     | of  | BERTopic |     | and Top2Vec |     |     |
| --- | --- | --- | --- | --- | --- | ---------- | --- | --- | -------- | --- | ----------- | --- | --- |
In essence, although topic models bring in statistical analysis By relying on an embedding model, BERTopic and Top2Vec
andcanadvancesocialscienceresearch,eachofthealgorithms require an interactive process for topic inspection. As such,
has its own uniqueness and relies on different assumptions. both algorithms allow researchers to discover highly relevant
Quantitative methods are limited in their ability to provide topics revolving around a specific term for a more in-depth
in-depth contextual understanding, and the results cannot be understanding. Using Top2Vec for demonstration purposes,
comparedwithanysingle“value”(EggerandYu,2021).Thus,the this section begins with the intuition behind the search query.
interpretationofmodelsstillreliesheavilyonhumanjudgment Presuming that there is an interest in topics related to the
FrontiersinSociology|www.frontiersin.org 6 May2022|Volume7|Article886498

| EggerandYu |     |     |     | ATopicModelingComparison |     |
| ---------- | --- | --- | --- | ------------------------ | --- |
TABLE1|TopicsidentifiedbyLDAandNMF.
|                   | LDA      |               |     | NMF      |     |
| ----------------- | -------- | ------------- | --- | -------- | --- |
| No. Topic/content | Keywords | Topic/content |     | Keywords |     |
1 Governmentresponse ban,travelgov,potus,dv2021, Governmentresponse whcovidresponse,potus,
loveisnottourism,whcovidresponse,end,visa, loveisnottourism,cdcdirector,presssec,
|     | please,vp |     |     | vp,cdctravel,cdcgov,liftthetravelban, |     |
| --- | --------- | --- | --- | ------------------------------------- | --- |
cdctravelcdcdirector
2 AssociationforMolecular amp,travel,come,spread,mask,place,follow, AssociationforMolecular covid,travel,people,amp,want,covid
Pathology(AMP)/mask stay,keep,virus Pathology(AMP)/desireto travel,time,travelcovid,like,year
| andvirus |     | travel |     |     |     |
| -------- | --- | ------ | --- | --- | --- |
3 Rtvalue/India,UK,Europe rt,travel,country,India,uk,covid,government, Rtvalue rt,covid,travel,https,covid19,traveler,rt
|     | list,eu,news |     |     | ollysmithtravel,traveler,httpstco, |     |
| --- | ------------ | --- | --- | ---------------------------------- | --- |
ollysmithtravel
4 Travelrestriction/England travel,covid,restriction,city,team,England, Travelrestriction restriction,travelrestriction,covidtravel,
andScotland despite,event,expect,Scotland covid19travel,ease,covidrestriction,
travel,lift,covid19restriction,restrictionlift
5 Vaccination/border vaccinate,covid19,international,traveler, Travelban/IndiaandUK ban,India,travelban,travelIndia,uk,list,
betweenCanadaandthe travel,vaccination,Canada,border,US,fully country,bantravel,red,variant
USA
6 Quarantineandlockdown/ traveler,day,quarantine,variant,allow,return, Generalabouttravel/ covid19,travel,covid19travel,
Australia lockdown,Australia,break,two Canada international,travelcovid19,country,
pandemic,internationaltravel,vaccination,
Canada
7 COVID-19cases/USA case,new,travel,health,state,tourism,public, Vaccinationandquarantine vaccinate,fully,fullyvaccinate,vaccinate
|     | number,close,include |     |     | covid19,traveler,vaccinatetraveler, |     |
| --- | -------------------- | --- | --- | ----------------------------------- | --- |
traveler,quarantine,cdc,require
8 Flight/COVID-19test test,travel,need,positive,covid,flight, COVID-19cases/New case,new,covidcase,covid19case,new
negative,air,take,airport Zealand case,rise,Zealand,NewZealand,report,
casecovid19
9 Death/Florida covid,die,death,cause,florida,child,spike, COVID-19test test,covidtest,negative,positive,test
|     | shoot,traveler002,flu |     |     | travel,testpositive,PCR,covid19test, |     |
| --- | --------------------- | --- | --- | ------------------------------------ | --- |
day,result
10 ChinaandUSA travel,covid,call,china,business,2020, Vaccinationpass vaccine,covid19vaccine,covidvaccine,
|     | trump,usa,dr |     |     | passport,vaccinepassport,require, |     |
| --- | ------------ | --- | --- | --------------------------------- | --- |
vaccinetravel,dose,mandate,vaccination
| 11 UnspecificI | not,covid,vaccine,people,do,travel,get, |     |     |     |     |
| -------------- | --------------------------------------- | --- | --- | --- | --- |
make,still,would
| 12 UnspecificII | travel,may,covid,2,please,1,help,show,3, |     |     |     |     |
| --------------- | ---------------------------------------- | --- | --- | --- | --- |
pass
| 13 UnspecificIII | covid19,travel,due,pandemic,world,today, |     |     |     |     |
| ---------------- | ---------------------------------------- | --- | --- | --- | --- |
first,update,coronavirus,safe
| 14 UnspecificIV | covid,be,go,travel,time,get,want,one,year, |     |     |     |     |
| --------------- | ------------------------------------------ | --- | --- | --- | --- |
see
term“cancel”duringCOVID-19,theTop2Vecmodelproduces “couldn,”“pls,”“having,”“guys,”“am,”“sir,”“supposed,”“hopefully,”
relevant outputs (topics) based on the order of their cosine “me,” “excited,” “postpone,” “so,” “days,” “dad,” “paid,” “option,”
similarity (Ghasiya and Okamura, 2021). Specifically, cosine “customers,”“request,”“bihar,”“thanks,”“amount,”“due,”“waiting,”
similarity,rangingfrom0to1,measuresthesimilaritybetween “to,” “got,” “back,” “impossible,” “service,” “hours,” “complete,”
“before,”“wait,”“nice,”“valid,”“book”].
thesearchtermandatopic.Inthecaseofthisresearch,outof309
topics,thesimilarityofTopic10provedtobethehighest[0.50],
followedbyTopic20[0.37],Topic7[0.33],Topic123[0.32],and
|     |     | In order | to acquire an | overview of the importance | of each |
| --- | --- | -------- | ------------- | -------------------------- | ------- |
Topic57[0.30]. term,awordcloudcanbeproducedforbettervisualization(see
Thereafter,themostimportantkeywordsforeachindividual Figure4); but, ultimately, an inspection of individual tweets is
topiccanberetrieved.Forexample,thekeywordsforTopic10
alsohighlyrecommended.Forinstance,thefindingssuggestthat
includethefollowing: document20189(tweets:“@PaytmTravelFlight-AI380dated9th
April,2020(CanceledduetoCOVID).NoRefundsincethen[...]”)
[“refund,” “booked,” “ticket,” “cancelled,” “tickets,” “booking,” has a similarity score of 0.8518. This information allows one
“cancel,”“flight,”“my,”“hi,”“trip,”“phone,”“email,”“myself,”“hello,” to gain deeper insights directly from the raw data. Meanwhile,
FrontiersinSociology|www.frontiersin.org 7 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
As a final note, when inspecting the keywords of BERTopic
and Top2Vec, despite the redundancy of some terms (e.g.,
“travel bubble” and “travelbubble,” as they are very close in the
same vector-space), they can, in fact, provide valuable insights,
especiallyfortheprocessoftopicnaming.Mostly,thecontentofa
topiccanbeunderstoodbasedonfrequently-repeatedkeywords.
Moreover,regardingthelogicofthealgorithm,sinceBERTopic
FIGURE4|Exampleofawordcloudbasedontheterm“cancel.” and Top2Vec should not be preprocessed, conjunction words
(e.g., after, before to, from, at) are helpful for connecting the
context. However, a major drawback without preprocessing is
that (in)definite articles or be-verbs appearing in the keywords
listsareoftenmeaninglessincomprehendingatopic.
in order to find more suitable keywords based on “cancel” for
evenfurtheranalysis,wordsthataremostsimilarcanbeoutput
Hierarchical Topic Reduction of Top2Vec
with their similarity, such as “canceled [0.60],” “refund [0.49],”
“booked[0.47],”“due[0.46],”and“ticket[0.43].” and BERTopic
Following the search process, a topic comparison between Finally, it is worth noting that both Top2Vec and BERTopic
Top2VecandBERTopiccouldbeestablished.Thistime,“flight” allowforhierarchicalreduction.Echoingthisstudy’sresults,the
and “travel bubble” were taken as other examples. Since cosine number of extracted topics tends to be relatively large, thereby
similarityhaspreviouslybeenintroduced,thefollowingsection necessitatingtheneedforintensivequalitativeanalysis.Inorder
merely lists some of the keywords that facilitate topic naming. to streamline the analysis, the algorithms offer the possibility
As mentioned above, this is because the results require human to reduce these topics further (Angelov, 2020). Starting with
interpretationtomakesenseofthedata(Hanniganetal.,2019). Top2Vec,ahierarchicalreductiondownto10topicsistypically
Starting with “flight,” Table2 provides an overview, out of considered a good starting point to begin topic analysis. In the
the 343 identified topics, of the six most relevant ones taken case of this research, the 10 remaining clusters deducted from
from BERTopic and five, out of 253, from Top2Vec. Overall, the 253 original topics are presented in Table4. Significantly,
Top2Vec topics appear to be more policy- and regulation- the original vectors remain after topic reduction, meaning that
oriented, focusing on pre-departure testing requirements (e.g., representative topics with keywords can still be sought after at
negative PCR test and full vaccination) in countries such as anytime.
Mexico, the Netherlands, and Canada. It also discusses the Turning to BERTopic, since some of the topics are close
government’straveladviceforpublictransport,suchasintrains, in proximity, as could be observed in the intertopic distance
buses, and flights. For a more qualitative inspection, relevant map(Figure3),visualizationandtopicreductionwouldprovide
tweets can be reviewed; take, for example, “Kind attention dear a better understanding of how the topics truly relate to each
passengers traveling to [...] Please follow COVID-19 norms at other. To reduce the number of topics, hierarchical clustering
the airport. Fly safe!” and “[My] flight [got] canceled by airlines wasperformedbasedonthecosinedistancematrixbetweentopic
duetocovid.Alsomytravelinsurancepremiumwasted.”Onthe embeddings. This study thus took 100 topics as an example to
other hand, topics identified by BERTopic are more related to provide an overview of how and to which extent topics can be
the nature of air transport. Specifically, common issues shared reduced(Figure5).Level0ofthedendrogramdemonstrateshow
on Twitter include the airline industry, flight routes, returning similar topics (those with the same colors) have been clustered
home,transmissionthroughair,andairtravelassociations. together. For example, Topic 4 (vaccine passports) and Topic
Turning to “travel bubble,” both algorithms produced five 8 (the NHS COVID-19 app) were grouped together because of
relevant topics, as presented in Table3. In this case, the theiradjacency.Correspondingly,Topic6(wearingfacemasks)
BERTopic results seem to be more specific, with a clear and Topic 96 (mask mandate) were treated as part of the same
distinction on travel between Australia and New Zealand, cluster. In essence, a visualization as such can help researchers
SingaporeandHongKong,aswellasCanadaandMexico.Other to better comprehend the algorithm’s criteria by which topics
issues center on travel passes and business travel. With regards are organized. After reviewing the proposed topic structure,
to Top2Vec, however, the results revealed a slight overlap. For researcherscanthendecideonanumberoftopicsthatalsoseem
example,thetravelbubblebetweenAustraliaandNewZealand tobemorerealisticinaninteractivemanner.
iscoveredinfouroutoffivetopics;similarly,Singapore,Hong However, for both algorithms, the underlying meanings of
Kong,andTaiwanarealsomentionedseveraltimes.Inaddition, thetopicsarestillsubjecttohumaninterpretation.Nevertheless,
Top2Vecproducestopicswithmultipleaspects,whichbecomes althoughtheintuitionistoprovidethebestpossibleresults,an
especiallyapparentinthethirdandfourthtopics.Thethirdtopic optimalnumberoftopicscouldnotbeestablishedbecausemost
containsissuesrelatedtosixdifferentcountries(i.e.,HongKong, ofthetopicsoverlapwithoneanotherandcoveramixtureoftwo
Singapore,Australia,NewZealand,theUK,andthePhilippines), tothreedifferentaspects.Forinstance,theresultsfromTop2Vec
andthefourthincludesquarantineregulationsineightcountries (Table4) present five topics associated with the US Diversity
(i.e., Singapore, Australia, New Zealand, Taiwan, Hong Kong, Visaprogram(e.g.,dv,selecteesfault,winners,anexcuse,justice,
Korea,Hawaii,andIndonesia). interview, the petition, exam) and several terms related to
FrontiersinSociology|www.frontiersin.org 8 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
TABLE2|TopicsidentifiedbyBERTopicandTop2Vecfor“flight.”
BERTopic Top2Vec
No. Topic/content Examplesofkeywords Topic/content Examplesofkeywords
1 Airlineindustry airtravel,airline,airtravelis,airlines, NegativePCR/vaccinationand hoursbefore,pre-departure,negative
aviation,flights,theairlineindustry,the quarantine covid,alltravelers,fullyvaccinated,pcr,
airline,airlineindustry,flight quarantine,days,requirement,mandatory
2 Flightroutes flightsfrom,flights,directflights,flights WhiteHouseSecretaryTests secretary,simon,house,white,tested
fromindia,canadaeyespolicy,canada Positive/travelguidefrom positive,travelguidelines,cdc,mps,
eyes,indiatocanada,tocanada,banon governmentalinstitution travelers,tofollow
direct,asindiacovid19
3 (Unable)toreturnhome/ australians,travelban,flyhome,flyhome NegativePCR/fullyvaccinated negativecovid,fullyvaccinated,foreign
Australian from,whoflyhome,whofly,toaustralia, beforedeparture/foreign travelers,predeparture,hoursbefore,
australianswhofly,covidtravelban,travel travelers/Mexico requiredto,beforeyou,toenter,pcr,
ban mexico
4 COVIDtransmissionthroughair theair,aerosols,droplets,air,airborne, NegativePCR/fullyvaccinated negativecovid,departure,hoursbefore,
covidtravels,throughtheair,virustravels, beforedeparture/foreign internationaltravelers,fullyvaccinated,
howcovidtravels,covidtravelsthrough travelers/theNetherlandsand biden,theunited,requirement,
Canada netherlands,canadians
5 AirportsAuthorityofIndia(AAI)/ aai,airports,aaiairports,airport,the Followtravelguidelinesonpublic train,bus,whiletraveling,covid
India airport,flights,aaiis,airportsare,fromaai, transport(train/bus/flight)/ appropriate,moreinformation,tofollow,
airtraffic seekhelpandmoreinfo covidguidelines,mandatory,byair,please
help
6 Airportnews newsairportairtravel,airtravelcovid19
covid19india,airportairtravel,airport
airtravelcovid19,travelersnewsairport,
airtravelcovid19,travelcovid19,flight
travelcovid19,airtravelassociations,
airportsair
TABLE3|TopicsidentifiedbyBERTopicandTop2Vecfor“travelbubble.”
BERTopic Top2Vec
No. Topic/content Examplesofkeywords Topic/content Examplesofkeywords
1 AustraliaandNewZealand travelbubble,travelbubblewith,thetravel AustraliaandNewZealand/ sydney,victoria,queensland,australia,
bubble,australiatravelbubble, quarantinehotel hotelquarantine,nz,inhotel,quarantine
zealandaustraliatravelbubble,new free,lockdown,auckland
zealandaustraliatravel,zealandtravel,
zealandtravelbubble,bubblewith
australia,aftertravelbubble
2 SingaporeandHongKong bubble,travelbubble,singapore,airtravel AustraliaandNewZealand/ zealand,quarantinefree,singapore,hotel
bubble,travelbubbleis,bubbleis, Singapore/Taiwan/vaccinated quarantine,2weeks,isolate,vaccinated
singaporehongkongair,singaporehong travelers,lockdown,melbourne,Taiwan
kong,breakingsingaporehongkong,as
singaporebattles
3 Travelpass travelpass,covidtravelpass,euscovid HongKongandSingapore/ hongkong,singapore,zerocovid,taiwan,
travel,euscovid,theeuscovid,covid AustraliaandNewZealand/ greenlist,australia,vaccinatedtravelers,
travel,summertravel,travelpasses,travel greenlist/vaccinated/UK/ philippines,zealand,businesstravel
passesas,launchcovidtravel Philippines
4 Nonessentialtravel/Canadaand canadaandmexico,onnon-essential Quarantinefree/Singapore/ quarantinefree,singapore,hk,auckland,
Mexicoferry/spreadof travel,nonessentialtravelat,nonessential AustraliaandNewZealand/ taiwan,korea,sydney,hawaii,indonesia,
COVID-19 travel,ferrycrossings,crossingswith Taiwan/HongKong/Korea/ vaccinatedtravelers
canada,ferrycrossingswith,landand Hawaii/Indonesia
ferry,andferrycrossings,spreadof
covid19
5 Businesstravel businesstravel,tourism,travelindustry, Singapore/HongKong/ taiwan,singapore,hongkong,business
thetravelindustry,tourismindustry,and Australia/Taiwan/fully travel,zealand,australia,fullyvaccinated,
tourism,travelandtourism,andtourism vaccinated/greenlist portugal,greenlist,israel
industry,traveland,tourismindustrythe
FrontiersinSociology|www.frontiersin.org 9 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
TABLE4|HierarchicaltopicreductionofTop2Vec.
No. Topic/content Examplesofkeywords
1 Diversityvisa/Studentlife byron,selecteesfault,bay,mask,areincreasing,student,theflu,exams,forever,
firstwave,take,traveling,covidpositive,there,hands,rapidly,want,big,stop,
death,interstate,fucking,haven,market,transmission,covidappropriate,bihar,
towear,short,exam,increasing
2 Diversityvisaandvisapetition/freedom/ thepetition,sign,testsfor,pcrcovid,selecteesfault,boris,ford,ontario,want,
internationaltravel/COVID-19curfew curfew,premier,theairport,free,friend,trudeau,postpone,checkout,rapidly,
pakistan,shot,uk,enjoy,stayat,true,thread,toronto,travelinsurance,
internationaltravel,normal,manycountries,variants,overseastravel,freedom,
mps,interstate,redlist,folks,canadians,reasons,province,bihar
3 Diversityvisa/unvaccinatedpeople/ selecteesfault,centersfor,di,disease,white,labor,fauci,economy,behavior,
vaccinatetoprevent million,notbeing,market,shame,europeans,kerala,americans,control,here
are,millionsof,trump,unvaccinated,buy,weekend,makesure,oct,and
tourism,dv,jobs,toprotect,shop,thisweekend,ofvaccination,concerns,for
your,airtravel,nextmonth,vaccines,open,toease,political,millions,virus,
prevention,cover,plansto,science,mexico,tourism
4 Politicians(GrantShapps,JustinTrudeau, onvaccination,eu,covidcertificate,requirementfor,ban,bordersto,biden,
Biden,Trump,AnthonyFauci)/greenlist grant,shapps,president,evenworse,chinese,olympics,trudeau,european,
countries/internationaltravelfor requiredfor,digital,vaccinatedtravelers,fauci,manycountries,justice,
vaccinatedpeople/olympics/COVID-19 vaccinatedtravelers,travelpass,visas,othercountries,trump,thefederal,
passport countries,australians,greenlist,law,infected,joe,theborder,forfully,interstate
travel,europe,open,nextmonth,covidpassports
5 Pre-COVIDandfirstwave/dreamingof firstwave,shelby,battle,solutions,simon,theyfind,theemergence,their
travel journey,countless,lives,future,someone,human,money,anexcuse,traveling,
love,beforecovid,dose,happy,traveled,pfizer,fromchina,dream,together,
selecteesfault,diedof
6 ComplaintstowardtheUSDiversityVisa anexcuse,toolset,selecteesfault,evenworse,onvaccination,uganda,death,
Lotteryprogram(COVID-19asanexcuse justice,pcrtests,newcases,arabia,interview,thehighest,unitedstates,fun,
forthedelayorcancellationthereof) winners,crazy,forfully,forforeign,nepal,imple,clear,african,nigeria,business
travel,puertorico,brexit,theairport,requiring,singapore
7 YellowfeverandCOVID-19vaccine/ saudi,astrazeneca,journey,arabia,staysafe,newcases,covidnumbers,dose
SaudiArabia/COVID-19cases of,nhscovid,wave,wearmask,gotcovid,yellowfever,pass,app,precovid,
doctors,eastern
8 TravelDestinations/Prevention/Travel dv,selecteesfault,blaming,lanka,covidappropriate,rapidly,european,
Measures solutions,union,theyfind,theemergence,winners,traveladvisory,increase,
nepal,prevention,thedelta,travelmeasures,covidcases,shelby,surgein,level,
donot,newcases,travelrelated,eu,probably,hawaii,postpone,indian,to
restrict,battle,florida,areincreasing,risingcovid,olympics,governor
9 NegativePCRtestpriortodeparture/fully proofof,departure,hoursbefore,covidappropriate,aslong,willneed,covid
vaccinatedforinternationaltravel testing,negativecovid,befully,predeparture,toshow,requirementfor,you
must,requiredto,byair,foreigntravelers,testfor,covidtest,behavior,
vaccinatedagainst,test,pcrtest,pcrtests,arrival,fullyvaccinated,on
vaccination,requirement,ofvaccination,negativetest,pcr,vaccination,
negative,arefully,cdc,required,forinternational,requirementsfor,distancing,to
require,guidance,onarrival,daysof
10 Travelbubble/Australia(severalcities nsw,queensland,sydney,victoria,havetested,coast,shelby,melbourne,travel
included)andNewZealand/HongKong/ bubble,zealand,quarantinefree,australia,inhotel,positivefor,simon,wales,
Scotland/quarantinefree/quarantine traveledfrom,kong,covidcase,positivecovid,battle,testedpositive,firstwave,
hotel vic,greater,auckland,woman,theirjourney,byron,thepetition,hotelquarantine,
scotland,south,army
politicians based in the USA and Canada (e.g., Grant Shapps, process contains errors, and it may be quite labor-intensive to
Justin Trudeau, Joe Biden, Donald Trump, Anthony Fauci). findanumberthatfitshumanjudgment.
Similarly, making sense of the hierarchical clustering produced As shown in Figure5 below, the dendrogram produced by
by BERTopic (Figure5) also requires an enormous effort since BERTopic shows the agglomeration levels of the individual
the topic structure changes whenever researchers experiment topics. This visualization, in particular, aids in finding an
withadifferentnumberoftopics.Despitethepossibilityofusing appropriate number of k-topics. Furthermore, similar to
existingdomainknow-howtosearchforspecifictopics,afeature Top2Vec, a table with keywords is obtained after fusing the
that is inexistent in other traditional algorithms, researchers topics; yet, it is also highly recommended to inspect individual
should be well aware of the aforementioned issues. The overall rawdocumentsformoreappropriateinterpretations.
FrontiersinSociology|www.frontiersin.org 10 May2022|Volume7|Article886498

| EggerandYu |     |     |     |     | ATopicModelingComparison |     |
| ---------- | --- | --- | --- | --- | ------------------------ | --- |
FIGURE5|HierarchicalreductioninBERTopic.
| DISCUSSION AND | CONCLUSION |     |     |     |     |     |
| -------------- | ---------- | --- | --- | --- | --- | --- |
“standard.”Contrarily,inadditiontotheexpectedoutcomes(i.e.,
|     |     |     | topics), BERTopic | was able to | generate novel | insights using its |
| --- | --- | --- | ----------------- | ----------- | -------------- | ------------------ |
Baring the difficulties of extracting useful information from embedding approach. Although Top2Vec also uses pretrained
| short and unstructured | texts in mind, | this research | intends |     |     |     |
| ---------------------- | -------------- | ------------- | ------- | --- | --- | --- |
embeddingmodels,theresultscovermoretopicsthatoverlapand
to confront such challenges by comparing the results of four contain multiple concepts. On the other side of the spectrum,
topic modeling algorithms. For an overall evaluation based similar to NMF, the topics produced by LDA do not seem to
| on human interpretation, | this study | supports the | potency             |               |              |                |
| ------------------------ | ---------- | ------------ | ------------------- | ------------- | ------------ | -------------- |
|                          |            |              | be very intriguing, | either. Thus, | despite some | Top2Vec topics |
of BERTopic and NMF, followed by Top2Vec and LDA, in appearing as irrelevant and difficult to understand, the model,
analyzing Twitter data. While, in general, both BERTopic and evenso,iscapableofproducingafewinterestingfindingsrarely
NMF provide a clear cut between any identified topics, the mentionedbyotheralgorithms(e.g.,politicians).Asaresult,in
results obtained from NMF can still be considered relatively favorofextractingnovelconclusions,thisresearchrecommends
FrontiersinSociology|www.frontiersin.org 11 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
Top2VecoverLDA.Toprovideamoresolidfoundationforthese thedocumentmaynotbeidentifiedseparately(Campbelletal.,
reasonings, a detailed evaluation for each algorithm will now 2015), thereby resulting in overlapping clusters (Passos et al.,
begiven. 2011). In opposition, other scholars believe that insufficient
Firstandforemost,comparedtoothertechniques,BERTopic statisticalinformation for feature extractionisthefundamental
works exceptionally with pretrained embeddings (Sánchez- factorbehindduplicatetopics(Caietal.,2018).
Franco and Rey-Moreno, 2022) due to a split between Lastly, when comparing BERTopic to NMF, a major
clustering the documents and using c-TF-IDF to extract topic shortcoming of NMF revolves around its low capability to
representations. Especially owing to the c-TF-IDF procedure identify embedded meanings within a corpus (Blair et al.,
(AbuzayedandAl-Khalifa,2021),BERTopiccansupportseveral 2020).Consideringthatthealgorithmdependsprimarilyonthe
topic modeling variations, such as guided topic modeling, Frobeniusnorm(Chenetal.,2019),whichistypicallyusefulfor
dynamic topic modeling, or class-based topic modeling. Its numericallinearalgebra,thisissueultimatelyleadstodifficulties
main strength lies in the fact that the algorithm performs ininterpretingfindings(WangandZhang,2021).ThoughNMF
well on most aspects of the topic modeling domain, whereas caneffectivelyanalyzenoisydata(Blairetal.,2020),othersargue
others typically excel in one single aspect. Additionally, thataccuracycannotbeguaranteed(Albalawietal.,2020).
after having trained a BERTopic model, it is also possible Based on the outcomes of this study, as discussed above,
to reduce the number of topics (Sánchez-Franco and Rey- Table5 summarizes the pros and cons of applying LDA,
Moreno, 2022), subsequently allowing researchers to settle NMF, BERTopic, and Top2Vec in order to help facilitate
on a number of (realistic) topics based on how many were social scientists in the necessary preprocessing steps, proper
actuallyproduced. hyperparametertuning,andcomprehensibleevaluationoftheir
SlightlydifferentfromBERTopicandtheimplementationof results. However, researchers should take into account that,
c-TF-IDF, Top2Vec creates jointly embedded word, document, depending on the nature of the datasets, topic models may not
andtopicvectorstofindtopicdescriptions(Angelov,2020).The alwaysperforminthesamefashion(EggerandYu,2021).
intuitionbehindthisalgorithmisthateveryinputisconsidereda
vector,andpivotingbetweenthemistrivial.Hence,Top2Veccan Theoretical and Practical Contributions
scalealargenumberoftopicsandvastquantitiesofdata.Such Inlightoftheexpansionofuser-generatedcontent,socialmedia
strength is especially required when multiple languages emerge hasbroadenedthehorizonsforhumaninteractionandprovoked
withinacorpus(Hendryetal.,2021).Themaindisadvantageof new phenomena and social research for further investigation
Top2Vec,however,isthatitisunqualifiedtoworkwithasmall (Murthy, 2012; Rizvi et al., 2019; Boccia Artieri et al., 2021).
amount of data (Abuzayed and Al-Khalifa, 2021; e.g., <1,000 Althoughseveralrecentstudieshavevouchedfortheexploration
documents). In fact, BERTopic and Top2Vec have a number ofshort-textsocialmediadata(Albalawietal.,2020;Qiangetal.,
of issues in common. For example, although outlier generation 2020), existing knowledge is rather restricted to conventional
might be beneficial in some cases, the solutions might actually modeling techniques such as LDA and LSA (Albalawi et al.,
generate more outliers than expected. Meanwhile, another flaw 2020). As the evolution of topic modeling has given rise to
involves topic distributions: they cannot be generated within a noveltechniques,especiallyonesthathaverarelybeenappliedor
single document because eachdocument isassignedto asingle evaluatedinsocialscience,thisstudyisvaluableinthatitanswers
topic. Although probabilities can indeed be extracted, they are the call to assess topic modeling via a thorough comparison of
notequivalenttoanactualtopicdistribution. fourdifferentalgorithms(ReisenbichlerandReutterer,2019).In
With regards to NMF and LDA, notwithstanding that both addition, this research scrutinizes the bright and dark sides of
algorithmsdonotrequiresocialscientiststohavepriordomain applyingembeddedvs.standardtopicmodels,butitalsooffers
knowledge,severaltopicsidentifiedbyLDAinthisstudyyielded socialscienceresearchersinsightsintomethodologicalchallenges
either universal (Rizvi et al., 2019) or irrelevant (Alnusyan thatmayhinderknowledgegeneration.
etal.,2020)piecesofinformation.Suchanissuefurtherreflects Foreseeingthatsocialscientistsmayindeedhesitatetochoose
the study’s findings of LDA being indeterministic (Egger and anappropriatealgorithmwhenanalyzingsocialmediadata,this
Yu, 2021). In order to achieve optimal results, LDA usually studypresentspossiblemethodologicalissuesandpromotesthe
requires detailed assumptions concerning the hyperparameters; efficacy of two different types of topic models. To be more
inparticular,discoveringtheoptimalnumberoftopicstypically precise,applyingBERTopictogenerateinsightsfromshortand
proves to be a difficult task (Egger and Yu, 2021). Although unstructured text offers the most potential when it comes to
NMF shares the same disadvantages, it can be assumed that embedding-based topic models. Thus, this study acknowledges
NMF puts forward better results since the algorithm relies on the capability of BERTopic to encode contextual information
TF-IDF weighting rather than raw word frequencies (Albalawi (ChongandChen,2021),anaspectthatmayremainconcealed
etal.,2020).Simultaneously,asalinear-algebraicmodel,scholars byothermodels.Regardingtraditionaltopicmodelalgorithms,
commonlyagreethatNMFworkswellwithshortertexts(Chen social science research is encouraged to consider NMF as an
et al., 2019), such as tweets. Since no prior knowledge is alternativeapproachtothecommonly-adoptedLDA(Gallagher
neededfortopicextraction(Albalawietal.,2020),thisstrength etal.,2017).Certainly,however,itisessentialtonotethateach
specifically benefits research based on social media data (Blair modelhasitsownstrengthsandshortcomings,andthefindings
et al., 2020). Additionally, as LDA extracts independent topics require intensive qualitative interpretation. Finally, this study
from word distributions, topics that are deemed dissimilar in alsostrivestomakeanotherimportantcontributionbyoutlining
FrontiersinSociology|www.frontiersin.org 12 May2022|Volume7|Article886498

| EggerandYu |     |     |     |     |     | ATopicModelingComparison |     |
| ---------- | --- | --- | --- | --- | --- | ------------------------ | --- |
TABLE5|Comparisonoftopicmodels.
|     | Advantages |     |     | Disadvantages |     |     |     |
| --- | ---------- | --- | --- | ------------- | --- | --- | --- |
LDA • Priordomainknowledgeisnotnecessarilyrequired • Detailedassumptionsarerequired
• Findscoherenttopicswhencorrecthyperparameter • Hyperparametersneedtobetunedcarefully
tuningisapplied • Results can easily produce overlapping topics as topics are soft
|     | • Candealwithsparseinput |     |     | clusters |     |     |     |
| --- | ------------------------ | --- | --- | -------- | --- | --- | --- |
• Thenumberoftopicsisgenerallysmallerthan • Objectiveevaluationmetricsarewidelymissing
word-embeddingbasedapproaches;thus,itiseasier • Thenumberoftopicsneedstobedefinedbytheuser(s)
tobeinterpreted • Sincetheresultsarenotdeterministic,reliabilityandvalidityarenot
|     | • Onedocumentcancontainseveraldifferenttopics |     |     | automaticallyensured |     |     |     |
| --- | --------------------------------------------- | --- | --- | -------------------- | --- | --- | --- |
(Mixedmembershipextraction) • Assumesthatthetopicsareindependentofeachother;hence,only
• Fullgenerativemodelswithmultinominaldistribution thefrequencyofthecommonoccurrenceofwordsisused
overtopicsaregenerated • Wordcorrelationsareignored,sonorelationshipsbetweentopics
|     | • Showsbothadjectivesandnounswithintopics |     |     | canbemodeled |     |     |     |
| --- | ----------------------------------------- | --- | --- | ------------ | --- | --- | --- |
NMF • Priordomainknowledgeisnotrequired • Frequentlydeliversincoherenttopics
• Supportsmixedmembershipmodels;thus,one • Thenumberoftopicstobeextractedmustbedefinedbytheuserin
|     | documentcancontainseveraltopics |     |     | advance |     |     |     |
| --- | ------------------------------- | --- | --- | ------- | --- | --- | --- |
• IncontrasttoLDA,whichusesrawwordfrequencies, • Implicitspecificationofprobabilisticgenerativemodels
theterm-documentmatrixcanbeweightedwith
TF-IDF
• Itprovestobecomputationallyefficientandvery
scalable
• Easytoimplement
Top2Vec • Supportshierarchicaltopicreduction • Theembeddingapproachmightresultintoomanytopics,requiring
• Allowsformultilingualanalysis labor-intensiveinspectionofeachtopic
|     | • Automaticallyfindsthenumberoftopics |     |     | • Generatesmanyoutliers |     |     |     |
| --- | ------------------------------------- | --- | --- | ----------------------- | --- | --- | --- |
Notverysuitableforsmalldatasets(<1,000)
|     | • Createsjointlyembeddedword,document,andtopic |     |     | •                                  |     |     |     |
| --- | ---------------------------------------------- | --- | --- | ---------------------------------- | --- | --- | --- |
|     | vectors                                        |     |     | • Eachdocumentisassignedtoonetopic |     |     |     |
• Containsbuilt-insearchfunctions(easytogofrom • Objectiveevaluationmetricsaremissing
topictodocuments,searchtopics,etc.)
• Canworkonverylargedatasetsizes
• Itusesembeddings,sonopreprocessingofthe
originaldataisneeded
BERTopic • Highversatilityandstabilityacrossdomains • Theembeddingapproachmightresultintoomanytopics,requiring
• Allowsformultilingualanalysis labor-intensiveinspectionofeachtopic
|     | • Supportstopicmodelingvariations(guidedtopic |     |     | • Generatesmanyoutliers |     |     |     |
| --- | --------------------------------------------- | --- | --- | ----------------------- | --- | --- | --- |
modeling,dynamictopicmodeling,orclass-based • Notopicdistributionsaregeneratedwithinasingledocument;rather,
|     | topicmodeling) |     |     | eachdocumentisassignedtoasingletopic |     |     |     |
| --- | -------------- | --- | --- | ------------------------------------ | --- | --- | --- |
• Itusesembeddings,sonopreprocessingofthe • Objectiveevaluationmetricsaremissing
originaldataisneeded
• Automaticallyfindsthenumberoftopics
• Supportshierarchicaltopicreduction
• Containsbuilt-insearchfunctions(easytogofrom
topictodocuments,searchtopics,etc.)
• BroadersupportofembeddingmodelsthanTop2Vec
guidedmodelingsolutionsthatcanbeappliedbysocialscientists selectedduetoitsstrictregulationsonthenumberofcharacters
todataanalyticsforknowledgeextraction. allowed per tweet, making it an ideal platform for exploratory
research.Nonetheless,themethodologicalapproachinthisstudy
Limitations and Recommendations for shouldbeapplicabletootherchannelsaswellsincesocialmedia
| Future Research |     |     |     |                    |           |                  |                |
| --------------- | --- | --- | --- | ------------------ | --------- | ---------------- | -------------- |
|                 |     |     |     | posts, in general, | are short | and unstructured | (Kasperiuniene |
Thisresearchiscertainlynotwithoutitslimitations.Whilethis et al., 2020). However, it is still critical to note that the nature
|               |            |                |                 | of social media | differs in | terms of user | demographics, text |
| ------------- | ---------- | -------------- | --------------- | --------------- | ---------- | ------------- | ------------------ |
| studyresponds | toa needto | utilizeTop2Vec | andBERTopic for |                 |            |               |                    |
the analysis of short-text data (Egger and Yu, 2021; Sánchez- presentation,orrhetoric,amongstothers.Thus,futureresearch
FrancoandRey-Moreno,2022),novellanguagemodels,suchas should continue to explore the effectiveness of topic modeling
GPT3andWuDao2.0,havecontinuedtoemergeastimepasses algorithms across other platforms. Lastly, acknowledging the
|             |                       |                 |                | epistemological | challenges | of big data is | also of importance; |
| ----------- | --------------------- | --------------- | -------------- | --------------- | ---------- | -------------- | ------------------- |
| (Nagisetty, | 2021), thereby acting | as an excellent | basis for even |                 |            |                |                     |
more powerful topic modeling approaches. To leverage the use regardless of the massive volumes of data that may appear
of topic modeling methods, social scientists are encouraged to tempting at face value, algorithms should be contextualized in
|     |     |     |     | a particular | social framework | (Egger and Yu, | 2022). Although |
| --- | --- | --- | --- | ------------ | ---------------- | -------------- | --------------- |
tryandevaluateothernewlydevelopedalgorithmsandtokeep
theirknowledgeuptodate.Inthecaseofthisstudy,Twitterwas topic models have quantified short-text social media data, both
FrontiersinSociology|www.frontiersin.org 13 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
the interpretation and justification of the results come at the material, further inquiries can be directed to the
expenseofdataaccuracy.Beingequippedwithextensivedomain correspondingauthor.
knowledgeindata-drivenscience(Canali,2016)wouldtherefore
allow social scientists to transform quantitative analytics into AUTHOR CONTRIBUTIONS
valuableinsightsforknowledgeacquisition.
RE collected and analyzed the data. JY wrote the manuscript
DATA AVAILABILITY STATEMENT in consultation with RE and interpreted the data. Both authors
designed the study and were responsible for the overall
The original contributions presented in the managementandplanning.Allauthorscontributedtothearticle
study are included in the article/supplementary andapprovedthesubmittedversion.
REFERENCES
Chen, Y., Zhang, H., Liu, R., Ye, Z., and Lin, J. (2019). Experimental
explorations on short text topic mining between LDA and NMF based
Abuzayed, A.,and Al-Khalifa,H.(2021).BERTforArabic topic modeling: an Schemes. Knowl. Based Syst. 163, 1–13. doi: 10.1016/j.knosys.2018.
experimentalstudyonBERTopictechnique.Proc.Comput.Sci.189,191–194. 08.011
doi:10.1016/j.procs.2021.05.096 Chong,M.,andChen,H.(2021).Racistframingthroughstigmatizednaming:
Albalawi, R., Yeap, T. H., and Benyoucef, M. (2020). Using topic modeling a topical and geo-locational analysis of #Chinavirus and #Chinesevirus
methodsforshort-textdata:acomparativeanalysis.Front.Artif.Intellig.3:42. on Twitter. Proc. Assoc. Inform. Sci. Technol. 58, 70–79. doi: 10.1002/
doi:10.3389/frai.2020.00042 pra2.437
Alcoforado,A.,Ferraz,T.P.,Gerber,R.,Bustos,E.,Oliveira,A.S.,Veloso,B. Egger, R. (2022a). “Text representations and word embeddings. Vectorizing
M.,etal.(2022).ZeroBERTo-leveragingzero-shottextclassificationbytopic textual data,” in Applied Data Science in Tourism. Interdisciplinary
modeling.arXiv[Preprint].arXiv:2201.01337.Cham:Fortaleza,Portugaland Approaches,MethodologiesandApplications,edR.Egger(Berlin:Springer),16.
Springer.Availableonlineat:http://arxiv.org/pdf/2201.01337v1 doi:10.1007/978-3-030-88389-8_16
Alnusyan, R., Almotairi, R., Almufadhi, S., Shargabi, A. A., and Alshobaili, Egger, R. (2022b). “Topic modelling. Modelling hidden semantic structures
J. (2020). “A semi-supervised approach for user reviews topic in textual data,” in Applied Data Science in Tourism. Interdisciplinary
modeling and classification,” in 2020 International Conference on Approaches,MethodologiesandApplications,edR.Egger(Berlin:Springer),18.
Computing and Information Technology (Piscataway, NJ: IEEE), 1–5. doi:10.1007/978-3-030-88389-8_18
doi:10.1109/ICCIT-144147971.2020.9213721 Egger, R., Pagiri, A., Prodinger, B., Liu, R., and Wettinger, F. (2022).
Anderson,C.(2008).TheEndofTheory:TheDataDelugeMakestheScientific “Topic modelling of tourist dining experiences based on the GLOBE
Method Obsolete. Available online at: https://www.wired.com/2008/06/pb- model,” in ENTER22 e-Tourism Conference (Berlin: Springer), 356–368.
theory/(accessedFebruary1,2022). doi:10.1007/978-3-030-94751-4_32
Angelov, D. (2020). Top2Vec: Distributed Representations of Topics. Available Egger, R., and Yu, J. (2021). Identifying hidden semantic structures in
onlineat:http://arxiv.org/pdf/2008.09470v1(accessedFebruary12,2022). Instagram data: a topic modelling comparison. Tour. Rev. 2021:244.
Arefieva, V., Egger, R., and Yu, J. (2021). A machine learning approach doi:10.1108/TR-05-2021-0244
to cluster destination image on Instagram. Tour. Manag. 85:104318. Egger, R., and Yu, J. (2022). “Epistemological challenges,” in Applied Data
doi:10.1016/j.tourman.2021.104318 Science in Tourism. Interdisciplinary Approaches, Methodologies and
Ariffin, S. N. A. N., and Tiun, S. (2020). Rule-based text normalization Applications, ed R. Egger (Berlin: Springer), 2. doi: 10.1007/978-3-030-883
for Malay Social Media Texts. Int. J. Adv. Comput. Sci. Appl. 11:21. 89-8_2
doi:10.14569/IJACSA.2020.0111021 Elragal, A., and Klischewski, R. (2017). Theory-driven or process-driven
Bi, J.-W., Liu, Y., Fan, Z.-P., and Cambria, E. (2019). Modelling customer prediction?Epistemologicalchallengesofbigdataanalytics.J.BigData4:2.
satisfaction from online reviews using ensemble neural network doi:10.1186/s40537-017-0079-2
and effect-based Kano model. Int. J. Prod. Res. 57, 7068–7088. Femenia-Serra, F., Gretzel, U., and Alzua-Sorzabal, A. (2022). Instagram
doi:10.1080/00207543.2019.1574989 travel influencers in #quarantine: communicative practices and roles
Blair, S. J., Bi, Y., and Mulvenna, M. D. (2020). Aggregated topic models during COVID-19. Tour. Manag. 89:104454. doi: 10.1016/j.tourman.2021.
for increasing social media topic coherence. Appl. Intellig. 50, 138–156. 104454
doi:10.1007/s10489-019-01438-z Gallagher,R.J.,Reing,K.,Kale,D.,andVerSteeg,G.(2017).Anchoredcorrelation
Boccia Artieri, G., Greco, F., and La Rocca, G. (2021). The construction explanation:topicmodelingwithminimaldomainknowledge.Trans.Assoc.
of the meanings of #coronavirus on Twitter: an analysis of the Comput.Linguist.5,529–542.doi:10.1162/tacl_a_00078
initial reactions of the Italian people. Int. Rev. Sociol. 31, 287–309. Ghasiya,P.,andOkamura,K.(2021).InvestigatingCOVID-19newsacrossfour
doi:10.1080/03906701.2021.1947950 nations: a topic modeling and sentiment analysis approach. IEEE Access 9,
Bradley, S. D., and Meeds, R. (2002). Surface-structure transformations and 36645–36656.doi:10.1109/ACCESS.2021.3062875
advertising slogans: the case for moderate syntactic complexity. Psychol. Grootendorst, M. (2020). BERTopic: Leveraging BERT and c-TF-IDF to Create
Market.19,595–619.doi:10.1002/mar.10027 EasilyInterpretableTopics.Zenodo.doi:10.5281/zenodo.4430182
Cai, G., Sun, F., and Sha, Y. (2018). Interactive Visualization for Topic Model Grootendorst,M.(2022).BERTopic:NeuralTopicModelingWithaClass-BasedTF-
Curation.Tokyo:IUIWorkshops. IDFProcedure.arXiv:2203.05794v0571.Availableonlineat:https://arxiv.org/
Cai, T., and Zhou, Y. (2016). What should sociologists know about big data? pdf/2203.05794.pdf(accessedMarch15,2022).
ISAeSymposium6,1–9.Availableonlineat:https://esymposium.isaportal.org/ Guo, Y., Barnes, S. J., and Jia, Q. (2017). Mining meaning from online
resources/resource/what-should-sociologists-know-about-big-data/ ratings and reviews: tourist satisfaction analysis using latent dirichlet
Campbell,J.C.,Hindle,A.,andStroulia,E.(2015).LatentDirichletallocation: allocation. Tour. Manag. 59, 467–483. doi: 10.1016/j.tourman.2016.09
extractingtopicsfromsoftwareengineeringdata.ArtSci.Anal.Softw.Data9, .009
139–159.doi:10.1016/B978-0-12-411519-4.00006-9 Hannigan, T. R., Haans, R. F. J., Vakili, K., Tchalian, H., Glaser, V. L.,
Canali, S. (2016). Big Data, epistemology and causality: knowledge in Wang, M. S., et al. (2019). Topic modeling in management research:
and knowledge out in EXPOsOMICS. Big Data Soc. 3:205395171666953. rendering new theory from textual data. Acad. Manag. Ann. 13, 586–632.
doi:10.1177/2053951716669530 doi:10.5465/annals.2017.0099
FrontiersinSociology|www.frontiersin.org 14 May2022|Volume7|Article886498

EggerandYu ATopicModelingComparison
Hendry, D., Darari, F., Nurfadillah, R., Khanna, G., Sun, M., Condylis, P. comments regarding the cancellation of the 2015 African Cup of Nations
C., et al. (2021). “Topic modeling for customer service chats,” in 2021 in Morocco. Int. Rev. Sociol. Sport 56, 252–275. doi: 10.1177/10126902198
International Conference on Advanced Computer Science and Information 99610
Systems (Piscataway, NJ: IEEE), 1–6. doi: 10.1109/ICACSIS53237.2021.96 Müller,O.,Junglas,I.,vomBrocke,J.,andDebortoli,S.(2016).Utilizingbigdata
31322 analyticsforinformationsystemsresearch:challenges,promisesandguidelines.
Hong, L., and Davison, B. D. (2010). Empirical study of topic modeling Eur.J.Inform.Syst.25,289–302.doi:10.1057/ejis.2016.2
in Twitter. Proc. First Workshop Soc. Media Analyt. 2010, 80–88. Murthy, D. (2012). Towards a sociological understanding of social media:
doi:10.1145/1964858.1964870 theorizingtwitter.Sociology46,1059–1073doi:10.1177/0038038511422553
Hu,W.(2012).Real-timetwittersentimenttowardmidtermexams.Sociol.Mind Nagisetty,V.(2021).DomainKnowledgeGuidedTestingandTrainingofNeural
2,177–184.doi:10.4236/sm.2012.22023 Networks.(Master’sthesis),UniversityofWaterloo,Waterloo,ON,Canada.
Islam, T. (2019). Yoga-Veganism: Correlation Mining of Twitter Health Data. Obadimu, A., Mead, E., and Agarwal, N. (2019). “Identifying latent toxic
Anchorage,AK:AssociationforComputingMachinery. featuresonYouTubeusingnon-negativematrixfactorization,”inTheNinth
Jaradat, S., and Matskin, M. (2019). “On dynamic topic models for InternationalConferenceonSocialMediaTechnologies,Communication,and
mining social media,” in Lecture Notes in Social Networks. Emerging Informatics(Valencia),1–6.
Research Challenges and Opportunities in Computational Social Park, S., Ok, C., and Chae, B. (2016). Using twitter data for cruise
Network Analysis and Mining, eds N. Agarwal, N. Dokoohaki, and tourism marketing and research. J. Travel Tour. Market. 33, 885–898.
S. Tokdemir (Berlin: Springer), 209–230. doi: 10.1007/978-3-319-941 doi:10.1080/10548408.2015.1071688
05-9_8 Passos, A., Wallach, H. M., and McCallum, A. (2011). “Correlations and
Joubert,M.,andCostas,R.(2019).Gettingtoknowsciencetweeters:apilotanalysis anti correlations in LDA inference,” in Proceedings of the 2011 Workshop
ofSouthAfricantwitteruserstweetingaboutresearcharticles.J.Altmetr.2:2. on Challenges in Learning Hierarchical Models: Transfer Learning and
doi:10.29024/joa.8 Optimization(Granada),1–5.
Kasperiuniene, J., Briediene, M., and Zydziunaite, V. (2020). “Automatic Qiang,J.,Qian,Z.,Li,Y.,Yuan,Y.,andWu,X.(2020).Shorttexttopicmodeling
content analysis of social media short texts: scoping review of methods techniques,applications,andperformance:asurvey.IEEETrans.Know.Data
and tools,” in Advances in Intelligent Systems and Computing. Computer Eng.34,1427–1445.doi:10.1109/TKDE.2020.2992485
Supported Qualitative Research, eds A. P. Costa, L. P. Reis, and Queiroz, M. M. (2018). A framework based on Twitter and big data analytics
A. Moreira (Berlin: Springer), 89–101. doi: 10.1007/978-3-030-317 to enhance sustainability performance. Environ. Qual. Manag. 28, 95–100.
87-4_7 doi:10.1002/tqem.21576
Kitchin, R. (2014). Big Data, new epistemologies and paradigm Reisenbichler, M., and Reutterer, T. (2019). Topic modeling in marketing:
shifts. Big Data Soc. 1:205395171452848. doi: 10.1177/20539517145 recent advances and research opportunities. J. Bus. Econ. 89, 327–356.
28481 doi:10.1007/s11573-018-0915-7
Kraska,T.,Talwalkar,A.,Duchi,J.C.,Griffith,R.,Franklin,M.J.,andJordan,M.I. Rizvi,R.F.,Wang,Y.,Nguyen,T.,Vasilakes,J.,Bian,J.,He,Z.,andZhang,R.
(2013).MLbase:adistributedmachine-learningsystem.CIDR1,1–7.Available (2019). Analyzing social media data to understand consumers’ information
onlineat:http://www.cidrdb.org/cidr2013/Papers/CIDR13_Paper118.pdf needs on dietary supplements. Stud. Health Technol. Inform. 264, 323–327.
Krishna,A.,Satuluri,P.,Sharma,S.,Kumar,A.,andGoyal,P.(2016).“Compound doi:10.3233/SHTI190236
typeidentificationinsanskrit:whatrolesdothecorpusandgrammarplay?,” Sabate,F.,Berbegal-Mirabent,J.,Cañabate,A.,andLebherz,P.R.(2014).Factors
in Proceedings of the 6th Workshop on South and Southeast Asian Natural influencingpopularityofbrandedcontentinFacebookfanpages.Eur.Manag.
LanguageProcessing(Osaka),1–10. J.32,1001–1011.doi:10.1016/j.emj.2014.05.001
Lazer, D., and Radford, J. (2017). Data ex machina: introduction to big Sánchez-Franco,M.J.,andRey-Moreno,M.(2022).Dotravelers’reviewsdepend
data. Ann. Rev. Sociol. 43, 19–39. doi: 10.1146/annurev-soc-060116-0 onthedestination?Ananalysisincoastalandurbanpeer-to-peerlodgings.
53457 Psychol.Market.39,441–459.doi:10.1002/mar.21608
Lee, D. D., and Seung, H. S. (1999). Learning the parts of objects by Shafqat,W.,andByun,Y.-C.(2020).Arecommendationmechanismforunder-
non-negative matrix factorization. Nature 401, 788–791. doi: 10.1038/ emphasized tourist spots using topic modeling and sentiment analysis.
44565 Sustainability12:320.doi:10.3390/su12010320
Li, Q., Li, S., Zhang, S., Hu, J., and Hu, J. (2019). A review of text corpus- She,J.,Zhang,T.,Chen,Q.,Zhang,J.,Fan,W.,Wang,H.,etal.(2022).Which
based tourism big data mining. Appl. Sci. 9:3300. doi: 10.3390/app91 socialmediapostsgeneratethemostbuzz?EvidencefromWeChat.Internet
63300 Res.32,273–291.doi:10.1108/INTR-12-2019-0534
Lu, Y., and Zheng, Q. (2021). Twitter public sentiment dynamics on cruise Simsek,Z.,Vaara,E.,Paruchuri,S.,Nadkarni,S.,andShaw,J.D.(2019).Newways
tourism during the COVID-19 pandemic. Curr. Iss. Tour. 24, 892–898. ofseeingbigdata.Acad.Manag.J.62,971–978.doi:10.5465/amj.2019.4004
doi:10.1080/13683500.2020.1843607 Thielmann, A. F., Weisser, C., Kneib, T., and Saefken, B. (2021). “Coherence
Lupton,D.(2015).TheThirteenPsofBigData.ThisSociologicalLife.Available based document clustering,” in The International Conference on Learning
onlineat:https://simplysociology.wordpress.com/2015/05/11/the-thirteen-ps- Representations(Online),1–14.
of-big-data/(accessedFebruary14,2022). Vu, H. Q., Li, G., and Law, R. (2019). Discovering implicit activity
Ma,P.,Zeng-Treitler,Q.,andNelson,S.J.(2021).Useoftwotopicmodeling preferencesintravelitinerariesbytopicmodeling.Tour.Manag.75,435–446.
methodstoinvestigatecovidvaccinehesitancy.Int.Conf.ICTSoc.Hum.Beings doi:10.1016/j.tourman.2019.06.011
2021384,221–226.Availableonlineat:https://www.ict-conf.org/wp-content/ Wang,J.,andZhang,X.-L.(2021).DeepNMFTopicModeling.Availableonline
uploads/2021/07/04_202106C030_Ma.pdf at:http://arxiv.org/pdf/2102.12998v1(accessedJanuary18,2022).
Maier, D., Waldherr, A., Miltner, P., Wiedemann, G., Niekler, A., Keinert, A., Witkemper,C.,Lim,C.H.,andWaldburger,A.(2012).Socialmediaandsports
etal.(2018).ApplyingLDAtopicmodelingincommunicationresearch:toward marketing:examiningthemotivationsandconstraintsofTwitterusers.Sport
a valid and reliable methodology. Commun. Methods Measur. 12, 93–118. Market. Quart. 21, 170–183. Available online at: https://is.muni.cz/el/1423/
doi:10.1080/19312458.2018.1430754 podzim2013/ZUR589b/um/SM_W8_Twitter_Sports_Marketing.pdf
Mazanec, J. A. (2020). Hidden theorizing in big data analytics: with Xue, J., Chen, J., Hu, R., Chen, C., Zheng, C., Su, Y., et al. (2020). Twitter
a reference to tourism design research. Ann. Tour. Res. 83:102931. discussions and emotions about the COVID-19 pandemic: machine
doi:10.1016/j.annals.2020.102931 learning approach. J. Med. Internet Res. 22:e20550. doi: 10.2196/
McFarland, D. A., Lewis, K., and Goldberg, A. (2016). Sociology in the era 20550
of big data: the ascent of forensic social science. Am. Sociol. 47, 12–35. Yang, M., Nazir, S., Xu, Q., and Ali, S. (2020). Deep learning algorithms
doi:10.1007/s12108-015-9291-8 and multicriteria decision-making used in big data: a systematic
Moreau, N., Roy, M., Wilson, A., and Atlani Duault, L. (2021). “Life is more literature review. Complexity 2020, 1–18. doi: 10.1155/2020/66
important than football”: comparative analysis of Tweets and Facebook 18245
FrontiersinSociology|www.frontiersin.org 15 May2022|Volume7|Article886498

| EggerandYu |     |     |     |     |     | ATopicModelingComparison |     |
| ---------- | --- | --- | --- | --- | --- | ------------------------ | --- |
Yu, J., and Egger, R. (2021). Color and engagement in Publisher’sNote:Allclaimsexpressedinthisarticlearesolelythoseoftheauthors
touristic Instagram pictures: a machine learning approach. anddonotnecessarilyrepresentthoseoftheiraffiliatedorganizations,orthoseof
Ann. Tour. Res. 2021:103204. doi: 10.1016/j.annals.2021. thepublisher,theeditorsandthereviewers.Anyproductthatmaybeevaluatedin
103204 thisarticle,orclaimthatmaybemadebyitsmanufacturer,isnotguaranteedor
| Zhou, L., Pan, | S., Wang, | J., and Vasilakos, | A. V. (2017). |     |     |     |     |
| -------------- | --------- | ------------------ | ------------- | --- | --- | --- | --- |
endorsedbythepublisher.
| Machine learning | on big        | data: opportunities | and challenges.        |     |     |     |     |
| ---------------- | ------------- | ------------------- | ---------------------- | --- | --- | --- | --- |
| Neurocomputing   | 237, 350–361. | doi:                | 10.1016/j.neucom.2017. |     |     |     |     |
Copyright©2022EggerandYu.Thisisanopen-accessarticledistributedunderthe
01.026
termsoftheCreativeCommonsAttributionLicense(CCBY).Theuse,distribution
orreproductioninotherforumsispermitted,providedtheoriginalauthor(s)and
ConflictofInterest:Theauthorsdeclarethattheresearchwasconductedinthe thecopyrightowner(s)arecreditedandthattheoriginalpublicationinthisjournal
absenceofanycommercialorfinancialrelationshipsthatcouldbeconstruedasa
|     |     |     |     | is cited, in accordance | with accepted academic | practice. No | use, distribution or |
| --- | --- | --- | --- | ----------------------- | ---------------------- | ------------ | -------------------- |
potentialconflictofinterest. reproductionispermittedwhichdoesnotcomplywiththeseterms.
FrontiersinSociology|www.frontiersin.org 16 May2022|Volume7|Article886498