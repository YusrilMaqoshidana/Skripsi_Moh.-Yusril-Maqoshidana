See discussions, stats, and author profiles for this publication at: https://www.researchgate.net/publication/344233900
IndoNLU: Benchmark and Resources for Evaluating Indonesian Natural
Language Understanding
Preprint · September 2020
DOI: 10.48550/arXiv.2009.05387
CITATIONS READS
10 1,632
11 authors, including:
Bryan Wilie Karissa Vincentio
Bandung Institute of Technology Multimedia Nusantara University
43 PUBLICATIONS 2,113 CITATIONS 10 PUBLICATIONS 557 CITATIONS
SEE PROFILE SEE PROFILE
Rahmad Mahendra
University of Indonesia
75 PUBLICATIONS 1,161 CITATIONS
SEE PROFILE
All content following this page was uploaded by Bryan Wilie on 27 October 2020.
The user has requested enhancement of the downloaded file.

IndoNLU: Benchmark and Resources for Evaluating Indonesian
Natural Language Understanding
BryanWilie1∗,KarissaVincentio2∗,GentaIndraWinata3∗,SamuelCahyawijaya3∗,
XiaohongLi4,ZhiYuanLim4,SidikSoleman5,RahmadMahendra6,
PascaleFung3,SyafriBahar4,AyuPurwarianti1,5
1InstitutTeknologiBandung 2UniversitasMultimediaNusantara
3TheHongKongUniversityofScienceandTechnology
4Gojek 5Prosa.ai 6UniversitasIndonesia
{bryanwilie92, karissavin}@gmail.com, {giwinata, scahyawijaya}@connect.ust.hk
Abstract publisheddataforresearch. Oneofthelanguages
whichsufferfromthisresourcescarcityproblemis
AlthoughIndonesianisknowntobethefourth Indonesian.
most frequently used language over the inter-
Indonesian is the fourth largest language used
net, the research progress on this language
over the internet, with around 171 million users
innaturallanguageprocessing(NLP)isslow-
across the globe.1 Despite a large amount of In-
moving due to a lack of available resources.
In response, we introduce the first-ever vast donesian data available over the internet, the ad-
resource for training, evaluation, and bench- vancementofNLPresearchinIndonesianisslow-
marking on Indonesian natural language un- moving. This problem occurs because available
derstanding (IndoNLU) tasks. IndoNLU in- datasetsarescattered,withalackofdocumentation
cludes twelve tasks, ranging from single sen-
and minimal community engagement. Moreover,
tenceclassificationtopair-sentencessequence
many existing studies in Indonesian NLP do not
labeling with different levels of complexity.
providecodesandtestsplits,makingitimpossible
The datasets for the tasks lie in different do-
mains and styles to ensure task diversity. We toreproduceresults.
also provide a set of Indonesian pre-trained To address the data scarcity problem, we pro-
models (IndoBERT) trained from a large and posethefirst-everIndonesiannaturallanguageun-
clean Indonesian dataset (Indo4B) collected derstandingbenchmark,IndoNLU,acollectionof
frompubliclyavailablesourcessuchassocial
twelvediversetasks. Thetasksaremainlycatego-
media texts, blogs, news, and websites. We
rizedbasedontheinput,suchassingle-sentences
release baseline models for all twelve tasks,
and sentence-pairs, and objectives, such as sen-
as well as the framework for benchmark eval-
uation, thus enabling everyone to benchmark tence classification tasks and sequence labeling
theirsystemperformances. tasks. The benchmark is designed to cater to a
range of styles in both formal and colloquial In-
1 Introduction donesian, which are highly diverse. We collect
a range of datasets from existing works: an emo-
Following the notable success of contextual pre-
tion classification dataset (Saputri et al., 2018),
trainedlanguagemethods(Petersetal.,2018;De-
QAfactoiddataset (Purwariantietal.,2007),senti-
vlinetal.,2019),severalbenchmarkstogaugethe
mentanalysisdataset (PurwariantiandCrisdayanti,
progress of general-purpose NLP research, such
2019),aspect-basedsentimentanalysisdataset (Il-
asGLUE(Wangetal.,2018),SuperGLUE(Wang
mania et al., 2018; Azhar et al., 2019), part-of-
etal.,2019),andCLUE(Xuetal.,2020),havebeen
speech (POS) tag dataset (Dinakaramani et al.,
proposed. Thesebenchmarkscoveralargerange
2014; Hoesen andPurwarianti,2018), named en-
of tasks to measure how well pre-trained models
tity recognition (NER) dataset (Hoesen and Pur-
achievecomparedtohumans. However,thesemet-
warianti,2018),spanextractiondataset (Mahfuzh
rics are limited to high-resource languages, such
et al., 2019; Septiandri and Sutiono, 2019; Fer-
asEnglishandChinese,thatalreadyhaveexisting
nandoetal.,2019),andtextualentailmentdataset
datasetsavailableandareaccessibletotheresearch
(SetyaandMahendra,2018). Itisdifficulttocom-
community. Most languages, by contrast, suffer
paremodelperformancesincethereisnoofficial
fromlimiteddatacollectionandlowawarenessof
∗Theseauthorscontributedequally. 1https://www.internetworldstats.com/stats3.htm
0202
tcO
8
]LC.sc[
3v78350.9002:viXra

split of information for existing datasets. There- andwordsensedisambiguation.
forewestandardizethebenchmarkbyresplitting
|              |             |           |          |                 |            |      | Contextual | Language    |     | Models   |     | In recent | years, |
| ------------ | ----------- | --------- | -------- | --------------- | ---------- | ---- | ---------- | ----------- | --- | -------- | --- | --------- | ------ |
| the datasets | on          | each task | for      | reproducibility |            | pur- |            |             |     |          |     |           |        |
|              |             |           |          |                 |            |      | contextual | pre-trained |     | language |     | models    | have   |
| poses.       | To expedite | the       | modeling | and             | evaluation |      |            |             |     |          |     |           |        |
shownamajorbreakthroughinNLP,startingfrom
processesforthisbenchmark,wepresentsamples
|     |     |     |     |     |     |     | ELMo (Peters |     | et al., | 2018). | With | the emergence |     |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | ------- | ------ | ---- | ------------- | --- |
ofthemodelpre-trainingcodeandaframeworkto
|                                     |     |     |     |     |     |        | of the transformer |     | model |     | (Vaswani | et  | al., 2017), |
| ----------------------------------- | --- | --- | --- | --- | --- | ------ | ------------------ | --- | ----- | --- | -------- | --- | ----------- |
| evaluatemodelsinalldownstreamtasks. |     |     |     |     |     | Wewill |                    |     |       |     |          |     |             |
Devlinetal.(2019)proposedBERT,afasterarchi-
publishthescoreofourbenchmarkonapublicly
|     |     |     |     |     |     |     | tecture to | train | a language |     | model | that | eliminates |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----- | ---------- | --- | ----- | ---- | ---------- |
accessibleleaderboardtoprovidebettercommunity
|     |     |     |     |     |     |     | recurrences | by  | applying | a   | multi-head |     | attention |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | -------- | --- | ---------- | --- | --------- |
engagementandbenchmarktransparency.
|     |     |     |     |     |     |     | layer. Liu | et al. | (2019) | later | proposed |     | RoBERTa, |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ------ | ------ | ----- | -------- | --- | -------- |
TofurtheradvanceIndonesianNLPresearch,we
whichimprovestheperformanceofBERTbyap-
collectaroundfourbillionwordsfromIndonesian
plyingdynamicmasking,increasingthebatchsize,
| preprocessed  |        | text data | (≈ 23 | GB),                | as a new | stan- |              |     |                   |     |     |             |     |
| ------------- | ------ | --------- | ----- | ------------------- | -------- | ----- | ------------ | --- | ----------------- | --- | --- | ----------- | --- |
|               |        |           |       |                     |          |       | and removing |     | the next-sentence |     |     | prediction. | Lan |
| dard dataset, | called | Indo4B,   |       | for self-supervised |          |       |              |     |                   |     |     |             |     |
etal.(2020)proposedALBERT,whichextendsthe
| learning. | Thedatasetcomesfromsourceslikeon- |     |     |     |     |     |     |     |     |     |     |     |     |
| --------- | --------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
BERTmodelbyapplyingfactorizationandweight
| line news, | social | media, | Wikipedia, |     | online | arti- |         |           |     |        |     |            |     |
| ---------- | ------ | ------ | ---------- | --- | ------ | ----- | ------- | --------- | --- | ------ | --- | ---------- | --- |
|            |        |        |            |     |        |       | sharing | to reduce | the | number | of  | parameters | and |
cles,subtitlesfromvideorecordings,andparallel
time.
| datasets. | WethenintroduceanIndonesianBERT- |     |     |     |     |     |     |     |     |     |     |     |     |
| --------- | -------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Manyresearchstudieshaveintroducedcontex-
| basedmodel, |          | IndoBERT,whichistrainedonour |                |     |         |     |                  |          |          |        |            |            |           |
| ----------- | -------- | ---------------------------- | -------------- | --- | ------- | --- | ---------------- | -------- | -------- | ------ | ---------- | ---------- | --------- |
|             |          |                              |                |     |         |     | tual pre-trained |          | language |        | models     | on         | languages |
| Indo4B      | dataset. | We                           | also introduce |     | another | In- |                  |          |          |        |            |            |           |
|             |          |                              |                |     |         |     | other than       | English. |          | Cui et | al. (2019) | introduced |           |
doBERTvariantbasedontheALBERTmodel(Lan
|                                  |     |     |     |     |             |     | the Chinese | BERT | and | RoBERTa |     | models, | while |
| -------------------------------- | --- | --- | --- | --- | ----------- | --- | ----------- | ---- | --- | ------- | --- | ------- | ----- |
| etal.,2020),calledIndoBERT-lite. |     |     |     |     | Thetwovari- |     |             |      |     |         |     |         |       |
Martinetal.(2019)andLeetal.(2019)introduced
antsofIndoBERTareusedasbaselinemodelsin
CamemBERTandFLAUBertrespectively,which
IndoNLU
| the |     | benchmark. | In  | this | work, | we also |                |     |        |     |     |        |           |
| --- | --- | ---------- | --- | ---- | ----- | ------- | -------------- | --- | ------ | --- | --- | ------ | --------- |
|     |     |            |     |      |       |         | are BERT-based |     | models | for | the | French | language. |
extensivelycompareourIndoBERTmodelstodif-
|                    |     |      |            |     |     |          | Devlin | et al. (2019) |     | introduced |     | the Multilingual |     |
| ------------------ | --- | ---- | ---------- | --- | --- | -------- | ------ | ------------- | --- | ---------- | --- | ---------------- | --- |
| ferent pre-trained |     | word | embeddings |     | and | existing |        |               |     |            |     |                  |     |
BERTmodel,aBERTmodeltrainedonmonolin-
multilingualpre-trainedmodels,suchasMultilin-
|     |     |     |     |     |     |     | gual Wikipedia |     | data | in many | languages. |     | Mean- |
| --- | --- | --- | --- | --- | --- | --- | -------------- | --- | ---- | ------- | ---------- | --- | ----- |
gualBERT(Devlinetal.,2019)andXLM-R(Con-
|         |             |     |         |       |                |     | while, Lample |     | and | Conneau | (2019) | introduced |     |
| ------- | ----------- | --- | ------- | ----- | -------------- | --- | ------------- | --- | --- | ------- | ------ | ---------- | --- |
| neau et | al., 2019), | to  | measure | their | effectiveness. |     |               |     |     |         |        |            |     |
XLM,across-lingualpre-trainedlanguagemodel
| Results | show | that our | pre-trained | models |     | outper- |     |     |     |     |     |     |     |
| ------- | ---- | -------- | ----------- | ------ | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
thatusesparalleldataasanewtranslationmasked
formmostoftheexistingpre-trainedmodels.
|     |     |     |     |     |     |     | losstoimprovethecross-linguality. |     |     |     |     | Finally,Con- |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------------------- | --- | --- | --- | --- | ------------ | --- |
neauetal.(2019)introducedXLM-R,aRoBERTa-
2 RelatedWork
basedXLMmodel.
| Benchmarks |     | GLUE | (Wang | et al., | 2018) | is a |                    |     |     |     |     |     |     |
| ---------- | --- | ---- | ----- | ------- | ----- | ---- | ------------------ | --- | --- | --- | --- | --- | --- |
|            |     |      |       |         |       |      | 3 IndoNLUBenchmark |     |     |     |     |     |     |
multi-taskbenchmarkfornaturallanguageunder-
standing(NLU)intheEnglishlanguage. Itconsists Inthissection,wedescribeourbenchmarkasfour
ofninetasks: single-sentenceinput,semanticsim- components. Firstly, we introduce the 12 tasks
ilarity detection, and natural language inference inIndoNLUforIndonesiannaturallanguageun-
(NLI) tasks. GLUE’s harder counterpart Super- derstanding. Secondly,weintroducealarge-scale
GLUE (Wangetal.,2019)coversquestionanswer- Indonesiandatasetforself-supervisedpre-training
ing,NLI,co-referenceresolution,andwordsense models. Thirdly, we explain the various kinds of
disambiguation tasks. CLUE (Xu et al., 2020) is baselinemodelsusedinourIndoNLUbenchmark.
aChineseNLUbenchmarkthatincludesatestset Lastly, we describe the evaluation metric used to
designedtoprobeauniqueandspecificlinguistic standardizethescoringoverdifferentmodelsinour
| phenomenonintheChineselanguage. |         |        |           |                  | Itconsists |     | IndoNLUbenchmark.   |     |     |     |     |     |     |
| ------------------------------- | ------- | ------ | --------- | ---------------- | ---------- | --- | ------------------- | --- | --- | --- | --- | --- | --- |
| of eight                        | diverse | tasks, | including | single-sentence, |            |     |                     |     |     |     |     |     |     |
|                                 |         |        |           |                  |            |     | 3.1 DownstreamTasks |     |     |     |     |     |     |
sentence-pair,andmachinereadingcomprehension
tasks. FLUE(Leetal.,2019)isanevaluationNLP TheIndoNLUdownstreamtaskscovers12tasks
benchmark for the French language which is di- divided into four categories: (a) single-sentence
videdintosixdifferenttaskcategories: textclassi- classification, (b) single-sentence sequence-
fication,paraphrasing,NLI,parsing,POStagging, tagging, (c) sentence-pair classification, and (d)

Dataset |Train| |Valid| |Test| TaskDescription #Label #Class Domain Style
Single-SentenceClassificationTasks
EmoT†
|     | 3,521 |     | 440 442 | emotionclassification |     |     | 1   | 5   | tweets | colloquial |     |
| --- | ----- | --- | ------- | --------------------- | --- | --- | --- | --- | ------ | ---------- | --- |
SmSA 11,000 1,260 500 sentimentanalysis 1 3 general colloquial
CASA 810 90 180 aspect-basedsentimentanalysis 6 3 automobile colloquial
HoASA†
2,283 285 286 aspect-basedsentimentanalysis 10 4 hotel colloquial
Sentence-PairClassificationTasks
| WReTE† | 300 |     | 50 100 | textualentailment |     |     | 1   | 2   | wiki | formal |     |
| ------ | --- | --- | ------ | ----------------- | --- | --- | --- | --- | ---- | ------ | --- |
Single-SentenceSequenceLabelingTasks
| POSP† | 6,720 |     | 840 840 | part-of-speechtagging |     |     | 1   | 26  | news | formal |     |
| ----- | ----- | --- | ------- | --------------------- | --- | --- | --- | --- | ---- | ------ | --- |
BaPOS 8,000 1,000 1,029 part-of-speechtagging 1 41 news formal
| TermA | 3,000 | 1,000 | 1,000   | spanextraction |     |     | 1   | 5   | hotel   | colloquial |     |
| ----- | ----- | ----- | ------- | -------------- | --- | --- | --- | --- | ------- | ---------- | --- |
| KEPS  | 800   |       | 200 247 | spanextraction |     |     | 1   | 3   | banking | colloquial |     |
NERGrit† 1,672 209 209 namedentityrecognition 1 7 wiki formal
NERP†
|     | 6,720 |     | 840 840 | namedentityrecognition |     |     | 1   | 11  | news | formal |     |
| --- | ----- | --- | ------- | ---------------------- | --- | --- | --- | --- | ---- | ------ | --- |
Sentence-PairSequenceLabelingTasks
| FacQA | 2,495 |     | 311 311 | spanextraction |     |     | 1   | 3   | news | formal |     |
| ----- | ----- | --- | ------- | -------------- | --- | --- | --- | --- | ---- | ------ | --- |
†Wecreatenewsplitsforthedataset.
|     |     | Table1: | Taskstatisticsanddescriptions. |     |     |     |     |     |     |     |     |
| --- | --- | ------- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
sentence-pairsequencelabeling. Thedatasamples etal.,2019).2 Thedatasetcoverstendifferentas-
foreachtaskareshowninAppendixA. pectsofhotelquality. SimilartotheCASAdataset,
eachreviewislabeledwithasinglesentimentlabel
3.1.1 Single-SentenceClassificationTasks
|     |     |     |     |     |     | foreachaspect. | Therearefourpossiblesentiment |     |     |     |     |
| --- | --- | --- | --- | --- | --- | -------------- | ----------------------------- | --- | --- | --- | --- |
EmoT
An emotion classification dataset col- classes for each sentiment label: positive, nega-
| lectedfromthesocialmediaplatformTwitter |     |                            |     |     | (Sa- |                |                        |     |          |      |           |
| --------------------------------------- | --- | -------------------------- | --- | --- | ---- | -------------- | ---------------------- | --- | -------- | ---- | --------- |
|                                         |     |                            |     |     |      | tive, neutral, | and positive-negative. |     |          | The  | positive- |
| putrietal.,2018).                       |     | Thedatasetconsistsofaround |     |     |      |                |                        |     |          |      |           |
|                                         |     |                            |     |     |      | negative       | label is given         | to  | a review | that | contains  |
4000Indonesiancolloquiallanguagetweets,cover- multiplesentimentsofthesameaspectbutfordif-
| ingfivedifferentemotionlabels: |     |     |     | anger,fear,happi- |     |     |     |     |     |     |     |
| ------------------------------ | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- |
ferentobjects(e.g.,cleanlinessofbedandtoilet).
ness,love,andsadness.
3.1.2 Sentence-PairClassificationTask
| SmSA    | This sentence-level |     | sentiment    |     | analysis   |             |                                    |     |     |     |     |
| ------- | ------------------- | --- | ------------ | --- | ---------- | ----------- | ---------------------------------- | --- | --- | --- | --- |
|         |                     |     |              |     |            | WReTE       | TheWikiRevisionEditsTextualEntail- |     |     |     |     |
| dataset | (Purwarianti        | and | Crisdayanti, |     | 2019) is a |             |                                    |     |     |     |     |
|         |                     |     |              |     |            | mentdataset | (SetyaandMahendra,2018)consists    |     |     |     |     |
collectionofcommentsandreviewsinIndonesian
of450sentencepairsconstructedfromWikipedia
| obtainedfrommultipleonlineplatforms. |     |     |     |     | Thetext |                  |                               |     |     |     |     |
| ------------------------------------ | --- | --- | --- | --- | ------- | ---------------- | ----------------------------- | --- | --- | --- | --- |
|                                      |     |     |     |     |         | revisionhistory. | Thedatasetcontainspairsofsen- |     |     |     |     |
wascrawledandthenannotatedbyseveralIndone-
tencesandbinarysemanticrelationsbetweenthe
| sian linguists | to  | construct  | this   | dataset. | There are |            |               |          |             |        |          |
| -------------- | --- | ---------- | ------ | -------- | --------- | ---------- | ------------- | -------- | ----------- | ------ | -------- |
|                |     |            |        |          |           | pairs. The | data are      | labeled  | as entailed |        | when the |
| three possible |     | sentiments | on the | SmSA     | dataset:  |            |               |          |             |        |          |
|                |     |            |        |          |           | meaning    | of the second | sentence |             | can be | derived  |
positive,negative,andneutral.
fromthefirstone,andnotentailedotherwise.
| CASA | An aspect-based |     | sentiment |     | analysis |     |     |     |     |     |     |
| ---- | --------------- | --- | --------- | --- | -------- | --- | --- | --- | --- | --- | --- |
3.1.3 Single-SentenceSequenceLabeling
datasetconsistingofaroundathousandcarreviews
Tasks
collectedfrommultipleIndonesianonlineautomo-
|                |               |          |                |     |             | POSP         | This Indonesian |     | part-of-speech |     | tagging |
| -------------- | ------------- | -------- | -------------- | --- | ----------- | ------------ | --------------- | --- | -------------- | --- | ------- |
| bile platforms |               | (Ilmania | et al., 2018). |     | The dataset |              |                 |     |                |     |         |
|                |               |          |                |     |             | (POS)        | dataset (Hoesen | and | Purwarianti,   |     | 2018)   |
| covers six     | aspects       | of       | car quality.   | We  | define the  |              |                 |     |                |     |         |
|                |               |          |                |     |             | is collected | fromIndonesian  |     | newswebsites.  |     | The     |
| task to be     | a multi-label |          | classification |     | task, where |              |                 |     |                |     |         |
datasetconsistsofaround8000sentenceswith26
eachlabelrepresentsasentimentforasingleaspect
|                          |     |     |                       |     |     | POStags. | ThePOStaglabelsfollowtheIndone- |     |     |     |     |
| ------------------------ | --- | --- | --------------------- | --- | --- | -------- | ------------------------------- | --- | --- | --- | --- |
| withthreepossiblevalues: |     |     | positive,negative,and |     |     |          |                                 |     |     |     |     |
sianAssociationofComputationalLinguistics(IN-
neutral.
ACL)POSTaggingConvention.3
| HoASA | An  | aspect-based | sentiment |     | analysis |     |     |     |     |     |     |
| ----- | --- | ------------ | --------- | --- | -------- | --- | --- | --- | --- | --- | --- |
2https://github.com/annisanurulazhar/absa-playground
datasetconsistingofhotelreviewscollectedfrom
3http://inacl.id/inacl/wp-content/uploads/2017/06/INACL-
thehotelaggregatorplatform,AiryRooms (Azhar POS-Tagging-Convention-26-Mei.pdf

Emb. Hidden FFN Language Pre-train
Model #Params #Layers #Heads
Size Size Size Type Emb.Type
Scratch 15.1M 6 10 300 300 3072 Mono -
fastText-cc-id 15.1M 6 10 300 300 3072 Mono WordEmb.
fastText-indo4b 15.1M 6 10 300 300 3072 Mono WordEmb.
IndoBERT-lite 11.7M 12 12 128 768 3072 Mono Contextual
BASE
IndoBERT 124.5M 12 12 768 768 3072 Mono Contextual
BASE
IndoBERT-lite 17.7M 24 16 128 1024 4096 Mono Contextual
LARGE
IndoBERT 335.2M 24 16 1024 1024 4096 Mono Contextual
LARGE
mBERT 167.4M 12 12 768 768 3072 Multi Contextual
XLM-R 278.7M 12 12 768 768 3072 Multi Contextual
BASE
XLM-R 561.0M 24 16 1024 1024 4096 Multi Contextual
LARGE
XLM-MLM 573.2M 16 16 1280 1280 5120 Multi Contextual
LARGE
Table2: ThedetailsofbaselinemodelsusedinIndoNLUbenchmark
BaPOS ThisPOStaggingdataset(Dinakaramani threekindsofnamedentitytags,PERSON(name
et al., 2014) contains about 1000 sentences, col- ofperson),PLACE(nameoflocation),andORGA-
lectedfromthePANLocalizationProject.4 Inthis NIZATION(nameoforganization).
dataset,eachwordistaggedbyoneof23POStag
NERP ThisNERdataset (HoesenandPurwari-
classes.5 Datasplittingusedinthisbenchmarkfol-
anti, 2018) contains texts collected from several
lowstheexperimentalsettingusedbyKurniawan
Indonesian news websites. There are five labels
andAji(2018).
available in this dataset, PER (name of person),
TermA Thisspan-extractiondatasetiscollected LOC (name of location), IND (name of product
from the hotel aggregator platform, AiryRooms or brand), EVT (name of the event), and FNB
(Septiandri and Sutiono, 2019; Fernando et al., (nameoffoodandbeverage). SimilartotheTermA
2019).6 Thedatasetconsistsofthousandsofhotel dataset,theNERPdatasetusestheIOBchunking
reviews,whicheachcontainaspanlabelforaspect format.
and sentiment words representing the opinion of
3.1.4 Sentence-PairSequenceLabelingTask
therevieweronthecorrespondingaspect. Thela-
FacQA ThegoaloftheFacQAdatasetistofind
belsuseInside-Outside-Beginning(IOB)tagging
theanswertoaquestionfromaprovidedshortpas-
representationwithtwokindsoftags, aspectand
sagefromanewsarticle(Purwariantietal.,2007).
sentiment.
EachrowintheFacQAdatasetconsistsofaques-
KEPS This keyphrase extraction dataset (Mah- tion,ashortpassage,andalabelphrase,whichcan
fuzh et al., 2019) consists of text from Twitter be found inside the corresponding short passage.
discussing banking products and services and is Therearesixcategoriesofquestions: date,location,
written in the Indonesian language. A phrase name,organization,person,andquantitative.
containing important information is considered
3.2 Indo4BDataset
a keyphrase. Text may contain one or more
Indonesian NLP development has struggled with
keyphrasessinceimportantphrasescanbelocated
the availability of data. To cope with this issue,
atdifferentpositions. ThedatasetfollowstheIOB
we provide a large-scale dataset called Indo4B
chunkingformat,whichrepresentsthepositionof
for building a self-supervised pre-trained model.
thekeyphrase.
Ourself-superviseddatasetconsistsofaround4B
NERGrit This NER dataset is taken from the words,witharound250Msentences. TheIndo4B
Grit-IDrepository,7andthelabelsarespansinIOB datasetcoversbothformalandcolloquialIndone-
chunking representation. The dataset consists of siansentencescompiledfrom12datasets,ofwhich
two cover Indonesian colloquial language, eight
4http://www.panl10n.net/
cover formal Indonesian language, and the rest
5http://bahasa.cs.ui.ac.id/postag/downloads/Tagset.pdf
6https://github.com/jordhy97/final project haveamixedstyleofbothcolloquialandformal.
7https://github.com/grit-id/nergrit-corpus The statistics of our large-scale dataset can be

| Dataset |     |     |     |     |     | #Words | #Sentences |     | Size | Style Source |     |
| ------- | --- | --- | --- | --- | --- | ------ | ---------- | --- | ---- | ------------ | --- |
OSCAR(OrtizSua´rezetal.,2019) 2,279,761,186 148,698,472 14.9GB mixed OSCAR
CoNLLuCommonCrawl(Ginteretal.,2017) 905,920,488 77,715,412 6.1GB mixed LINDAT/CLARIAH-CZ
OpenSubtitles(LisonandTiedemann,2016) 105,061,204 25,255,662 664.8MB mixed OPUSOpenSubtitles
TwitterCrawl2 115,205,737 11,605,310 597.5MB colloquial Twitter
WikipediaDump1
|     |     |     |     |     | 76,263,857 |     | 4,768,444 | 528.1MB |     | formal Wikipedia |     |
| --- | --- | --- | --- | --- | ---------- | --- | --------- | ------- | --- | ---------------- | --- |
WikipediaCoNLLu(Ginteretal.,2017) 62,373,352 4,461,162 423.2MB formal LINDAT/CLARIAH-CZ
TwitterUI2(Saputrietal.,2018)
|     |     |     |     |     | 16,637,641 |     | 1,423,212 | 88MB |     | colloquial Twitter |     |
| --- | --- | --- | --- | --- | ---------- | --- | --------- | ---- | --- | ------------------ | --- |
OPUSJW300(Agic´andVulic´,2019) 8,002,490 586,911 52MB formal OPUS
| Tempo3         |     |     |     |     | 5,899,252 |         | 391,591 | 40.8MB |     | formal ILSP            |     |
| -------------- | --- | --- | --- | --- | --------- | ------- | ------- | ------ | --- | ---------------------- | --- |
| Kompas3        |     |     |     |     | 3,671,715 |         | 220,555 | 25.5MB |     | formal ILSP            |     |
| TED            |     |     |     |     | 1,483,786 |         | 111,759 | 9.9MB  |     | mixed TED              |     |
| BPPT           |     |     |     |     |           | 500,032 | 25,943  | 3.5MB  |     | formal BPPT            |     |
| ParallelCorpus |     |     |     |     |           | 510,396 | 35,174  | 3.4MB  |     | formal PANLocalization |     |
TALPCo(Nomotoetal.,2018) 8,795 1,392 56.1KB formal TokyoUniversity
FrogStorytelling(Moeljadi,2012) 1,545 177 10.1KB mixed TokyoUniversity
| TOTAL |     |     |     |     | 3,581,301,476 |     | 275,301,176 | 23.43GB |     |     |     |
| ----- | --- | --- | --- | --- | ------------- | --- | ----------- | ------- | --- | --- | --- |
|       |     |     |     | 1   |               |     |             |         |     | 2   |     |
Table 3: Indo4B dataset statistics. https://dumps.wikimedia.org/backup-index.html. We crawl tweets from
Twitter. The Twitter data will not be shared publicly due to restrictions of the Twitter Developer Policy and
| Agreement. | 3https://ilps.science.uva.nl/. |     |     |     |     |     |     |     |     |     |     |
| ---------- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
found in Table 3. We share the datasets that are coverallwordsinthevocabulary.
| listed in | the table, | except | for | those | from | Twitter |                |     |          |        |          |
| --------- | ---------- | ------ | --- | ----- | ---- | ------- | -------------- | --- | -------- | ------ | -------- |
|           |            |        |     |       |      |         | Contextualized |     | Language | Models | We build |
duetorestrictionsoftheTwitterDeveloperPolicy
and Agreement. The details of Indo4B dataset ourownIndonesianBERTandALBERTmodels,
namedIndoBERTandIndoBERT-lite,respectively,
sourcesareshowninAppendixB.
|               |          |            |     |          |     |        | inbothbaseandlargesizes.                 |     |       | ThedetailsofourIn- |        |
| ------------- | -------- | ---------- | --- | -------- | --- | ------ | ---------------------------------------- | --- | ----- | ------------------ | ------ |
| 3.3 Baselines |          |            |     |          |     |        | doBERTandIndoBERT-litemodelsareexplained |     |       |                    |        |
|               |          |            |     |          |     |        | in Section                               | 4.  | Aside | from a monolingual | model, |
| In this       | section, | we explain | the | baseline |     | models |                                          |     |       |                    |        |
wealsoprovidemultilingualmodelbaselinessuch
| and the | fine-tuning | settings |     | that we | use | in the |     |     |     |     |     |
| ------- | ----------- | -------- | --- | ------- | --- | ------ | --- | --- | --- | --- | --- |
asMultilingualBERT(Devlinetal.,2019),XLM
IndoNLUbenchmark.
|     |     |     |     |     |     |     | (LampleandConneau,2019), |             |     | andXLM-R(Con-   |           |
| --- | --- | --- | --- | --- | --- | --- | ------------------------ | ----------- | --- | --------------- | --------- |
|     |     |     |     |     |     |     | neau et                  | al., 2019). | The | details of each | model are |
3.3.1 Models
|     |     |     |     |     |     |     | showninTable |     | 2.  |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | --- | --- | --- |
Weprovideadiversesetofbaselinemodels,from
| a non-pre-trained |     | model  | (scratch), |                | to a | word- |       |                     |     |     |     |
| ----------------- | --- | ------ | ---------- | -------------- | ---- | ----- | ----- | ------------------- | --- | --- | --- |
|                   |     |        |            |                |      |       | 3.3.2 | Fine-tuningSettings |     |     |     |
| embedding-based   |     | model, | to         | contextualized |      | lan-  |       |                     |     |     |     |
Wefine-tuneapre-trainedmodelforeachtaskwith
| guage models. |     | For the | word-embeddings-based |     |     |     |     |     |     |     |     |
| ------------- | --- | ------- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
initiallearningwitharangeoflearningrates[1e-5,
model,weuseanexistingfastTextmodeltrained
|     |     |     |     |     |     |     | 4e-5]. | Weapplyadecayrateof[0.8,0.9]forevery |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------------------------------------ | --- | --- | --- |
ontheIndonesianCommonCrawl(CC-ID)dataset
epoch,andsampleeachbatchwithasizeof16for
(Joulinetal.,2016;Graveetal.,2018).
alldatasetsexceptFacQAandPOSP,forwhichwe
fastText We build a fastText model with our useabatchsizeof8. Toestablishabenchmark,we
|             |                 |           |          |          |       |     | keep a                                  | fixed | setting, | and we use an | early stop on |
| ----------- | --------------- | --------- | -------- | -------- | ----- | --- | --------------------------------------- | ----- | -------- | ------------- | ------------- |
| large-scale | self-supervised |           | dataset, | Indo4B,  |       | for |                                         |       |          |               |               |
|             |                 |           |          |          |       |     | thevalidationscoretochoosethebestmodel. |       |          |               | The           |
| comparison  | with            | the CC-ID |          | fastText | model | and |                                         |       |          |               |               |
contextualized language model. For the models detailsofthefine-tuninghyperparametersettings
above and the fastText model, we use the trans- usedareshowninAppendixD.
| former | architecture | (Vaswani |     | et al., | 2017). | We  |     |                   |     |     |     |
| ------ | ------------ | -------- | --- | ------- | ------ | --- | --- | ----------------- | --- | --- | --- |
|        |              |          |     |         |        |     | 3.4 | EvaluationMetrics |     |     |     |
experimentwithdifferentnumbersoflayers,2,4,
and6,forthetransformerencoder. ForthefastText WeusetheF1scoretomeasuretheevaluationper-
model,wefirstpre-trainthefastTextembeddings formance of all tasks. For the binary and multi-
withskipgramwordrepresentationandproducea label classification tasks, we measure the macro-
300-dimensionalembeddingvector. Wethengen- averaged F1 score by taking the top-1 prediction
erateallrequiredembeddingsforeachdownstream from the model. For the sequence labeling task,
taskfromthepre-trainedfastTextembeddingsand wecalculateword-levelsequencelabelingmacro-

|     |     |     |     | MaximumSequenceLength=128 |     |     |     | MaximumSequenceLength=512 |     |     |     |     |
| --- | --- | --- | --- | ------------------------- | --- | --- | --- | ------------------------- | --- | --- | --- | --- |
Model
BatchSize LearningRate Steps Duration(Hr.) BatchSize LearningRate Steps Duration(Hr.)
| IndoBERT-liteBASE  |     |     | 4096 |     | 0.00176 | 112.5K | 38  | 1024 | 0.00088 | 50K  |     | 23  |
| ------------------ | --- | --- | ---- | --- | ------- | ------ | --- | ---- | ------- | ---- | --- | --- |
| IndoBERTBASE       |     |     | 256  |     | 0.00002 | 1M     | 35  | 256  | 0.00002 | 68K  |     | 9   |
| IndoBERT-liteLARGE |     |     | 1024 |     | 0.00044 | 500K   | 134 | 256  | 0.00044 | 129K |     | 45  |
| IndoBERTLARGE      |     |     | 256  |     | 0.0001  | 1M     | 89  | 128  | 0.00008 | 120K |     | 32  |
Table4: HyperparametersandtrainingdurationforIndoBERTmodelpre-training.
averagedF1-scoreforallmodelsbyfollowingthe Twitter data contains specific details, such as
sequencelabelingevaluationmethoddescribedin usernames,hashtags,emails,andURLhyperlinks.
the CoNLL evaluation script. We calculate two Topreserveprivacyandalsotoreducenoise,this
mean F1-scores separately for classification and privateinformationintheTwitterUIdataset (Sa-
sequencelabelingtaskstoevaluatemodelsonour putri et al., 2018) is masked into generics tokens
| IndoNLUbenchmark. |     |     |     |     |     |     | such as     | <username>,                    | <hashtag>, |     | <email> |     |
| ----------------- | --- | --- | --- | --- | --- | --- | ----------- | ------------------------------ | ---------- | --- | ------- | --- |
|                   |     |     |     |     |     |     | and<links>. | Ontheotherhand,thisinformation |            |     |         |     |
4 IndoBERT
isdiscardedinthelargerTwitterCrawldataset.
| In this            | section,       | we  | describe | the         | details | of our    |               |     |             |              |           |         |
| ------------------ | -------------- | --- | -------- | ----------- | ------- | --------- | ------------- | --- | ----------- | ------------ | --------- | ------- |
|                    |                |     |          |             |         |           | Vocabulary    | For | both        | the IndoBERT |           | and the |
| Indonesian         | contextualized |     |          | models,     |         | IndoBERT  |               |     |             |              |           |         |
|                    |                |     |          |             |         |           | IndoBERT-lite |     | models,     | we utilize   | Sentence- |         |
| and IndoBERT-lite, |                |     | which    | are trained |         | using our |               |     |             |              |           |         |
|                    |                |     |          |             |         |           | Piece (Kudo   | and | Richardson, | 2018)        | with      | a byte  |
Indo4B
|     | dataset. |     | We elucidate |     | the extensive | de- |               |       |           |     |                |     |
| --- | -------- | --- | ------------ | --- | ------------- | --- | ------------- | ----- | --------- | --- | -------------- | --- |
|     |          |     |              |     |               |     | pair encoding | (BPE) | tokenizer | as  | the vocabulary |     |
tailsofthemodels’development,firstthedataset
|     |     |     |     |     |     |     | generationmethod. |     | Weuseavocabsizeof30.522 |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ----------------------- | --- | --- | --- |
preprocessing,followedbythepre-trainingsetup.
fortheIndoBERTmodelsandvocabsizeof30.000
fortheIndoBERT-litemodels.
4.1 Preprocessing
| DatasetPreparation |     |     | Togetthemostbeneficial |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
4.2 Pre-trainingSetup
| next | sentence | prediction |     | task training |     | from the |     |     |     |     |     |     |
| ---- | -------- | ---------- | --- | ------------- | --- | -------- | --- | --- | --- | --- | --- | --- |
Indo4B dataset, we do either a paragraph sep- All IndoBERT models are trained on TPUv3-
| aration | or line | separation |     | if we | notice | document |          |         |        |              |     |          |
| ------- | ------- | ---------- | --- | ----- | ------ | -------- | -------- | ------- | ------ | ------------ | --- | -------- |
|         |         |            |     |       |        |          | 8 in two | phases. | In the | first phase, |     | we train |
separator absence in the dataset. This document the models with a maximum sequence length of
separationiscrucialasitisusedintheBERTarchi- 128. The training takes around 35, 89, 38 and
tecturetoextractlongcontiguoussequences (De- 134 hours on IndoBERT , IndoBERT ,
|     |     |     |     |     |     |     |     |     |     | BASE |     | LARGE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | ----- |
vlinetal.,2019). Aseparationbetweensentences IndoBERT-lite , and IndoBERT-lite , re-
|     |     |     |     |     |     |     |     | BASE |     |     | LARGE |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | ----- | --- |
with a new line is also required to differentiate spectively. In the second phase, we continue the
each sentence. These are used by BERT to cre- training of the IndoBERT models with a maxi-
| ate input | embeddings |     | out | of sentence |     | pairs that |              |     |           |               |     |        |
| --------- | ---------- | --- | --- | ----------- | --- | ---------- | ------------ | --- | --------- | ------------- | --- | ------ |
|           |            |     |     |             |     |            | mum sequence |     | length of | 512. It takes | 9,  | 32, 23 |
arecompactedintoasinglesequence. Wespecify and45hoursonIndoBERT ,IndoBERT ,
|     |     |     |     |     |     |     |     |     |     | BASE |     | LARGE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | ----- |
the number of duplication factors for each of the IndoBERT-lite , and IndoBERT-lite , re-
|     |     |     |     |     |     |     |     | BASE |     |     | LARGE |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | ----- | --- |
datasets differently due to the various formats of spectively. Thedetailsofthepre-traininghyperpa-
thedatasetsthatwecollected. Wecreateduplicates rametersettingsareshowninAppendixD.
| on datasets | with | the | end | of document |     | separators |     |     |     |     |     |     |
| ----------- | ---- | --- | --- | ----------- | --- | ---------- | --- | --- | --- | --- | --- | --- |
with a higher duplication factor. The preprocess- IndoBERT We use a batch size of 256 and a
ing method is applied in both the IndoBERT and learning rate of 2e-5 in both training phases for
| IndoBERT-litemodels. |     |     |     |     |     |     | IndoBERT | ,andweadjustthelearningrateto |     |     |     |     |
| -------------------- | --- | --- | --- | --- | --- | --- | -------- | ----------------------------- | --- | --- | --- | --- |
BASE
Wekeeptheoriginalformofawordtoholdits 1e-4forIndoBERT tostabilizethetraining.
LARGE
contextualinformationsinceIndonesianwordsare Duetomemorylimitation,wescaledownthebatch
builtwithrichmorphologicaloperations,suchas size to 128 and the learning rate to 8e-5 in the
compounding, affixation, and reduplication (Pis- second phase of the training, with a number of
celdo et al., 2008). In addition, this setting is trainingstepsadaptedaccordingly. Thebaseand
alsosuitableforcontextualpre-trainingmodelsthat largemodelsaretrainedusingthemaskedlanguage
leverageinflectionstoimprovethesentence-level modelingloss. Welimitthemaximumprediction
representations.(KutuzovandKuzmenko,2019) persequenceinto20tokens.

|     |     | Classification |     | SequenceLabeling |     |     |
| --- | --- | -------------- | --- | ---------------- | --- | --- |
Model
EmoT SmSA CASA HoASA WReTE AVG POSP BaPOS TermA KEPS NERGrit NERP FacQA AVG
Scratch 57.31 67.35 67.15 76.28 64.35 66.49 86.78 70.24 70.36 39.40 5.80 30.66 5.00 44.03
fastText-cc-id 65.36 76.92 79.02 85.32 67.36 74.79 94.35 79.85 76.12 56.39 37.32 46.46 15.29 57.97
fastText-indo4b 69.23 82.13 82.20 85.88 60.42 75.97 94.94 81.77 74.43 56.70 38.69 46.79 14.65 58.28
mBERT 67.30 84.14 72.23 84.63 84.40 78.54 91.85 83.25 89.51 64.31 75.02 69.27 61.29 76.36
XLM-MLM 65.75 86.33 82.17 88.89 64.35 77.50 95.87 88.40 90.55 65.35 74.75 75.06 62.15 78.88
XLM-RBASE 71.15 91.39 91.71 91.57 79.95 85.15 95.16 84.64 90.99 68.82 79.09 75.03 64.58 79.76
XLM-RLARGE 78.51 92.35 92.40 94.27 83.82 88.27 92.73 87.03 91.45 70.88 78.26 78.52 74.61 81.92
IndoBERT-liteBASE † 73.88 90.85 89.68 88.07 82.17 84.93 91.40 75.10 89.29 69.02 66.62 46.58 54.99 70.43
+phasetwo 72.27 90.29 87.63 87.62 83.62 84.29 90.05 77.59 89.19 69.13 66.71 50.52 49.18 70.34
†
IndoBERTBASE 75.48 87.73 93.23 92.07 78.55 85.41 95.26 87.09 90.73 70.36 69.87 75.52 53.45 77.47
+phasetwo 76.28 87.66 93.24 92.70 78.68 85.71 95.23 85.72 91.13 69.17 67.42 75.68 57.06 77.34
IndoBERT-liteLARGE 75.19 88.66 90.99 89.53 78.98 84.67 91.56 83.74 90.23 67.89 71.19 74.37 65.50 77.78
+phasetwo 70.80 88.61 88.13 91.05 85.41 84.80 94.53 84.91 90.72 68.55 73.07 74.89 62.87 78.51
IndoBERTLARGE 77.08 92.72 95.69 93.75 82.91 88.43 95.71 90.35 91.87 71.18 77.60 79.25 62.48 81.21
+phasetwo 79.47 92.03 94.94 93.38 80.30 88.02 95.34 87.36 92.14 71.27 76.63 77.99 68.09 81.26
Table5: ResultsofbaselinemodelswithbestperformingconfigurationontheIndoNLUbenchmark. Extensive
†The
experimental results are shown in Appendix E. Bold numbers are the best results among all. IndoBERT
modelsaretrainedusingtwotrainingphases.
IndoBERT-lite We follow the ALBERT pre- thatallpre-trainedmodelsoutperformthescratch
training hyperparameters setup (Lan et al., 2020) model,whichshowstheeffectivenessofmodelpre-
to pre-train the IndoBERT-lite models. We limit training. Anotherinterestingobservationisthatall
themaximumpredictionpersequenceinto20to- contextualizedpre-trainedmodelsoutperformword
kensonthemodels,pre-trainingwithwholeword embeddings-basedmodelsbysignificantmargins.
maskedloss. Wetrainthebasemodelwithabatch This shows the superiority of the contextualized
size of 4096 in the first phase, and 1024 in the embeddingsapproachoverthewordembeddings
| secondphase. | Sincewehavealimitationincom- |     | approach. |     |     |     |
| ------------ | ---------------------------- | --- | --------- | --- | --- | --- |
putationpower,weuseasmallerbatchsizeof1024
in the first phase and 256 in the second phase in 5.2 Performance-SpaceTrade-off
trainingourlargemodel.
|     |     |     | Figure 1 | shows the  | model performance | with re-   |
| --- | --- | --- | -------- | ---------- | ----------------- | ---------- |
|     |     |     | spect to | the number | of parameters.    | We can see |
5 ResultsandAnalysis
|     |     |     | twolargeclusters. | Onthebottomleft,thescratch |     |     |
| --- | --- | --- | ----------------- | -------------------------- | --- | --- |
In this section, we show the results of the andfastTextmodelsappear,andtheyhavethelow-
IndoNLU benchmark and analyze the perfor- est F1 scores and the least floating points in the
|     |     |     | inference | time. On | the top right, | we can see that |
| --- | --- | --- | --------- | -------- | -------------- | --------------- |
manceofourmodelsintermsofdownstreamtasks
scoreandperformance-spacetrade-off. Inaddition, thepre-trainedmodelsachievedecentperformance,
weshowananalysisoftheeffectivenessofusing butintheinferencetime,theyincurahighcompu-
|     |     |     | tationcost. | Interestingly,inthetop-leftregion,we |     |     |
| --- | --- | --- | ----------- | ------------------------------------ | --- | --- |
ourcollecteddatacomparedtoexistingbaselines.
canseetheIndoBERT-litemodels,whichachieve
5.1 BenchmarkResults similarperformancetotheIndoBERTmodels,but
OverallPerformance AsmentionedinSection with many fewer parameters and a slightly lower
computationcost.
| 3, we fine-tune | all baseline                   | models mentioned     | in                  |     |                   |     |
| --------------- | ------------------------------ | -------------------- | ------------------- | --- | ----------------- | --- |
| Section3.3,     | andevaluatethemodelperformance |                      |                     |     |                   |     |
|                 |                                |                      | 5.3 Multilingualvs. |     | MonolingualModels |     |
| over all tasks, | grouped                        | into two categories, | clas-               |     |                   |     |
sification and sequence labeling. We can see Based on Table 5, we can conclude that contex-
in Table 5, that IndoBERT , XLM-R , tualized monolingual models outperform contex-
|     |     | LARGE | LARGE |     |     |     |
| --- | --- | ----- | ----- | --- | --- | --- |
and IndoBERT BASE achieve the top-3 best per- tualizedmultilingualmodelsontheclassification
formance results on the classification tasks, and tasks by a large margin, but on the sequence la-
XLM-R ,IndoBERT ,andXLM-R belingtasks,multilingualmodelstendtoperform
| LARGE |     | LARGE | BASE |     |     |     |
| ----- | --- | ----- | ---- | --- | --- | --- |
achievethetop-3bestperformanceresultsonthe bettercomparedtomonolingualmodelsandeven
sequencelabelingtasks. Theexperimentalresults performmuchbetterontheNERGritandFacQA
alsosuggestthatlargermodelshaveaperformance tasks. AsshowninAppendixA,boththeNERGrit
advantageoversmallermodels. Itisalsoevident andFacQAtaskscontainmanyentitynameswhich

Figure1: Performance-spacetrade-offforallbaselinemodelsonclassificationtasks(left)andsequencelabeling
tasks(right). Wetakethebestmodelforeachmodelsize. 2L,4L,and6Ldenotethenumberoflayersusedinthe
model. ThesizeofthedotsrepresentsthenumberofFLOPsofthemodel. Weusepythonpackagethoptaken
fromhttps://pypi.org/project/thop/tocalculatethenumberofFLOPs.
come from other languages, especially English. on Table 5, the fact that fastText-indo4b outper-
Thesefactssuggestthatmonolingualmodelscap- formsfastText-cc-idwithahigherscoreon10out
ture the semantic meaning of a word better than of12taskssuggeststhatarelativelysmallerdataset
multilingualmodels,butmultilingualmodelsiden- (≈23GB)cansignificantlyoutperformitslarger
tifyforeigntermsbetterthanmonolingualmodels. counterpart (≈ 180 GB). We conclude that even
|     |     |     |     |     |     | though | our Indo4B |     | dataset | is  | smaller, | it covers |
| --- | --- | --- | --- | --- | --- | ------ | ---------- | --- | ------- | --- | -------- | --------- |
5.4 EffectivenessofIndo4BDataset
|     |     |     |     |     |     | more variety |     | of the | Indonesian |     | language | and has |
| --- | --- | --- | --- | --- | --- | ------------ | --- | ------ | ---------- | --- | -------- | ------- |
bettertextqualitycomparedtotheCC-IDdataset.
| Tasks |     | #Layer fastText-cc-id |     | fastText-indo4b |     |     |     |     |     |     |     |     |
| ----- | --- | --------------------- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
5.5 EffectivenessofIndoBERTand
|     |     | 2   | 72.00 |     | 74.17 |     |     |     |     |     |     |     |
| --- | --- | --- | ----- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
IndoBERT-lite
| Classification |     | 4   | 74.79 |     | 75.97 |     |     |     |     |     |     |     |
| -------------- | --- | --- | ----- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
|                |     | 6   | 74.80 |     | 76.00 |     |     |     |     |     |     |     |
Table5showsthattheIndoBERTmodelsoutper-
|          |     | 2   | 56.26 |     | 55.55 |                                           |     |     |     |     |     |     |
| -------- | --- | --- | ----- | --- | ----- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
| Sequence |     |     |       |     |       | formthemultilingualmodelson8outof12tasks. |     |     |     |     |     |     |
|          |     | 4   | 57.97 |     | 58.28 |                                           |     |     |     |     |     |     |
Labeling
|     |     | 6   | 56.82 |     | 57.42 | Ingeneral,theIndoBERTmodelsachievethehigh- |       |     |     |                |     |          |
| --- | --- | --- | ----- | --- | ----- | ------------------------------------------ | ----- | --- | --- | -------------- | --- | -------- |
|     |     |     |       |     |       | est average                                | score | on  | the | classification |     | task. We |
Table6:ExperimentresultsonfastTextembeddingson
|         |       |                |        |     |             | conjecture | that | monolingual |     | models |     | learn better |
| ------- | ----- | -------------- | ------ | --- | ----------- | ---------- | ---- | ----------- | --- | ------ | --- | ------------ |
| IndoNLU | tasks | with different | number | of  | transformer |            |      |             |     |        |     |              |
sentiment-levelsemanticsonbothcolloquialand
layers
|     |     |     |     |     |     | formal | language | styles | than | multilingual |     | models, |
| --- | --- | --- | --- | --- | --- | ------ | -------- | ------ | ---- | ------------ | --- | ------- |
eventhoughtheIndoBERTmodels’sizeis40%–
| According |     | to Grave | et al. | (2018), | Common |              |     |             |     |          |        |         |
| --------- | --- | -------- | ------ | ------- | ------ | ------------ | --- | ----------- | --- | -------- | ------ | ------- |
|           |     |          |        |         |        | 60% smaller. |     | On sequence |     | labeling | tasks, | the In- |
Crawlisacorpuscontainingover24TB.8
Wees-
|     |     |     |     |     |     | doBERT | models | cannot |     | perform | as  | well as the |
| --- | --- | --- | --- | --- | --- | ------ | ------ | ------ | --- | ------- | --- | ----------- |
timatethesizeoftheCC-IDdatasettobearound
|                     |     |              |                   |         |         | multilingual   |     | models                    | (XLM-R) |     | in three | sequence |
| ------------------- | --- | ------------ | ----------------- | ------- | ------- | -------------- | --- | ------------------------- | ------- | --- | -------- | -------- |
| ≈180GBuncompressed. |     |              | AlthoughtheIndo4B |         |         |                |     |                           |         |     |          |          |
|                     |     |              |                   |         |         | labelingtasks: |     | POSP,NERGrit,andFacQA.One |         |     |          |          |
| dataset size        | is  | much smaller | (≈                | 23 GB), | Table 6 |                |     |                           |         |     |          |          |
ofthepossibleexplanationsisthatthesedatasets
shows us that the fastText models trained on the havemanyborrowedwordsfromEnglish,andmul-
Indo4Bdataset(fastText-indo4b)consistentlyout-
tilingualmodelshavetheadvantageintransferring
| perform | fastText | models | trained | on  | the CC-ID |     |     |     |     |     |     |     |
| ------- | -------- | ------ | ------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
learningfromEnglish.
dataset(fastText-cc-id)inbothclassificationandse-
Meanwhile,theIndoBERT-litemodelsachieve
| quencelabelingtasksinallmodelsettings. |     |     |     |     | Based |          |             |     |     |      |                |     |
| -------------------------------------- | --- | --- | --- | --- | ----- | -------- | ----------- | --- | --- | ---- | -------------- | --- |
|                                        |     |     |     |     |       | a decent | performance |     | on  | both | classification | and |
sequencelabelingtaskswiththeadvantageofcom-
8https://commoncrawl.github.io/cc-crawl-
statistics/plots/languages pact size. Interestingly, the IndoBERT-lite
LARGE

model performance is on par with that of Guzma´n, Edouard Grave, Myle Ott, Luke Zettle-
|       |       |        |     |       |             | moyer, | and Veselin |     | Stoyanov. | 2019. | Unsupervised |     |
| ----- | ----- | ------ | --- | ----- | ----------- | ------ | ----------- | --- | --------- | ----- | ------------ | --- |
| XLM-R | while | having | 16x | fewer | parameters. |        |             |     |           |       |              |     |
BASE
Wealsoobservethatincreasingthemaximumse- cross-lingualrepresentationlearningatscale. arXiv
preprintarXiv:1911.02116.
quencelengthto512inphasetwoimprovestheper-
formanceonthesequencelabelingtasks. Moreover, Yiming Cui, Wanxiang Che, Ting Liu, Bing Qin,
trainingthemodelwithlongerinputsequencesen- Ziqing Yang, Shijin Wang, and Guoping Hu. 2019.
ablesittolearntemporalinformationfromagiven Pre-training with whole word masking for chinese
bert.
textinput.
|     |     |     |     |     |     | Jacob Devlin, | Ming-Wei |     | Chang, |     | Kenton | Lee, and |
| --- | --- | --- | --- | --- | --- | ------------- | -------- | --- | ------ | --- | ------ | -------- |
6 Conclusion
|              |     |       |            |           |     | Kristina           | Toutanova.                         |              | 2019. | Bert: | Pre-training | of     |
| ------------ | --- | ----- | ---------- | --------- | --- | ------------------ | ---------------------------------- | ------------ | ----- | ----- | ------------ | ------ |
|              |     |       |            |           |     | deep bidirectional |                                    | transformers |       | for   | language     | under- |
| We introduce | the | first | Indonesian | benchmark | for |                    |                                    |              |       |       |              |        |
|              |     |       |            |           |     | standing.          | InProceedingsofthe2019Conferenceof |              |       |       |              |        |
naturallanguageunderstanding,IndoNLU,which the North American Chapter of the Association for
consists of 12 tasks, with different levels of diffi- ComputationalLinguistics: HumanLanguageTech-
culty, domains, and styles. To establish a strong nologies, Volume1(LongandShortPapers), pages
4171–4186.
baseline,wecollectlargecleanIndonesiandatasets
Indo4B,
into a dataset called which we use for Arawinda Dinakaramani, Fam Rashel, Andry Luthfi,
| training | monolingual |     | contextual | pre-trained | lan- |          |           |     |       |           |     |            |
| -------- | ----------- | --- | ---------- | ----------- | ---- | -------- | --------- | --- | ----- | --------- | --- | ---------- |
|          |             |     |            |             |      | and Ruli | Manurung. |     | 2014. | Designing |     | an indone- |
guage models, called IndoBERT and IndoBERT- sian part of speech tagset and manually tagged in-
|                |             |             |     |               |             | donesiancorpus. |          | In2014InternationalConference |             |       |            |        |
| -------------- | ----------- | ----------- | --- | ------------- | ----------- | --------------- | -------- | ----------------------------- | ----------- | ----- | ---------- | ------ |
| lite. We       | demonstrate |             | the | effectiveness | of our      |                 |          |                               |             |       |            |        |
|                |             |             |     |               |             | on Asian        | Language |                               | Processing, |       | IALP 2014, | Kuch-  |
| dataset        | and our     | pre-trained |     | models in     | capturing   |                 |          |                               |             |       |            |        |
|                |             |             |     |               |             | ing, Malaysia,  |          | October                       | 20-22,      | 2014, | pages      | 66–69. |
| sentence-level | semantics,  |             | and | apply         | them to the |                 |          |                               |             |       |            |        |
IEEE.
| classificationandsequencelabelingtasks. |     |     |     |     | Tohelp |                 |     |                     |     |     |           |     |
| --------------------------------------- | --- | --- | --- | --- | ------ | --------------- | --- | ------------------- | --- | --- | --------- | --- |
|                                         |     |     |     |     |        | JordhyFernando, |     | MasayuLeyliaKhodra, |     |     | andAliAk- |     |
withthereproducibilityofthebenchmark,were-
|                    |             |                            |         |           |          | bar Septiandri. |       | 2019.  | Aspect     | and | opinion | terms     |
| ------------------ | ----------- | -------------------------- | ------- | --------- | -------- | --------------- | ----- | ------ | ---------- | --- | ------- | --------- |
| lease the          | pre-trained |                            | models, | including | the col- |                 |       |        |            |     |         |           |
|                    |             |                            |         |           |          | extraction      | using | double | embeddings |     | and     | attention |
| lecteddataandcode. |             | Inordertoacceleratethecom- |         |           |          |                 |       |        |            |     |         |           |
mechanismforindonesianhotelreviews.
munityengagementandbenchmarktransparency,
wehavesetupaleaderboardwebsitefortheNLP FilipGinter,JanHajicˇ,JuhaniLuotolahti,MilanStraka,
|            |                                  |     |     |     |     | andDanielZeman.2017. |     |     | CoNLL2017sharedtask |     |     |     |
| ---------- | -------------------------------- | --- | --- | --- | --- | -------------------- | --- | --- | ------------------- | --- | --- | --- |
| community. | Wepublishourleaderboardwebsiteat |     |     |     |     |                      |     |     |                     |     |     |     |
-automaticallyannotatedrawtextsandwordembed-
https://indobenchmark.com/.
dings. LINDAT/CLARIAH-CZdigitallibraryatthe
InstituteofFormalandAppliedLinguistics(U´FAL),
Acknowledgments
|     |     |     |     |     |     | Faculty | of Mathematics |     | and | Physics, | Charles | Uni- |
| --- | --- | --- | --- | --- | --- | ------- | -------------- | --- | --- | -------- | ------- | ---- |
versity.
| We want       | to thank | Cahya | Wirawan, | Pallavi        | Jain, |                |     |                   |     |         |     |            |
| ------------- | -------- | ----- | -------- | -------------- | ----- | -------------- | --- | ----------------- | --- | ------- | --- | ---------- |
| Irene Gianni, | Martijn  |       | Wieriks, | Ade Romadhony, |       |                |     |                   |     |         |     |            |
|               |          |       |          |                |       | Edouard Grave, |     | Piotr Bojanowski, |     | Prakhar |     | Gupta, Ar- |
and Andrea Madotto for insightful discussions mand Joulin, and Tomas Mikolov. 2018. Learning
about this project. We sincerely thank the three word vectors for 157 languages. In Proceedings
|     |     |     |     |     |     | of the International |     |     | Conference |     | on Language | Re- |
| --- | --- | --- | --- | --- | --- | -------------------- | --- | --- | ---------- | --- | ----------- | --- |
anonymousreviewersfortheirinsightfulcomments
sourcesandEvaluation(LREC2018).
onourpaper.
|     |     |     |     |     |     | Devin Hoesen | and | Ayu      | Purwarianti. |     | 2018.     | Investigat- |
| --- | --- | --- | --- | --- | --- | ------------ | --- | -------- | ------------ | --- | --------- | ----------- |
|     |     |     |     |     |     | ing bi-lstm  | and | crf with | pos          | tag | embedding | for in-     |
References
|               |     |              |       |        |         | donesiannamedentitytagger. |     |       |          | In2018International |     |         |
| ------------- | --- | ------------ | ----- | ------ | ------- | -------------------------- | --- | ----- | -------- | ------------------- | --- | ------- |
|               |     |              |       |        |         | Conference                 | on  | Asian | Language | Processing          |     | (IALP), |
| Zˇeljko Agic´ | and | Ivan Vulic´. | 2019. | Jw300: | A wide- |                            |     |       |          |                     |     |         |
pages35–38.IEEE.
coverageparallelcorpusforlow-resourcelanguages.
| In Proceedings |     | of the        | 57th | Annual Meeting | of the |                  |           |        |              |           |     |           |
| -------------- | --- | ------------- | ---- | -------------- | ------ | ---------------- | --------- | ------ | ------------ | --------- | --- | --------- |
|                |     |               |      |                |        | Arfinda Ilmania, |           | Samuel | Cahyawijaya, |           | Ayu | Purwari-  |
| Association    | for | Computational |      | Linguistics,   | pages  |                  |           |        |              |           |     |           |
|                |     |               |      |                |        | anti, et         | al. 2018. | Aspect |              | detection | and | sentiment |
3204–3210.
classificationusingdeepneuralnetworkforindone-
|              |     |            |     |                |       | sianaspect-basedsentimentanalysis. |     |     |     |     | In2018Inter- |     |
| ------------ | --- | ---------- | --- | -------------- | ----- | ---------------------------------- | --- | --- | --- | --- | ------------ | --- |
| A. N. Azhar, | M.  | L. Khodra, | and | A. P. Sutiono. | 2019. |                                    |     |     |     |     |              |     |
Multi-labelaspectcategorizationwithconvolutional nationalConferenceonAsianLanguageProcessing
neural networks and extreme gradient boosting. In (IALP),pages62–67.IEEE.
| 2019 | International | Conference |     | on Electrical | Engi- |                |     |         |        |       |             |     |
| ---- | ------------- | ---------- | --- | ------------- | ----- | -------------- | --- | ------- | ------ | ----- | ----------- | --- |
|      |               |            |     |               |       | Armand Joulin, |     | Edouard | Grave, | Piotr | Bojanowski, |     |
neeringandInformatics(ICEEI),pages35–40.
|     |     |     |     |     |     | Matthijs | Douze, | He´rve | Je´gou, | and | Tomas | Mikolov. |
| --- | --- | --- | --- | --- | --- | -------- | ------ | ------ | ------- | --- | ----- | -------- |
AlexisConneau, KartikayKhandelwal, NamanGoyal, 2016. Fasttext.zip: Compressing text classification
Vishrav Chaudhary, Guillaume Wenzek, Francisco models. arXivpreprintarXiv:1612.03651.

TakuKudoandJohnRichardson.2018. SentencePiece: Hiroki Nomoto, Kenji Okano, David Moeljadi, and
A simple and language independent subword tok- Hideo Sawada. 2018. Tufs asian language parallel
enizeranddetokenizerforneuraltextprocessing. In corpus(talpco). InProceedingsoftheTwenty-fourth
Proceedings of the 2018 Conference on Empirical AnnualMeetingoftheAssociationforNaturalLan-
Methods in Natural Language Processing: System guageProcessing,pages436–439.
Demonstrations, pages 66–71, Brussels, Belgium.
AssociationforComputationalLinguistics. Pedro Javier Ortiz Sua´rez, Benoˆıt Sagot, and Laurent
Romary.2019. AsynchronousPipelineforProcess-
KemalKurniawanandAlhamFikriAji.2018. Toward
ingHugeCorporaonMediumtoLowResourceIn-
astandardizedandmoreaccurateindonesianpart-of-
frastructures. In 7th Workshop on the Challenges
speech tagging. In 2018 International Conference
in the Management of Large Corpora (CMLC-
on Asian Language Processing (IALP), pages 303–
7), Cardiff, United Kingdom. Leibniz-Institut fu¨r
307.IEEE.
DeutscheSprache.
Andrey Kutuzov and Elizaveta Kuzmenko. 2019. To
lemmatize or not to lemmatize: How word normal- Matthew Peters, Mark Neumann, Mohit Iyyer, Matt
isation affects ELMo performance in word sense Gardner, Christopher Clark, Kenton Lee, and Luke
disambiguation. In Proceedings of the First NLPL Zettlemoyer.2018. Deepcontextualizedwordrepre-
Workshop on Deep Learning for Natural Language sentations. In Proceedings of the 2018 Conference
Processing,pages22–28,Turku,Finland.Linko¨ping of the North American Chapter of the Association
UniversityElectronicPress. for Computational Linguistics: Human Language
Technologies,Volume1(LongPapers),pages2227–
Guillaume Lample and Alexis Conneau. 2019. Cross- 2237.
lingual language model pretraining. CoRR,
abs/1901.07291. FemphyPisceldo,RahmadMahendra,RuliManurung,
and I Wayan Arka. 2008. A two-level morpholog-
Zhenzhong Lan, Mingda Chen, Sebastian Goodman,
ical analyser for the indonesian language. In Pro-
Kevin Gimpel, Piyush Sharma, and Radu Soricut.
ceedings of the Australasian Language Technology
2020. Albert:Alitebertforself-supervisedlearning
AssociationWorkshop2008,pages142–150.
of language representations. In International Con-
ferenceonLearningRepresentations.
Ayu Purwarianti and Ida Ayu Putu Ari Crisdayanti.
HangLe,Lo¨ıcVial,JibrilFrej,VincentSegonne,Max- 2019. Improving bi-lstm performance for in-
iminCoavoux, BenjaminLecouteux, AlexandreAl- donesian sentiment analysis using paragraph vec-
lauzen,BenoˆıtCrabbe´,LaurentBesacier,andDidier tor. In 2019 International Conference of Advanced
Schwab. 2019. Flaubert: Unsupervised language Informatics: Concepts, Theory and Applications
modelpre-trainingforfrench. (ICAICTA),pages1–5.IEEE.
Pierre Lison and Jo¨rg Tiedemann. 2016. Opensub-
AyuPurwarianti,MasatoshiTsuchiya,andSeiichiNak-
titles2016: Extracting large parallel corpora from
agawa. 2007. A machine learning approach for in-
movieandtvsubtitles. InProceedingsofthe10thIn-
donesian question answering system. In Artificial
ternationalConferenceonLanguageResourcesand
IntelligenceandApplications,pages573–578.
Evaluation.
YinhanLiu,MyleOtt,NamanGoyal,JingfeiDu,Man- Mei Silviana Saputri, Rahmad Mahendra, and Mirna
dar Joshi, Danqi Chen, Omer Levy, Mike Lewis, Adriani.2018. Emotionclassificationonindonesian
Luke Zettlemoyer, and Veselin Stoyanov. 2019. twitter dataset. In 2018 International Conference
Roberta: A robustly optimized bert pretraining ap- onAsianLanguageProcessing(IALP),pages90–95.
proach. arXivpreprintarXiv:1907.11692. IEEE.
Miftahul Mahfuzh, Sidik Soleman, and Ayu Pur- AliAkbarSeptiandriandAriePratamaSutiono.2019.
warianti. 2019. Improving joint layer rnn based Aspectandopiniontermextractionforaspectbased
keyphrase extraction by using syntactical features. sentiment analysis of hotel reviews using transfer
In 2019 International Conference of Advanced In- learning.
formatics: Concepts, Theory and Applications
(ICAICTA),pages1–6.IEEE.
Ken Nabila Setya and Rahmad Mahendra. 2018.
Semi-supervised textual entailment on indonesian
Louis Martin, Benjamin Muller, Pedro Javier Ortiz
Sua´rez,YoannDupont,LaurentRomary,E´ricVille- wikipedia data. In 2018 International Conference
on Computational Linguistics and Intelligent Text
monte de la Clergerie, Djame´ Seddah, and Benoˆıt
Processing(CICLing).
Sagot. 2019. Camembert: a tasty french language
model.
Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob
David Moeljadi. 2012. Usage of indonesian posses- Uszkoreit, Llion Jones, Aidan N Gomez, Łukasz
siveverbalpredicates: astatisticalanalysisbasedon Kaiser, and Illia Polosukhin. 2017. Attention is all
questionnaire and storytelling surveys. In APLL-5 you need. In Advances in neural information pro-
conference.SOAS,UniversityofLondon. cessingsystems,pages5998–6008.

| Alex Wang,      | Yada       | Pruksachatkun, |     | Nikita           | Nangia, |
| --------------- | ---------- | -------------- | --- | ---------------- | ------- |
| AmanpreetSingh, |            | JulianMichael, |     | FelixHill,       | Omer    |
| Levy,           | and Samuel | Bowman.        |     | 2019. Superglue: | A       |
stickierbenchmarkforgeneral-purposelanguageun-
| derstanding | systems. |     | In Advances | in  | Neural Infor- |
| ----------- | -------- | --- | ----------- | --- | ------------- |
mationProcessingSystems,pages3261–3275.
| Alex Wang,                          | Amanpreet        |                | Singh,   | Julian Michael, | Felix        |
| ----------------------------------- | ---------------- | -------------- | -------- | --------------- | ------------ |
| Hill,OmerLevy,andSamuelBowman.2018. |                  |                |          |                 | Glue:        |
| A multi-task                        |                  | benchmark      | and      | analysis        | platform for |
| natural                             | language         | understanding. |          | In              | Proceedings  |
| of the                              | 2018 EMNLP       |                | Workshop | BlackboxNLP:    | An-          |
| alyzing                             | and Interpreting |                | Neural   | Networks        | for NLP,     |
pages353–355.
| Liang Xu,   | Xuanwei       | Zhang, | Lu         | Li, Hai    | Hu, Chen-    |
| ----------- | ------------- | ------ | ---------- | ---------- | ------------ |
| jie Cao,    | Weitang       | Liu,   | Junyi      | Li, Yudong | Li, Kai      |
| Sun, Yechen |               | Xu, et | al. 2020.  | Clue: A    | chinese lan- |
| guage       | understanding |        | evaluation | benchmark. | arXiv        |
preprintarXiv:2004.05986.

| A DataSamples |     |     |     | C Pre-TrainingHyperparameters |     |     |
| ------------- | --- | --- | --- | ----------------------------- | --- | --- |
Inthissection,weshowexamplesfordownstream Inthissection,weshowallhyperparametersused
tasksintheIndoNLUbenchmark. inourIndoBERTandIndoBERT-litetrainingpro-
cess. ThehyperparametersisshowninTable20.
| • The   | examples of | SmSA task | are shown | in                           |     |     |
| ------- | ----------- | --------- | --------- | ---------------------------- | --- | --- |
| Table7. |             |           |           | D Fine-TuningHyperparameters |     |     |
• TheexamplesofEmoTtaskareshowninTa-
Inthissection,weshowallhyperparametersused
| ble8. |     |     |     | inthefine-tuningprocessofeachbaselinemodel. |     |     |
| ----- | --- | --- | --- | ------------------------------------------- | --- | --- |
ThehyperparameterconfigurationisshowninTa-
• TheexamplesofKEPStaskareshowninTa-
ble21.
ble9.
E ExtensiveExperimentResultson
| • The | examples of | HoASA | task are shown | in  |     |     |
| ----- | ----------- | ----- | -------------- | --- | --- | --- |
IndoNLUBenchmark
Table10.
Inthissection,weshowallexperimentsconducted
| • The | examples of | CASA task | are shown | in                     |                 |     |
| ----- | ----------- | --------- | --------- | ---------------------- | --------------- | --- |
|       |             |           |           | intheIndoNLUbenchmark. | Weuseabatchsize |     |
Table11.
of16foralldatasetsexceptFacQAandPOSP,for
| • The    | examples of | WReTE | task are shown | in                                |     |                 |
| -------- | ----------- | ----- | -------------- | --------------------------------- | --- | --------------- |
|          |             |       |                | whichweuseabatchsizeof8.          |     | Theresultsofthe |
| Table12. |             |       |                | fullexperimentsareshowninTable22. |     |                 |
• TheexamplesofNERGrittaskareshownin
Table13.
• TheexamplesofNERPtaskareshowninTa-
ble14.
| • The | examples of | BaPOS task | are shown | in  |     |     |
| ----- | ----------- | ---------- | --------- | --- | --- | --- |
Table15.
• TheexamplesofPOSPtaskareshowninTa-
ble16.
| • The | examples of | FacQA task | are shown | in  |     |     |
| ----- | ----------- | ---------- | --------- | --- | --- | --- |
Table17.
| • The | examples of | TermA task | are shown | in  |     |     |
| ----- | ----------- | ---------- | --------- | --- | --- | --- |
Table18.
B Indo4BDataSources
Inthissection,weshowthesourceofeachdataset
| that we | use to build | our Indo4B | dataset. | The |     |     |
| ------- | ------------ | ---------- | -------- | --- | --- | --- |
sourceofeachcorpusisshowninTable19.
| Sentence                                                      |                      |     |     | Sentiment    |                    |                    |
| ------------------------------------------------------------- | -------------------- | --- | --- | ------------ | ------------------ | ------------------ |
| pengecutdiaitu,cumabisanantangindaribelakangsaja              |                      |     |     | neg          |                    |                    |
| wortelmengandungvitaminayangbisajagakesehatanmata             |                      |     |     | neut         |                    |                    |
| mochafloatkfcituminumanterenakyangpernahguerasain             |                      |     |     | pos          |                    |                    |
| Table7:                                                       | SampledataontaskSmSA |     |     |              |                    |                    |
|                                                               |                      |     |     | Word Layanan | BCA Mobile         | Banking Bermasalah |
|                                                               |                      |     |     | Keyphrase O  | B I                | I B                |
|                                                               |                      |     |     | Word Tidak   | mengecewakan pakai | BCA Mobile         |
| Tweet                                                         |                      |     |     | Emotion      |                    |                    |
|                                                               |                      |     |     | Keyphrase O  | O B                | B I                |
| Masalahgaakanpernahmenjauh,hadapiSelasamudenganpenuhsemangat! |                      |     |     | happy        |                    |                    |
Sayangseribusayangnamuntakadasatupunygnyangkutsampaisekarang sadness Word nggak ada tandingannya e-channel BCA
|                                                                |                              |     |     | Keyphrase B | I I                  | B I |
| -------------------------------------------------------------- | ---------------------------- | --- | --- | ----------- | -------------------- | --- |
| ceweksukabolaitudimatacowokcantiknyanambah,biarpunmatanyapanda |                              |     |     | love        |                      |     |
|                                                                | Table8: SampledataontaskEmoT |     |     | Table9:     | SampledataontaskKEPS |     |

Aspect
Sentence
|     |     | AC  | AirPanas Bau | General Kebersihan | Linen | Service | SunriseMeal | TV WiFi |
| --- | --- | --- | ------------ | ------------------ | ----- | ------- | ----------- | ------- |
airpanaskurangberfungsidanhanduklembab. neut neg neut neut neut neg neut neut neut neut
Showerzonk,resepsionisyangwanitajudes neut neut neut neut neut neut neg neut neut neut
Kamarkurangbersih,terutamakamarmandi. neut neut neut neut neg neut neut neut neut neut
Table10: SampledataontaskHoASA
Aspect
Sentence
|     |                                                 |     |     | Fuel Machine | Others | Part Price | Service |     |
| --- | ----------------------------------------------- | --- | --- | ------------ | ------ | ---------- | ------- | --- |
|     | bodiplustampilannyaAvanzabarumantapjuragan      |     |     | neut neut    | neut   | pos neut   | neut    |     |
|     | udahgayanyastylishekonomispula,belicalyadeh     |     |     | neut neut    | neut   | pos pos    | neut    |     |
|     | MobilkualitasjelekkayakwulingsajamasukIndonesia |     |     | neut neut    | neg    | neut neut  | neut    |     |
Table11: SampledataontaskCASA
| SentenceA |     |     | SentenceB |     |     |     | Label |     |
| --------- | --- | --- | --------- | --- | --- | --- | ----- | --- |
Anaksebaiknyamenjalanitirahbaring Anaksebaiknyamenjalaniistirahat EntailorParaphrase
Keduakatainiditulisdenganhurufkanjiyangsama JepangdisebutNipponatauNihondalambahasaJepang NotEntail
Elektronhanyamenduduki0,06%massatotalatom Elektronhanyamengambil0,06%massatotalatom EntailorParaphrase
Table12: SampledataontaskWReTE
Word Produser David Heyman dan sutradara Mark Herman sedang mencari seseorang
| Entity | O B-PER I-PER | O   | O   | B-PER | I-PERS | O   | O   | O   |
| ------ | ------------- | --- | --- | ----- | ------ | --- | --- | --- |
Word Pada tahun 1996 Williams pindah ke Sebastopol , California di
| Entity | O O O | B-PER | O   | O   | B-PLA | O   | B-PLA | O   |
| ------ | ----- | ----- | --- | --- | ----- | --- | ----- | --- |
Word bekerja untuk penerbitan perusahaan teknologi O , Reilly Media .
| Entity | O O O | O   | O   | B-ORG | I-ORG | I-ORG | I-ORG | O   |
| ------ | ----- | --- | --- | ----- | ----- | ----- | ----- | --- |
Table13: SampledataontaskNERGrit. PER=PERSON,ORG=ORGANIZATION,PLA=PLACE
Word kepala dinas tata kota manado amos kenda menyatakan tidak tahu
| Entity | O O O | O   | B-PLC | B-PPL | I-PPL | O   | O   | O   |
| ------ | ----- | --- | ----- | ----- | ----- | --- | --- | --- |
Word telah mendaftar untuk menjadi official merchant bandung great sale 2017
| Entity | O O O | O   | O   | O   | B-EVT | I-EVT | I-EVT | I-EVT |
| ------ | ----- | --- | --- | --- | ----- | ----- | ----- | ----- |
Word sekitar timur dan barat arnhem , katherine dan daerah sekitar
| Entity | O B-PLC O                                                    | B-PLC | I-PLC | O   | B-PLC | O   | O   | O   |
| ------ | ------------------------------------------------------------ | ----- | ----- | --- | ----- | --- | --- | --- |
|        | Table14: SampledataontaskNERP.PLC=PLACE,PPL=PEOPLE,EVT=EVENT |       |       |     |       |     |     |     |
Word Pemerintah kota Delhi mengerahkan monyet untuk mengusir monyet-monyet lain yang
| Tag | B-NNP B-NNP B-NNP |     | B-VB | B-NN B-SC | B-VB | B-NN |     | B-JJ B-SC |
| --- | ----------------- | --- | ---- | --------- | ---- | ---- | --- | --------- |
Word Beberapa laporan menyebutkan setidaknya 10 monyet ditempatkan di luar arena
| Tag | B-CD B-NN B-VB |     | B-RB | B-CD B-NN | B-VB | B-IN |     | B-NN B-NN |
| --- | -------------- | --- | ---- | --------- | ---- | ---- | --- | --------- |
Word berencana mendatangkan 10 monyet sejenis dari negara bagian Rajasthan .
| Tag | B-VB B-VB B-CD |     | B-NN | B-NN B-IN | B-NNP | I-NNP |     | B-NNP B-Z |
| --- | -------------- | --- | ---- | --------- | ----- | ----- | --- | --------- |
Table15: SampledataontaskBaPOS.POStaglabelsfollowUniversitasIndonesiaPOSTagStandard. 9
Word kepala dinas tata kota manado amos kenda menyatakan tidak tahu
Tag B-NNO B-VBP B-NNO B-NNO B-NNP B-NNP B-NNP B-VBT B-NEG B-VBI
Word telah mendaftar untuk menjadi official merchant bandung great sale 2017
Tag B-ADK B-VBI B-PPO B-VBL B-NNO B-NNP B-NNP B-NNP B-NNP B-NUM
Word sekitar timur dan barat arnhem , katherine dan daerah sekitar
Tag B-PPO B-NNP B-CCN B-NNP B-NNP B-SYM B-NNP B-CCN B-NNO B-ADV
10
Table16: SampledataontaskPOSPPOStaglabelsfollowINACLPOSTaggingConvention.

| Question ”SiapakahpenasihatutamaPresidenASGeorgeWBush?”         |           |          |          |                   |     |     |
| --------------------------------------------------------------- | --------- | -------- | -------- | ----------------- | --- | --- |
| Passage Nasib                                                   | Karl      | Rove     | Akan     | Segera Diputuskan |     |     |
| Label O                                                         | B         | I        | O        | O O               |     |     |
| Question ”Dimanaterjadinyaletusangunungberapidahsyattahun1883?” |           |          |          |                   |     |     |
| Passage Di                                                      | Kepulauan | Krakatau | Terdapat | 400 Tanaman       |     |     |
| Label O                                                         | B         | I        | O        | O O               |     |     |
Question ”Perusahaanapakahyangsejak1Januari2006,menurunkanhargapertamaxdanpertamaxplus?”
Passage Pesaing Semakin Banyak , Pertamina Berusaha Kompetitif
| Label O | O   | O        | O                     | B O | O   |     |
| ------- | --- | -------- | --------------------- | --- | --- | --- |
|         |     | Table17: | SampledataontaskFacQA |     |     |     |
Word sayang wifi tidak bagus harus keluar kamar . fasilitas lengkap
| Entity O       | B-ASP | B-SEN  | I-SEN O    | O O         | O B-ASP     | B-SEN |
| -------------- | ----- | ------ | ---------- | ----------- | ----------- | ----- |
| Word pelayanan | nya   | sangat | bagus .    | kamar nya   | juga oke    | .     |
| Entity B-ASP   | I-ASP | B-SEN  | I-SEN O    | B-ASP I-ASP | O B-SEN     | O     |
| Word kamar     | cukup | luas   | , interior | menarik dan | unik sekali | ,     |
| Entity B-ASP   | B-SEN | I-SEN  | O B-ASP    | B-SEN O     | B-SEN I-SEN | O     |
Table18: SampledataontaskTermA.SEN=SENTIMENT,ASP=ASPECT
| CorpusName | Source | PublicURL                                                  |     |     |     |     |
| ---------- | ------ | ---------------------------------------------------------- | --- | --- | --- | --- |
| OSCAR      | OSCAR  | https://oscar-public.huma-num.fr/compressed/iddedup.txt.gz |     |     |     |     |
CoNLLuCommonCrawl LINDAT/CLARIAH-CZ https://lindat.mff.cuni.cz/repository/xmlui/bitstream/handle/11234/1-1989/Indonesian-annotated-conll17.tar
OpenSubtitles OPUSOpenSubtitles http://opus.nlpl.eu/download.php?f=OpenSubtitles/v2016/mono/OpenSubtitles.raw.id.gz
WikipediaDump Wikipedia https://dumps.wikimedia.org/idwiki/20200401/idwiki-20200401-pages-articles-multistream.xml.bz2
WikipediaCoNLLu LINDAT/CLARIAH-CZ https://lindat.mff.cuni.cz/repository/xmlui/bitstream/handle/11234/1-1989/Indonesian-annotated-conll17.tar
| TwitterCrawl | Twitter | Notpubliclyavailable          |     |     |     |     |
| ------------ | ------- | ----------------------------- | --- | --- | --- | --- |
| TwitterUI    | Twitter | Notpubliclyavailable          |     |     |     |     |
| OPUSJW300    | OPUS    | http://opus.nlpl.eu/JW300.php |     |     |     |     |
Tempo ILSP http://ilps.science.uva.nl/ilps/wp-content/uploads/sites/6/files/bahasaindonesia/tempo.zip
Kompas ILSP http://ilps.science.uva.nl/ilps/wp-content/uploads/sites/6/files/bahasaindonesia/kompas.zip
TED TED https://github.com/ajinkyakulkarni14/TED-Multilingual-Parallel-Corpus/tree/master/Monolingualdata
BPPT BPPT http://www.panl10n.net/english/outputs/Indonesia/BPPT/0902/BPPTIndToEngCorpusHalfM.zip
ParallelCorpus PANLocalization http://panl10n.net/english/outputs/Indonesia/UI/0802/Parallel/%20Corpus.zip
| TALPCo                    | TokyoUniversity | https://github.com/matbahasa/TALPCo                       |                       |               |               |       |
| ------------------------- | --------------- | --------------------------------------------------------- | --------------------- | ------------- | ------------- | ----- |
| FrogStorytelling          | TokyoUniversity | https://github.com/davidmoeljadi/corpus-frog-storytelling |                       |               |               |       |
|                           |                 |                                                           | Table19: Indo4BCorpus |               |               |       |
| Hyperparameter            |                 | IndoBERT                                                  | IndoBERT              | IndoBERT-lite | IndoBERT-lite |       |
|                           |                 |                                                           | BASE                  | LARGE         | BASE          | LARGE |
| attentionprobsdropoutprob |                 |                                                           | 0.1                   | 0.1           | 0             | 0     |
| hiddenact                 |                 |                                                           | gelu                  | gelu          | gelu          | gelu  |
| hiddendropoutprob         |                 |                                                           | 0.1                   | 0.1           | 0             | 0     |
| embeddingsize             |                 |                                                           | 768                   | 1024          | 128           | 128   |
| hiddensize                |                 |                                                           | 768                   | 1024          | 768           | 1024  |
| initializerrange          |                 |                                                           | 0.02                  | 0.02          | 0.02          | 0.02  |
| intermediatesize          |                 |                                                           | 3072                  | 4096          | 3072          | 4096  |
| maxpositionembeddings     |                 |                                                           | 512                   | 512           | 512           | 512   |
| numattentionheads         |                 |                                                           | 12                    | 16            | 12            | 16    |
| numhiddenlayers           |                 |                                                           | 12                    | 24            | 12            | 24    |
| typevocabsize             |                 |                                                           | 2                     | 2             | 2             | 2     |
| vocabsize                 |                 |                                                           | 30522                 | 30522         | 30000         | 30000 |
| numhiddengroups           |                 |                                                           | -                     | -             | 1             | 1     |
| netstructuretype          |                 |                                                           | -                     | -             | 0             | 0     |
| gapsize                   |                 |                                                           | -                     | -             | 0             | 0     |
| nummemoryblocks           |                 |                                                           | -                     | -             | 0             | 0     |
| innergroupnum             |                 |                                                           | -                     | -             | 1             | 1     |
| downscalefactor           |                 |                                                           | -                     | -             | 1             | 1     |
Table20: HyperparameterconfigurationsforIndoBERTandIndoBERT-litepre-trainedmodels.

batch size n layers n epochs lr early stop gamma max norm seed
| Scratch         | [8,16] | [2,4,6] | 25  | 1e-4 | 12  | 0.9 | 10 42 |
| --------------- | ------ | ------- | --- | ---- | --- | --- | ----- |
| fastText-cc-id  | [8,16] | [2,4,6] | 25  | 1e-4 | 12  | 0.9 | 10 42 |
| fastText-indo4B | [8,16] | [2,4,6] | 25  | 1e-4 | 12  | 0.9 | 10 42 |
| mBERT           | [8,16] | 12      | 25  | 1e-5 | 12  | 0.9 | 10 42 |
| XLM-MLM         | [8,16] | 16      | 25  | 1e-5 | 12  | 0.9 | 10 42 |
| XLM-R           | [8,16] | 12      | 25  | 2e-5 | 12  | 0.9 | 10 42 |
BASE
| XLM-R LARGE   | [8,16]      | 24  | 25  | 1e-5        | 12  | 0.9 | 10 42 |
| ------------- | ----------- | --- | --- | ----------- | --- | --- | ----- |
| IndoBERT-lite | BASE [8,16] | 12  | 25  | 1e-5        | 12  | 0.9 | 10 42 |
| +phase2       | [8,16]      | 12  | 25  | 1e-5        | 12  | 0.9 | 10 42 |
| IndoBERT-lite | [8,16]      | 24  | 25  | [1e-5,2e-5] | 12  | 0.9 | 10 42 |
LARGE
| +phase2  | [8,16]      | 24  | 25  | 2e-5        | 12  | 0.9 | 10 42 |
| -------- | ----------- | --- | --- | ----------- | --- | --- | ----- |
| IndoBERT | BASE [8,16] | 12  | 25  | [1e-5,4e-5] | 12  | 0.9 | 10 42 |
| +phase2  | [8,16]      | 12  | 25  | 4e-5        | 12  | 0.9 | 10 42 |
| IndoBERT | [8,16]      | 24  | 25  | 4e-5        | 12  | 0.9 | 10 42 |
LARGE
| +phase2 | [8,16] | 24  | 25  | [3e-5,4e-5] | 12  | 0.9 | 10 42 |
| ------- | ------ | --- | --- | ----------- | --- | --- | ----- |
Table 21: Hyperparameter configurations for fine-tuning in IndoNLU benchmark. We use a batch size of 8 for
POSP and FacQA, and a batch size of 16 for EmoT, SmSA, CASA, HoASA, WReTE, BaPOS, TermA, KEPS,
NERGrit,andNERP.
|       |                 |           | Classification |           |                  | SequenceLabeling |                |
| ----- | --------------- | --------- | -------------- | --------- | ---------------- | ---------------- | -------------- |
| Model | LR #Layer Param |           |                |           |                  |                  |                |
|       |                 | EmoT SmSA | CASA HoASA     | WReTE AVG | POSP BaPOS TermA | KEPS NERGrit     | NERP FacQA AVG |
scratch 1e-4 2 38.6M 58.51 64.22 65.58 78.31 59.54 65.23 85.69 66.30 69.67 47.71 4.62 31.14 4.08 44.17
scratch 1e-4 4 52.8M 57.31 67.35 67.15 76.28 64.35 66.49 86.78 70.24 70.36 39.40 5.80 30.66 5.00 44.03
scratch 1e-4 6 67.0M 52.84 67.07 69.88 76.83 58.06 64.94 86.16 68.18 70.64 45.65 5.14 27.88 5.21 44.12
fasttext-cc-id-300-no-oov-uncased 1e-4 6 15.1M 67.43 78.84 81.61 85.01 61.13 74.80 94.36 78.45 77.26 57.28 26.70 46.36 17.3 56.82
fasttext-cc-id-300-no-oov-uncased 1e-4 4 10.7M 65.36 76.92 79.02 85.32 67.36 74.79 94.35 79.85 76.12 56.39 37.32 46.46 15.29 57.97
fasttext-cc-id-300-no-oov-uncased 1e-4 2 6.3M 64.74 76.71 75.39 78.05 65.11 72.00 94.42 78.12 73.45 55.22 33.27 45.44 13.89 56.26
fasttext-4B-id-300-no-oov-uncased 1e-4 6 15.1M 68.47 83.07 81.96 86.20 60.33 76.00 95.15 80.61 75.26 44.71 40.83 47.02 18.39 57.42
fasttext-4B-id-300-no-oov-uncased 1e-4 4 10.7M 69.23 82.13 82.20 85.88 60.42 75.97 94.94 81.77 74.43 56.70 38.69 46.79 14.65 58.28
fasttext-4B-id-300-no-oov-uncased 1e-4 2 6.3M 70.97 83.63 78.97 80.16 57.11 74.17 94.93 80.11 71.92 56.67 31.46 45.08 8.65 55.55
indobert-lite-base-128-112.5k 1e-5 12 11.7M 73.88 90.85 89.68 88.07 82.17 84.93 91.40 75.10 89.29 69.02 66.62 46.58 54.99 70.43
indobert-lite-base-128-191.5k 1e-5 12 11.7M 71.95 89.87 84.71 87.57 80.30 82.88 87.27 67.33 89.15 65.84 67.67 49.32 51.76 68.33
indobert-lite-base-512-162.5k 1e-5 12 11.7M 72.27 90.29 87.63 87.62 83.62 84.29 90.05 77.59 89.19 69.13 66.71 50.52 49.18 70.34
indobert-base-128 4e-5 12 124.5M 75.48 87.73 93.23 92.07 78.55 85.41 95.26 87.09 90.73 70.36 69.87 75.52 53.45 77.47
indobert-base-512 1e-5 12 124.5M 76.61 90.90 91.77 90.70 79.73 85.94 95.10 86.25 90.58 69.39 63.67 75.36 53.14 76.21
indobert-base-512 4e-5 12 124.5M 76.28 87.66 93.24 92.70 78.68 85.71 95.23 85.72 91.13 69.17 67.42 75.68 57.06 77.34
indobert-lite-large-128 1e-5 24 17.7M 75.19 88.66 90.99 89.53 78.98 84.67 91.56 83.74 90.23 67.89 71.19 74.37 65.50 77.78
indobert-lite-large-512 1e-5 24 17.7M 71.67 90.13 88.88 88.80 81.19 84.13 91.53 83.51 90.07 67.36 73.27 74.34 69.47 78.51
indobert-lite-large-512 2e-5 24 17.7M 70.80 88.61 88.13 91.05 85.41 84.80 94.53 84.91 90.72 68.55 73.07 74.89 62.87 78.51
indobert-large-128-1100k 4e-5 24 335.2M 77.04 93.71 96.64 93.27 84.17 88.97 95.71 89.74 91.97 70.82 70.76 77.54 67.27 80.55
indobert-large-128-1000k 4e-5 24 335.2M 77.08 92.72 95.69 93.75 82.91 88.43 95.71 90.35 91.87 71.18 77.60 79.25 62.48 81.21
indobert-large-512-1100k 4e-5 24 335.2M 77.39 92.90 95.90 93.77 81.62 88.32 95.25 86.05 91.92 69.71 75.20 77.53 69.86 80.79
indobert-large-512-1100k 3e-5 24 335.2M 79.47 92.03 94.94 93.38 80.30 88.02 95.34 87.36 92.14 71.27 76.63 77.99 68.09 81.26
bert-base-multilingual-uncased 1e-5 12 167.4M 67.30 84.14 72.23 84.63 84.40 78.54 91.85 83.25 89.51 64.31 75.02 69.27 61.29 76.36
xlm-mlm-100-1280 1e-5 16 573.2M 65.75 86.33 82.17 88.89 64.35 77.50 95.87 88.40 90.55 65.35 74.75 75.06 62.15 78.88
xlm-roberta-base 2e-5 12 278.7M 71.15 91.39 91.71 91.57 79.95 85.15 95.16 84.64 90.99 68.82 79.09 75.03 64.58 79.76
xlm-roberta-large 1e-5 24 561.0M 78.51 92.35 92.40 94.27 83.82 88.27 92.73 87.03 91.45 70.88 78.26 78.52 74.61 81.92
Table22: ResultsofallexperimentsconductedinIndoNLUbenchmark. Wesampleeachbatchwithasizeof16
foralldatasetsexceptFacQAandPOSP,forwhichweuseabatchsizeof8.
View publication stats