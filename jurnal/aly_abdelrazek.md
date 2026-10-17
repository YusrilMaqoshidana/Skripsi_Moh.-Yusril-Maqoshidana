InformationSystems112(2023)102131
ContentslistsavailableatScienceDirect
InformationSystems
journalhomepage:www.elsevier.com/locate/is
Topicmodelingalgorithmsandapplications:Asurvey
AlyAbdelrazeka,∗ ,YomnaEida,EmanGawisha,WalaaMedhata,b,AhmedHassana
aInformationTechnologyandComputerScience,CIS,NileUniversity,Giza,Egypt
bFacultyofcomputersandartificialintelligence,BenhaUniversity,Egypt
a r t i c l e i n f o a b s t r a c t
Articlehistory: Topicmodelingisusedininformationretrievaltoinferthehiddenthemesinacollectionofdocuments
Received27August2022 and thus provides an automatic means to organize, understand and summarize large collections
Receivedinrevisedform3October2022 of textual information. Topic models also offer an interpretable representation of documents used
Accepted3October2022 in several downstream Natural Language Processing (NLP) tasks. Modeling techniques vary from
Availableonline17October2022
probabilistic graphical models to the more recent neural models. This paper surveys topic models
RecommendedbyDennisShashah
fromfouraspects.Thefirstaspectcategorizesdifferenttopicmodelingtechniquesintofourcategories:
Keywords: algebraic,fuzzy,probabilistic,andneural.Wereviewthewidevarietyofavailablemodelsfromeach
Topicmodeling category,highlightdifferencesandsimilaritiesbetweenmodelsandmodelcategoriesusingaunified
Neural perspective, investigate these models’ characteristics and limitations, and discuss their proper use
Probabilistic cases.Thesecondaspectillustratessixcriteriaforproperevaluationoftopicmodels,frommodeling
Evaluation quality to interpretability, stability, efficiency, and beyond. Topic modeling has found applications
LDA
in various disciplines, owing to its interpretability. We examine these applications along with some
popularsoftwaretoolswhichprovideanimplementationofsomemodels.Thefourthaspectreviews
available datasets and benchmarks. Using two benchmark datasets, we conducted experiments to
compare seven topic models along the proposed metrics. The discussion highlights the differences
between the models and their relative suitability for various applications. It notes the relationship
betweenevaluationmetricsandproposesfourkeyaspectstohelpdecidewhichmodeltouseforan
application.Ourdiscussionalsoshowsthattheresearchtrendsmovetowardsdevelopingandtuning
neural topic models and leveraging the power of pre-trained language models. Finally, it highlights
researchgapsindevelopingunifiedbenchmarksandevaluationmetrics.
©2022ElsevierLtd.Allrightsreserved.
Contents
1. Introduction......................................................................................................................................................................................................................... 2
2. Backgroundanddefinitions.............................................................................................................................................................................................. 3
3. Methodology....................................................................................................................................................................................................................... 3
4. Topicmodels....................................................................................................................................................................................................................... 3
4.1. Algebraicmodels.................................................................................................................................................................................................... 4
4.2. Probabilisticmodels.............................................................................................................................................................................................. 4
4.2.1. LatentDirichletallocation..................................................................................................................................................................... 5
4.2.2. ExtendingLDA........................................................................................................................................................................................ 5
4.3. Fuzzymodels.......................................................................................................................................................................................................... 5
4.4. Neuralmodels........................................................................................................................................................................................................ 6
4.4.1. Variationalautoencoders-neuraltopicmodels.................................................................................................................................. 6
5. Evaluationmetrics.............................................................................................................................................................................................................. 7
5.1. Qualityandperplexity.......................................................................................................................................................................................... 7
5.2. Interpretabilityandtopiccoherence .................................................................................................................................................................. 7
5.3. Topicdiversity(uniqueness)................................................................................................................................................................................ 7
5.4. Stability:Topicsimilarityacrossruns................................................................................................................................................................. 7
5.5. Efficiency;computationandmemorycomplexity............................................................................................................................................. 8
5.6. Flexibility ............................................................................................................................................................................................................... 8
∗
Correspondingauthor.
E-mailaddress: al.abdelrazek@nu.edu.eg(A.Abdelrazek).
https://doi.org/10.1016/j.is.2022.102131
0306-4379/©2022ElsevierLtd. Allrightsreserved.

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
6. Topicmodelstoolsandapplications................................................................................................................................................................................ 8
6.1. Topicmodelingapplications................................................................................................................................................................................. 8
6.2. Softwaretools........................................................................................................................................................................................................ 8
6.3. Datasets................................................................................................................................................................................................................... 9
7. Comparisonofmodels....................................................................................................................................................................................................... 9
7.1. Experimentalsetup................................................................................................................................................................................................ 9
7.2. Results..................................................................................................................................................................................................................... 10
8. Discussionandanalysis .................................................................................................................................................................................................... 10
8.1. Themodels............................................................................................................................................................................................................. 10
8.1.1. Coherence................................................................................................................................................................................................ 12
8.1.2. Diversity.................................................................................................................................................................................................. 12
8.1.3. Stability.................................................................................................................................................................................................... 12
8.1.4. Efficiency................................................................................................................................................................................................. 13
8.2. Modelselection...................................................................................................................................................................................................... 13
8.3. Researchtrends...................................................................................................................................................................................................... 13
8.4. Researchgaps......................................................................................................................................................................................................... 13
9. Conclusionandfuturework.............................................................................................................................................................................................. 13
Declarationofcompetinginterest.................................................................................................................................................................................... 14
Dataavailability.................................................................................................................................................................................................................. 14
References........................................................................................................................................................................................................................... 15
differentadvantagesandarebettersuitedforaparticularsetting.
1. Introduction Therefore,theyco-existsidebyside.
Due to a large number of available models, a need arises to
Topic modeling (TM) has been used successfully in mining summarizethem.Therehavebeenattemptsatsummarizingthe
large text corpora where a topic model takes a collection of widerangeofavailabletopicmodelsintheliterature.In[13],two
documents as an input and then attempts, without supervision, categorieswerepresented.Thefirstcategoryclassifiesthemodels
touncovertheunderlyingtopicsinthiscollection[1].Eachtopic intofoursubgroups,Latentsemanticindexing(LSI),Probabilistic
describesahuman-interpretablesemanticconcept.TMthenpro- latentsemanticindexing(PLSI),LatentDirichletallocation(LDA),
videsalatentinterpretablerepresentationofdocumentsaccord- andCorrelatedtopicmodel(CTM).Thesecondcategorydiscusses
ingtotheconceivedtopics[2]. different topic evolution models over time. In [14], the survey
Topicmodelingisappliedindifferentfields.NaturalLanguage proposedhierarchicalcategorizationcriteriawheremodelswere
Processing (NLP) tasks have leveraged topic modeling, like text classified according to being LDA and non-LDA based, bag-of-
summarizationandsentimentanalysis.Moreover,thepowerful- wordsorsequence-of-wordsapproach,andfinally,unsupervised
ness of topic modeling is extended to other fields, like bioinfor- or supervised learning models. In [15], different models were
matics and economics. TM is also used with other sets of data discussed in terms of their features and limitations. In [16], the
where the concept of words and documents is replaced with authors categorized topic models into 3 classes. The first dis-
similar entities of similar structure. The entities could be items cussestraditionaltopicmodelslikeLSI,PLSI,andLDA.Thesecond
inonlineshops,segmentsinimages,orgenesingenesets. classfocusesonthetopicevolutionmodels.Finally,thethirdclass
Since 1990 [3] with the introduction of Latent Semantic In- discussessomejointtechniquesoftopicmodelingandotheralgo-
dexing (LSI), researchers have developed several techniques for rithms, including LDA-VSM+K-means and LDA-Word2vec+SVM.
topicmodelingthatvaryinthemodelingcapacity.Moreover,dif- In[17],theauthorshaveinvestigatedtheresearchworkdoneon
ferentmodelsmakedifferentassumptionsaboutthecorpus,the LDAtopicmodeling.Adetailedsurveyontopicmodelingforlong
documents’ representation, and the topics. The developed topic andshorttextinthelastdecadewasintroducedin[18]whereas
models occupy a broad spectrum for different use cases. They thespecificcategoryofneuraltopicmodelswassurveyedin[19].
also exhibit different evaluation metrics scores. More models ThispapertakesaholisticapproachtosurveyTM.Itdiscusses
continuetobedevelopedtillnow.Thiscontinuousdevelopment thefourcategoriesofTMandpresentsthewidevarietyofavail-
tries to address the current research gaps and extend the TM able models in a structured perspective. The goal is to identify
applications’scope. researchgapsandhighlightsimilaritiesanddifferencesbetween
According to their underlying modeling techniques, four cat- modelsandmodelcategories.Furthermore,sinceevaluationmet-
egories of topic models are recognized: algebraic, fuzzy, proba- ricsvaryindifferentpapers,weproposeacomprehensivesetof
bilistic, and neural. Algebraic topic models were developed first evaluation metrics that can be applied to all models to ensure
duringthe1990s[3].Then,followingtheadventofLDAin2003, consistencyinmodels’evaluation.Additionally,availablebench-
most of the developed topic models were Bayesian Probabilistic mark datasets in topic modeling are reviewed, followed by an
Topic Models (BPTMs) such as [1,4,5]. These BPTMs have proof overviewofdifferenttoolsandapplicationsoftopicmodeling.We
of efficiency and dominated the research venues till 2015. The then experiment with various models from different categories
reasonisthattheyareusuallysimpletodeploy,easytointerpret, and compare them along the proposed evaluation criteria using
andmodularenoughtoextendintomorecomplexmodels.They two common benchmark datasets. This perspective considers
also are adequately computationally efficient since they have the latest advancements in different topic modeling techniques.
relativelyfewparameters[1].Recently,topicmodelsincreasingly Hopefully, it will ignite interest in TM and help the research
use neural components [6]. Examples of neural topic models communitydevelopimprovedmodels.
(NTMs) are [7,8]. Some NTMs use contextualized representation The rest of this paper is organized as follows. Section 2 pro-
torepresentthedocumentsinsteadoftheusualbagofwords[9– videsbackgroundinformationandestablishesthedefinitionsand
11]. They can use pre-trained models on a large corpus, such as notation whereas Section 3 provides the methodology. The cat-
BERT variants [12]. In general, NTM offers flexibility and scala- egorization of models is outlined in Section 4 followed by a
bility. It is important to note that different TM categories offer surveyofseveralmodelsfromthecategories.Differentevaluation
2

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
criteria of topic models are discussed in Section 5. Further, Sec- Where b vector is sparse, bv is the number of occurrences
tion 6 highlights some applications of various topic models and of the token (word) v ∈ {1,...,V} in the document. On the
introducespopularsoftwaretoolsthatimplementseveralmodels. other hand, some other models consider the sequence of con-
| It also briefly | shows | the     | available | datasets | and     | benchmarks | for  |                |              |     |     |            |         |     |          |
| --------------- | ----- | ------- | --------- | -------- | ------- | ---------- | ---- | -------------- | ------------ | --- | --- | ---------- | ------- | --- | -------- |
|                 |       |         |           |          |         |            |      | structs, which | acknowledges |     | the | dependence | between |     | the con- |
| topic models.   | In    | Section | 7, we     | compare  | various | models     | from |                |              |     |     |            |         |     |          |
structs.Intexts,aninputdocumenttoatopicmodelwillthusbe
different categories along the proposed metrics, and we discuss representedasadensevectorS oflengthL.
| the results | in Section | 8,  | where | we also | note the | research | trends |     |     |     |     |     |     |     |     |
| ----------- | ---------- | --- | ----- | ------- | -------- | -------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
∈ NL
andhighlighttheresearchgaps.Finally,thepaperisconcludedin s (2)
Section9.
|     |     |     |     |     |     |     |     | where s | ∈ {1,...,V} | is  | the index | of the | vocabulary | for | the jth |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ----------- | --- | --------- | ------ | ---------- | --- | ------- |
j
token(word),j∈{1,...,L},Listhelengthofthedocument.
2. Backgroundanddefinitions
Anotherdocumentrepresentationisthecontextualrepresen-
Topicmodelsattempttomodelthreeentities:constructs,col- tationthatisbecomingpopularwiththeubiquityoftransformer-
|           |             |     |            |     |              |      |      | based language | models |     | such as | BERT, where | the | document | is  |
| --------- | ----------- | --- | ---------- | --- | ------------ | ---- | ---- | -------------- | ------ | --- | ------- | ----------- | --- | -------- | --- |
| lections, | and topics. | The | constructs | are | the elements | that | come |                |        |     |         |             |     |          |     |
together to make a collection. In textual data, constructs are represented as an embedding vector. BERT models capture con-
usually words that are grouped to constitute a document or a textualwordembeddingsbetterthanglobalembeddingsasthey
collectionofwords.Atopicisaclusterofconstructsthattogether learndifferentrepresentationsforpolysemouswords.
| describe | a pure | semantic   | meaning.     | It  | is an idealized | notion        | of a |     |     |     |     |     |     |     |     |
| -------- | ------ | ---------- | ------------ | --- | --------------- | ------------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
| document | that   | is as pure | as possible. |     | Also, it is     | a homogeneous |      |     |     |     |     |     |     |     |     |
collection whose constructs have so much in common, usually 3. Methodology
semantically.Mathematically,atopicisdescribedasaprobability
distributionovertheconstructs[20].
|     |     |     |     |     |     |     |     | Models | are categorized |     | into four | categories: |     | algebraic, | fuzzy, |
| --- | --- | --- | --- | --- | --- | --- | --- | ------ | --------------- | --- | --------- | ----------- | --- | ---------- | ------ |
Most topic models work by observing the co-occurrence of Bayesianprobabilistic,andfinally,neuraltopicmodels.Thiscat-
constructs in the collections. In linguistics, this aligns with the egorizationisshowninFig.1.
| distributional | hypothesis |     | [21,22] | which | states that | the | distribu- |     |     |     |     |     |     |     |     |
| -------------- | ---------- | --- | ------- | ----- | ----------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
ThefirstTMcategoryisthealgebraicmodels.Theyaresimple
| tional properties |     | of tokens | dictate | their | semantic | meaning. | In  |     |     |     |     |     |     |     |     |
| ----------------- | --- | --------- | ------- | ----- | -------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
butdonothaveasolidstatisticalfoundation,nordotheydefine
| other words, | a   | word is characterized |     |     | by the context | in  | which it |     |     |     |     |     |     |     |     |
| ------------ | --- | --------------------- | --- | --- | -------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
apropergenerativedatamodel[20].Thislinearalgebraapproach
| appears. | Similarly, | the co-occurrence |     | of  | pixels in | images | defines |               |       |         |       |          |        |             |     |
| -------- | ---------- | ----------------- | --- | --- | --------- | ------ | ------- | ------------- | ----- | ------- | ----- | -------- | ------ | ----------- | --- |
|          |            |                   |     |     |           |        |         | was developed | first | in [3]. | There | are more | recent | approaches, |     |
segments(topics)duetothespatiallylocalcorrelationsbetween
pixels. too, such as [26] that use spectral decomposition for inference.
TMcanbeappliedtoseveraldataforms,butwewillonlycon- Algebraicmodelsaresimpleandrelativelyefficient.Ontheother
sidertheirapplicationintextthroughoutthefollowingsections. hand, fuzzy topic models are clustering techniques that target
|            |       |           |     |          |       |                 |     | assigning | words | to associated | topics. | They | have | proved | their |
| ---------- | ----- | --------- | --- | -------- | ----- | --------------- | --- | --------- | ----- | ------------- | ------- | ---- | ---- | ------ | ----- |
| In textual | data, | documents | are | presumed | to be | a heterogeneous |     |           |       |               |         |      |      |        |       |
collection of constructs that span more than one topic. Topic effectiveness in short text documents where they overcome the
sparsity is also presumed following the heuristic that any one sparsityproblem.
documentwillusuallybeaboutasmallnumberoftopics. ComingtotheBayesianprobabilisticmodels,theyweredomi-
TopicmodelstakeacorpusDasinputandattempttoobtain nantbefore2015,whentheresearcheffortsshiftedtodeveloping
twosetsofdistributions:ThefirstsetT isfortopics:K distribu- neural topic models (NTMs). Bayesian models are intuitive and
| tionsoverV | constructs(tokens)whereK |     |     |     | isthenumberoftopics, |     |     |     |     |     |     |     |     |     |     |
| ---------- | ------------------------ | --- | --- | --- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
extendable.Theydefineafictitiousgenerativeprocessabouthow
| usuallyahyperparameter,andV      |     |     |     | isthevocabularysizeinthecor- |     |     |     |               |           |        |            |           |         |                |       |
| -------------------------------- | --- | --- | --- | ---------------------------- | --- | --- | --- | ------------- | --------- | ------ | ---------- | --------- | ------- | -------------- | ----- |
|                                  |     |     |     |                              |     |     |     | the observed  | documents |        | come to    | be. Then, | they    | work           | back- |
| pus.ThesecondsetofdistributionsZ |     |     |     | isfordocuments,anditisa      |     |     |     |               |           |        |            |           |         |                |       |
|                                  |     |     |     |                              |     |     |     | ward to infer | the       | topics | that could | have      | created | the documents. |       |
distributionforeachdocumentincorpusoverK topics,wherefor Bayesianmodels’parameterstendtohavemoreconcretemean-
| eachdocument,z |     | k indicatestheweightofthekthtopic.Thissec- |     |     |     |     |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ingandthusareeasilyinterpreted.Thisinterpretabilityofparam-
| ond distribution |     | provides | an interpretable |     | latent | representation |     |     |     |     |     |     |     |     |     |
| ---------------- | --- | -------- | ---------------- | --- | ------ | -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
etersishelpfultotroubleshootamodel,validateit,andinterpret
ofdocuments(SimilartodisentangledVariationalAutoEncoder,
|                                            |     |     |     |     |     |                |     | the results,     | especially | in      | cross-disciplinary |      | use   | cases. | It is also |
| ------------------------------------------ | --- | --- | --- | --- | --- | -------------- | --- | ---------------- | ---------- | ------- | ------------------ | ---- | ----- | ------ | ---------- |
| VAE[23,24]).TheselatentrepresentationsandT |     |     |     |     |     | (TMparameters) |     |                  |            |         |                    |      |       |        |            |
|                                            |     |     |     |     |     |                |     | helpful whenever |            | we want | to generate        | more | data. | On     | the other  |
arelearnedtobestexplaintheobserveddocuments.Thislearning
hand,theinferenceprobleminthiscategoryofmodelsbecomes
iscalledtheinferenceprocess.Thegenerativeprocessgenerates
adocumentfromapresumedZ andT. morecomplicatedwithmorecomplexmodeling.
Note that there are several ways in which collections can Neural Topic Models (NTMs) are more flexible and scalable
bedecomposedintotopics,leadingtounstableoutcomeswhere because,inNTMs,theinferenceproblemisanoptimizationprob-
lem.However,theirparametersmaynothaveameaningfulinter-
| each model | run | results | in a separate |     | set of topics. | Accordingly, |     |     |     |     |     |     |     |     |     |
| ---------- | --- | ------- | ------------- | --- | -------------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
modelregularizationisnecessary,anditisdiscussedinSection5. pretation. It is usually hard to investigate why the model does
TM can uncover polysemy, where a single construct has sev- or does not work. NTMs train at different objective functions,
eralsemanticmeanings[25].TMcapturesthisbyhavingthesame for example, minimizing the reconstruction error of documents
construct showing up in several topics. Synonymity, where two or optimizing the model’s predictive accuracy. This optimiza-
| different | constructs | have | similar | semantic | meaning, | can | also be |     |     |     |     |     |     |     |     |
| --------- | ---------- | ---- | ------- | -------- | -------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
tiongoaldoesnotnecessarilyresultinhigh-qualityinterpretable
capturedbyTMwhendifferentconstructsappeartogetherinthe
|     |     |     |     |     |     |     |     | topics. A | comparison | between | different |     | modeling | techniques | is  |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---------- | ------- | --------- | --- | -------- | ---------- | --- |
sametopicinmorethanonedistributionofT.
presentedinTable1.
| The representation |     | of  | documents |     | is different | for | different |     |     |     |     |     |     |     |     |
| ------------------ | --- | --- | --------- | --- | ------------ | --- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
models.Somemodelsconsiderthecollectionasanunorderedset
ofits constructs. Intexts, thesemodels areknown asthe bagof 4. Topicmodels
wordsmodels[22].Theinputtothetopicmodel,inthiscase,is
avectorofwordcounts.
|        |     |     |     |     |     |     |     | The different            | model | categories |     | shall be | discussed | in  | detail in |
| ------ | --- | --- | --- | --- | --- | --- | --- | ------------------------ | ----- | ---------- | --- | -------- | --------- | --- | --------- |
| b ∈ ZV |     |     |     |     |     |     | (1) | thefollowingsubsections. |       |            |     |          |           |     |           |
>=0
3

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
|     |     |     |     | Fig.1. | Topicmodelscategorizationaccordingtotheusedtechnique. |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------ | ----------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Table1
Comparisonbetweentopicmodels’categories.
| Category |     | Description |     |     |     |     |     | Pros |     |     | Cons |     |     |     |
| -------- | --- | ----------- | --- | --- | --- | --- | --- | ---- | --- | --- | ---- | --- | --- | --- |
Algebraic Decomposethedocument-termmatrix,thenfind Simple,intuitive,andcomputationally Providesnosolidstatistical
alow-rankapproximationtoit. relativelyefficient.Someadaptations foundation.Anddoesnotdefinea
|     |     |     |     |     |     |     |     | canhandleshorttextdocuments. |     |     | generativedatamodel. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------------------- | --- | --- | -------------------- | --- | --- | --- |
Fuzzy Extracttopicsfromthedocuments,thenassign Itcanhandlesparsityinshorttext Mostoftheapplicationsfocuson
thewordstothesetopics/clustersusingadegree documents(forexample,tweets). medicaldata.
oftruthinsteadofBooleanlogic‘‘1or0’’.
Bayesian DefineagenerativeprocessthroughaBayesian Simple,intuitive,extensible,and Inferencebecomescomplicatedwith
probabilistic graphicalmodel(Directedacyclicgraph).Then interpretable. increasedmodelcomplexity.
workbackwardforinference.
Neuraltopic Substitutetheintractableposteriorinferencewith Flexibilityofjointtraining, Interpretabilityofmodelparameters.
models optimization. optimizingfortopiccoherence, Also,itgenerallycannothandle
|     |     |     |     |     |     |     |     | attainingcomplexmodels,scalability. |     |     | sparsity. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --------- | --- | --- | --- |
4.1. Algebraicmodels proposed in [28] to discover latent topics in short texts us-
|     |     |     |     |     |     |     |     | ing a semantics-assisted |     | NMF. | It exploits | the | word-context | se- |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------ | --- | ---- | ----------- | --- | ------------ | --- |
The first model to develop was Latent Semantic Allocation mantic associations among the words by applying neural word
(LSI) [3]. LSI is a BOW model that represents the corpus as embeddings. This approach has proved to boost the model per-
a document term matrix (DTM). Then it decomposes the DTM formance. It leverages the word-context semantic relationships
using singular value decomposition into its constituents. It con- learned from skip-gram. The extensive evaluations performed
sidersthelargestsingularvaluesineachdocument—correspond- over real-world short datasets demonstrate the superior perfor-
|            |      |         |             |          |          |         |     | manceofthe | presentedmodelsinterms |     |     | oftopiccoherenceand |     |     |
| ---------- | ---- | ------- | ----------- | -------- | -------- | ------- | --- | ---------- | ---------------------- | --- | --- | ------------------- | --- | --- |
| ing to the | most | evident | topics. LSI | uncovers | patterns | between |     |            |                        |     |     |                     |     |     |
accuracy.Topiccoherenceisametricthatevaluatesatopicmod-
termsofthecorpus,suchassynonymity.Itcanbeusedtocom-
elingtechniqueaccordingtoitshumaninterpretability,whichwe
| pare documents |     | and perform | queries | for | information | retrieval |     |     |     |     |     |     |     |     |
| -------------- | --- | ----------- | ------- | --- | ----------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
willdiscussindetailinSection5.
tasks,whereastheinterpretabilityofLSIissomehowlimited.This
| limitation                  | is common     | with       | several               | topic | models | that generate |        |                          |                |          |          |     |               |     |
| --------------------------- | ------------- | ---------- | --------------------- | ----- | ------ | ------------- | ------ | ------------------------ | -------------- | -------- | -------- | --- | ------------- | --- |
|                             |               |            |                       |       |        |               |        | 4.2. Probabilisticmodels |                |          |          |     |               |     |
| limited human-interpretable |               |            | documents.            |       | Being  | a BOW         | model, |                          |                |          |          |     |               |     |
| it disregards               | order         | and        | retains multiplicity. |       | LSI    | implicitly    | as-    |                          |                |          |          |     |               |     |
|                             |               |            |                       |       |        |               |        | Topic                    | models in this | category | consider | the | probabilistic | na- |
| sumes a                     | probabilistic | generative | model                 | where | words  | and           | docu-  |                          |                |          |          |     |               |     |
tureofthemodeledentities.Theymaptherelationshipbetween
mentsarejointlyGaussiandistributed.Thisassumptiondoesnot
|     |     |     |     |     |     |     |     | different | model random | variables | through | a graph, | usually | a di- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------------ | --------- | ------- | -------- | ------- | ----- |
matchreality.ProbabilisticLSIaddressesthiswithamultinomial rectedacyclicgraph(DAG),andthuscalledBayesianmodels.Note
generativemodel[20]. that some models such as [29] proposed an undirected graph.
Non-negative matrix factorization (NMF) [27] is another al- In the DAG, nodes represent random variables. These random
gebraic model used extensively in NLP. It assumes that a given variables are either observed, such as the constructs or words.
higher dimension vector can be factorized into a lower dimen- Theycanbelatentorhidden,suchasthetopicdistribution.The
sion representation, given that all the resultant representations existenceofanedgeindicatesprobabilisticdependencebetween
are non-negative. In this respect, a model called SeaNMF was anytworandomvariables.
4

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
4.2.1. LatentDirichletallocation normal distribution to model topics’ correlation instead of the
This is the simplest topic model in this category which was Dirichlet distribution in LDA. Furthermore, LDA uses standard
later extended in several ways. It is a bag of words model that variational inference. However, CTM uses the mean-field varia-
representsadocumentasavectoroflengthL.InLDA,document tionalinferencetoapproximatetheposteriorinference.Another
generation process is defined in probabilistic terms [1,30]. It example is the Pachinko allocation model [34], which models
assumesthateachdocumenti,isgenerated,onewordatatime, wordcorrelationsinadditiontothecorrelationbetweentopics.
through sampling a topic from the distribution of topics for this Many documents contain metadata about, for example, the
document,θ andthensamplingawordwfromthistopic(atopic author, the title, links, publication date, and other data. Some
i
isadistributionoverwords). LDA extensions incorporate these metadata, such as [35] which
The topic assignment document i is denoted z. The distribu- considerstheauthor,and[36]whichconsidersthelinksindocu-
i
tionoftopicsitselfθ isdrawnfromaDirichletdistributionwhere ments.OtherLDAvariantscaninferthenumberoftopicshyper-
i
each component -topic- in the sampled mixture is independent parameter from the data, such as the Bayesian non-parametric
oftheother.IncorporatingDirichletdistributionmodelsthetopic HierarchicalDirichletProcesses(HDP)modelproposedin[37].
sparsity per document; confirmatory to the observations in real Short text documents such as on social websites and mi-
documents. This generative process defines a joint probability croblogs pose a challenge due to the sparsity of words. An-
distribution over the observed documents and the hidden topic other generative probabilistic model, the biterm topic model
structure. (BTM) [38], considers each co-occurring word pair as a single
p(θ,z,w|α,β) (3) term.Themodelisbuiltuponabitermsetinsteadofdocuments.
where both α and β are Dirichlet priors and are model hyper- 4.3. Fuzzymodels
parameters.Thentoinferthehiddentopicstructure,weusethe
joint distribution to compute the conditional distribution of the There are two approaches for any clustering task: hard and
topic structure given the observed documents. The inference is fuzzy.Inthehardclusteringapproach,anitemisforcedtobelong
calculatedinEq.(4). to one cluster. However, it can belong to multiple clusters in
p(θ,z,w|α,β) thecaseoffuzzyclusteringapproachwithdifferentmembership
p(θ,z|w,α,β)= (4) degrees[39].
p(w|α,β)
Fuzzysettheoryisselectedamongothertopicmodelsbecause
The denominator in the last equation is the marginal proba- othermodelssufferfromcomputationalcomplexity.Othermod-
bility of the observations, which can be computed by summing els also require probabilistic inference like Gibbs sampling [40].
thejointdistributionovereverypossiblehiddentopicstructure. The authors of [41] have mentioned that applying fuzzy repre-
The number of possible topic structures is so large that this sentation to LDA enhances the topic’s coherence compared to
summation is intractable to compute. Thus, approximations via regular LDA and term-weighted LDA. In this work, the authors
variational inference or Markov Chain Monte Carlo (MCMC) are implementedLDAusingfuzzydocumentrepresentation.
usedforinference. Thisfuzzyrepresentationmapseachdocumenttoavectorof
However, the results are not very stable. The model suffers a keyword. Each keyword belongs to each document with some
fromtheordereffect,wheretheorderofthefeddocumentsdur- fuzzymembershipvalue,calculatedusingthesemanticsimilarity
ingtrainingcanchangethegeneratedtopics.Italsorequiresthe between each keyword and all the other words. This approach
explicitsettingofthenumberoftopics,whichmaybechallenging enhancesthequalityofgeneratedtopicsbyassigningweightsto
to determine. Moreover, LDA is not very robust against changes eachkeywordaccordingtoitsimportance.Italsoovercomesthe
toDirichletpriorsandothermodelhyperparameters.Thesearch sparsity problem. Moreover, it counts the semantic association
space of all possible hyperparameters is big. An optimization amongwords.
techniquesuchasgeneticalgorithmsordifferentialevolution[31] Fuzzy topic modeling is applied to different fields, like text
couldbeusedtoreducethesearchspace.LDAwasextendedinto mining and medical and educational fields. The authors of [42]
variousmodelstoovercomeitsshortcomingsandtobetteradapt have proposed a novel fuzzy topic modeling approach that tries
todifferentcorporaproperties. to solve the problems of noise and sparsity in short texts. The
three essential components of this approach are BOW, Principal
4.2.2. ExtendingLDA ComponentAnalysis(PCA),andfuzzyc-meansalgorithm.
OnewaytoextendLDAistorelaxthebagofwordsassump- This approach leverages BOW in generating both local and
tion,wherethemodeldoesnotconsidertheorderofwordsina global frequencies. The PCA dimension reduction algorithm is
document. This assumption is a reasonable assumption to make used with a global term to remove the negative impact of high
touncoverthetopicsinacorpus.Forbetterlanguagemodeling, dimensionality. Lastly, fuzzy-c-means assigns each point to a
this assumption is relaxed [32]. In sentence LDA, the words in differentclusterwithvaryingmembershipfunctionsdegreesfor
one sentence are assumed to have been generated by the same each cluster. The fuzzy topic modeling technique has enhanced
topic [33]. Sentence LDA models the co-occurrence of words in theclassificationandclusteringtasks’accuracycomparedtothe
finer granularity than LDA. The order of documents is also not baselinemethodologies.
consideredbyLDA.Inthecaseofcorporathatspanseveralyears, Fuzzytopicmodelingcanalsobeappliedinpersonalizedweb
topicsarelikelytochangeovertime,andtheorderofdocuments searching to get user-oriented results. The authors of [43] have
isthusrelevant.Anexampleisin[5],whereatopicisnotasingle presentedapersonalizationfuzzytopicmodelingtechnique.Po-
distributionbutasequenceofdistributionsoverwords. tential personalization is estimated to enhance the effectiveness
Another LDA variant observes that the topics per document of the search system. The fuzzy logic is used to handle the
areusuallycorrelated.Theoccurrenceofatopicinonedocument uncertainty of each document’s topics. On the other hand, the
correlateswiththeoccurrenceofother’relatedtopics.LDAdoes fuzzy C-Means algorithm is used to retrieve the relevant topics.
not model the correlation between topics and considers them Therankedresultsfromthefuzzytopicmodelingtechniquewere
independent. So, when inferring the latent topics of a docu- compared to those from LDA techniques. Finally, the proposed
ment,onemayendupwithdisparatetopics.Thecorrelatedtopic experimentshaveshownthatthefuzzytopicmodelingtechnique
model(CTM)[4]isoneexampleofthis.CTMutilizesthelogistic hasovercometheLDA.
5

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
Coming to the medical field, the authors of [44] aimed at enrichtopicsmodelinginthecontextofshorttext.Aspreviously
modelingmedicaldocumentswithlowercomputationalcostand mentioned,theshorttextssufferfromthesparsityproblem.This
higher performance accuracy. This technique uses the fuzzy set problem was tackled by exploiting the semantic relationships
theoryandwordweightingtechniques(theimportanceofaword betweenthewordsduringtopicinference.
in a document in a corpus) for feature transformation (repre- In [51], a new framework that leverages pre-trained word
| senting   | words into different |     | formats | like | numbers   | for    | better |            |      |             |          |                  |     |       |              |
| --------- | -------------------- | --- | ------- | ---- | --------- | ------ | ------ | ---------- | ---- | ----------- | -------- | ---------------- | --- | ----- | ------------ |
|           |                      |     |         |      |           |        |        | embeddings | were | introduced. |          | This framework   |     | first | obtains text |
| modeling) | in the preprocessing |     | stage.  | This | technique | models |        |            |      |             |          |                  |     |       |              |
|           |                      |     |         |      |           |        |        | embeddings | and  | then        | clusters | these embeddings |     | into  | semanti-     |
medicaltopicsin3basicsteps:localtermweighting,thenglobal
|     |     |     |     |     |     |     |     | cally similar | texts. | Words | are | then extracted |     | from | each clus- |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | ------ | ----- | --- | -------------- | --- | ---- | ---------- |
term weighting (with five different methodologies), and finally, ter to represent the topic. Each of these steps is independent,
fuzzyclustering. which allows for flexible modeling. In [7], the text embeddings
For dimension reduction, the authors did not use PCA like can be obtained using any pre-trained language model such
in the previous work. However, they have developed a different as Bidirectional Encoder Representations from Transformers or
technique. Each clustering step input is the step that precedes BERT [12]. The resulting embeddings are clustered using Hier-
it. So, if we have an nxm matrix with 10 clusters in the first archical Density-Based Spatial Clustering of Applications with
step,thenthenextstepwillbenx10matrixwith9clusters.The Noise or HDBSCAN [52] to obtain a semantically coherent set of
numberofcolumndimensionswilldecreaseuntiltheminimum documentsineachclusterthatrepresentatopic.Theauthorthen
numberofclustersarereached.
proposesusingaclass-basedTermFrequency-InverseDocument
Intheeducationalfield,andduetotheincreasingnumberof
FrequencyorcTF-IDFtoobtainthewordsrepresentingeachtopic.
availableonlinelecturevideos,manyvideolectureshavemultiple
Incorporatingneuralcomponentsisusuallyadvantageous.For
| labels as  | they contain    | overlapped | subjects. |         | This fact    | hinders  | the |          |                |     |           |               |     |            |       |
| ---------- | --------------- | ---------- | --------- | ------- | ------------ | -------- | --- | -------- | -------------- | --- | --------- | ------------- | --- | ---------- | ----- |
|            |                 |            |           |         |              |          |     | example, | the previously |     | discussed | probabilistic |     | correlated | topic |
| efficiency | of video search | and        | the       | quality | of retrieved | results. |     |          |                |     |           |               |     |            |       |
modelssufferfromhighcomputationalcostsandinefficientscal-
In[45],alecture-content-basedclusteringisappliedtoovercome
|     |     |     |     |     |     |     |     | ing. In | light of | these | challenges, | an  | efficient | correlated | topic |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | -------- | ----- | ----------- | --- | --------- | ---------- | ----- |
thepreviouschallenges.Thistechniqueleveragesthetranscripts
|     |     |     |     |     |     |     |     | model with | topic | embeddings |     | was developed |     | [53] where | topics |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ----- | ---------- | --- | ------------- | --- | ---------- | ------ |
oftheavailablevideostogetthecontentofthevideos.Foreach
|     |     |     |     |     |     |     |     | are represented |     | as vectors, | and | the model |     | is trained | to learn |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ----------- | --- | --------- | --- | ---------- | -------- |
clusterrepresentation,theyhavereliedonWikipediadocuments. the topics embeddings and correlations in terms of the vector’s
| Then,asimilarityvalueiscalculatedbetweentheextractedvideo |                    |         |            |        |      |            |       | closeness.                                       |     |     |     |     |     |     |     |
| --------------------------------------------------------- | ------------------ | ------- | ---------- | ------ | ---- | ---------- | ----- | ------------------------------------------------ | --- | --- | --- | --- | --- | --- | --- |
| topics and                                                | the representative |         | documents  | for    | each | cluster.   | Based |                                                  |     |     |     |     |     |     |     |
| on this similarity                                        | value,             | a fuzzy | clustering | method |      | is applied | to    |                                                  |     |     |     |     |     |     |     |
|                                                           |                    |         |            |        |      |            |       | 4.4.1. Variationalautoencoders-neuraltopicmodels |     |     |     |     |     |     |     |
clusterthecontentofthevideos.
ThemostpopularframeworkforNTMs,however,isthemod-
|     |     |     |     |     |     |     |     | els that | extend | the generative |     | process | of probabilistic |     | models |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ------ | -------------- | --- | ------- | ---------------- | --- | ------ |
4.4. Neuralmodels
throughVariationalAutoEncoders(VAEs)[54,55].Intheremain-
|     |     |     |     |     |     |     |     | ing of this | section, | we  | use NTMs | to refer | to  | this subcategory. |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | -------- | --- | -------- | -------- | --- | ----------------- | --- |
Thefirstsubcategoryofthesemodelsusesneuralcomponents
|     |     |     |     |     |     |     |     | NTMs offer | several | advantages |     | over Bayesian |     | probabilistic | mod- |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ------- | ---------- | --- | ------------- | --- | ------------- | ---- |
suchasthemodelsthatuseembeddings[8,46–48].LDA2VEC[47]
|               |                    |            |       |              |        |          |      | els. Documents |           | can be         | represented | as    | either    | probability | vectors      |
| ------------- | ------------------ | ---------- | ----- | ------------ | ------ | -------- | ---- | -------------- | --------- | -------------- | ----------- | ----- | --------- | ----------- | ------------ |
| is a model    | that uses Word2Vec |            | along | with         | LDA to | discover | the  |                |           |                |             |       |           |             |              |
|               |                    |            |       |              |        |          |      | that offer     | an easier | interpretation |             | or as | embedding |             | vectors that |
| topics behind | a set of           | documents. |       | The word2vec |        | model    | [49] |                |           |                |             |       |           |             |              |
areeasierforanetworktohandle.
| initially | assigns vectors | to words | randomly |     | and | then changes |     |          |           |     |        |         |               |     |            |
| --------- | --------------- | -------- | -------- | --- | --- | ------------ | --- | -------- | --------- | --- | ------ | ------- | ------------- | --- | ---------- |
|           |                 |          |          |     |     |              |     | The main | advantage |     | of NTM | is that | the inference |     | problem is |
thesevectorstooptimize(maximize)anobjectivefunction.
In word2vec [49], we start by specifying a window size and formulated as an optimization problem. This formulation makes
thenslidethiswindowoverthewordsinthedocument.Apivot it easier to optimize for specific aspects such as coherence [56].
is first chosen within the window, and all other words inside It also allows for joint training with other DNNs. Moreover, this
allowsNTMstoscaletobiggercorporaandmorecomplexmodels.
| the window  | are considered        | the | context.       | The | objective  | is          | to de- |             |               |          |         |                  |            |     |              |
| ----------- | --------------------- | --- | -------------- | --- | ---------- | ----------- | ------ | ----------- | ------------- | -------- | ------- | ---------------- | ---------- | --- | ------------ |
|             |                       |     |                |     |            |             |        | In Bayesian | probabilistic |          | models, | inference        | algorithms |     | must be      |
| velop a     | vector representation |     | that maximizes |     | the        | probability | of     |             |               |          |         |                  |            |     |              |
|             |                       |     |                |     |            |             |        | customized. | They          | tend     | to get  | more complicated |            | as  | models get   |
| the context | words given           | the | pivot. This    | is  | called the | skip-gram   |        |             |               |          |         |                  |            |     |              |
|             |                       |     |                |     |            |             |        | complex.    | In NTM,       | however, | the     | inference        | problem    |     | is easier to |
word2vec.
computeandparallelize.
InLDA2VEC[47],weaddadocumentvectortothepivotword,
Encoderanddecodernetworks,respectivelymodel
| both used | to obtain the | context | vector. | This | context | vector | is  |     |     |     |     |     |     |     |     |
| --------- | ------------- | ------- | ------- | ---- | ------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
TheinferenceandgenerativeprocessesinNTMs.Theencoder
thenusedtopredictcontextwords.Theobtainedvectorisdense,
|     |     |     |     |     |     |     |     | learns θ | where | z = θ(b); | the | projection | parameters |     | from the |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ----- | --------- | --- | ---------- | ---------- | --- | -------- |
makingithardtointerpretitsmeaningandultimatelymakedeci-
sionsoffit.LDA2VECthusdecomposesthedocumentvectorinto observeddocumentbtoitslatentrepresentationz.Thedecoder
|     |     |     |     |     |     |     |     | φ   |     | =   | φ(z,T); |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | --- | --- | --- | --- |
twocomponents:topicmixtureweightsandatopicmatrix.The learns where b the projection parameters from
mixtureweightsaresparsevectorsthatcanbeinterpreted.This the latent document representation to the observed document
is achieved by enforcing Dirichlet priors on the vector weights representation,T isthecollectionofworddistributionsofallthe
| to regularize | the model. | The | document | context |     | makes | better | topics. |     |     |     |     |     |     |     |
| ------------- | ---------- | --- | -------- | ------- | --- | ----- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- |
predictionsthanamodelthatonlyconsiderslocalcontext.Italso The learning process optimizes the ELBO, which is a lower
canlearnbetterwordvectorrepresentationsofaspeciallexicon. boundonthelog-marginallikelihoodoftheobserveddocument
|     |     |     |     |     |     |     |     | representation. |     | This optimization |     | is equivalent |     | to finding | an ap- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ----------------- | --- | ------------- | --- | ---------- | ------ |
AnothermodelthatusesembeddingsisETM[8],whichiscon-
proximatesolutiontotheposteriorprobabilitydistribution.
sideredavariantofLDAthatincorporatesneuralcomponents.In
|     |     |     |     |     |     |     |     | Different | NTMs | have | a different | configuration |     | of  | the prior |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---- | ---- | ----------- | ------------- | --- | --- | --------- |
ETM,thegeneratedtopicmixtureispulledfromalogisticnormal
distributionofz,theposteriordistribution,andtheobserveddata
| distribution, | and words | per | topic are | drawn | by projecting |     | the |     |     |     |     |     |     |     |     |
| ------------- | --------- | --- | --------- | ----- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
topicvectorontothevocabularyvector.Itperformsstate-of-the- distribution.Aswiththecaseofprobabilisticmodels,someNTMs
artresultsandprovidesmoreinterpretabletopics.ETMdoesnot considerthesequenceofwordsandthecorrelationbetweentop-
requiretheremovalofstopwordsandrarewords,unlikeLSI,LDA, ics.Someincorporatedocuments’metadata,whileothersaddress
and CTM. It performs well as the corpus vocabulary increases, shorttextdocuments’sparsity.Forexample,[9],usesDirichletas
especiallywithrareandstopwordsleftinthevocabulary. apriordistributionforz.Tocomputethegradientoftheexpecta-
Anotherutilizationofwordembeddingswasillustratedin[50]. tioninELBO,theauthorsapplytheLaplaceapproximation,where
This work focuses on the effect of auxiliary word embedding to Dirichlet samples are approximated by samples from a logistic
6

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
|     |     |     |     |     |     | Fig.2. | Topicmodelsevaluationcriteria. |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------ | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
normal distribution whose mean and co-variance are specifi- words for each topic. Then they calculated an asymmetric- sim-
callyconfigured.TheyusedtheirinferencemethodinProdLDA;a ilaritymeasurebetweenallcombinationsofwordpairs.Theau-
topicmodelinwhichthedistributionoverindividualwordsisa thorsexperimentedwithdifferentsimilaritymeasuresandfound
productofexpertsratherthanthemixturemodelusedinLDA. mutualinformationtobethemostconsistentperformer.Finally,
|     |     |     |     |     |     |     |     | they aggregate | all | obtained | pairwise | scores | (45 | scores) using | an  |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | -------- | -------- | ------ | --- | ------------- | --- |
aggregationfunctionsuchasthemeanormedian.
5. Evaluationmetrics
|     |     |     |     |     |     |     |     | The pointwise |     | mutual | information, |     | PMI, between | word | pair |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ------ | ------------ | --- | ------------ | ---- | ---- |
(wi,wj)iscalculatedasbelow
| Topic | models | can be | applied | in various | application |     | domains. |     |     |     |     |     |     |     |     |
| ----- | ------ | ------ | ------- | ---------- | ----------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
So, they can be evaluated extrinsically according to how they log p(w, w)
|     |     |     |     |     |     |     |     | (w , | w = |     | i j |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
performinthedomainwheretheywereapplied[57,58].Theycan PMI i j ) p(w)p( w) (5)
alsobeevaluatedintrinsicallybyconsideringthegeneratedtopics i j
themselves. Intrinsic evaluation is independent of any specific For the above equation. PMI, too, must be normalized. Note
domain and is thus more general. The different models differ thatthePMIcanonlybeevaluatedafterasolutionisobtained.Al-
ternatively,theinterpretabilitycanbeoptimizedfromthebegin-
insimplicity,computationefficiency,andmodelingassumptions.
ningbyconsideringadifferentmeasuresuchasWordEmbedding
Theyaccordinglydifferinhowtheyperformondifferentcorpora
|     |     |     |     |     |     |     |     | Topic Comprehension, |     | WETC | [56]. | It is | also important |     | to high- |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------- | --- | ---- | ----- | ----- | -------------- | --- | -------- |
anddifferentapplications.
lightthetrade-offbetweenperplexityandcoherence.Optimizing
| There | is little | consensus | on the | aspects | of  | topic model | eval- |     |     |     |     |     |     |     |     |
| ----- | --------- | --------- | ------ | ------- | --- | ----------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
perplexityusuallyresultsindecreasedcoherence[62].Notethat
| uation. There | have | also | been different |     | methods | to evaluate | a   |                  |     |         |            |     |            |           |        |
| ------------- | ---- | ---- | -------------- | --- | ------- | ----------- | --- | ---------------- | --- | ------- | ---------- | --- | ---------- | --------- | ------ |
|               |      |      |                |     |         |             |     | hyperparameters, |     | such as | the number |     | of topics, | will also | affect |
specificaspect.Thispaperreviewsacomprehensivedistilledset
| of evaluation | criteria     | and               | their methods. |     | The evaluation |       | criteria   | thismetric. |     |     |     |     |     |     |     |
| ------------- | ------------ | ----------------- | -------------- | --- | -------------- | ----- | ---------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
| discussed     | are quality, | interpretability, |                |     | stability,     | topic | diversity, |             |     |     |     |     |     |     |     |
efficiency, and flexibility (Fig. 2). Note that preprocessing stages 5.3. Topicdiversity(uniqueness)
beforefeedingthecorpustothetopicmodelimpacttheoutcome.
|              |     |           |     |        |       |           |        | This metric | describes |     | how semantically |     | diverse       | the obtained |         |
| ------------ | --- | --------- | --- | ------ | ----- | --------- | ------ | ----------- | --------- | --- | ---------------- | --- | ------------- | ------------ | ------- |
| For example, | it  | is common | to  | remove | words | that have | little |             |           |     |                  |     |               |              |         |
|              |     |           |     |        |       |           |        | topics are. | One way   | to  | define diversity |     | is introduced | in           | [8]. It |
topicalcontent,suchas‘‘the’’,‘‘and’’,and‘‘if’’.
|     |     |     |     |     |     |     |     | defines topic | diversityas |     | the percentage |     | of unique | wordsin | the |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | ----------- | --- | -------------- | --- | --------- | ------- | --- |
top25wordsofalltopics.Atopicmodelshouldgeneratediverse
5.1. Qualityandperplexity
topicsandscorehighonthismetric.Alowscoreindicatesredun-
danttopics,meaningthemodelcouldnotsufficientlydisentangle
| Perplexity | measures |     | the model’s | capability |     | to generate | the |     |     |     |     |     |     |     |     |
| ---------- | -------- | --- | ----------- | ---------- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
thecorpus’sthemes.Notethatselectinganumberoftopicsinthe
| documents | in corpus | based | on  | the learned | topics. | It  | measures |     |     |     |     |     |     |     |     |
| --------- | --------- | ----- | --- | ----------- | ------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
modelaffectsthetopicdiversity.Atoolargenumbercouldresult
| the model’s | predictive |     | power but | not | the latent | structure, | so  |     |     |     |     |     |     |     |     |
| ----------- | ---------- | --- | --------- | --- | ---------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
insimilartopicswithoverlappingtopwords.Atoosmallnumber
perplexity only shows how well the model explains the data. A couldresultinbroadtopicswithpoorinterpretability.
modelisperplexediftheinformationgainoflearningtherandom
variable’soutcomeissmall,sothelowertheperplexity,thebetter
|           |               |     |              |            |     |     |           | 5.4. Stability:Topicsimilarityacrossruns |     |     |     |     |     |     |     |
| --------- | ------------- | --- | ------------ | ---------- | --- | --- | --------- | ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
| the model | in explaining |     | the observed | documents. |     | The | posterior |                                          |     |     |     |     |     |     |     |
probabilitycalculationcanbeoptimizedforperplexity.
Oneofthesalientchallengesintopicmodelingistopicinsta-
| Note        | that perplexity |       | must be    | normalized |           | to the vocabulary |     |               |       |      |            |         |     |        |          |
| ----------- | --------------- | ----- | ---------- | ---------- | --------- | ----------------- | --- | ------------- | ----- | ---- | ---------- | ------- | --- | ------ | -------- |
|             |                 |       |            |            |           |                   |     | bility, which | means | that | top topics | ranking | can | change | signifi- |
| size in the | corpus          | since | it changes | with       | different | corpus            | and |               |       |      |            |         |     |        |          |
cantlyoverdifferentruns.Moreover,documents’assignmentsto
| topic sizes. | This | dependence | on vocabulary |     | size | makes | it harder |     |     |     |     |     |     |     |     |
| ------------ | ---- | ---------- | ------------- | --- | ---- | ----- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
differenttopicscanvarythroughouttheexperiments.Forexam-
| to compare | different | models. | A   | method | to estimate | the | proba- |     |     |     |     |     |     |     |     |
| ---------- | --------- | ------- | --- | ------ | ----------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
ple,LDAsuffersfrominstabilityduetoordereffects,i.e.,different
bility of held-out documents indicative of the model quality is inputorderingscanleadtodifferentgeneratedtopics.Thisresults
proposedin[59].Theirmethodcanbeusedtocomparedifferent in user confusion or, in the case of using TM for classification,
models quantitatively. Note that models with low perplexity do resultsinthedeteriorationoftheclassifier[31].
notnecessarilygeneratehuman-interpretabletopics. To quantify stability, several metrics were proposed. The
essenceistomeasurethesimilaritybetweentopicsacrossseveral
5.2. Interpretabilityandtopiccoherence runs. Notice that topics are represented by their top n words.
|     |     |     |     |     |     |     |     | More model | stability | is obtained |     | if similar | topics | are generated |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --------- | ----------- | --- | ---------- | ------ | ------------- | --- |
Atopicisadiscretedistributionoverwords.Thissetofwords
|     |     |     |     |     |     |     |     | across different | runs. | The | previous | approach |     | requires no | exper- |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | ----- | --- | -------- | -------- | --- | ----------- | ------ |
isevaluatedforbeinghuman-interpretable.Forthistooccur,the tise in the domain to which topic models are applied. Human
generated words should be associated with a single semantic judgment and PMI similarity measures require either direct or
meaning.Onewayofassessingtheinterpretabilityistoevaluate indirect expert knowledge, respectively. One way to measure
the coherence of the words in the generated topic as in [60], stability is to use the median Jaccard similarity of generated
and[61]. topics-topnwords-betweenrunsacrossalltopics[31],and[63].
In[61],coherenceisassessedbyobservingthelexicalsimilar- Jaccard similarity considers the intersection between the top n
itybetweenpairsofwords.Theirapproachconsideredthetop10 words in any two generated topics. It does not consider their
7

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
order.Alternatively,[64]proposedRankBiasedOverlap(RBO)to using any distance metric such as Jensen–Shannon Divergence
measuretopicstabilityasintheequationbelow. (JSD).
NLP leverage TM. In [57], the authors applied TM for word
x 1− p ∑ p x
RBO(T , T , p, d) = d .pd + i .pi (6) sense discrimination. Also, [58] used TM for document summa-
1 2
d p i rization,and[67]useditfortextsegmentation.TMhasalsobeen
i=1
usedinothertaskssuchasdiscoursesegmentationandmachine
where T1 and T2 represent an ordered list of top n words in
translation.
any two topics (across different runs), d is the evaluation depth
The representation can also aid humans in making sense of
typicallysetto10aswecomparethetop10words.x istheinter-
d large sets of documents and thus can serve in many disciplines,
sectionbetweenT1andT2atdepthd.pcontrolshowthemetric
varying from genetics to education, economics, sociology, and
isaffectedbytheorder.Settingpto1removesalldependenceon
more. Owing to their interpretability, topic models can help
order so that the metric considers only the intersection. Setting
scholars from different disciplines explore their data. For ex-
p to smaller values gives more weight to the order of words.
ample, by leveraging the power of social media, Topic models
Typically,avalueof0.9isusedassuggestedbytheauthors[64].
have been used to understand what people are saying about a
Asolutiontoaddressinstabilitywaselaboratedin[65]where
company [68,69]. In the transportation field, researchers used
differentensemblelearningstrategiesweretestedinthecontext
TM to explore the trends in the field [69,70]. Using LDA, the
of matrix factorization. Among all strategies, the K-Fold ensem-
authors of [70] aggregated topics over time. Hence, they could
ble method has achieved the best results. Another solution was
recognize general trends, like sustainability and travel behavior
proposedin[66].Theauthorsrealizethatovercominginstability
andsomeothertemporaltrends.Accordingly,thispaperprovides
can be done through careful initialization of the model hyper-
theresearchcommunitywithtrends,researchareas,andgapsin
parameters. They used differential evolution (DE) to optimize
thetransportationfield.
the selection of hyperparameters. They reported topic stability
TMhasalsobeenusedineconomics.Forexample,in[71],an
-measuredwithJaccardsimilarity-ofnearly88%ormore.
investigation of economics’s historical evolution over a specific
timewindowanditschangingstructurewasdiscussed.Theidea
5.5. Efficiency;computationandmemorycomplexity
istotrackthemostrelevanttopicsdiscussedbyeconomistsover
eachdecadeofthetwentiethcentury.Moreover,aweb-basedin-
In latent variable models, the computation of the posterior
teractivetoolcalled‘‘LDAvis’’isdevelopedtovisualizethetopics.
distribution is always intractable. So, we use approximate solu-
Insoftwareengineering(SE),topicmodelshavebeenusedinSE
tions such as Markov Chain Monte Carlo (MCMC) or variational
taskssuchassourcecodeanalysis[72],testing[73],requirements
inference. We may also try to estimate it by sampling methods
engineering[74],softwarearchitecture[75],andothers.Coming
(Gibbs sampling) which tend to be faster to develop and run.
to the field of bioinformatics, the authors of [76] reviewed the
Variationalinferenceiseasiertoparallelize.Differentalgorithms
applications of TM in the field. In [77], the bioinformatics field
differ in their computation time complexity. Thus, computation
isanalyzedwhereas[78]analyzedgenesequencedatausingTM,
complexity is a metric used to assess and compare different
and [79] used TM to classify gene expression data. In medicine,
models.
with the large scale of documents, it is becoming progressively
Sincetopicmodelsusuallydealswithlargecorporathatmay
hard to find relevant documents. In [44], a novel fuzzy TM ap-
not fit in memory. Radim Řehůřek, [66] proposed a software
proachwasusedtowardachievingthis.Numerousotherresearch
framework based on the idea of document streaming. Their
papersleveragedTMsuchas[80,81]incommunicationresearch,
framework implemented an LDA inference algorithm indepen-
and [82] who discovered business intelligence specifically for
dentofthecorpussize.
airlines by applying topic models to documents of customers’
reviews.
5.6. Flexibility
Duetothelong-taileddistributionoflanguages,topicmodels
This evaluation aspect is not measurable quantitatively. It is in big data sets need to learn a large number of coherent word
worth noting that different models have different capacities to sets(topics).Thislargenumberoftopicsistoobigtocomprehend
deal with text corpora exhibiting different characteristics. The byhumans.In[83],industrialapplicationssuchassearchengines
required preprocessing steps and the distribution of words in and online advertisement systems use LDA-based TM with at
documents, for example, impact the performance. Some models least105topicstoservemillionsofusers.
can train jointly with others or can be optimized for certain
aspects,suchascoherence. 6.2. Softwaretools
6. Topicmodelstoolsandapplications Many available software tools implement various topic mod-
els. Most open software tools implement LDA and LSI, whereas
Topic models have applications in several disciplines, from manyothermodelslackopen-sourceimplementationexceptfor
NLP to bioinformatics. In the following subsections, a review is afewexceptions[84,85].
introduced. Some of the early popular software tools was the Stanford
TopicModelingToolbox(TMT),whichaddressessocialscientists.
6.1. Topicmodelingapplications ItwaswrittenusinganoldversionofScalaandisnolongersup-
ported.Othertoolboxesandsoftwareframeworksarepresented
Topic models represent documents in terms of their topics. inTable2anddescribedbriefly.Gensimprovidesparallelizedim-
This representation can be used as features for other machine plementations of several models and can accommodate corpora
learning models, for example, document classification models. larger than the memory. It also provides storage for many text
Thesetopicalfeaturesusuallyaugmenttheengineeredfeaturesas datasetsaccessiblethroughastandardAPI.
aninputtoamodel.Thetopicaldistributioncanalsobeusedto Datacleaningiscrucialbeforefeedingthedatatoamodel.For
assesstheentropyofadocumenttoevaluateitsinformationrich- eachmodel,aplaywithhyperparametersandthepreprocessing
nesswhichisusedininformationretrievaltasksasafeature.Text steps can dramatically affect the quality of the obtained topics.
matchingcancomparethetopicaldistributionsoftwodocuments Basic cleaning steps are tokenization, removal of stop words,
8

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
Table2
Availableopen-sourcelibraries.
Tool Interface Models Workflow Pros Cons
Malleta Consoleapp. LDA,PAM,HLDA. Representdocumentsasastring, Userfriendliness. Limitedfinegrain
thenclean(usestdorextrastop control.
wordlistsoruseRegExp)and
import.Finally,train(choose
hyperparameters(#topics,alpha,
andbeta,#iterations)
Gensimb PythonAPI. LSI,LDA. Representdocumentsasastring, Highlyoptimized,memory Harder.
clean,thenrepresentdocumentsbya independent,andallowsforfine
featurevector,thenapplythemodel. controltotweakthemodels.
Familiac PythonAPI. LDA,SentenceLDA, Representdocumentsasastring, Itoffersreadytopicmodels Memorylimitations
Topicalword clean,andthencallappropriate trainedinlargeindustrialcorpora.
embedding. off-the-shelftrainedmodelusingthe Itofferstwomodels’
properAPIfunction. implementationbeyondLDA
OCTISd Python LSI,NMF,LDA,HDP, Useanavailabledataset,or Oneinterfacetorunmanytopic Notallmodelsare
package. ETM,CTM, customizeyours.Setthemodel models.Itestimatesoptimal available.Sacrifices
NeuralLDA,ProdLDA hyperparametersandtrain. hyperparameters. detailsforusability.
ahttp://mallet.cs.umass.edu/index.php.
bhttps://radimrehurek.com/gensim.
chttps://github.com/baidu/Familia.
dhttps://github.com/MIND-Lab/OCTIS.
and stemming. Tokenization decomposes the document into its different models evaluate them using different datasets. More-
constructs, usually words. Stop words are these words that do over, many papers report only a few of the evaluation metrics
not count as ‘constructs’ since they have little topical content, we mentioned in Section 5. The choice of hyperparameters and
suchas‘‘the’’,‘‘and’’,‘‘if’’.Theyaremeaninglesstothemodeland theexistenceofseveralmodelvariantsofthesametopicmodel
arethusremoved.Thelistofstopwordsissubjectiveandusually
add to the list of challenges. In this section, we conduct experi-
depends on the corpus and the application. In [86], the authors
ments to compare several topic models from various categories
arguethatremovingstopwordspriortomodelinferenceprovides
across the proposed evaluation metrics. Seven topic models are
a superficial improvement. Alternatively, removing stopwords
considered; LSI and NMF from the algebraic category, LDA and
past model inference is more transparent and produces similar
HDPfromtheprobabilisticcategory,andETM,CTM,andProdLDA
results.Stemmingwordsreducesthemtotheirstems.Stemming
from the neural category. The results are evaluated across a
is important since words with the same stem have the same
topicalcontentand,thus,mustbeseenasthesamebythemodel. commonevaluationmetricsusingtheexactimplementation.The
Mallet and Gensim can generate different topics (even with the opensourceOCTISpythonpackage[85]isusedtoconductthese
same set of hyperparameters selected and the same order of experiments.
feeding documents). This difference is due to the differences in
theinternalsofpreprocessingstepsindifferentimplementations.
7.1. Experimentalsetup
Familia is more industry oriented. It provides off-the-shelf
topic models trained on large-scale industrial corpora. It can be
used in the industry for semantic representation or semantic Eachmodelisruntentimesusingthesameselectionofdefault
matchingtasks,suchasdocumentclassification,documentclus- hyperparameters. The models are run against two datasets; the
tering,andpersonalizedrecommendations.NotethatFamilia,for OCTIS preprocessed 20 newsgroups dataset containing 16309
example,usesseveraltopicmodelsfromdifferentcategories.For
documents and the OCTIS preprocessed M10 dataset containing
example, it implements LDA from the probabilistic category of
8355documents.Bothdatasetshavecomparablevocabularysizes
models and topical word embeddings from the neural category
(1612 for 20 newsgroups and 1696 for M10). However, the av-
ofmodels.
erage word count per document is 48.02 for the 20 newsgroups
OCTIS or Optimizing and Comparing Topic Models is Sim-
dataset and 5.91 for the M10 dataset. The M10 dataset thus has
ple![85]providesaunifiedinterfacetotrainvarioustopicmodels
shorter documents and a larger number of rare words. Fig. 3
and optimize the selection of their hyperparameters. Various
models from algebraic, probabilistic, and neural categories are shows the number of words in vocabulary for each number of
available.OCTISalsocontainsarepositoryofpublicpreprocessed occurrences.
datasetsreadilyavailabletoloadandexperimentwith. The generated topics by the models are assessed for their
stabilityacrosseverytwosuccessiveruns.TheRankBasedOver-
6.3. Datasets lap (RBO) metric discussed in 5.4 is used to measure stability.
NormalizedPMIisusedtomeasurecoherence,andtopicdiversity
Tables 3 and 4 present some publicly available datasets for ismeasuredconsideringtheuniquetokensinthetop10words.
topic modeling. Note that the 20 Newsgroup dataset has been
The average score across the runs is reported for coherence,
particularlyusedasabenchmarkdataset[87,88].Moreover,itis
diversity, and computation time. The perplexity metric is not
observed that the other mentioned datasets are often used in a
evaluated in this experiment since non-generative models, such
limitednumberofresearchpublications.
asLSIandNMFwillnothaveadefinedperplexityscore.Notethat
7. Comparisonofmodels perplexitymetricisnotcorrelatedwithhumanjudgment[62].
Notethatallmodelsacceptthenumberoftopicsasahyper-
It is challenging to have a fair comparison between different parameterexceptfortheHierarchicalTopicModel(HDP),which
topic models. One challenge is that different papers proposing automaticallyinfersthenumberoftopicsinthecorpus.Notealso
9

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
Table3
Availablelongtextdatasets.
| Dataset | Description | Size | NO.oftopics | Language | Date |
| ------- | ----------- | ---- | ----------- | -------- | ---- |
Scientificjournal Articlesfrom22leadingtransportation 17,163articles 50 English From1990to2015
| articles | journals |     |     |     |     |
| -------- | -------- | --- | --- | --- | --- |
Economics 188economicsarticlesstoredintheJSTOR 250,846articles 25,50and100 English From1845to2013
| articlesa | database |     |     |     |     |
| --------- | -------- | --- | --- | --- | --- |
20Newsgroupsb
|     | Acollectionofnewsgroupdocuments, | 20000posts | 20  | English | 2008 |
| --- | -------------------------------- | ---------- | --- | ------- | ---- |
partitionedacross20differentnewsgroups
M10c
[89] Publicationsfrom10distinctresearchareas 10,310publications. 10 English –
queriedfromCiteSeerXusingthekeywords
fromMicrosoftAcademicSearch.
Applications GooglePlayArabicApplicationsnamesand 7657appdescriptions 10 Arabic –
| Information | descriptions |     |     |     |     |
| ----------- | ------------ | --- | --- | --- | --- |
NIPSd
AcollectionofallpapersfromNIPSMachine 1566documents 20and50 English From1988to2003
learningconference
ahttps://www.jstor.org/.
bhttp://qwone.com/jason/20Newsgroups/.
chttp://citeseerx.ist.psu.edu/.
dhttps://cs.nyu.edu/roweis/data.html.
Table4
Availableshorttextdatasets.
| Dataset | Description | Size | No.ofinferredtopics | Language | Date |
| ------- | ----------- | ---- | ------------------- | -------- | ---- |
The20-topics Tweetsfrom1200prominentTwitteraccounts. 4,170,382tweets 20 English FromMarch2015
| dataset |     |     |     |     | toFebruary2016 |
| ------- | --- | --- | --- | --- | -------------- |
Real-world SnippetsofanEnglishsearchengine. 12,340Websearch 8 English 2008
| snippets |     | snippets |     |     |     |
| -------- | --- | -------- | --- | --- | --- |
BaiduQAa QuestionsfromQ&AserviceinChinese) 648,514questions 35 Chinese –
Weibob
PostsfromWeibocommonlyreferredtoas 719,570posts – Chinese FromJanuary1to
|     | ‘‘ChineseTwitter’’,isamicro-bloggingsite. |     |     |     | June30,2020 |
| --- | ----------------------------------------- | --- | --- | --- | ----------- |
ahttps://zhidao.baidu.com/.
bhttps://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DULFFJ.
Fig.3. Datasetsexhibitdifferentworddistributions.Notethedifferenceinthey-axisscalebetweenthecharts.
that the ‘‘bert-base-nli-mean-tokens’’ bert model is used in the 8. Discussionandanalysis
zero-shotinferencetypemodelvariantforCTM.
|     |     | 8.1. Themodels |     |     |     |
| --- | --- | -------------- | --- | --- | --- |
7.2. Results
Examiningtheresults,itisevidentthatthemodels’scoresvary
TheobtainedscoresareshowninTables5and6. considerably and that no one model or model family performs
InTable7,welistthebestandworstperformingmodelsacross best in all aspects. For example, the result of LSI against the 20
theevaluatedmetrics. newsgroupsdatasetachievesthesecondworstscoresindiversity
The box plots of the obtained results across the 10 runs are and coherence but the best scores in stability and computation
showninFigs.4and5. time. Moreover, the models’ performance varies with the input
10

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
Fig.4. Topicmodels’evaluationmetricsscoresacrosstenrunsagainstthe20newsgroupsdataset.
Fig.5. Topicmodels’evaluationmetricsscoresacross10runsagainsttheM10dataset.
Table5 Table6
Resultsofrunningthetopicmodelsagainstthe20newsgroupsdataset. ResultsofrunningthetopicmodelsagainsttheM10dataset.
Model Coherence Diversity Stability Time(s) Model Coherence Diversity Stability Time(s)
LSI 0.0128 0.4810 1 3.2521 LSI −0.0235 0.546 1 1.6136
NMF 0.0821 0.6945 0.8163 4.8802 NMF −0.0311 0.713 0.6014 2.3121
LDA 0.0575 0.7105 0.7257 8.0566 LDA −0.0604 0.627 0.692 2.2156
HDP −0.1604 0.6264 0.8942 24.4717 HDP −0.5049 0.668 0.3194 7.3764
ETM 0.0395 0.3775 0.8942 45.9766 ETM −0.0014 0.383 0.8641 32.9827
CTM 0.0747 0.8900 0.6967 23.981 CTM 0.0197 0.98 0.7739 12.0966
ProdLDA 0.0552 0.8785 0.6266 27.3077 ProdLDA −0.0017 0.971 0.7881 12.7665
11

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
Fig.6. DiversityscoresversusStabilityscoresoftheexaminedtopicmodels.
Table7 the document level. NMF maintains its rank above LDA, which
Bestperformingmodelsacrosstheevaluatedmetrics.
|     |     |     |     |     |     | is consistent | with [65,90], | who | found | that | NMF is | more likely |
| --- | --- | --- | --- | --- | --- | ------------- | ------------- | --- | ----- | ---- | ------ | ----------- |
Evaluationmetric Bestmodels Worstmodels to generate better coherent topics than LDA. Finally, we note
Coherence CTM HDP thatneuralmodels’coherencescoresarenotalwaysbetterthan
Diversity CTMandProdLDA ETM algebraicorprobabilisticclassicalmodels.
| Stability |     | LSIandETM |     | CTMandProdLDA. |     |     |     |     |     |     |     |     |
| --------- | --- | --------- | --- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- |
HDP,NMF,andLDAin
|            |     |         |     | shortdocumentsdatasets. |     | 8.1.2. Diversity |                    |         |            |             |        |           |
| ---------- | --- | ------- | --- | ----------------------- | --- | ---------------- | ------------------ | ------- | ---------- | ----------- | ------ | --------- |
|            |     |         |     |                         |     | For diversity,   | the                | results | of running | the         | models | on both   |
| Efficiency |     | LSI,NMF |     | ETM                     |     |                  |                    |         |            |             |        |           |
|            |     |         |     |                         |     | datasets         | are similar, apart | from    | a slight   | degradation |        | of LDA on |
theM10dataset.Thebestmodel(CTM)scoresclosetothesecond
|     |     |     |     |     |     | best (ProdLDA). | NMF, | LDA, and | HDP | come next. | LSI | is again the |
| --- | --- | --- | --- | --- | --- | --------------- | ---- | -------- | --- | ---------- | --- | ------------ |
dataset in some metrics. For example, the ETM coherence score second worst model, and it only outperforms ETM. In [7], the
ranksfifthonthe20newsgroupsdataset.However,ETMachieves reporteddiversityscores,obtainedfromrunningvariousmodels
thesecond-bestcoherencescoreontheM10dataset.Alsonotable againstthe20newsgroupsdataset,showthatCTMachievesthe
isthevariabilitybetweenruns,owingtothestochasticnatureof best diversity, outperforming LDA and NMF, which is consistent
| manymodels. |     |     |     |     |     | withourobtainedresults. |     |     |     |     |     |     |
| ----------- | --- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- | --- |
Itisobservedthatarelationshipexistsbetweenstabilityand
| diversity, | which | is more observable |     | with the | 20 newsgroups | 8.1.3. Stability |     |     |     |     |     |     |
| ---------- | ----- | ------------------ | --- | -------- | ------------- | ---------------- | --- | --- | --- | --- | --- | --- |
dataset. As the model stability goes up, its generated topics are On both datasets, LSI achieves maximum stability and is fol-
lessdiverse.Wehypothesizethatitischallengingformodelsto lowed by ETM. LDA results are consistent in both datasets. HDP
generatediversetopicswithoutcompromisingtheirstabilityand achievesahighstabilityscoreonthe20newsgroupsdatasetand
thatdiversificationisdependent,atleastinpart,onthestochastic alowstabilityscoreontheM10dataset.NMFstabilityscorealso
natureofthemodelingalgorithms.Fig.6showsascatterplotof
degradedfrom82%to60%.Finally,CTMandProdLDAachievethe
models’diversityversusstabilityscoreswithafittedlineartrend
|       |     |     |     |     |     | worst and                                            | second worst | stability | scores | on  | the 20 | newsgroups |
| ----- | --- | --- | --- | --- | --- | ---------------------------------------------------- | ------------ | --------- | ------ | --- | ------ | ---------- |
| line. |     |     |     |     |     | datasetbutachieveahighstabilityscoreontheM10dataset. |              |           |        |     |        |            |
Inthefollowingsections,weconsiderevaluationmetricsand In general, on the 20 newsgroups dataset, neural models’
explorethespectrumofscoresachievedbythemodels. stabilityscoresarepoorcomparedtoclassicalmodels.Thiscon-
|     |     |     |     |     |     | clusion | agrees with the | findings | of  | the authors | of  | [91], who |
| --- | --- | --- | --- | --- | --- | ------- | --------------- | -------- | --- | ----------- | --- | --------- |
8.1.1. Coherence conductedanempiricalstudytocompareneuralmodelstoclas-
The 20 newsgroups dataset results show that NMF achieves sical models such as LDA and NMF. The authors considered the
the best score, followed by CTM. Next are LDA and ProdLDA, neural models that are based on encoder–decoder architecture
andbothmodelsscoreclosetoeachother.ETMachievesmodest andwhosedecoderscanworkwithabagofwordsrepresentation
results and then comes LSI, which only outperforms HDP. HDP of documents such as ProdLDA [9]. The authors concluded that,
scores the worst coherence. The results of all models on the compared to classical models, neural models are generally less
M10 dataset are generally less than the 20 newsgroups dataset stable, and their performance will vary significantly from run to
| in coherence | scores. | Moreover, | on the | M10 dataset, | the models | run. |     |     |     |     |     |     |
| ------------ | ------- | --------- | ------ | ------------ | ---------- | ---- | --- | --- | --- | --- | --- | --- |
aredifferentlyranked,whichisattributedtothedifferentdataset However,neuralmodels’stabilityscoresareimprovedonthe
characteristics. The difference in performance is noted in the M10 dataset. This observation could suggest that neural topic
scores of ETM, NMF, and LDA models. Excluding these models models outperform classical topic models in stability scores for
fromthelistofconsideredmodelswillresultinthesameranking datasets with short documents and a high percentage of rare
| ofmodelsonbothdatasets. |     |     |     |     |     | words. |     |     |     |     |     |     |
| ----------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- | --- |
TheabundanceofrarewordsintheM10datasetcouldresult Since topic models exhibit instability in their results if they
in the improvement of the performance of ETM compared to have stochastic elements in any of their steps, deterministic al-
othermodels.Theexistenceofrarewordsandshorterdocuments gorithms such as LSI are very stable and score maximum stabil-
couldalsodegradetheperformanceofNMFandLDAduetodata ity. LSI gives the same output every time it is run. In practice,
sparsityperdocument.Thisdegradationisbecausebothmodels there could be a slight variability with LSI-generated topics due
uncover topics by observing the word co-occurrence patterns at to implementation differences in Singular Value Decomposition
12

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
(SVD) computation. The exact implementation is used in this 8.3. Researchtrends
experiment,sonovariabilityisobserved.
NMF exhibits instability due to the random initialization in Probabilistic models enjoyed several years of research fol-
the implemented algorithm. Note, however, that apart from the lowing the advent of LDA in 2003. It was later extended in
examinedNMFvariant,thereisanotherNMFvariantthatusesa several ways to offer better corpora modeling, such as those
| non-random | initialization |     | approach, | namely, | Non-negative |     | Dou- |     |     |     |     |     |     |     |     |
| ---------- | -------------- | --- | --------- | ------- | ------------ | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
spanningalargetimeframeorthoseinvolvingshortdocuments.
bleSingularValueDecomposition(NNDSVD)[92],whichchooses
|     |     |     |     |     |     |     |     | The limited | interpretability |     | of  | the models | grabbed | the | attention |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ---------------- | --- | --- | ---------- | ------- | --- | --------- |
initialfactorsbasedonasparseSVDapproximationoftheoriginal
|     |     |     |     |     |     |     |     | of researchers |     | to design | better | models | with | better | coherence |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | --------- | ------ | ------ | ---- | ------ | --------- |
datamatrix.Inthiscase,theNMFalgorithmisdeterministicand
scores.Moreover,howthemodelsareevaluatedwasresearched
| thus very | stable | save for | SVD | implementation |     | details, | causing |           |        |          |      |         |            |          |      |
| --------- | ------ | -------- | --- | -------------- | --- | -------- | ------- | --------- | ------ | -------- | ---- | ------- | ---------- | -------- | ---- |
|           |        |          |     |                |     |          |         | to invent | better | metrics. | Fig. | 8 shows | the trends | observed | from |
slightvariability.
|     |          |               |     |        |           |           |       | the surveyed | papers. | We  | note | that although |     | research | in proba- |
| --- | -------- | ------------- | --- | ------ | --------- | --------- | ----- | ------------ | ------- | --- | ---- | ------------- | --- | -------- | --------- |
| LDA | requires | randomization |     | in the | inference | algorithm | (e.g. |              |         |     |      |               |     |          |           |
bilistictopicmodelingisstillactive,thefocusintheresearchhas
MCMCorvariationalinference)andaccordinglywillhaveinher-
shiftedtoneuralmodelsinthelastfiveyears.Inparticular,their
entinstability.
|     |     |     |     |     |     |     |     | flexibility | in jointly | training | them | with | other | models | and their |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ---------- | -------- | ---- | ---- | ----- | ------ | --------- |
scalability.Currently,researchintopolylingualmodelsisgaining
8.1.4. Efficiency
momentum.Ingeneral,transparencyofmachinelearningmodels
| Apart | from | ETM, the | computation |     | time is | stable | between |     |     |     |     |     |     |     |     |
| ----- | ---- | -------- | ----------- | --- | ------- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
runs. LSI, NMF, and LDA are the most efficient algorithms and hasbecomeahottopic,andtopicmodelingresearchfollowsthe
| run faster | than | HDP, CTM, | and | ProdLDA. | On average, |     | ETM takes | sametrend. |     |     |     |     |     |     |     |
| ---------- | ---- | --------- | --- | -------- | ----------- | --- | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
longerthananyothermodel.Theseresultsareconsistentinboth
datasets. This result agrees with [7,65] who conducted a study 8.4. Researchgaps
involvingseveralmodelsandfoundthatNMFisfastest,followed
by LDA, Top2Vec [93], BERTopic and finally CTM. Analytically, ThereareseveralresearchchallengesandopportunitiesinTM,
LSI complexity is O(mn2) to decompose the DTM of m rows whicharecategorizedintothreegroups.Bettermodels,automatic
(documents) and n columns (terms). In practice, truncated SVD evaluation, and data discovery. These research areas are illus-
is used since not all singular values are needed, which makes tratedasfollows.Someresearcheffortsgointobettermodelsthat
LSI very fast. LDA algorithm computational complexity varies provideimprovedstabilityandcoherence[95].Regularizationof
dependingontheeffectivenumberoftopicsperdocumentfrom the models and optimal selection of hyperparameters is also an
| polynomial-time |     | to NP-hard | [94] | which | is generally |     | faster than |                 |     |           |       |       |                  |     |        |
| --------------- | --- | ---------- | ---- | ----- | ------------ | --- | ----------- | --------------- | --- | --------- | ----- | ----- | ---------------- | --- | ------ |
|                 |     |            |      |       |              |     |             | area of ongoing |     | research. | While | other | researchdevelops |     | models |
neuralmodels(ETM,CTM,andProdLDA).Wenotethatdifferent
thatadaptbettertovariouscorporacharacteristics,suchasshort
| models’   | computation | times    | scale | differently | with | the         | number of |                |     |                     |     |            |     |          |            |
| --------- | ----------- | -------- | ----- | ----------- | ---- | ----------- | --------- | -------------- | --- | ------------------- | --- | ---------- | --- | -------- | ---------- |
|           |             |          |       |             |      |             |           | text documents |     | [96]. Computational |     | efficiency |     | is quite | essential, |
| documents | in the      | dataset. | For   | example,    | LDA  | computation | time      |                |     |                     |     |            |     |          |            |
whichaptlygrabstheattentionofsomeresearcherstoo[97].The
increasesmorerapidlycomparedtoNMF.
|     |     |     |     |     |     |     |     | use of deep | transformer-based |        |           | language | models       | to  | encode text |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----------------- | ------ | --------- | -------- | ------------ | --- | ----------- |
|     |     |     |     |     |     |     |     | documents   | has               | proved | effective | and is   | increasingly |     | deployed in |
8.2. Modelselection
NTM[98].
Anotherresearchareaisautomaticevaluation[99–101].While
Therearedifferentaspectstoconsiderwhenselectingatopic
|            |                 |        |        |             |             |       |            | human evaluation |         | is typically |         | considered | the   | gold       | standard in |
| ---------- | --------------- | ------ | ------ | ----------- | ----------- | ----- | ---------- | ---------------- | ------- | ------------ | ------- | ---------- | ----- | ---------- | ----------- |
| model for  | an application. |        | We     | propose     | to consider | four  | aspects    |                  |         |              |         |            |       |            |             |
|            |                 |        |        |             |             |       |            | NLP, it is       | usually | elaborate,   | costly, | and        | prone | to errors. | There       |
| pertaining | to the          | nature | of the | application | as          | shown | in Fig. 7. |                  |         |              |         |            |       |            |             |
These aspects specify the relative importance of the models’ exists no unified system of evaluation that researchers adopt.
evaluationcriteria.Oneaspectcheckswhetherthetopicmodel’s Different papers vary in their evaluation processes and metrics,
outputwillbeconsumedbyhumansormachinelearningmodels. which makes it harder to compare different models. Therefore,
Thecoherenceoftheoutputismorecriticalinthecaseofhuman there is a need for benchmarks and a unified evaluation system
consumption, such as the case in social sciences applications. If, oftopicmodels[85].
however, the topic model output is deployed in another down- Thelastareaofresearchismulti-disciplinaryapplications[82,
stream task and is consumed by a machine, interpretability and 102,103], where researchers from other disciplines, such as po-
hencecoherencearelesscritical.Anotheraspectchecksifacom- liticalscience[104],neuroscience[105],psychology[106],sociol-
prehensive coverage of input corpus is necessary. A diverse set ogy[107],bioinformatics[108],engineering[109]andmanyoth-
of generated topics is more likely to cover the available themes ers,usetopicmodelstoexploretheirdataandformhypotheses
| in the corpus, | which | is  | important | for applications |     | such | as text | aboutit. |     |     |     |     |     |     |     |
| -------------- | ----- | --- | --------- | ---------------- | --- | ---- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- |
summarizationandclassification.
| If the | application | involves |     | spatial or | temporal | analysis | or if |     |     |     |     |     |     |     |     |
| ------ | ----------- | -------- | --- | ---------- | -------- | -------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
9. Conclusionandfuturework
| it compares | between | different |     | datasets, | then | stability | is impor- |     |     |     |     |     |     |     |     |
| ----------- | ------- | --------- | --- | --------- | ---- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
tant.Thisimportanceisemphasizedmoreforapplicationswhose
|     |     |     |     |     |     |     |     | Topic | modeling | has | been | an active | area | of research | in the |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | -------- | --- | ---- | --------- | ---- | ----------- | ------ |
outputisconsumedbyhumans.Finally,iftheapplicationisinter-
pasttwodecades.Inthispaper,topicmodelsarecategorizedinto
activeortheinputcorpusisvast,themodel’sefficiencybecomes
fourcategoriesbasedontheirmodelingtechniques.Themodeling
important.
|       |      |            |     |                  |     |       |           | techniques | are | algebraic, | fuzzy,     | probabilistic, |           | and neural.      | Differ- |
| ----- | ---- | ---------- | --- | ---------------- | --- | ----- | --------- | ---------- | --- | ---------- | ---------- | -------------- | --------- | ---------------- | ------- |
| Apart | from | the nature | of  | the application, |     | there | are other |            |     |            |            |                |           |                  |         |
|       |      |            |     |                  |     |       |           | ent models | and | model      | categories | have           | different | characteristics. |         |
aspectstoconsiderwhenselectingatopicmodel.Oneaspectper-
|          |           |          |       |                 |     |     |            | They co-exist |                  | to serve | in different  |        | contexts | and     | on different |
| -------- | --------- | -------- | ----- | --------------- | --- | --- | ---------- | ------------- | ---------------- | -------- | ------------- | ------ | -------- | ------- | ------------ |
| tains to | the input | dataset, | whose | characteristics |     | can | impact the |               |                  |          |               |        |          |         |              |
|          |           |          |       |                 |     |     |            | corpora       | characteristics. |          | Probabilistic | models |          | provide | a straight-  |
models’performanceasmentionedin5.4.Forexample,datasets
withshortdocumentsarechallengingtotheclassicaltopicmod- forward interpretation but scaling them up to complex models
els,suchasLSIandLDA.Thesemodelsrevealtopicsbycapturing ischallenging.Ontheotherhand,neuralmodelsofferscalability
the word co-occurrence patterns at the document level; thus, andflexibilityandhencehavebeenthefocusofresearchefforts
they suffer from data sparsity. Also, in practice, the ease of use, in recent years. The models are evaluated against a set of cri-
availabilityofsoftwarepackages,andneedforrapiddevelopment teria to assess them. They are quality, interpretability, diversity,
playaroleindeterminingwhichtopicmodeltouse.Itisusually stability, efficiency, and flexibility. Using two common bench-
advisable to deploy a baseline model at first. LSI, NMF, and LDA markdatasets,weconductedexperimentstoevaluateseventopic
areamongstthemostcommonchoicesasabaselinemodel. modelsfromdifferentcategoriesacrosstheproposedcriteria.We
13

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
Fig.7. Fouraspectstoconsiderinapplicationstoidentifytherelativeimportanceofevaluationcriteria.
Fig.8. Evolutionoftopicmodelsaccordingtosurveyedpapers.
discussed how the performance changes due to different input in various disciplines ranging from medicine to literature and
datasetcharacteristics.Theevaluationcriteriaarecompeting,and beyond. To extend our study, future work to compare more
scoringhighinonecriterioncouldchallengetheothers,suchas models on several datasets exhibiting different characteristics is
the case with stability and diversity. Accordingly, we conclude required.Thiscomparisonwillhelpstratifydifferentusecasesin
that no single model achieves the best results in all criteria. We theindustryandhighlightkeymetricsforevaluation.
proposedconsideringfourkeyaspectsofthenatureofanappli-
cation to help determine which topic model to use. Evaluating Declarationofcompetinginterest
a topic model is challenging. Thus, research efforts are ongoing
to provide better metrics to evaluate the models automatically Theauthorsdeclarethattheyhavenoknowncompetingfinan-
andprovideaunifiedsetofbenchmarks,includingdatasets.Other cialinterestsorpersonalrelationshipsthatcouldhaveappeared
research goes into developing better models to generate more toinfluencetheworkreportedinthispaper.
coherent,diverse,andstabletopicsinacomputationallyefficient
manner. Another research direction is incorporating the rich se- Dataavailability
mantics representation of the pre-trained language models. Due
to their interpretability, topic models continue to be deployed Datawillbemadeavailableonrequest.
14

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
References [25] D.E. Klein, G.L. Murphy, The representation of polysemous words, J.
MemoryLang.45(2001)259–282.
[1] D.M.Blei,A.Y.Ng,M.I.Jordan,LatentDirichletallocation,J.Mach.Learn. [26] A. Anandkumar, R. Ge, D. Hsu, S.M. Kakade, M. Telgarsky, Tensor De-
|     |     |     |     |     |     |     |     | compositions | for | Learning | Latent | Variable | Models, | Tech. Rep., | Defense |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | -------- | ------ | -------- | ------- | ----------- | ------- |
Res.3(Jan)(2003)993–1022.
TechnicalInformationCenter,FortBelvoir,VA,2012,http://dx.doi.org/10.
[2] S.P.Crain,K.Zhou,S.-H.Yang,H.Zha,Dimensionalityreductionandtopic
modeling: From latent semantic indexing to latent Dirichlet allocation 21236/ADA604494.
|     |     |     |     |     |     |     |     | [27] D.D.Lee,H.S.Seung,Learningthepartsofobjectsbynon-negativematrix |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
andbeyond,in:C.C.Aggarwal,C.Zhai(Eds.),MiningTextData,Springer
|                |     |       |              |                                  |     |     |     | factorization, | Nature | 401 | (6755) | (1999) 788–791, |     | http://dx.doi.org/10. |     |
| -------------- | --- | ----- | ------------ | -------------------------------- | --- | --- | --- | -------------- | ------ | --- | ------ | --------------- | --- | --------------------- | --- |
| US, Boston,    | MA, | 2012, | pp. 129–161, | http://dx.doi.org/10.1007/978-1- |     |     |     |                |        |     |        |                 |     |                       |     |
| 4614-3223-4_5. |     |       |              |                                  |     |     |     | 1038/44565.    |        |     |        |                 |     |                       |     |
[3] S. Deerwester, S.T. Dumais, G.W. Furnas, T.K. Landauer, R. Harsh- [28] T. Shi, K. Kang, J. Choo, C.K. Reddy, Short-text topic modeling via
non-negativematrixfactorizationenrichedwithlocalword-contextcor-
| man,       | Indexing | by latent | semantic                                          | analysis, | J.  | Am. Soc. | Inf. Sci. 41 |            |                 |     |             |       |      |                |     |
| ---------- | -------- | --------- | ------------------------------------------------- | --------- | --- | -------- | ------------ | ---------- | --------------- | --- | ----------- | ----- | ---- | -------------- | --- |
|            |          |           |                                                   |           |     |          |              | relations, | in: Proceedings |     | of the 2018 | World | Wide | Web Conference | on  |
| (6) (1990) | 391–407, |           | http://dx.doi.org/10.1002/(SICI)1097-4571(199009) |           |     |          |              |            |                 |     |             |       |      |                |     |
41:6<391::AID-ASI1>3.0.CO;2-9. World Wide Web - WWW ’18, ACM Press, Lyon, France, 2018, pp.
1105–1114,http://dx.doi.org/10.1145/3178876.3186009.
[4] J.Lafferty,D.Blei,Correlatedtopicmodels,in:Y.Weiss,B.Schölkopf,J.
|     |     |     |     |     |     |     |     | [29] I. Korshunova, |     | H. Xiong, | M. Fedoryszak, | L.  | Theis, | Discriminative | topic |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------- | --- | --------- | -------------- | --- | ------ | -------------- | ----- |
Platt(Eds.),AdvancesinNeuralInformationProcessingSystems,Vol.18,
MITPress,2005,p.8. modelingwithlogisticLDA,in:H.Wallach,H.Larochelle,A.Beygelzimer,
[5] D.M.Blei,J.D.Lafferty,Dynamictopicmodels,in:Proceedingsofthe23rd F.d’AlchéBuc,E.Fox,R.Garnett(Eds.),AdvancesinNeuralInformation
ProcessingSystems,Vol.32,CurranAssociates,Inc.,2019.
| International | Conference    |     | on Machine | Learning     | -                          | ICML ’06, | ACM Press, |                      |     |           |         |            |         |       |             |
| ------------- | ------------- | --- | ---------- | ------------ | -------------------------- | --------- | ---------- | -------------------- | --- | --------- | ------- | ---------- | ------- | ----- | ----------- |
|               |               |     |            |              |                            |           |            | [30] T.L. Griffiths, | M.  | Steyvers, | Finding | scientific | topics, | Proc. | Natl. Acad. |
| Pittsburgh,   | Pennsylvania, |     | 2006,      | pp. 113–120, | http://dx.doi.org/10.1145/ |           |            |                      |     |           |         |            |         |       |             |
1143844.1143859. Sci. 101 (suppl 1) (2004) 5228–5235, http://dx.doi.org/10.1073/pnas.
|             |        |            |        |             |        |             |         | 0307752101, | Publisher: | National |     | Academy | of Sciences | Section: | Collo- |
| ----------- | ------ | ---------- | ------ | ----------- | ------ | ----------- | ------- | ----------- | ---------- | -------- | --- | ------- | ----------- | -------- | ------ |
| [6] Z. Cao, | S. Li, | Y. Liu, W. | Li, H. | Ji, A novel | neural | topic model | and its |             |            |          |     |         |             |          |        |
quium.
| supervised | extension, |     | in: Twenty-Ninth |     | AAAI Conference | on  | Artificial |     |     |     |     |     |     |     |     |
| ---------- | ---------- | --- | ---------------- | --- | --------------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
Intelligence,2015. [31] A. Agrawal, W. Fu, T. Menzies, What is wrong with topic modeling?
|     |     |     |     |     |     |     |     | (and how | to fix | it using search-based |     | software | engineering), |     | Inf. Softw. |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ------ | --------------------- | --- | -------- | ------------- | --- | ----------- |
[7] M.Grootendorst,BERTopic:Neuraltopicmodelingwithaclass-basedTF-
|     |     |     |     |     |     |     |     | Technol. | 98 (2018) | 74–88, | http://dx.doi.org/10.1016/j.infsof.2018.02.005, |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --------- | ------ | ----------------------------------------------- | --- | --- | --- | --- |
IDFprocedure,2022,http://dx.doi.org/10.48550/arXiv.2203.05794,arXiv:
arXiv:1608.08176.
2203.05794[cs].URLhttp://arxiv.org/abs/2203.05794.
[8] A.B. Dieng, F.J.R. Ruiz, D.M. Blei, Topic modeling in embedding spaces, [32] H.M.Wallach,Topicmodeling:beyondbag-of-words,in:Proceedingsof
the23rdInternationalConferenceonMachineLearning-ICML’06,ACM
| Trans. | Assoc. | Comput. | Linguist. | 8 (2020) | 439–453, | http://dx.doi.org/10. |     |        |             |               |       |              |     |                       |     |
| ------ | ------ | ------- | --------- | -------- | -------- | --------------------- | --- | ------ | ----------- | ------------- | ----- | ------------ | --- | --------------------- | --- |
|        |        |         |           |          |          |                       |     | Press, | Pittsburgh, | Pennsylvania, | 2006, | pp. 977–984, |     | http://dx.doi.org/10. |     |
1162/tacl_a_00325.
1145/1143844.1143967.
[9] A. Srivastava, C. Sutton, Autoencoding variational inference for topic [33] Y.Jo,A.H.Oh,Aspectandsentimentunificationmodelforonlinereview
models,2017,arXiv:1703.01488[stat].
analysis,in:ProceedingsoftheFourthACMInternationalConferenceon
| [10] Y. Miao, | E. Grefenstette, |     | P. Blunsom, | Discovering |     | discrete latent | topics |            |     |              |      |      |             |     |           |
| ------------- | ---------------- | --- | ----------- | ----------- | --- | --------------- | ------ | ---------- | --- | ------------ | ---- | ---- | ----------- | --- | --------- |
|               |                  |     |             |             |     |                 |        | Web Search | and | Data Mining, | WSDM | ’11, | Association | for | Computing |
withneuralvariationalinference,2018,arXiv:1706.00359[cs]. Machinery,NewYork,NY,USA,2011,pp.815–824,http://dx.doi.org/10.
[11] F.Bianchi,S.Terragni,D.Hovy,Pre-trainingisahottopic:Contextualized
1145/1935826.1935932.
documentembeddingsimprovetopiccoherence,2021,arXiv:2004.03974
|     |     |     |     |     |     |     |     | [34] W.Li,A.McCallum,Pachinkoallocation:DAG-structuredmixturemodels |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
[cs].
oftopiccorrelations,in:Proceedingsofthe23rdInternationalConference
[12] J.Devlin,M.-W.Chang,K.Lee,K.Toutanova,BERT:Pre-trainingofdeep on Machine Learning - ICML ’06, ACM Press, Pittsburgh, Pennsylvania,
bidirectionaltransformersforlanguageunderstanding,2019,arXiv:1810.
2006,pp.577–584,http://dx.doi.org/10.1145/1143844.1143917.
04805[cs].
|     |     |     |     |     |     |     |     | [35] M.Rosen-Zvi,T.Griffiths,M.Steyvers,P.Smyth,Theauthor-topicmodel |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
[13] R. Alghamdi, K. Alfalqi, A survey of topic modeling in text mining, Int. for authors and documents, in: Proceedings of the 20th Conference
J.Adv.Comput.Sci.Appl.6(1)(2015)http://dx.doi.org/10.14569/IJACSA.
|     |     |     |     |     |     |     |     | on Uncertainty |     | in Artificial | Intelligence, | UAI | ’04, AUAI | Press, | Arlington, |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | ------------- | ------------- | --- | --------- | ------ | ---------- |
2015.060121.
Virginia,USA,2004,pp.487–494.
[14] D. Sharma, A survey on journey of topic modeling techniques from [36] J. Chang, D. Blei, Relational topic models for document networks, in:
SVD to deep learning, Int. J. Mod. Educ. Comput. Sci. 9 (2017) 50–62, ArtificialIntelligenceandStatistics,PMLR,2009,pp.81–88.
http://dx.doi.org/10.5815/ijmecs.2017.07.06.
|                  |      |          |             |     |       |                  |     | [37] Y.W.Teh,M.I.Jordan,M.J.Beal,D.M.Blei,HierarchicalDirichletprocesses, |     |     |     |     |     |     |     |
| ---------------- | ---- | -------- | ----------- | --- | ----- | ---------------- | --- | ------------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
| [15] B.V. Barde, | A.M. | Bainwad, | An overview | of  | topic | modeling methods | and |                                                                           |     |     |     |     |     |     |     |
J.Amer.Statist.Assoc.101(476)(2006)1566–1581,http://dx.doi.org/10.
tools, in: 2017 International Conference on Intelligent Computing and 1198/016214506000000302,Publisher:Taylor&Francis.
| Control | Systems | (ICICCS), | IEEE, | Madurai, | 2017, pp. | 745–750, | http://dx. |                                                                   |     |     |     |     |     |     |     |
| ------- | ------- | --------- | ----- | -------- | --------- | -------- | ---------- | ----------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
|         |         |           |       |          |           |          |            | [38] X.Yan,J.Guo,Y.Lan,X.Cheng,Abitermtopicmodelforshorttexts,in: |     |     |     |     |     |     |     |
doi.org/10.1109/ICCONS.2017.8250563.
|     |     |     |     |     |     |     |     | Proceedings | of  | the 22nd | International | Conference | on  | World | Wide Web |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | -------- | ------------- | ---------- | --- | ----- | -------- |
[16] L.Xia,D.Luo,C.Zhang,Z.Wu,Asurveyoftopicmodelsintextclassifica- - WWW ’13, ACM Press, Rio de Janeiro, Brazil, 2013, pp. 1445–1456,
tion,in:20192ndInternationalConferenceonArtificialIntelligenceand http://dx.doi.org/10.1145/2488388.2488514.
| Big Data | (ICAIBD), | 2019, | pp. 244–250, | http://dx.doi.org/10.1109/ICAIBD. |     |     |     |                  |          |     |                   |       |         |           |     |
| -------- | --------- | ----- | ------------ | --------------------------------- | --- | --- | --- | ---------------- | -------- | --- | ----------------- | ----- | ------- | --------- | --- |
|          |           |       |              |                                   |     |     |     | [39] M.-S. Yang, | A survey | of  | fuzzy clustering, | Math. | Comput. | Modelling | 18  |
2019.8836970. (11)(1993)1–16,http://dx.doi.org/10.1016/0895-7177(93)90202-A.
[17] H. Jelodar, Y. Wang, C. Yuan, X. Feng, X. Jiang, Y. Li, L. Zhao, Latent [40] A.Karami,A.Gangopadhyay,B.Zhou,H.Kharrazi,Fuzzyapproachtopic
| Dirichlet | allocation | (LDA) | and   | topic modeling: |                     | models, applications, | a          |          |            |     |         |          |               |       |           |
| --------- | ---------- | ----- | ----- | --------------- | ------------------- | --------------------- | ---------- | -------- | ---------- | --- | ------- | -------- | ------------- | ----- | --------- |
|           |            |       |       |                 |                     |                       |            | modeling | for health | and | medical | corpora, | Int. J. Fuzzy | Syst. | 20 (2017) |
| survey,   | Multimedia | Tools | Appl. | 78 (11)         | (2019) 15169–15211, |                       | http://dx. |          |            |     |         |          |               |       |           |
http://dx.doi.org/10.1007/s40815-017-0327-9.
doi.org/10.1007/s11042-018-6894-4. [41] N.Akhtar,M.M.SufyanBeg,H.Javed,Topicmodellingwithfuzzydocu-
[18] S.Likhitha,B.S.,H.M.,Adetailedsurveyontopicmodelingfordocument mentrepresentation,in:M.Singh,P.Gupta,V.Tyagi,J.Flusser,T.Ören,
| and short | text | data, Int. | J. Comput. | Appl. | 178 | (39) (2019) | 1–9, http: |            |         |          |              |     |          |           |          |
| --------- | ---- | ---------- | ---------- | ----- | --- | ----------- | ---------- | ---------- | ------- | -------- | ------------ | --- | -------- | --------- | -------- |
|           |      |            |            |       |     |             |            | R. Kashyap | (Eds.), | Advances | in Computing |     | and Data | Sciences, | in: Com- |
//dx.doi.org/10.5120/ijca2019919265. munications in Computer and Information Science, Springer, Singapore,
[19] H.Zhao,D.Phung,V.Huynh,Y.Jin,L.Du,W.Buntine,Topicmodelling 2019,pp.577–587,http://dx.doi.org/10.1007/978-981-13-9942-8_54.
meetsdeepneuralnetworks:Asurvey,2021,arXiv:2103.00498[cs].
|     |     |     |     |     |     |     |     | [42] J.Rashid,S.M.A.Shah,A.Irtaza,Fuzzytopicmodelingapproachfortext |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
[20] T. Hofmann, Probabilistic latent semantic indexing, in: Proceedings of mining over short text, Inf. Process. Manage. 56 (6) (2019) 102060,
the 22nd Annual International ACM SIGIR Conference on Research and http://dx.doi.org/10.1016/j.ipm.2019.102060.
Development in Information Retrieval, SIGIR ’99, Association for Com- [43] S.Abri,R.Abri,Providingapersonalizationmodelbasedonfuzzytopic
| puting | Machinery, | New | York, NY, | USA, | 1999, pp. | 50–57, http://dx.doi. |     |     |     |     |     |     |     |     |     |
| ------ | ---------- | --- | --------- | ---- | --------- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
modeling,Arab.J.Sci.Eng.46(4)(2021)3079–3086,http://dx.doi.org/10.
| org/10.1145/312624.312649. |     |     |     |     |     |     |     | 1007/s13369-020-05048-7. |     |     |     |     |     |     |     |
| -------------------------- | --- | --- | --- | --- | --- | --- | --- | ------------------------ | --- | --- | --- | --- | --- | --- | --- |
[21] H. Rubenstein, J.B. Goodenough, Contextual correlates of synonymy, [44] A.Karami,A.Gangopadhyay,B.Zhou,H.Kharrazi,FLATM:Afuzzylogic
Commun.ACM8(10)(1965)627–633,http://dx.doi.org/10.1145/365628. approach topic model for medical documents, 2019, arXiv:1911.10953
| 365657. |     |     |     |     |     |     |     | [cs]. |     |     |     |     |     |     |     |
| ------- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
[22] Z.S. Harris, Distributional structure, WORD 10 (2–3) (1954) 146–162, [45] S.Basu,Y.Yu,R.Zimmermann,Fuzzyclusteringoflecturevideosbased
http://dx.doi.org/10.1080/00437956.1954.11659520,Publisher:Routledge on topic modeling, in: 2016 14th International Workshop on Content-
_eprint:https://doi.org/10.1080/00437956.1954.11659520. Based Multimedia Indexing (CBMI), IEEE, Bucharest, Romania, 2016, pp.
[23] Y.Bengio,A.Courville,P.Vincent,Representationlearning:Areviewand 1–6,http://dx.doi.org/10.1109/CBMI.2016.7500264.
new perspectives, IEEE Trans. Pattern Anal. Mach. Intell. 35 (8) (2013) [46] R.Das,M.Zaheer,C.Dyer,GaussianLDAfortopicmodelswithwordem-
1798–1828, http://dx.doi.org/10.1109/TPAMI.2013.50, Conference Name: beddings,in:Proceedingsofthe53rdAnnualMeetingoftheAssociation
IEEETransactionsonPatternAnalysisandMachineIntelligence. forComputationalLinguisticsandthe7thInternationalJointConference
[24] C.P. Burgess, I. Higgins, A. Pal, L. Matthey, N. Watters, G. Desjardins, A. on Natural Language Processing (Volume 1: Long Papers), Association
Lerchner,Understandingdisentanglinginβ-VAE,2018,arXiv:1804.03599
|            |     |     |     |     |     |     |     | for Computational                 |     | Linguistics, | Beijing, | China, | 2015, | pp. 795–804, | http: |
| ---------- | --- | --- | --- | --- | --- | --- | --- | --------------------------------- | --- | ------------ | -------- | ------ | ----- | ------------ | ----- |
| [cs,stat]. |     |     |     |     |     |     |     | //dx.doi.org/10.3115/v1/P15-1077. |     |              |          |        |       |              |       |
15

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
[47] C.E.Moody,MixingDirichlettopicmodelsandwordembeddingstomake [70] L.Sun,Y.Yin,Discoveringthemesandtrendsintransportationresearch
lda2vec,2016,arXiv:1605.02019[cs]. usingtopicmodeling,Transp.Res.C77(2017)49–66,http://dx.doi.org/
[48] D.Q. Nguyen, R. Billingsley, L. Du, M. Johnson, Improving topic models 10.1016/j.trc.2017.01.013.
withlatentfeaturewordrepresentations,2018,arXiv:1810.06306[cs]. [71] A.Ambrosino,M.Cedrini,J.B.Davis,S.Fiori,M.Guerzoni,M.Nuccio,What
[49] T. Mikolov, K. Chen, G. Corrado, J. Dean, Efficient estimation of word topic modeling could reveal about the evolution of economics, J. Econ.
representationsinvectorspace,2013,arXiv:1301.3781[cs]. Methodol. 25 (4) (2018) 329–348, http://dx.doi.org/10.1080/1350178X.
| [50] C. Li, | H. Wang, | Z. Zhang, | A. Sun, | Z. Ma, | Topic modeling | for short | texts |     |     |     |     |     |     |     |
| ----------- | -------- | --------- | ------- | ------ | -------------- | --------- | ----- | --- | --- | --- | --- | --- | --- | --- |
2018.1529215.
withauxiliarywordembeddings,in:Proceedingsofthe39thInternational [72] B.Dit,M.Revelle,M.Gethers,D.Poshyvanyk,Featurelocationinsource
ACM SIGIR Conference on Research and Development in Information code:ataxonomyandsurvey,J.Softw.:Evol.Process25(1)(2013)53–
Retrieval, ACM, Pisa Italy, 2016, pp. 165–174, http://dx.doi.org/10.1145/ 95,http://dx.doi.org/10.1002/smr.567,_eprint:https://onlinelibrary.wiley.
2911451.2911499.
com/doi/pdf/10.1002/smr.567.
[51] S.Sia,A.Dalmia,S.J.Mielke,Tiredoftopicmodels?Clustersofpretrained [73] H. Hemmati, Z. Fang, M.V. Mäntylä, B. Adams, Prioritizing manual
wordembeddingsmakeforfastandgoodtopicstoo!,2020,http://dx.doi. test cases in rapid release environments, Softw. Test. Verif. Reliab. 27
org/10.48550/arXiv.2004.14914,arXiv:2004.14914[cs].
|     |     |     |     |     |     |     |     | (6) | (2017) e1609, | http://dx.doi.org/10.1002/stvr.1609, |     |     |     | _eprint: https:// |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | ------------------------------------ | --- | --- | --- | ----------------- |
[52] L. McInnes, J. Healy, S. Astels, Hdbscan: Hierarchical density based onlinelibrary.wiley.com/doi/pdf/10.1002/stvr.1609.
clustering,J.OpenSourceSoftw.2(11)(2017)205,http://dx.doi.org/10. [74] A.Hindle,C.Bird,T.Zimmermann,N.Nagappan,Relatingrequirementsto
21105/joss.00205.
implementationviatopicanalysis:Dotopicsextractedfromrequirements
[53] J.He,Z.Hu,T.Berg-Kirkpatrick,Y.Huang,E.P.Xing,Efficientcorrelated
makesensetomanagersanddevelopers?in:201228thIEEEInternational
topicmodelingwithtopicembedding,in:Proceedingsofthe23rdACM Conference on Software Maintenance (ICSM), 2012, pp. 243–252, http:
SIGKDD International Conference on Knowledge Discovery and Data //dx.doi.org/10.1109/ICSM.2012.6405278.
| Mining, | ACM, | Halifax NS | Canada, | 2017, | pp. 225–233, | http://dx.doi.org/ |     |                 |     |          |              |                |     |                |
| ------- | ---- | ---------- | ------- | ----- | ------------ | ------------------ | --- | --------------- | --- | -------- | ------------ | -------------- | --- | -------------- |
|         |      |            |         |       |              |                    |     | [75] J. Garcia, | D.  | Popescu, | C. Mattmann, | N. Medvidovic, | Y.  | Cai, Enhancing |
10.1145/3097983.3098074. architectural recovery using concerns, in: Proceedings of the 2011 26th
[54] D.P. Kingma, M. Welling, Auto-encoding variational Bayes, 2014, arXiv: IEEE/ACMInternationalConferenceonAutomatedSoftwareEngineering,
1312.6114[cs,stat].
|           |         |             |                 |     |                |               |     | ASE                           | ’11, IEEE | Computer | Society, | USA, 2011, | pp. 552–555, | http://dx.doi. |
| --------- | ------- | ----------- | --------------- | --- | -------------- | ------------- | --- | ----------------------------- | --------- | -------- | -------- | ---------- | ------------ | -------------- |
| [55] D.P. | Kingma, | M. Welling, | An introduction |     | to variational | autoencoders, |     |                               |           |          |          |            |              |                |
|           |         | ®           |                 |     |                |               |     | org/10.1109/ASE.2011.6100123. |           |          |          |            |              |                |
Found. Trends Mach. Learn. 12 (4) (2019) 307–392, http://dx.doi.org/ [76] L.Liu,L.Tang,W.Dong,S.Yao,W.Zhou,Anoverviewoftopicmodeling
10.1561/2200000056,arXiv:1906.02691. anditscurrentapplicationsinbioinformatics,SpringerPlus5(1)(2016)
| [56] R. Ding, | R. Nallapati, | B.  | Xiang, Coherence-aware |     | neural | topic modeling, |     |     |     |     |     |     |     |     |
| ------------- | ------------- | --- | ---------------------- | --- | ------ | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
1608,http://dx.doi.org/10.1186/s40064-016-3252-8.
in:Proceedingsofthe2018ConferenceonEmpiricalMethodsinNatural
|     |     |     |     |     |     |     |     | [77] G.E.Heo,K.Y.Kang,M.Song,J.-H.Lee,Analyzingthefieldofbioinformat- |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
LanguageProcessing,AssociationforComputationalLinguistics,Brussels, icswiththemulti-facetedtopicmodelingtechnique,BMCBioinformatics
Belgium,2018,pp.830–836,http://dx.doi.org/10.18653/v1/D18-1096.
18(S7)(2017)251,http://dx.doi.org/10.1186/s12859-017-1640-x.
| [57] S. Brody, | M.  | Lapata, Bayesian | word | sense | induction, | in: Proceedings |     |                                                                       |     |     |     |     |     |     |
| -------------- | --- | ---------------- | ---- | ----- | ---------- | --------------- | --- | --------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
|                |     |                  |      |       |            |                 |     | [78] M.LaRosa,A.Fiannaca,R.Rizzo,A.Urso,Probabilistictopicmodelingfor |     |     |     |     |     |     |
of the 12th Conference of the European Chapter of the ACL (EACL theanalysisandclassificationofgenomicsequences,BMCBioinformatics
2009), Association for Computational Linguistics, Athens, Greece, 2009, 16(S6)(2015)S2,http://dx.doi.org/10.1186/1471-2105-16-S6-S2.
pp.103–111.
|                   |     |                 |     |           |         |            |        | [79] S.J.Kho,H.B.Yalamanchili,M.L.Raymer,A.P.Sheth,Anovelapproachfor |     |     |     |     |     |     |
| ----------------- | --- | --------------- | --- | --------- | ------- | ---------- | ------ | -------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
| [58] A. Haghighi, |     | L. Vanderwende, |     | Exploring | content | models for | multi- |                                                                      |     |     |     |     |     |     |
classifyinggeneexpressiondatausingtopicmodeling,in:Proceedingsof
documentsummarization,in:ProceedingsofHumanLanguageTechnolo- the8thACMInternationalConferenceonBioinformatics,Computational
gies:the2009AnnualConferenceoftheNorthAmericanChapterofthe
|     |     |     |     |     |     |     |     | Biology,and | Health | Informatics, |     | ACM, Boston | Massachusetts | USA, 2017, |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ------ | ------------ | --- | ----------- | ------------- | ---------- |
AssociationforComputationalLinguistics,AssociationforComputational
pp.388–393,http://dx.doi.org/10.1145/3107411.3107483.
Linguistics,Boulder,Colorado,2009,pp.362–370. [80] D.Maier,A.Waldherr,P.Miltner,G.Wiedemann,A.Niekler,A.Keinert,
[59] H.M.Wallach,I.Murray,R.Salakhutdinov,D.Mimno,Evaluationmethods
|     |               |                 |     |        |      |                      |     | B. Pfetsch, | G.  | Heyer, | U. Reber, | T. Häussler, | H. Schmid-Petri, | S. Adam, |
| --- | ------------- | --------------- | --- | ------ | ---- | -------------------- | --- | ----------- | --- | ------ | --------- | ------------ | ---------------- | -------- |
| for | topic models, | in: Proceedings |     | of the | 26th | Annual International |     |             |     |        |           |              |                  |          |
ApplyingLDAtopicmodelingincommunicationresearch:Towardavalid
| Conference | on  | Machine | Learning, | ICML | ’09, Association | for Computing |     |     |          |              |         |         |       |                 |
| ---------- | --- | ------- | --------- | ---- | ---------------- | ------------- | --- | --- | -------- | ------------ | ------- | ------- | ----- | --------------- |
|            |     |         |           |      |                  |               |     | and | reliable | methodology, | Commun. | Methods | Meas. | 12 (2–3) (2018) |
Machinery, New York, NY, USA, 2009, pp. 1105–1112, http://dx.doi.org/ 93–118,http://dx.doi.org/10.1080/19312458.2018.1430754.
10.1145/1553374.1553515.
|     |     |     |     |     |     |     |     | [81] C.Puschmann,T.Scheffler,TopicModelingforMediaandCommunication |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------------------------ | --- | --- | --- | --- | --- | --- |
[60] D.Mimno,H.M.Wallach,E.Talley,M.Leenders,A.McCallum,Optimizing
|          |           |     |               |     |             |        |         | Research: | A   | Short Primer, | SSRN | Scholarly | Paper ID | 2836478, Social |
| -------- | --------- | --- | ------------- | --- | ----------- | ------ | ------- | --------- | --- | ------------- | ---- | --------- | -------- | --------------- |
| semantic | coherence | in  | topic models, | in: | Proceedings | of the | Confer- |           |     |               |      |           |          |                 |
enceonEmpiricalMethodsinNaturalLanguageProcessing,EMNLP’11, ScienceResearchNetwork,Rochester,NY,2016,http://dx.doi.org/10.2139/
ssrn.2836478.
AssociationforComputationalLinguistics,USA,2011,pp.262–272.
|     |     |     |     |     |     |     |     | [82] S.Srinivas,S.Ramachandiran,Discoveringairline-specificbusinessintel- |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
[61] D.Newman,J.H.Lau,K.Grieser,T.Baldwin,Automaticevaluationoftopic
coherence,in:HumanLanguageTechnologies:The2010AnnualConfer- ligence from online passenger reviews: An unsupervised text analytics
approach,2020,arXiv:2012.08000[cs].version:1.
enceoftheNorthAmericanChapteroftheAssociationforComputational
|     |     |     |     |     |     |     |     | [83] Y.Wang,X.Zhao,Z.Sun,H.Yan,L.Wang,Z.Jin,L.Wang,Y.Gao,C.Law,J. |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
Linguistics,HLT’10,AssociationforComputationalLinguistics,USA,2010,
Zeng,Peacock:Learninglong-tailtopicfeaturesforindustrialapplications,
pp.100–108.
[62] J.Chang,S.Gerrish,C.Wang,J.Boyd-graber,D.Blei,Readingtealeaves: 2014,arXiv:1405.4402[cs].
|     |        |           |               |     |            |                |     | [84] D.Jiang,Z.Chen,R.Lian,S.Bao,C.Li,Familia:Anopen-sourcetoolkitfor |     |     |     |     |     |     |
| --- | ------ | --------- | ------------- | --- | ---------- | -------------- | --- | --------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
| How | humans | interpret | topic models, | in: | Y. Bengio, | D. Schuurmans, | J.  |                                                                       |     |     |     |     |     |     |
industrialtopicmodeling,2017,arXiv:1707.09823[cs].version:1.
| Lafferty, | C. Williams, | A.  | Culotta | (Eds.), Advances | in  | Neural Information |     |     |     |     |     |     |     |     |
| --------- | ------------ | --- | ------- | ---------------- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
ProcessingSystems,Vol.22,CurranAssociates,Inc.,2009. [85] S. Terragni, E. Fersini, B.G. Galuzzi, P. Tropeano, A. Candelieri, OCTIS:
[63] M.Mäntylä,M.Claes,U.Farooq,MeasuringLDAtopicstabilityfromclus- Comparing and optimizing topic models is simple!, in: Proceedings
|     |     |     |     |     |     |     |     | of the | 16th | Conference | of the | European | Chapter of | the Association |
| --- | --- | --- | --- | --- | --- | --- | --- | ------ | ---- | ---------- | ------ | -------- | ---------- | --------------- |
tersofreplicatedruns,in:Proceedingsofthe12thACM/IEEEInternational
SymposiumonEmpiricalSoftwareEngineeringandMeasurement,2018, for Computational Linguistics: System Demonstrations, Association for
pp.1–4,http://dx.doi.org/10.1145/3239235.3267435,arXiv:1808.08098. ComputationalLinguistics,Online,2021,pp.263–270.
|                 |     |             |           |              |         |                       |     | [86] A.Schofield,M.Magnusson,D.Mimno,Pullingoutthestops:Rethinking |         |     |               |                 |     |               |
| --------------- | --- | ----------- | --------- | ------------ | ------- | --------------------- | --- | ------------------------------------------------------------------ | ------- | --- | ------------- | --------------- | --- | ------------- |
| [64] W. Webber, |     | A. Moffat,  | J. Zobel, | A similarity | measure | for indefinite        |     |                                                                    |         |     |               |                 |     |               |
|                 |     |             |           |              |         |                       |     | stopword                                                           | removal | for | topic models, | in: Proceedings | of  | the 15th Con- |
| rankings,       | ACM | Trans. Inf. | Syst. 28  | (4) (2010)   | 1–38,   | http://dx.doi.org/10. |     |                                                                    |         |     |               |                 |     |               |
1145/1852102.1852106. ference of the European Chapter of the Association for Computational
[65] M. Belford, B. Mac Namee, D. Greene, Stability of topic modeling via Linguistics: Volume 2, Short Papers, Association for Computational Lin-
guistics,Valencia,Spain,2017,pp.432–436,URLhttps://aclanthology.org/
matrixfactorization,ExpertSyst.Appl.91(2018)159–169,http://dx.doi.
| org/10.1016/j.eswa.2017.08.047. |     |     |     |     |     |     |     | E17-2069. |     |     |     |     |     |     |
| ------------------------------- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --- |
[66] R.Rehurek,P.Sojka,Softwareframeworkfortopicmodellingwithlarge [87] S. Kesiraju, O. Plchot, L. Burget, S.V. Gangashetty, Learning document
embeddingsalongwiththeiruncertainties,IEEE/ACMTrans.AudioSpeech
corpora,in:ProceedingsoftheLREC2010WorkshoponNewChallenges
forNLPFrameworks,2010,pp.45–50. Lang. Process. 28 (2020) 2319–2332, http://dx.doi.org/10.1109/TASLP.
[67] Q. Sun, R. Li, D. Luo, X. Wu, Text segmentation with LDA-based Fisher 2020.3012062,arXiv:1908.07599version:3.
kernel, in: Proceedings of ACL-08: HLT, Short Papers, Association for [88] Y. Miao, L. Yu, P. Blunsom, Neural variational inference for text
processing,2016,arXiv:1511.06038[cs,stat].version:4.
ComputationalLinguistics,Columbus,Ohio,2008,pp.269–272.
[68] B. Jeong, J. Yoon, J.-M. Lee, Social media mining for product planning: [89] K.W. Lim, W. Buntine, Bibliographic analysis with the citation network
A product opportunity mining approach based on topic modeling and topic model, in: D. Phung, H. Li (Eds.), Proceedings of the Sixth Asian
sentimentanalysis,Int.J.Inf.Manage.48(2019)280–290,http://dx.doi. Conference on Machine Learning, in: Proceedings of Machine Learning
org/10.1016/j.ijinfomgt.2017.09.009. Research,39,PMLR,NhaTrangCity,Vietnam,2015,pp.142–158.
[69] J. Zhu, S. Chowdhury, Towards the ontology development for smart [90] D. O’Callaghan, D. Greene, J. Carthy, P. Cunningham, An analysis of the
transportation infrastructure planning via topic modeling, ISARC Proc. coherence of descriptors in topic modeling, Expert Syst. Appl. 42 (13)
(2019)507–514,Publisher:IAARC. (2015)5645–5657,http://dx.doi.org/10.1016/j.eswa.2015.02.055.
16

A.Abdelrazek,Y.Eid,E.Gawishetal. InformationSystems112(2023)102131
[91] T.-N.Doan,T.-A.Hoang,Benchmarkingneuraltopicmodels:Anempirical [101] S. Koltcov, V. Ignatenko, M. Terpilovskii, P. Rosso, Analysis and tuning
study, in: Findings of the Association for Computational Linguistics: of hierarchical topic models based on Renyi entropy approach, 2021,
ACL-IJCNLP 2021, Association for Computational Linguistics, 2021, pp. arXiv:2101.07598[cs,stat].version:1.
4363–4368,http://dx.doi.org/10.18653/v1/2021.findings-acl.382,Online.
|     |     |     |     |     |     |     |     | [102] J. Marjanen, | E. Zosa, S. | Hengchen, | L. Pivovarova, | M. Tolonen, | Topic |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------ | ----------- | --------- | -------------- | ----------- | ----- |
[92] C.Boutsidis,E.Gallopoulos,SVDbasedinitialization:Aheadstartfornon-
modellingdiscoursedynamicsinhistoricalnewspapers,2020,arXiv:2011.
negativematrixfactorization,PatternRecognit.41(4)(2008)1350–1362,
10428[cs].version:1.
http://dx.doi.org/10.1016/j.patcog.2007.09.010.
[93] D. Angelov, Top2Vec: Distributed representations of topics, 2020, http: [103] C.Schöch,Topicmodelinggenre:Anexplorationoffrenchclassicaland
//dx.doi.org/10.48550/arXiv.2008.09470,arXiv:2008.09470[cs,stat]. enlightenmentdrama,2021,arXiv:2103.13019[cs].
|     |     |     |     |     |     |     |     | [104] J.Dehler-Holland,K.Schumacher,W.Fichtner,Topicmodelinguncovers |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------------------------------------------------------- | --- | --- | --- | --- | --- |
[94] D.Sontag,D.Roy,ComplexityofinferenceinlatentDirichletallocation,
in: Advances in Neural Information Processing Systems, Vol. 24, Curran shiftsinmediaframingofthegermanrenewableenergyact,Patterns2
Associates,Inc.,2011. (1)(2021)100169,http://dx.doi.org/10.1016/j.patter.2020.100169.
[95] R.Wang,D.Zhou,Y.Xiong,H.Huang,VariationalGaussiantopicmodel [105] T. Renteria-Vazquez, W.S. Brown, C. Kang, M. Graves, F. Castelli, L.K.
withinvertibleneuralprojections,2021,arXiv:2105.10095[cs].version: Paul, Social inferences in agenesis of the corpus callosum and autism:
1.
|              |         |          |                 |     |         |              |       | Semantic | analysis and topic | modeling, | J. Autism | Dev. Disord. | (2021) |
| ------------ | ------- | -------- | --------------- | --- | ------- | ------------ | ----- | -------- | ------------------ | --------- | --------- | ------------ | ------ |
| [96] S. Sia, | K. Duh, | Adaptive | mixed component |     | LDA for | low resource | topic |          |                    |           |           |              |        |
http://dx.doi.org/10.1007/s10803-021-04957-2.
| modeling, | in: Proceedings |     | of the | 16th Conference |     | of the | European |     |     |     |     |     |     |
| --------- | --------------- | --- | ------ | --------------- | --- | ------ | -------- | --- | --- | --- | --- | --- | --- |
Chapter of the Association for Computational Linguistics: Main Volume, [106] M.D.Armstrong,D.Maupomé,M.-J.Meurs,Topicmodelinginembedding
AssociationforComputationalLinguistics,2021,pp.2451–2469,Online. spacesfordepressionassessment,in:ProceedingsoftheCanadianConfer-
enceonArtificialIntelligence,2021,http://dx.doi.org/10.21428/594757db.
[97] H.Zhao,L.Du,W.Buntine,G.Liu,MetaLDA:atopicmodelthatefficiently
9e67a9f0.
incorporatesmetainformation,2017,arXiv:1709.06365[cs,stat].version:
1. [107] A. Arseniev-Koehler, S.D. Cochran, V.M. Mays, K.-W. Chang, J.G. Foster,
[98] F.Bianchi,S.Terragni,D.Hovy,D.Nozza,E.Fersini,Cross-lingualcontex- Integratingtopicmodelingandwordembeddingtocharacterizeviolent
tualized topic models with zero-shot learning, 2021, arXiv:2004.07737 deaths, 2020, http://dx.doi.org/10.31235/osf.io/nkyaq, arXiv:2106.14365
[cs].
[cs].
| [99] A. Hoyle, | P. Goel, | D. Peskov, | A. Hian-Cheong, |          | J. Boyd-Graber, |                 | P. Resnik, |                    |                    |               |                                  |                |     |
| -------------- | -------- | ---------- | --------------- | -------- | --------------- | --------------- | ---------- | ------------------ | ------------------ | ------------- | -------------------------------- | -------------- | --- |
|                |          |            |                 |          |                 |                 |            | [108] A. Pancheva, | H. Wheadon,        | S. Rogers,    | T. Otto, Using                   | topic modeling | to  |
| Is automated   | topic    | model      | evaluation      | broken?: |                 | The incoherence | of         |                    |                    |               |                                  |                |     |
|                |          |            |                 |          |                 |                 |            | detect             | cellular crosstalk | in scrna-seq, | 2021, http://dx.doi.org/10.1101/ |                |     |
coherence,2021,arXiv:2107.02173[cs].version:1.
[100] C.Doogan,W.Buntine,Topicmodelortopictwaddle?Re-evaluatingse- 2021.07.26.453767,bioRxiv.arXiv:https://www.biorxiv.org/content/early/
manticinterpretabilitymeasures,in:Proceedingsofthe2021Conference 2021/07/26/2021.07.26.453767.full.pdf.
|        |                |     |            |                 |     |                   |     | [109] S. Rani, | M. Kumar, Topic | modeling | and its applications | in materials |     |
| ------ | -------------- | --- | ---------- | --------------- | --- | ----------------- | --- | -------------- | --------------- | -------- | -------------------- | ------------ | --- |
| of the | North American |     | Chapter of | the Association |     | for Computational |     |                |                 |          |                      |              |     |
Linguistics: Human Language Technologies, Association for Computa- scienceandengineering,Mater.Today:Proc.45(2021)5591–5596,http:
tional Linguistics, 2021, pp. 3824–3848, http://dx.doi.org/10.18653/v1/ //dx.doi.org/10.1016/j.matpr.2021.02.313.
2021.naacl-main.300,Online.
17