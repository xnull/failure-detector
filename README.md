# Failure-detector

Deep dive topic will be about implementing and redesign a Failure Detector in CorfuDb.

#### Problem:
The Failure Detector mechanism is responsible for the detection of node failures or crashes, 
the previous version struggles to detect failures accurately, also sometimes it made incorrect decisions that make a node in the cluster unresponsive when the node actually healthy.

#### Motivation
CorfuDb is the main database for one of the major VMware projects. 
Partition tolerance one of the most critical components in the database and the whole project depends on it, a buggy failure detector made the whole system unstable.

#### Solution
To make failure detection accurate and stable I have redesigned and refactored the most critical parts of it, I have introduced a "decision-maker" protocol and implemented a "cluster state graph" mechanism.

#### Result
The new version of the Failure Detector make the entire project more stable and reliable and saved a lot of engineering hours and money, also it was a critical component for the first major release of the project to make the project Generally Available
