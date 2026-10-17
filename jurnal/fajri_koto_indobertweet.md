INDOBERTWEET: A Pretrained Language Model for Indonesian Twitter
|     | with | Effective |     | Domain-Specific | Vocabulary |                |     | Initialization |     |     |     |
| --- | ---- | --------- | --- | --------------- | ---------- | -------------- | --- | -------------- | --- | --- | --- |
|     |      | FajriKoto |     | JeyHanLau       |            | TimothyBaldwin |     |                |     |     |     |
SchoolofComputingandInformationSystems
TheUniversityofMelbourne
ffajri@student.unimelb.edu.au, jeyhan.lau@gmail.com, tb@ldwin.net
|            |     | Abstract      |     |                  | term   | in biology. | To     | tackle     | this problem, |          | Poerner |
| ---------- | --- | ------------- | --- | ---------------- | ------ | ----------- | ------ | ---------- | ------------- | -------- | ------- |
|            |     |               |     |                  | et al. | (2020);     | Tai et | al. (2020) |               | proposed | simple  |
| We present |     | INDOBERTWEET, |     | the first large- |        |             |        |            |               |          |         |
methodstodomain-extendtheBERTvocabulary:
| scale | pretrained | model | for Indonesian | Twitter |     |     |     |     |     |     |     |
| ----- | ---------- | ----- | -------------- | ------- | --- | --- | --- | --- | --- | --- | --- |
Poerneretal.(2020)initializenewvocabularyus-
| that | is trained | by extending | a   | monolingually- |     |     |     |     |     |     |     |
| ---- | ---------- | ------------ | --- | -------------- | --- | --- | --- | --- | --- | --- | --- |
1202 peS 01  ]LC.sc[  1v70640.9012:viXra
ingalearnedprojectionfromword2vec(Mikolov
trainedIndonesianBERTmodelwithadditive
domain-specific vocabulary. We focus in par- etal.,2013),whileTaietal.(2020)userandomini-
ticularonefficientmodeladaptationundervo- tializationwithweightaugmentation,substantially
cabulary mismatch, and benchmark different increasingthenumberofmodelparameters.
waysofinitializingtheBERTembeddinglayer
Newvocabularyaugmentationhasbeenalsocon-
| for new | word        | types. | We find | that initializing |        |     |                   |      |              |     |         |
| ------- | ----------- | ------ | ------- | ----------------- | ------ | --- | ----------------- | ---- | ------------ | --- | ------- |
|         |             |        |         |                   | ducted | for | language-adaptive |      | pretraining, |     | mainly  |
| with    | the average | BERT   | subword | embedding         |        |     |                   |      |              |     |         |
|         |             |        |         |                   | based  | on  | multilingual      | BERT | (MBERT).     |     | For in- |
makespretrainingfivetimesfaster,andismore
|           |      |          |         |             | stance, | Chau | et al. | (2020) | replace | 99  | “unused” |
| --------- | ---- | -------- | ------- | ----------- | ------- | ---- | ------ | ------ | ------- | --- | -------- |
| effective | than | proposed | methods | for vocabu- |         |      |        |        |         |     |          |
laryadaptationintermsofextrinsicevaluation WordPiece tokens of MBERT with new com-
oversevenTwitter-baseddatasets.1
|     |     |     |     |     | mon | tokens | in the | target | language, | while | Wang |
| --- | --- | --- | --- | --- | --- | ------ | ------ | ------ | --------- | ----- | ---- |
etal.(2020)extendMBERTvocabularywithnon-
1 Introduction
|     |     |     |     |     | overlappingtokens(|V |     |     |       | −V  | |). | Thesetwo |
| --- | --- | --- | --- | --- | -------------------- | --- | --- | ----- | --- | --- | -------- |
|     |     |     |     |     |                      |     |     | MBERT |     | new |          |
Transformer-based pretrained language models approachesuserandominitializationfornewWord-
Piecetokenembeddings.
(Vaswanietal.,2017;Devlinetal.,2019;Liuetal.,
2019;Radfordetal.,2019)havebecometheback- In this paper, we focus on the task of learning
boneofmodernNLPsystems,duetotheirsuccess anIndonesianBERTmodelforTwitter,andshow
acrossvariouslanguagesandtasks. However,ob- that initializing domain-specific vocabulary with
taininghigh-qualitycontextualizedrepresentations average-poolingofBERTsubwordembeddingsis
forspecificdomains/datasourcessuchasbiomedi- more efficient than pretraining from scratch, and
cal,socialmedia,andlegal,remainsachallenge. moreeffectivethaninitializingbasedonword2vec
Previous studies (Alsentzer et al., 2019; projections (Poerner et al., 2020). We use IN-
Chalkidis et al., 2020; Nguyen et al., 2020) have DOBERT (Koto et al., 2020b), a monolingual
shown that for domain-specific text, pretraining BERTforIndonesianasthedomain-generalmodel
fromscratchoutperformsoff-the-shelfBERT.As todevelopapretraineddomain-specificmodelIN-
analternativeapproachwithlowercost,Gururan- DOBERTWEETforIndonesianTwitter.
ganetal.(2020)demonstratedthatdomainadap-
|     |     |     |     |     | There | are | two primary |     | reasons | to  | experiment |
| --- | --- | --- | --- | --- | ----- | --- | ----------- | --- | ------- | --- | ---------- |
tivepretraining(i.e.pretrainingthemodelontarget withIndonesianTwitter. First,despitebeingtheof-
domain text before task fine-tuning) is effective, ficiallanguageofthe5thmostpopulousnation,In-
althoughstillnotasgoodastrainingfromscratch.
donesianisunderrepresentedinNLP(notwithstand-
Themaindrawbackofdomain-adaptivepretrain-
|     |     |     |     |     | ing | recent | Indonesian | benchmarks |     | and | datasets |
| --- | --- | --- | --- | --- | --- | ------ | ---------- | ---------- | --- | --- | -------- |
ingisthatdomain-specificwordsthatarenotinthe (Wilie et al., 2020; Koto et al., 2020a,b)). Sec-
pretrained vocabulary are often tokenized poorly. ond,withalargeuserbase,Twitterisoftenutilized
| Forinstance,in |     | BIOBERT | (Leeetal.,2019),Im- |     |            |     |               |     |          |         |         |
| -------------- | --- | ------- | ------------------- | --- | ---------- | --- | ------------- | --- | -------- | ------- | ------- |
|                |     |         |                     |     | to support |     | policymakers, |     | business | (Fiarni | et al., |
munoglobulinistokenizedinto{I,##mm, ##uno, 2016),ortomonitorelections(Suciatietal.,2019)
##g,##lo,##bul,##in},despitebeingacommon or health issues (Prastyo et al., 2020). Note that
mostpreviousstudiesthattargetIndonesianTwit-
| 1Code | and models | can | be accessed | at https:// |     |     |     |     |     |     |     |
| ----- | ---------- | --- | ----------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
tertendtousetraditionalmachinelearningmodels
github.com/indolem/IndoBERTweet

(e.g. n-gram and recurrent models (Fiarni et al., feed-forward hidden layers (dimension=3,072).
2016;KotoandRahmaningtyas,2017)). The only difference is the maximum sequence
Tosummarizeourcontributions: (1)werelease length, which we set to 128 tokens based on the
INDOBERTWEET,thefirstlarge-scalepretrained average number of words per document in our
Twittercorpus.
Indonesianlanguagemodelforsocialmediadata;
| and (2) | through | extensive |     | experimentation, |     | we  |                     |     |     |                  |     |     |
| ------- | ------- | --------- | --- | ---------------- | --- | --- | ------------------- | --- | --- | ---------------- | --- | --- |
|         |         |           |     |                  |     |     | Inthiswork,wetrain5 |     |     | INDOBERTWEETmod- |     |     |
comparearangeofapproachestodomain-specific els. The first model is pretrained from scratch
vocabulary initialization over a domain-general basedontheaforementionedconfiguration. There-
BERTmodel,andfindthatasimpleaverageofsub-
mainingfourmodelsarebasedondomain-adaptive
wordembeddingsismoreeffectivethanpreviously- pretraining with different vocabulary adaptation
proposed methods and reduces the overhead for strategies,asdiscussedinSection2.3.
domain-adaptivepretrainingby80%.
|     |     |     |     |     |     |     | 2.3 Domain-AdaptivePretrainingwith |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
2 INDOBERTWEET
Domain-SpecificVocabulary
Initialization
2.1 TwitterDataset
We crawl Indonesian tweets over a 1-year period We apply domain-adaptive pretraining on the
using the official Twitter API,2 from December domain-general INDOBERT (Kotoetal.,2020b),
2019toDecember2020,with60keywordscover- whichistrainedoverIndonesianWikipedia,news
| ing4maintopics: |     | economy,health,education,and |     |     |     |     |           |        |            |     |        |         |
| --------------- | --- | ---------------------------- | --- | --- | --- | --- | --------- | ------ | ---------- | --- | ------ | ------- |
|                 |     |                              |     |     |     |     | articles, | and an | Indonesian | web | corpus | (Medved |
government. We found that the Twitter language and Suchomel, 2017). Our goal is to fully re-
(V
identifierisreasonablyaccurateforIndonesian,and place INDOBERT’s vocabulary ) of 31,923
IB
INDOBERTWEET’svocabulary(V
| souseittofilteroutnon-Indonesiantweets. |     |     |     |     |     | From | typeswith |     |     |     |     | IBT ) |
| --------------------------------------- | --- | --- | --- | --- | --- | ---- | --------- | --- | --- | --- | --- | ----- |
100randomly-sampledtweets,wefoundamajority (31,984 types). In INDOBERTWEET, there are
ofthem(87)tobeIndonesian,withasmallnumber 14,584(46%)newtypes,and17,400(54%)Word-
| beingMalay(12)andSwahili(1).3 |     |     |     |     |     |     |     |     |     |     | INDOBERT.6 |     |
| ----------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --- |
Piecetypeswhicharesharedwith
Afterremovingredundanttweets(withthesame
Toinitializethedomain-specificvocabulary,we
ID),weobtain26Mtweetswith409Mwordtokens,
useINDOBERTembeddingsforthe17,400shared
twotimeslargerthanthetrainingdatausedtopre- types,andexplorefourinitializationstrategiesfor
trainINDOBERT(Kotoetal.,2020b). Wesetaside new word types: (1) random initialization from
230Ktweetsfordevelopment,andextractavocabu-
U(−1,1);(2)randominitializationfromN(µ,σ),
laryof31,984typesbasedonWordPiece(Wuetal., whereµandσ arelearnedfrom INDOBERT em-
2016). We lower-case all words and follow the beddings;(3)linearprojectionviafastTextem-
| samepreprocessingstepsasEnglish |     |     |     |     | BERTWEET |     |     |     |     |     |     |     |
| ------------------------------- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
beddings(Poerneretal.,2020);and(4)averaging
| (Nguyen   | et al., | 2020): | (1)   | converting | user     | men- |          |                    |     |     |     |     |
| --------- | ------- | ------ | ----- | ---------- | -------- | ---- | -------- | ------------------ | --- | --- | --- | --- |
|           |         |        |       |            |          |      | INDOBERT | subwordembeddings. |     |     |     |     |
| tions and | URLs    | into   | @USER | and        | HTTPURL, | re-  |          |                    |     |     |     |     |
Forthelinearprojectionstrategy(Method3),we
spectively;and(2)translatingemoticonsintotext train 300d fastText embeddings (Bojanowski
usingtheemojipackage.4
|     |     |     |     |     |     |     | et al., 2017) | over      | the tokenized |            | Indonesian  | Twit- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --------- | ------------- | ---------- | ----------- | ----- |
|     |     |     |     |     |     |     | ter corpus.   | Following |               | Poerner et | al. (2020), | we    |
2.2 INDOBERTWEETModel
|     |     |     |     |     |     |     | usethesharedtypes(V |     |     | ∩V  | )totrainalinear |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------- | --- | --- | --- | --------------- | --- |
|     |     |     |     |     |     |     |                     |     | IB  | IBT |                 |     |
INDOBERTWEET is trained based on a masked transformationfromfastTextembeddingsE
FT
| language | model |     | objective | (Devlin |     | et al., |             |     |             |            |     |     |
| -------- | ----- | --- | --------- | ------- | --- | ------- | ----------- | --- | ----------- | ---------- | --- | --- |
|          |       |     |           |         |     |         | to INDOBERT |     | embeddingsE | asfollows: |     |     |
IB
| 2019) | following | the | same | procedure |     | as the |     |     |     |     |     |     |
| ----- | --------- | --- | ---- | --------- | --- | ------ | --- | --- | --- | --- | --- | --- |
model.5
| indobert-base-uncased |     |         |     | (INDOBERT) |        |        |        |     | (cid:88)   |        |     |               |
| --------------------- | --- | ------- | --- | ---------- | ------ | ------ | ------ | --- | ---------- | ------ | --- | ------------- |
|                       |     |         |     |            |        |        | argmin |     | (cid:107)E | (x)W−E |     | (x)(cid:107)2 |
| It is a transformer   |     | encoder |     | with 12    | hidden | layers |        |     |            | FT     | IB  | 2             |
W
x∈V IB∩V
| (dimension=768), |     |     | 12 attention | heads, |     | and 3 |     |     | IBT |     |     |     |
| ---------------- | --- | --- | ------------ | ------ | --- | ----- | --- | --- | --- | --- | --- | --- |
2https://developer.twitter.com/ whereWisadim(E )×dim(E )matrix.
|     |     |     |     |     |     |     |     |     | FT  |     | IB  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
3NotethatIndonesianandMalayareverycloselyrelated,
|                                                       |     |     |     |     |     |     | To average | subword |     | embeddings | of x | ∈ V |
| ----------------------------------------------------- | --- | --- | --- | --- | --- | --- | ---------- | ------- | --- | ---------- | ---- | --- |
| butalsothatweimplicitlyevaluatetheimpactofthelanguage |     |     |     |     |     |     |            |         |     |            |      | IBT |
confluenceinourexperimentsover(pure)Indonesiandatasets.
4https://pypi.org/project/emoji/
|     |     |     |     |     |     |     | 6Intheimplementation, |     |     | wesettheadaptivevocabulary |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------- | --- | --- | -------------------------- | --- | --- |
5https://huggingface.co/indolem/ to be the same size with INDOBERT by discarding some
| indobert-base-uncased |     |     |     |     |     |     | “[unused-x]”tokensofINDOBERTWEET. |     |     |     |     |     |
| --------------------- | --- | --- | --- | --- | --- | --- | --------------------------------- | --- | --- | --- | --- | --- |

Task Data #labels #train #dev #test 5-Fold Evaluation
IndoLEM(Kotoetal.,2020b) 2 3,638 399 1,011 Yes F1
SentimentAnalysis pos
SmSA(Wilieetal.,2020) 3 11,000 1,260 500 No F1
macro
EmotionClassification EmoT(Wilieetal.,2020) 5 3,521 440 442 No F1
macro
HS1(Alfinaetal.,2017) 2 499 72 142 Yes F1
HateSpeechDetection pos
HS2(IbrohimandBudi,2019) 2 9,219 2,633 1,317 Yes F1
pos
Formal(Munarkoetal.,2018) 3 6,500 657 1,122 No F1
NamedEntityRecognition entity
Informal(Munarkoetal.,2018) 3 6,500 657 1,227 No F1
entity
Table1: SummaryofIndonesianTwitterdatasetsusedinourexperiments.
(Method4),wecompute: mixtureofformalandinformaltweets,andshared
acrossthetwotestsets.
1 (cid:88)
E (x) = E (y) Fine-tuning. Forsentiment,emotion,andhate
IBT IB
|T (x)|
IB y∈TIB(x) speech classification, we add an MLP layer that
takes the average pooled output of INDOBER-
where T (x) is the set of WordPiece tokens for
IB TWEET as input, while for NER we use the first
wordxproducedby INDOBERT’stokenizer.
subwordofeachwordtokenfortagprediction. We
pre-processthetweetsasdescribedinSection2.1,
3 ExperimentalSetup
anduseabatchsizeof30,maximumtokenlength
Weaccumulategradientsover4stepstosimulatea of128,learningrateof5e−5,Adamoptimizerwith
batchsizeof2048. Whenpretrainingfromscratch, epsilonof1e−8,andearlystoppingwithpatience
wetrainthemodelfor1Msteps,andusealearning of 5. We additionally introduce a canonical split
rateof1e−4andtheAdamoptimizerwithalinear for both hate speech detection tasks with 5-fold
scheduler. All pretraining experiments are done crossvalidation,followingKotoetal.(2020b). In
using4×V100GPUs(32GB). Table1,SmSA,EmoT,andNERusetheoriginal
For domain-adaptive pretraining (using IN- held-outevaluationsplits.
DOBERTmodel),weconsiderthreebenchmarks: Baselines. WeusethetwoINDOBERTmodels
(1) domain-adaptive pretraining without domain- from Koto et al. (2020b) and Wilie et al. (2020)
specific vocabulary adaptation (V IBT = V IB ) for as baselines, in addition to multilingual BERT
200Ksteps;(2)applyingthenewvocabularyadap- (MBERT,whichincludesIndonesian)andamono-
tation approaches from Section 2.3 without addi- lingualBERTforMalay(MALAYBERT).7 Ourra-
tionaldomain-adaptivepretraining;and(3)apply- tionaleforincludingMALAYBERTisthatweare
ingthenewvocabularyadaptationapproachesfrom interestedintestingitsperformanceonIndonesian,
Section2.3with200Kdomain-adaptivepretraining given that the two languages are closely related
steps. andweknowthattheTwittertrainingdataincludes
Downstreamtasks. Toevaluatethepretrained someamountofMalaytext.
models, we use 7 Indonesian Twitter datasets, as
summarized in Table 1. This includes sentiment 4 ExperimentalResults
analysis(KotoandRahmaningtyas,2017;Purwari-
antiandCrisdayanti,2019),emotionclassification Table 2 shows the full results across the differ-
(Saputri et al., 2018), hate speech detection (Al- ent pretrained models for the 7 Indonesian Twit-
fina et al., 2017; Ibrohim and Budi, 2019), and ter datasets. Note that the first four models are
named entity recognition (Munarko et al., 2018). pretrained models without domain-adaptive pre-
For emotion classification, the classes are fear, training(i.e.theyareusedaspurelyoff-the-shelf
angry, sad, happy, and love. Named en- models). In terms of baselines, MALAYBERT is
tity recognition (NER) is based on the PERSON, abettermodelforIndonesianthan MBERT,con-
ORGANIZATION,andLOCATIONtags. NERhas sistent with Koto et al. (2020b), and better again
twotestsetpartitions,wherethefirstisformaltexts are the two different INDOBERT models at al-
(e.g. news snippets on Twitter) and the second is
7https://huggingface.co/huseinzol05/
informal texts. The train and dev partitions are a bert-base-bahasa-cased

|           |     |     |         | Sentiment |      | Emotion | HateSpeech |      |        | NER |          |         |
| --------- | --- | --- | ------- | --------- | ---- | ------- | ---------- | ---- | ------ | --- | -------- | ------- |
| Model     |     |     |         |           |      |         |            |      |        |     |          | Average |
|           |     |     | IndoLEM |           | SmSA | EmoT    | HS1        | HS2  | Formal |     | Informal |         |
| MBERT     |     |     |         | 76.6      | 84.7 | 67.5    | 85.1       | 75.1 | 85.2   |     | 83.2     | 79.6    |
| MALAYBERT |     |     |         | 82.0      | 84.1 | 74.2    | 85.0       | 81.9 | 81.9   |     | 81.3     | 81.5    |
INDOBERT(Wilieetal.,2020) 84.1 88.7 73.3 86.8 80.4 86.3 84.3 83.4
INDOBERT(Kotoetal.,2020b) 84.1 87.9 71.0 86.4 79.3 88.0 86.9 83.4
INDOBERTWEET(1Msteps) 86.2 90.4 76.0 88.8 87.5 88.1 85.4 86.1
INDOBERT(Kotoetal.,2020b)+200Kstepsofdomain-adaptivepretraining
| Samevocabulary(V |     | =V     |     |      |      |      |      |      |      |     |      |      |
| ---------------- | --- | ------ | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- | ---- | ---- |
|                  |     | IBT IB | )   | 86.4 | 92.7 | 76.8 | 88.7 | 82.2 | 87.9 |     | 86.9 | 85.9 |
INDOBERT(Kotoetal.,2020b) +vocabularyadaptation+0stepsofdomain-adaptivepretraining
| Uniformdistribution |     |     |     | 82.9 | 84.6 | 73.2 | 84.9 | 78.2 | 84.3 |     | 84.4 | 81.8 |
| ------------------- | --- | --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- | ---- | ---- |
| Normaldistribution  |     |     |     | 83.5 | 86.7 | 71.1 | 85.2 | 77.4 | 85.0 |     | 86.3 | 82.2 |
| fastTextprojection  |     |     |     | 84.4 | 83.6 | 72.2 | 85.5 | 80.9 | 85.4 |     | 85.6 | 82.5 |
| Averageofsubwords   |     |     |     | 84.2 | 88.1 | 71.6 | 86.2 | 78.3 | 86.4 |     | 87.4 | 83.2 |
INDOBERT(Kotoetal.,2020b)+vocabularyadaptation+200Kstepsofdomain-adaptivepretraining
| Uniformdistribution |     |     |     | 85.6 | 90.9 | 75.7 | 88.4 | 83.0 | 87.7 |     | 85.9 | 85.3 |
| ------------------- | --- | --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- | ---- | ---- |
| Normaldistribution  |     |     |     | 87.1 | 92.5 | 75.4 | 88.8 | 82.5 | 88.7 |     | 86.6 | 85.9 |
fastTextprojection
|                   |     |     |     | 86.4 | 89.7 | 78.5 | 88.7 | 84.4 | 88.0 |     | 86.6 | 86.0 |
| ----------------- | --- | --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- | ---- | ---- |
| Averageofsubwords |     |     |     | 86.6 | 92.7 | 79.0 | 88.4 | 84.0 | 87.7 |     | 86.9 | 86.5 |
Table 2: A comparison of pretrained models with different adaptive pretraining strategies for Indonesian tweets
(%).
performance.8
most identical INDOBERTWEET formingthebest,infactoutperformingthedomain-
—trainedfromscratchfor1Msteps—resultsin specific INDOBERTWEET when trained for 1M
asubstantialimprovementintermsofaverageper- stepsfromscratch. Thesefindingsrevealthatwe
formance(almost+3%absolute),consistentwith canadaptanoff-the-shelfpretrainedmodelveryef-
previousfindingsthatoff-the-shelfdomain-general ficiently(5timesfasterthantrainingfromscratch)
pretrained models are sub-optimal for domain- withbetteraverageperformance.
| specific tasks                | (Alsentzer | et       | al., | 2019; | Chalkidis |      |            |     |     |     |     |     |
| ----------------------------- | ---------- | -------- | ---- | ----- | --------- | ---- | ---------- | --- | --- | --- | --- | --- |
| etal.,2020;Nguyenetal.,2020). |            |          |      |       |           | 5    | Discussion |     |     |     |     |     |
| First, we                     | pretrain   | INDOBERT |      | (Koto | et        | al., |            |     |     |     |     |     |
2020b) without vocabulary adaptation for 200K GiventhesepositiveresultsonIndonesian,wecon-
steps, and find that the results are slightly lower ductedasimilarexperimentinasecondlanguage,
|                    |     |     |          |     |           | English: | wefollowNguyenetal.(2020)inadapt- |     |     |     |     |     |
| ------------------ | --- | --- | -------- | --- | --------- | -------- | --------------------------------- | --- | --- | --- | --- | --- |
| than INDOBERTWEET. |     | In  | the next | set | of exper- |          |                                   |     |     |     |     |     |
iments, we take INDOBERT (Koto et al., 2020b) ing ROBERTA 9 forTwitterusingtheembedding
andreplacethedomain-generalvocabularywiththe averagingmethodtoinitializenewvocabulary,and
|     |     |     |     |     |     | compare | ourselves |     | against | BERTWEET |     | (trained |
| --- | --- | --- | --- | --- | --- | ------- | --------- | --- | ------- | -------- | --- | -------- |
domain-specificvocabularyofINDOBERTWEET,
withoutanypretraining(“0steps”). Resultsdrop fromscratchon845MEnglishtweets).
overall relative to the original model, with the AcaveathereisthatBERTWEET(Nguyenetal.,
embedding averaging method (“Average of Sub- 2020)and ROBERTA (Liuetal.,2019)usediffer-
|     |     |     |     |     |     |     |     |     |     | byte-level |     | BPEvs. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------ |
words”)yieldingthesmallestoverallgapof−0.2% enttokenizationmethods:
| absolute. |     |     |     |     |     | fastBPE(Sennrichetal.,2016). |     |     |     |     | Becauseofthis, |     |
| --------- | --- | --- | --- | --- | --- | ---------------------------- | --- | --- | --- | --- | -------------- | --- |
Finally, we pretrain INDOBERT (Koto et al., ratherthanreplacingROBERTA’svocabularywith
2020b)for200Kstepsinthetargetdomain,after BERTWEET’s(likeourIndonesianexperiments),
performingvocabularyadaptation. Weseeastrong we train ROBERTA’s BPE tokenizer on English
improvement for all initialization methods, with Twitterdata(describedbelow)tocreateadomain-
theembeddingaveragingmethodonceagainper- specificvocabulary. Thismeansthatthetwomod-
|     |     |     |     |     |     | els(BERTWEET |     |     | anddomain-adapted |     |     | ROBERTA |
| --- | --- | --- | --- | --- | --- | ------------ | --- | --- | ----------------- | --- | --- | ------- |
8NotingthatWilieetal.(2020)’sversionincludes100M
| words of tweets | for pretraining, |     | but Koto | et  | al. (2020b)’s |                  |     |     |     |     |     |     |
| --------------- | ---------------- | --- | -------- | --- | ------------- | ---------------- | --- | --- | --- | --- | --- | --- |
| versiondoesnot. |                  |     |          |     |               | 9Thebaseversion. |     |     |     |     |     |     |

Model Average
BERTweet (ours) IndoBERTweet
ROBERTA 72.9 12500
BERTWEET(Nguyenetal.,2020) 76.3
10000
ROBERTA+vocabularyadaptation+
74.1
200Kstepsofdomain-adaptivepretraining 7500
5000
Table 3: English results (%). The presented perfor-
2500
mance is averaged over 7 downstream tasks (Nguyen
etal.,2020). RefertotheAppendixfordetails.
0
1 2 3 4 5 6 7 8 9 10 >10
#subword of a new type (vocabulary)
withmodifiedvocabulary)willnotbedirectlycom-
parable. Figure 1: Frequency of #subword of new types in
Following Nguyen et al. (2020), we download BERTWEET (ours) and INDOBERTWEET, tokenized
42MtweetsfromtheInternetArchive10overthepe- by ROBERTA and INDOBERT tokenizers, respec-
tively. #subword=1meansthenewtypeistokenized
riodJuly2017toOctober2019(thefirsttwodays
as“[UNK]”.
ofeachmonth),whichweusefordomain-adaptive
pretraining. Notethatthispretrainingdataisanor-
derofmagnitudesmallerthanthatof BERTWEET
new types are 2.6 and 3.4 for INDOBERTWEET
(42Mvs.845M).WeuseSpaCy11 tofilterEnglish
and BERTWEET,respectively).
tweets, and follow the same preprocessing steps
and downstream tasks as Nguyen et al. (2020) (7 6 Conclusion
tasks in total; see the Appendix for details). We
pretrain ROBERTA for200Kstepsusingtheem- Wepresentthefirstlarge-scalepretrainedmodelfor
beddingaveragingmethod. IndonesianTwitter. Weexploreddomain-adaptive
In Table 3, we see that BERTWEET outper- pretrainingwithdomain-specificvocabularyadap-
formsROBERTA(+3.4%absolute). Withdomain- tationusingseveralstrategies, andfoundthatthe
adaptivepretrainingusingdomain-specificvocabu- bestmethod—averagingofsubwordembeddings
lary,theperformancegapnarrowsto+2.2%,but fromtheoriginalmodel—achievedthebestaver-
are not as impressive as our Indonesian experi- age performance across 7 tasks, and is five times
ments. There are two reasons for this: (1) our faster than the dominant paradigm of pretraining
domain-adaptive pretraining data is an order of fromscratch.
magnitudesmallerthanfor BERTWEET; and(2)
the difference in tokenization methods between Acknowledgements
BERTWEET and ROBERTA resultsinaverydif-
We are grateful to the anonymous reviewers for
ferentvocabulary.
their helpful feedback and suggestions. The first
Lastly, we argue that the different tokeniza-
authorissupportedbytheAustraliaAwardsSchol-
tion settings between INDOBERTWEET and
arship(AAS),fundedbytheDepartmentofForeign
BERTWEET(ours)mayalsocontributetothedif-
AffairsandTrade(DFAT),Australia. Thisresearch
ference in results. The differences include: (1)
wasundertakenusingtheLIEFHPC-GPGPUFa-
uncased vs. cased; (2) WordPiece vs. fastBPE
cilityhostedatTheUniversityofMelbourne. This
tokenizer; and(3)vocabularysize(32Kvs.50K)
facilitywasestablishedwiththeassistanceofLIEF
between both models. In Figure 1, we present
GrantLE170100200.
the frequency distribution of #subword of new
types in both models after tokenizing by each
general-domain tokenizer. Interestingly, we find
References
that BERTWEET has more new types than IN-
DOBERTWEET,with#subwordaftertokenization Ika Alfina, Rio Mulia, Mohamad Ivan Fanany, and
beingmorevaried(averagelengthof#subwordof Yudo Ekanata. 2017. Hate speech detection in the
indonesian language: A dataset and preliminary
10https://archive.org/details/ study. In 2017 International Conference on Ad-
twitterstream vancedComputerScienceandInformationSystems
11https://spacy.io/ (ICACSIS),pages233–238.

Emily Alsentzer, John Murphy, William Boag, Wei- and Noah A. Smith. 2020. Don’t stop pretraining:
Hung Weng, Di Jindi, Tristan Naumann, and Adapt language models to domains and tasks. In
MatthewMcDermott.2019. Publiclyavailableclini- Proceedings of the 58th Annual Meeting of the
cal BERT embeddings. In Proceedings of the 2nd Association for Computational Linguistics, pages
Clinical Natural Language Processing Workshop, 8342–8360, Online. Association for Computational
| pages 72–78, |     | Minneapolis, |     | Minnesota, | USA. | Asso- | Linguistics. |     |     |     |     |     |     |
| ------------ | --- | ------------ | --- | ---------- | ---- | ----- | ------------ | --- | --- | --- | --- | --- | --- |
ciationforComputationalLinguistics.
|     |     |     |     |     |     |     | Muhammad | Okky | Ibrohim |     | and | Indra | Budi. 2019. |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---- | ------- | --- | --- | ----- | ----------- |
PiotrBojanowski,EdouardGrave,ArmandJoulin,and Multi-label hate speech and abusive language de-
TomasMikolov.2017. Enrichingwordvectorswith tection in Indonesian Twitter. In Proceedings of
subword information. Transactions of the Associa- the Third Workshop on Abusive Language Online,
tionforComputationalLinguistics,5:135–146.
|     |     |     |     |     |     |     | pages | 46–57, | Florence, | Italy. | Association |     | for Com- |
| --- | --- | --- | --- | --- | --- | --- | ----- | ------ | --------- | ------ | ----------- | --- | -------- |
putationalLinguistics.
IliasChalkidis,ManosFergadiotis,ProdromosMalaka-
| siotis, Nikolaos |     | Aletras, | and | Ion | Androutsopoulos. |     |     |     |     |     |     |     |     |
| ---------------- | --- | -------- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
FajriKoto,JeyHanLau,andTimothyBaldwin.2020a.
2020. LEGAL-BERT: The muppets straight out of Liputan6: A large-scale Indonesian dataset for text
lawschool. InFindingsoftheAssociationforCom- summarization. In Proceedings of the 1st Confer-
putational Linguistics: EMNLP 2020, pages 2898– ence of the Asia-Pacific Chapter of the Association
| 2904, Online. |     | Association |     | for Computational |     | Lin- |     |     |     |     |     |     |     |
| ------------- | --- | ----------- | --- | ----------------- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
forComputationalLinguisticsandthe10thInterna-
guistics.
|     |     |     |     |     |     |     | tional   | Joint | Conference | on  | Natural | Language | Pro-     |
| --- | --- | --- | --- | --- | --- | --- | -------- | ----- | ---------- | --- | ------- | -------- | -------- |
|     |     |     |     |     |     |     | cessing, | pages | 598–608,   |     | Suzhou, | China.   | Associa- |
EthanC.Chau,LucyH.Lin,andNoahA.Smith.2020.
tionforComputationalLinguistics.
ParsingwithmultilingualBERT,asmallcorpus,and
| a small | treebank. | In  | Findings | of  | the Association |     |             |        |         |     |         |      |           |
| ------- | --------- | --- | -------- | --- | --------------- | --- | ----------- | ------ | ------- | --- | ------- | ---- | --------- |
|         |           |     |          |     |                 |     | Fajri Koto, | Afshin | Rahimi, |     | Jey Han | Lau, | and Timo- |
forComputationalLinguistics:EMNLP2020,pages thy Baldwin. 2020b. IndoLEM and IndoBERT: A
| 1324–1334, | Online. |     | Association | for | Computational |     |           |         |     |                 |     |          |       |
| ---------- | ------- | --- | ----------- | --- | ------------- | --- | --------- | ------- | --- | --------------- | --- | -------- | ----- |
|            |         |     |             |     |               |     | benchmark | dataset |     | and pre-trained |     | language | model |
Linguistics.
|                      |                                    |              |                      |                |             |          | forIndonesianNLP.                      |            |     | InProceedingsofthe28thIn- |               |       |               |
| -------------------- | ---------------------------------- | ------------ | -------------------- | -------------- | ----------- | -------- | -------------------------------------- | ---------- | --- | ------------------------- | ------------- | ----- | ------------- |
|                      |                                    |              |                      |                |             |          | ternational                            | Conference |     | on                        | Computational |       | Linguis-      |
| LeonDerczynski,      |                                    | EricNichols, |                      | MariekevanErp, |             | and      |                                        |            |     |                           |               |       |               |
|                      |                                    |              |                      |                |             |          | tics, pages                            | 757–770,   |     | Barcelona,                |               | Spain | (Online). In- |
| NutLimsopatham.2017. |                                    |              | ResultsoftheWNUT2017 |                |             |          |                                        |            |     |                           |               |       |               |
|                      |                                    |              |                      |                |             |          | ternational                            | Committee  |     | on                        | Computational |       | Linguis-      |
| shared task          | on                                 | novel        | and emerging         |                | entity      | recogni- |                                        |            |     |                           |               |       |               |
| tion. In             | Proceedingsofthe3rdWorkshoponNoisy |              |                      |                |             |          | tics.                                  |            |     |                           |               |       |               |
| User-generated       |                                    | Text,        | pages                | 140–147,       | Copenhagen, |          |                                        |            |     |                           |               |       |               |
|                      |                                    |              |                      |                |             |          | FajriKotoandGemalaYRahmaningtyas.2017. |            |     |                           |               |       | InSet         |
| Denmark.             | Association                        |              | for                  | Computational  |             | Linguis- |                                        |            |     |                           |               |       |               |
lexicon:EvaluationofawordlistforIndonesiansen-
tics.
|               |          |     |        |        |     |          | timentanalysisinmicroblogs. |     |       |          | In2017International |            |         |
| ------------- | -------- | --- | ------ | ------ | --- | -------- | --------------------------- | --- | ----- | -------- | ------------------- | ---------- | ------- |
|               |          |     |        |        |     |          | Conference                  | on  | Asian | Language |                     | Processing | (IALP), |
| Jacob Devlin, | Ming-Wei |     | Chang, | Kenton |     | Lee, and |                             |     |       |          |                     |            |         |
pages391–394.IEEE.
| Kristina           | Toutanova. |              | 2019. | BERT: | Pre-training | of     |     |     |     |     |     |     |     |
| ------------------ | ---------- | ------------ | ----- | ----- | ------------ | ------ | --- | --- | --- | --- | --- | --- | --- |
| deep bidirectional |            | transformers |       | for   | language     | under- |     |     |     |     |     |     |     |
standing. In Proceedings of the 2019 Conference Jinhyuk Lee, Wonjin Yoon, Sungdong Kim,
|                   |          |              |         |       |                 |          | Donghyeon      |            | Kim,  | Sunkyu   | Kim,           | Chan            | Ho So, |
| ----------------- | -------- | ------------ | ------- | ----- | --------------- | -------- | -------------- | ---------- | ----- | -------- | -------------- | --------------- | ------ |
| of the North      | American |              | Chapter | of    | the Association |          |                |            |       |          |                |                 |        |
|                   |          |              |         |       |                 |          | and Jaewoo     |            | Kang. | 2019.    |                | BioBERT:        | a pre- |
| for Computational |          | Linguistics: |         | Human |                 | Language |                |            |       |          |                |                 |        |
|                   |          |              |         |       |                 |          | trained        | biomedical |       | language | representation |                 | model  |
| Technologies,     |          | Volume       | 1 (Long | and   | Short           | Papers), |                |            |       |          |                |                 |        |
|                   |          |              |         |       |                 |          | for biomedical |            | text  | mining.  |                | Bioinformatics, |        |
pages4171–4186,Minneapolis,Minnesota.Associ-
| ationforComputationalLinguistics. |     |     |     |     |     |     | 36(4):1234–1240. |     |     |     |     |     |     |
| --------------------------------- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- |
CutFiarni,HerastiaMaharani,andRinoPratama.2016. Yijia Liu, Yi Zhu, Wanxiang Che, Bing Qin, Nathan
SentimentanalysissystemforIndonesiaonlineretail Schneider,andNoahA.Smith.2018. Parsingtweets
|     |     |     |     |     |     |     | intoUniversalDependencies. |     |     |     | InProceedingsofthe |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------------------------- | --- | --- | --- | ------------------ | --- | --- |
shopreviewusinghierarchynaiveBayestechnique.
2018ConferenceoftheNorthAmericanChapterof
In20164thinternationalconferenceoninformation
|                   |     |     |            |           |     |          | the Association |               | for           | Computational |        | Linguistics:  | Hu-         |
| ----------------- | --- | --- | ---------- | --------- | --- | -------- | --------------- | ------------- | ------------- | ------------- | ------ | ------------- | ----------- |
| and communication |     |     | technology | (ICoICT), |     | pages 1– |                 |               |               |               |        |               |             |
| 6.IEEE.           |     |     |            |           |     |          | man Language    |               | Technologies, |               | Volume |               | 1 (Long Pa- |
|                   |     |     |            |           |     |          | pers),          | pages965–975, |               | NewOrleans,   |        | Louisiana.As- |             |
Kevin Gimpel, Nathan Schneider, Brendan O’Connor, sociationforComputationalLinguistics.
| Dipanjan | Das, | Daniel | Mills, | Jacob |     | Eisenstein, |     |     |     |     |     |     |     |
| -------- | ---- | ------ | ------ | ----- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
MichaelHeilman,DaniYogatama,JeffreyFlanigan, YinhanLiu,MyleOtt,NamanGoyal,JingfeiDu,Man-
and Noah A. Smith. 2011. Part-of-speech tagging dar Joshi, Danqi Chen, Omer Levy, Mike Lewis,
|              |             |     |           |     |                  |     | Luke | Zettlemoyer, |     | and | Veselin | Stoyanov. | 2019. |
| ------------ | ----------- | --- | --------- | --- | ---------------- | --- | ---- | ------------ | --- | --- | ------- | --------- | ----- |
| for Twitter: | Annotation, |     | features, |     | and experiments. |     |      |              |     |     |         |           |       |
In Proceedings of the 49th Annual Meeting of the RoBERTa: A robustly optimized BERT pretraining
Association for Computational Linguistics: Human approach. arXivpreprintarXiv:1907.11692.
LanguageTechnologies,pages42–47,Portland,Ore-
gon, USA. Association for Computational Linguis- Marek Medved and Vít Suchomel. 2017. Indonesian
|     |     |     |     |     |     |     | webcorpus(idWac). |     |     | InLINDAT/CLARINdigitalli- |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | ------------------------- | --- | --- | --- |
tics.
braryattheInstituteofFormalandAppliedLinguis-
Suchin Gururangan, Ana Marasovic´, Swabha tics (ÚFAL), Faculty of Mathematics and Physics,
| Swayamdipta, |     | Kyle | Lo, Iz | Beltagy, | Doug | Downey, | CharlesUniversity. |     |     |     |     |     |     |
| ------------ | --- | ---- | ------ | -------- | ---- | ------- | ------------------ | --- | --- | --- | --- | --- | --- |

Tomas Mikolov, Kai Chen, Greg Corrado, and Jef- Rico Sennrich, Barry Haddow, and Alexandra Birch.
frey Dean. 2013. Efficient estimation of word 2016. Neural machine translation of rare words
representations in vector space. arXiv preprint withsubwordunits. InProceedingsofthe54thAn-
arXiv:1301.3781. nual Meeting of the Association for Computational
Linguistics (Volume 1: Long Papers), pages 1715–
Yuda Munarko, MS Sutrisno, WAI Mahardika, Ilyas 1725, Berlin, Germany. Association for Computa-
Nuryasin, and Yufis Azhar. 2018. Named entity tionalLinguistics.
recognition model for Indonesian tweet using CRF
classifier. InIOPConferenceSeries: MaterialsSci- Benjamin Strauss, Bethany Toma, Alan Ritter, Marie-
enceandEngineering,volume403.IOPPublishing. CatherinedeMarneffe, andWeiXu.2016. Results
of the WNUT16 named entity recognition shared
Dat Quoc Nguyen, Thanh Vu, and Anh Tuan Nguyen.
task. InProceedingsofthe2ndWorkshoponNoisy
2020. BERTweet: A pre-trained language model
User-generated Text (WNUT), pages 138–144, Os-
for English tweets. In Proceedings of the 2020
aka,Japan.TheCOLING2016OrganizingCommit-
Conference on Empirical Methods in Natural Lan-
tee.
guageProcessing:SystemDemonstrations,pages9–
14, Online. Association for Computational Linguis- Andi Suciati, Ari Wibisono, and Petrus Mursanto.
tics. 2019. TwitterbuzzerdetectionforIndonesianpres-
idential election. In 2019 3rd International Con-
Nina Poerner, Ulli Waltinger, and Hinrich Schütze.
ferenceonInformaticsandComputationalSciences
2020. Inexpensive domain adaptation of pretrained
(ICICoS),pages1–5.IEEE.
languagemodels: CasestudiesonbiomedicalNER
and covid-19 QA. In Findings of the Association
Wen Tai, H. T. Kung, Xin Dong, Marcus Comiter,
forComputationalLinguistics:EMNLP2020,pages
and Chang-Fu Kuo. 2020. exBERT: Extending
1482–1490, Online. Association for Computational
pre-trainedmodelswithdomain-specificvocabulary
Linguistics. under constrained training resources. In Findings
of the Association for Computational Linguistics:
PulungHendroPrastyo,AminSiddiqSumi,AdeWidy-
EMNLP 2020, pages 1433–1439, Online. Associa-
atama Dian, and Adhistya Erna Permanasari. 2020.
tionforComputationalLinguistics.
Tweets responding to the Indonesian government’s
handling of COVID-19: Sentiment analysis using
Cynthia Van Hee, Els Lefever, and Véronique Hoste.
SVM with normalized poly kernel. Journal of In-
2018. SemEval-2018task3: IronydetectioninEn-
formationSystemsEngineeringandBusinessIntelli-
glish tweets. In Proceedings of The 12th Interna-
gence,6(2):112–122.
tionalWorkshoponSemanticEvaluation,pages39–
50, New Orleans, Louisiana. Association for Com-
Ayu Purwarianti and Ida Ayu Putu Ari Crisdayanti.
putationalLinguistics.
2019. Improving Bi-LSTM performance for In-
donesian sentiment analysis using paragraph vec-
Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob
tor. In 2019 International Conference of Advanced
Uszkoreit, Llion Jones, Aidan N. Gomez, Lukasz
Informatics: Concepts, Theory and Applications
Kaiser, and Illia Polosukhin. 2017. Attention is all
(ICAICTA),pages1–5.IEEE.
you need. In Proceedings of the 31st International
Conference on Neural Information Processing Sys-
Alec Radford, Jeffrey Wu, Rewon Child, David Luan,
tems,volume30,pages5998–6008.
DarioAmodei,andIlyaSutskever.2019. Language
modelsareunsupervisedmultitasklearners. OpenAI
Zihan Wang, Karthikeyan K, Stephen Mayhew, and
blog,1(8):9.
Dan Roth. 2020. Extending multilingual BERT to
Alan Ritter, Sam Clark, Mausam, and Oren Etzioni. low-resource languages. In Findings of the Associ-
2011. Named entity recognition in tweets: An ex- ationforComputationalLinguistics: EMNLP2020,
perimental study. In Proceedings of the 2011 Con- pages2649–2656,Online.AssociationforComputa-
ferenceonEmpiricalMethodsinNaturalLanguage tionalLinguistics.
Processing,pages1524–1534,Edinburgh,Scotland,
Bryan Wilie, Karissa Vincentio, Genta Indra Winata,
UK.AssociationforComputationalLinguistics.
Samuel Cahyawijaya, Xiaohong Li, Zhi Yuan Lim,
SaraRosenthal,NouraFarra,andPreslavNakov.2017. Sidik Soleman, Rahmad Mahendra, Pascale Fung,
SemEval-2017 task 4: Sentiment analysis in Twit- SyafriBahar,andAyuPurwarianti.2020. IndoNLU:
ter. In Proceedings of the 11th International BenchmarkandresourcesforevaluatingIndonesian
Workshop on Semantic Evaluation (SemEval-2017), natural language understanding. In Proceedings of
pages502–518,Vancouver,Canada.Associationfor the1stConferenceoftheAsia-PacificChapterofthe
ComputationalLinguistics. Association for Computational Linguistics and the
10thInternationalJointConferenceonNaturalLan-
Mei Silviana Saputri, Rahmad Mahendra, and Mirna guage Processing, pages 843–857, Suzhou, China.
Adriani.2018. EmotionclassificationonIndonesian AssociationforComputationalLinguistics.
Twitter dataset. In 2018 International Conference
onAsianLanguageProcessing(IALP),pages90–95. Yonghui Wu, Mike Schuster, Zhifeng Chen, Quoc V.
IEEE. Le, Mohammad Norouzi, Wolfgang Macherey,

Maxim Krikun, Yuan Cao, Qin Gao, Klaus
Macherey, Jeff Klingner, Apurva Shah, Melvin
Johnson, Xiaobing Liu, Łukasz Kaiser, Stephan
Gouws, Yoshikiyo Kato, Taku Kudo, Hideto
Kazawa, Keith Stevens, George Kurian, Nishant
Patil, Wei Wang, Cliff Young, Jason Smith, Jason
Riesa, Alex Rudnick, Oriol Vinyals, Greg Corrado,
MacduffHughes,andJeffreyDean.2016. Google’s
neural machine translation system: Bridging the
gapbetweenhumanandmachinetranslation. arXiv
preprintarXiv:1609.08144.

| A ResultswithEnglish | BERTWEET   |             |             |     |     |
| -------------------- | ---------- | ----------- | ----------- | --- | --- |
|                      | POSTagging | SemEval2017 | SemEval2018 |     | NER |
Model Avg.
|          | Ritter11 ARK | TB-v2 Sentimentan. | Ironydet. | WNUT2016 | WNUT2017  |
| -------- | ------------ | ------------------ | --------- | -------- | --------- |
| ROBERTA  | 88.6 91.0    | 93.4 70.8          | 71.6      | 45.5     | 49.9 72.9 |
| BERTWEET | 90.5 93.2    | 94.8 72.6          | 75.5      | 51.9     | 55.9 76.3 |
steps=0
| ROBERTAw/ | 87.7 90.2 | 92.5 65.7 | 66.1 | 39.2 | 39.2 68.7 |
| --------- | --------- | --------- | ---- | ---- | --------- |
BERTWEET
tokenizer
| ROBERTAw/new | 87.4 89.6 | 92.8 66.5 | 70.7 | 42.5 | 42.4 70.3 |
| ------------ | --------- | --------- | ---- | ---- | --------- |
tokenizer
steps=200K
| ROBERTAw/new | 90.1 90.9 | 94.9 72.1 | 73.3 | 47.2 | 50.0 74.1 |
| ------------ | --------- | --------- | ---- | ---- | --------- |
tokenizer
Table4:EnglishResults(%)overthetestsets.Alldata,metrics,andsplitsarebasedofftheexperimentsofNguyen
et al. (2020). We re-ran all experiments and found slightly lower performance for some models as compared to
BERTWEET. Forevaluation, thePOStaggingdatasets(Ritteretal.,2011;Gimpeletal.,2011;Liuetal.,2018)
useaccuracy,SemEval2017(Rosenthaletal.,2017)usesAvg ,SemEval2018(VanHeeetal.,2018)usesF1 ,
Rec pos
| andNER(Straussetal.,2016;Derczynskietal.,2017)usesF1 |     |     | entity . |     |     |
| ---------------------------------------------------- | --- | --- | -------- | --- | --- |