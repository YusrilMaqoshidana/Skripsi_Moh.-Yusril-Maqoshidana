2023 2nd International Conference on Futuristic Technologies (INCOFT)
Karnataka, India. Nov 24-26, 2023
Whatsapp Chat Analyzer using Machine learning
and Natural Language processing.
|     |     | R.Prakash Kumar               |     |     |     |     |     |     | Dr.Manja Naik.N,  |             |     |     |     |
| --- | --- | ----------------------------- | --- | --- | --- | --- | --- | --- | ----------------- | ----------- | --- | --- | --- |
|     |     | Senior Assistant Professor,   |     |     |     |     |     |     |                   | Professor,  |     |     |     |
ECE Department, CVR College of Engineering,  E&CE Department,
Mangalpalli,Hyderabd-501510.  University B.D.T College of Engineering VTU,
|     |     | Research Scholar,  |     |     |     |     |     |                               | Davangere, Karnataka.   |     |     |     |     |
| --- | --- | ------------------ | --- | --- | --- | --- | --- | ----------------------------- | ----------------------- | --- | --- | --- | --- |
|     |     | Department E&CE,   |     |     |     |     |     | Email:manjubdt2009@gmail.com  |                         |     |     |     |     |
University B.D.T College of Engineering,
VTU, Davangere , Karnataka
Email:prakah.rachmagdu@gmail.com
Abstarct—  The  most  popular  and  effective  form  of  methods are generally categorized as either human based or
electronic communication now in use is WhatsApp. There are  automated. There are various methods to analyze emotions
many different types of conversations that take place among  such as keyword processing, manual processing, and Natural
36352401.3202.35706TFOCNI/9011.01 :IOD | EEEI 3202© 00.13$/32/6-4880-3053-8-979 | )TFOCNI( seigolonhceT citsirutuF no ecnerefnoC lanoitanretnI dn2 3202
groups of individuals in WhatsApp chats. This data can offer a  Language  Processing.  Here  we  are  using  text  mining
wealth  of  information  for  cutting-edge  technologies  like  techniques for EDA. Emotion detection on given text data is
machine learning. Users have a platform to analyze WhatsApp  the  objective  of  the  project.  Detecting  human  emotions
conversations through WhatsApp chat analyzer. The input for
|                |     |                 |     |              |             |            | accurately    | and  | effortlessly,  | without        |     | requiring  | direct  |
| -------------- | --- | --------------- | --- | ------------ | ----------- | ---------- | ------------- | ---- | -------------- | -------------- | --- | ---------- | ------- |
| the  WhatsApp  |     | chat  analyzer  |     | is  a  text  | file  that  | has  been  |               |      |                |                |     |            |         |
|                |     |                 |     |              |             |            | questioning,  |      | is  crucial.   | Additionally,  |     | gaining    | an      |
exported from WhatsApp. The main goals of this essay are to
understanding of how the proposed LSTM model operates,
identify emotions, present various concepts, visualizations, and
including the functioning of its intermediate layers, is also a
analyze discussions. It provides a detailed examination of the
|     |     |     |     |     |     |     | key  objective.  |     | Data-set  sentences  |     | and  their  | emotions  | are  |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | -------------------- | --- | ----------- | --------- | ---- |
total number of messages, each user's activity, the overall
volume of words, the monthly timeline, the busiest day, and a  essential for identifying emotion in text. Joy, surprise, anger,
|          |            |              |     |            |           |          | sadness,  | happy  | etc  based  | sentence  | or  | negations  | in  the  |
| -------- | ---------- | ------------ | --- | ---------- | --------- | -------- | --------- | ------ | ----------- | --------- | --- | ---------- | -------- |
| variety  | of  other  | statistics.  |     | Also,  it  | provides  | graphic  |           |        |             |           |     |            |          |
sentence make the emotion detection very challenging. The
representations of weekly activity and the busiest users, and we
|     |     |     |     |     |     |     | LSTM  | network  | with  analysis  |     | of  emotion,  |     | knowledge  |
| --- | --- | --- | --- | --- | --- | --- | ----- | -------- | --------------- | --- | ------------- | --- | ---------- |
may exploit these results.
|     |     |     |     |     |     |     | obtained  | during  | emotion  | detection  |     | research  | is  the  |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------- | -------- | ---------- | --- | --------- | -------- |
groundwork. In LSTM, different layers need to be employed
Keywords— WhatsApp, Machine Learning, WhatsApp chat
analyzer, Visualizations, Emotions component.  to understand how the proposed model works and responds
to the given text data.
|     |     | I.  | INTRODUCTION  |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
WhatsApp conversation analyzer's primary objective is to
| WhatsApp  | is  | a  popular  | instant  | messaging  |     | application  |     |     |     |     |     |     |     |
| --------- | --- | ----------- | -------- | ---------- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
identify human emotions. Finding out a person's feelings can
used by millions of people worldwide. With the increasing
help you understand them better, which can help you comfort
volume of conversations, there is a need for effective ways to
them when they're unhappy or in many other situations. The
| analyze  | and  extract  |     | meaningful  | insights  |     | from  these  |     |     |     |     |     |     |     |
| -------- | ------------- | --- | ----------- | --------- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
WhatsApp conversation analyzer's other feature is a visual
messages. Machine learning and natural language processing
|     |     |     |     |     |     |     | representation  |     | of  user  activity.  |     | Visualization  |     | provides  a  |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | -------------------- | --- | -------------- | --- | ------------ |
techniques can be used to develop an intelligent WhatsApp
visual depiction of the total number of messages sent, the
| chat  analyzer  | that  | can  | automatically  |     | identify  | emotions,  |     |     |     |     |     |     |     |
| --------------- | ----- | ---- | -------------- | --- | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
busiest user, and the number of messages sent by each user,
extract useful information, and present them in an easy-to-
busiest time.
understand format The WhatsApp chat analyzer can provide
insights into user behavior, such as the number of messages  The structure that follows describes how the paper is
sent by each user, the most active users, and the busiest  structured:  Section  II  examines  the  relevant  literature.
|     |     |     |     |     |     |     | Section  | III  describes  | the  | suggested  | procedure,  |     | while              |
| --- | --- | --- | --- | --- | --- | --- | -------- | --------------- | ---- | ---------- | ----------- | --- | ------------------ |
periods. It can also identify the most common words and
phrases used in the chat and analyze the sentiment of each  Section IV displays the outcomes. Section V serves as the
message to determine the overall mood of the conversation.  paper's conclusion.
| This  can  | be  | particularly  |     | useful  for  | businesses  | and  |     |     |     |     |     |     |     |
| ---------- | --- | ------------- | --- | ------------ | ----------- | ---- | --- | --- | --- | --- | --- | --- | --- |
organizations that need to monitor customer feedback or  II. RELATED WORKS USE
| track  employee  |     | communications.  |     | By  | leveraging  | machine  |     |     |     |     |     |     |     |
| ---------------- | --- | ---------------- | --- | --- | ----------- | -------- | --- | --- | --- | --- | --- | --- | --- |
Numerous studies and analyses have been done on the
learning  and  natural  language  processing  techniques,  the  use of WhatsApp and its effects, including one by Ravi
WhatsApp chat analyzer can provide a powerful tool for  Shankara et al. [1] that included a demo survey analysis.
analyzing large volumes of messages quickly and efficiently.  Some  studies  examined  WhatsApp's  effects  on  students,
It can save time and resources while providing valuable  while others examined its effects on the local community at
| insights  | that  can  | inform  | decision-making  |     | and  | improve  |     |     |     |     |     |     |     |
| --------- | ---------- | ------- | ---------------- | --- | ---- | -------- | --- | --- | --- | --- | --- | --- | --- |
large. For instance, a research was done in the southern
communication.  region of India on people between the ages of 18 and 23 to
|     |     |     |     |     |     |     | find  out  | how  | important  | WhatsApp  | is  to  | young  | people.  |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ---- | ---------- | --------- | ------- | ------ | -------- |
Exploratory data analysis aims to examine data using
According to the report, students were online for roughly 16
visual techniques, while emotion detection seeks to predict
hours daily and used WhatsApp for eight hours every day.
| an  individual's  |     | mood  | or  perspective  |     | by  analyzing  | their  |     |     |     |     |     |     |     |
| ----------------- | --- | ----- | ---------------- | --- | -------------- | ------ | --- | --- | --- | --- | --- | --- | --- |
language  in  relation  to  a  particular  topic,  sentence,  or  All respondents said that they exchanged photographs, audio
files, and video files with their pals via WhatsApp. It was
| paragraph.  | Various  | methods  |     | can  be  | used  to  | analyze  the  |     |     |     |     |     |     |     |
| ----------- | -------- | -------- | --- | -------- | --------- | ------------- | --- | --- | --- | --- | --- | --- | --- |
also discovered.
emotion in text whether it is happy, sad, anger etc. These
| 979-8-3503-0884-6/23/$31.00 ©2023 IEEE |     |     |     |     |     |     | 1   |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Authorized licensed use limited to: NATIONAL INSTITUTE OF TECHNOLOGY CALICUT. Downloaded on February 23,2024 at 09:32:35 UTC from IEEE Xplore.  Restrictions apply.

In order to statistically analyse WhatsApp conversations, The above architectural diagram is used to perform EDA
Sunil Joshi [2] proposed categorising and analysing chats on the chat data and to analyze the emotion from any text.
based on a variety of criteria. The investigation used a Pre-processing of the dataset is done. For Exploratory data
dataset from a WhatsApp group discussion with 55,563 analysis, a WhatsApp group chat has been considered as a
entries that covered the period from May 2019 to May 2020. benchmark and for emotion detection a dataset with 4
The dataset included factors that indicated how frequently a different emotions has been taken. Emotion detection model
certain user of WhatsApp chat groups interacted with others, was being implemented using LSTM network architecture.
including years of usage, daily usage length, response rates,
A. Process Flow-
and the kind of messages each member of the group
submitted (smiley, text, various). The primary parameters 1. Data Collection
used in this research were the type of message being sent, its
2. Pre-processing
duration over the course of a year, month, week, day, or
hour, its timestamp (AM/PM), the age range of the senders, 3. Exploratory Data Analysis
and its sender gender (male or female). RStudio, used to do
4. Fast text Word Vector Model
exploratory data analysis and visualisation for the acquired
data. 5. LSTM
Subarno Pal et al.'s study [3] suggested analysing the B. Data Collection
possibility of more accurate modelling of temporal
For Exploratory Data Analysis, any WhatsApp exported
sequences and their long-range relationships. Long Short-
chat can be considered as a dataset. By default, WhatsApp
Term Memory (LSTM), a particular kind of recurrent neural
exports all the chats in the form of text file. All the exported
network (RNN) architecture, was used to do this. Users'
chats have a fixed pattern [Timestamp-Username-Messages]
opinions and attitudes towards confident things or
as a sequential string, so here regular expressions have been
occurrences were conveyed in text that the researchers
used for extracting information from it. There are two
gathered from a variety of sources, including blogs and user
different options whether to include media and whether to
reviews. They piled several LSTM layers on top of one
not. In case media are included then file size will be
another to increase the accuracy of their analysis.
increased hence it is preferred to export the chats without
In their study, Huang Zou [5] proposed the use of a using media files. Once chats will be exported then it is
directional LSTM layer that could transfer and deliver data uploaded as raw dataset. The chat in WhatsApp application
both forward and backward in the network. To achieve this, can be exported by following:- Launch WhatsApp on the
they split the neurons of a regular LSTM into two directions: phone. Then open the individual or group chat. After that tap
one for positive time direction forward states and another for on More options or three dots. Click More and then tap on
negative time direction backward states. The outputs were Export chat. At last select export without media.
not connected to inputs of the opposite direction states. They
C. Pre-processing
found that a layered deep LSTM with bidirectional
connections performed better in terms of accuracy compared Once exported chat is loaded to the application then the
to simpler versions of LSTM. As the complexity of the very first requirement is to extract all the information like
network increased, validation accuracy increased, and Date, Time, Day, User, Message, URL etc. Then after Date
validation loss dropped. However, an increase in the related manipulations and cleaning process on messages by
complexity of the layers also increased the computational removing stop-words and punctuations are being followed.
cost of the network. The performance of conventional Following are six major sub-modules under Pre-Processing:
LSTM, deep LSTM, and bidirectional deep LSTM was
1. Splitting Fields
evaluated based on evaluation metrics such as validation loss
and validation accuracy. 2. Data frame creation
3. Date format conversion
III. PROPOSED METHOD
WhatsApp conversation analyzer's primary objective is to 4. Time format conversion (24 hour)
identify human emotions. Finding out a person's feelings can
5. Feature addition
help you understand them better, which can help you comfort
them when they're unhappy or in many other situations. The 6. Cleaning
WhatsApp conversation analyzer's other feature is a visual
D. Exploratory data analysis
representation of user activity. Visualization provides a
visual depiction of the total number of messages sent, the This module is mainly used for visualization and
busiest user, and the number of messages sent by each user, observation. Here we have used bar graph, line chart, pie
busiest time. chart etc. on the basis of count, most engagement etc. This
module has various sub-modules like fetch stats, timeline,
top users and message length, word cloud.
E. Fast text Word Vector Model
Word embedding techniques were considered as an
important factor in sentiment evaluation. In this project, fast-
Text word embedding technique is used. Fast-Text is a word
embedding method that is an extension of the word2vec
model. Instead of using words to build word embedding,
Fast-Text goes one level deeper. This deeper level consists of
Fig.1. Proposed model.
2
Authorized licensed use limited to: NATIONAL INSTITUTE OF TECHNOLOGY CALICUT. Downloaded on February 23,2024 at 09:32:35 UTC from IEEE Xplore. Restrictions apply.

parts of words and characters. For example, the word, I pay attention as the panic intensifies into a sense of
“artificial” with n=3, the fast-Text representation of this being overtaken and powerless.
word is (cid:1766)ar,art,rti,ti f,i f i, f ic,ici,ial,al(cid:1767), where the angular
I don't even have to disguise myself with this set of
brackets indicate the beginning and end of the word. There
individuals since I feel so at ease, happy.
are two main advantages to this approach. First,
generalization is possible as long as new words have the I find myself in the peculiar situation of loving and
same characters as known ones. Second, less training data is supporting others.
needed since more information can be extracted from each
Just like Katniss, I was experiencing the same level of
piece of text.
sadness.
F. LSTM
With my pessimism, unhappiness, and melancholy, I
Long Short-Term Memory (LSTM) networks are a
feel like my only function right now is to tear the wind out of
modified version of recurrent neural networks, which makes
your sails.
it easier to remember past data in memory. The vanishing
gradient problem of RNN is resolved here. LSTM is well- I believe that when we argue, we do it out of a need for
suited to classify, process and predict time series given time attention and to spread our wrath to the world.
lags of unknown duration. It trains the model by using
The colours red and purple seem to me to be very rich
backpropagation. The heart of a LSTM network is the cell
and joyful.
state which provides a bit of memory to the LSTM so it can
remember the past. Gates in LSTM are the sigmoid 2) Training
activation functions i.e they output a value between 0 or 1 Five data sets are preprocessed in this step and given to
and in most of the cases it is either 0 or 1. In an LSTM the LSTM for training. LSTM stands for Long short-term
network, three gates are present. memory networks, used in the field of deep learning. It is a
variety of recurrent neural networks that are capable of
IV. EXPERIMENTAL RESULTS learning long-term dependencies, especially in sequence
prediction problems.
A. EMOTION DETECTION:
1) Data Set
The module has been tested using the following dataset.
I'm not feeling very ambitious right now because I feel so
lousy; melancholy.
I'm updating my blog because I'm depressed.
Because I never want her to feel as though I'm ashamed
of her or sad with her, I never force her to be apart from me.
I felt a bit more upbeat as I left with my bouquet of red
and yellow tulips than when I had come. Joy I was feeling a
little vain when I did this one. Sadness
There is nowhere I can enter a store without feeling
uneasy or afraid.
Despite the excitement I should have been experiencing
after being accepted into the master's programme at the
University of Virginia, fear felt anger at the end of a phone
Fig.2. Block diagram of training the Data set
call; anger I explain why I clung to a relationship with a boy
who was, in many ways, immature and uncommitted; joy I
The switch in the previous image denotes that the LSTM
like to have the same breathless feeling as a reader eager to
received all five users' data for prediction. Either one of the
see what will happen next; joy
four emotions—anger, fear, sadness, or happiness—will be
I simply feel angry, weary, and premenstrual, which I the result of the forecast.
definitely am, but it's just been a week and I'm not much
3) Validation
fitter than a walrus on summer vacation.
Model accuracy determines the model performance, and
I don't feel especially anxious or afraid. it evaluates the prediction accuracy. The number of accurate
predictions divided by the total number of predictions across
I simply feel angry, weary, and premenstrual, which I
all classes is the value of accurate classifications that a
definitely am, but it's just been a week and I'm not much
trained machine learning model achieves. Depending on the
fitter than a walrus on summer vacation.
scale used, it is given as a value between [0,1] or [0,100]. If
I don't feel especially anxious or afraid. the classifier's accuracy is 0, it consistently guesses the
incorrect label; if it's 1, or 100, it consistently predicts the
Sadness at the fact that these ladies, of whom I knew just right label.
a small number, were supporting my baby and I while we
travelled.
3
Authorized licensed use limited to: NATIONAL INSTITUTE OF TECHNOLOGY CALICUT. Downloaded on February 23,2024 at 09:32:35 UTC from IEEE Xplore. Restrictions apply.

| TABLE I. | TABLETYPE STYLES | B. Visualization  |        |                     |     |     |
| -------- | ---------------- | ----------------- | ------ | ------------------- | --- | --- |
|          |                  |                   | Fig.5. | Pre-processed data  |     |     |
Real world chat conversations contain lot of shortcut
|     |     | words,       | missing  values,  | blank  | spaces,                  | and  multiple |
| --- | --- | ------------ | ----------------- | ------ | ------------------------ | ------------- |
|     |     | punctuation  | which  are        | not    | useful  in  exploration  | and           |
visualization. Pre-processing needs to be performed to clean
the dataset and extract and separate from the data.
Fig.3. .Traing and Testing data  Accuracy
|     |     |      | Fig.6.         | Message count  |                 |             |
| --- | --- | ---- | -------------- | -------------- | --------------- | ----------- |
|     |     | The  | above  figure  | 6  shows       | message  count  | and  date,  |
ascending order of message count from the given chat.
| Fig.4. | . Model Accuracy  |     |        |                    |     |     |
| ------ | ----------------- | --- | ------ | ------------------ | --- | --- |
|        |                   |     | Fig.7. | Day wise messages  |     |     |
In order to recognize an emotion, a set of words is taught
for that emotion. For instance, certain words that have been
trained to recognize happy emotion may be mixed in with
Day wise message activity throughout the year has been
ones that have been trained to recognize sad emotion. Here,
displayed andhigher raised line states that most conversation
the probability of making an incorrect forecast is determined
occur in chats in a that day.
by the loss function. The loss is zero if the model's forecast is
accurate. Otherwise, the loss will grow in proportion to the
cost of making incorrect predictions.
4
Authorized licensed use limited to: NATIONAL INSTITUTE OF TECHNOLOGY CALICUT. Downloaded on February 23,2024 at 09:32:35 UTC from IEEE Xplore.  Restrictions apply.

Based on the graph provided in Fig-11, it can be inferred
that the number of messages sent is highest on Sundays and
in the month of September, while the lowest number of
messages is observed on Mondays and in the month of
January.
Fig.8. . Final data frame
Fig.12.Word cloud from group chat
Word Cloud is a powerful visual representation object for
Fig.9. Total messages sent and average message lengths
text processing, which shows the most frequent word with
The top 10 members with most sent messages have been bigger and bolder letters, and with different colors. The
displayed in Fig-9 and average word length has been smaller the the size of the word the lesser it’s important.
displayed here to detect who sends long message normally. Figure states the most used words which have been filtered
Here matplotlib bar chart and line chart have been used for after removing punctuation and stop words. From above it
visualization. can be understood that visualization gives us information
about various factors such as message count and the date the
message is sent, messages per day over a period of time,
busiest days, number of messages sent by users, most active
hours and users who shared the media most frequently.
V. CONCLUSION
This Paper states that exploratory data analysis or EDA is
a gateway to the unexplored field of WhatsApp Chats. It
allows the analysis of bilingual users. It was able to use the
Python programming language and its libraries, to create an
analysis of a WhatsApp group chat and visually represent the
top 10 and top 20 users in the chat group, analyze the emojis
and most active day/month/year etc. At the end of the work
Fig.10..Most active user
the expected results were obtained and the analysis was able
to show the level of participation of all individuals on the
Fig-10 shows most active hours by users in 24-hour
given WhatsApp group.
format. We can conclude that 22nd hour and 23th hour are
the most active hours in a day while 5th and 6th hour are the Emotion Detection using the LSTM model needed
least active hours. several intermediate layers for passing memory to get the
desired output. In this project seven intermediate layers are
used to make the sequential model and to predict the emotion
in 4 different categories [’sadness’,’anger’,’joy’,’fear’].
Dataset of 16000 records has been used but most of the
records have either joy or sadness
REFERENCES
[1] IS Srajan, K Ravishankara, and Vaisakh Dhanush. WhatsApp chat
analyzer. International Journal of Engineering Research &
Technology, 9(5):897–900, 2020.
Fig.11.Total messages sent [2] Sunil Joshi. Sentiment analysis on WhatsApp group chat using r.
Data, Engineering and Applications, pages 47–55, 2019.
5
Authorized licensed use limited to: NATIONAL INSTITUTE OF TECHNOLOGY CALICUT. Downloaded on February 23,2024 at 09:32:35 UTC from IEEE Xplore. Restrictions apply.

[3] Subarno Pal, Soumadip Ghosh, and Amitava Nag. Sentiment analysis [7] G RajKumar, P Brundha, and V Selina Annie Retna. People’s
in the light of LSTM recurrent neural networks. International Journal behavior analysis in chat messages using natural language processing.
of Synthetic Emotions (IJSE), 9(1):33–39, 2018. pages 1128–1133, 2021.
[4] Huang Zou, Xinhua Tang, Bin Xie, and Bing Liu. Sentiment [8] Astha Mohta, Atishay Jain, and Sonika Dahiya. Text classification
classification using machine learning techniques with syntax features. based behavioral analysis of whatsapp chats. pages 717–724, 2020.
pages 175–179, 2015. [9] Blessing Nwamaka Iduh WhatsApp network group chat analysis
[5] Alec Yenter and Abhishek Verma. Deep cnn-lstm with combined using python programming. International Journal of Education, pages
kernels from multiple branches for IMDB review sentiment analysis. 124–126, 2018.
pages 540–546, 2017. [10] J Andjelic. WhatsApp statistics: Revenue, usage, and history.
[6] Chinthapanti Bharath Sai Reddy, G Gopichand, Kumar MV Rakesh, Fortunely, pages 101– 103, 2019.
O Nikhil Kumar, and S Kowshik. Analyzing and predicting the [11] George Dominic Ewur and Johnson Yeboah. The impact of
emotion of WhatsApp chats using sentiment analysis. TEST WhatsApp messenger usage on students' performance in tertiary
Engineering & Management, 83:15454–15461, 2020. institutions in Ghana. Journal of Education and practice, 5(6):157–
164, 2014.
6
Authorized licensed use limited to: NATIONAL INSTITUTE OF TECHNOLOGY CALICUT. Downloaded on February 23,2024 at 09:32:35 UTC from IEEE Xplore. Restrictions apply.