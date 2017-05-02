---
title: Efficiently processing aggregation function in massively parallel computing

categories: works
background-image: background.jpg
excerpt: ""
author: czhang
---

# Objective of research

The goal of our research work is efficiently processing aggregation function in massively parallel computing, particularly in spark and flink.

# Introduction

The ability of summarizing information, the intrinsic feature of aggregation, is drawing increasing attention for information analysis. Simultaneously under the progress of data explosive growth, processing aggregate function has to experience a transition to massively distributed and parallel framework, e.g. MapReduce, Spark, Flink etc. In our work, we are interested by the design of a generic framework that enables to map an aggregation function into an efficient massively parallel algorithm.

The inherently property of aggregation, taking several values as input and generating a single value based on a certain criteria, requires a decomposition approach in order to be executed in distributed architecture. Decomposition of an aggregation function enables to compute partial aggregation that can then be merged together to obtain the final result. When an aggregation function is decomposable, how to decompose it and when a decomposition is 'efficient' is a hard nut to crack.

My research focuses on designing generic framework that enables to map symmetric and asymmetric aggregation functions into an efficient massively parallel algorithm. 

# Platform setup

1 driver node

* Name: Master
* OS: Ubuntu Server _Spark
* CPU: 2 cores
* RAM: 2GB
* Disk: 40GB

3 worker nodes

* Name:Slave_(1,2,3)
* OS: Ubuntu Server _Spark
* CPU: 1 core
* RAM: 2GB
* Disk: 80GB

# Test
Commming soon...
