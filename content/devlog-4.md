---
id: learning-from-the-fediverse
aliases:
  - learning-from-the-fediverse
tags: []
date: "2025-03-30"
draft: False
title: "Devlog 4: Learning from the Fediverse"
---

## Or, Towards a Decentralized Library Infrastructure

In recent years, and especially following the consolidation of social media companies such as Twitter, Instagram, Facebook, etc., there is general collective feeling that the _status quo_ of "the open web" is gone. In its place arose _federated_ social media apps, such as Mastodon, Lemmy, and Pixelfed. As OCLC proves itself to care less and less about being a non-profit institution, it is time to break down the late 20th-century thinking on centralization, and move towards a decentralized library infrastructure. It is my belief that we as librarians take a queue from the success of federated systems to implement a federated library discovery and lending protocol.  This post is a first draft of my ideas on what that protocol must include.

## Introduction

### Terms

1. Node: A node is owned by a single library. A node serves data to a library's *agents*. May also be referred to as a "server."
2. Institution: An institution is a library. Each institution is composed of many *agents*.
3. Collective: A group one or more institutions that mutually agree to *federate* nodes with one-another.
4. Collection: A group of one or more *works*.
5. Work: A cataloged resource to which *metadata* (or optionally, the object itself), is attributed.
6. Metadata: Data about a *work*. Can be formatted in a number of different standards, including RDF, Dublin Core, MARC, BIBFRAME, etc.
7. Agents: Human or non-human (robot) users of the federated database. May also be referred to as a "client."

### Architecture, in Human Terms

Each library (institution) runs a node. The node serves as a data provider *at the edge*. When a searches for "Moby Dick" at Northwestern University, the query is routed to Northwestern's node. The node then returns the top results matching the query "Moby Dick". When a user checks out a book, the status is changed from "available" to "checked-out" on Northwestern's node.

Northwestern University library may like their users to see what other Big 10 (Big Ten? BigTen?) institutions have in their collection, say, with the University of Chicago, and *vice versa*. Northwestern University's database then *federates* with the University of Chicago's database, in which the two institutions *nodes* exchange data with one-another. Thus, if a user at University of Chicago wants to view Northwestern's collections, they can do so from the University of Chicago's website. For example, one of Northwestern's more unique collections include Environmental Impact Statements. If a user at the University of Chicago searches through the University of Chicago's website for environmental impact statements, the request will hit the University of Chicago's node, which then the University of Chicago node requests Northwestern's node for their results. This allows for universities that federate with one-another to interoperate with one another efficiently.

## Data Model

There are really only four objects required in this data model: agents, institutions, works, and sets thereof.

### The AGENT model

The AGENT model consists of the following required attributes:

1. Name
2. Institution (if any)
3. Checked out works (if any)

So long as the AGENT consists of these three fields, a single institution can add other fields to fit the needs of that specific institution (barcode numbers for ID cards, email address, phone numbers, etc.) 

Optional extensions to the AGENT model that could be helpful would be a "privileges" field that determines what an AGENT can do on the instance (can they create metadata? new records? Search? Check out books?)

### The INSTITUTION Model

The INSTITUTION model consists of the following required attributes.

1. Name
2. Location
3. Agents

The name of the institution is self-explanatory, the location is the ROR identified location of the institution, and the agents are agents "belonging" in that institution.

### The WORK Model

The WORK model consists of the following required attributes:

1. Metadata
2. Availability Status
3. Institution Owner
4. Copy Num.

Metadata is information about the work (title, date published, creators, etc.), Availability status: can be one of many fields (unavailable, available, etc.), the institution is the owner of that particular *instance* of that work. Copy Num is unique value (not necessarily sequential) that differentiates between different instances of the same work.

### The SET Model

The SET model consists of a set of objects listed above to carry out a specific purpose.

A SET of AGENT objects can represent the students currently enrolled in the institution. A SET of INSTITUTION objects can represent an academic alliance (Big Ten, for example, I don't know any other academic alliances and I don't care to find out). A SET of WORK models can represent a particular building in which each WORK is housed, etc.

## HTTP Methods

### The SEARCH Method

#### Parameters

AGENT: The agent making the request
QUERY: A query to the database (be it keyword, structured, faceted, etc.)

This method is initiated by a client and hits a node. The query is run by the server, and results are returned to the client. This query does not propagate to other nodes.

### The CREATE_WORK Method

#### Parameters

AGENT: The agent making the request (including authorization)
WORK: A representation of a WORK object.

This method creates a new work in the server. This method propagates to other servers.

### The CHECK_OUT Method

AGENT: The agent making the request (including authorization)
WORK: A representation of a WORK object.

This method changes the availability status of a work to unavailable. This status then propagates to other nodes in the federation.

### The CREATE_USER Method

INSTITUTION: The institution creating the user.
AGENT: The user being created.

Creates a user that belongs to an institution.
