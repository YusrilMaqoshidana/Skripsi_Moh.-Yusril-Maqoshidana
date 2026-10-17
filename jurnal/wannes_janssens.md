Received10November2025,accepted25November2025,dateofpublication28November2025,
dateofcurrentversion5December2025.
DigitalObjectIdentifier10.1109/ACCESS.2025.3638956
A Comparative Analysis of Topic Reduction
Techniques for BERTopic
WANNESJANSSENS ,MATTHIASBOGAERT ,
ANDDIRKVANDENPOEL ,(SeniorMember,IEEE)
ResearchGroupDataAnalytics,FacultyofEconomicsandBusinessAdministration,GhentUniversity,9000Ghent,Belgium
FlandersMake@UGent–corelabCVAMO,9000Ghent,Belgium
Correspondingauthor:MatthiasBogaert(matthias.bogaert@ugent.be)
ThisworkwassupportedbyFlandersMakeunderGrant180C0123.
ABSTRACT BERTopicisastate-of-the-arttopicmodelingframeworkthatgeneratestopicsbyclustering
contextualized document embeddings. However, its default clustering algorithm, HDBSCAN, often
generates an excessive number of topics, which hinders meaningful comparisons or applications in
downstream tasks. While different topic reduction methods exist, literature lacks a comparison of these
methods and their impact on the quality of the reduced topics. This study offers an in-depth exploration
of1)topicreductionmethodsforBERTopic,includingexistingapproachesfordirectorindirectreduction,
and 2) novel techniques that leverage large language models (LLMs), either by using the LLM-generated
topiclabelstocreatetopicembeddingsorbydirectlypromptingthemodelforidentifyingoverlappingtopics.
Acomparativestudyofthesetopicreductionmethodsisperformed,evaluatingtheirperformanceinterms
ofcoherenceanddiversityacrossmultiplesocialmediaandwebdatasets.Ourfindingsindicatethatindirect
topic reduction (e.g., agglomerative clustering) yields more diverse topics, though sometimes at the cost
of coherence, compared to direct topic reduction (increasing the minimum cluster size). LLM prompting
outperforms agglomerative clustering in both coherence and diversity, though at a higher computational
cost.Therefore,werecommendselectingareductionmethodbasedondatasetcharacteristics,computational
resources,andthedesiredbalancebetweendiversityandcoherence.
INDEX TERMS BERTopic, HDBSCAN, large language models, natural language processing, topic
modeling,topicreduction.
I. INTRODUCTION HDBSCAN (Hierarchical Density-Based Spatial Clustering
BERTopic [1] is widely adopted by practitioners and of Applications with Noise) [7], and (iv) a representation
researchers, due to its user-friendly modular approach and module combining CountVectorizer and class-based term
itsprovenabilitytogeneratehigh-qualitytopics.Priorwork frequency-inverse document frequency (c-TF-IDF) for the
hasshownthatitperformsfavorablycomparedtotraditional tokenizer and weighting steps, respectively. Each module
topicmodelingtechniques[1],[2],[3],[4].Itisparticularly involves distinct underlying algorithms and is governed by
popular for analyzing user-generated content (UGC) and its own set of parameters, making BERTopic a complex
shorttexts,astheseoftenbenefitfromBERTopic’sstrengths frameworkwithalargeparameterspacefortuning.
in handling noisy, and sparse content [2]. The default The HDBSCAN module is arguably the most critical
structure involves four modules: (i) document embedding component of the BERTopic framework. The module cre-
using Sentence-BERT (SBERT) [5], (ii) dimensionality ates density-based hierarchical clusters from the reduced
reductionviaUMAP(UniformManifoldApproximationand document embeddings, also identifying outliers (documents
ProjectionforDimensionReduction)[6],(iii)clusteringwith that are considered noise and not assigned to any cluster).
HDBSCAN does not require specifying the number of
The associate editor coordinating the review of this manuscript and clusters(topics)upfront,whichoftenresultsincoherentbut
approvingitforpublicationwasGiacomoFiumara . anexcessivenumberoftopics,especiallywhendealingwith
2025TheAuthors.ThisworkislicensedunderaCreativeCommonsAttribution4.0License.
VOLUME13,2025 Formoreinformation,seehttps://creativecommons.org/licenses/by/4.0/ 204087

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
short-text and UGC. Consequently, topic reduction should topic reduction via agglomerative clustering and eval-
be applied to obtain a manageable number of dimensions uateitseffectivenesswithinBERTopic.
for downstream tasks (e.g. classification) or to enable fair • We propose an indirect topic reduction technique for
comparisonswithothertopicmodelingapproaches,wherean BERTopic by using LLM prompting to identify over-
equalnumberoftopicsisessential. lappingtopics.Toevaluateitseffectiveness,weconduct
A first gap in the literature is the lack of clarity and an empirical analysis using the OpenAI GPT-4o-
systematic comparison of BERTopic’s built-in topic reduc- mini [15] model and Meta’s open-source Llama-3-8B-
tionmethods.BERTopicincludesbuilt-infunctionalitiesfor instruct[16]model.
| topic reduction |     | in a direct | way | (i.e., performed |     | during the |     |     |     |     |     |     |     |
| --------------- | --- | ----------- | --- | ---------------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
Theaimofthisstudyistwofold:(1)toprovideBERTopic
| fitting process |     | of the BERTopic |     | model) | and an | indirect |     |     |     |     |     |     |     |
| --------------- | --- | --------------- | --- | ------ | ------ | -------- | --- | --- | --- | --- | --- | --- | --- |
userswithdeeperinsightintohowtheframeworkgenerates
| way (i.e.,  | applied | after     | the model | has          | been fitted). | These    |            |             |         |            |           |             |         |
| ----------- | ------- | --------- | --------- | ------------ | ------------- | -------- | ---------- | ----------- | ------- | ---------- | --------- | ----------- | ------- |
|             |         |           |           |              |               |          | a specific | set of      | topics, | which      | reduction | methods     | exist,  |
| methods     | can, in | turn, be  | applied   | on different | types         | of topic |            |             |         |            |           |             |         |
|             |         |           |           |              |               |          | how they   | work,       | and how | they       | impact    | the quality | of the  |
| embeddings. | In      | addition, | studies   | that employ  | BERTopic      | are      |            |             |         |            |           |             |         |
|             |         |           |           |              |               |          | reduced    | topics; and | (2)     | to explore | the       | potential   | of LLMs |
oftenunclearaboutwhichreductionmethodstheyuse.Some
|     |     |     |     |     |     |     | to support | and enhance |     | the topic | reduction |     | process, ulti- |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----------- | --- | --------- | --------- | --- | -------------- |
relyonthedefaultsettings[1],[3],[4],othersdonotspecify
|                |                 |             |            |         |           |            | mately aiming | to       | produce          | higher-quality                  |         | topics. | To support |
| -------------- | --------------- | ----------- | ---------- | ------- | --------- | ---------- | ------------- | -------- | ---------------- | ------------------------------- | ------- | ------- | ---------- |
| their approach |                 | at all [8], | and others | perform | manual    | topic      |               |          |                  |                                 |         |         |            |
|                |                 |             |            |         |           |            | transparency  | and      | reproducibility, |                                 | we have | made    | all code   |
| reduction      | [9], indicating |             | that users | have    | limited   | knowledge  |               |          |                  |                                 |         |         |            |
|                |                 |             |            |         |           |            | and data      | publicly | available        | at https://github.com/Wannes15/ |         |         |            |
| of existing    | reduction       | methods     | and        | how     | different | techniques |               |          |                  |                                 |         |         |            |
BERTopic_reduction
affectthequalityofthereducedtopics,leadingtosuboptimal
SectionIIcoversrelatedliteratureontopicmodeling,the
useoftheframework.
|     |     |     |     |     |     |     | performance | of BERTopic, |     | topic | reduction | techniques, | and |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ------------ | --- | ----- | --------- | ----------- | --- |
Asecondgapisthelimitedexplorationoflargelanguage
|           |           |           |                |     |            |           | the application | of       | LLMs.      | Section   | III outlines |                | both existing |
| --------- | --------- | --------- | -------------- | --- | ---------- | --------- | --------------- | -------- | ---------- | --------- | ------------ | -------------- | ------------- |
| models    | (LLMs)    | for topic | reduction      |     | within     | BERTopic. |                 |          |            |           |              |                |               |
|           |           |           |                |     |            |           | and newly       | proposed | topic      | reduction | techniques   |                | evaluated     |
| LLMs have | recently  | gained    | popularity     |     | in topic   | modeling, |                 |          |            |           |              |                |               |
|           |           |           |                |     |            |           | in this study.  | Section  | IV         | details   | the          | experimental   | setup,        |
| either by | enhancing | the       | interpretation |     | of complex | topic     |                 |          |            |           |              |                |               |
|           |           |           |                |     |            |           | including       | dataset  | selection, | BERTopic  |              | configuration, | and           |
representations [10], [11] or by enabling end-to-end topic evaluation metrics. Section V discusses obtained results.
modeling[12],[13],[14].Theseend-to-endapproachesoften
SectionVIsummarizesthefindingsandoffersrecommenda-
| include | a topic | merging | step, where | overlapping |     | topics are |     |     |     |     |     |     |     |
| ------- | ------- | ------- | ----------- | ----------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
tionsonselectingthemostsuitablereductionmethod.Finally,
identifieddirectlythroughLLMprompting.However,despite
sectionVIIcoverslimitationsandfurtherresearch.
theirgrowingrelevance,theuseofLLMsfortopicreduction
inBERTopichasreceivedlittleattention.
To address these gaps, we first review various topic II. RELATEDWORK
reduction techniques for BERTopic, including both existing A. APPLICATIONSOFTOPICMODELING
|         |        |            |            |     |            |     | Topic modeling | is  | an unsupervised |     | machine |     | learning tech- |
| ------- | ------ | ---------- | ---------- | --- | ---------- | --- | -------------- | --- | --------------- | --- | ------- | --- | -------------- |
| methods | (i.e., | tuning the | parameters |     | of HDBSCAN | and |                |     |                 |     |         |     |                |
applying agglomerative clustering) and new approaches nique used to find underlying topics in a collection of
involving the use of LLMs (i.e., improving the topic documents (or corpus). It reveals the underlying semantic
embeddingsandLLMpromptingtojoinoverlappingtopics). structure of unstructured texts by identifying patterns of
Finally, we evaluate these techniques across three datasets word use and connecting documents that exhibit similar
|             |          |       |     |          |          |           | patterns | [17], [18]. | Traditionally, |     | the primary |     | focus of topic |
| ----------- | -------- | ----- | --- | -------- | -------- | --------- | -------- | ----------- | -------------- | --- | ----------- | --- | -------------- |
| (i.e., Yelp | reviews, | Trump | and | #Covid19 | tweets), | analyzing |          |             |                |     |             |     |                |
theirimpactontopiccoherenceanddiversity. modeling was on the efficient analysis of large volumes
Ourkeycontributionsareasfollows: of longer text, such as emails, scientific abstracts, and
• Wepresentthefirstcomprehensivecomparativeanalysis newspaperarchives[17],[19].However,theriseofcustomer
of topic reduction methods for BERTopic, systemati- engagementandexperienceplatforms,suchassocialmedia,
callyevaluatingvarioustechniquesbasedoncoherence consumer review sites and peer-to-peer applications, has
and diversity across multiple social media and web tremendouslyincreasedtheamountofunstructureddataand
datasetsandHDBSCANparameterconfigurations. especiallyUGC.Thishasdrivenagrowingneedforadvanced
• We categorize both established and newly proposed text analytical techniques [20], including topic modeling,
topic reduction techniques, provide insights into their to identify hidden patterns and relationships hidden within
mechanismsandeffectiveness,andgivepracticalguide- thesemessages[2].
linesfordecidingwhichtopicreductionmethodstouse. Acommonapplicationistheanalysisoftweetswheretopic
• We analyze the different steps of the HDBSCAN modelingcanbeusedtoidentifybroadtopicsofconversation
algorithm and the impact of the minimum cluster size or emerging themes [9], [21], and to conduct sentiment
andclusterselectionmethodparametersontheresulting analysis on these topics [22]. Additionally, it enables the
topics,supportedbyempiricalresultsillustratingeffects tracking of trending subjects and their evolution over time,
onoutliercreation,topiccoherenceanddiversity. providing valuable insights into how public discourse shifts
• We propose using SBERT embeddings of LLM- in response to events or social dynamics (e.g Covid 19)
generated topic labels as a representation for indirect [4], [23]. Other studies employ topic modeling to extract
| 204088 |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
features or dimensions from textual data, which can then following, we examine the key strengths and limitations of
be utilized in various downstream processes. For instance, BERTopic.
topics extracted from Airbnb property descriptions have Firstly, Grootendorst [1] demonstrated BERTopic’s com-
been used to predict demand [24], while topics from tweets petitiveperformanceingeneratingcoherenttopics,compar-
have been integrated into online analytical processing [25]. ingitwithLDA,NMF,andCTMacrossbenchmarkdatasets.
Similarly, topics identified from company web pages have Otherstudies[3],[4],[8]alsoconfirmedBERTopic’ssuperior
beenleveragedtoclassifytheinnovativenessoffirms[26]. topic coherence across various applications and configura-
In the following, the most common topic modeling tions.However,topicmodelsshouldnotbeevaluatedsolely
methods are discussed in studies involving social media on coherence [27]. Egger and Yu [2] conducted a qualita-
and web data as this is the primary focus of our research. tive comparison of BERTopic, LDA, NMF, and Top2Vec,
For a comprehensive overview of different topic modeling emphasizing BERTopic’s well-separated topics, its modular
approaches we refer the reader to [27]. Topic modeling flexibility, and its use of HDBSCAN for hierarchical topic
approaches can be categorized into non-contextual and reduction. They also noted LDA’s unsuitability for social
contextual methods. Non-contextual methods are based on mediadata.Additionally,BERTopichasshownadvantagesin
a Bag-of-Words and include techniques such as Latent clusteringperformance.Ganetal.[33]founditoutperformed
Dirichlet Allocation (LDA) and Non-Negative Matrix Fac- LDA and Top2Vec, improving clustering by at least 34.2%
torization (NMF) [28]. In the case of LDA, a probabilistic onChineseandEnglishdatasets.Similarly,Turanetal.[34]
model, each document in a collection is represented as found BERTopic produced more meaningful results on
a finite mixture of underlying topics, and each topic is an Amazon review dataset compared to LDA and NMF.
represented as a distribution over an underlying set of word These findings further support BERTopic’s effectiveness
probabilities [29]. NMF, a non-probabilistic algorithm, uses overtraditionaltopicmodelingmethodsespeciallyonsocial
matrix factorization to model each document as a mixture media and web data, which motivates our decision to focus
ofhiddentopics[2].Despiteshowingadecentperformance, on the BERTopic framework for the comparative analysis
traditionalBag-of-Wordsapproachesdonottakeintoaccount presentedinthispaper.
the order of words, thereby failing to capture semantic AlthoughBERTopicoffersnotableadvantages,researchers
relationshipsamongwordsandsentences[30].Additionally, have also pointed out some drawbacks of BERTopic. Egger
theyfrequentlyrequireextensivepreprocessingstepssuchas and Yu [2] noted the inability of BERTopic to generate
stop-wordremovalandlemmatizationtoachievesatisfactory true topic distributions since each document is assigned
performance [31]. Consequently, the emergence of neural to a single topic. Other studies also argued that outlier
embeddingtechniqueshasledtocriticismofthesetraditional generationcan,insomecases,beexcessiveforBERTopicand
methodsintheliteratures[1],[2],and[31]. Top2Vec,whichcanmakeanalysisdifficult[2],[8].Despite
Contextualmethodsemployembeddingtechniquestotake these concerns, Grootendorst [1] argued that outliers can
intoaccountthecontextofawordorsentencetocreatevector actuallyimprovetopicqualitybypreventingtheassignment
representationsinsuchawaythatsimilartexts/sentencesare of irrelevant documents. This view is supported by De
closerinvectorspace.Thisway,textembeddingscancapture Groot et al. [8], who found that BERTopic, when used
semantic relationships between words and documents [1]. with HDBSCAN, achieves higher topic coherence and
Examples of topic models that use an embedding approach diversity. Furthermore, BERTopic includes built-in methods
are Top2Vec [31] and BERTopic [1]. Top2Vec leverages for both outlier reduction and topic distribution approxima-
Doc2Vec’s [30] word- and document representations to tion, although these features fall outside the scope of this
jointly learn embedded topic, document, and word vectors. study. Regarding the issue of single-topic assignment, this
Similar documents are then clustered together and topic assumption is often reasonable for social media and web
representations are created by finding words close to the texts,whereindividualpoststypicallyfocusonasingletopic.
cluster’s centroid [31]. BERTopic leverages SBERT [5] Another notable property of BERTopic is that it does not
embeddingsandusesaclass-basedversionofTF-IDF[32]to requirethenumberoftopicstobespecifiedinadvance.This
extracttopicrepresentations,overcomingthecentroid-based can be viewed as both an advantage and a disadvantage.
assumptionofTop2Vec[1]. On the one hand, BERTopic’s clustering module can auto-
maticallyidentifyacoherentsetoftopics,ontheotherhand,
thiscansometimesresultinanundesirablenumberoftopics.
B. BERTopicPERFORMANCE Tosetthenumberoftopicstoafixednumberandincreasethe
BERTopichasbeenfrequentlyadoptedbothinindustryand overallinterpretabilityofthetopics,topicreductionisoften
academia. It has been used not only for uncovering trends applied.However,thereisnoclearconsensusintheliterature
andtopicsindatabutalsoinnumerouscomparativestudies. onwhichreductionmethodismostappropriate.
These studies have evaluated BERTopic against traditional For instance, Grootendorst [1] and Abuzayed and Al-
topic modeling methods such as LDA and NMF, as well Khalifa[3]trainedmodelsacrossarangeoftopicnumbersto
as more contemporary approaches such as Top2Vec. In the compareresultsbutdidnotexplicitlydescribetheirreduction
VOLUME13,2025 204089

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
method for BERTopic. From context, they likely used the Lietal.[11]usedChatGPTtoimprovetopicrepresentation
nr_topicsparameter,whichmergestopicsbasedonc-TF-IDF by generating more interpretable labels for the top 10 most
embeddings. Similarly, Ogunleye et al. [4] explicitly stated frequentwordsrelatedtotopicsoutputbyanLDAmodeland
thattheyusedthenr_topicsparametertoreducethenumber showedpromisingresults.Theirstudyreachedtheinteresting
of topics in their BERTopic model with the HDBSCAN conclusion that these generated labels are often preferred
modulefromover100to10. over human-generated labels. More advanced approaches
Incontrast,EggerandYu[2]explicitlydescribedmerging could include in-context learning techniques, such as the
topics based on the cosine distance matrix of the topic inclusionofcarefullycrafteddemonstrationsandinstructions
embeddingsfortheirqualitativecomparison.However,they intheprompttocreatemoreaccurateandinterpretabletopic
did not clarify whether the embeddings used were neural representations. In related work, Koloski et al. [10] applied
embeddings or c-TF-IDF embeddings. In the case of de LLMs to generate topic labels that are tailored to specific
Grootetal.[8],themethodusedfortopicreductionisentirely domains,showingthatpromptsinformedbydomainexpertise
unclear. Meanwhile, Baird et al. [9] identified the optimal can yield labels that more closely reflect the context of
number of topics based on coherence and then manually the data. They further introduced a new evaluation metric
reducedtopicsthroughadetailedprocedure,notbymerging and explored adapting BERTopic to particular domains by
butbysimplydroppingcertaintopics. fine-tuning sentence transformer embeddings, though their
Insummary,thespecificreductionmethodsusedinthese study did not investigate tuning BERTopic parameters or
studies are often not clearly reported. Some studies rely on applyingposthoctopicreduction.
the default methods, others do not specify their approach, PromptTopic and TopicGPT are two recent LLM-based
whereasothersperformmanualtopicreduction.Thislackof end-to-endapproachestotopicmodeling.PromptTopic[13]
clarity and methodological consistency suggests that many involves three stages: extracting high-level topics at the
studiesarelikelyunawareoftheexactunderlyingprocesses sentence level using carefully crafted prompts, iteratively
andthatinsufficientattentionisgiventoexploringdifferent merging similar topics to reduce redundancy, and refining
topicreductionmethods.Therefore,itisessentialtoconduct topic representations by selecting the most representative
a systematic comparison of the different topic reduction words. Their study made use of ChatGPT and LLaMA-
methods available in BERTopic, as their impact on topic 13B.TopicGPT[14]followsatwo-stageprocess:generating
coherenceanddiversityremainsunderexplored.Specifically, topics from a document sample and assigning these topics
thisstudyaimsto(1)provideastructuredoverviewofthese to the full corpus. Similar to PromptTopic, it refines topics
reductiontechniquesand(2)performacomparativeanalysis by merging similar ones using embedding similarities, but
of their impact on coherence and diversity. This type of usingGPT-3.5-TurboandMistral-7B-Instruct.Doietal.[12]
analysisiscrucialforguidingpractitionersandresearchersin present another end-to-end topic modeling framework in
selectingthemostappropriatetopicreductiontechniquefor whichlargelanguagemodelsarepromptedeitherinparallel
theirapplicationsandiscurrentlymissingfromtheliterature. or sequentially to extract and merge topics, using GPT-
3.5 and GPT-4. Similarly, Mu et al. [36] demonstrate that
C. LLMsFORTOPICMODELING LLMs can be prompted to generate topics from a set of
More recently, studies have explored the potential of LLMs documents and refine them according to human guidelines,
to enhance the topic modeling process in several ways, highlightingboththepotentialandlimitationsofLLM-based
includingtopicevaluationandinterpretation,aswellasend- topic extraction. While these approaches demonstrate that
to-endtopicgeneration. LLMs can produce coherent topics, they come with notable
Stammbach et al. [35] leverage LLMs to evaluate topic drawbacks, including substantial computational overhead
models by assessing the topic coherence through two key and long runtimes. Although effective at identifying broad,
tasks: an intrusion detection task and a coherence rating high-leveltopics,theyoftenstruggletocapturemoredetailed
task. In the intrusion detection task, the LLM is prompted or nuanced themes, and their evaluations against BERTopic
to identify an ‘‘intruder’’ word from a list of top words donottakeintoaccountthesensitivityofBERTopictoparam-
associatedwithagiventopic,aimingtogaugehowwellthe etersettings.Incontrast,ourworkexplicitlyaddressesthisby
top words represent the topic. In the coherence rating task, averagingresultsacrossmultipleHDBSCANconfigurations.
the LLM is asked to rate the coherence of the topic words The above studies show the potential of LLMs to add
on a scale of 1 to 3, providing a more direct evaluation of value in the topic modeling process. None of these studies,
the quality of the topic. The study utilized both ChatGPT however, have explored the potential of LLMs to assist in
and the open-source FLAN-T5 model, concluding that the topic reduction process for BERTopic, which we aim
LLMscaneffectivelyandaccuratelyassesstopiccoherence. to investigate in this study. In particular, we employ LLMs
Moreover, the research demonstrated that LLMs can assist in two ways: (1) to identify overlapping topics within the
in automatically determining the optimal number of topics set of topics generated by BERTopic, and (2) to label topic
for LDA and other bag-of-words-based topic modeling representationspriortoembeddingthemforuseinthetopic
techniques. reductionprocess.
204090 VOLUME13,2025

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
III. TOPICREDUCTIONTECHNIQUES
| BERTopic       | generates  |             | a set of  | topics,        | which       | is often too |     |     |     |     |
| -------------- | ---------- | ----------- | --------- | -------------- | ----------- | ------------ | --- | --- | --- | --- |
| large for      | downstream |             | tasks or  | for comparison |             | with other   |     |     |     |     |
| topic modeling |            | techniques. | To        | address this,  | topic       | reduction    |     |     |     |     |
| is applied     | to obtain  | a           | smaller   | number         | of topics.  | To our       |     |     |     |     |
| knowledge,     | no         | study       | has yet   | explored       | or compared | topic        |     |     |     |     |
| reduction      | techniques | for         | BERTopic. | This           | section     | classifies   |     |     |     |     |
anddescribesthetopicreductiontechniquesanalyzedinthis
study.
Topicreductionmethodsareclassifiedintotwocategories:
| direct and  | indirect. | Direct | approaches | are    | performed     | during |     |     |     |     |
| ----------- | --------- | ------ | ---------- | ------ | ------------- | ------ | --- | --- | --- | --- |
| the fitting | process   | of     | a BERTopic | model, | specifically, | the    |     |     |     |     |
clusteringstepoftheframeworkisalteredtoproducefewer
| clusters. | Indirect | approaches |     | start with | an  | initial set of |     |     |     |     |
| --------- | -------- | ---------- | --- | ---------- | --- | -------------- | --- | --- | --- | --- |
clusters/topicsanditerativelymergesimilarones.Therefore,
| indirect | approaches | can | also be | applied | to other | embedding |     |     |     |     |
| -------- | ---------- | --- | ------- | ------- | -------- | --------- | --- | --- | --- | --- |
basedtopicmodelingframeworks,suchasTop2Vec.
FIGURE1. Topicreductiontechniquescomparedinthisstudy,with
Figure 1 summarizes the topic reduction techniques existingmethodsshowningrayandnewmethodsshowninblue.
comparedinthisstudywithexistingmethodsshowningray
andnewlyproposedmethodshighlightedinblue.Thenumber
oftopicscanbereduceddirectlybyincreasingtheminimum B. AGGLOMERATIVECLUSTERING
clustersizeparameterofHDBSCAN(BERTopic’sclustering InBERTopic,thenumberoftopicscanbereducedindirectly
module). BERTopic also includes built-in functionalities through a post-processing step involving agglomerative
for indirect topic reduction using agglomerative clustering, clustering.Thismethodisconsideredindirectbecauseitdoes
whichcanbebasedoneitherthetopic’sc-TF-IDFembedding
notalterthetopicmodelingprocess.Instead,itisappliedafter
or the average reduced SBERT embedding of the topic. the BERTopic model has already been fitted and the topics
We extend this analysis by introducing a new embedding havebeengenerated.
option for agglomerative clustering, which utilizes the Agglomerative clustering starts from a set of clusters
SBERT embeddings of the topic labels generated by an outputbyaBERTopicmodelanditerativelymergesthetwo
| LLM or | the top | 10 keywords. |     | Additionally, |     | we apply an |          |                  |                      |               |
| ------ | ------- | ------------ | --- | ------------- | --- | ----------- | -------- | ---------------- | -------------------- | ------------- |
|        |         |              |     |               |     |             | clusters | that are closest | to each other, based | on the cosine |
indirect reduction method for BERTopic that merges topics average linkage distance between the topic embeddings.
using prompts to an LLM. A detailed description of each Inotherwords,itcalculatestheaverageembeddingoftopics
topic reduction method and its implementation is discussed and merges the two nearest ones. The average embedding
| below. |     |     |     |     |     |     | ofthesemergedclustersisthenusedtorepresentthenewly |     |     |     |
| ------ | --- | --- | --- | --- | --- | --- | -------------------------------------------------- | --- | --- | --- |
mergedtopic.Thisprocesscontinuesuntilthedesirednumber
| A. INCREASINGTHEMINIMUMCLUSTERSIZE |     |     |     |     |     |     | oftopicsisreached. |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- |
IncreasingtheminimumclustersizeparameteroftheHDB- While the impact of various distance metrics and linkage
SCAN module is considered a direct reduction technique methods could also be explored, we focus on comparing
since it directly influences the tree condensing process step different types of topic embeddings since their averages are
of the HDBSCAN algorithm. As the minimum cluster size used for merging nearby clusters. Specifically, we consider
increases,fewerclustersarecreatedandsubsequentlyavail- the c-TF-IDF embedding, the average reduced SBERT
able for selection. Additionally, variations in this parameter embedding, and the newly proposed SBERT topic label
influencethecreationofoutliers,whichinturnaffectstopic embeddings,whicharedescribedinmoredetailbelow.
| representations. |     | For a | more thorough | understanding |     | of the |     |     |     |     |
| ---------------- | --- | ----- | ------------- | ------------- | --- | ------ | --- | --- | --- | --- |
HDBSCANalgorithmanditsparameterswereferthereader
1) C-TF-IDFEMBEDDING
tosectionIV. The c-TF-IDF embedding of a topic is generated by
It should be noted that this method does not allow consolidatingalldocumentsassignedtothattopic/clusterand
for specifying the exact number of topics. As a result, thenextractingtheimportanceofalltermsinthevocabulary
achieving the desired number of clusters or topics may usingthefollowingformula:
requiretrialanderrorwhentuningtheminimumclustersize
c-TF-IDF(t,c)=TF(t,c)×IDF(t) (1)
| parameter.           | Nevertheless,adjusting |     |          | the minimum |        | clustersize |     |     |     |     |
| -------------------- | ---------------------- | --- | -------- | ----------- | ------ | ----------- | --- | --- | --- | --- |
| is a straightforward |                        | and | commonly | used        | method | for topic   |     |     |     |     |
where:
| reduction, | often | serving | as the | first approach |     | in practical |     |     |     |     |
| ---------- | ----- | ------- | ------ | -------------- | --- | ------------ | --- | --- | --- | --- |
f t,c
applications. For the purposes of this study, this method is TF(t,c)=
P
| usedasabenchmark. |     |     |     |     |     |     |     |     | t′∈c f t′,c |        |
| ----------------- | --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ------ |
| VOLUME13,2025     |     |     |     |     |     |     |     |     |             | 204091 |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
|     |     |     |     | (cid:18) | A (cid:19) |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | -------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
IDF(t)=log 1+ SBERTtopicembedding,and(2)toobtainatopicembedding
f that better represents the overall message of the documents
t
Here, t represents a term (word), c represents a cluster assignedtothistopic.AvisualillustrationoftheSBERTtopic
labelembeddingisprovidedinFig.3.
| (topic), | f t,c is the | frequency |     | of term | t in cluster | c,  | f is the |     |     |     |     |     |     |
| -------- | ------------ | --------- | --- | ------- | ------------ | --- | -------- | --- | --- | --- | --- | --- | --- |
t
| frequency | of term | t across | all | clusters, | and | A is the | average |     |     |     |     |     |     |
| --------- | ------- | -------- | --- | --------- | --- | -------- | ------- | --- | --- | --- | --- | --- | --- |
numberofwordspercluster.
| The c-TF-IDF |     | embedding |     | is a bag-of-words |     | approach | to  |     |     |     |     |     |     |
| ------------ | --- | --------- | --- | ----------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
representatopic.Thissameformulaisalsousedtoidentify
themostimportantwordswithinacluster(i.e.,thosewiththe
| highest | c-TF-IDF | score), | which | are then | used | to create | the |     |     |     |     |     |     |
| ------- | -------- | ------- | ----- | -------- | ---- | --------- | --- | --- | --- | --- | --- | --- | --- |
topicrepresentation.Asaresult,topicswithsimilarc-TF-IDF
embeddingsareexpectedtosharesimilarimportantwords.
2) AVERAGEREDUCEDSBERTTOPICEMBEDDING
| The average | reduced |               | SBERT | embedding |             | for a topic | is    |                                                     |     |     |     |     |     |
| ----------- | ------- | ------------- | ----- | --------- | ----------- | ----------- | ----- | --------------------------------------------------- | --- | --- | --- | --- | --- |
|             |         |               |       |           |             |             |       | FIGURE3. IllustrationoftheSBERTtopiclabelembedding. |     |     |     |     |     |
| computed    | by      | taking        | the   | mean of   | the reduced |             | SBERT |                                                     |     |     |     |     |     |
| embeddings  | of      | the documents |       | assigned  | to          | that topic. | This  |                                                     |     |     |     |     |     |
Whenusingthetop-10wordsrepresentation,thetenmost
| approach | provides | a   | semantic | embedding | that | captures | the |     |     |     |     |     |     |
| -------- | -------- | --- | -------- | --------- | ---- | -------- | --- | --- | --- | --- | --- | --- | --- |
representativewordsforeachtopicareselectedbasedontheir
overallmeaningofthedocumentswithinthetopic.
The BERTopic clustering algorithm, HDBSCAN, is den- c-TF-IDFscoresandencodedintoa384-dimensionalvector
usingSBERT.FortheLLM-labelrepresentation,atopiclabel
| sity based, | but         | averaging  |        | the embeddings   |                | of a | cluster |                |              |              |     |                     |            |
| ----------- | ----------- | ---------- | ------ | ---------------- | -------------- | ---- | ------- | -------------- | ------------ | ------------ | --- | ------------------- | ---------- |
|             |             |            |        |                  |                |      |         | is constructed | by prompting | an           | LLM | (in our             | case, GPT- |
| transforms  | the         | embedding  | into   | a centroid-based |                | one. | Fig. 2  |                |              |              |     |                     |            |
|             |             |            |        |                  |                |      |         | 4o-mini) with  | the topic’s  | keywords     | and | four representative |            |
| illustrates | this        | issue with | two    | clusters         | that could     | have | been    |                |              |              |     |                     |            |
|             |             |            |        |                  |                |      |         | documents,     | as provided  | by BERTopic. |     | An example          | of this    |
| found by    | the HDBSCAN |            | module | for              | two dimensions |      | (note   |                |              |              |     |                     |            |
thatinreality,typically5dimensionsareused).Theredcross promptformatisshownintable1.Theresultinglabelisthen
encodedintoavectorusingSBERT.
| represents | the     | resulting     | average | SBERT         | embedding |      | of each |     |     |     |     |     |     |
| ---------- | ------- | ------------- | ------- | ------------- | --------- | ---- | ------- | --- | --- | --- | --- | --- | --- |
| cluster.   | For the | left cluster, |         | the embedding | falls     | well | within  |     |     |     |     |     |     |
the cluster, indicating that it effectively captures the overall TABLE1. IllustrationoftheLLMpromptforlabellingtopicsbasedon
theirtop10keywordsandfourrepresentativedocumentsfromtheTrump
| meaning | of the | topic. | In the | right cluster, |     | the embedding |     |     |     |     |     |     |     |
| ------- | ------ | ------ | ------ | -------------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- |
Tweetsdataset.
| lies outside | the       | main | cluster, | which | may negatively |         | impact |     |     |     |     |     |     |
| ------------ | --------- | ---- | -------- | ----- | -------------- | ------- | ------ | --- | --- | --- | --- | --- | --- |
| the topic    | reduction |      | process  | when  | relying        | on this | topic  |     |     |     |     |     |     |
embedding.
FIGURE2. Illustrationofthecentroid-basedassumptionoftheaverage
reducedSBERTtopicembedding.Theredcrossindicatesthetopic
| embeddingforeachcluster. |     |     |     |     |     |     |     | C. LLMPROMPTING |     |     |     |     |     |
| ------------------------ | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- |
Nexttoagglomerativeclusteringbasedondifferenttypesof
|     |     |     |     |     |     |     |     | topic embeddings, | a novel | indirect | topic | reduction | method |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------------- | ------- | -------- | ----- | --------- | ------ |
3) SBERTTOPICLABELEMBEDDING thatleveragesLLMstomergeoverlappingtopicsisproposed.
Finally, we introduce a new type of topic embedding which This approach involves representing each topic either by
starts from the topic representations. Each topic is either its top 10 keywords, extracted using c-TF-IDF, or by its
represented by their top 10 keywords, or by an LLM- LLM-generated topic label (using the prompt defined in
generatedlabel. table 1). The LLM is then prompted to identify the two
This topic representation (top 10 words or LLM label) mostoverlappingtopicsbasedontheirrepresentation.These
is then embedded using the same SBERT model used topicsaresubsequentlymerged,andtheirrepresentationsare
in BERTopic’s embedding module. By embedding the updatedaccordingly.ThismethodisillustratedinFig.4.
topic label we attempt (1) to overcome the centroid-based In this study, we use OpenAI’s GPT-4o-mini [15] and
assumption that is present when using the average reduced Meta’s Llama-3-8B-instruct [16]. When prompted with
| 204092 |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
TABLE2. LLMpromptformergingbasedontop10wordsrepresentation.
FIGURE4. IllustrationoftopicreductionbypromptinganLLM.
LLM-generatedtopiclabels,Llamaoftendeclinedtorespond
to sensitive content, such as defamation of political figures
orconspiracytheories,particularlyintheTrumpTweetsand
#Covid19Tweetsdatasets.Asaresult,fortheLlamamodel, TABLE3. Demonstrationpromptformergingbasedonlabelledtopics.
wefocusedsolelyonthetop10wordswhenreducingtopics
throughprompting.
Tables2and3presentthefullpromptsusedforidentifying
similar topics based on the topic’s top 10 words and its
LLM label respectively. To enhance the performance of
the LLM, prompts were developed through a trial-and-error
process informed by best practices in prompt engineering,
incorporating a structured format with a system prompt,
demonstration examples, and a clear instruction prompt to
improve response robustness [37]. While an ablation study
onprompttemplates,temperature,andotherhyperparameters
couldprovideusefulinsightsintovariability,itisconsidered
beyondthescopeofthisstudy.
IV. EXPERIMENTALSETUP
In this section, we discuss our experimental setup for
comparing the abovementioned topic reduction techniques.
This includes a description of the datasets, the detailed
settings of the BERTopic framework, including an inter-
pretation of the HDBSCAN module for topic modeling,
and the specific evaluation metrics employed for com-
paring the different reduction methods. Fig. 5 provides including BERTopic configurations, topic reduction pro-
an overview of our experimental setup. All experiments, cedures, and evaluation workflows, can be reproduced
VOLUME13,2025 204093

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
using the code and data provided in our public repository: sentences.Thisenablesfastandaccuratesemanticsimilarity
https://github.com/Wannes15/BERTopic_reduction comparisons[5].
|     |     |     |     |     |     |     |     | The pre-trained |     | ’’all-MiniLM-L6-v2’’ |     |     | model | is  | used to |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | -------------------- | --- | --- | ----- | --- | ------- |
transformeachinputdocumentinto384-dimensionalvector
A. DATASETS
The different topic reduction methods are benchmarked on representations where semantically similar documents will
threecommonlyusedopen-sourcedatasets:TrumpTweets,1 be ‘close’ in the high-dimensional vector space. While
Tweets,2 reviews.3 alternativeembeddingmodelsarepossible,the’’all-MiniLM-
| #Covid19 |     | and | Yelp |     | The Trump | Tweets |     |     |     |     |     |     |     |     |     |
| -------- | --- | --- | ---- | --- | --------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
dataset consists of 43,352 tweets scraped from the @real- L6-v2’’ is chosen for its good balance between speed and
| DonaldTrump | account |     | of former | United | States | President |     | quality. |     |     |     |     |     |     |     |
| ----------- | ------- | --- | --------- | ------ | ------ | --------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
DonaldTrump,spanningtheperiodfromMay2009toJune
2020.The#Covid19Tweetsdatasetcontains178,683tweets 2) DIMENSIONALITYREDUCTION
from June 2020 to August 2020, all featuring the hashtag After embedding the input documents, UMAP reduces the
Covid19.Theaveragelengthofthesetweetsiscomparableto dimensions of each embedding to five to simplify the
thoseintheTrumpdataset.Finally,theYelpreviewsdataset clustering process for HDBSCAN. UMAP is a non-linear
includes 10,000 reviews from April 2005 to May 2013, dimensionality reduction algorithm that learns the man-
covering 4,171 companies. These reviews are significantly ifold structure of high-dimensional data and creates a
longer, with an average length approximately six times that lower-dimensional embedding that preserves its essen-
ofthetweetsintheotherdatasets.Byincludingbothtweets tial topological structure. Although other dimensionality
and reviews, we combine short-text with longer-text UGC, reduction techniques are available, UMAP is particularly
offering a diverse range of input for analysis. The datasets effective at capturing both local and global structures in
arenotpreprocessedtoensurefaircomparisonsandpreserve high-dimensional spaces and transferring them to lower-
as much contextual information as possible for the SBERT dimensionalrepresentations[39].Thecandidatesettingsfor
embeddingmodulewithintheBERTopicframework.Table4 UMAP are given in table 5. These hyperparameters remain
summarizesthemaincharacteristicsofeachdataset. unchangedduringourexperiments.
TABLE4. Datasetsizeandaveragedocumentlength. TABLE5. UMAPcandidatesettings.
B. BERTopicFRAMEWORKSETUP
| The BERTopic |     | framework | consists | of  | four sequential |     | mod- |     |     |     |     |     |     |     |     |
| ------------ | --- | --------- | -------- | --- | --------------- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
ules: an embedding module, a dimensionality reduction 3) CLUSTERINGWITHHDBSCAN
|         |              |         |     |                      |     |         |     | In the clustering |     | step, | we employ |     | HDBSCAN | to  | extract |
| ------- | ------------ | ------- | --- | -------------------- | --- | ------- | --- | ----------------- | --- | ----- | --------- | --- | ------- | --- | ------- |
| module, | a clustering | module, |     | and a representation |     | module. |     |                   |     |       |           |     |         |     |         |
While BERTopic allows flexibility in selecting alternatives density-based hierarchical clusters from the reduced doc-
|          |         |             |                |     |     |      |        | ument embeddings, |            | including |          | the identification |              | of  | outliers |
| -------- | ------- | ----------- | -------------- | --- | --- | ---- | ------ | ----------------- | ---------- | --------- | -------- | ------------------ | ------------ | --- | -------- |
| for each | module, | the default | configurations |     | are | used | due to |                   |            |           |          |                    |              |     |          |
|          |         |             |                |     |     |      |        | (documents        | classified |           | as noise | and                | not assigned |     | to any   |
itsstrongperformanceandwidespreadadoptioninpractice.
| The default | setup | includes | the | pre-trained | ’’all-MiniLM-L6- |     |     | cluster). |     |     |     |     |     |     |     |
| ----------- | ----- | -------- | --- | ----------- | ---------------- | --- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
RatherthanusingthedefaultconfigurationofHDBSCAN,
| v2’’ model | from | SBERT | for embedding |     | generation, | UMAP |     |     |     |     |     |     |     |     |     |
| ---------- | ---- | ----- | ------------- | --- | ----------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
fordimensionalityreduction,HDBSCANforclustering,and we vary the minimum cluster size and cluster selection
|     |     |     |     |     |     |     |     | method, | which | significantly | affect |     | the clustering |     | process. |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ----- | ------------- | ------ | --- | -------------- | --- | -------- |
arepresentationmodulecombiningCountVectorizerwithc-
|     |     |     |     |     |     |     |     | To understand |     | exactly | how these | hyperparameters |     |     | affect |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ------- | --------- | --------------- | --- | --- | ------ |
TF-IDF,asillustratedinFig.6.
HDBSCAN4
|     |     |     |     |     |     |     |     | the clustering |     | process, | the pseudocode |     | of  |     | is  |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | -------- | -------------- | --- | --- | --- | --- |
providedinAlgorithm1.
1) EMBEDDING
SBERTisamodificationoftheBERTmodel[38]designed The algorithm starts from the reduced document embed-
dingsandcalculatesthepairwisemutualreachabilitydistance
forefficientsentenceembeddings.UnliketraditionalBERT,
|                |     |           |            |          |           |               |        | between       | all embeddings. |        | The       | mutual  | reachability |       | distance |
| -------------- | --- | --------- | ---------- | -------- | --------- | ------------- | ------ | ------------- | --------------- | ------ | --------- | ------- | ------------ | ----- | -------- |
| which requires |     | comparing |            | sentence | pairs     | individually, |        |               |                 |        |           |         |              |       |          |
|                |     |           |            |          |           |               |        | will ‘‘push’’ | dense           | points | further   | from    | less         | dense | points.  |
| SBERT uses     | a   | siamese   | or triplet | network  | structure |               | with a |               |                 |        |           |         |              |       |          |
|                |     |           |            |          |           |               |        | Using this    | distance        |        | matrix, a | minimum | spanning     |       | tree is  |
poolinglayertogeneratefixed-sizevectorrepresentationsof
|     |     |     |     |     |     |     |     | then constructed |     | via | Prim’s algorithm, |     | which | starts | from a |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | ----------------- | --- | ----- | ------ | ------ |
1https://www.kaggle.com/datasets/austinreese/trump-tweets random node and iteratively connects the shortest edge not
2https://www.kaggle.com/datasets/gpreda/covid19-tweets
3https://www.kaggle.com/datasets/omkarsabnis/yelp-reviews-dataset 4https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html
| 204094 |     |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |     |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
FIGURE5. OverviewoftheexperimentalsetupforcomparingtopicreductiontechniquesforBERTopic.
Theresultingcondensedtreeistypicallydeepandcontains
|     |     |     |     |     |     | numerous                            | nested   | clusters.       | To      | select   | clusters            | from this |
| --- | --- | --- | --- | --- | --- | ----------------------------------- | -------- | --------------- | ------- | -------- | ------------------- | --------- |
|     |     |     |     |     |     | structure,                          | HDBSCAN  | offers          | two     | cluster  | selection           | methods   |
|     |     |     |     |     |     | (definedbytheclusterselectionmethod |          |                 |         |          | parameter):‘‘excess |           |
|     |     |     |     |     |     | of mass’’                           | (eom)    | and ‘‘leaf’’.   | The     | ‘‘leaf’’ | method              | selects   |
|     |     |     |     |     |     | all leaf clusters,                  |          | while the       | ‘‘eom’’ | method   | moves               | up the    |
|     |     |     |     |     |     | tree, selecting                     | a        | parent cluster  |         | when     | it is deemed        | more      |
|     |     |     |     |     |     | ‘‘stable’’                          | than its | child clusters. |         | Cluster  | stability,          | in this   |
context,reflectshowpersistentaclusterisorhow‘‘slowly’’
itdecays.Itisworthnotingthatthe‘‘leaf’’selectionmethod
typicallyresultsinmoreoutliers,asitcapturesmorecluster
|     |     |     |     |     |     | splits, which | naturally | include | newly | created | outliers. | For |
| --- | --- | --- | --- | --- | --- | ------------- | --------- | ------- | ----- | ------- | --------- | --- |
thisstudy,weoperateundertheassumptionthatourprimary
FIGURE6. TheBERTopicframeworkshownwiththespecificchosen
modules.
goalisnottoassigneverydocumenttoatopicbutratherto
identifyunderlyingtrends.Therefore,thepresenceofoutliers
Algorithm1HDBSCANClusteringAlgorithm isacceptableinourcontextifitenhancesthecoherenceand
| Compute | the Mutual | Reachability |     | Distance | (MRD) |                                 |     |     |     |     |     |     |
| ------- | ---------- | ------------ | --- | -------- | ----- | ------------------------------- | --- | --- | --- | --- | --- | --- |
| 1:      |            |              |     |          |       | diversityofthetopicsdiscovered. |     |     |     |     |     |     |
matrixbetweenallreduceddocumentembeddings.
2: ConstructtheMinimumSpanningTree(MST)fromthe
4) TOPICREPRESENTATION
MRDgraph.
Afterthereduceddocumentembeddingshavebeenclustered,
3: Performhierarchicalclusteringbysortinganditeratively
|     |     |     |     |     |     | a topic representation |     | is generated |     | for | each cluster | using |
| --- | --- | --- | --- | --- | --- | ---------------------- | --- | ------------ | --- | --- | ------------ | ----- |
removingedgesfromtheMST.
|             |          |              |     |                 |       | CountVectorizer |     | for corpus | tokenization |     | and a | class-based |
| ----------- | -------- | ------------ | --- | --------------- | ----- | --------------- | --- | ---------- | ------------ | --- | ----- | ----------- |
| 4: Condense | the tree | by retaining |     | only the splits | where |                 |     |            |              |     |       |             |
TF-IDFproceduretodeterminetheimportanceofallwords
remainingpointsarelargerthanminimumclustersize.
inacluster,usingthisscore,thetop10mostimportantwords
Assignnoisepoints(outliers)tolabel−1.
5:
|           |                 |          |     |                       |     | for each   | cluster/topic | are   | typically | used       | for representing |     |
| --------- | --------------- | -------- | --- | --------------------- | --- | ---------- | ------------- | ----- | --------- | ---------- | ---------------- | --- |
| 6: Select | either all leaf | clusters | or  | apply stability-based |     |            |               |       |           |            |                  |     |
|           |                 |          |     |                       |     | the topic. | The c-TF-IDF  | score | is        | calculated | as described     | in  |
selection.
equation1.
7: returnFinalclustersandoutliers.
C. EVALUATION
yet included in the tree. Edges are subsequently removed For a fair and objective evaluation of the topic reduction
techniquesandduetothescaleofourexperiments,wechose
| from the | tree one by one, | starting | with | the largest | edge, |     |     |     |     |     |     |     |
| -------- | ---------------- | -------- | ---- | ----------- | ----- | --- | --- | --- | --- | --- | --- | --- |
torelyonautomatedmetrics.Morespecifically,wecompare
| causing points | or clusters | to  | split off | from the | rest. This |     |     |     |     |     |     |     |
| -------------- | ----------- | --- | --------- | -------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
processcreatesahierarchicaltreestructure.However,many eachreductiontechniquebasedontheNormalisedPointwise
|     |     |     |     |     |     | Mutual Information |     | (NPMI) | coherence |     | and topic | diversity |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | ------ | --------- | --- | --------- | --------- |
edgeremovalsmayresultinonlyafewpointsorsingletons
splitting off, resembling a decaying cluster rather than a scores. This way, we achieve both a local and global
evaluationofthereducedtopics.Inaddition,wedothisacross
| meaningful | split. To address | this, | the | tree is condensed | by  |          |                |     |           |     |           |         |
| ---------- | ----------------- | ----- | --- | ----------------- | --- | -------- | -------------- | --- | --------- | --- | --------- | ------- |
|            |                   |       |     |                   |     | multiple | configurations | of  | BERTopic, |     | each time | varying |
retainingonlyclusterswherethenumberofremainingpoints
exceedstheminimumclustersizeparameter.Pointsthatfail the minimum cluster size and the cluster selection method
parameters.
tomeetthiscriterionafterasplitareclassifiedasoutliers.
| VOLUME13,2025 |     |     |     |     |     |     |     |     |     |     |     | 204095 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
1) COHERENCE an initial BERTopic model. The choice of initial hyperpa-
|         |            |         |        |           |      |               |          | rameters | can therefore |     | significantly | influence |     | the reduction |     |
| ------- | ---------- | ------- | ------ | --------- | ---- | ------------- | -------- | -------- | ------------- | --- | ------------- | --------- | --- | ------------- | --- |
| Several | coherence  | metrics | exist, | including |      | Cv Coherence, |          |          |               |     |               |           |     |               |     |
| UMass   | Coherence, | and     | NPMI   | Coherence | [2], | [3],          | [4]. All | process. |               |     |               |           |     |               |     |
these metrics are quite similar, as they involve taking the Fig.7illustratesthisimpactfortheTrumpdataset,where
set of top N words of a topic and summing a confirmation westartedfromaminimumclustersizeof50,andincreased
measure over all word pairs. The greatest correlation with thisvalueto400instepsof50whilealternatingbetweenthe
|     |     |     |     |     |     |     |     | eom and | leaf cluster | selection |     | method. | The | plot shows | the |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ------------ | --------- | --- | ------- | --- | ---------- | --- |
humantopiccoherenceratingswasobservedwhenusingthe
NPMI metric [40]. The formula for this metric is given in number of outliers as well as the NPMI and topic diversity
equation2. scores compared to the number of topics. Moving right on
(cid:16) (cid:17) the graphs corresponds to decreasing minimum cluster size,
|     |     |     |     | P(wi | ,wj)        |     |     |            |      |         |      |                  |     |            |     |
| --- | --- | --- | --- | ---- | ----------- | --- | --- | ---------- | ---- | ------- | ---- | ---------------- | --- | ---------- | --- |
|     |     |     |     | ln   |             |     |     | leading to | more | topics. | Each | cross represents |     | a BERTopic |     |
|     |     |     |     | P (w | i )·P (w j) |     |     |            |      |         |      |                  |     |            |     |
NPMI(w ,w )= (2) model with a specific minimum cluster size and cluster
|     |     |     | i j | −ln (P | ( w , w )) |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------ | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |        | i j        |     |     |     |     |     |     |     |     |     |     |
selectionmethod.
Theleftgraphshowsthattheleafclusterselectionmethod
TheNPMIimplementation[41]usesaslidingwindowof
ten words to calculate P(w,w) (probability of w and w results in significantly more outliers compared to the eom
|           |          |     | i            | j   |          | i        | j   |                   |      |          |       |           |       |          |        |
| --------- | -------- | --- | ------------ | --- | -------- | -------- | --- | ----------------- | ---- | -------- | ----- | --------- | ----- | -------- | ------ |
|           |          |     |              |     |          |          |     | cluster selection |      | method,  | which | is        | to be | expected | since  |
| occurring | together | in  | the corpus). | In  | our case | we chose | to  |                   |      |          |       |           |       |          |        |
|           |          |     |              |     |          |          |     | taking the        | leaf | clusters | will  | result in | more  | cluster  | splits |
focusonthetop10wordsforeachtopic.ThevaluesofNPMI
rangefrom[−1,1],with1indicatingperfectco-occurrence, in HDBSCAN’s algorithm and more outliers. This implies
|                |     |               |     | −1  |            |      |     | that more | documents       |     | are excluded |     | from | clusters  | which |
| -------------- | --- | ------------- | --- | --- | ---------- | ---- | --- | --------- | --------------- | --- | ------------ | --- | ---- | --------- | ----- |
| 0 representing |     | independence, |     | and | signifying | that | two |           |                 |     |              |     |      |           |       |
|                |     |               |     |     |            |      |     | impacts   | the calculation |     | of c-TF-IDF  | and | the  | resulting | topic |
wordsneveroccurtogether.ThisrangemakesNPMIahighly
words.Genuineoutlierscanimprovetopicrepresentationby
| interpretable | measure |        | for topic | coherence. | The    | measure    | is  |          |        |               |     |           |              |     |     |
| ------------- | ------- | ------ | --------- | ---------- | ------ | ---------- | --- | -------- | ------ | ------------- | --- | --------- | ------------ | --- | --- |
|               |         |        |           |            |        |            |     | reducing | noise, | but excessive |     | exclusion | of documents |     | may |
| then averaged |         | across | all word  | pairs      | within | each topic | and |          |        |               |     |           |              |     |     |
subsequently across all topics, resulting in an overall topic negativelyinfluencecoherenceanddiversity,ascoherenceis
calculatedacrosstheentirecorpus,includingtheseoutliers.
coherencescoreforthereducedtopics.
|     |     |     |     |     |     |     |     | The middle |            | graph shows | no     | clear monotonic |            | relationship |       |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ---------- | ----------- | ------ | --------------- | ---------- | ------------ | ----- |
|     |     |     |     |     |     |     |     | between    | the number | of          | topics | and NPMI        | coherence, |              | indi- |
2) DIVERSITY
|           |           |     |       |                |     |            |     | cating the | need | for balance | in  | setting | the minimum |     | cluster |
| --------- | --------- | --- | ----- | -------------- | --- | ---------- | --- | ---------- | ---- | ----------- | --- | ------- | ----------- | --- | ------- |
| The topic | diversity | is  | found | by calculating |     | the number | of  |            |      |             |     |         |             |     |         |
size.Additionally,theplotshowsnoconsistentdifferencein
| unique words |     | in the top | m across | all | topics | and dividing | it  |     |     |     |     |     |     |     |     |
| ------------ | --- | ---------- | -------- | --- | ------ | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
coherencebetweeneomandleafselection.Itshouldbenoted
| by the total | number | of  | topic | words. | The formula | from | the |     |     |     |     |     |     |     |     |
| ------------ | ------ | --- | ----- | ------ | ----------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
thatsimilarrelationshipsareobservedbetweenthenumberof
OCTISlibraryisused[42]andisgiveninequation3where
outliersandNPMIcoherenceforboththe#Covid19andYelp
| m represents | the | top | m (10 | in our case) | words | from | each |     |     |     |     |     |     |     |     |
| ------------ | --- | --- | ----- | ------------ | ----- | ---- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
datasets.Tomaintainclarityandavoidclutter,theresultsare
| topic. A | higher | topic | diversity | indicates | better | separation | of  |     |     |     |     |     |     |     |     |
| -------- | ------ | ----- | --------- | --------- | ------ | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
notincluded,butavailableuponrequest.
differenttopics.
|     |     |     |     |     |     |     |     | Lastly, | the relationship |     | between | topic | diversity |     | and the |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ---------------- | --- | ------- | ----- | --------- | --- | ------- |
|uniquewords| number of topics is also not very straightforward. While
TD=
(3)
m×|topics| moretopicsintuitivelymightbecomelessdiverse,forsmall
|                         |     |     |     |     |     |     |     | numbers   | of topics, | this    | relation  | is less | apparent | and            | differs |
| ----------------------- | --- | --- | --- | --- | --- | --- | --- | --------- | ---------- | ------- | --------- | ------- | -------- | -------------- | ------- |
| V. RESULTSANDDISCUSSION |     |     |     |     |     |     |     |           |            | cluster | selection | method. |          |                |         |
|                         |     |     |     |     |     |     |     | depending | on         | the     |           |         |          | For short-text |         |
This section presents the results of our analysis and is datasets, such as Trump and #Covid19, we found that eom
structured as follows. First, we examine the direct topic cluster selection often results in more diverse topics. This
| reduction | method | by  | analyzing | the | effects | of different |     |                |      |           |     |        |             |       |     |
| --------- | ------ | --- | --------- | --- | ------- | ------------ | --- | -------------- | ---- | --------- | --- | ------ | ----------- | ----- | --- |
|           |        |     |           |     |         |              |     | pattern aligns | with | intuition | but | is not | universally | true. | For |
HDBSCAN parameter settings on the resulting topics. Yelpreviews,therelationshipwesawislessconsistent:eom
Next, we compare this benchmark with indirect topic selection yields better coherence at lower minimum cluster
reduction methods via agglomerative clustering (using the sizes,whileleafselectionperformsbetterathigherminimum
different topic embeddings). Finally, we discuss the results clustersizes.Thesevariationsunderscorethedependencyon
| of LLM-prompting |     | and | compare | this | method | to both | the |     |     |     |     |     |     |     |     |
| ---------------- | --- | --- | ------- | ---- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
theinitialBERTopicconfiguration.
benchmarkandagglomerativeclustering. To ensure robustness against the influence of the initial
|     |     |     |     |     |     |     |     | parameter | settings, | we  | run multiple | configurations |     | for | each |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --------- | --- | ------------ | -------------- | --- | --- | ---- |
A. INCREASINGTHEMINIMUMCLUSTERSIZE dataset, apply the topic reduction techniques, and report
Beforecomparingdifferentindirecttopicreductionmethods, the average coherence and diversity across runs. For the
wefirstillustratekeypropertiesoftheBERTopicframework. Trump dataset, this involved six different configurations:
Specifically,weexaminetheimpactoftheminimumcluster threedifferentclustersizes(50,100and150),eachevaluated
size and cluster selection method in HDBSCAN on the with both the eom and leaf cluster selection methods. The
number of topics, NPMI coherence, topic diversity, and the #Covid-19 dataset used six configurations as well (with
number of outliers. Understanding this impact is crucial, clustersizes100,200and300).FortheYelpreviewsdataset,
as other reduction techniques build on topics generated by weusedeightconfigurations:fourdifferentminimumcluster
| 204096 |     |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |     |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
FIGURE7. Numberofoutlierdocuments,NPMIcoherenceandtopicdiversitycomparedtothenumberoftopicsforthebenchmarktopic
reductionmethodfortheTrumpTweetsdataset.Eachcrossindicatesanincreaseof50oftheminimumclustersizeparameterinHDBSCAN.The
linecolourindicatestheclusterselectionmethodwhichcanbe‘excessofmass’(eom)ortheleafclusterselectionmethod.
sizes (10, 20, 30 and 40), again with both cluster selection dataset, where the coherence gap is slightly larger, and the
methods. SBERT top 10 Words embedding performs the poorest. For
Tocompareincreasingtheminimumclustersizewithother the #Covid19 dataset, the c-TF-IDF, the average reduced
topic reduction techniques, two predefined topic counts are SBERT, and the SBERT LLM Label embedding slightly
chosen for each dataset: 50 and 25 for the Trump dataset, outperform the benchmark in coherence when reducing to
100 and 50 for the #Covid19 dataset, and 40 and 20 for 100 topics. When further reducing to 50 topics, only the
the Yelp reviews dataset. To achieve these target quantities, c-TF-IDF and SBERT LLM Label embeddings continue
weadjustedtheminimumclustersizeuntilthedesirednumber to show higher coherence, suggesting that topic reduction
of topics was approximately reached (within a range of performance through agglomerative clustering also depends
±10%), also alternating between the eom and leaf cluster onthedataset.
selectionmethods. Whenexaminingtopicdiversity,adifferenttrendemerges.
|     |     |     |     | Agglomerative | clustering         | results | in significantly | higher |
| --- | --- | --- | --- | ------------- | ------------------ | ------- | ---------------- | ------ |
|     |     |     |     | diversity     | than the benchmark | method. | The c-TF-IDF     | and    |
B. AGGLOMERATIVECLUSTERING
First,wecomparethebenchmarkofincreasingtheminimum SBERT LLM Label embeddings yield the most diverse
clustersizetoagglomerativeclustering,whichencompasses topics,withdiversityscoresapproximately0.10higherwhen
|     |     |     |     | reducing | to 50 topics | and 0.06 | higher when reducing | to  |
| --- | --- | --- | --- | -------- | ------------ | -------- | -------------------- | --- |
fourdifferenttypesoftopicembeddings(SectionIII).Figs.8
and9presenttheNPMIcoherenceandtopicdiversityscores, 25 topics in the Trump dataset. The same holds true for
|     |     |     |     | the #Covid19 | tweets | and Yelp | Reviews datasets, | where |
| --- | --- | --- | --- | ------------ | ------ | -------- | ----------------- | ----- |
respectively,foreachdatasetandreductionmethodwiththe
line colouring representing the reduced topic count. Within the largest increases in diversity are also observed when
each dataset, the topic count differs and only lines of the usingthec-TF-IDForSBERTLLMlabelembedding.While
|             |             |              |                    | the average | reduced SBERT | embedding | and SBERT | Top |
| ----------- | ----------- | ------------ | ------------------ | ----------- | ------------- | --------- | --------- | --- |
| same colour | should thus | be compared, | as they correspond |             |               |           |           |     |
to reductions to the same number of topics. The NPMI 10 words embedding also produce more diverse topics than
thebenchmarkfortheTrumptweets,theydonotsurpassc-
| coherence | and topic | diversity values | for the reduced topics |     |     |     |     |     |
| --------- | --------- | ---------------- | ---------------------- | --- | --- | --- | --- | --- |
are averaged across various runs involving different fixed TF-IDF or SBERT LLM Label embeddings. For the other
HDBSCAN parameter settings, as discussed previously. datasets, the average reduced SBERT embedding struggles
toachieveahigherdiversityscorethanthebenchmark.One
| To illustrate | stability | across configurations, | standard devi- |     |     |     |     |     |
| ------------- | --------- | ---------------------- | -------------- | --- | --- | --- | --- | --- |
ations are provided in parentheses. Some methods display possibleexplanationforthepoorperformanceoftheaverage
a higher standard deviation than others, suggesting that reduced SBERT embedding is that it relies on a centroid-
their performance is more sensitive to the initial BERTopic based representation, which is less suited for density-based
configuration. clusters.Additionally,theworseperformanceoftheSBERT
|     |     |     |     | Top 10 | Words embedding | compared | to the SBERT | LLM |
| --- | --- | --- | --- | ------ | --------------- | -------- | ------------ | --- |
FortheTrumpdataset,thebenchmarkmethodachievesthe
highestcoherencecomparedtoagglomerativeclusteringwith Labelembeddingcanbeexplainedbythefactthatitdoesnot
differentembeddings.Whenreducingto50topics,coherence capture contextual information, as the top 10 words are not
structuredintoasentence.TheLLM-generatedlabel,onthe
| is 0.025 | higher than | with the c-TF-IDF | and SBERT LLM |     |     |     |     |     |
| -------- | ----------- | ----------------- | ------------- | --- | --- | --- | --- | --- |
Label embeddings. A similar but smaller gap is observed otherhand,providesamoremeaningfulrepresentation.
Overall,reducingtopicsthroughagglomerativeclustering
| when reducing | to 25 | topics, with | c-TF-IDF embedding |     |     |     |     |     |
| ------------- | ----- | ------------ | ------------------ | --- | --- | --- | --- | --- |
performing best again, followed by the SBERT LLM label leads to more diverse topics compared to the benchmark
embedding. The average Reduced SBERT embedding and method,whileremainingcompetitiveintermsofcoherence.
|     |     |     |     | The increase | in diversity | appears | to be more | significant |
| --- | --- | --- | --- | ------------ | ------------ | ------- | ---------- | ----------- |
SBERTTop10Wordsembeddingresultinlowercoherence,
with the average reduced SBERT embedding performing than the decrease in coherence, but the choice between
coherenceanddiversitydependsonthespecificapplication.
| the worst.    | A similar | pattern emerges | in the Yelp Reviews |     |     |     |     |        |
| ------------- | --------- | --------------- | ------------------- | --- | --- | --- | --- | ------ |
| VOLUME13,2025 |           |                 |                     |     |     |     |     | 204097 |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
FIGURE8. ValuesrepresentmeanNPMIcoherencescores(standarddeviationacrosssixHDBSCANconfigurations)oftheagglomerativeclustering
reductionmethodwhenreducingtotwopredefinedtopicamounts.Differenttopicembeddingsarecomparedwiththebenchmark(increasing
min.clustersize)acrossdatasets.Increasingtheminimumclustersizeperformsstronglyincoherence,closelyfollowedbyagglomerative
clusteringwithc-TF-IDFtopicembeddings.
FIGURE9. Valuesrepresentmeantopicdiversityscores(standarddeviationacrosssixHDBSCANconfigurations)oftheagglomerativeclustering
reductionmethodwhenreducingtotwopredefinedtopicamounts.Differenttopicembeddingsarecomparedwiththebenchmark(increasing
min.clustersize)acrossdatasets.Thec-TF-IDFembeddingconsistentlyachievesthehighestdiversity.
Amongtheembeddings,c-TF-IDFemergesasthepreferred samecolourshouldbecomparedwithineachdataset,asthey
option, with the SBERT LLM Label embedding as a correspondtothesamereducedtopiccount.
viablealternative,thoughthelatterismorecomputationally For the Trump dataset, when reducing to 50 topics,
intensive without offering substantial improvements over LLM prompting struggles to surpass the benchmark in
c-TF-IDF. Given its simplicity and strong performance, coherence,thoughthegapissmallerthanwithagglomerative
c-TF-IDF is recommended for agglomerative clustering. clustering. However, when reducing to 25 topics with GPT
The average reduced SBERT embedding and SBERT Top promptingusingeitherthetop10wordsorLlama,coherence
10 words embedding are less favourable, as they perform improves significantly. Among the LLM-based methods,
poorlyinbothcoherenceanddiversitycomparedtotheother GPT prompting with the top 10 words achieves the highest
| topicembeddings. |     |     |     | overallcoherenceforthisdataset. |     |     |     |     |
| ---------------- | --- | --- | --- | ------------------------------- | --- | --- | --- | --- |
Forthe#Covid19dataset,GPTprompting(whetherusing
|     |     |     |     | the top | 10 words or | the LLM-generated | label) | results in |
| --- | --- | --- | --- | ------- | ----------- | ----------------- | ------ | ---------- |
C. LLMPROMPTING
Finally, we describe the results obtained using the LLM a higher coherence than the benchmark for both 100 and
|           |                         |            |                    | 50 topics. | Llama also     | slightly improves | coherence   | when      |
| --------- | ----------------------- | ---------- | ------------------ | ---------- | -------------- | ----------------- | ----------- | --------- |
| prompting | method, as described    | in Section | III. It should     |            |                |                   |             |           |
|           |                         |            |                    | reducing   | to 100 topics, | but when          | reducing to | 50, it no |
| be noted  | that for GPT prompting, | we use     | either the topic’s |            |                |                   |             |           |
top 10 words or the LLM-generated topic label. For Llama longeroutperformsthebenchmark.Overall,GPTprompting
|            |              |                   |                | provides | the highest | coherence gains | for this dataset. | For |
| ---------- | ------------ | ----------------- | -------------- | -------- | ----------- | --------------- | ----------------- | --- |
| prompting, | we only used | the top 10 words, | as Llama often |          |             |                 |                   |     |
refusedtogeneratemeaningfulresultswhenusingtheLLM- the Yelp reviews dataset, none of the LLM prompting
|           |                 |                |                   | methods | improve coherence | compared | to the benchmark. |     |
| --------- | --------------- | -------------- | ----------------- | ------- | ----------------- | -------- | ----------------- | --- |
| generated | label. Figs. 10 | and 11 present | the coherence and |         |                   |          |                   |     |
However,whencomparingLLMpromptingmethodsamong
| diversity | scores across the | three datasets | when reducing to |     |     |     |     |     |
| --------- | ----------------- | -------------- | ---------------- | --- | --- | --- | --- | --- |
two predefined topic counts. As before, only lines of the themselves,GPTstillslightlyoutperformsLlama.
| 204098 |     |     |     |     |     |     | VOLUME13,2025 |     |
| ------ | --- | --- | --- | --- | --- | --- | ------------- | --- |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
FIGURE10. ValuesrepresentmeanNPMIcoherencescores(standarddeviationacrosssixHDBSCANconfigurations)oftheLLMpromptingmethod
whenreducingtotwopredefinedtopicamounts,comparedwiththebenchmark(increasingmin.clustersize)acrossdatasets.TheLLMprompting
methodshowscompetitiveperformancetothebenchmark,withsomedataset-specificvariationandmorepronounceddifferencesbetweenthe
tworeductionamounts.
FIGURE11. Valuesrepresentmeantopicdiversityscores(standarddeviationacrosssixHDBSCANconfigurations)oftheLLMpromptingmethod
whenreducingtotwopredefinedtopicamounts,comparedwiththebenchmark(increasingmin.clustersize)acrossdatasets.Theprompting
methodconsistentlyoutperformsthebenchmark,withGPTprompting(top-10wordsrepresentation)showingthestrongestperformance.
Regarding topic diversity, LLM prompting significantly TABLE6. Runtimeandtokenusagefordifferenttopicreductionmethods
onatoyexamplefromtheTrumpTweetsdataset.
| enhances     | diversity     | compared | to the   | benchmark  | across | all     |     |     |     |     |     |
| ------------ | ------------- | -------- | -------- | ---------- | ------ | ------- | --- | --- | --- | --- | --- |
| datasets.    | GPT prompting |          | with the | topic’s    | top 10 | words   |     |     |     |     |     |
| consistently | achieves      | the      | highest  | diversity. | The    | ranking |     |     |     |     |     |
betweenGPTpromptingwiththeLLM-generatedlabeland
| Llama prompting |     | with the   | top 10 | words   | varies depending |     |     |     |     |     |     |
| --------------- | --- | ---------- | ------ | ------- | ---------------- | --- | --- | --- | --- | --- | --- |
| on the dataset  | and | the number | of     | topics. | Additionally,    | for |     |     |     |     |     |
theTrumpandYelpreviewsdatasets,LLMpromptingyields
| higher maximum |     | diversity | than agglomerative |     | clustering, |     |     |     |     |     |     |
| -------------- | --- | --------- | ------------------ | --- | ----------- | --- | --- | --- | --- | --- | --- |
thoughforthe#Covid19dataset,itfallsjustshort.
| One possible | explanation    |                   | for these | results         | is that        | GPT     |     |     |     |     |     |
| ------------ | -------------- | ----------------- | --------- | --------------- | -------------- | ------- | --- | --- | --- | --- | --- |
| prompting    | with           | the topic’s       | top 10    | words           | captures       | more    |     |     |     |     |     |
| information  | than           | the LLM-generated |           | label.          | It is possible |         |     |     |     |     |     |
| that the     | LLM inherently |                   | performs  | an intermediate |                | step of |     |     |     |     |     |
generatingalabelandcomparingitwithothertopics,making
the explicit LLM label generation redundant. Additionally, in both coherence and diversity. However, this approach is
whileLlamaperformswell,itisoftenslightlyoutperformed
morecomputationallyintensive,asitrequiresrepeatedLLM
by GPT. This may be due to differences in model size calls, which may be costly depending on the application.
| andcapabilities(GPT-4o-mini |     |     | isgenerallyconsideredmore |     |     |     |               |          |               |                      |     |
| --------------------------- | --- | --- | ------------------------- | --- | --- | --- | ------------- | -------- | ------------- | -------------------- | --- |
|                             |     |     |                           |     |     |     | Additionally, | c-TF-IDF | must still be | computed beforehand, |     |
advancedthanLlama-38B-Instruct),whichcouldexplainits as it is necessary for generating the top 10 words used
strongerperformance. in LLM prompting. When comparing short and long texts,
Insummary,whenreducingtopicsusingLLMprompting,
|     |     |     |     |     |     |     | Yelp reviews | are generally | longer than | tweets, which | may |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ------------- | ----------- | ------------- | --- |
GPT-4o-mini with the topic’s top 10 words is preferred enhancetransformerembeddingsand,consequently,improve
| and LLM | prompting | outperforms |     | agglomerative | clustering |     |     |     |     |     |     |
| ------- | --------- | ----------- | --- | ------------- | ---------- | --- | --- | --- | --- | --- | --- |
HDBSCAN’sclusteringquality.Thiscouldexplainwhythe
| VOLUME13,2025 |     |     |     |     |     |     |     |     |     |     | 204099 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ |

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
FIGURE12. Flowchartforselectingatopicreductionmethodbasedondatacharacteristics,performancepriorities,andresourceconstraints.Qualitative
decisionpointssuchas‘‘highcoherence’’and‘‘highdiversity’’representtheirrelativeimportancewithinthecontextofspecifictasksanduser
preferences,withoutfixedthresholds.Thisflowchartisintendedasgeneralguidanceratherthanastrictdecisionrule.
benchmarkmethodperformsrelativelywellforYelpreviews, as each topic must first be labeled by an LLM before being
astheinitialclusteringstepyieldsmorecoherenttopicsthan embedded with SBERT. The LLM prompting methods are
otherreductionmethods.However,whentopicdiversityisa substantially slower and incur additional token costs. When
primaryconcern,alternativemethodsremainpreferable. prompting with the top 10 words, token usage is limited
to identifying overlapping topics. However, prompting with
LLM-generated topic labels requires an additional labeling
D. RUNTIMEANDTOKENUSAGE
step, resulting in significantly higher runtimes and token
This subsection compares the computational costs of the
consumption.
evaluated topic reduction methods. Both runtime and token
usage depend strongly on the number of topics present VI. CONCLUSIONANDRECOMMENDATIONS
before applying reduction. To illustrate relative differences, This study is the first to categorize and compare various
we report a simple example of reducing 50 topics to topic reduction techniques for the BERTopic framework.
25 topics from the Trump Tweets dataset, with runtimes Byrevealingsomeofthe‘‘blackbox’’aspectsofBERTopic
and token usage summarized in Table 6. All LLM-based and exploring how different initial configurations and topic
reductionswereperformedviatheOpenAIAPI.Experiments reduction techniques affect the quality of reduced topics,
were conducted on a laptop equipped with an NVIDIA weallowuserstomakemoreinformeddecisionswhenusing
RTX4050GPU,anIntel(R)Core(TM)Ultra7CPU,and32 theframework,enhancingboththeusabilityandeffectiveness
GBRAM. ofBERTopic.
Since increasing the minimum cluster size represents a Ourfindingsshowthatdirecttopicreductionbyincreasing
directreductionmethod,noseparateruntimeisreported,asit the minimum cluster size in HDBSCAN often results in
requires re-running the entire BERTopic model rather than coherent topics. However, indirect reduction methods offer
an additional reduction step. Among the indirect methods, greater diversity and diversity can often be significantly
agglomerative clustering based on the c-TF-IDF, average improved with little or no loss of coherence, particularly
reduced SBERT, or SBERT Top-10 words embeddings is in short-text datasets. For longer texts, such as the Yelp
very fast because these embeddings are already computed review,thedirectmethodyieldsahighcoherencescore,while
during the initial BERTopic run. Using the SBERT LLM indirect approaches show a notable drop in coherence but
label embedding introduces a clear increase in runtime, substantially improve diversity. This suggests that for long
204100 VOLUME13,2025

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
texts, there could be a trade-off between high diversity and prompting with the top 10 topic words is a strong option.
highcoherencewhenreducingtopics.Greatertopicdiversity Otherwise, agglomerative clustering based on the topic’s
is especially valuable in scenarios where capturing a wider c-TF-IDFembeddingisamoreefficientalternative.Formid-
rangeofperspectivesisdesired. length texts, users are advised to experiment with different
Forindirecttopicreductionwithagglomerativeclustering, approaches while considering the results presented in this
c-TF-IDF is the most effective topic embedding, offering study.Areasonablestartingpointisthebenchmarkmethod,
strongperformancewithminimalcomputationalcost.While followedbyagglomerativeclusteringusingthetopic’sc-TF-
theSBERTLLMlabelembeddingisapotentialalternative, IDFembedding.
it is more resource-intensive (as it requires an LLM for Itshouldbenotedthattheserecommendationsarebasedon
labellingtopics)withoutsignificantimprovements.Theaver- theresultsobtainedforthespecificdatasetsinthisstudy,and
agereducedSBERTandSBERTTop10wordsembeddings outcomesmayvarydependingontheapplication.Wesuggest
are less favorable, as they in most cases perform poorly in starting with a BERTopic configuration that produces a
both coherence and diversity compared to the other topic manageable number of topics before applying a reduction
embeddings. technique. By experimenting with different configurations
For indirect topic reduction via LLM prompting, using and leveraging the outlined techniques, users can achieve
GPT-4o-mini with the top 10 topic words of each topic optimalresultstailoredtotheirdatasetsandobjectives.
appears to be the most practical and effective method
for short-text datasets. It achieves an excellent balance VII. LIMITATIONSANDFUTURERESEARCH
between high diversity, good coherence, and relatively low While this study provides a comprehensive comparison
computational cost compared to prompting GPT with the of topic reduction methods for BERTopic, a number of
LLM-generated topic labels. Prompting GPT with a topic’s limitationsremain.
top 10 words avoids the need to re-label merged topics at First,thisstudyprimarilyexaminestopicreductionwithin
each iteration. Llama also shows promise, achieving high the BERTopic framework. While BERTopic is widely used,
diversityanddecentcoherencewiththetop10topicwords. other topic modeling techniques, such as Top2Vec, could
However, it falls slightly short of GPT and can be sensitive benefit from similar comparative studies. Future research
to certain corpus content, occasionally refusing to process could explore whether the findings from this study hold
specifictopics. across different topic modeling frameworks and investigate
Finally, LLM prompting tends to outperform agglomer- how reduction techniques influence results in alternative
ative clustering in both coherence and diversity. However, clusteringorembeddingconfigurations.
it is more computationally expensive due to the need for Second, the study focuses on a limited set of datasets,
multiple LLM calls and is also slower, potentially incurring primarilyconsistingofshortsocialmediatextsandcustomer
costsdependingontheapplication.Sincec-TF-IDFmustbe reviews. While these are relevant for many applications,
computed beforehand to generate the top 10 words before it remains unclear how well the proposed topic reduction
prompting can be applied, this method will always be more techniques generalize to more structured domains, such as
compute-intensivethanagglomerativeclusteringwiththec- scientific literature, legal documents, or highly technical
TF-IDFembedding. corpora. Exploring topic reduction in these contexts would
To support practitioners in selecting an appropriate topic bevaluableforexpandingtheapplicabilityofBERTopic.
reductionmethod,weproposeadecisionflowchart(Fig.12). Third, due to the scale of our experiments, we did
It is designed to guide users based on the type of input not perform human or LLM-based qualitative evaluations.
text (short vs. long), the relative importance of coherence Instead, we relied on validated automated metrics (e.g.,
vs. diversity in their use case, and computational resource NPMI), following the precedent of prior studies [1], [3],
availability. While the flowchart uses qualitative decision [4]. Similarly, we did not apply formal statistical tests
points like ‘‘high coherence’’ and ‘‘high diversity’’ these (e.g. Friedman test) due to their limited applicability in
termsrefertotherelativeimportanceofthesemetricsinthe unsupervised topic modeling and the small number of
contextofthespecificdownstreamtask.Thesearenotbased datasets, which would result in low statistical power [21],
onfixedthresholds,asacceptablevaluescanvarybyusecase [43]. We acknowledge that the absence of statistical testing
anduserpreference. andhumanevaluationlimitsthestrengthoftheevidenceand
Thefirstdecisiondependsonwhetheryourdatasetconsists future work could explore incorporating human evaluation
of short texts (<40 words on average) or longer texts (>100 and statistical analyses to further validate the comparative
words on average). Next, a trade-off is made between findings.
coherenceanddiversity.Ifcoherenceispreferred,increasing Finally, there are some limitations related to the use of
the minimum cluster size is often sufficient. If diversity LLM prompting for topic reduction. While these methods
is important, an indirect reduction method should be offer promising improvements in topic diversity, they come
considered.Thechoicedependsoncomputationalresources with significant computational costs. In this study, we used
and processing speed requirements. If sufficient computing GPT-4o-mini and Llama-3-8B, selecting methods that are
power is available and speed is not a major concern, GPT alreadywell-establishedandwidelyadopted.Giventherapid
VOLUME13,2025 204101

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
developmentinthisfieldandthegrowingnumberofavailable [20] R. Cheruku, K. Hussain, I. Kavati, A. M. Reddy, and K. S. Reddy,
implementations, future work could explore the integration ‘‘SentimentclassificationwithmodifiedRoBERTaandrecurrentneural
networks,’’ Multimedia Tools Appl., vol. 83, no. 10, pp.29399–29417,
of morelightweight orfine-tuned LLMs whichmay leadto
Sep.2023.
morescalableandcost-effectivesolutionsfortopicreduction. [21] Zoya,S.Latif,F.Shafait,andR.Latif,‘‘AnalyzingLDAandNMFtopic
Beyondcomputationalcosts,LLMscanalsobeconstrained models for Urdu tweets via automatic labeling,’’ IEEE Access, vol. 9,
pp.127531–127547,2021.
bytokenlimits,especiallywhenprocessinganexceptionally
[22] M.Reusens,M.Reusens,M.Callens,S.vandenBroucke,andB.Baesens,
large number of topics. In addition, their outputs can be ‘‘Comparison of different modeling techniques for flemish Twitter
inconsistent and often depend heavily on the quality of sentimentanalysis,’’Analytics,vol.1,no.2,pp.117–134,Oct.2022.
[23] A.BogdanowiczandC.Guan,‘‘DynamictopicmodelingofTwitterdata
prompt engineering and the nature of the content itself. For
duringtheCOVID-19pandemic,’’PLoSONE,vol.17,no.5,May2022,
example, performance may vary when handling sensitive Art.no.e0268669.
material such as political tweets. Future research could [24] B.Janssens,M.Bogaert,andD.VandenPoel,‘‘Evaluatingtheinfluence
ofairbnblistings’descriptionsondemand,’’Int.J.HospitalityManage.,
include ablation studies on prompt design and temperature
vol.99,Oct.2021,Art.no.103071.
settingstobetterunderstandtheirimpactonperformance. [25] D. Yu, D. Xu, D. Wang, and Z. Ni, ‘‘Hierarchical topic modeling of
Twitter data for online analytical processing,’’ IEEE Access, vol. 7,
pp.12373–12385,2019.
REFERENCES [26] A.Crijns,V.Vanhullebusch,M.Reusens,M.Reusens,andB.Baesens,
‘‘Topicmodellingappliedoninnovationstudiesofflemishcompanies,’’J.
[1] M.Grootendorst,‘‘BERTopic:Neuraltopicmodelingwithaclass-based
Bus.Anal.,vol.6,no.4,pp.243–254,Oct.2023.
TF-IDFprocedure,’’2022,arXiv:2203.05794.
[27] A.Abdelrazek,Y.Eid,E.Gawish,W.Medhat,andA.Hassan,‘‘Topic
[2] R.EggerandJ.Yu,‘‘AtopicmodelingcomparisonbetweenLDA,NMF, modeling algorithms and applications: A survey,’’ Inf. Syst., vol. 112,
Top2Vec,andBERTopictodemystifyTwitterposts,’’FrontiersSociology, Feb.2023,Art.no.102131.
vol.7,May2022,Art.no.886498. [28] Y.Zhang,R.Jin,andZ.-H.Zhou,‘‘Understandingbag-of-wordsmodel:
[3] A.AbuzayedandH.Al-Khalifa,‘‘BERTforArabictopicmodeling:An Astatisticalframework,’’Int.J.Mach.Learn.Cybern.,vol.1,nos.1–4,
experimentalstudyonBERTopictechnique,’’Proc.Comput.Sci.,vol.189, pp.43–52,Dec.2010.
pp.191–194,Jan.2021. [29] D.M.Blei,A.Y.Ng,andM.I.Jordan,‘‘LatentDirichletallocation,’’J.
[4] B. Ogunleye, T. Maswera, L. Hirsch, J. Gaudoin, and T. Brunsdon, Mach.Learn.Res.,vol.3,pp.993–1022,Jan.2003.
‘‘Comparisonoftopicmodellingapproachesinthebankingcontext,’’Appl. [30] Q.V.LeandT.Mikolov,‘‘Distributedrepresentationsofsentencesand
Sci.,vol.13,no.2,p.797,Jan.2023. documents,’’inProc.Int.Conf.Mach.Learn.,vol.4,2014,pp.1188–1196.
[5] N. Reimers and I. Gurevych, ‘‘Sentence-BERT: Sentence embeddings [31] D. Angelov, ‘‘Top2 Vec: Distributed representations of topics,’’ 2020,
usingSiameseBERT-networks,’’2019,arXiv:1908.10084. arXiv:2008.09470.
[32] B.DasandS.Chakraborty,‘‘Animprovedtextsentimentclassification
[6] L. McInnes, J. Healy, N. Saul, and L. Großberger, ‘‘UMAP: Uniform
modelusingTF-IDFandnextwordnegation,’’2018,arXiv:1806.06407.
manifoldapproximationandprojection,’’J.OpenSourceSoftw.,vol.3,
[33] L.Gan,T.Yang,Y.Huang,B.Yang,Y.Y.Luo,L.Richard,andD.Guo,
no.29,p.861,Sep.2018,doi:10.21105/joss.00861.
‘‘ExperimentalcomparisonofthreetopicmodelingmethodswithLDA,
[7] C.MalzerandM.Baum,‘‘Ahybridapproachtohierarchicaldensity-based
Top2VecandBERTopic,’’inProc.Int.Symp.Artif.Intell.Robot.,2024,
cluster selection,’’ in Proc. IEEE Int. Conf. Multisensor Fusion Integr.
pp.376–391.
Intell.Syst.(MFI),Sep.2020,pp.223–228.
[34] S.C.Turan,K.Yildiz,andB.Büyüktanir,‘‘ComparisonofLDA,NMF
[8] M.deGroot,M.Aliannejadi,andM.R.Haas,‘‘Experimentsongeneraliz- and BERTopic topic modeling techniques on Amazon product review
abilityofBERTopiconmulti-domainshorttext,’’2022,arXiv:2212.08459. dataset:Acasestudy,’’inProc.Int.Conf.Comput.Intell.DataAnal.,2024,
[9] A. Baird, Y. Xia, and Y. Cheng, ‘‘Consumer perceptions of telehealth pp.23–31.
for mental health or substance abuse: A Twitter-based topic modeling [35] D.Stammbach,V.Zouhar,A.Hoyle,M.Sachan,andE.Ash,‘‘Revisiting
analysis,’’JAMIAOpen,vol.5,no.2,p.028,Apr.2022. automated topic model evaluation with large language models,’’ 2023,
[10] B.Koloski,N.Lavrač,B.Cestnik,S.Pollak,B.Škrlj,andA.Kastrin, arXiv:2305.12152.
‘‘AHAM:Adapt,help,ask,modelharvestingllmsforliteraturemining,’’ [36] Y.Mu,C.Dong,K.Bontcheva,andX.Song,‘‘Largelanguagemodels
inProc.Int.Symp.Intell.DataAnal.,2024,pp.254–265. offeranalternativetothetraditionalapproachoftopicmodelling,’’2024,
[11] D. Li, B. Zhang, and Y. Zhou, ‘‘Can large language models (LLM) arXiv:2403.16248.
labeltopicsfromatopicmodel?’’SocArXiv,2023.[Online].Available: [37] P.Sahoo,A.KumarSingh,S.Saha,V.Jain,S.Mondal,andA.Chadha,
https://doi.org/10.31235/osf.io/23x4m ‘‘Asystematicsurveyofpromptengineeringinlargelanguagemodels:
Techniquesandapplications,’’2024,arXiv:2402.07927.
[12] T.Doi,M.Isonuma,andH.Yanaka,‘‘Topicmodelingforshorttextswith
[38] J.D.M.-W.C.KentonandL.K.Toutanova,‘‘Bert:Pre-trainingofdeep
large language models,’’ in Proc. 62nd Annu. Meeting Assoc. Comput.
bidirectionaltransformersforlanguageunderstanding,’’inProc.NAACL-
LinguisticsStudentRes.Workshop,2024,pp.21–33.
HLT,J.Bursteinetal.,Eds.,AssociationforComputationalLinguistics,
[13] H. Wang, N. Prakash, N. K. Hoang, M. S. Hee, U. Naseem, and
2019,pp.4171–4186.
R.K.-W.Lee,‘‘Promptinglargelanguagemodelsfortopicmodeling,’’in
[39] UmapDocumentation.Accessed:Feb.5,2024.[Online].Available:https://
Proc.IEEEInt.Conf.BigData(BigData),Dec.2023,pp.1236–1241.
umap-learn.readthedocs.io/en/latest/parameters.html
[14] C.MinhPham,A.Hoyle,S.Sun,P.Resnik,andM.Iyyer,‘‘TopicGPT:A [40] M. Röder, A. Both, and A. Hinneburg, ‘‘Exploring the space of topic
prompt-basedtopicmodelingframework,’’2023,arXiv:2311.01449. coherence measures,’’ in Proc. 8th ACM Int. Conf. Web Search Data
[15] (2024).GPT-4OMini:AdvancingCost-EfficientIntelligence.Accessed: Mining,Feb.2015,pp.399–408.
Feb.7,2025.[Online].Available:https://openai.com/index/gpt-4o-mini- [41] R. Řehuřek and P. Sojka, ‘‘Software framework for topic mod-
advancing-cost-efficient-intelligence/ elling with large corpora,’’ in Proc. LREC Workshop New Chal-
[16] (2024). Llama 3: Open Foundation and Fine-Tuned Chat Models. lenges NLP Frameworks, May 2010, pp.45–50. [Online]. Available:
Accessed: Feb. 27, 2025. [Online]. Available: https://ai.meta.com/bl http://is.muni.cz/publication/884893/en
og/meta-llama-3/ [42] S. Terragni,E. Fersini,B. G.Galuzzi, P.Tropeano, andA. Candelieri,
[17] D.M.BleiandJ.D.Lafferty,‘‘Topicmodels,’’inTextMining.London, ‘‘OCTIS:Comparingandoptimizingtopicmodelsissimple!’’inProc.
U.K.:Chapman&Hall,2009,pp.101–124. 16th Conf. Eur. Chapter Assoc. Comput. Linguistics, Syst. Demonstra-
[18] P.KherwaandP.Bansal,‘‘Topicmodeling:Acomprehensivereview,’’ tions,2021,pp.263–270.
EAIEndorsedTrans.scalableInf.Syst.,vol.7,no.24,Jul.2018,Art.no. [43] S. García, A. Fernández, J. Luengo, and F. Herrera, ‘‘Advanced
159623,doi:10.4108/eai.13-7-2018.159623. nonparametric tests for multiple comparisons in the design of exper-
[19] G.Xu,Y.Meng,Z.Chen,X.Qiu,C.Wang,andH.Yao,‘‘Researchon iments in computational intelligence and data mining: Experimen-
topicdetectionandtrackingforonlinenewstexts,’’IEEEAccess,vol.7, tal analysis of power,’’ Inf. Sci., vol. 180, no. 10, pp.2044–2064,
pp.58407–58418,2019. May2010.
204102 VOLUME13,2025

W.Janssensetal.:ComparativeAnalysisofTopicReductionTechniquesforBERTopic
WANNES JANSSENS receivedtheM.S.degree DIRK VAN DEN POEL (SeniorMember,IEEE)
(summa cum laude) in business engineering: received the master’s degree in business engi-
data analytics from Ghent University, in 2024. neering and the Ph.D. degree from KU Leuven.
HeiscurrentlyaPh.D.ResearcherwiththeData He is currently a Senior Full Professor of data
AnalyticsResearchGroup,GhentUniversity.Heis analytics,bigdata,andAIwithGhentUniversity,
with FlandersMake@UGent—corelab CVAMO. Belgium. He teaches courses, such as big data
His research interests include natural language andanalyticalcustomerrelationshipmanagement.
processing, predictive and prescriptive analytics, In1999,heco-foundedtheadvancedMaster’sof
andmachinelearning,withapplicationsinreman- Scienceinmarketinganalysis,thefirst(predictive)
ufacturingandstrategicdecision-making. analyticsmaster’sprogramintheworld,andthe
Master’sofScienceinstatisticaldataanalysisandtheMaster’sofSciencein
businessengineering/dataanalytics.Hehasco-authoredmorethan150peer-
reviewedresearchpublicationsinjournals,suchasJournalofMarketing,
MATTHIASBOGAERTiscurrentlyanAssociate JournalofStatisticalSoftware,JournalofProductInnovationManagement
ProfessorofdataanalyticswithGhentUniversity, (Best Paper Award), in 2017, Computers and Chemical Engineering,
whereheteachessocialmediaandwebanalytics EuropeanJournalofOperationalResearch,IEEETRANSACTIONSONPARALLEL
andpredictiveandprescriptiveanalytics.Heisalso ANDDISTRIBUTEDSYSTEMS,DecisionSupportSystems,andIEEETRANSACTIONS
affiliated with FlandersMake@UGent—corelab ONPOWERSYSTEMS.Hehasgraduatedmorethan20Ph.D.students.Several
CVAMO,andaVisitingProfessorwiththeUniver- ofthemarecontinuingtheircareersinU.S.Hehelpedmorethan100for-
sityofNamur.Hehaspublishedinjournals,such profitandnon-profitorganizationsinapplyingtheaforementionedmethods
as European Journal of Operational Research, toreal-lifebusinesscases.
Machine Learning, and Decision Sciences. His
research interests include the applications of
descriptive, predictive, and prescriptive analytics in social media, CRM,
sports,andproductionandmanufacturing.
VOLUME13,2025 204103