<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Teatro Stignani – RDF Triples</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 950px;
      margin: 40px auto;
      line-height: 1.6;
      padding: 0 20px;
      color: #333;
    }
    nav {
      background: #f0f0f0;
      padding: 12px 15px;
      margin-bottom: 30px;
      border-radius: 6px;
      font-size: 15px;
    }
    nav a {
      margin-right: 8px;
      text-decoration: none;
      color: #1a73e8;
    }
    nav a:hover {
      text-decoration: underline;
    }
    h1 { font-size: 1.8em; margin-bottom: 10px; }
    h2 {
      color: #222;
      margin-top: 45px;
      border-bottom: 2px solid #eee;
      padding-bottom: 6px;
    }
    h3 { margin-top: 25px; color: #444; }
    pre {
      background: #f8f8f8;
      padding: 15px;
      overflow-x: auto;
      border-radius: 5px;
      font-size: 0.88em;
      line-height: 1.45;
    }
    hr {
      margin: 40px 0;
      border: none;
      border-top: 1px solid #ddd;
    }
    .resource {
      background: #f5f5f5;
      padding: 8px 12px;
      border-radius: 4px;
      font-family: monospace;
      word-break: break-all;
      font-size: 0.9em;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 15px 0;
      font-size: 0.92em;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px 10px;
      text-align: left;
      vertical-align: top;
    }
    th { background: #f0f0f0; }
  </style>
</head>
<body>

<nav>
  <a href="https://github.com/KatyaMugai/Teatro-comunale-Ebe-Stignani" target="_blank">View on GitHub</a> |
  <a href="index.html">🏠 Home</a> |
  <a href="topic.html">🏛️ Topic</a> |
  <a href="methodology.html">🛠️ Methodology</a> |
  <a href="sparql.html">📊 SPARQL & Results</a> |
  <a href="gaps.html">🔍 Identifying Gaps</a> |
  <a href="prompts.html">💬 LLM Prompts</a> |
  <a href="triples.html"><strong>🔗 RDF Triples</strong></a> |
  <a href="challenges.html">⚠️ Challenges</a> |
  <a href="conclusion.html">✅ Conclusion</a>
</nav>

<h1>RDF Triples — Proposed Enrichment</h1>

<p>This page presents the RDF triples proposed to fill the three identified gaps for the resource:</p>
<p class="resource">http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_</p>
<p>(also related to <code>CulturalInstituteOrSite/107917</code>)</p>

<hr>

<!-- ==================== GAP 1 ==================== -->
<h2>Gap 1 — No Subject / CulturalProperty classification</h2>

<p>Unlike what might be expected for a well-documented monument, the Teatro Stignani has no corresponding entity typed as <code>arco:CulturalProperty</code> or <code>arco:Subject</code>.</p>

<h3>Confirmed information</h3>
<pre>@prefix cis:  &lt;http://dati.beniculturali.it/cis/&gt; .
@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .

&lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
  a cis:CreativeWork ;
  rdfs:label "Imola - Teatro comunale Ebe Stignani" ;
  rdfs:label "Teatro comunale Ebe Stignani" .</pre>

<h3>Proposed enrichment (Turtle)</h3>
<pre>@prefix arco:    &lt;https://w3id.org/arco/ontology/arco/&gt; .
@prefix rdfs:    &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix dcterms: &lt;http://purl.org/dc/terms/&gt; .

&lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
  a arco:CulturalProperty ,
    arco:TangibleCulturalProperty ,
    arco:ImmovableCulturalProperty ;
  rdfs:label "Teatro comunale Ebe Stignani"@it ;
  dcterms:title "Teatro comunale Ebe Stignani"@it ;
  dcterms:spatial "Imola" .</pre>

<h3>Explanation of each triple</h3>
<table>
  <tr>
    <th>Triple</th>
    <th>Justification</th>
  </tr>
  <tr>
    <td><code>a arco:CulturalProperty</code></td>
    <td>The resource describes a recognised Italian cultural heritage asset (theatre). ArCo’s top-level class for any cultural property.</td>
  </tr>
  <tr>
    <td><code>a arco:TangibleCulturalProperty</code></td>
    <td>The theatre is a physical building.</td>
  </tr>
  <tr>
    <td><code>a arco:ImmovableCulturalProperty</code></td>
    <td>It is a fixed architectural structure (cannot be moved).</td>
  </tr>
  <tr>
    <td><code>rdfs:label "Teatro comunale Ebe Stignani"@it</code></td>
    <td>Standardised Italian preferred label (language-tagged).</td>
  </tr>
  <tr>
    <td><code>dcterms:title "Teatro comunale Ebe Stignani"@it</code></td>
    <td>Dublin Core title, common in cultural-heritage Linked Data.</td>
  </tr>
  <tr>
    <td><code>dcterms:spatial "Imola"</code></td>
    <td>Minimal geographic reference already implied by the existing label.</td>
  </tr>
</table>

<h3>SPARQL CONSTRUCT</h3>
<pre>PREFIX arco:    &lt;https://w3id.org/arco/ontology/arco/&gt;
PREFIX rdfs:    &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX dcterms: &lt;http://purl.org/dc/terms/&gt;

CONSTRUCT {
  &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
    a arco:CulturalProperty ,
      arco:TangibleCulturalProperty ,
      arco:ImmovableCulturalProperty ;
    rdfs:label "Teatro comunale Ebe Stignani"@it ;
    dcterms:title "Teatro comunale Ebe Stignani"@it ;
    dcterms:spatial "Imola" .
}
WHERE {
  &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt; a ?type .
  FILTER NOT EXISTS {
    &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt; a arco:CulturalProperty
  }
}</pre>

<hr>

<!-- ==================== GAP 2 ==================== -->
<h2>Gap 2 — No alternative naming captured</h2>

<p>The resource currently contains only two almost identical labels. No alternative or variant names are recorded.</p>

<h3>Confirmed information</h3>
<pre>rdfs:label "Imola - Teatro comunale Ebe Stignani" ;
rdfs:label "Teatro comunale Ebe Stignani" .</pre>

<h3>Proposed enrichment (Turtle)</h3>
<pre>@prefix skos:    &lt;http://www.w3.org/2004/02/skos/core#&gt; .
@prefix rdfs:    &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix dcterms: &lt;http://purl.org/dc/terms/&gt; .

&lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
  rdfs:label "Teatro comunale Ebe Stignani"@it ;
  rdfs:label "Teatro Ebe Stignani"@it ;
  rdfs:label "Teatro Stignani"@it ;
  skos:altLabel "Teatro Stignani"@it ;
  skos:altLabel "lo Stignani"@it ;
  skos:altLabel "Teatro Comunale di Imola"@it ;
  dcterms:title "Teatro comunale Ebe Stignani"@it ;
  dcterms:alternative "Teatro Stignani"@it .</pre>

<h3>Explanation of the labels</h3>
<ul>
  <li><strong>"Teatro Ebe Stignani"</strong> — common official short form</li>
  <li><strong>"Teatro Stignani"</strong> — most frequent public and press name</li>
  <li><strong>"lo Stignani"</strong> — local colloquial designation</li>
  <li><strong>"Teatro Comunale di Imola"</strong> — historical name before the 1977 dedication</li>
</ul>

<h3>SPARQL CONSTRUCT</h3>
<pre>PREFIX rdfs:    &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX skos:    &lt;http://www.w3.org/2004/02/skos/core#&gt;
PREFIX dcterms: &lt;http://purl.org/dc/terms/&gt;

CONSTRUCT {
  &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
    rdfs:label "Teatro comunale Ebe Stignani"@it ;
    rdfs:label "Teatro Ebe Stignani"@it ;
    rdfs:label "Teatro Stignani"@it ;
    skos:altLabel "Teatro Stignani"@it ;
    skos:altLabel "lo Stignani"@it ;
    skos:altLabel "Teatro Comunale di Imola"@it ;
    dcterms:title "Teatro comunale Ebe Stignani"@it ;
    dcterms:alternative "Teatro Stignani"@it .
}
WHERE {
  &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt; ?p ?o .
}</pre>

<hr>

<!-- ==================== GAP 3 ==================== -->
<h2>Gap 3 — Explicit link to the person it is named after</h2>

<p>The theatre was officially named after the mezzo-soprano <strong>Ebe Stignani</strong> in 1977, yet nothing in the retrieved data connects the resource to an Agent/Person entity representing her.</p>

<h3>Proposed enrichment (Turtle)</h3>
<pre>@prefix schema:  &lt;http://schema.org/&gt; .
@prefix rdfs:    &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix foaf:    &lt;http://xmlns.com/foaf/0.1/&gt; .
@prefix owl:     &lt;http://www.w3.org/2002/07/owl#&gt; .
@prefix dcterms: &lt;http://purl.org/dc/terms/&gt; .

&lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
  schema:namedAfter &lt;http://www.wikidata.org/entity/Q456908&gt; ;
  dcterms:subject &lt;http://www.wikidata.org/entity/Q456908&gt; ;
  rdfs:seeAlso &lt;http://www.wikidata.org/entity/Q456908&gt; .

&lt;http://www.wikidata.org/entity/Q456908&gt;
  a foaf:Person , schema:Person ;
  rdfs:label "Ebe Stignani"@it ;
  rdfs:label "Ebe Stignani"@en ;
  owl:sameAs &lt;http://www.wikidata.org/entity/Q456908&gt; .</pre>

<h3>Explanation of each triple</h3>
<table>
  <tr>
    <th>Triple</th>
    <th>Explanation</th>
  </tr>
  <tr>
    <td><code>schema:namedAfter &lt;...Q456908&gt;</code></td>
    <td>Explicit statement that the theatre is named after Ebe Stignani (standard Schema.org property).</td>
  </tr>
  <tr>
    <td><code>dcterms:subject &lt;...Q456908&gt;</code></td>
    <td>Indicates that the person is a significant subject of the resource.</td>
  </tr>
  <tr>
    <td><code>rdfs:seeAlso &lt;...Q456908&gt;</code></td>
    <td>Provides a recommended related resource for further information.</td>
  </tr>
  <tr>
    <td><code>a foaf:Person , schema:Person</code></td>
    <td>Types the target entity as a person.</td>
  </tr>
  <tr>
    <td><code>rdfs:label "Ebe Stignani"@it / @en</code></td>
    <td>Preferred name of the person in Italian and English.</td>
  </tr>
  <tr>
    <td><code>owl:sameAs &lt;...Q456908&gt;</code></td>
    <td>Reinforces identity with the canonical Wikidata entity.</td>
  </tr>
</table>

<h3>SPARQL CONSTRUCT</h3>
<pre>PREFIX schema:  &lt;http://schema.org/&gt;
PREFIX rdfs:    &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX foaf:    &lt;http://xmlns.com/foaf/0.1/&gt;
PREFIX owl:     &lt;http://www.w3.org/2002/07/owl#&gt;
PREFIX dcterms: &lt;http://purl.org/dc/terms/&gt;

CONSTRUCT {
  &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt;
    schema:namedAfter &lt;http://www.wikidata.org/entity/Q456908&gt; ;
    dcterms:subject &lt;http://www.wikidata.org/entity/Q456908&gt; ;
    rdfs:seeAlso &lt;http://www.wikidata.org/entity/Q456908&gt; .

  &lt;http://www.wikidata.org/entity/Q456908&gt;
    a foaf:Person , schema:Person ;
    rdfs:label "Ebe Stignani"@it ;
    rdfs:label "Ebe Stignani"@en ;
    owl:sameAs &lt;http://www.wikidata.org/entity/Q456908&gt; .
}
WHERE {
  &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt; ?p ?o .
  FILTER NOT EXISTS {
    &lt;http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_&gt; schema:namedAfter ?person
  }
}</pre>

<hr>

<p><em>Last updated: September 2026</em></p>

</body>
</html>
