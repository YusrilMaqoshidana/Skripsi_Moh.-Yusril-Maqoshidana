|     | GLOW | : Global | Weighted | Self-Attention |     | Network |     | for Web |     |
| --- | ---- | -------- | -------- | -------------- | --- | ------- | --- | ------- | --- |
Search
|     |     | XuanShan      |     | ChuanjieLiu   |     |     | YiqianXia     |     |     |
| --- | --- | ------------- | --- | ------------- | --- | --- | ------------- | --- | --- |
|     |     | MicrosoftSTCA |     | MicrosoftSTCA |     |     | MicrosoftSTCA |     |     |
xuanshan@microsoft.com chuanli@microsoft.com yiqxia@microsoft.com
|     |                       | QiChen |     | YusiZhang            |     |     | KaizeDing              |     |     |
| --- | --------------------- | ------ | --- | -------------------- | --- | --- | ---------------------- | --- | --- |
|     | MicrosoftResearchAsia |        |     | MicrosoftSTCA        |     |     | ArizonaStateUniversity |     |     |
|     | cheqi@microsoft.com   |        |     | zhangyusi@pku.edu.cn |     |     | kding9@asu.edu.cn      |     |     |
1202 yaM 42  ]RI.sc[  3v68150.7002:viXra
|          |                       | YaoboLiang |     | AngenLuo         |          |     | YuxiangLuo       |     |     |
| -------- | --------------------- | ---------- | --- | ---------------- | -------- | --- | ---------------- | --- | --- |
|          | MicrosoftResearchAsia |            |     | MicrosoftSTCA    |          |     | MicrosoftSTCA    |     |     |
|          | yalia@microsoft.com   |            |     | anluo@pku.edu.cn |          |     | yuxlu@pku.edu.cn |     |     |
| ABSTRACT |                       |            |     |                  | KEYWORDS |     |                  |     |     |
Deepmatchingmodelsaimtofacilitatesearchenginesretrieving Websearch,transformermodels,globalweightrepresentation,deep
| morerelevantdocumentsbymappingqueriesanddocumentsinto |     |     |     |     | matchingmodels |     |     |     |     |
| ----------------------------------------------------- | --- | --- | --- | --- | -------------- | --- | --- | --- | --- |
semanticvectorsinthefirst-stageretrieval.WhenleveragingBERT
ACMReferenceFormat:
asthedeepmatchingmodel,theattentionscoreacrosstwowords XuanShan,ChuanjieLiu,YiqianXia,QiChen,YusiZhang,KaizeDing,
aresolelybuiltuponlocalcontextualizedwordembeddings.Itlacks YaoboLiang,AngenLuo,andYuxiangLuo.2018.GLOW:GlobalWeighted
priorglobalknowledgetodistinguishtheimportanceofdifferent Self-AttentionNetworkforWebSearch.InWoodstock’18:ACMSymposium
words,whichhasbeenprovedtoplayacriticalroleininformation onNeuralGazeDetection,June03–05,2018,Woodstock,NY.ACM,NewYork,
retrievaltasks.Inadditiontothis,BERTonlyperformsattention NY,USA,11pages.https://doi.org/10.1145/1122445.1122456
acrosssub-wordstokenswhichweakenswholewordattentionrep-
resentation.WeproposeanovelGlobalWeightedSelf-Attention 1 INTRODUCTION
(GLOW)networkforwebdocumentsearch.GLOWfusesglobal Nowadays,modernsearchenginesleveragetwo-stagealgorithms
corpusstatisticsintothedeepmatchingmodel.Byaddingprior toretrieveidealresultsfromamassiveamountofdocumentsin
| weights | into | attention generation | from global information, | like |     |     |     |     |     |
| ------- | ---- | -------------------- | ------------------------ | ---- | --- | --- | --- | --- | --- |
ordertoobtainmillisecondsqueryresponsetime.Thefirststage
BM25,GLOWsuccessfullylearnsweightedattentionscoresjointly
appliesacoarse-grainedsearchtoquicklyselectasmallsetofcan-
withquerymatrix𝑄andkeymatrix𝐾.Wealsopresentanefficient didatesfrombillionsofdocumentsusinglow-costmetrics.Then
wholewordweightsharingsolutiontobringpriorwholeword somecomplexrankingalgorithmsatthesecondstageareadopted
knowledgeintosub-wordslevelattention.ItaidsTransformerto toprunetheresults.Traditionally,thefirst-stageretrievalisbuilt
learnwholewordlevelattention.Tomakeourmodelsapplicable
ontopofaninvertedindexusingkeywordmatchwithsomequery
tocomplicatedwebsearchscenarios,weintroducecombinedfields
|     |     |     |     |     | alterations. However, | it is | hard to cover | all the ideal cases | and |
| --- | --- | --- | --- | --- | --------------------- | ----- | ------------- | ------------------- | --- |
representation to accommodate documents with multiple fields wellunderstanduser’sintention.Ifthealterationtechniquefails
evenwithvariablenumberofinstances.WedemonstrateGLOWis toenumerateallthekeywordexpansions,someidealdocuments
moreefficienttocapturethetopicalandsemanticrepresentation willbemissed.Withrecentbreakthroughindeeplearning,web
bothinqueriesanddocuments.Intrinsicevaluationandexperi-
contentscanbemoremeaningfullyrepresentedassemanticvectors.
mentsconductedonpublicdatasetsrevealGLOWtobeageneral
Especiallyforlargescaleretrievaltasks,vectorrecall[38]hasbeen
frameworkfordocumentretrievetask.Itsignificantlyoutperforms attractingmoreattentiontoremedythedisadvantagesoftraditional
BERTandothercompetitivebaselinesbyalargemarginwhilere- keyword-basedapproach.ItleverageshighefficientApproximate
tainingthesamemodelcomplexitywithBERT.Thesourcecodeis NearestNeighbor(ANN)[2]searchalgorithmstoretrieverelevant
availableathttps://github.com/GLOW-deep/GLOW.
resultsaccordingtothevectordistance.GiventhattheANNindex
issupposedtobepre-builtaheadofserving,documentshaveno
chancetointeractthequeriesatencodingstage.Toachievethis,
deepmatchingmodelsusuallyadoptaSiamesearchitecturetoem-
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalor beddocumentswithoutthehelpofqueries.Traditionalexamples
classroomuseisgrantedwithoutfeeprovidedthatcopiesarenotmadeordistributed
forprofitorcommercialadvantageandthatcopiesbearthisnoticeandthefullcitation includeDSSM[13],C-DSSM[34]andARC-I[11].Recently,Trans-
onthefirstpage.CopyrightsforcomponentsofthisworkownedbyothersthanACM formerbasedmodelslikeBERT[8]arebeingwidelyusedasthe
mustbehonored.Abstractingwithcreditispermitted.Tocopyotherwise,orrepublish,
deepmatchingmodel[23,28,30].However,whenleveragingthe
topostonserversortoredistributetolists,requirespriorspecificpermissionand/ora
fee.Requestpermissionsfrompermissions@acm.org. vanillaBERT,therearethreelimitationsweneedtoaddress.
Woodstock’18,June03–05,2018,Woodstock,NY First,theattentioncalculationinBERTreliesonlocalcontext
©2018AssociationforComputingMachinery. withinthesinglesequence.Itfailstocaptureglobalinformation
ACMISBN978-1-4503-XXXX-X/18/06...$15.00
https://doi.org/10.1145/1122445.1122456 fromwholecorpus.Forexample,inthequery“whataretheworst

Woodstock’18,June03–05,2018,Woodstock,NY Shan,etal.
effectsofpesticidestonature",theembeddingrepresentationtothis improvesthesearchrelevancebyintrinsicevaluationwithBing’s
queryarejointlytrainedbasedonquerymatrix𝑄,keymatrix𝐾 searchlogs.WealsomeasureGLOWonMSMARCO[4],theresults
and value matrix𝑉 from entire words without distinction. But andanalysesshowGLOWissuperiorinretrievalqualitywithout
itisobviousthat“pesticides"and“worst"shouldcommithigher increasinganymodelcomplexity.
attentionscoressincethesetwowordsaremorecrucialtorepresent Tosummarize,ourcontributionsare:
thetopic.Ifwestandataglobalstatisticsview,wedohavechances
• WepointoutthatvanillaTransformermaynotobtainaccu-
toidentitytheimportanceof“pesticides"and“worst".Thesetwo
rateattentionscoresinWebsearchscenarioduetolacking
wordsrarelyappearinothersequenceswhile“what",“are"and
globalpriorknowledge.
“effects"empiricallyhavehigherfrequencies,onealternativeisthat
• Wedemonstrateanoveldeepmatchingmodelbyintegrating
wecanleverageglobalstatisticsfeatureslikeInverseDocument
globalweightinformationintoTransformerandthewhole
Frequency(IDF)orBM25[31]assignalsofglobalweightstoadjust
wordweightsharingsuccessfullybridgesthesub-wordto-
theoriginalattentionscores.
kensandfullwordsdiscrepancies.
ThesecondissueisthatwhenapplyingWordPieceembedding[37],
• Weproposethecombinedfieldsrepresentationformulti-
anaturalwordmaybesplitintoseveraldifferenttokens,which
fieldsdocuments.Itwellhandlesfieldsprejudicebyfield
leadstoBERT’sattentionsolelybehavingatsub-wordsleveland
embeddingsandconsolidatesintoonevectorrepresentation
lackingwholewordlevelinteraction.Toremedythislimitation,
forperdocument.
thelatestreleasedBERTmodelhasupgradedthemasklanguage
• Weconductrigorouscomparisonsoverstate-of-the-artdeep
modeltasktowholewordlevel,butitstilldoesnotinvolveweight
matchingmodelsonpublicdatasetandBing’slargescale
distinctionsacrossdifferentwholewords.
validationdatapoints.Detailedanalysisisalsoconductedto
Thirdly,buildingasuitabledeepmatchingmodeltoforwebdoc-
studywhyGLOWcanachievebetterresults.
umentretrievalischallenging,notonlybecausetheaforementioned
challenges,butalsomultiplefieldsofdocumentsshouldbetaken
intoconsideration.Therearealwaysmultiplesourcesoftextual 2 RELATEDWORK
description(fields)correspondingtoonewebdocument.Lotsof Recently,avarietyofdeepmatchingmodelshavebeenproposedfor
studies[32,43]revealthatdifferentfieldscontaincomplementary thetextmatchingproblems,MitraandCraswell[19]gaveadetailed
information.Previousstudiesondeepmatchingmodelmainlycon- introductionabouttheresearchesmadeoninformationretrieval
siderwiththesinglefielddocumentorsimplyconcatenatemultiple withdeepneuralnetworks.Specifically,Huangetal.[13]developed
fieldsasoneunifiedfield[11,13,34].Seldomresearchespropose DSSMwithadeepstructurethatprojectqueriesanddocuments
suitablesolutionstoadaptmulti-fieldswebdocumentscenarios. intoacommonlow-dimensionalspace.Shenetal.[34]upgraded
Thus,toobtainamorecomprehensivevectorrepresentationforthe DSSMtoC-DSSMbyusingtheconvolution-maxpoolingopera-
first-stageretrieval,anefficientsolutiononmulti-fieldsiscritical. tion.Guoetal.[9]formulatedthead-hocretrievalasamatching
Empiricalstudies[32,35]showglobalrepresentativefeatures problemandproposedDeepRelevanceMatchingModel(DRMM).
likeBM25wellexpresstermimportancewithglobalcontextin- Deepmatchingmodelsareusuallyequippedintosearchengines
formation.AwordwithhighBM25scorerevealsitsuniqueness byaSiamese(symmetric)architecture[11,13,34]oranInteraction-
inthecorpus.Ithasbeenwidelyadoptedintraditionallearning focusedmanner[12,18,26].Themajordifferencebetweenthese
to rank tasks, unfortunately seldom studies investigate to inte- twoarchitecturesliesinwhenaqueryinteractswiththedocument,
grateitintoTransformerasdeepmatchingmodels.Kimetal.[15] theSiameseapproachencodesthequeryanddocumentseparately
significantlyimprovesspeech-enhancementperformancebyinte- whileInteractivewayjointlylearnstheircorrelationsattheverybe-
gratingaGaussian-weightintoattentioncalculation.Inspiredby ginning.Forlargescaledocumentmatchingtasks,especiallythose
this,inthispaperweintroduceGLOW:aGlobalWeightedSelf- thatdependonvectorsearch,theSiameseapproachispreferred
Attentionnetworktolearnthesemanticrepresentationsofqueries sinceamultitudeofdocumentsaresupposedtobeencodedwithout
anddocuments.Specifically,itpre-computesBM25scoresforquery thehelpofqueries.Tobetterfacilitatedocumentmatchingtasks,
termsanddocumenttermsrespectively,thentakingthescoresas ourproposedframeworkGLOWisbuiltuponSiamesearchitecture.
theglobalguidingweightwhenperformingself-attention.GLOW Inadditiontothis,pre-trainlanguagemodelinghasbeenproved
leveragesa30ktokenvocabularyfromWordPieceembedding,while tobeeffectiveonnaturallanguageprocessingtasks.Oneofsuch
BM25isusuallygeneratedonnaturalwordlevel,sinceonenatural models,BERT,hasbeenwidelyappliedintoretrieval-basedtasks
wordmaybemappedintodifferentWordPiecetokens,Itisvital like document ranking[40] and question answering[23, 39]. MS
topaveawaytopassBM25scorefromwordleveltotokenlevel. MARCO[4]isacollectiondatasetformulti-perspectivewebsearch
Todemonstratewholewordlevelattention,weproposeawhole tasks.Thetop10winnersintheleadingboardallleverageBERT
wordweightsharingmechanismtobridgethediscrepancybetween asabasis.Typically,Nogueiraetal.[24]builtamulti-stageranking
naturalwordsandWordPiecetokens.Sincewebdocumentsarede- architectureonBERTbyformulatingtherankingproblemaspoint-
scribedwithmultiplefields,wefurtherintroduceacombinedfields wiseandpairwiseclassification,respectively.Hanetal.combined
representationsolution,whichsuccessfullydifferentiatesdocument DeepCTretrievalmodel[7]withaTF-RankingBERTensemble[27].
fieldsbyinvolvingfieldembeddings. TheDeepCT-Indexproducestermweightsthatcanbestoredin
To the best of our knowledge, this is the first research work anordinaryinvertedindexfordocumentranking.Observedfrom
thatsuccessfullyintegratesglobalstatisticinformationintoself- anotherfamousinformationretrievaldatasetClueWeb09[5],the
attentionbasedmodelsasaguidingweight.GLOWsignificantly announced high results are also trained on Transformer based

GLOW:GlobalWeightedSelf-AttentionNetworkforWebSearch Woodstock’18,June03–05,2018,Woodstock,NY
| Matching  |     |     |     |     | Cosine  |     |     |     |     |
| --------- | --- | --- | --- | --- | ------- | --- | --- | --- | --- |
similarity
score
|                 | C   |     | T2           | T4  |     |      | … T[SEP]     | … TN-1 | TN  |
| --------------- | --- | --- | ------------ | --- | --- | ---- | ------------ | ------ | --- |
|                 |     | T1  | T3           |     |     | C T1 |              |        |     |
| Semantic level  |     |     | GLOW Encoder |     |     |      |              |        |     |
| representation  |     |     |              |     |     |      | GLOW Encoder |        |     |
…
E[CLS] Esl E##aye E##rs Eevolution E[CLS] Etoken1 … E[SEP] Esl E##aye
|     |     |     |     |     |                  |         | …   | …   |     |
| --- | --- | --- | --- | --- | ---------------- | ------- | --- | --- | --- |
|     |     |     |     |     | Field embeddings | Ef1 Ef1 | Ef2 | Ef3 | Ef3 |
Token level
|                | E0  | E1  | E2 E3 | E4  | Position embeddings |       | …   |      |      |
| -------------- | --- | --- | ----- | --- | ------------------- | ----- | --- | ---- | ---- |
| representation |     |     |       |     |                     | E0 E1 | EI  | … EN | EN+1 |
Tokenembeddings
|     | [CLS] | sl  | ##aye ##rs | evolution |     |             | …     | …   |       |
| --- | ----- | --- | ---------- | --------- | --- | ----------- | ----- | --- | ----- |
|     |       |     |            |           |     | [CLS] anime | [SEP] | sl  | ##aye |
Whole word
| Word level  |     |     |     |     | weight share |     |     |     |     |
| ----------- | --- | --- | --- | --- | ------------ | --- | --- | --- | --- |
Combined fields representation
global weight
|     | [CLS]:0.125 |     | slayers:1.25 | evolution:0.875 |     |     | …   |     |     |
| --- | ----------- | --- | ------------ | --------------- | --- | --- | --- | --- | --- |
generation [CLS]:0.125 anime: 3.157 [SEP]:0.125 … slaye:2.254
Query: “slayer evolution” Document: “https://myanimelist.net/anime/5233/Slayers_Evolution-R”
Figure1:IllustrationofGLOW.Wepresentasamplequeryanddocumenttodescribethenetworkstructure.Thecoreblock
GLOWEncodercanberepeatedmanytimes.Thebluearrowsbetweenwordlevelweightgenerationandtokenlevelrepresen-
tationindicatethewholewordweightsharingmethodology.Onewordmightmaptosingleormultipletokens.
models. By proposing a generalized autoregressive pretraining D fromamassofcandidates.d representsoneinstancefromD.
methodXLNet[41]claimeditsstate-of-the-artresult,superiorto Sinceinwebsearchdisalwaysequippedwithmultifieldscontents.
RoBERTa[17],GPT[29]andBERT+DCMN[45].Besides,Yilmazet LetF𝑑 ={𝐹 ,𝐹 ,···,𝐹 𝑘}denoteasetoffieldsassociatedwiththe
1 2
| al.[42]presentedBirch,asystemthatappliesBERTtodocument |     |     |     |     | documentd. |     |     |     |     |
| ------------------------------------------------------ | --- | --- | --- | --- | ---------- | --- | --- | --- | --- |
retrievalviaintegrationwiththeopen-sourceAnseriniinformation Forasingleq,dpair,adeepmatchingmodelusuallydescribesa
retrievaltoolkittodemonstrateend-to-endsearchoverlargedocu- matchingscorebasedontherepresentationofqandd.
mentcollections.Fromthedocument-querymatchingperspective,
|     |     |     |     |     |     | 𝑚𝑎𝑡𝑐ℎ(𝑞,𝑑)=𝐹𝑢𝑛𝑐(Φ(𝑞),Φ(F𝑑)) |     |     | (1) |
| --- | --- | --- | --- | --- | --- | --------------------------- | --- | --- | --- |
Doc2query[25]predictswhichquerieswillbeissuedforagiven
documentandthenexpandsitwiththosepredictionswithavanilla
whereΦisamodelfunctiontomapeachqueryanddocumenttoa
Transformermodel,trainedusingdatasetsconsistingofpairsof
|     |     |     |     |     | representationvector,and𝐹𝑢𝑛𝑐 |     | isthescoringfunctionbasedon |     |     |
| --- | --- | --- | --- | --- | ---------------------------- | --- | --------------------------- | --- | --- |
queryandrelevantdocuments.ColBERT[?]introducesalateinter-
thesimilaritybetweenthem.
actionarchitecturethatindependentlyencodesthequeryandthe
documentusingBERT.
|               |         |             |           |                 | 3.2 OverviewofGLOW |     |     |     |     |
| ------------- | ------- | ----------- | --------- | --------------- | ------------------ | --- | --- | --- | --- |
| Most of these | studies | consolidate | on single | field document. | Al-                |     |     |     |     |
thoughZamanietal.[43]proposedadeepneuralrankingmodel AsshowinFigure1,tofitlargescaledocumentmatchingscenario,
GLOWisbuiltonaSiamesemanner,weemploytwoGLOWEn-
onmulti-fieldsdocumentranking.Self-Attentionbasedapproaches
coderstorepresentqueriesanddocumentsrespectively.Froma
havenotbeenwellstudiedyetformulti-fieldsdocument.
horizontalview,GLOWiscomprisedoffourparts,Wordlevelglobal
weightgeneration,Tokenlevelrepresentation,Semanticlevelrepre-
3 THEGLOWFRAMEWORK
sentationandMatchingscore.Oneprerequisiteondatapreparation
Inthissection,wefirstprovidetheformulationofdocumentre-
beforetrainingisthatwesimplyprependa[CLS](classification)
trievaltask.Thenweintroduceahigh-leveloverviewofourframe-
tokentobothqueryanddocument.Fordocumentside,a[SEP]
workandfurtherdescribehowweimplementeachcomponentof
(separating)tokenisinsertedacrossdifferentfieldstoconstitute
theproposedframework.Wefinallyexplainhowweoptimizeour
thecombinedfieldsrepresentation.
deepmatchingmodel.
WeintroducesemanticlevelrepresentationinSection3.3and
|     |     |     |     |     | 3.4, which | takes GLOW | Encoder by stacking | 3   | times. Then we |
| --- | --- | --- | --- | --- | ---------- | ---------- | ------------------- | --- | -------------- |
3.1 ProblemStatement describehowtogeneratethewordlevelglobalweightinSection
Thefirst-stageofdocumentretrievaltaskcanbedescribedas,given 3.5,whatweadoptfinallyasglobalweightisBM25.Thewhole
onequeryq,thesystemproducesafixedamountofdocuments wordweightsharingisdescribedinSection3.6toexplainhowwe

| Woodstock’18,June03–05,2018,Woodstock,NY |     |     |     |     |     |     |     |     |     |     |     |     |     | Shan,etal. |
| ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- |
mapweightfromwholewordstoWordPiecetokens.Forthetoken Global weighted self-attention
| level | representation, |     | we  | use the | sum of | token embeddings |     | and |     |     |     |     |     |     |
| ----- | --------------- | --- | --- | ------- | ------ | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
positionembeddingstoformthetokenrepresentationforquery
side.Fordocument,weintroducethecombinedfieldsrepresention
inSection3.7,itaddsfieldembeddingstodifferentiatemulti-fields Reshape
Global weighted
| indocuments.Weadoptcosinesimilaritytodescribethematching |     |     |     |     |     |     |     |     | attention matrix |     |     |     |     |     |
| -------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- |
score.Section3.8explainshowweoptimizethematchingscore
withtraininglabels.
Expand dim
| 3.3                                      | GlobalWeightedSelf-Attention |        |           |                                    |           |               |         |     | Original attention |         |     |         |               |     |
| ---------------------------------------- | ---------------------------- | ------ | --------- | ---------------------------------- | --------- | ------------- | ------- | --- | ------------------ | ------- | --- | ------- | ------------- | --- |
|                                          |                              |        | R𝑑×𝑇      |                                    |           |               |         |     | matrix             |         |     |         | Global weight |     |
| Let’sdefineX                             |                              |        | ∈         | isa𝑑-dimensionalsequenceembedding  |           |               |         |     |                    |         |     |         |               |     |
| inputofonequeryordocumentwithlengthof𝑇,𝑥 |                              |        |           |                                    |           | isthe𝑖thtoken |         |     |                    |         |     |         |               |     |
|                                          |                              |        |           |                                    |           | 𝑖             |         |     |                    | Reshape |     | Reshape |               |     |
| inthesequence.𝑄,𝐾and𝑉                    |                              |        |           | arematricesinitiatedbyXmultiplying |           |               |         |     |                    |         |     |         |               |     |
| different                                |                              | weight | matrices. | The                                | attention | score matrix  | in such | a   |                    |         |     |         |               |     |
sequenceisdenotedbyA∈R𝑇×𝑇.Foratokenpair𝑥
|     |     |     |     |     |     |     | 𝑖 ,𝑥 𝑗 ,𝑞 | 𝑖 and |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ----- | --- | --- | --- | --- | --- | --- |
𝑘 𝑗 arethecolumnselectionfrom𝑄 and𝐾 accordingto𝑖or 𝑗,its WQ WK WV
| attentionscore𝐴 |     |     | iscalculatedinScaledDot-ProductAttention |     |     |     |     |     |     |     |     |     |     |     |
| --------------- | --- | --- | ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
𝑖𝑗
|     |     | 𝑞𝑖 ·𝑘𝑇                                        |     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| as𝐴 |     | 𝑗 .In[36],theyclaimtheattentionunitisalreadya |     |     |     |     |     |     |     |     |     |     |     |     |
𝑖𝑗 = √
𝑑
weightedsumofvalues,wheretheweightassignedtoeachvalueis
learnedfrom𝑞 and𝑘 .Whereas,ininformationretrievalarea,itis Input sequence Sequence BM25 score
|     |     | 𝑖   | 𝑗   |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
wellequippedwithpriorknowledgetorepresenttheweightofone
word.Weenrichtheattentioncalculationwiththesetechniques. Figure 2: Block diagram of the proposed Global Weighted
|               |     | ∈R𝑇 |                                          |     |     |     |     |     | Self-Attention. |     |     |     |     |     |
| ------------- | --- | --- | ---------------------------------------- | --- | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- |
| Assuming𝑤     |     | 𝑖   | representstheglobalweightofthe𝑖thtokenin |     |     |     |     |     |                 |     |     |     |     |     |
| thesequence,𝑤 |     |     | isanon-trainablescalar.Inthispaperweuse  |     |     |     |     |     |                 |     |     |     |     |     |
𝑖
BM25torepresentthisglobalimportance.Thusanewweighted
Algorithm1EncodingAlgorithm
| attentionscore𝐴𝑤 |     |     | iscomputedas |     |     |     |     |     |     |     |     |     |     |     |
| ---------------- | --- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
𝑖𝑗
|     |     |     |     |       |     |     |     |     |        | Onequery𝑞,Onedocument𝑑,Onevocabularyfile𝑉 |     |     |     | for |
| --- | --- | --- | --- | ----- | --- | --- | --- | --- | ------ | ----------------------------------------- | --- | --- | --- | --- |
|     |     |     |     |       |     |     |     |     | Input: |                                           |     |     |     | 𝑡   |
|     |     |     |     | 𝑞 ·𝑘𝑇 |     | 𝑇   |     |     |        |                                           |     |     |     |     |
𝑖 𝑗 𝑞 𝑗 ·𝑘 tok e n s, O n e i d f v o c a b u la ry fi l e 𝑉 𝑤 fo r w o r d s,hyper-parameter
|     |     |     | 𝐴 𝑤 =𝑤 | √   | ,𝐴𝑤 =𝑤 | √ 𝑖 |     | (2) |     |     |     |     |     |     |
| --- | --- | --- | ------ | --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
𝑖 𝑗 𝑗 𝑗𝑖 𝑖 𝛼 fo r B M 2 5 , h y p e r - p a ra m et e r 𝛽 for B M 2 5 F .
|     |     |     |     | 𝑑   |     | 𝑑   |     |     |         |                                              |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | -------------------------------------------- | --- | --- | --- | --- |
|     |     |     |     |     |     |     |     |     | Output: | Thecosinesimilarity𝑠ofthisquerydocumentpair; |     |     |     |     |
where𝑞 and𝑘 sharethesameshapeandonlydifferinrandom /*Generatinginputfeaturesforalltokens,𝑊 iswordset,𝑤 is
initialization.Symmetrically,theweightedattentionscoreof𝐴 word,𝑡 istoken,𝑆issegmentIdset*/
𝑗𝑖
canberepresentedintherightpartofEq.2.TherightpartofFigure
|     |     |     |     |     |     |     |     |     | 1:  | for𝑤 𝑖 ∈𝑊 | do  |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | --- | --- |
1presentshowWeightedSelf-Attentionworks.Withimportingthe
|                                 |     |     |     |     |                        |     |     |     | 2:  | for𝑡 𝑗 | ∈𝑤 𝑖 do   |     |     |     |
| ------------------------------- | --- | --- | --- | --- | ---------------------- | --- | --- | --- | --- | ------ | --------- | --- | --- | --- |
| weightinformationandpackingall𝑤 |     |     |     |     | into𝑊,weformallydefine |     |     |     |     |        |           |     |     |     |
|                                 |     |     |     |     | 𝑖                      |     |     |     | 3:  | 𝑖𝑑𝑓    | =𝑉 𝑤(𝑤 𝑖) |     |     |     |
𝑗
| GlobalWeightedSelf-Attention(GWSA)as |     |                                 |     |           |     |     |     |     |     | 𝑡𝑓        | =𝑡𝑓(𝑤 𝑖) |     |     |     |
| ------------------------------------ | --- | ------------------------------- | --- | --------- | --- | --- | --- | --- | --- | --------- | -------- | --- | --- | --- |
|                                      |     |                                 |     |           |     |     |     |     | 4:  | 𝑗         |          |     |     |     |
|                                      |     |                                 |     |           |     |     |     |     |     | 𝑡𝑜𝑘𝑒𝑛𝐼𝑑   | =𝑉 𝑡(𝑡   |     |     |     |
|                                      |     | WeightedSelfAttention(𝑄,𝐾,𝑊,𝑉)= |     |           |     |     |     |     | 5:  |           | 𝑗 𝑗)     |     |     |     |
|                                      |     |                                 |     |           |     |     |     |     | 6:  | 𝑠𝑒𝑔𝑚𝑒𝑛𝑡𝐼𝑑 | 𝑗 =𝑆(𝑡   | 𝑗)  |     |     |
|                                      |     |                                 |     |           |     | 𝑄𝐾𝑇 |     | (3) |     |           |          |     |     |     |
|                                      |     |                                 |     | softmax(𝑊 |     | )𝑉  |     |     | 7:  | endfor    |          |     |     |     |
⊙ √
|     |     |     |     |     |     | 𝑑   |     |     | 8:  | endfor |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- |
/*GeneratingEncodedVectorfor𝑑and𝑞*/
where𝑊 isonedimensionvectoranditsmultiplicandisamatrix
|     |     |     |     |     |     |     |     |     |     | 𝑣 =𝐺𝐿𝑂𝑊𝐸𝑛𝑐𝑜𝑑𝑒𝑟𝑞 |     | (𝑞,𝑖𝑑𝑓 ,𝑡𝑓 | ,𝑡𝑜𝑘𝑒𝑛𝐼𝑑 |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ---------- | -------- | --- |
. ⊙ represents a Hadamard product by repeating𝑊 to perform 9: 𝑞 𝑞 𝑞 𝑞)
=𝐺𝐿𝑂𝑊𝐸𝑛𝑐𝑜𝑑𝑒𝑟𝑑
element-wisemultiplication.Eq4explainsthisspecialoperation. 10: 𝑣 (𝑑,𝑖𝑑𝑓 ,𝑡𝑓 ,𝑡𝑜𝑘𝑒𝑛𝐼𝑑 ,𝑓𝑖𝑒𝑙𝑑𝐼𝑑 𝑑)
|     |     |     |     |     |     |     |     |     |     | 𝑑           |       | 𝑑   | 𝑑 𝑑 |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----- | --- | --- | --- |
|     |     |     |     |     |     |     |     |     | 11: | 𝑠 =𝑐𝑜𝑠𝑖𝑛𝑒(𝑣 | ,𝑣 𝑑) |     |     |     |
𝑞
|     |     |       |      | 𝑤              | ·𝑎   | ··· 𝑤 | ·𝑎 1𝑛         |     |     |     |     |     |     |     |
| --- | --- | ----- | ---- | -------------- | ---- | ----- | ------------- | --- | --- | --- | --- | --- | --- | --- |
|     |     |       |      |                | 1 11 | 1     |               |     |     |     |     |     |     |     |
|     |     |       |      | (cid:169)      | .    | ...   | . (cid:170)   |     |     |     |     |     |     |     |
|     | 𝑊   | ⊙𝐴=(𝑤 | 𝑖 ·𝑎 | 𝑖𝑗)= (cid:173) | . .  |       | . . (cid:174) | (4) |     |     |     |     |     |     |
|     |     |       |      | (cid:173)      |      |       | (cid:174)     |     |     |     |     |     |     |     |
|     |     |       |      | 𝑤 𝑚·𝑎          |      | 𝑤 𝑚·𝑎 |               |     |     |     |     |     |     |     |
|     |     |       |      |                | 𝑚1   | ···   | 𝑚𝑛            |     |     |     |     |     |     |     |
(cid:171) (cid:172) areemployedtofacilitatetherobustnessofGLOWEncoder.
| 3.4 | GLOWEncoder |     |     |     |     |     |     |     |     |     |     | ,...,WSAn | )𝑊𝑜 |     |
| --- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --- |
CWSA=Concat(WSA1
G L O W En co d e r p i ck s th is W e i gh t e d S e l f -A t te n t io n a s i t s b lo c k u n it . CWSAout=LayerNorm(CWSA+X)
(5)
| It  | is a lso | bu il t u p | o n m u | lt i- he a d s | t ru c t u r e b | y c o n c at e | n a t in g s | e v e ra l |     |     |     |     |     |     |
| --- | -------- | ----------- | ------- | -------------- | ---------------- | -------------- | ------------ | ---------- | --- | --- | --- | --- | --- | --- |
WeightedSelf-Attentioninstances.Withre-scalingby𝑊𝑜,wecan GLOWEncoder=
|     |     |     |     |     |     |     |     |     |     | LayerNorm(CWSAout |     | +FeedForward(CWSAout |     | ))  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | -------------------- | --- | --- |
getaComplexWeightedSelf-Attention(CWSA).Afullyconnected
Feed-Forwardnetworkisthenfollowedastheothersub-layer.In
bothsub-layers,layernormalization[3]andresidualconnection[10] WeformulatethewholeencodinglogicinAlgorithm1.

GLOW:GlobalWeightedSelf-AttentionNetworkforWebSearch Woodstock’18,June03–05,2018,Woodstock,NY
Document: https://www.alimentation-boisson-portugaise.ch/
|     | Title |     | Anchor |     | URL |     | Clicked Query |     |
| --- | ----- | --- | ------ | --- | --- | --- | ------------- | --- |
https www
cave cristalepic ##erieet  www alimentation  cave cristal##l cave cristal
| [CLS] |     | [SEP] |     | [SEP] | alimentation bois  | [SEP] |     |     |
| ----- | --- | ----- | --- | ----- | ------------------ | ----- | --- | --- |
cave portugais##e aai  bois ##son portugais  ai ##glecave cristal
|     | ##gle |     | ##e ch | ##son portugais ##e  |     |     | produitsportugaisdis   |     |
| --- | ----- | --- | ------ | -------------------- | --- | --- | ---------------------- | --- |
|     |       |     |        |                      | ch  |     | ##tri ##but ##eurgene  |     |
##vecristal
|     | Field 0 |     | Field 1 |     | Field 2 |     |     | Field 3 |
| --- | ------- | --- | ------- | --- | ------- | --- | --- | ------- |
Figure3:Combinedfieldsrepresentation
3.5 GlobalWeightGeneration where 𝑓𝑤 is the weight of field𝑐; 𝑓𝑙𝑛 is the normalized field
|                                                    |     |     |     |                    | 𝑐                          |     | 𝑐   |               |
| -------------------------------------------------- | --- | --- | --- | ------------------ | -------------------------- | --- | --- | ------------- |
|                                                    |     |     |     | lengthforfield𝑐;𝑡𝑓 | 𝑐 isthetermfrequencyof𝑤𝑜𝑟𝑑 |     |     | withinfield𝑐; |
| AkeypointofGLOWistofindanappropriatewaytorepresent |     |     |     |                    | 𝑗                          |     |     | 𝑗             |
globalweight.BM25anditsvariantsshowthesuperiorityinglobal 𝑓𝑙 𝑐 istheoriginalfieldlengthoffield𝑐;𝑎𝑣𝑙 𝑐 istheaveragelength
| weightrepresentationfordocumentrankingtasksagainstother |     |     |     | forfield𝑐. |     |     |     |     |
| ------------------------------------------------------- | --- | --- | --- | ---------- | --- | --- | --- | --- |
𝑎𝑡𝑓
a lt e rn a t iv es . W e l ev e r a g e B M 2 5 t o g e n e r a te th e g l o b a l w e ig h t s co r e s 𝑤𝐵 𝑀25𝐹 𝑗
=𝑖𝑑𝑓 𝑗 (8)
|     |     |     |     |     | 𝑗   |     | 𝑘 +𝑎 𝑡𝑓 |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- |
fo r a q u e ry a n d B M 2 5 F [ 3 3 ] to c o m p u t e t h e w ei g h t s c o r es f o r a m u l ti - 1 𝑗
AnditscorrespondinginherentBM25FscoreiscomputedinEq.8,
fieldsdocument.BM25FisamodificationofBM25inwhichthe
documentisconsideredtobecomposedfromseveralfieldswith wherethecalculationof𝑖𝑑𝑓 𝑗 isthesamewith𝑖𝑑𝑓 𝑖 .
differentdegreesofimportanceintermofrelevancesaturationand
lengthnormalization.BothBM25andBM25Fdependon𝑡𝑓 and𝑖𝑑𝑓, 3.6 WholeWordWeightSharing
𝑡𝑓 meansTermFrequency,itdescribesthenumberofoccurrences Sub-wordbasedapproachhasbeenprovedefficienttoalleviateout
of the word in the field. While𝑖𝑑𝑓 (InverseDocFrequency) is a ofvocabularyissueandlimitvocabularysize.BERTusesWordPiece
measureofhowmuchinformationthewordprovides,i.e.,ifit’s toproducetokensfromoriginalrawtext.Oneshortcomingofthis
common or rare across all documents. It is the logarithmically methodologyisthatwecannotdirectlyapplytheword-levelprior
scaledinversefractionofthedocumentsthatcontaintheword.For knowledge.Moreover,insomeNLPtasks,token-levelweightis
|     | 𝑁 − 𝑑 𝑓 + 0 . 5 |     | 1i  |     |     |     |     |     |
| --- | --------------- | --- | --- | --- | --- | --- | --- | --- |
w o r d 𝑖 , 𝑖𝑑 𝑓 𝑖 = lo g 𝑖 , w h er e 𝑁 i s a s c al ar n d ic ti n g h o w n o t e n o u gh t o d is t i n g ui s h th e i m p o rt a n c e o f d i ff er en t w o r ds . T h e
𝑑 𝑓 𝑖 + 0 . 5
m a n y d o cu m en ts w e a r e s e r v in g in s ys t e m a n d 𝑑𝑓 i s th e n u m b e r la te s t B E R T m o d e l h a s p r ov e d t ha t u p g r a di n g t h e M a sk L a n g u a g e
ofdocumentswheretheword𝑖appears. Modeltasktowholewordlevel2 improvesperformance.Inour
|     |     |     |     | task,the𝑊 | usedforattentionscoreisalsobasedonwholeword |     |     |     |
| --- | --- | --- | --- | --------- | ------------------------------------------- | --- | --- | --- |
InherentQueryBM25. ThecalculationofclassicBM25isbased weights.Thatis,wefirstcollectandcalculateweightsinwhole
on𝑡𝑓 inadocument.SinceinGLOWqueriesanddocumentsare
wordlevel,thengivethesamewordweighttotokenscorresponding
encodedseparately,herewecomputeaninherentqueryBM25by
tooneword.Bythisway,oneWordPiecetokenmayhasdifferent
| computing𝑡𝑓 | withinaqueryinstead.AninherentBM25term |     |     |     |     |     |     |     |
| ----------- | -------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
weightrepresentationifitoccupiesindifferentwords.Wealso
weightforqueryword𝑖canbere-calculatedas conductexperimentinAnalysissectiontocomparetheeffectof
token-levelweightgenerationandword-level.Theresultssuggest
𝑡𝑓 𝑖
|     | 𝑤 𝐵𝑀25=𝑖𝑑𝑓 |         | (6) | theword-levelmannerissuperiorthantoken-level. |     |     |     |     |
| --- | ---------- | ------- | --- | --------------------------------------------- | --- | --- | --- | --- |
|     | 𝑖 𝑖        | 𝑙       |     |                                               |     |     |     |     |
|     | 𝑡𝑓 +𝑘      | (1− 𝑏+𝑏 | 𝑞 ) |                                               |     |     |     |     |
𝑖 1 𝑎 𝑣 𝑙𝑞
3.7 CombinedFieldsRepresentation
| where𝑡𝑓 𝑖 isthetermfrequencyof𝑤𝑜𝑟𝑑 |     | 𝑖 withinquery;𝑙 | 𝑞 isthe |     |     |     |     |     |
| ---------------------------------- | --- | --------------- | ------- | --- | --- | --- | --- | --- |
Inad-hocretrievaltasks,therearealwaysmultiplesourcesoftex-
| querylength;𝑎𝑣𝑙 | isthequeryaveragelengthamongallqueries |     |     |     |     |     |     |     |
| --------------- | -------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
𝑞
inthetrainingset;𝑘 isafreeparameterusuallychosenas2and tualdescription(fields)correspondingtoonedocument.Lotsof
1
0<=𝑏<=1(commonlyusedis0.75). studies[32,43]revealthatdifferentfieldscontaincomplementary
information.Thus,toobtainamorecomprehensiveunderstanding
InherentDocumentBM25F. InBM25F,insteadofusing𝑡𝑓 directly, ofdocument,whenencodingthedocumentintosemanticvector
empirically𝑎𝑡𝑓 (AdjustedTermFrequency) is widely adopted. It space,weneedtotakemultiplefieldsintoconsideration.
| isproposedbyaddingseveralfield-wisefactors.Fora𝑤𝑜𝑟𝑑 |     |     | in  |                                                     |     |     |     |     |
| --------------------------------------------------- | --- | --- | --- | --------------------------------------------------- | --- | --- | --- | --- |
|                                                     |     |     | 𝑗   | Thewell-knownfieldsforadocumentinwebsearcharetitle, |     |     |     |     |
documentfield𝑐,its𝑎𝑡𝑓𝑐
isdefinedinEq.7 header, keyword, body, and the URL itself etc. These fields are
𝑗
primitivefromthewebsiteandcanbefetchedfromHTMLtags.
𝑓 𝑤 ·𝑡 𝑓 𝑐
𝑐 𝑗 A n o th e r k i n d o f fi e l d s , l i k e a n c h o r, l e v e r a g e t h e de s c r i p t i o n f r o m t h e
|     | 𝑎𝑡𝑓 𝑐 = |     | (7) |     |     |     |     |     |
| --- | ------- | --- | --- | --- | --- | --- | --- | --- |
𝑗 𝑓 𝑙 b r o th e r w e b s i t e . V i a t h i s w a y , w e c a n i n f e r w i t h u s e f u l i n f o r m a ti o n
|     | 1.0+𝑓𝑙 | 𝑛 𝑐 ·( 𝑐 −1.0) |     |     |     |     |     |     |
| --- | ------ | -------------- | --- | --- | --- | --- | --- | --- |
𝑎 𝑣 𝑙 𝑐
|     |     |     |     | fr o m o t h | e r d o c u m e n t s . | In a d d it i o n | t o t h i s , c l i c | k s i g n a l i s a l s o w i th |
| --- | --- | --- | --- | ------------ | ----------------------- | ----------------- | --------------------- | -------------------------------- |
1Herewesetitby100,000,000 2https://github.com/google-research/bert

Woodstock’18,June03–05,2018,Woodstock,NY Shan,etal.
highqualityandcanbeeasilyparsedfromthesearchlog.When RQ4 DoesGLOWincreasemodelcomplexityandisiteasierto
auserclickedonthedocumentdwithaqueryq,wewilladdqto convergetotrainingdata?
theclickedqueryfieldofd.
Thespecialpropertiesofthesedocumentfieldsmakeitdifficult 4.1 EvaluationDatasets
tounifythemintoonesemanticspace.Onecommonapproach[43] WeevaluatetheperformanceofGLOWonMSMARCO3andBing’s
istoseparatelyencodethemultiplefieldsrespectivelyandlearna large scale data points. Table 1 illustrates the properties of the
jointlossacrossthesefields.Otheralternativesunifyallfieldsby trainingdatawiththesetwodatasets,itcanbeobservedthatthe
simplyconcatenatingallthesefieldswithspaces. number of queries and documents in MS MARCO are within a
AsshowninFigure3wetranslatethesegmentdefinitionof prettylowerscale,onlythreehundredthousandqueriesandthree
pre-nextsentenceinBERTtodifferentfieldsindocumentbymap- milliondocuments.Itishardtoidentifythedeepmatchingmodel’s
pingmultiplefieldsintodifferentsegments.Fieldembeddingsare qualityforindustrialwebsearchengineswithsolelymeasurement
introducedtodifferentiatefields.Everyfieldhasamaxlengthcon- onMSMARCO.Thusweexpandthedatascalebycollectingmore
strain,wesetitto20tokensforanchor,URLandtitlefields.For trainingdatafromBing’ssearchlogs.IntheBing’sinternaldata
clickedquery fields,sinceapopulardocumentmayexistalarge points,wescaleupthequerycountsto30millionanddocumentsto
magnitudeofclickinstances,weonlypickthetop5clickedqueries 140million.What’smore,wealsoaddclickedqueriesastheextra
foronedocumentwithamaxlengthof68tokens.Forallthese fieldintheinternalset.
fields,wepadthemaccordingtotheneed.Toobtainanunified
documentembedding,a[CLS]tokenisaddedatthebeginningof Table1:Statisticsofdatasetsusedinourexperiments.We
thecombinedfields,anda[SEP]tokenisalsoinsertedbetween usethedevelopmentsetofMSMARCOtoevaluatemodel
eachfieldtodistinguishdifferentfields. performance.
3.8 ObjectiveOptimization Dataset MSMARCO Intrinsicdataset
WecanachieveasequenceofsemanticembeddingsafterGLOW
Train 367kqueries,36mq-dpairs 30mqueries,310mq-dpairs
Encoder.Inspiredby[8],usingtheembeddingof[CLS]inthelast
Dev 5kqueries,3mdocuments 14kqueries,70mdocuments
layerasthematchingfeaturesisalreadygoodenough.Nogueiraet
al.[23]alsoprovedthatinpassagerankingtask,addingmorecom- Fields url,title,body anchor,title,url,clickedquery
ponentsuponTransformerdoesnothelptoomuch[28].Therefore,
GLOWusestheembeddingof[CLS]asthesemanticrepresentation
forthequeryanddocument,thematchingscore𝑠ismeasuredby 4.1.1 MSMARCO. ThedocumentfullrankingtaskinMSMARCO
cosinesimilarityonthequeryanddocumentvectors. issimilarwithourscenarioasthedocumentcontainsmultifields
withtitleandbody.Basedonourpractice,thedocumentURLcan
𝑠 =cos(GLOW(query)last,GLOW(document)last) (9) providetopicalinformation,sowetokenizetherawURLintolex-
cls cls
icalrepresentationasonemorefield.Inthistask,trainingdata
Weadoptabinarycrossentropylosstooptimizethemodel,which
contains6millionquery-documentpairswithasimplebinaryposi-
determineswhetheraquery-documentpairisrelevantornot.We
tive/negativelabelingwhiledevelopmentsetincludes5kqueries
alsotriedpair-wiselossandfoundithadnoextraimprovement.
and3milliondocuments.Foreachqueryinevaluationset,were-
Priorworks[23,28]alsoconfirmonthis.
trievetop20documentswiththehighestsimilarityscoresforMRR
𝐿𝑜𝑠𝑠 =−𝑦log(𝛿(w·s+b))−(1−y)log(1−𝛿(w·s+b)) (10) calculation.
where𝑦 is the label denoting if query-document is relevant, 𝛿 4.1.2 InstrinsicBing’slargescaledataset. Similarwith[13,22]we
representsSigmoidfunction.𝑤and𝑏areusedtogenerateweighted sample30millionrealuserqueriesandfromrealsearchengine
cosinesimilaritytofittheSigmoidfunction. logs.Forthe𝑡𝑟𝑎𝑖𝑛𝑖𝑛𝑔step,foreachquery,wetreatitstop5clicked
documentsaspositives.Bythiswayweobtain150millionquery-
4 EXPERIMENTS documentpairspositivetrainingexamples.Forthenegatives,we
TodemonstratewhetherandhowourproposedGLOWframework useamixturerandomsamplingapproachcombiningNCEnega-
canachieveperformanceimprovementsinthefirst-stageretrieval, tivesamplingandHardnegativeintegration,whicharedetailed
weconductcomprehensivesuiteofexperimentsbasedonpublic describedbelow.Thesetwomethodsconsolidatetheremaining160
datasetandrealworldsearchenginedatasetincludingofflineex- millionnegativequery-documentpairs.
periments,ablationstudyaswellascasestudies.Specifically,we NCEnegativesampling Directlyrandompickinganegativecase
breakdowntheprincipalresearchquestionsintofourindividual istooeasyforthemodeltolearn,whichweakensthemodel’sgener-
onestoguideourexperimentation. alization.Instead,weusethenoise-contrastiveestimation(NCE)to
pickcompetitivenegatives[21,44].Italwayspicksnegativeswithin
RQ1 CanGLOWimprovedocuments’qualitycomparingwiththe
currenttrainingbatchwiththesamesizeofpositives.
state-of-the-artretrievalmodels?
RQ2 HowdoeseachcomponentofGLOWcontributetoitsgen- Hardnegativeintegration ThenegativesfromNCEsampling
eralperformance? areallclickeddocuments,whichonlyhelpsthemodeltolearnentire
RQ3 IsGLOWbetterthanBERTtocapturethetopicalandthe- 3ThesourcecodeofourmeasurementonMSMARCOisavailableathttps://github.
maticrepresentationofthedocument? com/GLOW-deep/GLOW

GLOW:GlobalWeightedSelf-AttentionNetworkforWebSearch Woodstock’18,June03–05,2018,Woodstock,NY
non-relatedquery-documentpairs.Tofacilitatemodelwiththeca- vectorswhileC-DSSMusesaconvolutional-poolingstructureover
pabilitytodistinguishpartial-relatedquery-documentpairs,wein- wordsequencestolearnlow-dimensionalvectorrepresentations
corporatemoredifficultnegativesbysampling50thousandqueries forsearchqueriesandWebdocuments.
fromthesearchlogandthensendingthesequeriestotheproduc- Pre-trainlanguagemodels. Whensteppingintolanguagemodel
tionsystemtoretrieve10millionpartial-relatedquery-document pre-trainingboom,Transformer-basedmodelhasdominatedthe
pairsasthehardnegativesforthesequeries.Thesecasesareadded documentrankingtasks.SoweadoptBERTasonerepresentative
ascompanionsofNCEnegatives. baselineofthisgroup.XL-Net[41],ageneralizedautoregressive
Theintrinsicevaluationsareperformedinacommonusedway[1] pretrainingmethod,claimsitachievesthestate-of-the-artondocu-
toevaluatethequalityofsemanticembeddingrepresentation.We mentrankingtask,weadditasthecompanionbaselinewithBERT.
pick14krepresentativequeriesand70milliondocumentscandi- WealsoreferprominentmodelsinTRECdeeplearningtrack4,such
datesfromthesearchlogsasthedevelopmentset. Eachquery- asDeepCT[7]andDoc2query[25]astheremainingbaselines.The
documentishumanlabelledwithfivestandardcategoriesininfor- BERT+DeepCTbaselinereplacestheBERTcomponentinDeepCT
mationretrieval(Perfect,Excellent,Good,Fair,Bad). with context-independent word embeddings. For a target docu-
ment,Doc2querypredictsaquery,whichcanbetreatedasanother
4.2 ExperimentalSetup newfieldtothedocument,hencetheBERT+Doc2querybaseline
4.2.1 Evaluationmetric. Toevaluatetheeffectivenessofthemeth- stilltakesBERTasbasemodelwithaddingonemorenewfield
odsonMSMARCO,weuseitsofficialmetric,MeanReciprocal generatedbyDoc2queryforalldatasets.
Rank(MRR) of the top-10 and 20 documents. MRR is a statistic
measureforevaluatinganyprocessthatproducesalistofpossible 4.2.3 Trainingimplementation. Tobetteraccommodateindustrial
responsestoasampleofqueries,orderedbyprobabilityofcor- websearchengine’sdemands,takingefficiencyandscalabilityinto
rectness.FortheBing’slargescaledataset,weadoptNormalized consideration,alsotomakeafaircomparison,weapplyaSiamese
DiscountedCumulativeGain(NDCG)[14],andreporttheresultsat frameworkwith3-layerconfigurationforallaforementioneddeep
position1,3and10.Sincewearefocusingonthefirststageretrieval learningbasedbenchmarks.AllmodelsareimplementedusingTen-
inindustrialwebsearch,basedonourexperiences,NormalizedCu- sorFlow5.WetrainGLOWwith8TeslaV100GPU,32GBmemory
mulativeGain(NCG)isanotheralternativetomeasurethematching foreach.Tobestacceleratetraining,Weimplementadataparallel
documents’quality.UnlikeNDCG,NCGconsidersmoreaboutthe trainingpipelinebaseonhorovoddistributetraining.What’smore,
numberofrelevantdocumentsgotreturnedwithoutcaringthe AutomaticMixedPrecisionisenabledtotrainwithhalfprecision
positionbecausethesecondrankingstageismoreresponsiblefor whilemaintainingthenetworkaccuracy.Finally,thetrainingbatch
thefinalrankingpositions.NCGiscomputedas sizeis500query-documentpairs.Adamoptimizer[16]isemployed
totrainourmodel.Thelearningrateweusedis8e-5.Wesetthe
𝐶𝐺
NCG= (11) batchsizeto300.Otherhyber-parametersarethesamewithBERT.
𝑖𝐶𝐺
Allofthesecompetitormodelsaretrainedbyfollowingbestprac-
whereCumulativeGain(CG)isthesumofalltherelevancescores
tisessuggestedinpreviousworks.Theyareevaluatedstrictlythe
intherankingset.
samewithGLOWbyaveragingtheresultscollectedfrom5times
𝑛 repeatedtrainingsteps.
∑︁
CumulativeGain(CG)= 𝑟𝑒𝑙𝑒𝑣𝑎𝑛𝑐𝑒 𝑖 (12)
𝑖=1
4.3 RetrievalQualityResults(RQ1)
andidealCumulativeGain(iCG)isthesumofidealdocumentsets’
CG. ToanswerRQ1,wecomparetheretrivalperformanceGLOWwith
aforementionedbaselinesonMSMARCOandBing’slargescale
4.2.2 Baselines. AsmentionedinSection2,ourbaselinescontain datapoints.TheevaluationresultsarelistedinTable2.
classicinformationretrievalmatchingmethods,typicaldeeplearn-
MS MARCO results It can be observed from the left part of
ingmodelsforsentenceencoding,advancedpre-trainlanguage
Table2,(1):GLOWshowsthebestperformancesonthisdataset,it
modelsandmostrecentvitalbenchmarksondocumentranking.
significantlybeatsBERTbyalargemarginof7.3.%atMRR@10and
Classicretrievalmethods. Giventheirdeservedreputationsin 15.9.%atMRR@20.(2):Whenincreasingtheretrievalcountfrom
informationretrievalhistory,wechooseTF-IDFandBM25asrepre- 10to20,GLOWperformsmuchbetteratMRR@20thanMRR@10.
sentativesoftheclassicmethods.TF-IDFisanumericalstatistics This trend indicates GLOW performing well when we want to
that,byscoringthewordsinatext,indicateshowimportantaword fetchmoreidealdocuments.(3):EvenconsideringBERT+DeepCT
isinadocumentconsideringthecorpusthatdocumentbelongsto. andBERT+Doc2query,GLOWisalsosuperiortothemacrossall
WhileBM25isabag-of-wordsretrievalfunctionthatranksasetof metrics.ThisresultindicatesthatthemannerGLOWperformedwith
documentsbasedonthequerytermsappearingineachdocument, fusingglobalinformationintoTransformeriseffectiveforthefirst-
regardlessoftheirproximitywithinthedocument. stageretrieval.
Deepsemanticmodels. Manyprimitivedeeplearningstudiesex-
ploredhowtoencodesentencesintosemanticembeddings.Among
them,theUniversalSentenceEncoder[6](USE)andC-DSSM[34]are
widelyrecognisedtobemoreefficientandaccurate.Theformer
4https://microsoft.github.io/TREC-2020-Deep-Learning/
oneleveragestransferlearningtoencodesentencesintoembedding 5http://tensorflow.org/

Woodstock’18,June03–05,2018,Woodstock,NY Shan,etal.
Table2:ComparisonofdifferentdeepmatchingmodelsoverMSMARCOdatasetandBing’sinternaldatapoints.Fullranking
taskispickedforMSMARCOdatasetandDevsetresultsarereported.XL-Net,BERT,BERT+DeepCT,BERT+Doc2queryand
GLOWarealltrainedwith3-layersSiamesearchitecture.Theboldnumbersindictthebestresultamongothercompetitors
andthesuperscript*denotessignificantimprovementsoveralltheothermodels.
| Model |     | MSMARCO(Dev)  |               | BingLargeScaleQuerySet |        |        |        |
| ----- | --- | ------------- | ------------- | ---------------------- | ------ | ------ | ------ |
|       |     | MRR@10 MRR@20 | NDCG@1 NDCG@3 | NDCG@10                | NCG@10 | NCG@20 | NCG@50 |
|       |     | 0.1835 0.1917 | 0.1828 0.2586 | 0.3062                 | 0.3748 | 0.4561 | 0.6274 |
TF-IDF
| BM25 |     | 0.2068 0.2141 | 0.2061 0.2946 | 0.3472 | 0.4072 | 0.4889 | 0.6574 |
| ---- | --- | ------------- | ------------- | ------ | ------ | ------ | ------ |
| USE  |     | 0.0627 0.0648 | 0.0860 0.1003 | 0.1171 | 0.3548 | 0.4215 | 0.6045 |
C-DSSM 0.1461 0.1506 0.1900 0.2680 0.3113 0.3845 0.4541 0.6345
XL-Net 0.2597 0.2659 0.2528 0.3515 0.4017 0.4217 0.4947 0.6541
|      |           | 0.2624 0.2677 | 0.3346 0.4567 | 0.5154 | 0.4255 | 0.5054 | 0.6574 |
| ---- | --------- | ------------- | ------------- | ------ | ------ | ------ | ------ |
| BERT | Fine Tune |               |               |        |        |        |        |
|      |           | 0.2677 0.2725 | 0.3364 0.4598 | 0.5275 | 0.4425 | 0.5147 | 0.6748 |
BERT+DeepCT
|                |     | 0.2697 0.2802 | 0.3404 0.4621 | 0.5298 |        | 0.5172 | 0.6799 |
| -------------- | --- | ------------- | ------------- | ------ | ------ | ------ | ------ |
| BERT+Doc2query |     |               |               |        | 0.4574 |        |        |
|                |     |               | *             | * *    |        |        | *      |
| GLOW           |     | 0.2816 0.3104 | 0.3461 0.4772 | 0.5443 | 0.4562 | 0.5284 | 0.7015 |
Table 3: Ablation evaluation comparison of GLOW vari- comparetheNCGandNDCGresultswithBERTandGLOWfullim-
ants with BERT and GLOW on Bing’s large scale dataset. plementationontheBing’sinternaldataset.Eachvariationdisables
GLOW𝑖𝑑𝑓 means using inverse document frequency as acomponentwhilekeepsothersunchanged.Theresultsreported
weightsource.GLOW𝑤𝑡 integratestheglobalweightsinto inTable3indicatethatallthesethreecomponentsarecriticalto
originalattentionbyasimpletrainableMLPlayer.GLOW𝑡𝑤 GLOW,missinganyoneofthemwoulddegradetheperformance
indicatesgeneratingtokenlevelweightforqueryanddocu- ofGLOW.Detailedanalysesaredescribedasfollows.
ment.GLOW𝑢𝑠usesanunionfieldrepresentationbysetting
alltokens’fieldembeddingsasthesame.
|     |     |     |     | 4.4.1 Howtorepresentandintegrateglobalweight? |     |     | Therearemany |
| --- | --- | --- | --- | --------------------------------------------- | --- | --- | ------------ |
alternativestoEq.3toserveasweight.Oneofcommonusedonesin
Variant NDCG@1 NDCG@3 NDCG@10 NCG@10 NCG@20 NCG@50 IRcommunityisinversedocumentfrequency(idf),itstandsforthe
BERT 0.3346 0.4567 0.5154 0.4255 0.5054 0.6574 frequencyacrossglobaldocumentsforoneparticularword.How-
ever,idfonlyconsiderstheglobalstatisticswithouttakinglocal
| GLOW𝑖𝑑𝑓 0.3349 | 0.4587 | 0.5149 0.4397 | 0.5169 0.6551 |     |     |     |     |
| -------------- | ------ | ------------- | ------------- | --- | --- | --- | --- |
GLOW𝑤𝑡 0.3330 0.4625 0.5134 0.4269 0.5084 0.6545 contextintoconsideration.Simplyadoptingidfastheglobalweight
0.3289 0.4598 0.5146 0.4287 0.5011 0.6589 iseasytoleadweightbias.TovalidateifBM25isthebestprior
GLOW𝑡𝑤
sourceforglobalweightestimation,weexploitavariantGLOW𝑖𝑑𝑓 ,
| GLOW𝑢𝑠 0.3455 | 0.4704 | 0.5197 0.4454 | 0.5146 0.6898 |     |     |     |     |
| ------------- | ------ | ------------- | ------------- | --- | --- | --- | --- |
ituseinversedocumentfrequencyasweightsource.
| GLOW 0.3461 | 0.4772 | 0.5243 0.4502 | 0.5204 0.7015 |     |     |     |     |
| ----------- | ------ | ------------- | ------------- | --- | --- | --- | --- |
GLOWcombinestheglobalweightwithoriginalattentionwith
themultiplication.Tovalidateifthemultiplicationisthebestalter-
Intrinsicevaluationresults LookattherightpartofTable2,(1): nativetocombinethesetwodifferentweights,wedesignGLOW𝑤𝑡 ,
SimilarwithresultsofMSMARCO,GLOWoutperformsallbench- itintegratestheglobalweightsintooriginalattentionbyasimple
marksinmetricsofNDCG@1,3,10andNCG@10,50andsignifi- trainableMLPlayerandoutputsthefinalattention.
cantlygainsinNDCG@3,10andNCG@50forthisintrinsicdataset. ComparingtheBERT,GLOW𝑖𝑑𝑓 ,GLOW𝑤𝑡 andGLOWresultsinTable
(2)WeseeBERT+Doc2queryaccountsforthebestresultinNCG@10 3,GLOW 𝑖𝑑𝑓 onlyperformsslightbetterthanBERTonNCG@10
butveryclosewithGLOW,alwaysbetterthanBERT+DeepCTaccross andNCG@20,butnearlynochangeonNCG@50.AmongallNDCG
allmetrics.Thisreflectsthatcapturingdocuments’topicalwords measurements,GLOW showstheflattrend.Besides,GLOW ’s
𝑖𝑑𝑓 𝑤𝑡
mightbemoreusefulthatassigningtermweightingforqueriesin resultsareverycloseresultswithBERTonNCGandNDCG,largely
industriallargescaledocumentretrieval. dropcomparingwithGLOW.Thisindicatestherepresentationand
TheevaluationsonMSMARCOandBing’slargescaledataset integrationofglobalweightiscrucialforGLOW,usingimproper
revealthatGLOWcannotonlyaddresstherealencodingproblem weightrepresentationorotherintegrationmannerscoulddegrade
forindustrialsearchengine,butalsoextendstobeageneralsolver themodelperformance.
forordinarydocumentmatchingtaskinIRcommunity.
|     |     |     |     | 4.4.2 Wholewordlevelweight𝑣𝑠 |     | tokenlevel. | Toverifythefunc- |
| --- | --- | --- | --- | ---------------------------- | --- | ----------- | ---------------- |
4.4 AblationStudy(RQ2) tionalityofwholewordweightsharingweproposed,wedesign
TostudyRQ2,asaforementioned,threekeycomponentsempower ,itremovesthewholewordweightsharingbyastraightfor-
GLOW𝑡𝑤
theembeddingqualityofGLOW.Tofurtherinvestigatetheindivid- wardtokenlevelweightgeneration,whichgeneratesbothquery
ualcontributionofeachpart,weexaminethreeGLOWvariantsand anddocumentBM25scoresonWordPiecetokenlevel.

GLOW:GlobalWeightedSelf-AttentionNetworkforWebSearch Woodstock’18,June03–05,2018,Woodstock,NY
Table4:Top5wordswithhighestattentionscoresfromdocumentbetweenBERTandGLOW,theyareselectedfromUrland
Titlefields.WefetchUrlfieldbytokenizationfromrawweburl.Thegreenboldwordsinthetableindicatethetopicalwords
whiletheredboldonesareofftopic.
Document Field FieldContent BERTtop5wordswithhighest GLOW top 5 words with
|     |     |     |     |     | attention |     | highestattention |     |     |
| --- | --- | --- | --- | --- | --------- | --- | ---------------- | --- | --- |
Doc1 Title Top30Doctorinsightson:CanLowSodiumLevelsCauseSeizures insights low healthtap sodium healthetap
|     |     |     |     |     | level | cause | seizureslow |     | insights |
| --- | --- | --- | --- | --- | ----- | ----- | ----------- | --- | -------- |
Url httpswwwhealthtapcomtopicscanlowsodiumlevelscauseseizures
Doc2 Title PoliceorSheriff’sPatrolOfficerSalary payscale research policepa- payscale sheriff 27s pa-
troofficer
trol salary
Url httpswwwpayscalecomresearchusjobpoliceorsheriff27spatrolofficer
salary
Title Inpictures:InsideHangSonDoong,theworld’slargestcavesinVietnam pictures caves
| Doc3 |     |     |     |     |              | 10914205earth |         | hangsondoong |     |
| ---- | --- | --- | --- | --- | ------------ | ------------- | ------- | ------------ | --- |
|      |     |     |     |     | largestcases |               | largest |              |     |
Url httpswwwtelegraphcouknewspicturegalleriesearth10914205inpictures
insidehangsondoongtheworldslargestcavesinvietnamhtml
FromTable3,thereisnearlynoimprovementbetweenGLOW𝑡𝑤 failedtoemphasize"HangSonDoong”,whichisvitaltodescribethe
andBERTonallmetrics,thisprovescomputingBM25onsub-word topicofthisdocument.ButGLOWsuccessfullyenhance"HangSon
tokenlevelisnotfeasible.Thatisthereasonwhytraditionalsearch Doong“’sattention.Itisalsoexplainablesince"HangSonDoong”
enginealwaysuseBM25scoreonnaturalwordlevel. areallrarewords,theirglobalweightsareprettyhigherthanother
|     |     |                               |     | words, in                         | addition, | they repeat | twice in | this document | so their |
| --- | --- | ----------------------------- | --- | --------------------------------- | --------- | ----------- | -------- | ------------- | -------- |
|     |     | Thetokenlevelrepresentationof |     | BM25valuearehigherthanotherwords. |           |             |          |               |          |
4.4.3 Isfieldembeddingamust?
GLOWconsistsof3parts:tokenembeddings,positionembeddings
andfieldembeddings.Fieldembeddingsaredesignedtodifferentiate 4.6 EfficiencyAnalysis(RQ4)
fieldsfordocument.Tovalidateiffieldembeddingsarenecessary. ThentoanswerRQ4,weevaluatetheefficiencyofGLOWfromthe
WedesignGLOW𝑢𝑠 ,whichusesanunionfieldrepresentationby pointsofviewofmodelcomplexityandtrainingcost.Thetraining
settingalltokens’fieldembeddingsasthesame.
trendrevealsGLOWiseasiertoconvergewhileretainingthesame
| outperformsBERTandGLOW𝑖𝑑𝑓 |     | andGLOW𝑡𝑤 | onmostmet- |                             |     |     |     |     |     |
| ------------------------- | --- | --------- | ---------- | --------------------------- | --- | --- | --- | --- | --- |
| GLOW𝑢𝑠                    |     |           |            | trainingparameterswithBERT. |     |     |     |     |     |
rics,butstillhaveaslightergapwithGLOWFull,whichsignifies
removingfieldembeddingswillinevitablyjeopardizetheperfor-
manceof GLOW.
|     |     |     |     | 0.200       |       |      | 0.6 |     |      |
| --- | --- | --- | --- | ----------- | ----- | ---- | --- | --- | ---- |
|     |     |     |     |             |       | BERT |     |     | BERT |
|     |     |     |     | 0.175 0.174 | 0.176 | GLOW |     |     | GLOW |
0.5
| 4.5 CaseStudy(RQ3) |     |     |     | 0.165 |     |     |     |           | 0.463                                     |
| ------------------ | --- | --- | --- | ----- | --- | --- | --- | --------- | ----------------------------------------- |
|                    |     |     |     | 0.150 |     |     |     | 0         | . 4 2 30 . 4 2 7 0 . 4 3 9 0 . 4 4 20.445 |
|                    |     |     |     |       |     |     | 0.4 | 0 . 4 0 1 | 0 . 4 1 3 0 . 4 3 1 0 . 4 2 6             |
ThedesignpurposeofGLOWistoenhancetheattentionforthose 0.125 evitisop_ytiralimis 0.3500 . 3 8 0 0 . 3 9 9
0.115
| wordshavinghigherweights.Weconductsomecasestudiesto |     |     |     | ssol  | 0 . 0 9 5 |                               |       |     |     |
| --------------------------------------------------- | --- | --- | --- | ----- | --------- | ----------------------------- | ----- | --- | --- |
|                                                     |     |     |     | 0.100 | 0 . 0 9 0 | 0 . 0 9 3 0 . 0 8 9 0 . 0 8 7 | 0 . 3 |     |     |
answerRQ3.ComparingBERTandGLOW,Table4illustratestop5 0 . 0 9 3 0 . 0 8 8 0 . 0 7 7
|     |     |     |     | 0.075 |     | 0 . 0 8 6 0 . 0 7 9 0 . 0 8 0 0 . 0 7 3 | 0.240 0.1920.197 |     |     |
| --- | --- | --- | --- | ----- | --- | --------------------------------------- | ---------------- | --- | --- |
wordswhichhavethehighestattentionscoresforeachdocument. 0 . 2
0.050
Heretheattentionscoresaregeneratedfromthelastlayer’shidden 0.1
0.025
stateoutputs,foreachtoken,wefirstlymultipleallothersbyan
|     |     |     |     | 0.000 |     |     | 0.0 |     |     |
| --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- |
innerproductandaveragethevalue,thensortalltokens’attention 0 1000 2000 30 0 0 4000 5000 6000 0 1000 2000 3000 4000 5000 6000
|     |     |     |     |     | s t ep |     |     |     | step |
| --- | --- | --- | --- | --- | ------ | --- | --- | --- | ---- |
score.Forthosewordsbelongtomultipletokens,wesumupthe
attentionscoretofetchthosewords’attention. (a)Trainingloss (b)Weightedcosinesimilarity
FromTable4,wecanobservethatGLOWismoreeffectiveto
Figure4:EfficiencycomparisonbetweenBERTandGLOW.
capturetopicalandsemanticwordsfromdocuments.Doc1triesto
|     |     |     |     | The yellow | dotted | lines represent | BERT | while | green full |
| --- | --- | --- | --- | ---------- | ------ | --------------- | ---- | ----- | ---------- |
sharetheanswertoquestion"canlowsodiumlevelscauseseizures",
linesindicateGLOW.
itisprettyclearhere"low","sodium"and"seizures"arethetopical
wordstothesedocument.GLOWsuccessfullyrankthese3words
OneoftheadvantagesforGLOWisthatit
into Top5 while BERT only rank "low" to #2. In Doc2, "sheriff" Modelcomplexity.
|             |                    |                 |                | does not | involve any | new trainable | parameters. | Thus | it retains |
| ----------- | ------------------ | --------------- | -------------- | -------- | ----------- | ------------- | ----------- | ---- | ---------- |
| cannot rank | into top 5 highest | attention words | in BERT, while |          |             |               |             |      |            |
itrankssecondpositioninGLOW.Thisdocumenthasastrong thesamemodelcomplexitywithBERT.Theonlyextraworkisto
preferenceondescribingtheofficersalaryinformationat𝑠ℎ𝑒𝑟𝑖𝑓𝑓 generateweightscoresforallwordswhichcanbewellprepared
area,weakeningthisinformationmakestheretrievalsystemharder beforemodeltrainingandinference.
togetthisdocumentbackwhenpeoplesearchesaqueryrelated Researchersalwaysexpectdeepmodelstobe
Trainingefficiency.
with"sheriffpatrol".SimilarphenomenontakesplaceatDoc3,BERT trainedasfastaspossibletoreducethetrainingcost.Asdescribed

Woodstock’18,June03–05,2018,Woodstock,NY Shan,etal.
inSec3.8,thevalueofweightedcosinesimilarityisimportantsince [13] Po-SenHuang,XiaodongHe,JianfengGao,LiDeng,AlexAcero,andLarryHeck.
itdescribesthediscriminationbetweenthequeryembeddingsand Learningdeepstructuredsemanticmodelsforwebsearchusingclickthrough
document embeddings. We plot the training loss and weighted
data. InProceedingsofthe22ndACMInternationalConferenceonInformation
KnowledgeManagement,CIKM’13,page2333–2338,NewYork,NY,USA,2013.
cosinesimilaritytrendcurveofGLOWandBERTbasedonthe AssociationforComputingMachinery.
trainingexperiencefromMSMARCO.AccordingtoFigure4a,in [14] KalervoJärvelinandJaanaKekäläinen.Cumulatedgain-basedevaluationofir
techniques.ACMTrans.Inf.Syst.,20(4):422–446,October2002.
thefirst2kstepsthetraininglossofGLOWdecreasessignificantly [15] JaeyoungKim,MostafaEl-Khamy,andJungwonLee.T-gsa:Transformerwith
fasterthanBERT.ThisindicatesthatGLOWismoreeasiertocon- gaussian-weightedself-attentionforspeechenhancement.ArXiv,abs/1910.06762,
vergeontrainingdata,whichcouldbeabigtimesavingwhenwe 2019.
[16] DiederikPKingmaandJimmyBa.Adam:Amethodforstochasticoptimization.
traindocumentrepresentationonalargescaledataset.Practically, arXivpreprintarXiv:1412.6980,2014.
wealwaysexpecttheweightedcosinesimilaritytobemoredif- [17] YinhanLiu,MyleOtt,NamanGoyal,JingfeiDu,MandarJoshi,DanqiChen,Omer
Levy,MikeLewis,LukeZettlemoyer,andVeselinStoyanov.Roberta:Arobustly
ferentiatedtopreventtheoverlapacrosspositivesandnegatives.
optimizedbertpretrainingapproach.arXivpreprintarXiv:1907.11692,2019.
Thusalargevalueofweightedcosinesimilarityispreferred.Figure [18] ZhengdongLuandHangLi.Adeeparchitectureformatchingshorttexts.In
4bshowsthatGLOWissuperiorinenlargingtheweightedcosine C.J.C.Burges,L.Bottou,M.Welling,Z.Ghahramani,andK.Q.Weinberger,
editors,AdvancesinNeuralInformationProcessingSystems26,pages1367–1375.
similarityrangerapidly. CurranAssociates,Inc.,2013.
[19] B.MitraandN.Craswell.AnIntroductiontoNeuralInformationRetrieval.2018.
[20] BhaskarMitra,FernandoDiaz,andNickCraswell. Learningtomatchusing
5 CONCLUSION localanddistributedrepresentationsoftextforwebsearch.InProceedingsofthe
WepresentGLOW,ageneralframeworkformatchingphasein 26thInternationalConferenceonWorldWideWeb,WWW’17,page1291–1299,
RepublicandCantonofGeneva,CHE,2017.InternationalWorldWideWeb
websearch.Itlearnssemanticrepresentationforbothqueriesand ConferencesSteeringCommittee.
documentsbyintegratingglobalweightintoattentionscorecalcu- [21] AndriyMnihandKorayKavukcuoglu.Learningwordembeddingsefficientlywith
lation.Byintegratingthewholewordweightsharing,itenhances
noise-contrastiveestimation.InProceedingsofthe26thInternationalConference
onNeuralInformationProcessingSystems-Volume2,NIPS’13,page2265–2273,
wholewordlevelattentioninteraction.Moreover,combinedfields RedHook,NY,USA,2013.CurranAssociatesInc.
representationisproposedtofitGLOWintomulti-fieldsdocument [22] EricNalisnick,BhaskarMitra,NickCraswell,andRichCaruana. Improving
documentrankingwithdualwordembeddings.InProceedingsofthe25thInter-
scenario.Weconductextensiveexperimentsandrigorousanalysis, nationalConferenceCompaniononWorldWideWeb,WWW’16Companion,page
demonstratingthatGLOWoutperformsothermodernframeworks 83–84,RepublicandCantonofGeneva,CHE,2016.InternationalWorldWide
asthedeepmatchingmodel. WebConferencesSteeringCommittee.
[23] RodrigoNogueiraandKyunghyunCho. Passagere-rankingwithbert. arXiv
preprintarXiv:1901.04085,2019.
[24] RodrigoNogueira,WeiYang,KyunghyunCho,andJimmyLin. Multi-stage
REFERENCES
documentrankingwithbert.arXivpreprintarXiv:1910.14424,2019.
[1] Placing search in context: The concept revisited. ACM Trans. Inf. Syst., [25] RodrigoNogueira,WeiYang,JimmyLin,andKyunghyunCho.Documentex-
20(1):116–131,January2002. pansionbyqueryprediction,2019.
[2] MartinAumüller,ErikBernhardsson,andAlexanderFaithfull.Ann-benchmarks: [26] LiangPang,YanyanLan,JiafengGuo,JunXu,ShengxianWan,andXueqiCheng.
Abenchmarkingtoolforapproximatenearestneighboralgorithms.InInterna- Textmatchingasimagerecognition.InProceedingsoftheThirtiethAAAIConfer-
tionalConferenceonSimilaritySearchandApplications,pages34–49.Springer, enceonArtificialIntelligence,AAAI’16,page2793–2799.AAAIPress,2016.
2017. [27] RamaKumarPasumarthi,SebastianBruch,XuanhuiWang,ChengLi,Mike
[3] JimmyLeiBa,JamieRyanKiros,andGeoffreyEHinton.Layernormalization. Bendersky,MarcNajork,JanPfeifer,NadavGolbandi,RohanAnil,andStephan
arXivpreprintarXiv:1607.06450,2016. Wolf.Tf-ranking:Scalabletensorflowlibraryforlearning-to-rank.InProceedings
[4] PayalBajaj,DanielCampos,NickCraswell,LiDeng,JianfengGao,Xiaodong ofthe25thACMSIGKDDInternationalConferenceonKnowledgeDiscoveryand
Liu,RanganMajumder,AndrewMcNamara,BhaskarMitra,TriNguyen,etal. DataMining(KDD),pages2970–2978,2019.
Msmarco:Ahumangeneratedmachinereadingcomprehensiondataset.arXiv [28] YifanQiao,ChenyanXiong,ZhenghaoLiu,andZhiyuanLiu.Understandingthe
preprintarXiv:1611.09268,2016. behaviorsofbertinranking.arXivpreprintarXiv:1904.07531,2019.
[5] JamieCallan,MarkHoy,ChangkukYoo,andLeZhao.Clueweb09dataset,2009. [29] AlecRadford,KarthikNarasimhan,TimSalimans,andIlyaSutskever.Improving
[6] DanielCer,YinfeiYang,Sheng-yiKong,NanHua,NicoleLimtiaco,RhomniSt languageunderstandingbygenerativepre-training. URLhttps://s3-us-west-2.
John,NoahConstant,MarioGuajardo-Cespedes,SteveYuan,ChrisTar,etal. amazonaws.com/openai-assets/researchcovers/languageunsupervised/languageun-
Universalsentenceencoder.arXivpreprintarXiv:1803.11175,2018. derstandingpaper.pdf,2018.
[7] ZhuyunDaiandJamieCallan.Context-awaresentence/passagetermimportance [30] NilsReimersandIrynaGurevych.Sentence-bert:Sentenceembeddingsusing
estimationforfirststageretrieval.arXivpreprintarXiv:1910.10687,2019. siamesebert-networks.arXivpreprintarXiv:1908.10084,2019.
[8] JacobDevlin,Ming-WeiChang,KentonLee,andKristinaToutanova. BERT: [31] StephenRobertsonandHugoZaragoza.Theprobabilisticrelevanceframework:
Pre-trainingofdeepbidirectionaltransformersforlanguageunderstanding.In Bm25andbeyond.Found.TrendsInf.Retr.,3(4):333–389,April2009.
Proceedingsofthe2019ConferenceoftheNorthAmericanChapteroftheAssociation [32] StephenRobertson,HugoZaragoza,andMichaelTaylor.Simplebm25extension
forComputationalLinguistics:HumanLanguageTechnologies,Volume1(Longand tomultipleweightedfields.InProceedingsoftheThirteenthACMInternational
ShortPapers),pages4171–4186,Minneapolis,Minnesota,June2019.Association ConferenceonInformationandKnowledgeManagement,CIKM’04,page42–49,
forComputationalLinguistics. NewYork,NY,USA,2004.AssociationforComputingMachinery.
[9] JiafengGuo,YixingFan,QingyaoAi,andWBruceCroft. Adeeprelevance [33] StephenE.Robertson,SteveWalker,SusanJones,MichelineHancock-Beaulieu,
matchingmodelforad-hocretrieval.InProceedingsofthe25thACMInternational andMikeGatford.Okapiattrec-3.InTREC,1994.
onConferenceonInformationandKnowledgeManagement,pages55–64,2016. [34] YelongShen,XiaodongHe,JianfengGao,LiDeng,andGrégoireMesnil.Learning
[10] KaimingHe,XiangyuZhang,ShaoqingRen,andJianSun.Deepresiduallearning semanticrepresentationsusingconvolutionalneuralnetworksforwebsearch.
forimagerecognition.InProceedingsoftheIEEEconferenceoncomputervision InProceedingsofthe23rdInternationalConferenceonWorldWideWeb,WWW’14
andpatternrecognition,pages770–778,2016. Companion,page373–374,NewYork,NY,USA,2014.AssociationforComputing
[11] BaotianHu,ZhengdongLu,HangLi,andQingcaiChen.Convolutionalneural Machinery.
networkarchitecturesformatchingnaturallanguagesentences.InZ.Ghahra- [35] KrystaM.SvoreandChristopherJ.C.Burges. Amachinelearningapproach
mani,M.Welling,C.Cortes,N.D.Lawrence,andK.Q.Weinberger,editors, forimprovedbm25retrieval. InProceedingsofthe18thACMConferenceon
AdvancesinNeuralInformationProcessingSystems27,pages2042–2050.Curran InformationandKnowledgeManagement,CIKM’09,page1811–1814,NewYork,
Associates,Inc.,2014. NY,USA,2009.AssociationforComputingMachinery.
[12] BaotianHu,ZhengdongLu,HangLi,andQingcaiChen.Convolutionalneural [36] AshishVaswani,NoamShazeer,NikiParmar,JakobUszkoreit,LlionJones,
networkarchitecturesformatchingnaturallanguagesentences.InZ.Ghahra- AidanNGomez,ŁukaszKaiser,andIlliaPolosukhin.Attentionisallyouneed.
mani,M.Welling,C.Cortes,N.D.Lawrence,andK.Q.Weinberger,editors, InI.Guyon,U.V.Luxburg,S.Bengio,H.Wallach,R.Fergus,S.Vishwanathan,
AdvancesinNeuralInformationProcessingSystems27,pages2042–2050.Curran andR.Garnett,editors,AdvancesinNeuralInformationProcessingSystems30,
Associates,Inc.,2014. pages5998–6008.CurranAssociates,Inc.,2017.

GLOW:GlobalWeightedSelf-AttentionNetworkforWebSearch Woodstock’18,June03–05,2018,Woodstock,NY
[37] YonghuiWu,MikeSchuster,ZhifengChen,QuocVLe,MohammadNorouzi, [42] ZeynepAkkalyoncuYilmaz,ShengjinWang,WeiYang,HaotianZhang,and
WolfgangMacherey,MaximKrikun,YuanCao,QinGao,KlausMacherey,etal. JimmyLin.Applyingberttodocumentretrievalwithbirch.InProceedingsofthe
Google’sneuralmachinetranslationsystem:Bridgingthegapbetweenhuman 2019ConferenceonEmpiricalMethodsinNaturalLanguageProcessingandthe9th
andmachinetranslation.arXivpreprintarXiv:1609.08144,2016. InternationalJointConferenceonNaturalLanguageProcessing(EMNLP-IJCNLP):
[38] LeeXiong,ChenyanXiong,YeLi,Kwok-FungTang,JialinLiu,PaulBennett, SystemDemonstrations,pages19–24,2019.
JunaidAhmed,andArnoldOverwijk.Approximatenearestneighbornegative [43] HamedZamani,BhaskarMitra,XiaSong,NickCraswell,andSaurabhTiwary.
contrastivelearningfordensetextretrieval. arXivpreprintarXiv:2007.00808, Neuralrankingmodelswithmultipledocumentfields. InProceedingsofthe
2020. EleventhACMInternationalConferenceonWebSearchandDataMining,WSDM
[39] WeiYang,YuqingXie,AileenLin,XingyuLi,LuchenTan,KunXiong,MingLi, ’18,page700–708,NewYork,NY,USA,2018.AssociationforComputingMachin-
andJimmyLin.End-to-endopen-domainquestionansweringwithbertserini. ery.
arXivpreprintarXiv:1902.01718,2019. [44] HongfeiZhang,XiaSong,ChenyanXiong,CorbyRosset,PaulBennett,Nick
[40] WeiYang,HaotianZhang,andJimmyLin.Simpleapplicationsofbertforadhoc Craswell,andSaurabhTiwary.Genericintentrepresentationinwebsearch.In
documentretrieval.arXivpreprintarXiv:1903.10972,2019. The42ndInternationalACMSIGIRConferenceonResearchandDevelopmentin
[41] ZhilinYang,ZihangDai,YimingYang,JaimeG.Carbonell,RuslanSalakhutdinov, InformationRetrieval(SIGIR2019).ACM,July2019.
andQuocV.Le. Xlnet:Generalizedautoregressivepretrainingforlanguage [45] ShuailiangZhang,HaiZhao,YuweiWu,ZhuoshengZhang,XiZhou,andXiang
understanding.InNeurIPS,2019. Zhou.Dualco-matchingnetworkformulti-choicereadingcomprehension.arXiv
preprintarXiv:1901.09381,2019.