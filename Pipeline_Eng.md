# Pipeline

## Goal

We want to seek information on the Web regarding a certain person, to enrich her Wikidata.

## Classifier

The classifier reads texts written for humans and taken from various sources. It returns triples (according to a given format) describing the sought person. The triples are coupled with a probability, grading the reliability of each triple, and possibly with a score to give an indication on biases that affect the triple. 

## CDuce-based tool

The CDuce-based tool organises the triples by creating a knowledge graph that is compatible with the Wikidata's graph, in such a way the information collected and formalised can be integrated into Wikidata writings about the sought person in a formally safe way.

In particular, the CDuce-based must:

- Find a type for the triples: this is the core of the elaboration, because the type represents in an abstract and formal manner the information included in the triple, how much it is reliable and whether if it is affected by biases or not. A type-checking algorithm will separate valid triples from not valid ones. The criteria on which the algorithm will do the checks are also a fundamental part of the study. We plan to have a flexible algorithm, in such a way criteria can be enriched and changed overtime.

- Check if a triple is valid.

- Establish if two triples represents the same information.

- Build an ontology about the sought person with the validated triples, in such a way the ontology can be integrated within the Wikidata's graph.


###### Type hierarchy

We plan to create a type hierarchy describing some aspects of the life of a person, on the basis of statistical analyses and/or via consultations with Humanities experts. 
When a triple is retrieved, we would like to include it in a deterministic position into the hierarchy. This approach will endow modelling and organising knowledge in a precise way, and will help tracing the reasoning flow when querying an ontology typed within such a type hierarchy. 


#### Typing of the triples: obstacles

The main difficulty is to be able to gather as many aspect as possible of a person's life beforehand, to be modelled with formal types. We surely can do that for the average person, however it would be interesting to be able to include in the types uncommon aspects according to the needs (for instance, when we want to study a certain group/category of people), in order to enrich the base hierarchy structure and avoid loosing important information in the formalisation, for instance about biases.

However, the task of modelling concepts regarding ethics and moral issues with formal types is difficult, being those themes rather sensitive. Therefore, at first, we will concentrate on types representing objective feautures of people. Then, we plan to discuss more descriptive types with Humanities experts.


###### Naive approach

Without creating a proper hierarchy, we can exploit the triples extracted by the classifier to create a non-structured knowledge basis. With this approach the checks on the triples can be performed directly, mainly by considering the extra data attachd to the triples, i.e., the probability grading the reliability of each triple, and the score giving an indication on possible biases.

On the one hand, this approach has the advantage of not needing "a priori" knowledege of the domain, that is, the features to be considered in order to model a certain category of people. The analysis of the triples would be done mostly manually, including the integration of new data into the Wikidata graph. On the other hand, we do think that the formal approach hinted at above can give benefits, in terms of correctness of the data and efficiency of the integrations. 

This naive approach is nevertheless necessary in order to tackle the formal approach, in order to learn how to build knowledge basis compatible with the Wikidata format, and to extract precise requirements for the classifier and the CDuce-based tool.


## Glance at high level

<img title="" src="Pictures/pipeline_white.svg" alt="" width="983">
