<img width="1538" height="1130" alt="image" src="https://github.com/user-attachments/assets/366ca32c-be61-4ef9-be2f-4a2827250a14" />layout: default
---

# Teatro comunale Ebe Stignani

## Enriching Cultural Heritage Knowledge with ArCo and Large Language Models

[View on GitHub](https://github.com/aermosina86-sudo/fontanadelnettuno)

[🏠 Home](index.html) | [🏛️ Topic](topic.html) | [🛠️ Methodology](methodology.html) | [📊 SPARQL & Results](sparql.html) | 🔍 Identifying Gaps | [💬 LLM Prompts](prompts.html) | [🔗 RDF Triples](triples.html) | [⚠️ Challenges](challenges.html) | [✅ Conclusion](conclusion.html)

---

# Identifying Gaps
After exploring the ArCo Knowledge Graph through SPARQL queries, several possible information gaps were identified in the representation of the Teatro Stignani in Imola. The purpose of this section is to explain which information is already present in the dataset and which relationships could be made more explicit through RDF enrichment.
What is already present
The theatre is represented as a CulturalInstituteOrSite (record 107917), surrounded by a small cluster of satellite resources following ArCo's standard modeling template for cultural institutes:
•	A CreativeWork record ("Imola - Teatro comunale Ebe Stignani")
•	A Site resource, capturing its physical presence/location
•	An Address, describing where the theatre is situated
•	An OpeningHoursSpecification, indicating closure periods
•	A TimeIndexedRole, recording MiBACT's supervisory/custodianship role over time
This shows that ArCo does capture the theatre's basic institutional identity, physical location, and administrative oversight — the minimum structural "skeleton" expected for a cultural site.
Gaps identified
1.	No Subject classification. Unlike what might be expected for a well-documented monument, Teatro Stignani has no corresponding entity typed as arco:Subject. This means the theatre is not linked to any semantic/thematic descriptors (e.g., architectural style, historical period, typology such as "teatro all'italiana") that would allow it to be discovered or related through subject-based browsing, the way iconographically rich monuments like the Fontana del Nettuno can be.
2.	No alternative naming captured. The UNION query testing for a possible historical or colloquial name (e.g., "Politeama") returned no additional matches. Every associated resource uses only the single official name, "Teatro comunale Ebe Stignani." If the theatre had earlier names, nicknames, or was known differently before its dedication to soprano Ebe Stignani, this is not reflected in the graph — a missed opportunity for skos:altLabel or similar enrichment.
3.	No explicit link to the person it is named after. The theatre's name commemorates soprano Ebe Stignani, yet nothing in the retrieved data connects the CulturalInstituteOrSite to an Agent/Person entity representing her. A property such as dedicatedTo or a link to a biographical resource would make this relationship explicit and queryable, rather than only implicit in the string label.
4.	No linked creative works, events, or holdings. Aside from the generic CreativeWork record duplicating the institute's name, there are no connections to performances, seasons, artistic productions, or cultural events historically or currently hosted at the theatre — even though Query 6/7 showed ArCo does model CulturalEvent entities extensively elsewhere (e.g., for archaeological sites and amphitheatres). This suggests an inconsistency in coverage: event-rich documentation exists for some site types but not for this theatre.
5.	Ambiguity in broader "teatro" search results. The general keyword search for "teatro" was heavily diluted by (a) unrelated event/ticketing records, and (b) lexical overlap with "anfiteatro." This indicates that ArCo's current labeling and typing conventions make it difficult to isolate theatres as a coherent subset without additional filtering — a structural limitation that could be addressed by a dedicated TheatreType subclass or consistent thematic tagging distinguishing theatres from amphitheatres and other performance/event-hosting sites.
Summary
Compared to the Fontana del Nettuno, which is enriched with Subject-level and iconographic metadata, Teatro Stignani's ArCo representation is comparatively minimal: it captures institutional and administrative facts (site, address, hours, custodianship) but lacks semantic classification, alternative naming, person-linkage to its namesake, and connections to artistic/cultural activity. These gaps suggest that RDF enrichment — particularly around Subject typing, skos:altLabel, and explicit dedicatedTo/agent relationships — would substantially improve the discoverability and semantic richness of the theatre's record in the knowledge graph.

