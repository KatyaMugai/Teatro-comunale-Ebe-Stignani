layout: default
title: Challenges
---


---

# Challenges

Working with the ArCo Knowledge Graph and Large Language Models to enrich the representation of Teatro Stignani presented several practical and methodological challenges.

## Locating and Identifying the Correct Resource

A first challenge was simply confirming which ArCo resource actually corresponded to the theatre. Some endpoint pages returned no embedded statements at all, while others returned inconsistent results depending on whether the data was retrieved as raw Turtle or parsed from embedded HTML+Microdata. This made it difficult to fully trust a single source as authoritative and required cross-checking multiple retrieval methods before treating any fact as confirmed.

## Sparse and Uneven Data Coverage

The theatre's record captures only the basic institutional "skeleton" expected of a cultural site — its site, address, opening hours, and custodianship role — but little else. This contrasts with other ArCo entities, such as the Fontana del Nettuno, which are enriched with Subject-level and iconographic metadata. This unevenness across resources of comparable importance made it hard to predict, in advance, what kind of data any given query would actually return.

## Ambiguous Keyword Search Results

General keyword searches for "teatro" were heavily diluted by unrelated event and ticketing records, as well as lexical overlap with "anfiteatro." Isolating theatres as a coherent subset required additional filtering beyond simple string matching, revealing a structural limitation in ArCo's current labeling and typing conventions rather than a one-off data quality issue.

## Distinguishing Confirmed Facts from Plausible Inference

Because several gaps involved missing links (to a person, to alternative names, to a subject classification), it was tempting to fill them with plausible-sounding values. A recurring challenge was keeping proposed enrichment strictly separate from confirmed data, and resisting the temptation to assert an ontology term, identifier, or property whose exact structure had not been independently verified — for example, avoiding ArCo's `CISNameInTime` pattern once its internal property structure could not be confirmed, in favor of the safer, standard `skos:altLabel`.

## Choosing Appropriate Vocabulary for Missing Relationships

ArCo does not offer a ready-made property for some of the identified gaps, such as linking a cultural institute to the person it is named after. This required searching outside ArCo itself — ultimately using Wikidata's `wdt:P138` ("named after") — and carefully verifying that any external vocabulary chosen was well-established and properly documented, rather than inventing a new predicate.

## Comparing Outputs from Two LLMs

Using both Claude and Grok to propose candidate enrichment triples introduced the challenge of comparing two independent outputs for consistency, accuracy, and adherence to valid RDF/Turtle syntax. Differences in how each model approached vocabulary choice, syntax conventions, or handling of uncertain facts had to be reconciled manually rather than merged automatically.

## Inconsistent Modeling Across Site Types

Query results showed that ArCo models `CulturalEvent` entities extensively for some site types, such as archaeological sites and amphitheatres, but not for the theatre. This inconsistency in coverage across otherwise comparable entity types made it harder to generalize a single enrichment strategy across the knowledge graph, since gaps identified for one resource type do not necessarily apply uniformly to others.
