# Intrusion Detection System
This project can **identify network attacts** with the help of packet data flow patterns on the network. Currently it is a binary **Classification Supervised learning** project that'll deal with detecting only DoS attacks, but I'll be more than happy to expand this project to larger domain scale than current if time permits.

## [Problem Statement](Problem-Statement.txt)
**Intrusion Detection Systems** (IDSs) and **Intrusion Prevention Systems** (IPSs) are the most important **defense tools** against the sophisticated and ever-growing network attacks. Given a **Network flow data**, can we detect different network attacks?

<img src='Graphics/IDS.png'/>

### About Data
[Data Here](https://drive.google.com/drive/folders/1jME_jU3uq_wwKvdBoN7Eao6Ks8rq_PJC?usp=sharing)    
There are different types of network attacks such as Brute Force FTP, Brute Force SSH, DoS, Heartbleed, Web Attack, Infiltration, Botnet and DDoS. But, in this data set we have only provided **DoS attack**.
- Data is in **csv** format, training samples: 519519 , features: 79 which contains ID, Label, Packet Info Features, Session Info Features.
- It is quite **Imbalanced Dataset**.
<img src='Graphics/Unbalanced-Data.png' width=150/>

### Evaluation Metric
In context to this problem, I think **Recall** must be the considerable metric to be used because we do not want any **False Negatives** i.e., to predict it's not an attack when it is actually an attack. Because, if it's an attack, the system will most probably shut down if Server Side Precautions are not implemented.

<img src='Graphics/Confusion-Matrix.png' width=250/>

### Data Analysis Insights with understanding
- Data has **missing values** as well as **infinity values**, that represents a DoS attack.
- There are mostly **Contineous Features** as well as some **Categorial Nominal Features**(flags).
<img src='Graphics/Eda.gif'/>
   
#### Techniques 
- **SMOTE** for Data Sampling.
- **Feature Selection** using sklean.feature_selection.mutual_info_classif() of 30 features from 79 features with little to no variation in evaluation metric and then using **Corelation Matrix** to reduce to 19 features removing **Multicolinearity**.


### Different Approaches Used
- [X] Approach 1: XGBoost

[Approach 1](Notebooks/ids.ipynb)

## Output
[Submission File Here][submission_file.csv]
|ID | Classification|
|---|---------------|
|0	|	BENIGN|
|1	|	DoS|
|2	|	BENIGN|
|3  |	DoS|
|4  |	DoS|
|.  |...|
|.  |...|
|.  |...|


## Conclusion
Yes, we can indeed detect different Network Attacks using patterns in Data Packet Flows in Network.


### Business Understanding
**DoS**: Flooding the targeted machine or resource with superfluous requests in an attempt to overload systems and prevent some or all legitimate requests from being fulfilled.
**Some DoS Techniques**:
- Holds the connection open by sending valid, incomplete HTTP requests to the server at regular intervals to keep the sockets from closing.
- By repeatedly sending initial connection request (SYN) packets(Getting ACK packet from server and not sending back 3rd handshake ACK packet while the server waits at that port forever), the attacker is able to overwhelm all available ports on a targeted server machine. [Read More Here](https://www.cloudflare.com/learning/ddos/syn-flood-ddos-attack/)
- a time delay between successive attacking packets.
- HTTP slow POST DoS attack: sends large content length header and sends content very slow speed.- the attacker sends traffic consisting of complicated requests to the system.

###### Interview Project by/for [Quadratyx](https://quadratyx.com)
