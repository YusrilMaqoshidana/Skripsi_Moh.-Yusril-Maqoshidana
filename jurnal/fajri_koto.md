IndoLEM and IndoBERT: A Benchmark Dataset and Pre-trained
Language Model for Indonesian NLP
FajriKoto1 AfshinRahimi2 JeyHanLau1 TimothyBaldwin1
1TheUniversityofMelbourne
2TheUniversityofQueensland
ffajri@student.unimelb.edu.au, afshinrahimi@gmail.com
jeyhan.lau@gmail.com, tb@ldwin.net
Abstract
Although the Indonesian language is spoken by almost 200 million people and the 10th most-
spoken language in the world,1 it is under-represented in NLP research. Previous work on In-
donesian has been hampered by a lack of annotated datasets, a sparsity of language resources,
and a lack of resource standardization. In this work, we release the INDOLEM dataset com-
prising seven tasks for the Indonesian language, spanning morpho-syntax, semantics, and dis-
course. We additionally release INDOBERT, a new pre-trained language model for Indonesian,
and evaluate it over INDOLEM, in addition to benchmarking it against existing resources. Our
experimentsshowthat INDOBERT achievesstate-of-the-artperformanceovermostofthetasks
in INDOLEM.
1 Introduction
Despitetherebeingover200Mfirst-languagespeakersoftheIndonesianlanguage,thelanguageisunder-
represented in NLP. We argue that there are three root causes: a lack of annotated datasets, a sparsity
of language resources, and a lack of resource standardization. In English, on the other hand, there are
ever-increasingnumbersofdatasetsfordifferenttasks(Hermannetal.,2015;LuongandManning,2016;
Rajpurkar et al., 2018; Agirre et al., 2016), (pre-)trained models for language modelling and language
understandingtasks(Devlinetal.,2019;Yangetal.,2019;Radfordetal.,2019),andstandardizedtasks
to benchmark research progress (Wang et al., 2019b; Wang et al., 2019a; Williams et al., 2018), all of
whichhavecontributedtorapidprogressinthefieldinrecentyears.
We attempt to redress this situation for Indonesian, as follows. First, we introduce INDOLEM
(“IndonesianLanguageEvaluationMontage”2),acomprehensivedatasetencompassingsevenNLPtasks
and eight sub-datasets, five of which are based on previous work and three are novel to this work. As
part of this, we standardize data splits and evaluation metrics, to enhance reproducibility and robust
benchmarking. These tasks are intended to span a broad range of morpho-syntactic, semantic, and dis-
courseanalysiscompetenciesforIndonesian,tobeabletobenchmarkprogressinIndonesianNLP.First,
formorpho-syntax, weexaminepart-of-speech(POS)tagging(Dinakaramanietal., 2014), dependency
parsing with two Universal Dependency (UD) datasets, and two named entity recognition (NER) tasks
using public data. For semantics, we examine sentiment analysis and single-document summarization.
Fordiscourse,wecreatetwoTwitter-baseddocumentcoherencetasks: Twitterresponseprediction(asa
multiple-choicetask),andTwitterdocumentthreadordering.
Second, we develop and release INDOBERT, a monolingual pre-trained BERT language model for
Indonesian (Devlin et al., 2019). This is one of the first monolingual BERT models for the Indonesian
language,trainedfollowingthebestpracticeinthefield.3
1https://www.visualcapitalist.com/100-most-spoken-languages/
2Yes, guilty as charged, a slightly-forced backronym from lem, which is Indonesian for “glue”, following the English
benchmarknamingtrend(e.g.GLUE(Wangetal.,2019b)andSuperGLUE(Wangetal.,2019a)).
3Turnsoutweweren’tthefirsttothinktotrainamonolingualBERTmodelforIndonesian,ortonameitIndoBERT,with(at
least)twocontemporaneousBERTmodelsforIndonesianthatarenamed“IndoBERT”:AzhariandLintang(2020)andWilie
etal.(2020).
0202
voN
2
]LC.sc[
1v77600.1102:viXra

Ourcontributionsinthispaperare: (1)wereleaseINDOLEM,whichisbyfarthemostcomprehensive
NLP dataset for Indonesian, and intended to provide a benchmark to catalyze further NLP research on
the language; (2) as part of INDOLEM, we develop two novel discourse tasks and datasets; and (3)
we follow best practice in developing and releasing for general use INDOBERT, a BERT model for
Indonesian, which we show to be superior to existing pre-trained models based on INDOLEM. The
INDOLEM dataset, INDOBERT model, and all code associated with this paper can be accessed at:
https://indolem.github.io.
2 RelatedWork
Tocomprehensivelyevaluatenaturallanguageunderstanding(NLU)methodsforEnglish,collectionsof
tools and corpora such as GLUE (Wang et al., 2019b) and SuperGLUE (Wang et al., 2019a) have been
proposed. Generally, such collections aim to benchmark models across various NLP tasks covering a
varietyofcorpussizes, domains, andtaskformulations. GLUEcomprisesninelanguageunderstanding
tasksbuiltonexistingpublicdatasets,whileSuperGLUEisasetofeighttasksthatisnotonlydiversein
task format but also includes low-resource settings. SuperGLUE is a more challenging framework, and
BERTmodelstrailhumanperformanceby20pointsatthetimeofwriting.
In the cross-lingual setting, XGLUE (Liang et al., 2020) was introduced as a benchmark dataset that
coversnearly20languages. UnlikeGLUE,XGLUEincludeslanguagegenerationtaskssuchasquestion
and headline generation. One of the largest cross-lingual corpora is dependency parsing provided by
UniversalDependencies.4 Ithasconsistentannotationof150treebanksacross90languages,constructed
through an open collaboration involving many contributors. Recently, other cross-lingual benchmarks
have been introduced, such as Hu et al. (2020) and Lewis et al. (2020). While these three cross-lingual
benchmarkscontainsomeresources/datasetsforIndonesian,thecoverageislowanddataislimited.
BeyondtheEnglishandcross-lingualsettings,ChineseGLUE5isacomprehensiveNLUcollectionfor
Mandarin Chinese, covering eight different tasks. For the Vietnamese language, Nguyen and Nguyen
(2020) gathered a dataset covering four tasks (NER, POS tagging, dependency parsing, and language
inference),andempiricallyevaluatedthemagainstamonolingualBERT.Elsewhere,thereareindividual
efforts to maintain a systematic catalogue of tasks and datasets, and state-of-the-art methods for each
acrossmultiplelanguages,6 includingonespecificallyforIndonesian.7 However,thereisnocomprehen-
sive dataset for evaluating NLU systems in the Indonesian language, a void which we seek to fill with
INDOLEM.
3 INDOBERT
Transformers (Vaswani et al., 2017) have driven substantial progress in NLP research based on pre-
trained models in the last few years. Although attention-based models are data- and GPU-hungry, the
full attention mechanisms and parallelism offered by the transformer are highly compatible with the
high levels of parallelism that GPU computation offers, and have been shown to be highly effective
at capturing the syntax (Jawahar et al., 2019) and sentence semantics of text (Sun et al., 2019). In
particular, transformer-based language models (Devlin et al., 2019; Radford et al., 2018; Conneau and
Lample, 2019; Raffel et al., 2019) pre-trained on large volumes of text based on simple tasks such as
maskedwordpredictionandsentenceorderingprediction, havequicklybecomeubiquitousinNLPand
drivensubstantialempiricalgainsacrosstasksincludingNER(Devlinetal.,2019),POStagging(Devlin
et al., 2019), single document summarization (Liu and Lapata, 2019), syntactic parsing (Kitaev et al.,
2019), and discourse analysis (Nie et al., 2019). However, this effect has been largely observed for
high-resourcelanguagessuchasEnglish.
INDOBERTisatransformer-basedmodelinthestyleofBERT(Devlinetal.,2019),buttrainedpurely
asamaskedlanguagemodeltrainedusingtheHuggingface8framework,followingthedefaultconfigura-
4https://universaldependencies.org/
5https://github.com/ChineseGLUE/ChineseGLUE
6https://github.com/sebastianruder/NLP-progress
7https://github.com/kmkurn/id-nlp-resource
8https://huggingface.co/

| Data | #train #dev | #test 5-Fold | Evaluation |
| ---- | ----------- | ------------ | ---------- |
Morpho-syntax/SequenceLabellingTasks
| POSTagging*                        | 7,222 802 | 2,006 Yes | Accuracy         |
| ---------------------------------- | --------- | --------- | ---------------- |
| NERUI                              | 1,530 170 | 425 No    | micro-averagedF1 |
| NERUGM                             | 1,687 187 | 469 No    | micro-averagedF1 |
| UD-IndonesianGSD*                  | 4,477 559 | 557 No    | UAS,LAS          |
| UD-IndonesianPUD(CorrectedVersion) | 700 100   | 200 Yes   | UAS,LAS          |
SemanticTasks
| SentimentAnalysis | 3,638 399  | 1,011 Yes | F1    |
| ----------------- | ---------- | --------- | ----- |
| IndoSum*          | 14,262 750 | 3,762 Yes | ROUGE |
CoherencyTasks
| NextTweetPrediction(NTP) | 5,681 811 | 1,890 No  | Accuracy |
| ------------------------ | --------- | --------- | -------- |
| TweetOrdering            | 5,327 760 | 1,521 Yes | RankCorr |
Table1: SummaryofdatasetsincorporatedinINDOBERT.Datasetsmarkedwith‘*’werealreadyavail-
ablewithcanonicalsplits.
tionforBERT-Base(uncased). Ithas12hiddenlayerseachof768d,12attentionheads,andfeed-forward
hidden layers of 3,072d. We modify the Huggingface framework to read a separate text stream for dif-
ferent document blocks,9 and set the training to use 512 tokens per batch. We train INDOBERT with
31,923-sizeIndonesianWordPiecevocabulary.
Intotal,wetrain INDOBERT over220Mwords,aggregatedfromthreemainsources: (1)Indonesian
Wikipedia (74M words); (2) news articles from Kompas,10 Tempo11 (Tala et al., 2003), and Liputan612
(55M words in total); and (3) an Indonesian Web Corpus (Medved and Suchomel, 2017) (90M words).
Afterpreprocessingthecorpusinto512-tokendocumentblocks,weobtain1,067,581traininstancesand
13,985developmentinstances(withoutreduplication). Intraining,weuse4NvidiaV100GPUs(16GB
each) with a batch size of 128, learning rate of 1e-4, the Adam optimizer, and a linear scheduler. We
trainedthemodelfor2.4Msteps(180epochs)foratotalof2calendarmonths,13withthefinalperplexity
overthedevelopmentsetbeing3.97(similartoEnglishBERT-base).
4 INDOLEM:Tasks
In this section, we present an overview of INDOLEM, in terms of the NLP tasks and sub-datasets it
includes. We group the tasks into three categories: morpho-syntax/sequence labelling, semantics, and
discourse coherence. We summarize the sub-datasets include in INDOLEM in Table 1, in addition to
detailingrelatedworkontherespectivetasks.
4.1 Morpho-syntaxandSequenceLabellingTasks
Part-of-speech (POS) tagging. The first Indonesian POS tagging work was done over a 15K-token
dataset. Pisceldoetal.(2009)defines37tagscoveringfivemainPOStags: katakerja(verb), katasifat
(adjective),kataketerangan(adverb),katabenda(noun),andkatatugas(functionwords). Theyutilized
news domain and partial data from the PanLocalisation project (“PANL10N”14). In total, “PANL10N”
comprises 900K tokens, and was generated by machine-translating an English POS-tagged dataset and
noisilyprojectingthePOStagsfromEnglishtotheIndonesiantranslations.
9Theexistingimplementationmergesalldocumentsintoonetextstream
10https://kompas.com
11https://koran.tempo.co
12https://liputan6.com
13Wecheckpointedthemodelat1Mand2Msteps,andfoundthat2Mstepsyieldedalowerperplexityoverthedevset.
14http://www.panl10n.net/

Tocreatealargerandmorereliablecorpus,Dinakaramanietal.(2014)publishedamanually-annotated
corpus of 260K tokens (10K sentences). The text was sourced from the IDENTIC parallel corpus
(Larasati, 2012), which was translated from data in the Penn Treebank corpus. The text is manually
annotated with 23 tags based on Indonesian tag definition of Adriani et al. (2009). For INDOLEM,
we use the Indonesian POS tagging dataset of Dinakaramani et al. (2014), and 5-fold partitioning of
KurniawanandAji(2018).15
Namedentityrecognition(NER).Budietal.(2005)wasthefirststudyonnamedentityrecognition
forIndonesian,whereroughly2,000sentencesfromanewsportalwereannotatedwiththreeNEclasses:
person, location, and organization. In other work, Luthfi et al. (2014) utilized Wikipedia
and DBPedia to automatically generate an NER corpus, and trained a model with Stanford CRF-NER
(Finkel et al., 2005). Rachman et al. (2017) studied LSTM performance over 480 tweets with the same
threenamedentityclasses. Noneoftheseauthorsreleasedthedatasetsusedintheresearch.
There are two publicly-available Indonesian NER datasets. The first, NER UI, comprises 2,125 sen-
tences obtained via an annotation assignment in an NLP course at the University of Indonesia in 2016
(Gultom and Wibowo, 2017). The corpus has the same three named entity classes as its predecessors
(Budietal.,2005). Thesecond,NERUGM,comprises2,343sentencesfromnewsarticles,andwascon-
structed at the University of Gajah Mada (Fachri, 2014) based on five named entity classes: person,
organization,location,time,andquantity.
Dependency parsing. Kamayani and Purwarianti (2011) and Green et al. (2012) pioneered depen-
dency parsing for the Indonesian language. Kamayani and Purwarianti (2011) developed language-
specific dependency labels based on 20 sentences, adapted from Stanford Dependencies (de Marneffe
and Manning, 2016). Green et al. (2012) annotated 100 sentences of IDENTIC without dependency
labels, and used an ensemble SVM model to build a parser. Later, Rahman et al. (2017) conducted a
comparative evaluation over models trained using off-the-shelf tools such as MaltParser (Nivre et al.,
2005) on 2,098 annotated sentences from the news domain. However, this corpus is not publicly avail-
able.
TheUniversalDependencies(UD)project16hasreleasedtwodifferentIndonesiancorporaofrelatively
smallsize: (1)5,593sentencesofUD-Indo-GSD(McDonaldetal.,2013);17 and(2)1,000sentencesof
UD-Indo-PUD (Zeman et al., 2018).18 Alfina et al. (2019) found that these corpora contain annotation
errors and did not deal adequately with Indonesian morphology. They released a corrected version of
UD-Indo-PUDbyfixingannotationsforreduplicated-words,clitics,compoundwords,andnounphrases.
WeincludetwoUD-baseddependencyparsingdatasetsinINDOLEM:(1)UD-Indo-GSD,and(2)the
corrected version of UD-Indo-PUD. As our reference dependency parser model, we use the BiAffine
dependency parser (Dozat and Manning, 2017), which has been shown to achieve strong performance
forEnglish.
4.2 SemanticTasks
Sentiment analysis. There has been sentiment analysis for Indonesian domains/data sources including
presidentialelections(Ibrahimetal.,2015),stockprices(CakraandTrisedya,2015),Twitter(Kotoand
Rahmaningtyas, 2017), and movie reviews (Nurdiansyah et al., 2018). Most previous work, however,
hasusednon-publicandlow-resourcedatasets.
Weincludein INDOLEM anIndonesiansentimentanalysisdatasetbasedonbinaryclassification. In
total,thedatadistributionis3638/399/1011sentencesfortrain/development/test,respectively. Thedata
was sourced from Twitter (Koto and Rahmaningtyas, 2017) and hotel reviews.19 The hotel review data
is annotated at the aspect level, where one review can have multiple polarities for different aspects. We
15WedonotincludePOSdatafromtheUniversalDependencyproject,aswefoundthedatatocontainmanyforeignbor-
rowings(withoutanyattempttotranslatethemintoIndonesian),andsomesentencestobepoortranslations(apointwereturn
tointhecontextoferroranalysisofdependencyparsinginSection7).
16https://universaldependencies.org/
17https://github.com/UniversalDependencies/UD_Indonesian-GSD
18https://github.com/UniversalDependencies/UD_Indonesian-PUD
19https://github.com/annisanurulazhar/absa-playground/

Premise Premise
Ini kak Gracia sama kak Jerome saudaranya apa crushnya, serius Seriously ask, is Gracia Jerome's crush? or are they family?
tanya bang His crush, they know each other when they got Mitsui scholarship
Crush, karena awal mereka kenal karena sama2 dapet beasiswa
mitsui
Possible next tweets: Possible next tweets:
selamat pagi min. Jika ingin bertanya terkait Latsar Cpns Kemdikbud good morning admin. What is the contact for Latsar Cpns Kemdikbud??
lewat kontak mana ya?? Wow, thank you, sorry, I am a new follower.
Waw terimakasii, maaf aku followers baru. the new school academic year is January, on the first day I may get
tahun ajaran barunya januari terus nnt aku masuk masuk ke sekolah di question about "tukang keong".
tanyain malah jadi tukang keong what are you doing beautiful?
lgi ap cantik?
Figure1: Exampleforthenexttweetpredictiontask. TotheleftistheoriginalIndonesianversionand
totherightisanEnglishtranslation. Thetweetindicatedinboldisthecorrectnexttweet.
simplycounttheproportionofpositiveandnegativepolarityaspects,andlabelthesentencebasedonthe
majoritysentiment. Wediscardareviewifthereisatieinpositiveandnegativeaspects.
Summarization. From attention mechanisms (Rush et al., 2015; See et al., 2017) to pre-trained
language models (Liu and Lapata, 2019; Zhang et al., 2019), recent summarization work on English
in terms of both extractive and abstractive methods has relied on ever-larger datasets and data-hungry
methods.
Indonesian (single document) text summarization research has inevitably focused predominantly on
extractivemethods,basedonsmalldatasets. Aristotelesetal.(2012)deployedageneticalgorithmover
a 200-document summarization dataset, and Gunawan et al. (2017) performed unsupervised summa-
rization over 3,075 news articles. As an attempt to create a standardized corpus, Koto (2016) released
a 300-document chat summarization dataset, and Kurniawan and Louvan (2018) released the IndoSum
19K document–summary dataset. At the time we carried out this work,20 IndoSum was the largest In-
donesian summarization corpus in the news domain, manually constructed from CNN Indonesia21 and
Kumparan22 documents. IndoSum is a single-document summarization dataset where each article has
one abstractive summary. Kurniawan and Louvan (2018) released IndoSum together with the ORACLE
— a set of extractive summaries generated automatically by maximizing ROUGE score between sen-
tences of the article and its abstractive summary. We include IndoSum as the summarization dataset in
INDOLEM,andevaluatetheperformanceofextractivesummarizationinthispaper.
4.3 DiscourseCoherenceTasks
WealsointroducetwotasksthatmeasuretheabilityofmodelstomeasurediscoursecoherenceinIndone-
sian, based on message ordering in Twitter threads, namely: (1) next tweet prediction; and (2) message
ordering. Utilizing tweets instead of edited text arguably makes the task harder and allows us to assess
therobustnessofmodels.
First, we use the standard twitter API filtered with the language parameter to harvest 9M Indonesian
tweetsfromtheperiodApril–May2020,coveringthefollowingtopics: health,education,economy,and
government. Wediscardthreadsthatcontainmorethanthreeself-replies,andthreadscontainingsimilar
tweets (usually from Twitter bots). Specifically, we discard a thread if 90% of the tweets are similar,
as based on simple lexical overlap.23 We gather threads that contain 3–5 tweets, and anonymize all
mentions. Thisdataisusedasthebasisforthetwodiscoursecoherencetasks.
Next tweet prediction. To evaluate model coherence, we design a next tweet prediction (NTP) task
that is similar to the next sentence prediction (NSP) task used to train BERT (Devlin et al., 2019). In
NTP, each instance consists of a Twitter thread (2–4 tweets) that we call the premise, and four possible
options for the next tweet (see Figure 1 for an example), one of which is the actual response from the
20Noting that the soon-to-be-released Liputan6 dataset (Koto et al., to appear) will be substantially larger, but was not
availablewhenthisresearchwascarriedout.
21https://www.cnnindonesia.com/
22https://kumparan.com/
23Twotweetsareconsideredtobesimilariftheyhaveavocabularyoverlap≥80%.

original thread. In total, we construct 8,382 instances, where the distractors are obtained by randomly
picking three tweets from the Twitter crawl. We ensure that there is no overlap between the next tweet
candidatesinthetrainingandtestsets.
Tweetordering. Forthesecondtask,weproposearelatedbutmorecomplextaskofthreadmessage
ordering, based on the sentence ordering task of Barzilay and Lapata (2008) to assess text relatedness.
We construct the data by shuffling Twitter threads (containing 3–5 tweets), and assessing the predicted
orderingintermsofrankcorrelationwiththeoriginal. Afterremovingallduplicatesmessages,weobtain
7,608instancesforthistask.
5 EvaluationMethodology
Weprovidedetailsoftheevaluationmethodologyinthissection.
Morpho-syntax/SequenceLabelling. ForPOStagging,weevaluateby5-foldcrossvalidationusing
thepartitionsprovidedbyKurniawanandAji(2018). UnlikeKurniawanandAji(2018)whousemacro-
averaged F1, we use the standard POS tag accuracy for evaluation. For NER, both corpora (NER UI
and NER UGM) are from the news domain. We convert them into IOB2 format, and reserve 10% of
the original training set as a validation set. We evaluate using entity-level F1 over the provided test
set.24 In addition, we conducted our own in-house evaluation of the annotation quality of both datasets
by randomly picking 100 sentences and counting the number of annotation errors. We found that NER
UI has better quality than NER UGM with 1% vs. 30% errors, respectively. Annotation errors in NER
UGMarelargelyduetolowrecall,i.e.annotatingnamedentitieswiththetagO.
Fordependencyparsingwedonotapply5-foldcross-validationforUD-Indo-GSD,asitwasreleased
with a pre-defined test set, which allows us to directly benchmark against previous work. UD-Indo-
PUD, on the other hand, only includes 1,000 sentences with no fixed test set, so we evaluate via 5-fold
cross-validation with fixed splits.25 Note that the text in UD-Indo-PUD was manually translated from
documents in other languages, while UD-Indo-GSD was sourced from texts authored in Indonesian.
Additionally, the translation quality of UD-Indo-PUD is low in parts, which impacts on evaluation, as
wereturntodiscussinSection7. Weevaluatebothdependencyparsingdatasetsbasedontheunlabelled
attachmentscore(UAS)andlabelledattachmentscore(LAS).
Semantics. Because the sentiment analysis data is low-resource and imbalanced, we use stratified
5-fold cross-validation, and evaluate based on F1 score. For summarization, on the other hand, we use
thecanonicalsplitsprovidedbyKurniawanandLouvan(2018),andevaluatetheresultingsummarywith
ROUGE(F1)(Lin,2004)intheformofthreedifferentmetrics: R1,R2,andRL.
DiscourseCoherence. Wedonotperform5-foldcross-validationoverNTPfortworeasons. First,we
needtoensurethedistractorsinthetestsetdonotoverlapwiththetrainingordevelopmentsets,toavoid
possiblebiasbecauseofdatasetartefacts. Second,thesizeofthedatasetintermsofpair-wiselabellingis
actuallyfourtimesthereportedsize(Table1)astherearethreedistractorsforeachthread. Weevaluate
theNTPtaskbasedonaccuracy,meaningtherandombaselineis25%.
For tweet ordering, we evaluate using Spearman’s rank correlation (ρ). Specifically, we average the
rankcorrelationbetweenthegoldandpredictedorderofeachthreadinthedataset.
6 ComparativeEvaluation
6.1 Baselines
MostofourexperimentsuseaBiLSTMwith300dfastTextpre-trainedIndonesianembeddings(Bo-
janowskietal.,2016)asabaseline. DetailsofthebaselinesareprovidedinTable2.
For extractive summarization baselines, we use the models of Kurniawan and Louvan (2018) and
Cheng and Lapata (2016) as baselines. Kurniawan and Louvan (2018) propose a sentence tagging ap-
proach based on a hidden Markov model, while Cheng and Lapata (2016) use a hierarchical LSTM
24WeusedtheseqevallibrarytoevaluatethePOSandNERtasks.
25The split for cross validation is 70/10/20 for train/development/test, respectively. We first create 5 folds with non-
overlappingtestpartitions, andforeachfoldwesetthefirstportionoftheremainingdataasthedevelopment(andtherest
astrainingdata).

Task Baselines BERTmodels
Lampleetal.(2016)26
AhierarchicalBiLSTM+CRFwithinput: Fine-tuning:
character-levelembedding(updated), addingaclassificationlayerforeachtoken,
POSTaggingandNER
andword-levelfastTextembedding(fixed), lr:5e-5,epoch:100withearlystopping
lr:0.001,epoch:100withearlystopping (patience=5)
(patience=5)
1.DozatandManning(2017),Bi-Affine
parser,Embedding:fastText(fixed)
DozatandManning(2017),Bi-Affine
Dependencyparsing 2.RahmanandPurwarianti(2020)†
parser,Embedding:BERToutput(fixed)
3.KondratyukandStraka(2019)†
4.Alfinaetal.(2019)†
1.200-dBiLSTM
Fine-tuning:
Embedding:fastText(fixed),
Input:200tokens;epoch:20;lr:5e-5;
lr:0.001,epoch:100withearlystopping
SentimentAnalysis batchsize:30;warm-up:10%ofthetotalsteps;
(patience=5)
earlystopping(patience=5);
2.NaiveBayesandLogisticRegression
Outputlayerusestheencoded[CLS]
input:Byte-pairencoding(unigram+bigram)27
1.KurniawanandLouvan(2018)† LiuandLapata(2019),extractivemodel,
Summarization
2.ChengandLapata(2016)† 20,000steps,lr:2e-3,andtokens:512.28
Fine-tuning:
Input:60tokens(for1singletweet);
200-dBiLSTM(binary-class.)
epoch:20;learningrate;5e-5;batchsize:20;
NTP Embedding:fastText(fixed),lr:0.001,
warm-up:10%ofthetotalsteps;earlystopping
epoch:100withearlystopping(patience=20)
(patience=5);Outputlayerusesthe
encoded[CLS]
Fine-tuning:
Input:50tokens(for1singletweet);
Hierarchical200-dBiLSTMs(multi-class.)
epoch:20;learningrate;5e-5;batchsize:20;
TweetOrdering Embedding:fastText(fixed),lr:0.001,
warm-up:10%ofthetotalsteps;earlystopping
epoch:100withearlystopping(patience=20)
(patience=5);BERTfine-tuningisbasedonthe
LiuandLapata(2019)trick(alternatedseq.)
Table 2: Comparison of baselines and BERT-based models for all INDOLEM tasks. All listed models
wereimplementedandrunbytheauthors,exceptforthosemarkedwith“†”wheretheresultsaresourced
fromtheoriginalpaper.
encoder with attention. In addition, we present ORACLE results, obtained by greedily maximizing the
ROUGE score between the reference summary and different combinations of sentences from the docu-
ment. ORACLEdenotestheupperboundfortheextractivesummarization.
For next tweet prediction, we concatenate all premise tweets into a single document, and use a BiL-
STMandfastTextwordembeddingstoobtainthebaselinedocumentencoding. Westructurethistask
asabinaryclassificationwherewematchthepremisewitheachcandidatenexttweet. Wepickthetweet
with the highest probability as the prediction. We use the same BiLSTM to encode the next tweet, and
feedtheconcatenatedrepresentationsfromthelasthiddenstatesintotheoutputlayer.
For tweet ordering, we use a hierarchical BiLSTM model. The first BiLSTM is used to encode a
singletweetbyaveragingallhiddenstates. WeusethesecondBiLSTMtolearntheinter-tweetordering.
We design the tweet ordering task as a sequence labelling task, where we aim to obtain P(r|t), the
probability distribution across rank positions r for a given tweet t. Note that in this experiment, each
instanceiscomprisedof3–5tweets,andwemodelthetaskviamulti-classification(with5classes/ranks).
We perform inference based on P(r|t), where we decide the final rank based on the highest sum of
probabilitiesfromtheexhaustiveenumerationofdocumentranks.

6.2 BERTBenchmarks
To benchmark INDOBERT, we compare against two pre-existing BERT models: multilingual BERT
(“MBERT”), and a monolingual BERT for Malay (“MALAYBERT”).29 MBERT is trained by concate-
natingWikipediadocumentsfor104languagesincludingIndonesian,andhasbeenshowntobeeffective
for zero-shot multilingual tasks (Wu and Dredze, 2019; Wang et al., 2019c). MALAYBERT is a a pub-
licly available model that was trained on Malay documents from Wikipedia, local news sources, social
media, and some translations from English. We expect MALAYBERT to provide better representations
thanMBERTfortheIndonesianlanguage,becauseMalayandIndonesianaremutuallyintelligible,with
manylexicalsimilarities,butnoticeabledifferencesingrammar,pronunciationandvocabulary.
Forthesequencelabellingtasks(POStaggingandNER),sentimentanalysis,NTP,andtweetordering
task,thefine-tuningprocedureisdetailedinTable2.
For dependency parsing, we follow Nguyen and Nguyen (2020) in incorporating BERT into the Bi-
Affine dependency parser (Dozat and Manning, 2017) by replacing the word embeddings with the cor-
responding contextualized representations. Specifically, we generate the BERT embedding of the first
WordPiece token as the word embedding, and train the BiAffine parser in its default configuration. In
addition, we also benchmark against a pre-existing fine-tuned version of MBERT trained over 75 con-
catenatedUDdatasetsindifferentlanguages(KondratyukandStraka,2019).
Forsummarization,wefollowLiuandLapata(2019)inencodingthedocumentbyinsertingthetokens
[CLS] and [SEP] between sentences. We also apply alternating segment embeddings based on whether
thepositionofasentenceisoddoreven. Ontopofthepre-trainedmodel, weuseasecondtransformer
encoder to learn inter-sentential relationships. The input is the encoded [CLS] representation, and the
outputistheextractivelabely ∈ {0,1}(1=includeinsummary;0=don’tinclude).
7 Results
Table3showstheresultsforPOStaggingandNER.MBERT,MALAYBERT,andINDOBERTperform
verysimilarlyoverthePOStaggingtask,wellabovetheBiLSTMbaseline. Thisindicatesthatallthree
contextual embedding models are able to generalize well over low-level morpho-syntactic tasks. Given
that Indonesian and Malay share a large number of words, it is not surprising that MALAYBERT per-
formsonparwithINDOBERTforPOStagging. OntheNERtasks,bothMALAYBERTandINDOBERT
outperformMBERT,whichperformssimilarlytoorslightlyabovetheBiLSTM.ThisisdespiteMBERT
having been trained on a much larger corpus, and having seen many more entities during training. IN-
DOBERT slightlyoutperforms MALAYBERT.
In Table 4, we show that augmenting the BiAffine parser with the pre-trained models yields a strong
resultfordependencyparsing,wellabovepreviously-publishedresultsovertherespectivedatasets. Over
UD-Indo-GSD, INDOBERT outperforms all methods on both metrics. The universal fine-tuning ap-
proach(KondratyukandStraka,2019)yieldssimilarperformanceasBiAffine+fastText,whileaug-
mentingBiAffinewithMBERTandMALAYBERTyieldslowerUASandLASscoresthanINDOBERT.
OverUD-Indo-PUD,weseethataugmentingBiAffinewithMBERToutperformsallmethodsincluding
INDOBERT. Note that Kondratyuk and Straka (2019) is trained on the original version of UD-Indo-
PUD, and Alfina et al. (2019) is based on 10-fold cross-validation, meaning the results are not 100%
comparable.
To better understand why MBERT performs so well over UD-Indo-PUD, we randomly selected 100
instances for manual analysis. We found that 44 out of the 100 sentences contained direct borrowings
of foreign words (29 names, 10 locations, and 15 organisations), some of which we would expect to be
localizedintoIndonesian,suchas: St.Rastislav,StarReach,RoyalNationalParkAustralia,andZettel’s
Traum. Wealsothoroughlyexaminedthetranslationqualityandfoundthatroughly20%ofthesentences
26Thebaseline codeis availableas chars-lstm-lstm-crfathttps://github.com/guillaumegenthial/
tf_ner.
27Wealsoexperimentedwithsimpletermfrequency,butobservedlowerperformancesoomittheresultsfromthepaper.
28Wecheckpointevery2,500steps,andperforminferenceoverthetestsetbasedonthetop-3bestcheckpointsaccordingto
thedevelopmentset
29https://huggingface.co/huseinzol05/bert-base-bahasa-cased

|     |     |     |     | POStagging | NERUGM | NERUI |     |
| --- | --- | --- | --- | ---------- | ------ | ----- | --- |
Method
|     |                              |     |     | Acc  | F1   | F1   |     |
| --- | ---------------------------- | --- | --- | ---- | ---- | ---- | --- |
|     | BiLSTM-CRF(Lampleetal.,2016) |     |     | 95.4 | 70.9 | 82.2 |     |
|     | MBERT                        |     |     | 96.8 | 71.6 | 82.2 |     |
|     | MALAYBERT                    |     |     | 96.8 | 73.2 | 87.4 |     |
|     | INDOBERT                     |     |     | 96.8 | 74.9 | 90.1 |     |
Table 3: Results onPOS and NER tasksusing accuracy averagedoverfive folds forPOS tagging task,
andentity-levelF1overthetestsetfortheNERtasks.
|        |     | UD-Indo-GSD |     |        |     | UD-Indo-PUD |     |
| ------ | --- | ----------- | --- | ------ | --- | ----------- | --- |
| Method |     |             |     | Method |     |             |     |
|        |     | UAS         | LAS |        |     | UAS         | LAS |
RahmanandPurwarianti(2020)* 82.56 76.04 Alfinaetal.(2019)* 83.33 79.39
KondratyukandStraka(2019) 86.45 80.10 KondratyukandStraka(2019)* 77.47 56.90
| BiAffinew/fastText |     |       |       | BiAffinew/fastText |     |       |       |
| ------------------ | --- | ----- | ----- | ------------------ | --- | ----- | ----- |
|                    |     | 85.25 | 80.35 |                    |     | 84.04 | 79.01 |
| BiAffinew/MBERT    |     | 86.85 | 81.78 | BiAffinew/MBERT    |     | 90.58 | 85.44 |
BiAffinew/MALAYBERT 86.99 81.87 BiAffinew/MALAYBERT 88.91 83.56
BiAffinew/INDOBERT 87.12 82.32 BiAffinew/INDOBERT 89.23 83.95
Table4: Resultsfordependencyparsing. Methodsmarkedwith‘*’(frompreviouswork)donotusethe
sametestpartition.
|            |     | Sentiment    |        |     |     | Summarization(F1) |       |
| ---------- | --- | ------------ | ------ | --- | --- | ----------------- | ----- |
| Method     |     |              | Method |     |     |                   |       |
|            |     | Analysis(F1) |        |     |     | R1 R2             | RL    |
| NaiveBayes |     | 70.95        | ORACLE |     |     | 79.27 72.52       | 78.82 |
LogisticRegression 72.14 KurniawanandLouvan(2018) 17.62 4.70 15.89
BiLSTMw/fastText
|           |     | 71.62                                | ChengandLapata(2016) |     |     | 67.96 61.65 | 67.24 |
| --------- | --- | ------------------------------------ | -------------------- | --- | --- | ----------- | ----- |
| MBERT     |     | 76.58                                | MBERT                |     |     | 68.40 61.66 | 67.67 |
| MALAYBERT |     | 82.02                                | MALAYBERT            |     |     | 68.44 61.38 | 67.71 |
| INDOBERT  |     | 84.13                                | INDOBERT             |     |     | 69.93 62.86 | 69.21 |
|           |     | Table5: Resultsoverthesemantictasks. |                      |     |     |             |       |
arelow-qualitytranslations. Forinstance,Ketidaksesuaiandataekonomidanretorikapolitiktidakasing,
atauseharusnyatidakasingisnotanaturalsentenceinIndonesian.
For the semantic tasks, INDOBERT outperforms all other methods for both sentiment analysis and
extractive summarization (Table 5). For sentiment analysis, the improvement over the baselines is im-
pressive: +13.2 points over naive Bayes, and +7.5 points over MBERT. As expected, MALAYBERT
alsoperformswellforsentimentanalysis,butsubstantiallylowerthan INDOBERT.Forsummarization,
MBERTandMALAYBERTachievesimilarperformance,andonlyoutperformChengandLapata(2016)
byaround0.5ROUGEpoints. INDOBERT,ontheotherhand,is1–2ROUGEpointsbetter.
Lastly,inTable6,weobservethatINDOBERTisonceagainsubstantiallybetterthantheothermodels
at discourse coherence modelling, despite its training not including next sentence prediction (as per the
EnglishBERT).ToassessthedifficultyoftheNTPtask,werandomlyselected100testinstances,andthe
firstauthor(anativespeakerofIndonesian)manuallypredictedthenexttweet. Thehumanperformance
was90%,lowerthanthepre-trainedlanguagemodels. Forthetweetorderingtask,wealsoassesshuman
performancebyrandomlyselecting100testinstances,andfoundtherankcorrelationscoreofρ = 0.61
to be slightly higher than INDOBERT. The gap between INDOBERT and the other BERT models was
biggeronthistask.
Overall, with the possible exception of POS tagging and NTP, there is substantial room for improve-

NextTweet TweetOrdering
Method
Prediction(Acc) (ρ)
Random 25.0 0.00
Human(100samples) 90.0 0.61
BiLSTMw/fastText 73.6 0.45
MBERT 92.4 0.53
MALAYBERT 93.1 0.51
INDOBERT 93.7 0.59
Table6: Resultsfordiscoursecoherence. “Human”istheoracleperformancebyahumanannotator.
mentacrossalltasks,andourhopeisthatINDOLEMcanserveasabenchmarkdatasettotrackprogress
inIndonesianNLP.
8 Conclusion
In this paper, we introduced INDOLEM, a comprehensive dataset encompassing seven tasks, spanning
morpho-syntax, semantics, and discourse coherence. We also detailed INDOBERT, a new BERT-style
monolingualpre-trainedlanguagemodelforIndonesian. WeusedINDOLEMtobenchmarkINDOBERT
(includingcomparativeevaluationagainstabroadrangeofbaselinesandcompetitorBERTmodels),and
showedittoachievestate-of-the-artperformanceoverthedataset.
Acknowledgements
Wearegratefultotheanonymousreviewersfortheirhelpfulfeedbackandsuggestions. Thefirstauthor
is supported by the Australia Awards Scholarship (AAS), funded by the Department of Foreign Af-
fairsandTrade(DFAT),Australia. ThisresearchwasundertakenusingtheLIEFHPC-GPGPUFacility
hostedat TheUniversityof Melbourne. Thisfacility wasestablishedwith theassistanceof LIEFGrant
LE170100200.
References
Mirna Adriani, Ruli Manurung, and Femphy Pisceldo. 2009. Statistical based part of speech tagger for Bahasa
Indonesia. InProceedingsofthe3rdInternationalMALINDOWorkshop.
Eneko Agirre, Carmen Banea, Daniel M. Cer, Mona T. Diab, Aitor Gonzalez-Agirre, Rada Mihalcea, German
Rigau, and Janyce Wiebe. 2016. Semeval-2016 task 1: Semantic textual similarity, monolingual and cross-
lingualevaluation. InProceedingsofthe10thInternationalWorkshoponSemanticEvaluation(SemEval-2016),
pages497–511.
IkaAlfina, ArawindaDinakaramani, MohamadIvanFanany, andHeruSuhartanto. 2019. Goldstandarddepen-
dencytreebankforIndonesia. InProceedingofthe33rdPacificAsiaConferenceonLanguage,Informationand
Computation(PACLIC33),Hakodate,Japan.
Aristoteles Aristoteles, Yeni Herdiyeni, Ahmad Ridha, and Julio Adisantoso. 2012. Text feature weighting for
summarization of document Bahasa Indonesia using genetic algorithm. IJCSI International Journal of Com-
puterScienceIssues,9(1):1–6.
SariweningAzhariandSarahLintang. 2020. Indobert: Transformer-basedmodelforIndonesianlanguageunder-
standing. Undergraduatethesis,UniversitasGadjahMada.
ReginaBarzilayandMirellaLapata. 2008. Modelinglocalcoherence: Anentity-basedapproach. Computational
Linguistics,34(1):1–34.
Piotr Bojanowski, Edouard Grave, Armand Joulin, and Tomas Mikolov. 2016. Enriching word vectors with
subwordinformation. arXivpreprintarXiv:1607.04606.

IndraBudi,Ste´phaneBressan,GatotWahyudi,ZainalA.Hasibuan,andBobbyA.A.Nazief. 2005. Namedentity
recognitionfortheIndonesianlanguage: combiningcontextual,morphologicalandpart-of-speechfeaturesinto
aknowledgeengineeringapproach. DiscoveryScience,pages57–69.
Yahya Eru Cakra and Bayu Distiawan Trisedya. 2015. Stock price prediction using linear regression based on
sentimentanalysis. In2015InternationalConferenceonAdvancedComputerScienceandInformationSystems
(ICACSIS),pages147–154.
JianpengChengandMirellaLapata. 2016. Neuralsummarizationbyextractingsentencesandwords. InProceed-
ings of the 54th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers),
volume1,pages484–494.
Alexis Conneau and Guillaume Lample. 2019. Cross-lingual language model pretraining. In NeurIPS 2019:
Thirty-thirdConferenceonNeuralInformationProcessingSystems,pages7057–7067.
Marie-CatherinedeMarneffeandChristopherD.Manning. 2016. Stanfordtypeddependenciesmanual. Technical
report,StanfordUniversity.
Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova. 2019. BERT: Pre-training of deep bidi-
rectional transformers for language understanding. In NAACL-HLT 2019: Annual Conference of the North
AmericanChapteroftheAssociationforComputationalLinguistics,pages4171–4186.
ArawindaDinakaramani,FamRashel,AndryLuthfi,andRuliManurung. 2014. DesigninganIndonesianpartof
speech tagset and manually tagged Indonesian corpus. In 2014 International Conference on Asian Language
Processing(IALP),pages66–69.
Timothy Dozat and Christopher D. Manning. 2017. Deep biaffine attention for neural dependency parsing. In
Proceedingsofthe2016InternationalConferenceonLearningRepresentations,pages1–8.
MuhammadFachri. 2014. NamedentityrecognitionforIndonesiantextusinghiddenMarkovmodel. Undergrad-
uateThesis.
JennyRoseFinkel,TrondGrenager,andChristopherManning. 2005. Incorporatingnon-localinformationintoin-
formationextractionsystemsbyGibbssampling. InProceedingsofthe43rdAnnualMeetingoftheAssociation
forComputationalLinguistics(ACL’05),pages363–370.
NathanGreen,SeptinaDianLarasati,andZdenekZabokrtsky. 2012. Indonesiandependencytreebank: Annota-
tionandparsing. InProceedingsofthe26thPacificAsiaConferenceonLanguage,Information,andComputa-
tion,pages137–145.
YohanesGultomandWahyuCaturWibowo. 2017. AutomaticopendomaininformationextractionfromIndone-
siantext. In2017InternationalWorkshoponBigDataandInformationSecurity(IWBIS),pages23–30.
D Gunawan, A Pasaribu, R F Rahmat, and R Budiarto. 2017. Automatic text summarization for Indonesian
languageusingTextTeaser. IOPConferenceSeries: MaterialsScienceandEngineering,190(1):12048.
Karl Moritz Hermann, Toma´sˇ Kocˇisky´, Edward Grefenstette, Lasse Espeholt, WillKay, Mustafa Suleyman, and
Phil Blunsom. 2015. Teaching machines to read and comprehend. In NIPS’15: Proceedings of the 28th
InternationalConferenceonNeuralInformationProcessingSystems-Volume1,pages1693–1701.
JunjieHu,SebastianRuder,AdityaSiddhant,GrahamNeubig,OrhanFirat,andMelvinJohnson. 2020. Xtreme:
A massively multilingual multi-task benchmark for evaluating cross-lingual generalization. arXiv preprint
arXiv:2003.11080.
MochamadIbrahim,OmarAbdillah,AlfanF.Wicaksono,andMirnaAdriani. 2015. Buzzerdetectionandsenti-
mentanalysisforpredictingpresidentialelectionresultsinatwitternation. In2015IEEEInternationalConfer-
enceonDataMiningWorkshop(ICDMW),pages1348–1353.
GaneshJawahar,BenoˆıtSagot,andDjame´Seddah. 2019. WhatdoesBERTlearnaboutthestructureoflanguage.
InACL2019: The57thAnnualMeetingoftheAssociationforComputationalLinguistics,pages3651–3657.
Mia Kamayani and Ayu Purwarianti. 2011. Dependency parsing for Indonesian. In Proceedings of the 2011
InternationalConferenceonElectricalEngineeringandInformatics,pages1–5.
Nikita Kitaev, Steven Cao, and Dan Klein. 2019. Multilingual constituency parsing with self-attention and pre-
training. In Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics, pages
3499–3505,Florence,Italy,July.

DanKondratyukandMilanStraka. 2019. 75languages,1model: Parsinguniversaldependenciesuniversally. In
Proceedingsofthe2019ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages2779–2795.
FajriKotoandGemalaY.Rahmaningtyas. 2017. Insetlexicon: Evaluationofawordlistforindonesiansentiment
analysisinmicroblogs. In2017InternationalConferenceonAsianLanguageProcessing(IALP),pages391–
394.
Fajri Koto, Jey Han Lau, and Timothy Baldwin. to appear. Liputan6: A large-scale Indonesian dataset for text
summarization. InProceedingsofthe1stConferenceoftheAsia-PacificChapteroftheAssociationforCom-
putational Linguistics and the 10th International Joint Conference on Natural Language Processing (AACL-
IJCNLP2020).
FajriKoto. 2016. ApubliclyavailableIndonesiancorporaforautomaticabstractiveandextractivechatsumma-
rization. InProceedingsofLREC2016.
KemalKurniawanandAlhamFikriAji. 2018. TowardastandardizedandmoreaccurateIndonesianpart-of-speech
tagging. In2018InternationalConferenceonAsianLanguageProcessing(IALP),pages303–307.
Kemal Kurniawan and Samuel Louvan. 2018. Indosum: A new benchmark dataset for Indonesian text summa-
rization. In2018InternationalConferenceonAsianLanguageProcessing(IALP),pages215–220.
GuillaumeLample,MiguelBallesteros,SandeepSubramanian,KazuyaKawakami,andChrisDyer. 2016. Neural
architectures for named entity recognition. In Proceedings of the 2016 Conference of the North American
Chapter of the Association for Computational Linguistics: Human Language Technologies, pages 260–270,
SanDiego,California,June.
SeptinaDianLarasati. 2012. IDENTICcorpus: MorphologicallyenrichedIndonesian-Englishparallelcorpus. In
LREC,pages902–906.
PatrickLewis,BarlasOguz,RutyRinott,SebastianRiedel,andHolgerSchwenk. 2020. MLQA:Evaluatingcross-
lingualextractivequestionanswering. InACL2020:58thAnnualMeetingoftheAssociationforComputational
Linguistics,pages7315–7330.
Yaobo Liang, Nan Duan, Yeyun Gong, Ning Wu, Fenfei Guo, Weizhen Qi, Ming Gong, Linjun Shou, Daxin
Jiang, Guihong Cao, Xiaodong Fan, Bruce Zhang, Rahul Agrawal, Edward Cui, Sining Wei, Taroon Bharti,
YingQiao,Jiun-HungChen,WinnieWu,ShuguangLiu,FanYang,RanganMajumder,andMingZhou. 2020.
XGLUE:Anewbenchmarkdatasetforcross-lingualpre-training,understandingandgeneration. arXivpreprint
arXiv:2004.01401.
Chin-Yew Lin. 2004. ROUGE: A package for automatic evaluation of summaries. In Text Summarization
BranchesOut: ProceedingsoftheACL-04Workshop,pages74–81.
Yang Liu and Mirella Lapata. 2019. Text summarization with pretrained encoders. In Proceedings of the 2019
ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages3728–3738.
Minh-ThangLuongandChristopherD.Manning. 2016. Achievingopenvocabularyneuralmachinetranslation
with hybrid word-character models. In Proceedings of 54th Annual Meeting of the Association for Computa-
tionalLinguistics(ACL2016),Berlin,Germany.
AndryLuthfi,BayuDistiawan,andRuliManurung. 2014. BuildinganIndonesiannamedentityrecognizerusing
WikipediaandDBPedia. In2014InternationalConferenceonAsianLanguageProcessing(IALP),pages19–
22.
RyanMcDonald,JoakimNivre,YvonneQuirmbach-Brundage,YoavGoldberg,DipanjanDas,KuzmanGanchev,
KeithHall,SlavPetrov,HaoZhang,OscarTa¨ckstro¨m,ClaudiaBedini,Nu´riaBertomeuCastello´,andJungmee
Lee. 2013. Universal dependency annotation for multilingual parsing. In Proceedings of the 51st Annual
MeetingoftheAssociationforComputationalLinguistics(Volume2: ShortPapers),volume2,pages92–97.
MarekMedvedandV´ıtSuchomel. 2017. Indonesianwebcorpus(idWac). InLINDAT/CLARINdigitallibraryat
theInstituteofFormalandAppliedLinguistics(U´FAL),FacultyofMathematicsandPhysics,CharlesUniver-
sity.
DatQuocNguyenandAnhTuanNguyen. 2020. PhoBERT:Pre-trainedlanguagemodelsforVietnamese. arXiv
preprintarXiv:2003.00744.
AllenNie,ErinBennett,andNoahGoodman. 2019. DisSent:Learningsentencerepresentationsfromexplicitdis-
courserelations. InProceedingsofthe57thAnnualMeetingoftheAssociationforComputationalLinguistics,
pages4497–4510,Florence,Italy,July.

JoakimNivre,JohanHall,JensNilsson,AtanasChanev,Gu¨lsenEryigit,SandraKu¨bler,SvetoslavMarinov,and
ErwinMarsi. 2005. MaltParser: Alanguage-independentsystemfordata-drivendependencyparsing. Natural
LanguageEngineering,13(2):95–135.
YanuarNurdiansyah,SaifulBukhori,andRahmadHidayat. 2018. Sentimentanalysissystemformoviereviewin
BahasaIndonesiausingna¨ıvebayesclassifiermethod. JournalofPhysics: ConferenceSeries,1008:12011.
Femphy Pisceldo, Ruli Manurung, and Mirna Adriani. 2009. Probabilistic part of speech tagging for Bahasa
Indonesia. InThirdInternationalMALINDOWorkshop,pages1–6.
ValdiRachman,SeptivianaSavitri,FithriannisaAugustianti,andRahmadMahendra. 2017. Namedentityrecog-
nitiononIndonesiantwitterpostsusinglongshort-termmemorynetworks. In2017InternationalConference
onAdvancedComputerScienceandInformationSystems(ICACSIS).
AlecRadford,KarthikNarasimhan,TimSalimans,andIlyaSutskever. 2018. Buildingadiscourse-taggedcorpus
intheframeworkofrhetoricalstructuretheory. InCoRR,abs/1704.01444,2017.
AlecRadford,JeffreyWu,RewonChild,DavidLuan,DarioAmodei,andIlyaSutskever. 2019. Languagemodels
areunsupervisedmultitasklearners. OpenAIBlog,1(8):9.
ColinRaffel,NoamShazeer,AdamRoberts,KatherineLee,SharanNarang,MichaelMatena,YanqiZhou,WeiLi,
andPeterJ.Liu. 2019. Exploringthelimitsoftransferlearningwithaunifiedtext-to-texttransformer. arXiv
preprintarXiv:1910.10683.
Arief Rahman and Ayu Purwarianti. 2020. Dense word representation utilization in Indonesian dependency
parsing. JurnalLinguistikKomputasional,3(1):12–19.
Arief Rahman, Kuncoro Adhiguna, and Ayu Purwarianti. 2017. Ensemble technique utilization for Indonesian
dependencyparser. PACLIC,pages64–71.
PranavRajpurkar, RobinJia, andPercyLiang. 2018. Knowwhatyoudon’tknow: Unanswerablequestionsfor
SQuAD. arXivpreprintarXiv:1806.03822.
Alexander M. Rush, Sumit Chopra, and Jason Weston. 2015. A neural attention model for abstractive sentence
summarization. InProceedingsofthe2015ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,
pages379–389.
Abigail See, Peter J. Liu, and Christopher D. Manning. 2017. Get to the point: Summarization with pointer-
generatornetworks. InProceedingsofthe55thAnnualMeetingoftheAssociationforComputationalLinguis-
tics(Volume1: LongPapers),volume1,pages1073–1083.
ChiSun,LuyaoHuang,andXipengQiu. 2019. UtilizingBERTforaspect-basedsentimentanalysisviaconstruct-
ingauxiliarysentence. InNAACL-HLT(1),pages380–385.
F.Tala,J.Kamps,K.E.Mu¨ller,andM.deRijke. 2003. TheimpactofstemmingoninformationretrievalinBahasa
Indonesia. InProceedingsofThe14thMeetingofComputationalLinguisticsintheNetherlands.
Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Lukasz Kaiser,
andIlliaPolosukhin. 2017. Attentionisallyouneed. InProceedingsofthe31stInternationalConferenceon
NeuralInformationProcessingSystems,pages5998–6008.
Alex Wang, Yada Pruksachatkun, Nikita Nangia, Amanpreet Singh, Julian Michael, Felix Hill, Omer Levy, and
SamuelR.Bowman. 2019a. SuperGLUE:Astickierbenchmarkforgeneral-purposelanguageunderstanding
systems. InAdvancesinNeuralInformationProcessingSystems,pages3266–3280.
AlexWang, AmanpreetSingh, JulianMichael,FelixHill,OmerLevy, andSamuelR.Bowman. 2019b. GLUE:
Amulti-taskbenchmarkandanalysisplatformfornaturallanguageunderstanding. InICLR2019: 7thInterna-
tionalConferenceonLearningRepresentations.
Yuxuan Wang, Wanxiang Che, Jiang Guo, Yijia Liu, and Ting Liu. 2019c. Cross-lingual BERT transformation
for zero-shot dependency parsing. In Proceedings of the 2019 Conference on Empirical Methods in Natural
LanguageProcessing,pages5720–5726.
Bryan Wilie, Karissa Vincentio, Genta Indra Winata, Samuel Cahyawijaya, Xiaohong Li, Zhi Yuan Lim, Sidik
Soleman,RahmadMahendra,PascaleFung,SyafriBahar,andAyuPurwarianti. 2020. IndoNLU:Benchmark
andresourcesforevaluatingIndonesiannaturallanguageunderstanding. arXivpreprintarXiv:2009.05387.

AdinaWilliams,NikitaNangia,andSamuelBowman. 2018. Abroad-coveragechallengecorpusforsentenceun-
derstandingthroughinference. InNAACLHLT2018: 16thAnnualConferenceoftheNorthAmericanChapter
oftheAssociationforComputationalLinguistics:HumanLanguageTechnologies,volume1,pages1112–1122.
ShijieWuandMarkDredze. 2019. Beto, Bentz, Becas: Thesurprisingcross-lingualeffectivenessofBERT. In
Proceedingsofthe2019ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages833–844.
ZhilinYang,ZihangDai,YimingYang,JaimeCarbonell,RuslanSalakhutdinov,andQuocVLe. 2019. XLNet:
Generalizedautoregressivepretrainingforlanguageunderstanding. InNeurIPS2019: Thirty-thirdConference
onNeuralInformationProcessingSystems,pages5754–5764.
DanielZeman,JanHajicˇ,MartinPopel,MartinPotthast,MilanStraka,FilipGinter,JoakimNivre,andSlavPetrov.
2018. CoNLL2018sharedtask: Multilingualparsingfromrawtexttouniversaldependencies. InConference
onComputationalNaturalLanguageLearning(CoNLL),pages1–21.
Jingqing Zhang, Yao Zhao, Mohammad Saleh, and Peter J Liu. 2019. PEGASUS: Pre-training with extracted
gap-sentencesforabstractivesummarization. arXivpreprintarXiv:1912.08777.