# N-BaIoT: Data for Network-Based Detection of IoT Botnet Attacks

This dataset addresses the critical lack of public botnet datasets, especially for the Internet of Things (IoT). It enables empirical evaluation with **real traffic data**, gathered from nine commercial IoT devices infected by authentic **Mirai** and **BASHLITE** botnets in an isolated network.

---

## 1. Source and Attribution

### Creators and Affiliations
* **Yair Meidan, Michael Bohadana, Yael Mathov, Yisroel Mirsky, Asaf Shabtai:** Department of Software and Information Systems Engineering, Ben-Gurion University of the Negev, Beer-Sheva, Israel.
* **Dominik Breitenbacher, Yuval Elovici:** iTrust Centre of Cybersecurity at Singapore University of Technology and Design, Singapore.
* **Donor:** Yair Meidan (yairme@bgu.ac.il)
* **Date:** March, 2018

### Required Citations

Please cite the following papers if you use this dataset:

1.  **Article where the dataset was initially described and used:**
    > Y. Meidan, M. Bohadana, Y. Mathov, Y. Mirsky, D. Breitenbacher, A. Shabtai, and Y. Elovici. "N-BaIoT: Network-based Detection of IoT Botnet Attacks Using Deep Autoencoders", *IEEE Pervasive Computing, Special Issue - Securing the IoT* (July/Sep 2018).

2.  **Article describing the feature extractor (from *.pcap to *.csv):**
    > Y. Mirsky, T. Doitshman, Y. Elovici & A. Shabtai. "Kitsune: An Ensemble of Autoencoders for Online Network Intrusion Detection", in *Network and Distributed System Security (NDSS) Symposium*, San Diego, CA, USA (2018).

---

## 2. Dataset Structure and Attributes

The traffic data was captured from nine different IoT devices and processed into CSV files.

| Statistic | Value |
| :--- | :--- |
| **Number of Instances** | Varies for every device and attack type. |
| **Number of Attributes** | **115** independent features + **1** class label. |
| **Prediction Attribute** | Distinguishing between **benign** and **Malicious** traffic. |
| **Classification Use** | Multi-class classification: **10 classes of attacks** plus **1 class of "benign"**. |

### Feature Information

The dataset includes 115 features derived from different statistical aggregations over time, calculated using the feature extractor described in the Kitsune paper.

#### 2.1. Stream Aggregation Headers

These define the scope of the network traffic being summarized:

| Header | Corresponding Concept | Description |
| :--- | :--- | :--- |
| **H** | Source IP | Stats summarizing the recent traffic from this packet's host (IP). |
| **MI** | Source MAC-IP | Stats summarizing the recent traffic from this packet's host (IP + MAC). |
| **HH** | Channel | Stats summarizing the recent traffic going from this packet's host (IP) to the destination host. |
| **HH\_jit** | Channel Jitter | Stats summarizing the jitter of the traffic going from this packet's host (IP) to the destination host. |
| **HpHp** | Socket | Stats summarizing the recent traffic going from this packet's host+port (IP) to the destination host+port. (e.g., `192.168.4.2:1242 -> 192.168.4.12:80`). |

#### 2.2. Time-Frame (Decay Factor $\lambda$)

The time-frame indicates how much recent history of the stream is captured in the statistics. It corresponds to the decay factor $\lambda$ used in the damped window:

* **L5, L3, L1, L0.1, L0.01**

#### 2.3. Extracted Statistics

These statistics are calculated for each combination of Stream Aggregation and Time-Frame:

* `weight`: The weight of the stream (can be viewed as the number of items observed in recent history).
* `mean`
* `std`
* `radius`: The root squared sum of the two streams' variances.
* `magnitude`: The root squared sum of the two streams' means.
* `cov`: An approximated covariance between two streams.
* `pcc`: An approximated correlation coefficient between two streams.

### Class Label

The class label should be derived from the respective filename (e.g., `"benign"` or `"TCP attack"`).

---

## 4. Relevant Information

This dataset is significant because it provides realistic, empirical data for examining two of the most common IoT-based botnets, Mirai and BASHLITE. Prior experimental studies often relied on emulated or simulated traffic, which this dataset aims to overcome by using data gathered from **real, commercial IoT devices**.
