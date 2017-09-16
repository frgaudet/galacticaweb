---
title: Practical Passive Leakage - Abuse Attacks on Symmetric Searchable Encryption
categories: works
background-image: background.jpg
excerpt: ""
author: mgiraud
---

# Main goal

The goal of the profect is to evaluate the impact of our
attacks on encrypted data sets produced via Symmetric Searchable
Encryption schemes.

# Excerpt

With the growing importance of digital data in everyday life,
it is necessary to have backups and to have access from anywhere. For
these reasons, outsourcing this digital data to a cloud provider is an
enticing solution. However, some of this data, such as legal
documents, banking and medical, the industrial patents or simply our
emails can be sensitive and/or confidential, forcing the user to trust
its cloud provider. Client-side symmetric encryption is the classical
answer to the problem of data confidentiality. However, encryption
prevents any server-side processing of the client data as is the norm
on plaintext data. In particular, a server is not able to answer
search queries, that is given a keyword, retrieve the documents
containing that keyword. Symmetric Searchable Encryption (SSE) schemes
introduced in 2000 by Song et al. aim at retaining this search
capability on encrypted data. SSE scheme is a protocol between a
client and a server. The client owns a sensitive data set but has
limited computational power and storage capacity. The server has a
large storage space and high processing power, but is not trusted by
the client except for executing correctly the search protocol. The set
of plaintext documents are stored in a database. An SSE scheme creates
metadata that is protected in an encrypted database and then stored by
the server. From a keyword and his symmetric secret key the client
creates a search token that is sent to the server who finds the
encrypted documents matching the query with the help of encrypted
database. Such documents are then sent back to the client for
decryption.

In this project, we run our three different attacks on real-world
encrypted data sets to show their devastating effect. The first data
set is the email data set from the Enron corporation, built of 490,369
emails. The second and third data sets are mailing lists from the
Apache foundation, namely Apache Commons and Apache Lucene composed
respectively of 28,997 and 58,884 emails. The last data set is the
Project Gutenberg composed of 21,602 copyright free books.

# Resources used (RAM CPU etc...)

16 VCPU, 64Gb of ram.

# Software used

The programming language Python and the NoSQL
database SSDB (an alternative to Redis).

# Results

Our attacks are devastating and have a real impact on the
protected data in the cloud: regardless of the leakage profile,
knowing a mere 1% of the document sets translates into over 90% of
documents whose content is revealed over 70%. Moreover, having same
knowledge from the data set, we show that we recover same rate of
keywords whether it is with L4- or with L3-SSE schemes. We show too
that the gap of security that exists between L2- and L1-SSE schemes is
important since L1 attacks need to know a large amount of information
to recover frequent keywords contrary to our L2 attack. Our results
give a better understanding of the practical security of SSE schemes
and hopefully will help practitioners make more secure SSE schemes.

# Publication:
Practical Passive Leakage-Abuse Attacks on Symmetric Searchable
Encryption.
Alexandre Anzala-Yamajako, Olivier Bernard, Matthieu Giraud, and
Pascal Lafourcade.
SECRYPT (International Conference on Security and Cryptography),
Madrid, Spain, July 24-26, 2017.

Link:
[http://www.scitepress.org/DigitalLibrary/Link.aspx?doi=10.5220/0006461202000211](http://www.scitepress.org/DigitalLibrary/Link.aspx?doi=10.5220/0006461202000211)
