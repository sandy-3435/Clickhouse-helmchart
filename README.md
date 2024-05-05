# PillaSandeep-Datazip-Assignment
 DataZip assignment

To install clickhouse-server we have to install Helm package manager for Kubernetes and Command line tool (kubectl) for kubernates.\ and then,

1. Execute the command "$ helm install clickhouse ["Path of the repo downloaded"]"
2. To check the ClickHouse pods are running "$ kubectl get pods"
------------------------------------
   
# **Testing Data Movement**

To specifically test data movement from hot to cold storage based on the configured move factor (0.2):

1.Deploy ClickHouse with Hot-Cold Configuration:
>Use the Helm chart you've created to deploy ClickHouse with the hot-cold configuration onto your Kubernetes cluster.

2.Create a Test Table:
>Connect to the ClickHouse instance deployed in the Kubernetes cluster.
>Create a test table similar to the one specified in your SQL statements 

       CREATE TABLE dz_test
       (
         `B` Int64,
         `T` String,
         `D` Date
       )
       ENGINE = MergeTree
       PARTITION BY D
       ORDER BY B
       insert into dz_test select number, number, '2023-01-01' from numbers(1e9);


3.Generate Data:
> Insert a significant amount of data into your ClickHouse database, ensuring it exceeds the threshold for hot storage.

4.Monitor Mutation:
> Continuously monitor the system.mutations table to observe mutations occurring in the database.

5.Data Redistribution:
> Over time, observe how data is redistributed between hot and cold storage. With a move factor of 0.2, approximately 20% of the data should be moved from hot to cold storage as per ClickHouse's built-in policies.

6.Verify Results:
>Check the size of storage volumes associated with ClickHouse pods to verify that data has been moved according to the configured move factor.
