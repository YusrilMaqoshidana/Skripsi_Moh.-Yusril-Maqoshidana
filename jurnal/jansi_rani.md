2022 3rd International Conference for Emerging Technology (INCET)
Belgaum, India. May 27-29, 2022

Whatsapp Sentiment Analysis Using R

S.Jansi Rani
AP/IT,
 Sri Ramakrishna Engineering College,
Coimbatore-22
Corresponding Author:
jansi.sankar@srec.ac.in,
jansiranis89@gmail.com

T.N.Prabhu
AP/IT,
 Sri Ramakrishna Engineering College,
Coimbatore-22

J.Angel Ida Chellam
AP/IT,
 Sri Ramakrishna Engineering College,
Coimbatore-22

Abstract: In  today’s  internet  era,  there  are  many  chat
application are used for conversions like whatsapp. Every smart
phone user uses the Whatsapp application for private and group
messaging, as well as video calling. Users join a variety of desired
and  undesirable  WhatsApp  groups,  resulting  in  confusion,  low
storage  capacity,  and  unmonitored  issues.  Sentiment  analysis  is
progressively  driving  the  design  and  delivery  of  more  products
and services that match customers' demands, from mining tweets
to  Facebook  postings  to  scraping  online  reviews.  It  is  somewhat
easier to do nowadays, because of improved packages in popular
programming languages. In this paper on Sentimental analysis of
whatsapp  data  done  by  using  R.  This  brings  nature  of  the
whatsapp  group  whether  the  conversion  is  positive  or  negative.
Based  on  the  result users  can  deliberate  on  those  whatsapp
group.

Keywords: Sentimental Analysis, R, Whatsapp data

I.

INTRODUCTION

In the internet world, everything is simple and quick. There
are  many  chat  applications  available  for  messaging  and  chat.
One  such  free  application  is  whatsapp.  WhatsApp  appears  to
be  gaining  in  popularity  as  a  conversation  application  as  well
as  a  messaging  service[1].  WhatsApp  is  the  world's  most
popular  social  media  app.  The  amount  of  messages  delivered
on  a  daily  basis  is  increasing  as  the  user  base  grows.  [2]
WhatsApp  is  an  excellent  data  source  for  analysing  a  wide
range of patterns and correlations between two or more people
conversing privately or in teams. Thus, the large amount of the
chat data can be visualized using sentimental analysis and text
analysis.[3] "It  provides  an  evaluation  of  how  "positive"  or
"negative" a piece of text is," according to sentiment analysis,
also known as subjectivity analysis or opinion mining.[4] One
key  notion  pertinent  to  this  work  as  a  starting  assumption  is
sentiment  visualisation,  which  visually  depicts  the  sentiment
analysis results.

The paper's aim is divided into three parts:

(1)  Getting the Chat Data from WhatsApp

(2) Sentimental analysis of chat data using R

(3) Create Word Cloud

The paper has organized as follows:

Section2  describes  the  literature  survey  on  Sentimental
analysis.  Section3  tells  how  to  get  data  from  WhatsApp.
Section 4 describes R Process with visualization.

The  purpose  of  this  study  is  to  utilise  R  to  estimate  chat

sentiment and provide useful information to users.

II.

LITERATURE REVIEW

Types of Data:

Big  Data  [5]  is  defined  as  a  large  volume,  high  velocity,
and  diverse  set  of  data.  Structured  data,  semi-structured  data,
and unstructured data are the three types.

Structured  Data:  For  effective  analysis,  structured  data
has  elements  that  can  be  handled.  It's  been  organised  into  a
database, which is a standardised repository. It refers to all data
that can be stored in a SQL database as a table with rows and
columns. They have relational keys and are simple to map into
pre-designed  fields.  Those  data  are  presently  the  most
commonly processed in the development and easiest approach
to managing information. One example is relational data.

Semi-  Structured  Data:  Semi-structured  data  is  data  that
is  not  stored  in  a  relational  database  but  has  organisational
qualities that make it easier to examine. Some processes can be
stored  in  a  relation  database  (though  this  may  be  difficult  for
semi-structured  data),  but  semi-structured  data  exists  to  save
space.  E-mail,  XML  and  other  markup  language  are  an
example.

Unstructured  Data:  Unstructured  data  is  data  that  isn't
arranged  in  a  preset  way  or  doesn't  have  an  established  data
model,  making  it  unsuitable  for  a  traditional  relational
database. So there are other platforms for storing and managing
unstructured data; it is becoming more common in IT systems
and  is  utilised  by  businesses  in  a  number  of  business
intelligence  and  analytics  applications.  Word,  PDF,  Text,  and
Media logs are just a few examples.

Sentiment analysis is done on data taken from Twitter and
Stock  Twits  in  this  study[6].  The  information  is  evaluated  in
order  to  determine  the  mood  of  the  user's  comment.  These
responses  are  divided  into  four  groups:  joyful,  up,  down,  and
rejected. To predict the outcomes, an artificial neural network
is fed the polarity index together with market data.

This  study  employs  Python  and  Tableau  to  do  sentiment
analysis of the text and semantically classify the keywords into
actionable  insights.  Data  was  collected  from  Amazon  website
reviews (n=3,413) of the most popular product (Trigger Point
Grid Foam Roller) in five different colours from 2018 to 2019.

3
0
6
4
2
8
9
.
2
2
0
2
.
1
3
5
4
5
T
E
C
N

I
/
9
0
1
1
.
0
1
:
I

O
D

|

E
E
E
I

2
2
0
2
©
0
0
.
1
3
$
/
2
2
/
1
-
9
9
4
9
-
4
5
6
6
-
1
-
8
7
9

|

)
T
E
C
N

I
(

y
g
o
l
o
n
h
c
e
T
g
n
i
g
r
e
m
E
r
o
f

e
c
n
e
r
e
f
n
o
C

l
a
n
o
i
t
a
n
r
e
t
n
I

d
r
3

2
2
0
2

978-1-6654-9499-1/22/$31.00 ©2022 IEEE

1

Authorized licensed use limited to: Tsinghua University. Downloaded on November 05,2022 at 06:27:30 UTC from IEEE Xplore.  Restrictions apply.

(black, camo, pink, orange, and lime). The black colour has the
most optimistic attitude when compared to the other colours.

Additionally,  SpaCy's  named  entity  recognition  for  the
object  also  detected  clusters  of  people,  places,  and  things,  or
events.

III. COLLECTION OF CHAT DATA FROM WHATSAPP:

To collect the chat data from WhatsApp, the following are

the instructions,

From iPhone WhatsApp:

(cid:120) On your iPhone, open a chat with a person or a group.

(cid:120)

(cid:120)

Simply touch on the person's or group's profile.

There's an option to export chat down below.

From Android WhatsApp:

(cid:120) On your Android, open a chat with a person or a group.

(cid:120)

Toggle between the three dots above.

(cid:120) More information can be found by clicking here.

(cid:120)

Select Export Chat from the drop-down menu.

When  exporting  chat,  notice  an  opportunity  to  connect
media. It is better not to attach media for the sake of simplicity.
Finally,
to  email  address,  and  WhatsApp
conversation will appear in given inbox.

input  chat

Sentimental Analysis Using R:

Step  1:  Install  dplyr  package:  The  dplyr  package  in  the  R
Programming  Language  is  a  data  manipulation  structure  that
provides a consistent collection of verbs for resolving the most
common data manipulation issues.

Step 2:

Load  the  chat  text  data  into  chat  object  which  has  411

observations of 7 varaiables

Fig. 1. Load data

Step 3:

R Lubridate package that makes it easier to work with dates

and times. To visualize the no.of messages per day.

Fig. 2. No. of Messages per day

Step 4:

To get most often used words from chat data.

Fig. 3. Most used words

Step: 5

Use  Syuzhet  packages:  Sentiment  Derived  Plot  and
Sentiment are extracted from text. Text is used to extract plot
arcs.  Extracts  sentiment  and  sentiment-derived  plot  arcs  from
text using a number of sentiment dictionaries that are elegantly
packed for consumption by R users.

Fig. 4. Sentiment with count

Authorized licensed use limited to: Tsinghua University. Downloaded on November 05,2022 at 06:27:30 UTC from IEEE Xplore.  Restrictions apply.

2

Step 6: Visualize the Sentiment

Fig. 5. Visualize the sentiment

Fig. 7. Word frequency

Fig 5 shows the visualization of chat data. From the plot it
shows  that  positive  conversion  in  the  chat  is  high  with  the
value  441.  Also,  disguist  and  other  negative  chat  is  less.  It  is
concluded that, user can retain in the group.

Step 7: Create word cloud

(cid:120)

Build word cloud

Fig. 8. Word Cloud

From the Figure 8, it shows that the word link occurrences

are 147.

IV. CONCLUSION:

Because everyone uses WhatsApp in their day-to-day lives,
the data on it is rising every day. Users can also join numerous
groups, such as known and unknown people. As a result, it is
necessary  to  organize  all  of  the  groups  and  to  leave  the
unwelcomed  ones.  This  paper  explains  how  to  conduct
sentimental  analysis  and  create  a  word  cloud.  The  user  can
choose to stay in the group or leave it based on the results of
the analysis.

REFERENCES:

[1]

[2]

https://medium.com/analytics-vidhya/sentiment-analysis-of-whatsapp-
chat-a906105917f4
https://thecleverprogrammer.com/2021/06/06/whatsap  p-chat-sentiment-
analysis-using-python/

[3] M.,  Wattenberg  and  D.  Fisher.  “Analyzing  Perceptual  Organization  in
Information Graphics,” Information Visualization, vol 3, no.2, PP. 123-
133., 2004, doi: 10.1057/palgrave.ivs.9500070

[4] K. Kucher, C. Paradis and A. Kerren, “The state of the art in sentiment
visualization,” Computer Graphics Forum, vol. 37, no. 1, pp. 71-96, Jun.
2017, doi: 10.1111/cgf.13217.

Fig. 6. Steps for creation of word cloud

(cid:120)

(cid:120)

(cid:120)

Load the data as corpus: docs <-
Corpus(VectorSource(text))

Text transformation using tm_map(), replace all
“/”,”@”,”|” with space

Build term-document matrix

Authorized licensed use limited to: Tsinghua University. Downloaded on November 05,2022 at 06:27:30 UTC from IEEE Xplore.  Restrictions apply.

3

[5]

https://www.geeksforgeeks.org/difference-between-structured-semi-
structured-and-unstructured-data/

[6] Sunil Kumar Khatri , Ayush Srivastava, “Using Sentimental Analysis in
Investment”,  pp.  566-569,  DOI:

Prediction  of  Stock  Market
10.1109/ICRITO.2016.7785019.

[7] Hanan  Alasmari,”  Sentimental  Visualization:  Semantic  Analysis  of
Online  Product  Reviews  Using  Python  and  Tableau”,  Dec-2020,  DOI:
10.1109/BigData50022.2020.9391769
http://www.sthda.com/english/wiki/text-mining-and-word-cloud-
fundamentals-in-r-5-simple-steps-you-should-know

[8]

Authorized licensed use limited to: Tsinghua University. Downloaded on November 05,2022 at 06:27:30 UTC from IEEE Xplore.  Restrictions apply.

4

