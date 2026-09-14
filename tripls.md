---
layout: default
---

# Teatro Ebe Stignani

## Enriching Cultural Heritage Knowledge with ArCo and Large Language Models

[View on GitHub](https://github.com/aermosina86-sudo/fontanadelnettuno)

[🏠 Home](index.html) | [🏛️ Topic](topic.html) | [🛠️ Methodology](methodology.html) | [📊 SPARQL & Results](sparql.html) | [🔍 Identifying Gaps](gaps.html) | [💬 LLM Prompts](prompts.html) | 🔗 RDF Triples | [⚠️ Challenges](challenges.html) | [✅ Conclusion](conclusion.html)

---

# Generating New RDF Triples
Generating new RDF triples
1.	No Subject classification. Unlike what might be expected for a well-documented monument, Teatro Stignani has no corresponding entity typed as arco:Subject. This means the theatre is not linked to any semantic/thematic descriptors (e.g., architectural style, historical period, typology such as "teatro all'italiana").
2.	No alternative naming captured. The UNION query testing for a possible historical or colloquial name (e.g., "Politeama") returned no additional matches. 
•	3.  explicit link to the person it is named after. The theatre's name commemorates soprano Ebe Stignani, yet nothing in the retrieved data connects the CulturalInstituteOrSite to an Agent/Person entity representing her. 
4.	No linked creative works, events, or holdings.
I am working on a Knowledge Graph enrichment project about the Fontana del Nettuno in Bologna using the ArCo Knowledge Graph.
My project identified three information gaps:
1.	No Subject classification. Unlike what might be expected for a well-documented monument, Teatro Stignani has no corresponding entity typed as arco:Subject. This means the theatre is not linked to any semantic/thematic descriptors (e.g., architectural style, historical period, typology such as "teatro all'italiana").
2.	No alternative naming captured. The UNION query testing for a possible historical or colloquial name (e.g., "Politeama") returned no additional matches. 
•	3.  explicit link to the person it is named after. The theatre's name commemorates soprano Ebe Stignani, yet nothing in the retrieved data connects the CulturalInstituteOrSite to an Agent/Person entity representing her. 

Please propose RDF triples in Turtle syntax for these three gaps.

Requirements:
1. Separate confirmed information from proposed enrichment.
2. Use ArCo or standard RDF vocabularies where possible.
3. Use valid Turtle syntax.
4. Do not invent unsupported facts.
5. Clearly explain each triple.
6. Also create SPARQL CONSTRUCT queries for the proposed triples.
http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/107917

1. Triple set for Gap
No Subject classification. 

Unlike what might be expected for a well-documented monument, Teatro Stignani has no corresponding entity typed as arco:Subject.

http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_
Claude
Teatro Stignani — Knowledge Graph Enrichment (ArCo)
 <img width="1120" height="441" alt="image" src="https://github.com/user-attachments/assets/357f845b-df38-41a0-9e4e-6e700ea071f5" />

Triple-by-triple explanation:
•	cw:5725_Subject_TeatroStignani a a-cd:Subject — creates the missing Subject individual, using ArCo's own Subject class (context-description module), whose absence is precisely the gap flagged.
•	a-cd:subject "..."@it, "..."@en — ArCo's subject datatype property, carrying the subject as a literal in Italian and English (no verified controlled-vocabulary term exists for this specific building, so a literal is the honest choice rather than a fabricated URI).
•	rdfs:comment — plain-language clarification of what the subject node represents, for human readers of the graph.

SPARQL CONSTRUCT queries for the proposed triples
Query 1 — construct the Subject node and link it to the CIS:
sparql
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/>
PREFIX cis:  <http://dati.beniculturali.it/cis/>
PREFIX cw:   <http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/>
PREFIX res-cis: <http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/>

CONSTRUCT {
  cw:5725_Subject_TeatroStignani
      a a-cd:Subject ;
      a-cd:subject "Teatro comunale Ebe Stignani"@it, "Teatro comunale Ebe Stignani (theatre building)"@en ;
      rdfs:comment "The photographed subject is the Teatro comunale Ebe Stignani in Imola."@en ;
      skos:related res-cis:107917 .

  cw:5725_ a-cd:hasSubject cw:5725_Subject_TeatroStignani .
}
WHERE {
  cw:5725_ a cis:CreativeWork .
  FILTER NOT EXISTS { cw:5725_ a-cd:hasSubject ?anySubject }
}

The result 
 <img width="1249" height="908" alt="image" src="https://github.com/user-attachments/assets/f54bbc2b-aba6-4c55-9c03-c46d5cc7fb4b" />


This query generated 7 RDF statements, so it was successfully executed in the SPARQL endpoint.
Grok triples for the first gap
 <img width="1259" height="505" alt="image" src="https://github.com/user-attachments/assets/75f7c6c8-2c08-41e0-b811-dd526f9411af" />



Explanation of each proposed triple
Triple	Justification
a arco:CulturalProperty	The resource describes a recognised Italian cultural heritage asset (theatre). ArCo’s top-level class for any cultural property.
a arco:TangibleCulturalProperty	The theatre is a physical building.
a arco:ImmovableCulturalProperty	It is a fixed architectural structure (cannot be moved).
rdfs:label "Teatro comunale Ebe Stignani"@it	Standardised Italian preferred label (already partially present, language-tagged for clarity).
dcterms:title "Teatro comunale Ebe Stignani"@it	Dublin Core title, common in cultural-heritage Linked Data.
dcterms:spatial "Imola"	Minimal, non-invented geographic reference already implied by the existing label.
 <img width="1155" height="627" alt="image" src="https://github.com/user-attachments/assets/37296008-3f82-431a-8251-1800ba8aa034" />

The result
 <img width="880" height="536" alt="image" src="https://github.com/user-attachments/assets/2103b022-1920-448c-99c0-12aaddd02ab3" />

This query generated 6 RDF statements, so it was successfully executed in the SPARQL endpoint.


Gap 2 No alternative naming captured.

Claude
The gap description here mixes two things (the heading says "No alternative naming captured," but the body text repeats the old Subject-classification copy). I'll treat alternative naming as the actual gap to fill, since that's the heading and a distinct, genuine gap — the theatre's various documented name-forms aren't captured as skos:altLabels anywhere.
<img width="1078" height="334" alt="image" src="https://github.com/user-attachments/assets/29369bd9-854e-42ed-ac14-20a458a83ed6" />
 
Explanation of each label:
•	"Teatro Ebe Stignani"@it — the form used by the theatre's own digital archive (archivio.teatrostignani.it) and by the IF Imola-Faenza tourism board.
•	"Teatro Stignani"@it — the short colloquial form used repeatedly by the Comune di Imola's own press releases and local press (Bologna24ore).
•	"Teatro Comunale di Imola"@it — the theatre's name before the 1977 dedication to Ebe Stignani, attested in bibliographic references (e.g. "Regolamento pel Teatro Comunale di Imola", 1863; "Teatro Comunale di Imola", 1974) cited in the theatre's own scholarly bibliography.

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX res-cis: <http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/>
PREFIX cw:      <http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/>

CONSTRUCT {
res-cis:107917 skos:altLabel
"Teatro Ebe Stignani"@it ,
"Teatro Stignani"@it ,
"Teatro Comunale di Imola"@it ,
"Imola - Teatro comunale Ebe Stignani"@it .
}
WHERE {
  res-cis:107917 rdfs:label "Teatro comunale Ebe Stignani"@it .
  FILTER NOT EXISTS { res-cis:107917 skos:altLabel ?anyAlt }
}

The result of Claude
 <img width="989" height="527" alt="image" src="https://github.com/user-attachments/assets/f9a7d3d5-cc70-40a0-9be4-be366ba308cc" />


Gap 2 Grok
<img width="1109" height="367" alt="image" src="https://github.com/user-attachments/assets/e80ed1b1-7da5-4240-8f2b-cd2ebebc262d" />
 

Explanation
•	rdf:type cis:CreativeWork — the only type currently asserted.
•	The two rdfs:label values are the only naming information published in the existing RDF.
 <img width="1255" height="523" alt="image" src="https://github.com/user-attachments/assets/452fe210-e9b6-43ee-980b-dd8b50f981c5" />

The result
 <img width="1169" height="783" alt="image" src="https://github.com/user-attachments/assets/559722b3-c1c9-4413-8d48-bb247d07f68a" />


This query generated 7 RDF statements, so it worked successfully.

Gap 3 
3.	explicit link to the person it is named after.
Claude
 <img width="1066" height="491" alt="image" src="https://github.com/user-attachments/assets/c6add7ab-e389-46b5-819a-b8a08e776c14" />

•  wd:Q456908 with rdfs:label, schema:birthDate, schema:deathDate — restates Wikidata's own confirmed identity data for the mezzo-soprano, cross-verified against Carnegie Hall's authority-record aggregation. 
•  owl:sameAs dbr:Ebe_Stignani — the DBpedia alignment, also confirmed by the same cross-reference. 
•  The theatre's label — already-established baseline the new link attaches to.
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wdt:  <http://www.wikidata.org/prop/direct/>
PREFIX wd:   <http://www.wikidata.org/entity/>
PREFIX res-cis: <http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/>

CONSTRUCT {
  res-cis:107917
      wdt:P138 wd:Q456908 ;
      rdfs:comment "Named after mezzo-soprano Ebe Stignani by decision of the Imola town council on 20 December 1977."@en .
}
WHERE {
  res-cis:107917 rdfs:label "Teatro comunale Ebe Stignani"@it .
  FILTER NOT EXISTS { res-cis:107917 wdt:P138 ?anyone }
}
the result
 <img width="974" height="688" alt="image" src="https://github.com/user-attachments/assets/e368f486-ad64-4d63-a258-1ff5229db49b" />

This query generated 2 embedded RDF statements, so it worked successfully

Gap 3 with Grok
 
<img width="1152" height="569" alt="image" src="https://github.com/user-attachments/assets/32dadba3-a990-40e8-827c-c2a0f1848a86" />

Explanation of each proposed triple
Triple	Explanation
schema:namedAfter <http://www.wikidata.org/entity/Q456908>	Explicit statement that the theatre is named after Ebe Stignani (standard Schema.org property for this relation).
dcterms:subject <http://www.wikidata.org/entity/Q456908>	Indicates that the person is a significant subject of the resource.
rdfs:seeAlso <http://www.wikidata.org/entity/Q456908>	Provides a recommended related resource for further information.
a foaf:Person , schema:Person	Types the target entity as a person (minimal safe typing).
rdfs:label "Ebe Stignani"@it / @en	Preferred name of the person in Italian and English.
owl:sameAs <http://www.wikidata.org/entity/Q456908>	Reinforces identity with the canonical Wikidata entity.
 <img width="1328" height="731" alt="image" src="https://github.com/user-attachments/assets/1d5b4e4f-9cd2-4227-9489-f63b13203c3a" />

The result
 <img width="1020" height="919" alt="image" src="https://github.com/user-attachments/assets/8df8393a-3410-451c-a0c6-dd067a834667" />

This query generated 8 embedded RDF statements, so it worked successfully.
