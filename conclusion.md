layout: default
title: Conclusion
---

## Teatro comunale Ebe Stignani

---

# Conclusion

This project set out to investigate how the Teatro comunale Ebe Stignani in Imola is represented in the ArCo Knowledge Graph, to identify gaps in that representation, and to test whether Large Language Models could meaningfully support the process of proposing RDF enrichment.

## What the SPARQL Exploration Revealed

The initial queries confirmed that the theatre is indeed present in ArCo's linked open data, but not within the main ICCD/ArCo catalogue used for monuments such as the Fontana del Nettuno. Instead, it belongs to the "Luoghi della Cultura" dataset, represented as a `CulturalInstituteOrSite` (record 107917) surrounded by a small cluster of satellite resources — a `CreativeWork`, a `Site`, an `Address`, an `OpeningHoursSpecification`, and a `TimeIndexedRole`. This confirmed that ArCo captures the theatre's basic institutional identity, location, and administrative oversight, but stops there.

Broader searches for "teatro" and for images linked to the theatre exposed two further structural issues: the keyword "teatro" is heavily diluted by unrelated event/ticketing records and by lexical overlap with "anfiteatro," and no photographic documentation exists for the theatre under `arco:HistoricOrArtisticProperty`, unlike the richly documented Fontana del Nettuno. These were not query failures, but genuine, meaningful findings about how differently ArCo models institutional sites compared to iconographically rich monuments.

## Gaps Identified

Five gaps were identified in the theatre's representation:

1. No `arco:Subject` classification linking the theatre to any semantic or thematic descriptor.
2. No alternative naming captured — only the single official label is used throughout the dataset.
3. No explicit link between the theatre and Ebe Stignani, the person it is named after.
4. No linked creative works, events, or holdings, despite ArCo modelling such connections extensively for other site types.
5. Structural ambiguity in keyword search caused by overlap with unrelated entity types.

Three of these gaps — Subject classification, alternative naming, and the link to Ebe Stignani — were carried forward into the enrichment phase.

## What the LLM Comparison Showed

Both Claude and Grok were tested with the same prompts, first for name classification, then for a structured chain-of-thought cultural analysis of the theatre, and finally for generating candidate RDF triples addressing the three selected gaps.

The chain-of-thought prompt produced the most useful results overall. Claude leaned toward narrative and art-historical detail (architectural specifics, social history, comparisons with theatres named after composers), while Grok leaned toward concise institutional facts (capacity, addresses, historical names, comparisons with theatres named after singers). Neither output was wrong, but each emphasised different aspects of the same subject — a reminder that LLM output reflects a particular framing rather than a single objective description.

For RDF generation, both models produced syntactically valid Turtle and were able to execute successfully as SPARQL CONSTRUCT queries, each generating between two and eight statements depending on the gap. However, their approaches diverged in vocabulary choice: for the "named after" relationship, Claude used the Wikidata property `wdt:P138`, while Grok used `schema:namedAfter` alongside `dcterms:subject` and `rdfs:seeAlso`. Both are defensible, standard choices, but they are not identical — which confirms that LLM-generated triples cannot be merged automatically and require human review before being accepted into a knowledge graph.

## Final Reflections

The project confirms that Large Language Models can be genuinely useful assistants in cultural heritage knowledge graph enrichment: they are effective at drafting candidate triples, explaining their reasoning, and suggesting relevant external vocabularies (Wikidata, Getty AAT, SKOS) that a manual process might overlook. At the same time, their outputs are not interchangeable or fully autonomous — each model made different modelling choices for the same gap, and some proposed identifiers or properties required independent verification before they could be trusted as accurate.

The most reliable workflow to emerge from this project is therefore a hybrid one: SPARQL exploration to establish what is confirmed and what is missing, LLM assistance to draft candidate enrichment triples and vocabulary options, and human verification to separate confirmed facts from proposed enrichment before anything is added to the graph. This approach preserves the rigour expected of a cultural heritage knowledge graph while taking advantage of what LLMs are genuinely good at: fast, well-reasoned drafting of structured knowledge.
