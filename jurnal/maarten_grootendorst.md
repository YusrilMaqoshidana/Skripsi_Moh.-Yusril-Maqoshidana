BERTopic: Neural topic modeling with a class-based TF-IDF procedure
MaartenGrootendorst
maartengrootendorst@gmail.com
|     |       |        | Abstract |              |             | Thesemanticpropertiesofthesevectorrepresen- |                   |          |               |
| --- | ----- | ------ | -------- | ------------ | ----------- | ------------------------------------------- | ----------------- | -------- | ------------- |
|     |       |        |          |              |             | tations                                     | allow the meaning | of texts | to be encoded |
|     | Topic | models | can be   | useful tools | to discover |                                             |                   |          |               |
insuchawaythatsimilartextsarecloseinvector
|     | latent | topics in | collections | of documents. | Re- |     |     |     |     |
| --- | ------ | --------- | ----------- | ------------- | --- | --- | --- | --- | --- |
space.
| 2202 raM 11  ]LC.sc[  1v49750.3022:viXra | cent | studies have | shown | the feasibility | of ap- |     |     |     |     |
| ---------------------------------------- | ---- | ------------ | ----- | --------------- | ------ | --- | --- | --- | --- |
proach topic modeling as a clustering task. Althoughembeddingtechniqueshavebeenused
|     | We present | BERTopic, |     | a topic | model that ex- |     |     |     |     |
| --- | ---------- | --------- | --- | ------- | -------------- | --- | --- | --- | --- |
foravarietyoftasks,rangingfromclassificationto
tendsthisprocessbyextractingcoherenttopic
neuralsearchengines,researchershavestartedto
|     | representation |     | through | the development | of a |     |     |     |     |
| --- | -------------- | --- | ------- | --------------- | ---- | --- | --- | --- | --- |
adoptthesepowerfulcontextualrepresentationsfor
|     | class-based | variation |           | of TF-IDF. | More specif- |                |                               |     |     |
| --- | ----------- | --------- | --------- | ---------- | ------------ | -------------- | ----------------------------- | --- | --- |
|     |             |           |           |            |              | topicmodeling. | Siaetal.(2020)demonstratedthe |     |     |
|     | ically,     | BERTopic  | generates | document   | embed-       |                |                               |     |     |
ding with pre-trained transformer-based lan- viability of clustering embeddings with centroid-
basedtechniques,comparedtoconventionalmeth-
guagemodels,clusterstheseembeddings,and
finally, generates topic representations with ods such as LDA, as a way to represent topics.
theclass-basedTF-IDFprocedure. BERTopic Fromtheseclusteredembeddings,topicrepresenta-
generatescoherenttopicsandremainscompet-
tionswereextractedbyembeddingwordsandfind-
|     | itive | across a | variety | of benchmarks | involv- |     |     |     |     |
| --- | ----- | -------- | ------- | ------------- | ------- | --- | --- | --- | --- |
ingthosethatareincloseproximitytoacluster’s
ingclassicalmodelsandthosethatfollowthe
|     |     |     |     |     |     | centroid. | Similarly,Top2VecleveragesDoc2Vec’s |     |     |
| --- | --- | --- | --- | --- | --- | --------- | ----------------------------------- | --- | --- |
morerecentclusteringapproachoftopicmod-
word-anddocumentrepresentationstolearnjointly
eling.
embeddedtopic,document,andwordvectors(An-
1 Introduction
|     |     |     |     |     |     | gelov, | 2020; Le and Mikolov, |     | 2014). Compara- |
| --- | --- | --- | --- | --- | --- | ------ | --------------------- | --- | --------------- |
bletoSiaetal.(2020)’sapproach,documentsare
|     | To uncover | common | themes | and | the underlying |     |     |     |     |
| --- | ---------- | ------ | ------ | --- | -------------- | --- | --- | --- | --- |
narrativeintext,topicmodelshaveproventobea clusteredandtopicrepresentationsarecreatedby
|     |                           |                  |     |                     |             | findingwordsclosetoacluster’scentroid. |           |                 | Interest- |
| --- | ------------------------- | ---------------- | --- | ------------------- | ----------- | -------------------------------------- | --------- | --------------- | --------- |
|     | powerfulunsupervisedtool. |                  |     | Conventionalmodels, |             |                                        |           |                 |           |
|     |                           |                  |     |                     |             | ingly, although                        | the topic | representations | are gen-  |
|     | such as                   | Latent Dirichlet |     | Allocation          | (LDA) (Blei |                                        |           |                 |           |
et al., 2003) and Non-Negative Matrix Factoriza- eratedfromacentroid-basedperspective,theclus-
tersaregeneratedfromadensity-basedperspective,
|     | tion (NMF) | (Févotte | and | Idier, 2011), | describe a |        |               |         |              |
| --- | ---------- | -------- | --- | ------------- | ---------- | ------ | ------------- | ------- | ------------ |
|     |            |          |     |               |            | namely | by leveraging | HDBSCAN | (McInnes and |
documentasabag-of-wordsandmodeleachdocu-
Healy,2017).
mentasamixtureoflatenttopics.
One limitation of these models is that through Theaforementionedtopicmodelingtechniques
bag-of-words representations, they disregard se- assumethatwordsincloseproximitytoacluster’s
centroidaremostrepresentativeofthatcluster,and
|     | manticrelationshipsamongwords. |     |     |     | Astheserepre- |     |     |     |     |
| --- | ------------------------------ | --- | --- | --- | ------------- | --- | --- | --- | --- |
sentationsdonotaccountforthecontextofwords thereby a topic. In practice, however, a cluster
in a sentence, the bag-of-words input may fail to willnotalwaysliewithinaspherearoundacluster
|     |     |     |     |     |     | centroid. | Assuch,theassumptioncannotholdfor |     |     |
| --- | --- | --- | --- | --- | --- | --------- | --------------------------------- | --- | --- |
accuratelyrepresentdocuments.
everyclusterofdocuments,andtherepresentation
Asananswertothisissue,textembeddingtech-
niqueshaverapidlybecomepopularinthenatural of those clusters, and thereby the topic might be
languageprocessingfield. Morespecifically,Bidi- misleading. Although (Sia et al., 2020) attempts
toovercomethisissuebyre-rankingtopicwords
rectionalEncoderRepresentationsfromTransform-
ers(BERT)(Devlinetal.,2018)anditsvariations based on their frequency in a cluster, the initial
(e.g.,Leeetal.,2020;Liuetal.,2019;Lanetal., candidatesarestillgeneratedfromacentroid-based
perspective.
2019),haveshowngreatresultsingeneratingcon-
textualword-andsentencevectorrepresentations. In this paper, we introduce BERTopic, a topic

3 BERTopic
| model       | that leverages |     | clustering | techniques |             | and a |     |     |     |     |     |     |
| ----------- | -------------- | --- | ---------- | ---------- | ----------- | ----- | --- | --- | --- | --- | --- | --- |
| class-based | variation      |     | of TF-IDF  |            | to generate | co-   |     |     |     |     |     |     |
BERTopicgeneratestopicrepresentationsthrough
| herent | topic representations. |     |     | More | specifically, |     |              |        |      |          |     |              |
| ------ | ---------------------- | --- | --- | ---- | ------------- | --- | ------------ | ------ | ---- | -------- | --- | ------------ |
|        |                        |     |     |      |               |     | three steps. | First, | each | document | is  | converted to |
wefirstcreatedocumentembeddingsusingapre-
|     |     |     |     |     |     |     | its embedding |     | representation |     | using | a pre-trained |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | -------------- | --- | ----- | ------------- |
trainedlanguagemodeltoobtaindocument-level
|              |             |         |            |        |        |        | language    | model. | Then,          | before | clustering | these         |
| ------------ | ----------- | ------- | ---------- | ------ | ------ | ------ | ----------- | ------ | -------------- | ------ | ---------- | ------------- |
| information. |             | Second, | we first   | reduce | the    | dimen- |             |        |                |        |            |               |
|              |             |         |            |        |        |        | embeddings, | the    | dimensionality |        | of         | the resulting |
| sionality    | of document |         | embeddings |        | before | creat- |             |        |                |        |            |               |
embeddingsisreducedtooptimizetheclustering
ingsemanticallysimilarclustersofdocumentsthat
|                              |     |     |     |                  |     |     | process. | Lastly, | from | the clusters |     | of documents, |
| ---------------------------- | --- | --- | --- | ---------------- | --- | --- | -------- | ------- | ---- | ------------ | --- | ------------- |
| eachrepresentadistincttopic. |     |     |     | Third,toovercome |     |     |          |         |      |              |     |               |
topicrepresentationsareextractedusingacustom
thecentroid-basedperspective,wedevelopaclass-
class-basedvariationofTF-IDF.
basedversionofTF-IDFtoextractthetopicrepre-
| sentationfromeachtopic. |     |     | Thesethreeindependent |     |     |     |     |     |     |     |     |     |
| ----------------------- | --- | --- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
3.1 Documentembeddings
| steps allow | for | a flexible | topic | model | that | can be |     |     |     |     |     |     |
| ----------- | --- | ---------- | ----- | ----- | ---- | ------ | --- | --- | --- | --- | --- | --- |
InBERTopic,weembeddocumentstocreaterep-
| used in | a variety | of  | use-cases, | such | as  | dynamic |     |     |     |     |     |     |
| ------- | --------- | --- | ---------- | ---- | --- | ------- | --- | --- | --- | --- | --- | --- |
resentationsinvectorspacethatcanbecompared
topicmodeling.
|     |     |     |     |     |     |     | semantically. | Weassumethatdocumentscontain- |     |                  |          |             |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ----------------------------- | --- | ---------------- | -------- | ----------- |
|     |     |     |     |     |     |     | ing the       | same topic                    |     | are semantically |          | similar. To |
|     |     |     |     |     |     |     | perform       | the embedding                 |     | step,            | BERTopic | uses the    |
2 RelatedWork
Sentence-BERT(SBERT)framework(Reimersand
|     |     |     |     |     |     |     | Gurevych,2019). |     | Thisframeworkallowsusersto |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | -------------------------- | --- | --- | --- |
convertsentencesandparagraphstodensevector
Inrecentyears,neuraltopicmodelshaveincreas-
inglyshownsuccessinleveragingneuralnetworks representationsusingpre-trainedlanguagemodels.
Itachievesstate-of-the-artperformanceonvarious
| to improve | upon | existing |     | topic | modeling | tech- |     |     |     |     |     |     |
| ---------- | ---- | -------- | --- | ----- | -------- | ----- | --- | --- | --- | --- | --- | --- |
sentenceembeddingtasks(ReimersandGurevych,
niques(Terragnietal.,2021;Caoetal.,2015;Zhao
2020;Thakuretal.,2020).
| et al., 2021; | Larochelle |     | and | Lauly, | 2012). | The |     |     |     |     |     |     |
| ------------- | ---------- | --- | --- | ------ | ------ | --- | --- | --- | --- | --- | --- | --- |
incorporation of word embeddings into classical Theseembeddings,however,areprimarilyused
toclustersemanticallysimilardocumentsandnot
| models, | such | as LDA, | demonstrated |     | the | viability |          |         |            |     |         |           |
| ------- | ---- | ------- | ------------ | --- | --- | --------- | -------- | ------- | ---------- | --- | ------- | --------- |
|         |      |         |              |     |     |           | directly | used in | generating | the | topics. | Any other |
ofusingthesepowerfulrepresentations(Liuetal.,
2015;Nguyenetal.,2015;Shietal.,2017;Qiang embeddingtechniquecanbeusedforthispurpose
et al., 2017). Foregoing incorporation into LDA- ifthelanguagemodelgeneratingthedocumentem-
|     |     |     |     |     |     |     | beddingswasfine-tunedonsemanticsimilarity. |     |     |     |     | As  |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------------ | --- | --- | --- | --- | --- |
likemodels,therehasbeenarecentsurgeoftopic
aresult,thequalityofclusteringinBERTopicwill
modelingtechniquesbuiltprimarilyaroundembed-
dingmodelsillustratingthepotentialofembedding- increaseasnewandimprovedlanguagemodelsare
|             |          |     |            |     |          |         | developed. | ThisallowsBERTopictocontinuously |     |     |     |     |
| ----------- | -------- | --- | ---------- | --- | -------- | ------- | ---------- | -------------------------------- | --- | --- | --- | --- |
| based topic | modeling |     | techniques |     | (Bianchi | et al., |            |                                  |     |     |     |     |
growwiththecurrentstate-of-the-artinembedding
2020b;Diengetal.,2020;ThompsonandMimno,
| 2020). | CTM, | for example, |     | demonstrates |     | the ad- | techniques. |     |     |     |     |     |
| ------ | ---- | ------------ | --- | ------------ | --- | ------- | ----------- | --- | --- | --- | --- | --- |
vantageofrelyingonpre-trainedlanguagemodels,
3.2 Documentclustering
namelythatfutureimprovementsinlanguagemod-
|     |     |     |     |     |     |     | As data | increases | in  | dimensionality, |     | distance to |
| --- | --- | --- | --- | --- | --- | --- | ------- | --------- | --- | --------------- | --- | ----------- |
elsmaytranslateintobettertopicmodels(Bianchi
| etal.,2020a). |     |     |     |     |     |     | thenearestdatapointhasbeenshowntoapproach |     |              |      |       |           |
| ------------- | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | ------------ | ---- | ----- | --------- |
|               |     |     |     |     |     |     | the distance                              | to  | the farthest | data | point | (Aggarwal |
Severalapproacheshavestartedsimplifyingthe
|                |     |         |     |            |       |     | etal.,2001;Beyeretal.,1999). |     |     |     | Asaresult,inhigh |     |
| -------------- | --- | ------- | --- | ---------- | ----- | --- | ---------------------------- | --- | --- | --- | ---------------- | --- |
| topic building |     | process | by  | clustering | word- | and |                              |     |     |     |                  |     |
dimensionalspace,theconceptofspatiallocality
documentembeddings(Siaetal.,2020;Angelov,
|     |     |     |     |     |     |     | becomes | ill-defined |     | and distance | measures | differ |
| --- | --- | --- | --- | --- | --- | --- | ------- | ----------- | --- | ------------ | -------- | ------ |
2020). Thisclusteringapproachallowsforaflex-
little.
| ible topic | model | as the | generation |     | of the | clusters |          |            |     |            |     |                 |
| ---------- | ----- | ------ | ---------- | --- | ------ | -------- | -------- | ---------- | --- | ---------- | --- | --------------- |
|            |       |        |            |     |        |          | Although | clustering |     | approaches |     | exist for over- |
canbeseparatedfromtheprocessofgeneratingthe
comingthiscurseofdimensionality(Pandoveetal.,
topicrepresentations.
|     |     |     |     |     |     |     | 2018; Steinbach |     | et  | al., 2004), | a   | more straight- |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | --- | ----------- | --- | -------------- |
BERTopicbuildsontopoftheclusteringembed- forward approach is to reduce the dimensional-
dings approach and extends it by incorporating a ityofembeddings. AlthoughPCAandt-SNEare
class-based variant of TF-IDF for creating topic well-knownmethodsforreducingdimensionality,
| representations. |     |     |     |     |     |     | UMAPhasshowntopreserversmoreofthelocal |     |     |     |     |     |
| ---------------- | --- | --- | --- | --- | --- | --- | -------------------------------------- | --- | --- | --- | --- | --- |

| and global                                   | features | of high-dimensional  |     | data in  |     |        |         |      |     |
| -------------------------------------------- | -------- | -------------------- | --- | -------- | --- | ------ | ------- | ---- | --- |
| lowerprojecteddimensions(McInnesetal.,2018). |          |                      |     |          |     |        |         | A    |     |
|                                              |          |                      |     |          |     | W = tf | ·log(1+ | )    | (2) |
|                                              |          |                      |     |          |     | t,c    | t,c     |      |     |
| Moreover,                                    | since it | has no computational |     | restric- |     |        |         | tf t |     |
tions on embedding dimensions, UMAP can be Wherethetermfrequencymodelsthefrequency
usedacrosslanguagemodelswithdifferingdimen-
|               |       |             |     |            | of term | t in a class | c or in | this instance. | Here, |
| ------------- | ----- | ----------- | --- | ---------- | ------- | ------------ | ------- | -------------- | ----- |
| sional space. | Thus, | we use UMAP | to  | reduce the |         |              |         |                |       |
theclasscisthecollectionofdocumentsconcate-
dimensionalityofdocumentembeddingsgenerated
|     |     |     |     |     | natedintoasingledocumentforeachcluster. |     |     |     | Then, |
| --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | ----- |
in3.1(McInnesetal.,2018). theinversedocumentfrequencyisreplacedbythe
| The | reduced embeddings | are | clustering | used |     |     |     |     |     |
| --- | ------------------ | --- | ---------- | ---- | --- | --- | --- | --- | --- |
inverseclassfrequencytomeasurehowmuchinfor-
| HDBSCAN | (McInnes | et al., 2017). |     | It is an ex- |                              |     |     |                |     |
| ------- | -------- | -------------- | --- | ------------ | ---------------------------- | --- | --- | -------------- | --- |
|         |          |                |     |              | mationatermprovidestoaclass. |     |     | Itiscalculated |     |
tensionofDBSCANthatfindsclustersofvarying bytakingthelogarithmoftheaveragenumberof
densitiesbyconvertingDBSCANintoahierarchi-
wordsperclassAdividedbythefrequencyofterm
| calclusteringalgorithm. |     | HDBSCANmodelsclus- |     |     |                    |                             |     |     |     |
| ----------------------- | --- | ------------------ | --- | --- | ------------------ | --------------------------- | --- | --- | --- |
|                         |     |                    |     |     | tacrossallclasses. | Tooutputonlypositivevalues, |     |     |     |
tersusingasoft-clusteringapproachallowingnoise
weaddonetothedivisionwithinthelogarithm.
tobemodeledasoutliers. Thispreventsunrelated Thus, thisclass-basedTF-IDFproceduremod-
documentstobeassignedtoanyclusterandisex-
elstheimportanceofwordsinclustersinsteadof
pectedtoimprovetopicrepresentations.‘Moreover,
|     |     |     |     |     | individualdocuments. |     | Thisallowsustogenerate |     |     |
| --- | --- | --- | --- | --- | -------------------- | --- | ---------------------- | --- | --- |
(Allaoui et al., 2020) demonstrated that reducing topic-word distributions for each cluster of docu-
highdimensionalembeddingswithUMAPcanim-
ments.
| prove the | performance | of well-known |     | clustering |     |     |     |     |     |
| --------- | ----------- | ------------- | --- | ---------- | --- | --- | --- | --- | --- |
Finally,byiterativelymergingthec-TF-IDFrep-
algorithms,suchask-MeansandHDBSCAN,both
resentationsoftheleastcommontopicwithitsmost
intermsofclusteringaccuracyandtime. similarone,wecanreducethenumberoftopicsto
auser-specifiedvalue.
3.3 TopicRepresentation
Thetopicrepresentationsaremodeledbasedonthe
4 DynamicTopicModeling
documentsineachclusterwhereeachclusterwill
beassignedonetopic. Foreachtopic,wewantto Traditionaltopicmodelingtechniquesarestaticin
natureanddonotallowforsequentially-organized
| know what | makes | one topic, based | on  | its cluster- |     |     |     |     |     |
| --------- | ----- | ---------------- | --- | ------------ | --- | --- | --- | --- | --- |
worddistribution,differentfromanother? Forthis ofdocumentstobemodeled. Dynamictopicmod-
purpose,wecanmodifyTF-IDF,ameasureforrep- elingtechniques,firstintroducedby(BleiandLaf-
ferty,2006)asanextensionofLDA,overcomethis
resentingtheimportanceofawordtoadocument,
suchthatitallowsforarepresentationofaterm’s bymodelinghowtopicsmighthaveevolvedover
importancetoatopicinstead. timeandtheextenttowhichtopicrepresentations
| The         | classic TF-IDF  | procedure | combines | two      | reflectthat. |     |           |               |     |
| ----------- | --------------- | --------- | -------- | -------- | ------------ | --- | --------- | ------------- | --- |
|             |                 |           |          |          | In BERTopic, | we  | can model | this behavior | by  |
| statistics, | term frequency, | and       | inverse  | document |              |     |           |               |     |
frequency(Joachims,1996): leveragingthec-TF-IDFrepresentationsoftopics.
Here,weassumethatthetemporalnatureoftopics
N
W = tf ·log( ) (1) shouldnotinfluencethecreationofglobaltopics.
|     | t,d | t,d |      |     |                                              |     |     |     |     |
| --- | --- | --- | ---- | --- | -------------------------------------------- | --- | --- | --- | --- |
|     |     |     | df t |     | Thesametopicmightappearacrossdifferenttimes, |     |     |     |     |
Wherethetermfrequencymodelsthefrequency albeitpossiblyrepresenteddifferently. Asanexam-
of term t in document d. The inverse document ple,aglobaltopicaboutcarsmightcontainwords
frequencymeasureshowmuchinformationaterm suchas"car"and"vehicle"regardlessofthetem-
providestoadocumentandiscalculatedbytaking poral nature of specific documents. Car-related
the logarithm of the number of documents in a documentscreatedin2020,however,mightbebet-
corpusN
dividedbythetotalnumberofdocuments ter represented with words such as "Tesla" and
thatcontaint. "self-driving" whereas these words would likely
Wegeneralizethisproceduretoclustersofdoc- notappearincar-relateddocumentscreatedin1990.
uments. First, wetreatalldocumentsinacluster Althoughthesametopicisassignedtocar-related
asasingledocumentbysimplyconcatenatingthe documents in 1990 and 2020, its representation
documents. Then, TF-IDFisadjustedto account mightdiffer. Thus,wefirstgenerateaglobalrep-
forthisrepresentationbytranslatingdocumentsto resentationoftopics,regardlessoftheirtemporal
| clusters: |     |     |     |     | nature,beforedevelopingalocalrepresentation. |     |     |     |     |
| --------- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- |

Todothis,BERTopicisfirstfittedontheentire usedtoruntheexperiments, validateresults, and
corpusasiftherewerenotemporalaspectstothe preprocessthedata(Terragnietal.,2021).
datainordertocreateaglobalviewoftopics. Then, BoththeimplementationofBERTopicaswellas
wecancreatealocalrepresentationofeachtopic theexperimentalsetuparefreelyavailableonline.
| bysimplymultiplyingthetermfrequencyofdocu- |     |     |     |     |     |     | 12  |     |     |     |     |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
mentsattimestepiwiththepre-calculatedglobal
|     |     |     |     |     |     |     | 5.1 Datasets |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | --- | --- | --- |
IDFvalues:
|     |     |     |     |     |     |     | Three datasets | were used | to validate | BERTopic, |     |
| --- | --- | --- | --- | --- | --- | --- | -------------- | --------- | ----------- | --------- | --- |
A
|     | W     | = tf | ·log(1+ |     | )   | (3) | namely20NewsGroups,BBCNews,andTrump’s       |     |     |     |     |
| --- | ----- | ---- | ------- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- |
|     | t,c,i |      | t,c,i   |     |     |     |                                             |     |     |     |     |
|     |       |      |         | tf  | t   |     | tweets. Wechoosetothoroughlypreprocessthe20 |     |     |     |     |
Amajoradvantageofusingthistechniqueisthat NewsGroups and BBC News datasets, and only
theselocalrepresentationscanbecreatedwithout slightly preprocess Trump’s tweets to generate
morediversitybetweendatasets.
| the need | to embed | and | cluster | documents |     | which |     |     |     |     |     |
| -------- | -------- | --- | ------- | --------- | --- | ----- | --- | --- | --- | --- | --- |
allowforfastcomputation. Moreover,thismethod The 20 NewsGroups dataset3 contains 16309
canalsobeusedtomodeltopicrepresentationsby news articles across 20 categories (Lang, 1995).
TheBBCNewsdataset4
| othermeta-data,suchasauthororjournal. |     |     |     |     |     |     |              |                  | contains2225documents |        |      |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | ------------ | ---------------- | --------------------- | ------ | ---- |
|                                       |     |     |     |     |     |     | from the     | BBC News website | between               | 2004   | and  |
| 4.1 Smoothing                         |     |     |     |     |     |     | 2005 (Greene | and Cunningham,  |                       | 2006). | Both |
Although we can observe how topic representa- datasetswereretrievedusingOCTIS,andprepro-
cessedbyremovingpunctuation,lemmatization,re-
| tions | are different | from | one | time to | another, | the |     |     |     |     |     |
| ----- | ------------- | ---- | --- | ------- | -------- | --- | --- | --- | --- | --- | --- |
movingstopwords,andremovingdocumentswith
topicrepresentationattimesteptisindependentof
| timestept-1. | Asaresult,thisdynamicrepresenta- |     |     |     |     |     | lessthan5words. |     |     |     |     |
| ------------ | -------------------------------- | --- | --- | --- | --- | --- | --------------- | --- | --- | --- | --- |
tionoftopicsmightnotresultinlinearlyevolving To represent more recent data in a short-text
|         |         |        |          |          |     |         | form,wecollectedalltweetsofTrump5 |     |     | beforeand |     |
| ------- | ------- | ------ | -------- | -------- | --- | ------- | --------------------------------- | --- | --- | --------- | --- |
| topics. | When we | expect | linearly | evolving |     | topics, |                                   |     |     |           |     |
weassumethatatopicrepresentationattimestept during his presidency. The data contains 44253
dependsonthetopicrepresentationattimestept-1. tweets, excluding re-tweets, between 2009 and
|     |     |     |     |     |     |     | 2021. Inbothdatasets,welowercasedalltokens. |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- |
Toovercomethis,wecanleveragethec-TF-IDF
ToevaluateBERTopicinadynamictopicmod-
matricesthatwerecreatedateachtimesteptoincor-
poratethislinearassumption. Foreachtopicand elingsetting,Trump’stweetswereselectedasthey
timestep,thec-TF-IDFvectorisnormalizedbydi- inherentlyhadatemporalnaturetothem. Addition-
ally,thetranscriptionsoftheUnitedNations(UN)
| vidingthevectorwiththeL1-norm. |     |     |     |     | Whencompar- |     |                                   |     |     |          |     |
| ------------------------------ | --- | --- | --- | --- | ----------- | --- | --------------------------------- | --- | --- | -------- | --- |
|                                |     |     |     |     |             |     | generaldebatesbetween2006and20156 |     |     | wereana- |     |
ingvectors,thisnormalizationprocedureprevents
topicrepresentationsfromhavingdisproportionate lyzed(Baturoetal.,2017). TheTrumpdatasetwas
|     |     |     |     |     |     |     | binned to | 10 timesteps | and the | UN datasets | to 9 |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------------ | ------- | ----------- | ---- |
effectsasaresultofthesizeofthedocumentsthat
timesteps.
makeupthetopic.
| Then, | for each | topic | and | representation |     | at  |            |     |     |     |     |
| ----- | -------- | ----- | --- | -------------- | --- | --- | ---------- | --- | --- | --- | --- |
|       |          |       |     |                |     |     | 5.2 Models |     |     |     |     |
timestept,wesimplytaketheaverageofthenor-
BERTopicwillbecomparedtoLDA,NMF,CTM,
| malizedc-TF-IDFvectorsattandt-1. |     |           |                |     | Thisallows |          |              |         |     |          |         |
| -------------------------------- | --- | --------- | -------------- | --- | ---------- | -------- | ------------ | ------- | --- | -------- | ------- |
|                                  |     |           |                |     |            |          | and Top2Vec. | LDA and | NMF | were run | through |
| us to influence                  |     | the topic | representation |     | at         | t by in- |              |         |     |          |         |
corporating the representation at t-1. Thus, the OCTIS with default parameters. The "all-mpnet-
resultingtopicrepresentationsaresmoothedbased base-v2"SBERTmodelwasusedastheembedding
ontheirtemporalposition.
1https://github.com/MaartenGr/BERTopic
It should be noted that although we might ex- 2https://github.com/MaartenGr/
pectlinearlyevolvingtopics,thisisnotalwaysthe BERTopic_evaluation
3https://github.com/MIND-Lab/OCTIS/
case. Hence,thissmoothingtechniqueisoptional
tree/master/preprocessed_datasets/
| whenusingBERTopicandwillbereflectedinthe |     |     |     |     |     |     | 20NewsGroup                         |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- |
| experimentalsetup.                       |     |     |     |     |     |     | 4https://github.com/MIND-Lab/OCTIS/ |     |     |     |     |
tree/master/preprocessed_datasets/BBC_
news
5 ExperimentalSetup
5https://www.thetrumparchive.com/faq
6https://runestone.academy/runestone/
OCTIS(OptimizingandComparingTopicmodels
books/published/httlads/_static/
| is Simple), | an  | open-source | python |     | package, | was |     |     |     |     |     |
| ----------- | --- | ----------- | ------ | --- | -------- | --- | --- | --- | --- | --- | --- |
un-general-debates.csv

|     |     |                |     | 20NewsGroups |      | BBCNews |      | Trump |      |     |     |
| --- | --- | -------------- | --- | ------------ | ---- | ------- | ---- | ----- | ---- | --- | --- |
|     |     |                |     | TC           | TD   | TC      | TD   | TC    | TD   |     |     |
|     |     | LDA            |     | .058         | .749 | .014    | .577 | -.011 | .502 |     |     |
|     |     | NMF            |     | .089         | .663 | .012    | .549 | .009  | .379 |     |     |
|     |     | T2V-MPNET      |     | .068         | .718 | -.027   | .540 | -.213 | .698 |     |     |
|     |     | T2V-Doc2Vec    |     | .192         | .823 | .171    | .792 | -.169 | .658 |     |     |
|     |     | CTM            |     | .096         | .886 | .094    | .819 | .009  | .855 |     |     |
|     |     | BERTopic-MPNET |     | .166         | .851 | .167    | .794 | .066  | .663 |     |     |
Table 1: Ranging from 10 to 50 topics with steps of 10, topic coherence (TC) and topic diversity (TD) were
calculated at each step for each topic model. All results were averaged across 3 runs for each step. Thus, each
scoreistheaverageof15separateruns.
modelforBERTopicandCTM(Songetal.,2020). Rangingfrom10to50topicswithstepsof10,
TwovariationsofTop2Vecweremodeled,onewith the NPMI score was calculated at each step for
Doc2Vec and one with the "all-mpnet-base-v2" eachtopicmodel. Allresultswereaveragedacross
| SBERTmodel7. |     |     |     |     |     | 3runsforeachstep. |     | Toevaluatethedynamictopic |     |     |     |
| ------------ | --- | --- | --- | --- | --- | ----------------- | --- | ------------------------- | --- | --- | --- |
For fair comparisons between BERTopic and models,theNPMIscorewascalculatedat50topics
Top2Vec, the parameters of HDBSCAN and for each timestep and then averaged. All results
| UMAPwerefixedbetweentopicmodels. |     |     |     |     |     | wereaveragedacross3runs. |     |     |     |     |     |
| -------------------------------- | --- | --- | --- | --- | --- | ------------------------ | --- | --- | --- | --- | --- |
To measure the generalizability of BERTopic Validation measures such are topic coherence
across language models, four different language and topic diversity are proxies of what is essen-
|        |      |         |                 |     |      | tiallyasubjectiveevaluation. |     |     | Oneusermightjudge |     |     |
| ------ | ---- | ------- | --------------- | --- | ---- | ---------------------------- | --- | --- | ----------------- | --- | --- |
| models | were | used in | the experiments |     | with |                              |     |     |                   |     |     |
BERTopic,namelytheUniversalSentenceEncoder the coherence and diversity of a topic differently
(Ceretal.,2018),Doc2Vec,andthe"all-MiniLM- fromanotheruser. Asaresult,althoughthesemea-
L6-v2" (MiniLM) and "all-mpnet-base-v2" (MP- surescanbeusedtogetanindicationofamodel’s
performance,theyarejustthat,anindication.
NET)SBERTmodels.
Finally,BERTopic,withandwithouttheassump- ItshouldbenotedthatalthoughNPMIhasbeen
tionoflinearly-evolvingtopics,wascomparedwith shown to correlate with human judgment, recent
theoriginaldynamictopicmodel,referredhereto research states that this may only be the case for
|     |     |     |     |     |     | classical models |     | and that | this relationship |     | might |
| --- | --- | --- | --- | --- | --- | ---------------- | --- | -------- | ----------------- | --- | ----- |
asLDASequence.
|                |     |     |     |     |     | not exist with                               | neural | topic | models | (Hoyle | et al., |
| -------------- | --- | --- | --- | --- | --- | -------------------------------------------- | ------ | ----- | ------ | ------ | ------- |
| 5.3 Evaluation |     |     |     |     |     | 2021). Inpart,theauthorssuggestaneeds-driven |        |       |        |        |         |
approachtoevaluationastopicmodeling’sprimary
Theperformanceofthetopicmodelsinthispaper
useisincomputer-assistedcontentanalysis.
| is reflected | by  | two widely-used |     | metrics, | namely |     |     |     |     |     |     |
| ------------ | --- | --------------- | --- | -------- | ------ | --- | --- | --- | --- | --- | --- |
Tothispurpose,thedifferencesinrunningtimes
| topiccoherenceandtopicdiversity. |           |           |     | Foreachtopic |       |                       |      |                        |     |          |         |
| -------------------------------- | --------- | --------- | --- | ------------ | ----- | --------------------- | ---- | ---------------------- | --- | -------- | ------- |
|                                  |           |           |     |              |       | of each model         | were | explored               | as  | they can | greatly |
| model,                           | its topic | coherence | was | evaluated    | using |                       |      |                        |     |          |         |
|                                  |           |           |     |              |       | impacttheirusability. |      | Here,wechoosetofocuson |     |          |         |
normalizedpointwisemutualinformation(NPMI,
|                                 |            |                             |          |            |         | the wall times                             | as  | it more    | accurately | reflects | how     |
| ------------------------------- | ---------- | --------------------------- | -------- | ---------- | ------- | ------------------------------------------ | --- | ---------- | ---------- | -------- | ------- |
| (Bouma,2009)).                  |            | Thiscoherencemeasurehasbeen |          |            |         |                                            |     |            |            |          |         |
|                                 |            |                             |          |            |         | the topic modeling                         |     | techniques | would      | be       | used in |
| shown                           | to emulate | human                       | judgment | with       | reason- |                                            |     |            |            |          |         |
|                                 |            |                             |          |            |         | practice. Allthemodelsarerunonamachinewith |     |            |            |          |         |
| ableperformance(Lauetal.,2014). |            |                             |          | Themeasure |         |                                            |     |            |            |          |         |
2coresofIntel(R)Xeon(R)CPU@2.00GHzand
rangesfrom[-1,1]where1indicatesaperfectas-
aTeslaP100-PCIE-16GBGPU.
| sociation. | Topic | diversity, | as defined | by  | (Dieng |     |     |     |     |     |     |
| ---------- | ----- | ---------- | ---------- | --- | ------ | --- | --- | --- | --- | --- | --- |
Moreover,inSection7,thestrengthsandweak-
etal.,2020),isthepercentageofuniquewordsfor
nessesoftheproposedmodelacrossusecaseswill
| alltopics. | Themeasurerangesfrom[0,1]where |     |     |     |     |     |     |     |     |     |     |
| ---------- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
bediscussedextensivelytofurthershedalighton
0indicatesredundanttopicsand1indicatesmore
whatthemodelcanandcannotdo.
variedtopics.
6 Results
7ForanoverviewofSBERTmodelsandtheirperformance,
seehttps://www.sbert.net/docs/pretrained_
OurmainresultscanbefoundinTable1.
models.html

|     |     |                  |     |     |     | 20NewsGroups | BBCNews |      |       | Trump |     |     |
| --- | --- | ---------------- | --- | --- | --- | ------------ | ------- | ---- | ----- | ----- | --- | --- |
|     |     |                  |     |     |     | TC TD        | TC      | TD   | TC    | TD    |     |     |
|     |     | BERTopic-USE     |     |     |     | .149 .858    | .158    | .764 | .051  | .684  |     |     |
|     |     | BERTopic-Doc2Vec |     |     |     | .173 .871    | .168    | .819 | -.088 | .536  |     |     |
|     |     | BERTopic-MiniLM  |     |     |     | .159 .833    | .170    | .802 | .060  | .660  |     |     |
|     |     | BERTopic-MPNET   |     |     |     | .166 .851    | .167    | .792 | .066  | .663  |     |     |
Table2: UsingfourdifferentlanguagemodelsinBERTopic,coherencescore(TC)andtopicdiversity(TD)were
calculated ranging from 10 to 50 topics with steps of 10. All results were averaged across 3 runs for each step.
Thus,eachscoreistheaverageof15separateruns.
6.1 Performance mains competitive regardless of the embedding
|               |     |        |       |           |        |          | model.     | By separating |              | the process | of embedding     |      |
| ------------- | --- | ------ | ----- | --------- | ------ | -------- | ---------- | ------------- | ------------ | ----------- | ---------------- | ---- |
| From Table    | 1,  | we     | can   | observe   | that   | BERTopic |            |               |              |             |                  |      |
|               |     |        |       |           |        |          | documents  | and           | constructing |             | the word-topic   | dis- |
| generally     | has | high   | topic | coherence | scores | across   |            |               |              |             |                  |      |
|               |     |        |       |           |        |          | tribution, | BERTopic      |              | is flexible | in its embedding |      |
| all datasets. |     | It has | the   | highest   | scores | on the   |            |               |              |             |                  |      |
procedure.
| slightly         | preprocessed |             | dataset, |     | Trump’s | tweets,    |     |     |     |     |     |     |
| ---------------- | ------------ | ----------- | -------- | --- | ------- | ---------- | --- | --- | --- | --- | --- | --- |
| whilst remaining |              | competitive |          |     | on the  | thoroughly |     |     |     |     |     |     |
6.3 DynamicTopicModeling
preprocesseddatassets,20NewsGroupsandBBC
|     |     |     |     |     |     |     | From Table | 3,  | we can | observe | that BERTopic |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------ | ------- | ------------- | --- |
News. AlthoughBERTopicdemonstratescompet-
withandwithouttheassumptionoflinearlyevolv-
| itive topic | diversity |     | scores, | it is | consistently | out- |     |     |     |     |     |     |
| ----------- | --------- | --- | ------- | ----- | ------------ | ---- | --- | --- | --- | --- | --- | --- |
ingtopicsperformsconsistentlywellacrossboth
| performed | by  | CTM. | This | is consistent |     | with their |           |     |        |                |     |        |
| --------- | --- | ---- | ---- | ------------- | --- | ---------- | --------- | --- | ------ | -------------- | --- | ------ |
|           |     |      |      |               |     |            | datasets. | For | Trump, | it outperforms | LDA | on all |
resultsindicatinghightopicdiversity,albeitusing
measureswhereasitonlyachievesthetopscoreon
adifferenttopicdiversitymeasure(Bianchietal.,
topiccoherencefortheUNdataset.
2020a).
|     |     |     |     |     |     |     | On both           | datasets, |     | there seems | to be no        | effect |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --------- | --- | ----------- | --------------- | ------ |
|     |     |     |     |     |     |     | of the assumption |           | of  | linearly    | evolving topics | on     |
6.2 LanguageModels
bothtopiccoherenceandtopicdiversityindicating
TheresultsinTable2demonstratethestabilityof
thatfromanevaluationperspective,theproposed
| BERTopic, | in  | terms | of both | topic | coherence | and |     |     |     |     |     |     |
| --------- | --- | ----- | ------- | ----- | --------- | --- | --- | --- | --- | --- | --- | --- |
assumptiondoesnotimpactperformance.
| topicdiversity,acrossSBERTlanguagemodels. |     |     |     |     |     | As  |     |     |     |     |     |     |
| ----------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
aresult,thesmallerandfastermodel,"all-MiniLM-
|         |       |               |     |      |         |     |     |     |     | Trump | UN  |     |
| ------- | ----- | ------------- | --- | ---- | ------- | --- | --- | --- | --- | ----- | --- | --- |
| L6-v2", | might | be preferable |     | when | limited | GPU |     |     |     |       |     |     |
|         |       |               |     |      |         |     |     |     |     | TC TD | TC  | TD  |
capacityisavailable.
Although the USE and Doc2Vec language in LDASequence .009 .715 .173 .820
BERTopic generally have similar performance, BERTopic .079 .862 .231 .779
Doc2VecscoreslowontheTrumpdataset. Thisis BERTopic-Evolve .079 .863 .226 .769
reflectedintheresultswefindin1whereTop2Vec
with Doc2Vec has poor performance. These re- Table 3: The topic coherence (TC) and topic diversity
|     |     |     |     |     |     |     | (TD) scores | were | calculated | on dynamic | topic | model- |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ---- | ---------- | ---------- | ----- | ------ |
sultssuggestthatDoc2Vecstruggleswithcreating
accuraterepresentationsoftheTrumpdataset. ing tasks. The TC and TD scores were calculated for
eachofthe9timestepsineachdataset.Then,allresults
Ontopiccoherence,Top2VecwithDoc2Vecem-
|          |       |             |     |              |     |      | wereaveragedacross3runsforeachstep. |     |     |     | Thus,each |     |
| -------- | ----- | ----------- | --- | ------------ | --- | ---- | ----------------------------------- | --- | --- | --- | --------- | --- |
| beddings | shows | competitive |     | performance. |     | How- |                                     |     |     |     |           |     |
scorerepresentstheaverageof27values.
| ever, when | MPNET     |     | embeddings    |     | are  | used both  |     |     |     |     |     |     |
| ---------- | --------- | --- | ------------- | --- | ---- | ---------- | --- | --- | --- | --- | --- | --- |
| its topic  | coherence |     | and diversity |     | drop | across all |     |     |     |     |     |     |
6.4 Walltime
datasetssuggestingthatTop2Vecmightnotbebest
suitedwithembeddingsoutsideofthosegenerated FromtheleftgraphinFigure1,CTMusingaMP-
throughDoc2Vec. Thisisnotunexpectedasboth NETSBERTmodel,isquiteslowcomparedtoall
wordanddocumentsvectorsinDoc2Vecarejointly othermodels. Ifweremovethatmodelfromthere-
embeddedinthesamespace,whichdoesnothold sults,wecanmoreeasilycomparethewalltimeof
foralllanguagemodels. thetopicmodelsthataremorecloseinspeed. Then,
In turn, this also suggests why BERTopic re- We can observe that the classical models, NMF

Figure1: Computationtime(walltime)insecondsofeachtopicmodelontheTrumpdataset. Increasingsizesof
vocabularieswereregulatedthroughselectionofdocumentsrangingfrom1000documentsuntil43000documents
withstepsof2000.Left:computationalresultswithCTM.Right:computationalresultswithoutCTMasitinflates
they-axismakingdifferentiationbetweenothertopicmodelsdifficulttovisualize.
| andLDA,arefasterthantheneuralnetwork-based |     |                   |     | 7.1 Strengths |         |         |     |           |             |
| ------------------------------------------ | --- | ----------------- | --- | ------------- | ------- | ------- | --- | --------- | ----------- |
| topicmodelingtechniques.                   |     | Moreover,BERTopic |     |               |         |         |     |           |             |
|                                            |     |                   |     | There are     | several | notable |     | strengths | of BERTopic |
andTop2Vecarequitesimilarinwalltimesifthey
comparedtothetopicmodelsusedinthisstudy.
| areusingthesamelanguagemodels. |     |     | Interestingly, |     |     |     |     |     |     |
| ------------------------------ | --- | --- | -------------- | --- | --- | --- | --- | --- | --- |
theMiniLMSBERTmodelseemstobesimilarin First, the experiments demonstrate that
speed compared with Doc2Vec indicating that in BERTopic remains competitive regardless of the
languagemodelusedtoembedthedocumentsand
| BERTopic, | MiniLM | is a good trade-off | between |                  |     |     |          |      |            |
| --------- | ------ | ------------------- | ------- | ---------------- | --- | --- | -------- | ---- | ---------- |
|           |        |                     |         | that performance |     | may | increase | when | leveraging |
speedandperformance.
|     |     |     |     | state-of-the-art |     | language | models. | This | indicates |
| --- | --- | --- | --- | ---------------- | --- | -------- | ------- | ---- | --------- |
However,itshouldbenotedthatintheenviron-
ment used in this experiment a GPU was avail- its ability to scale performance with new devel-
|                               |     |               |     | opments         | in the | field       | of language | models       | whilst   |
| ----------------------------- | --- | ------------- | --- | --------------- | ------ | ----------- | ----------- | ------------ | -------- |
| ableforcreatingtheembeddings. |     | Asaresult,the |     |                 |        |             |             |              |          |
|                               |     |               |     | still remaining |        | competitive |             | if classical | language |
walltimeisexpectedtoincreasesignificantlywhen
|     |     |     |     | models | are used. | Moreover, |     | its stability | across |
| --- | --- | --- | --- | ------ | --------- | --------- | --- | ------------- | ------ |
embeddingdocumentswithoutaGPU.Although
|     |     |     |     | language | models | allows | it  | to be used | in a wide |
| --- | --- | --- | --- | -------- | ------ | ------ | --- | ---------- | --------- |
Doc2Veccanbeusedasalanguagemodelinstead,
|     |     |     |     | rangeofsituations. |     | Forexample,whenauserdoes |     |     |     |
| --- | --- | --- | --- | ------------------ | --- | ------------------------ | --- | --- | --- |
previousexperimentsinthisstudyhaveputitssta-
nothaveaccesstoaGPU,Doc2Veccanbeusedto
| bility with            | respect | to topic coherence | and topic |                             |            |     |     |            |           |
| ---------------------- | ------- | ------------------ | --------- | --------------------------- | ---------- | --- | --- | ---------- | --------- |
| diversityintoquestion. |         |                    |           | generatecompetitiveresults. |            |     |     |            |           |
|                        |         |                    |           | Second,                     | separating |     | the | process of | embedding |
documentsfromrepresentingtopicsallowsforsig-
7 Discussion
nificantflexibilityintheusageandfine-tuningof
Although we attempted to validate BERTopic BERTopic. Differentpreprocessingprocedurescan
across several experiments, topic modeling tech- beusedwhenembeddingthedocumentsandwhen
|     |     |     |     | generatingthetopicrepresentations. |     |     |     |     | Forexample, |
| --- | --- | --- | --- | ---------------------------------- | --- | --- | --- | --- | ----------- |
niquescanbevalidatedthroughmanyotherevalua-
onemightwanttoremovestopwordsinthetopic
tionmetrics,suchasmetricsforunsupervisedand
supervisedmodelingperformance. Moreover,topic representationsbutnotbeforecreatingdocument
|     |     |     |     | embeddings. |     | Similarly,oncethedocumentshave |     |     |     |
| --- | --- | --- | --- | ----------- | --- | ------------------------------ | --- | --- | --- |
modelingtechniquescanbeusedacrossavariety
beenclustered,thetopicgenerationprocesscanbe
ofusecases,manyofwhicharenotcoveredinthis
study. Forthosereasons, weadditionallydiscuss fine-tuned,by,forexample,increasingthen-gram
thestrengthsandweaknessesofBERTopictofur- of words in the topic representation, without the
needtore-clusterthedata.
therdescribewhen,andperhapsmostimportantly,
whennottouseBERTopic. Third,byleveragingaclass-basedversionofTF-

IDF, we can represent topics as a distribution of thatBERTopiclearnscoherentpatternsoflanguage
words. ThesedistributionshaveallowedBERTopic and demonstrates competitive and stable perfor-
tomodelthedynamicandevolutionaryaspectsof manceacrossavarietyoftasks.
| topics with | little | changes | to             | the | core algorithm. |          |     |     |     |     |     |     |     |
| ----------- | ------ | ------- | -------------- | --- | --------------- | -------- | --- | --- | --- | --- | --- | --- | --- |
| Similarly,  | with   | these   | distributions, |     | we              | can also |     |     |     |     |     |     |     |
References
modeltherepresentationsoftopicsacrossclasses.
|     |     |     |     |     |     |     | Charu C | Aggarwal, |     | Alexander | Hinneburg, |     | and |
| --- | --- | --- | --- | --- | --- | --- | ------- | --------- | --- | --------- | ---------- | --- | --- |
7.2 Weaknesses Daniel A Keim. 2001. On the surprising behavior
|                             |            |                                |              |                |     |            | of distance                              | metrics | in  | high | dimensional | space. | In    |
| --------------------------- | ---------- | ------------------------------ | ------------ | -------------- | --- | ---------- | ---------------------------------------- | ------- | --- | ---- | ----------- | ------ | ----- |
| No model                    | is perfect |                                | and BERTopic |                | is  | definitely |                                          |         |     |      |             |        |       |
|                             |            |                                |              |                |     |            | Internationalconferenceondatabasetheory, |         |     |      |             |        | pages |
| noexception.                |            | Thereareseveralweaknessestothe |              |                |     |            | 420–434.Springer.                        |         |     |      |             |        |       |
| modelthatshouldbeaddressed. |            |                                |              | First,BERTopic |     |            |                                          |         |     |      |             |        |       |
MebarkaAllaoui,MohammedLamineKherfi,andAb-
| assumes | that each | document |     | only | contains | a sin- |          |          |       |              |     |           |     |
| ------- | --------- | -------- | --- | ---- | -------- | ------ | -------- | -------- | ----- | ------------ | --- | --------- | --- |
|         |           |          |     |      |          |        | delhakim | Cheriet. | 2020. | Considerably |     | improving |     |
gle topic which does not reflect the reality that clusteringalgorithmsusingumapdimensionalityre-
| documentsmaycontainmultipletopics. |     |     |     |     |     | Although |                   |     |                    |     |     |            |     |
| ---------------------------------- | --- | --- | --- | --- | --- | -------- | ----------------- | --- | ------------------ | --- | --- | ---------- | --- |
|                                    |     |     |     |     |     |          | ductiontechnique: |     | Acomparativestudy. |     |     | InInterna- |     |
documents can be split up into smaller segments, tional Conference on Image and Signal Processing,
pages317–325.Springer.
suchassentencesandparagraphs,itisnotanideal
representation. However,asHDBSCANisasoft- DimoAngelov.2020. Top2vec:Distributedrepresenta-
clustering technique, we can use its probability tionsoftopics. arXivpreprintarXiv:2008.09470.
matrixasaproxyofthedistributionoftopicsina
|     |     |     |     |     |     |     | Alexander | Baturo, | Niheer | Dasandi, |     | and | Slava J |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------- | ------ | -------- | --- | --- | ------- |
document. Thisresolvestheissuetosomeextent Mikhaylov. 2017. Understanding state prefer-
| but it does | not | take into | account | that | documents |     |            |      |     |       |             |     |        |
| ----------- | --- | --------- | ------- | ---- | --------- | --- | ---------- | ---- | --- | ----- | ----------- | --- | ------ |
|             |     |           |         |      |           |     | ences with | text | as  | data: | Introducing |     | the un |
maycontainmultipletopicsduringthetrainingof general debate corpus. Research & Politics,
4(2):2053168017712821.
BERTopic.
Second, although BERTopic allows for a con- Kevin Beyer, Jonathan Goldstein, Raghu Ramakrish-
textual representation of documents through its nan, and Uri Shaft. 1999. When is “nearest neigh-
|     |     |     |     |     |     |     |     |     |     | International |     | conference | on  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ---------- | --- |
transformer-basedlanguagemodels,thetopicrep- bor” meaningful? In
databasetheory,pages217–235.Springer.
resentationitselfdoesnotdirectlyaccountforthat
| as they | are generated |     | from | bags-of-words. |     | The |                   |     |        |           |     |      |       |
| ------- | ------------- | --- | ---- | -------------- | --- | --- | ----------------- | --- | ------ | --------- | --- | ---- | ----- |
|         |               |     |      |                |     |     | Federico Bianchi, |     | Silvia | Terragni, | and | Dirk | Hovy. |
wordsinatopicrepresentationmerelysketchthe 2020a. Pre-training is a hot topic: Contextual-
|     |     |     |     |     |     |     | ized document |     | embeddings |     | improve | topic | coher- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ---------- | --- | ------- | ----- | ------ |
importanceofwordsinatopicwhilstthosewords
ence. arXivpreprintarXiv:2004.03974.
| are likely | to be | related. | As  | a result, | words | in a |     |     |     |     |     |     |     |
| ---------- | ----- | -------- | --- | --------- | ----- | ---- | --- | --- | --- | --- | --- | --- | --- |
topic might be similar to one another and can be Federico Bianchi, Silvia Terragni, Dirk Hovy, Debora
redundant for the interpretation of the topic. In Nozza,andElisabettaFersini.2020b. Cross-lingual
contextualizedtopicmodelswithzero-shotlearning.
theory,thiscouldberesolvedbyapplyingmaximal
arXivpreprintarXiv:2004.07737.
| marginal | relevance | to  | the top | n words |     | in a topic |     |     |     |     |     |     |     |
| -------- | --------- | --- | ------- | ------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
butitwasnotexploredinthisstudy(Carbonelland David M Blei and John D Lafferty. 2006. Dynamic
|     |     |     |     |     |     |     | topic models. |     | In Proceedings |     | of the | 23rd | interna- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | -------------- | --- | ------ | ---- | -------- |
Goldstein,1998).
|     |     |     |     |     |     |     | tional conference |     | on  | Machine | learning, | pages | 113– |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | ------- | --------- | ----- | ---- |
120.
8 Conclusion
|     |     |     |     |     |     |     | David M Blei, | Andrew |     | Y Ng, | and Michael | I   | Jordan. |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ------ | --- | ----- | ----------- | --- | ------- |
We developed BERTopic, a topic model that ex- 2003. Latentdirichletallocation. theJournalofma-
tendstheclusterembeddingapproachbyleverag- chineLearningresearch,3:993–1022.
ingstate-of-the-artlanguagemodelsandapplyinga
|     |     |     |     |     |     |     | Gerlof Bouma. | 2009. | Normalized |     | (pointwise) |     | mutual |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ----- | ---------- | --- | ----------- | --- | ------ |
class-basedTF-IDFprocedureforgeneratingtopic information in collocation extraction. Proceedings
| representations. |     | Byseparatingtheprocessofclus- |            |     |       |           | ofGSCL,30:31–40. |     |     |     |     |     |     |
| ---------------- | --- | ----------------------------- | ---------- | --- | ----- | --------- | ---------------- | --- | --- | --- | --- | --- | --- |
| tering documents |     | and                           | generating |     | topic | represen- |                  |     |     |     |     |     |     |
ZiqiangCao,SujianLi,YangLiu,WenjieLi,andHeng
| tations, | significant | flexibility |     | is introduced |     | in the |           |         |        |       |       |         |        |
| -------- | ----------- | ----------- | --- | ------------- | --- | ------ | --------- | ------- | ------ | ----- | ----- | ------- | ------ |
|          |             |             |     |               |     |        | Ji. 2015. | A novel | neural | topic | model | and its | super- |
modelallowingforeaseofusability. visedextension. InProceedingsoftheAAAIConfer-
Wepresentinthispaperanin-depthanalysisof enceonArtificialIntelligence,pages2210–2216.
| BERTopic, | ranging | from | evaluation |     | studies | with |                                      |     |     |     |     |          |     |
| --------- | ------- | ---- | ---------- | --- | ------- | ---- | ------------------------------------ | --- | --- | --- | --- | -------- | --- |
|           |         |      |            |     |         |      | JaimeCarbonellandJadeGoldstein.1998. |     |     |     |     | Theuseof |     |
classicaltopiccoherencemeasurestoanalysesin- mmr, diversity-based reranking for reordering doc-
| volving | running | times. | Our | experiments |     | suggest |        |               |     |            |     |                |     |
| ------- | ------- | ------ | --- | ----------- | --- | ------- | ------ | ------------- | --- | ---------- | --- | -------------- | --- |
|         |         |        |     |             |     |         | uments | and producing |     | summaries. |     | In Proceedings |     |

ofthe21stannualinternationalACMSIGIRconfer- Jinhyuk Lee, Wonjin Yoon, Sungdong Kim,
ence on Research and development in information Donghyeon Kim, Sunkyu Kim, Chan Ho So, and
retrieval,pages335–336. JaewooKang.2020. Biobert: apre-trainedbiomed-
|             |                    |        |          |       |       |            | ical language |                                 | representation |               | model for  | biomedical |
| ----------- | ------------------ | ------ | -------- | ----- | ----- | ---------- | ------------- | ------------------------------- | -------------- | ------------- | ---------- | ---------- |
| Daniel Cer, | Yinfei             | Yang,  | Sheng-yi |       | Kong, | Nan Hua,   |               |                                 |                |               |            |            |
|             |                    |        |          |       |       |            | textmining.   | Bioinformatics,36(4):1234–1240. |                |               |            |            |
| Nicole      | Limtiaco,          | Rhomni | St       | John, | Noah  | Constant,  |               |                                 |                |               |            |            |
|             |                    |        |          |       |       |            | YangLiu,      | ZhiyuanLiu,                     |                | Tat-SengChua, | andMaosong |            |
| Mario       | Guajardo-Cespedes, |        |          | Steve | Yuan, | Chris Tar, |               |                                 |                |               |            |            |
et al. 2018. Universal sentence encoder. arXiv Sun. 2015. Topical word embeddings. In Twenty-
preprintarXiv:1803.11175. ninthAAAIconferenceonartificialintelligence.
Jacob Devlin, Ming-Wei Chang, Kenton Lee, and YinhanLiu,MyleOtt,NamanGoyal,JingfeiDu,Man-
KristinaToutanova.2018. Bert:Pre-trainingofdeep dar Joshi, Danqi Chen, Omer Levy, Mike Lewis,
bidirectional transformers for language understand- Luke Zettlemoyer, and Veselin Stoyanov. 2019.
arXivpreprintarXiv:1810.04805. Roberta: A robustly optimized bert pretraining ap-
ing.
|                     |                                 |             |          |                   |            |         | proach.                | arXivpreprintarXiv:1907.11692. |               |                |       |             |
| ------------------- | ------------------------------- | ----------- | -------- | ----------------- | ---------- | ------- | ---------------------- | ------------------------------ | ------------- | -------------- | ----- | ----------- |
| Adji B Dieng,       |                                 | Francisco   | JR Ruiz, | and               | David      | M Blei. |                        |                                |               |                |       |             |
|                     |                                 |             |          |                   |            |         | L. McInnes,            | J. Healy,                      | and           | J. Melville.   | 2018. | UMAP:       |
| 2020.               | Topicmodelinginembeddingspaces. |             |          |                   |            | Trans-  |                        |                                |               |                |       |             |
|                     |                                 |             |          |                   |            |         | Uniform                | Manifold                       | Approximation |                | and   | Projection  |
| actions             | of the                          | Association |          | for Computational |            | Lin-    |                        |                                |               |                |       |             |
| guistics,8:439–453. |                                 |             |          |                   |            |         | forDimensionReduction. |                                |               | ArXive-prints. |       |             |
|                     |                                 |             |          |                   |            |         | Leland McInnes         |                                | and John      | Healy.         | 2017. | Accelerated |
| Cédric Févotte      |                                 | and Jérôme  | Idier.   | 2011.             | Algorithms |         |                        |                                |               |                |       |             |
for nonnegative matrix factorization with the β- hierarchical density based clustering. In Data Min-
divergence. Neuralcomputation,23(9):2421–2456. ingWorkshops(ICDMW),2017IEEEInternational
Conferenceon,pages33–42.IEEE.
| Derek Greene |           | and Pádraig | Cunningham. |             | 2006.    | Prac-    |                 |                                     |             |     |       |               |
| ------------ | --------- | ----------- | ----------- | ----------- | -------- | -------- | --------------- | ----------------------------------- | ----------- | --- | ----- | ------------- |
|              |           |             |             |             |          |          | Leland McInnes, |                                     | John Healy, | and | Steve | Astels. 2017. |
| tical        | solutions | to the      | problem     | of          | diagonal | dom-     |                 |                                     |             |     |       |               |
|              |           |             |             |             |          |          | hdbscan:        | Hierarchicaldensitybasedclustering. |             |     |       | The           |
| inance       | in kernel | document    |             | clustering. |          | In Proc. |                 |                                     |             |     |       |               |
JournalofOpenSourceSoftware,2(11):205.
23rdInternationalConferenceonMachinelearning
(ICML’06),pages377–384.ACMPress.
|     |     |     |     |     |     |     | Leland                 | McInnes, | John | Healy,               | Nathaniel | Saul, and |
| --- | --- | --- | --- | --- | --- | --- | ---------------------- | -------- | ---- | -------------------- | --------- | --------- |
|     |     |     |     |     |     |     | LukasGrossberger.2018. |          |      | Umap:Uniformmanifold |           |           |
AlexanderHoyle,PranavGoel,AndrewHian-Cheong,
|       |         |        |              |     |     |        | approximationandprojection. |     |     |     | TheJournalofOpen |     |
| ----- | ------- | ------ | ------------ | --- | --- | ------ | --------------------------- | --- | --- | --- | ---------------- | --- |
| Denis | Peskov, | Jordan | Boyd-Graber, |     | and | Philip |                             |     |     |     |                  |     |
SourceSoftware,3(29):861.
| Resnik.2021. |     | Isautomated |     | topicmodel |     | evaluation |     |     |     |     |     |     |
| ------------ | --- | ----------- | --- | ---------- | --- | ---------- | --- | --- | --- | --- | --- | --- |
broken? theincoherenceofcoherence. Advancesin Dat Quoc Nguyen, Richard Billingsley, Lan Du, and
NeuralInformationProcessingSystems,34.
|             |           |           |      |               |                  |     | MarkJohnson.2015. |             |                       | Improvingtopicmodelswith |     |              |
| ----------- | --------- | --------- | ---- | ------------- | ---------------- | --- | ----------------- | ----------- | --------------------- | ------------------------ | --- | ------------ |
|             |           |           |      |               |                  |     | latent            | feature     | word representations. |                          |     | Transactions |
| Thorsten    | Joachims. | 1996.     | A    | probabilistic | analysis         | of  |                   |             |                       |                          |     |              |
|             |           |           |      |               |                  |     | of the            | Association | for                   | Computational            |     | Linguistics, |
| the rocchio |           | algorithm | with | tfidf for     | text categoriza- |     |                   |             |                       |                          |     |              |
3:299–313.
| tion. | Technical | report, | Carnegie-mellon |     |     | univ pitts- |     |     |     |     |     |     |
| ----- | --------- | ------- | --------------- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- |
burghpadeptofcomputerscience. Divya Pandove, Shivan Goel, and Rinkl Rani. 2018.
|     |     |     |     |     |     |     | Systematic | review | of  | clustering | high-dimensional |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ------ | --- | ---------- | ---------------- | --- |
Zhenzhong Lan, Mingda Chen, Sebastian Goodman, and large datasets. ACM Transactions on Knowl-
Kevin Gimpel, Piyush Sharma, and Radu Soricut. edgeDiscoveryfromData(TKDD),12(2):1–68.
| 2019. | Albert: | A lite | bert for | self-supervised |     | learn- |     |     |     |     |     |     |
| ----- | ------- | ------ | -------- | --------------- | --- | ------ | --- | --- | --- | --- | --- | --- |
ing of language representations. arXiv preprint Jipeng Qiang, Ping Chen, Tong Wang, and Xindong
arXiv:1909.11942.
|           |       |             |          |             |     |           | Wu. 2017.                  | Topic        | modeling | over      | short              | texts by in- |
| --------- | ----- | ----------- | -------- | ----------- | --- | --------- | -------------------------- | ------------ | -------- | --------- | ------------------ | ------------ |
|           |       |             |          |             |     |           | corporatingwordembeddings. |              |          |           | InPacific-AsiaCon- |              |
| Ken Lang. | 1995. | Newsweeder: |          | Learning    |     | to filter |                            |              |          |           |                    |              |
|           |       |             |          |             |     |           | ference                    | on Knowledge |          | Discovery | and                | Data Mining, |
|           |       | Machine     | Learning | Proceedings |     | 1995,     |                            |              |          |           |                    |              |
| netnews.  | In    |             |          |             |     |           | pages363–374.Springer.     |              |          |           |                    |              |
pages331–339.Elsevier.
|     |     |     |     |     |     |     | Nils Reimers | and | Iryna | Gurevych. | 2019. | Sentence- |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | ----- | --------- | ----- | --------- |
Hugo Larochelle and Stanislas Lauly. 2012. A neural bert: Sentence embeddings using siamese bert-
autoregressivetopicmodel. AdvancesinNeuralIn- networks. InProceedingsofthe2019Conferenceon
formationProcessingSystems,25. EmpiricalMethodsinNaturalLanguageProcessing.
AssociationforComputationalLinguistics.
| Jey Han | Lau, | David Newman, |     | and Timothy |     | Baldwin. |     |     |     |     |     |     |
| ------- | ---- | ------------- | --- | ----------- | --- | -------- | --- | --- | --- | --- | --- | --- |
2014. Machine reading tea leaves: Automatically Nils Reimers and Iryna Gurevych. 2020. Mak-
| evaluating | topic | coherence |     | and topic | model | quality. |                 |     |          |     |            |           |
| ---------- | ----- | --------- | --- | --------- | ----- | -------- | --------------- | --- | -------- | --- | ---------- | --------- |
|            |       |           |     |           |       |          | ing monolingual |     | sentence |     | embeddings | multilin- |
In Proceedings of the 14th Conference of the Euro- gual using knowledge distillation. arXiv preprint
| peanChapteroftheAssociationforComputational |     |     |     |     |     |     | arXiv:2004.09813. |     |     |     |     |     |
| ------------------------------------------- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- |
Linguistics,pages530–539.
|     |     |     |     |     |     |     | Min Shi, | Jianxun | Liu, Dong | Zhou, | Mingdong | Tang, |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------- | --------- | ----- | -------- | ----- |
QuocLeandTomasMikolov.2014. Distributedrepre- andBuqingCao.2017. We-lda: awordembeddings
sentations of sentences and documents. In Interna- augmentedldamodelforwebservicesclustering. In
tionalconferenceonmachinelearning,pages1188– 2017 ieee international conference on web services
| 1196.PMLR. |     |     |     |     |     |     | (icws),pages9–16.IEEE. |     |     |     |     |     |
| ---------- | --- | --- | --- | --- | --- | --- | ---------------------- | --- | --- | --- | --- | --- |

Suzanna Sia, Ayush Dalmia, and Sabrina J Mielke.
2020. Tiredoftopicmodels? clustersofpretrained
wordembeddingsmakeforfastandgoodtopicstoo!
arXivpreprintarXiv:2004.14914.
Kaitao Song, Xu Tan, Tao Qin, Jianfeng Lu, and Tie-
Yan Liu. 2020. Mpnet: Masked and permuted pre-
trainingforlanguageunderstanding. arXivpreprint
arXiv:2004.09297.
Michael Steinbach, Levent Ertöz, and Vipin Kumar.
2004. Thechallengesofclusteringhighdimensional
data. InNewdirectionsinstatisticalphysics,pages
273–309.Springer.
Silvia Terragni, Elisabetta Fersini, Bruno Giovanni
Galuzzi, Pietro Tropeano, and Antonio Candelieri.
2021. Octis: Comparingandoptimizingtopicmod-
els is simple! In Proceedings of the 16th Confer-
enceoftheEuropeanChapteroftheAssociationfor
ComputationalLinguistics: SystemDemonstrations,
pages263–270.
Nandan Thakur, Nils Reimers, Johannes Daxenberger,
andIrynaGurevych.2020. Augmentedsbert: Data
augmentationmethodforimprovingbi-encodersfor
pairwise sentence scoring tasks. arXiv preprint
arXiv:2010.08240.
LaureThompsonandDavidMimno.2020. Topicmod-
eling with contextualized word representation clus-
ters. arXivpreprintarXiv:2010.12626.
HeZhao,DinhPhung,VietHuynh,YuanJin,LanDu,
and Wray Buntine. 2021. Topic modelling meets
deep neural networks: A survey. arXiv preprint
arXiv:2103.00498.