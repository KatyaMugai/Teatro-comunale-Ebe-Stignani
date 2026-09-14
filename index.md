---
layout: default
---

# Teatro comunale Ebe Stignani

<img src="images/teatro_stagnani.jpg" alt="Teatro Stagnani" width="600">
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Teatro comunale Ebe Stignani – Home</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
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
    h1 {
      font-size: 1.9em;
      margin-bottom: 8px;
    }
    h2 {
      color: #222;
      margin-top: 35px;
      border-bottom: 2px solid #eee;
      padding-bottom: 6px;
    }
    .subtitle {
      color: #555;
      font-size: 1.15em;
      margin-bottom: 25px;
    }
    ul {
      padding-left: 20px;
    }
    li {
      margin-bottom: 6px;
    }
    .resource {
      background: #f5f5f5;
      padding: 8px 12px;
      border-radius: 4px;
      font-family: monospace;
      word-break: break-all;
      font-size: 0.9em;
    }
  </style>
</head>
<body>

<nav>
  <a href="https://github.com/KatyaMugai/Teatro-comunale-Ebe-Stignani" target="_blank">View on GitHub</a> |
  <a href="index.html"><strong>🏠 Home</strong></a> |
  <a href="topic.html">🏛️ Topic</a> |
  <a href="methodology.html">🛠️ Methodology</a> |
  <a href="sparql.html">📊 SPARQL & Results</a> |
  <a href="gaps.html">🔍 Identifying Gaps</a> |
  <a href="prompts.html">💬 LLM Prompts</a> |
  <a href="triples.html">🔗 RDF Triples</a> |
  <a href="challenges.html">⚠️ Challenges</a> |
  <a href="conclusion.html">✅ Conclusion</a>
</nav>

<h1>Teatro comunale Ebe Stignani</h1>
<p class="subtitle">Enriching Cultural Heritage Knowledge with ArCo and Large Language Models</p>

<p>This project explores and enriches the representation of the <strong>Teatro comunale Ebe Stignani</strong> (Imola, Italy) in the ArCo / MiBACT Knowledge Graph.</p>

<p>Main resource analysed:</p>
<p class="resource">http://dati.beniculturali.it/mibact/luoghi/resource/CreativeWork/5725_</p>

<h2>Project Structure</h2>
<ul>
  <li><strong>Topic</strong> — Description of the theatre and its cultural context</li>
  <li><strong>Methodology</strong> — How the research was conducted</li>
  <li><strong>SPARQL & Results</strong> — Queries used to explore the data</li>
  <li><strong>Identifying Gaps</strong> — The three main information gaps found</li>
  <li><strong>LLM Prompts</strong> — Prompts used with large language models</li>
  <li><strong>RDF Triples</strong> — Proposed enrichment triples in Turtle</li>
  <li><strong>Challenges</strong> — Difficulties encountered during the work</li>
  <li><strong>Conclusion</strong> — Final remarks and outcomes</li>
</ul>

<h2>Identified Gaps (summary)</h2>
<ol>
  <li><strong>No Subject / CulturalProperty classification</strong> — the resource is only typed as <code>cis:CreativeWork</code></li>
  <li><strong>No alternative naming captured</strong> — missing common variants such as “Teatro Stignani” and “lo Stignani”</li>
  <li><strong>No explicit link to the person it is named after</strong> — missing connection to Ebe Stignani (Wikidata Q456908)</li>
</ol>

<p>Use the navigation menu above to explore each section of the project.</p>

<hr>
<p><em>Project by KatyaMugai · September 2026</em></p>

</body>
</html>
## Описание

Здесь напишите текст о театре.

## Автор

Ekaterina Mugaiskikh
