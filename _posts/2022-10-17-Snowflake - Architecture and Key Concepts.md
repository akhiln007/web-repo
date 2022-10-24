---
layout: post

title: Snowflake - Architecture and Key Concepts
---



{{ page.title }}

================
What is Snowflake

A cloud data platform offered as a service. Snowflake is the first analytical database built for the cloud, delivered as a datawarehouse as a service.

How does Snowflake differ from other traditional architectures.

Snowflake’s architecture is a hybrid of traditional shared-disk and shared-nothing database architectures. Similar to shared-disk architectures, Snowflake uses a central data repository for persisted data that is accessible from all compute nodes in the platform. But similar to shared-nothing architectures, Snowflake processes queries using MPP (massively parallel processing) compute clusters where each node in the cluster stores a portion of the entire data set locally. This approach offers the data management simplicity of a shared-disk architecture, but with the performance and scale-out benefits of a shared-nothing architecture.

![image](https://user-images.githubusercontent.com/8998457/196169851-da0ff0a2-dad8-4c2e-a001-b0bb95cf8a1b.png)


Snowflake’s unique architecture consists of three key layers:

I. Database Storage

Snowflake manages all aspects of how this data is stored — the organization, file size, structure, compression, metadata, statistics, and other aspects of data storage are handled by Snowflake. 

1. Hybrid Columnar

2. Automatic micro-partitioning

3. Natural data clustering and optimization.

4. Native semi-structured data support and optimization.

5. All storage within Snowflake is billable(Compressed).

II. Query Processing

Query execution is performed in the processing layer. Snowflake processes queries using “virtual warehouses”. Each virtual warehouse is an MPP compute cluster composed of multiple compute nodes allocated by Snowflake from a cloud provider.

III. Cloud Services

1. Brains of the service. 

2. Manages and coordinates activities across Snowflake.

3. Runs on compute instances provisioned by Snowflake.

Services managed in this layer include:

Authentication

Infrastructure management

Metadata management

Query parsing and optimization

Access control
