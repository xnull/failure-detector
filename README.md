# Failure-detector

#### Problem:
The Failure Detector mechanism is responsible for the detection of node failures or crashes, 
the previous version struggles to detect failures accurately, also sometimes it made incorrect decisions that make a node in the cluster unresponsive when the node actually healthy.

#### Motivation
CorfuDb is the main database for one of the major VMware projects. 
Partition tolerance one of the most critical components in the database and the whole project depends on it, a buggy failure detector made the whole system unstable.

#### Solution
Redesig and refactor the most critical parts of it, implement a "decision-maker" protocol and a "cluster state graph" mechanism.

#### Result
The new version of the Failure Detector make the entire project more stable and reliable and saved a lot of engineering hours and money, also it was a critical component for the first major release of the project to make the project Generally Available


### Details
 - [Failure Detector Mechanism](https://github.com/CorfuDB/CorfuDB/blob/f75d756b830ecdfad196f29025f1c012a0eee09e/infrastructure/src/main/java/org/corfudb/infrastructure/RemoteMonitoringService.java#L328) - correctWrongEpochs, empty slot, failure detection, healing, state transfer
 
 - [ClusterAdvisor](https://github.com/CorfuDB/CorfuDB/blob/f75d756b830ecdfad196f29025f1c012a0eee09e/infrastructure/src/main/java/org/corfudb/infrastructure/management/CompleteGraphAdvisor.java#L55) decision maker on top of succesful connection
 
 - [ClusterGraph](https://github.com/CorfuDB/CorfuDB/blob/f75d756b830ecdfad196f29025f1c012a0eee09e/infrastructure/src/main/java/org/corfudb/infrastructure/management/failuredetector/ClusterGraph.java#L98) NodeStates, collection states from the cluster.
 
 - [ClusterGraphTest](https://github.com/CorfuDB/CorfuDB/blob/f75d756b830ecdfad196f29025f1c012a0eee09e/infrastructure/src/test/java/org/corfudb/infrastructure/management/ClusterGraphTest.java#L28) and [ClusterGraphAdvisorTest](https://github.com/CorfuDB/CorfuDB/blob/f75d756b830ecdfad196f29025f1c012a0eee09e/infrastructure/src/test/java/org/corfudb/infrastructure/management/CompleteGraphAdvisorTest.java#L22) ability to emulate entire an cluster state.
 
 - [Universe Framework, Integration Testing](https://github.com/CorfuDB/CorfuDB/blob/785f8ba21792fbaf816de60e90df0996ea2de1f1/it/src/test/java/org/corfudb/universe/scenario/OneNodeDownIT.java#L39) to test the whole functionality
