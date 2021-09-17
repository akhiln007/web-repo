---
layout: post

title: SingleStore - Architecture
---



{{ page.title }}

================


SingleStore is based on distributed computing. It has three core hardware components, which are Aggregators, Leaf Nodes and Partitions.

![image](https://user-images.githubusercontent.com/8998457/133766368-336c3b0b-4fab-46ef-b8ba-7035618cae1a.png)



1) Nodes:- The client application will send requests to a SQL interpretor and that is routed to an Aggregator and that request is distributed to the Leaf nodes. Leaf nodes will compute the results for the request on the partition of the storage. Once the results are computed, they are aggregated back to the Aggregators and the results are shared to the client application. Aggregators and Leaves are known as the Nodes.

2) Aggregators:- There are two types of aggregators, they are master aggregator and child aggregator. Master aggregator can run the DML, DDL and CML commands. The child aggregator runs the DML commands. Child aggregator forwards the DDL commands to the Master aggregator. Child aggregators are mainly used for load balancing of the requests.

3) Cluster Requirements:- 

Master Aggregator - Must have one, Can only have one, Runs the DML, DDL and CML statements.

Child Aggregator - Don't need any, Can have multiple, DML, DDL through forwarding.

Leaf - Must have atleast one, Can have multiple or many.

4) Leaf Nodes and Data Storage:- 


![image](https://user-images.githubusercontent.com/8998457/133766672-13fa7321-62af-413f-a141-1d0700705e6c.png)


Master Aggregator -> Child Aggregator -> Leaf -> Partitions

Partitions hold the databases and the tables. SingleStore uniformally distributes the data among the Leaf nodes.

5) All Up Architecture:-

Master Aggregator and Child Aggregator load balances to the leaf nodes.



![image](https://user-images.githubusercontent.com/8998457/133602455-2ac3ceb1-18a2-454b-8723-50142be7ae35.png)


6) High Concurrency Architecture:-



![image](https://user-images.githubusercontent.com/8998457/133602491-0938c3f7-976d-4260-a0ca-1a80ee978a05.png)

7) Low Latency Architecture:-



![image](https://user-images.githubusercontent.com/8998457/133602539-974c2b1d-c944-467e-9f9a-1291110cc0ec.png)



References:

SingleStore Training.
