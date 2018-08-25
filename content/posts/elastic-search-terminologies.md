+++
draft = false
date = 2018-08-25T13:58:43-07:00
title = "High-level Overview of Elasticsearch"
slug = ""
tags = []
categories = ["Elasticsearch"]
+++

---

## What this post is about

This is to summarize key concepts used in understanding Elasticsearch.

In Elasticsearch, the term **index** appears quite often in different contexts. This post is to clear this ambiguity and to facilitate understanding what Elasticsearch is about.

## What is Elasticsearch

1. A **NoSQL** database specialized for extremely fast search capability.
2. A **distributed system** where you may shard and replicate your database content throughout your cluster.

## Key Concepts

1. Elasticsearch Index
2. Lucene
3. Shard
4. Replication

##### Elasticsearch Index

**Elasticsearch Index** is logically equivalent to SQL table.

Since Elasticsearch is a NoSQL database, documents do not have a fixed schema. However, similar to how SQL tables contain similarly typed information, you group your documents in different Elasticsearch Indexes.

When you insert/update a document from your Elasticsearch Index, it is called **indexing your document** into your Elasticsearch Index.

##### Lucene

If you are coming from SQL background, you would know InnoDB is MySQL's search engine which indexes your table entries allowing for a near instantaneous look-up.

What happens underneath is that your primary keys are used to build a tree where each node in the tree points to their corresponding table entry.

This tree building step is called **indexing**.

**Lucene** is a Java-based search engine backed by Apache Software Foundation.

What Lucene does is it basically breaks down your document into many terms and maps each term to your original document.
For example, "Hello World" is tokenized(broken down) into two terms: "Hello" and "World". Then each term would be pointing toward the original sentence "Hello World".

This concept is similar to SQL database's indexing. Lucene builds its index tree using the tokenized terms to point toward the original document.

Therefore, when you are indexing your document, you are essentially building a new updated Lucene search index.

##### Shard

In SQL databases, sharding is about breaking down your data source into multiple servers for scaling your database to reduce loads on each of your database servers.

In Elasticsearch, a single Lucene Index is basically an Elasticsearch Index's shard. If your Elasticsearch Index has two shards, it means your Index is broken into two Ludene Indexes.

By breaking into multiple Lucene Indexes, you can execute parallel operations across your shards.

To put it to summary, **An Elasticsearch Index is made up of one or more Lucene Indexes**.

##### Replication

When managing your database, you must be ready to handle failure scenarios.

Your server may die due to hardware problem, or your connection to the database can be shut off due to power outage or network failures.

In Elasticsearch, it allows replicating your shards across the cluster.

The very basic benefit of replicating your shards is **the chance of losing your data is reduced**.

Another benefit is that with more shards, **more parallel search operations can be executed**.

## Summary

1. Elasticsearch uses Lucene as its search engine
2. Elasticsearch Index is made up of one or more Lucene Indexes.
3. Lucene builds an index tree by tokenizing your document to use it as the search key.
4. Sharding and Replication allows horizontal scalability with high fault tolerance.

As you can see the term **index**, is used in different contexts along different layers of the Elasticsearch architecture.

Following sentence should summarize your understanding of this post:

**In Elasticsearch, you index your document into an Elasticsearch Index where Lucene shard is updated with a new index tree for fast loop up performance.**

---

## References

1. [Elasticsearch Basic Concepts](https://www.elastic.co/guide/en/elasticsearch/reference/current/_basic_concepts.html)
2. [Elasticsearch from the Top Down](https://www.elastic.co/blog/found-elasticsearch-top-down)
3. [Elasticsearch from the Bottom Up](https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up)
