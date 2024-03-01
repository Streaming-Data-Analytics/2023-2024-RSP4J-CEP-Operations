# 2023-2024 RSP4J CEP Operations

Optional project of the [Streaming Data Analytics](http://emanueledellavalle.org/teaching/streaming-data-analytics-2023-24/) course provided by [Politecnico di Milano](https://www11.ceda.polimi.it/schedaincarico/schedaincarico/controller/scheda_pubblica/SchedaPublic.do?&evn_default=evento&c_classe=811164&polij_device_category=DESKTOP&__pj0=0&__pj1=d563c55e73c3035baf5b0bab2dda086b).

Student: **[To be assigned]**

## Description 

Complex Event Processing (CEP) is an advanced method used to process and analyse large streams of information from various sources in real time. It allows organisations to monitor, detect patterns, and respond to complex sequences of events in an efficient and timely manner. This technology is particularly useful in scenarios where the ability to make immediate decisions based on dynamic data is crucial.

CEP works by identifying and correlating events that occur across different data streams. An event can be anything that happens, or a notable change in data, which can be processed to derive insights. CEP systems are designed to handle high volumes of data with minimal latency, making them ideal for applications in finance, healthcare, telecommunications, and other sectors where real-time analytics are essential.


### Project Goal

This project aims at designing and implementing Complex Event Operators in RSP4J.

In particular, the project targets CEP function available in RSEP-QL, an extended model for CEP over RDF streams, Allen Algebra Operations, and The Every operation.

### RSP4J

RSP4J is a library to build RDF Stream Processing (RSP) Engines according with the reference model RSP-QL. RDF is a graph data model for the Web. RDF streams are infinite sequences of RDF timestamped RDF data. The library  is inspired by the OWL API, and attempt to uniform the access to existing RDF-based DSMS. 

In this [repository](https://github.com/streamreasoning/rsp4j), you will find several projects, including

- API, which contains the interfaces and abstractions required to develop your RSP engine.
- yasper, which is an reference implementation that aims at showing the API usage by providing org.streamreasoning.rsp4j.yasper.examples.
- examples to understand the genral functioning of RSP4K

## Prior Knowledge

### CEP Operations

First return the first occurrence of an event in the stream

Last return the last occurrence of an event in a stream

Every Operator Examples

|Example|Description|
|---|---|
|every ( A -> B )|Detect an A event followed by a B event. At the time when B occurs the pattern matches, then the pattern matcher restarts and looks for the next A event.<br><br>1. Matches on B1 for combination {A1, B1}<br>    <br>2. Matches on B3 for combination {A2, B3}<br>    <br>3. Matches on B4 for combination {A4, B4}|
|every A -> B|The pattern fires for every A event followed by a B event.<br><br>1. Matches on B1 for combination {A1, B1}<br>    <br>2. Matches on B3 for combination {A2, B3} and {A3, B3}<br>    <br>3. Matches on B4 for combination {A4, B4}|
|A -> every B|The pattern fires for an A event followed by every B event.<br><br>1. Matches on B1 for combination {A1, B1}.<br>    <br>2. Matches on B2 for combination {A1, B2}.<br>    <br>3. Matches on B3 for combination {A1, B3}<br>    <br>4. Matches on B4 for combination {A1, B4}|
|every A -> every B|The pattern fires for every A event followed by every B event.<br><br>1. Matches on B1 for combination {A1, B1}.<br>    <br>2. Matches on B2 for combination {A1, B2}.<br>    <br>3. Matches on B3 for combination {A1, B3} and {A2, B3} and {A3, B3}<br>    <br>4. Matches on B4 for combination {A1, B4} and {A2, B4} and {A3, B4} and {A4, B4}|


### Allen's Algebra

Allen's Interval Algebra is a calculus for temporal reasoning that allows one to infer relationships between time intervals. In this system, time intervals are defined by their start and end points, and relationships describe how intervals relate to one another in time. Allen identified 13 basic, mutually exclusive relationships that can exist between two time intervals, along with their inverses and the identity relation. These relationships provide a powerful framework for reasoning about temporal events.

Here is a table summarizing Allen's Interval Algebra operations (relationships):

| **Relationship** | **Symbol** | **Description**                                              |
|------------------|------------|--------------------------------------------------------------|
| Before           | \(A < B\)  | A happens completely before B.                               |
| After            | \(A > B\)  | A happens completely after B. (Inverse of Before)            |
| Meets            | \(A m B\)  | A ends exactly when B starts.                                |
| Met by           | \(A mi B\) | A starts exactly when B ends. (Inverse of Meets)            |
| Overlaps         | \(A o B\)  | A starts before B and ends after B starts but before B ends. |
| Overlapped by    | \(A oi B\) | A starts after B starts but before B ends, and ends after B. (Inverse of Overlaps) |
| During           | \(A d B\)  | A starts after B starts and ends before B ends.              |
| Contains         | \(A di B\) | A starts before B starts and ends after B ends. (Inverse of During) |
| Starts           | \(A s B\)  | A and B start at the same time, but A ends before B.         |
| Started by       | \(A si B\) | A and B start at the same time, but A ends after B. (Inverse of Starts) |
| Finishes         | \(A f B\)  | A starts after B starts and ends at the same time as B.      |
| Finished by      | \(A fi B\) | A starts before B starts and ends at the same time as B. (Inverse of Finishes) |
| Equals           | \(A = B\)  | A and B start and end at the same times.                     |

## Material

### RSP4J

In this [repository](https://github.com/streamreasoning/rsp4j), you will find several information about RSP4J, including

- API, which contains the interfaces and abstractions required to develop your RSP engine.
- Yasper, which is an reference implementation that aims at showing the API usage by providing org.streamreasoning.rsp4j.yasper.examples.
- examples to understand the general functioning of RSP4J

#### Window Operators in RSP4J

RSP4J combines the logic of CQL and SECRET. It identified operators according to three families (see figure below)

![[cql.png]]

The internals of window operator follow the logic of SECRET. They are operationalised according to four functions: tick, scope, content, and report. The operations needs to be redefined for incorporating the Frame semantics. Example of existing implementation for time-based sliding windows are linked below.

- [Example from C-SPARQL](https://github.com/streamreasoning/rsp4j/wiki/C-SPARQL-SLIDING-WINDOW-OPERATOR)
- [Example from CQELS](https://github.com/streamreasoning/rsp4j/wiki/CQELS-SLIDING-WINDOW-OPERATOR)

### Datasets

The project should work with two datasets, 

- [DEBS Challenge 2017](https://ckan.project-hobbit.eu/dataset/debs-grand-challenge-2017)
- New York City Taxi,  by representing the data in RDF
- and a synthetic dataset to be created for the test cases.


## References

- [RSP4J](https://openreview.net/pdf?id=IbXJmD1i2WA)
-  [@dellaglioQueryModelCapture2016](https://www.zora.uzh.ch/id/eprint/132902/1/main.pdf)
- [@2018tommasiniQueryModelOntologyBased](https://biblio.ugent.be/publication/8581984/file/8581985.pdf)
- *[@2012cugolaProcessingFlowsInformation](https://margara.faculty.polimi.it/papers/survey.pdf)

## Note for Students

* Clone the created repository offline;
* Add your name and surname into the Readme file;
* Make any changes to your repository, according to the specific assignment;
* Add a `requirement.txt` file for code reproducibility and instructions on how to replicate the results;
* Commit your changes to your local repository;
* Push your changes to your online repository.
