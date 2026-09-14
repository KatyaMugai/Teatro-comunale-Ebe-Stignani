## layout: default
---

# Teatro comunale Ebe Signani

## Enriching Cultural Heritage Knowledge with ArCo and Large Language Models

[View on GitHub](https://github.com/aermosina86-sudo/fontanadelnettuno)

[🏠 Home](index.html) | [🏛️ Topic](topic.html) | [🛠️ Methodology](methodology.html) | 📊 SPARQL & Results | [🔍 Identifying Gaps](gaps.html) | [💬 LLM Prompts](prompts.html) | [🔗 RDF Triples](triples.html) | [⚠️ Challenges](challenges.html) | [✅ Conclusion](conclusion.html)

---

# SPARQL Queries & Results

## Query 1 — Does ArCo contain our topic?
SPARQL Query
sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?resource ?label
WHERE {
  ?resource rdfs:label ?label .
  FILTER(REGEX(STR(?label), "Stignani", "i") || REGEX(STR(?label), "Stagnani", "i"))
}
LIMIT 50


 
Results
The query returned nine distinct resources whose labels contain "Stignani", confirming that ArCo/MiBACT's linked open data does contain information about Teatro Stignani. Interestingly, none of these resources use the standard arco: ontology namespace tested in earlier queries — instead, they all belong to a different vocabulary: http://dati.beniculturali.it/mibact/luoghi/resource/.... This indicates that Teatro Stignani is represented in the "Luoghi della Cultura" (Places of Culture) dataset, a linked-data resource published by MiBACT that is distinct from — though related to — the core ArCo ICCD catalogue records used in the Fontana del Nettuno queries.
All nine resources share the same numeric identifier, 107917, which functions as the internal key linking them together as a single semantic cluster describing the theatre.

Query 2
Discovering the actual predicates of a RoleInTime resource

Explanation of keywords used. Here we do not write a specific predicate (core:hasAgent); instead we use the variable ?predicate. This is a classic “DESCRIBE-style” pattern: we take the known URI of the resource as the subject and retrieve all triples in which it appears as the subject.
?object is the value or the linked resource for each predicate.
No FILTER/REGEX is used, because the URI is already exact (this is not a text search).


PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?predicate ?object
WHERE {
  <http://dati.beniculturali.it/mibact/luoghi/resource/RoleInTime/Mibac_enteCompetenteTutela_107917> ?predicate ?object .
}
 
Key finding: RO:forEntity does not point to the agent that holds the role, but back to the theatre itself (CulturalInstituteOrSite/107917). And RO:withRole does not point to a specific organisation, but to a role type — Role/enteCompetente (“competent authority”), i.e. to an abstract role category rather than to its bearer.In other words, this triple literally says: “there exists a time-indexed role of the type ‘competent authority for protection’ that applies to entity 107917” — but it does not say who that competent authority actually is. The agent’s name (probably MiBAC / the Ministry of Culture or a specific Soprintendenza) is not explicitly extracted in the data as a value — it is encoded only in the URI slug of the resource itself: Mibac_enteCompetenteTutela_107917. This directly confirms the original enrichment-gap hypothesis: the human-readable name of the agent exists only as part of the identifier, and not as a separate RDF triple — meaning the data is not fully dereferenced for machine processing.

## Query 3 — Finding image-related resources about Teatro Stignani

The task is to find visual resources (photographs of the façade, the auditorium, decorations by Felice Giani) linked to the theatre. However, this must take into account the finding from previous queries: the theatre itself lives in the “Luoghi della Cultura” dataset (dati.beniculturali.it/mibact/luoghi/, RO/schema-like ontology), and not in the main ICCD ArCo catalogue (arco:HistoricOrArtisticProperty), where photographic documentation, drawings, postcards, etc. are stored. This means that images must be searched in both vocabularies simultaneously — otherwise the result may be empty simply because we are looking in the wrong place.Explanation of keywords used
•	UNION — combines two independent search strategies: one in the main ArCo catalogue (photographic documentation as separate CulturalProperty records), the other in the “Luoghi” dataset (possible schema:image / foaf:depiction on the institutional record itself). 
•	FILTER/REGEX — search for “Stignani” in the label. 
•	OPTIONAL — retrieves the type and depiction only if they exist, without excluding the other results. 
•	DISTINCT — removes duplicates.

SPARQL Query
sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX schema: <http://schema.org/>

SELECT DISTINCT ?image ?label ?type ?depiction
WHERE {
  {
    ?image a arco:HistoricOrArtisticProperty ;
           rdfs:label ?label .
  }
  UNION
  {
    ?image rdfs:label ?label .
    FILTER(REGEX(STR(?image), "fotografico", "i"))
  }
  UNION
  {
    ?image rdfs:label ?label .
    ?image foaf:depiction ?depiction .
  }

  FILTER(REGEX(STR(?label), "Stignani", "i"))

  OPTIONAL { ?image rdf:type ?type . }
  OPTIONAL { ?image foaf:depiction ?depiction . }
  OPTIONAL { ?image schema:image ?depiction . }
}
LIMIT 50


Result

 
The table returned empty, containing only the column headers (image, label) and not a single row. This confirms the hypothesis: the query did not find any images or photographic documentation linked to the theater through arco:HistoricOrArtisticProperty, foaf:depiction, or the "fotografico" pattern.
Interpretation of the Results
This is a significant null result. In the context of an academic project, this is not a case of "the query failed to work," but rather a meaningful finding regarding the data structure. Let us compare this with what we already know about the Teatro Stignani from previous queries:
•	All 9 previously discovered resources (Query 1) belong to the "Luoghi della Cultura" vocabulary (dati.beniculturali.it/mibact/luoghi/) and represent the theater purely as an administrative and institutional entity, detailing its address, geographic coordinates, opening hours, and the roles of responsible authorities (enteCompetenteTutela, enteProprietario).
•	None of these 9 resources belong to the arco:HistoricOrArtisticProperty class. This means the theater lacks a parallel, fully-fledged catalog entry in the main ICCD/ArCo dataset—the very dataset where we found photos, postcards, engravings, and negatives for the Fontana del Nettuno.
Consequently, the absence of images in Query 3 is neither an accident nor a syntax error. It is a direct result of the fact that the required record type (a HistoricOrArtisticProperty linked to a PhotographicDocumentation, as defined in the ArCo denotative description model) simply does not exist for this object within the graph—at least not under the label "Stignani".

## Query 4
Searching for "Stignani" across all resource types in ArCo

This query was designed to find unique resources anywhere in the ArCo knowledge graph — regardless of RDF class — whose label contains the word "Stignani." Unlike Query 4, it drops the restriction to arco:Subject and instead retrieves each matching resource together with its rdf:type. This is useful for understanding how ArCo actually represents the Teatro Stignani — or the person Bruna Stignani, after whom it may be named — within the ontology's class structure, even when the expected classification (Subject) does not contain a match.

Check whether the resource exists under a different class Drop the a arco:Subject restriction entirely and search all labels in the graph: 
sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?resource ?label ?type
WHERE {
  ?resource rdfs:label ?label ;
            a ?type .
  FILTER (CONTAINS(LCASE(STR(?label)), "stignani"))
}
 


Interpretation:
•	The theatre is represented in ArCo  as a CulturalInstituteOrSite — this is the core/primary typing.
•	Around that core entity, ArCo generates a cluster of satellite resources sharing the same internal ID (107917): a CreativeWork record, a Site (physical location instance), an Address, an OpeningHoursSpecification, and a TimeIndexedRole (likely capturing MiBACT's supervisory/competence role over time).
•	This reflects ArCo's general modeling pattern for cultural institutes: rather than one flat record, the entity is decomposed into interlinked sub-resources (site, address, hours, custodianship role, etc.) — quite different from how monument-type resources like fountains might be linked to Subject classifications describing their iconographic or thematic content.

## Query 5 
Using UNION to retrieve multiple naming patterns (Teatro Stignani)
In this query, we explored whether the Teatro Stignani appears in ArCo through different naming patterns. In particular, we wanted to compare the standard name "Teatro comunale Ebe Stignani" with an alternative expression sometimes associated with the venue — for example "Politeama" (a name historically used for many Italian municipal theatres before rededication) or simply "Ebe Stignani" (the name of the soprano the theatre is dedicated to, used without the word "Teatro"). The aim of the query was to retrieve resources that contain either one of these naming patterns. This helps us understand whether the theatre is represented through different labels, alternative names, or related records in the dataset.

sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?resource ?label ?type
WHERE {
  {
    ?resource rdfs:label ?label ;
              a ?type .
    FILTER (CONTAINS(LCASE(STR(?label)), "stignani"))
  }
  UNION
  {
    ?resource rdfs:label ?label ;
              a ?type .
    FILTER (CONTAINS(LCASE(STR(?label)), "politeama"))
  }
}
A couple of notes so you can adapt this before running it:
1.	Swap the alternative term — I used "politeama" as a plausible stand-in for "Gigante" (i.e., a nickname/older name), but I don't have confirmation that this is actually an alternative name used for Teatro Stignani in Imola. If you know the actual alternative/historical name (e.g., an older name the theatre had before being dedicated to Ebe Stignani), substitute it in the second UNION block.
2.	Structure mirrors the fountain query — same two-branch UNION pattern, each branch filtering on one naming variant, so results merge into a single deduplicated table via DISTINCT.
3.	Expected outcome — based on the previous query's results, you'll likely see the "stignani" branch return the same cluster of resources (CulturalInstituteOrSite, Site, Address, etc.), while the alternative-name branch may return nothing — which would itself be a useful negative finding, suggesting (unlike the fountain/"Gigante" case) ArCo does not record a popular alternative name for this theatre, only its official dedicated name.
 
Result:
The UNION query returned exactly the same six resources as the single-keyword "stignani" search — the CreativeWork, CulturalInstituteOrSite, Site, Address, OpeningHoursSpecification, and TimeIndexedRole records tied to ID 107917.
The "politeama" branch of the UNION contributed zero additional resources.
Interpretation:
The Teatro Stignani shows no alternative naming pattern in ArCo. Only the official dedicated name — "Teatro comunale Ebe Stignani" — is used across every associated resource; no historical, colloquial, or nickname variant (like "Politeama") appears anywhere in the dataset.
This is itself a meaningful negative finding for your methodology: it suggests that while some monuments (like the fountain) are documented in ArCo with multiple co-existing naming traditions — reflecting how they're popularly and historically referred to — cultural institute records like the theatre tend to be represented through a single, standardized institutional name only, with no folk or alternate labels captured in the knowledge graph.

##Query 6 
General search for "teatro" entities
After gathering specific data about the Teatro Stignani, we broadened the research by exploring other entities in ArCo whose labels contain the word "teatro." The aim of this query was to compare our selected topic with other theatre-related resources in the ArCo ontology. This broader search can help identify how theatres are generally represented in the dataset and whether there are properties, patterns, or types of information that might be missing from the description of the Teatro Stignani.
Since the word "teatro" can appear in many different contexts, we used LIMIT 50 to avoid producing an excessively large result table.
sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?resource ?label ?type
WHERE {
  ?resource rdfs:label ?label ;
            a ?type .
  FILTER (CONTAINS(LCASE(STR(?label)), "teatro"))
}
LIMIT 50

 
Result:
The general "teatro" search returned a very different picture than expected — instead of surfacing other municipal theatres comparable to Teatro Stignani, the results are dominated by event records (CulturalEvent, OnlineContactPoint, Biglietteria, Prenotazioni) where "teatro" simply appears as a substring inside longer descriptive labels, not as a dedicated theatre entity.
Examples:
•	"L'architettura a Claterna tra domus e teatro" — an educational visit/workshop event, where "teatro" is part of the phrase "domus e teatro" (house and theatre), referring to archaeological remains, not a modern theatre institute.
•	"Una giornata da gladiatore all'Anfiteatro romano di Ancona" — repeated multiple times (42419, 42421, 42424, 42431...) with each occurrence spawning a cluster of four resource types: CulturalEvent, OnlineContactPoint, Biglietteria (ticket office), and Prenotazioni (bookings).
Interpretation:
1.	"Teatro" as a keyword is too broad and context-dependent. Unlike "fontana," which likely points fairly directly to fountain monuments, "teatro" appears heavily in event and cultural-activity labels (guided tours, ticketing, bookings) rather than in institutional site records. This is an important methodological finding: a single-word LIMIT 50 search is dominated by noise from an entirely different resource domain (events tied to archaeological sites) rather than by comparable theatre institutes like Teatro Stignani.
2.	No other CulturalInstituteOrSite theatres appear in the first 50 results. This suggests that theatres as institutional entities (like Teatro Stignani) are comparatively rare in ArCo relative to the volume of event-related records mentioning "teatro" — or that alphabetical/insertion ordering pushed the institute-type results further down, past the LIMIT 50 cutoff.
3.	Data quality observation. The presence of repeated _Copia suffixed duplicates is a useful side-finding for your methodology: it points to redundancy/duplication issues in ArCo's event data that wouldn't have been visible from the targeted Fontana del Nettuno or Teatro Stignani queries alone.

## Query 7 
Refined property inspection for "teatro" (excluding event noise)
The aim of this query was to understand which properties and values are used to describe entities whose labels contain the word "teatro" in the ArCo dataset.
After exploring resources directly related to Teatro Stignani, this query broadened the search. The purpose was to compare the selected topic with other resources containing the term "teatro" and to inspect which RDF properties are used in their descriptions.  To isolate genuine theatre-institute resources from the event/ticketing noise identified above, this refined version restricts the search to resources typed as cis:CulturalInstituteOrSite (or excludes the event-related classes explicitly), before inspecting their properties and values.
sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX cis: <http://dati.beniculturali.it/cis/>

SELECT ?resource ?property ?value
WHERE {
  ?resource a cis:CulturalInstituteOrSite ;
            rdfs:label ?label ;
            ?property ?value .
  FILTER (CONTAINS(LCASE(STR(?label)), "teatro"))
}
LIMIT 100

 
## Result:
Restricting to CulturalInstituteOrSite worked as intended — the noise from CulturalEvent/OnlineContactPoint (ticketing, bookings, contact points) is gone, and the results now consist entirely of genuine institute/site-level records. However, since only rdf:type is shown for every row here, this particular page of results only surfaces the type declaration property (rdf:type → cis:CulturalInstituteOrSite), rather than a variety of descriptive properties — this is simply the first property returned per resource; further rows (beyond what's visible in the screenshot) would likely show other properties like rdfs:label, address, or role-related predicates.
What the resource labels reveal:
The matching resources fall into two distinct groups, confirming the "teatro" ambiguity flagged earlier:
1.	Genuine theatres — e.g. Teatro Comunale (S000352, S003332), Piazza del Grano - Teatro (S000785), Teatro del Corso (S002044), Teatro neoclassico detto Civico (S002667).
2.	False positives from "Anfiteatro" — e.g. Via Appia - Acquetotto dell'Anfiteatro romano (S000257), Anfiteatro romano presso l'Abbazia di S. Paolo (S000258), Resti dell'antico Anfiteatro romano (S000837), and several more Roman amphitheatre remains. These match the substring "teatro" embedded inside "anfiteatro," even though an amphitheatre is architecturally and functionally distinct from a theatre.
Interpretation:
1.	The CulturalInstituteOrSite restriction successfully eliminated the event/ticketing noise seen in Query 6, but it did not eliminate the lexical ambiguity — "teatro" as a substring still pulls in unrelated Roman amphitheatre sites. This is the direct structural counterpart to your Fontana finding: where "fontana" was confused with the surname Fontana (onomastic ambiguity), "teatro" is confused with anfiteatro (compositional/morphological ambiguity — one word contained inside another).
2.	None of these theatres share Teatro Stignani's naming pattern ("[Comune] - Teatro [dedication name]"); instead, most appear under generic descriptive labels ("Teatro Comunale," "Teatro del Corso"), suggesting Teatro Stignani's more elaborate naming (crediting the theatre to soprano Ebe Stignani) is comparatively distinctive within ArCo's dataset — most municipal theatres are recorded more plainly, by function or street name rather than by a dedicatee's name.
3.	Methodological note for your writeup: to get a truly clean set of theatre-only resources, you'd need an additional filter excluding labels containing "anfiteatro" specifically (e.g., FILTER (!CONTAINS(LCASE(STR(?label)), "anfiteatro"))), mirroring how the Fontana query likely needed to exclude surname-pattern matches. Want me to draft that final refined version?
