---
layout: default
title: LLM Prompts
---



---

# LLM Prompts

This page documents the prompts used to test Claude and Grok, and compares how each model responded.

## Prompt 1 — Zero-Shot Prompt: Location Ambiguity

This is a zero-shot prompt because the model was asked a direct question without examples or additional instructions. The aim was to test whether the model could recognize that "Teatro Stignani" is a unique, unambiguous name — rather than confusing it with another place, or assuming it needed more context to identify.

> Is there a Teatro Stignani in other cities?

**Claude's answer**
<img width="1220" height="716" alt="Claude answer to Prompt 1" src="https://github.com/user-attachments/assets/16e3d701-ff72-4da3-8fc8-ee278c6e41e3" />

**Grok's answer**
<img width="1289" height="677" alt="Grok answer to Prompt 1" src="https://github.com/user-attachments/assets/362ae15e-d068-4a58-a98b-ac83983de768" />

## Prompt 2 — Zero-Shot Prompt: Biographical Fact Retrieval

Another zero-shot prompt, this time testing whether the model could retrieve a specific historical/biographical fact — the identity of the theatre's namesake and her connection to the city — without being given any supporting context.

> Which opera singer was the theater in Imola named after in 1977, and what is her connection with the city?

**Claude's answer**
<img width="1217" height="661" alt="Claude answer to Prompt 2" src="https://github.com/user-attachments/assets/3f6a2076-d7ef-4caf-9bf1-5a145c368a75" />

**Grok's answer**
<img width="1474" height="744" alt="Grok answer to Prompt 2" src="https://github.com/user-attachments/assets/b7b21a3b-f55a-4a24-ba9e-140c92e4ff40" />

## Prompt 3 — Entity Classification

> Identify whether these are names of theaters or names of people. For example:
> Teatro Stignani is a theater
> Ebe Stignani is a name

**Claude's answer**
<img width="1358" height="398" alt="Claude answer to the classification prompt" src="https://github.com/user-attachments/assets/3e731dec-9403-4887-a4a8-d8cfb42825fa" />

**Grok's answer**
<img width="1327" height="492" alt="Grok answer to the classification prompt" src="https://github.com/user-attachments/assets/eed42adc-5078-45db-b36e-ee65189c3ce0" />

## Prompt 4 — Chain-of-Thought: Cultural Description of the Monument

> Analyze the Teatro Stignani in Imola by following these steps:
>
> 1. Describe accurately what can be observed in the building: its location, architectural style, façade, interior layout (auditorium, boxes, stage), materials, decorative elements, and urban setting.
> 2. Explain the symbolic meaning of the main elements: the choice to name the theater after Ebe Stignani, the theater's role as a civic and cultural space, its position within the city, and the relationship between the building and local identity or civic pride.
> 3. Interpret the cultural significance of the theater: what does it represent for Imola? Why is it considered an important cultural landmark in the city?
> 4. Place the theater in its historical and artistic context: when was it built or renovated, who was involved in its design and construction, and what was the political, social, or urban context of Imola at that time?
> 5. Summarize the main cultural or art-historical interpretations of the theater: for example, its role as a symbol of civic culture, its connection to Italian provincial theater architecture, and its relationship to the representation of local identity and the performing arts tradition.
> 6. Compare the Teatro Stignani briefly with other Italian provincial theaters named after opera singers or performers, noting similarities and differences in function, architecture, or civic role.

**Claude's answer**
<img width="1077" height="827" alt="Claude chain-of-thought answer" src="https://github.com/user-attachments/assets/0fdce6a1-1b56-4640-8108-f22fcc552365" />

**Grok's answer**
<img width="1538" height="1130" alt="Grok chain-of-thought answer" src="https://github.com/user-attachments/assets/619fdd59-936c-43de-91d1-5f20c4212d5d" />

## Considerations

The chain-of-thought prompt produced the most useful results for cultural enrichment.

### Comparison Overview

| Feature | Claude | Grok |
|---|---|---|
| **Structure & Length** | Formal typography, narrative focus (~260 words) | Standard layout, fact-heavy and concise (~230 words) |
| **Architectural Detail** | Highlights specific interior geometry (17 boxes per tier across 3 tiers, stage openings) | Highlights modern updates (glass-and-steel addition, total seat count of 468) |
| **Historical Nuance** | Focuses on social history (excommunication threats, box sales by local notables) | Focuses on institutional timeline (original name Teatro dei Signori Associati, Felice Giani, modern restorations) |
| **Comparative Basis** | Compares to theatres named after native composers (e.g., Rossini in Pesaro, Bellini in Catania) | Compares to theaters named after opera singers (e.g., Pavarotti-Freni in Modena, Mario Del Monaco in Treviso) |

**Claude** focuses on artistic and historical storytelling: it details architectural nuances (17 boxes per tier, stage openings), colourful historical events (threats of excommunication, local box sales), specific famous actors (Gassman, Melato), and contrasts the theatre with others named after native composers (Rossini, Bellini).

**Grok** focuses on practical and institutional facts: it provides precise data (street address, 468-seat capacity, 2005–2010 glass-and-steel addition), historical names (Teatro dei Signori Associati), and compares it to other theaters named after singers (Pavarotti, Del Monaco).

### General Considerations

The LLM prompting phase showed that Claude and Grok can both be useful tools for cultural heritage enrichment, but their outputs cannot be used automatically — each proposes different facts, emphases, and vocabulary choices, so human review remains essential before anything is added to the knowledge graph.
