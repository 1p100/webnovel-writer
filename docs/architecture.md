# System Architecture and Module Design

## Core Concepts

### Three Laws of Anti-Hallucination

| Law | Explanation | Implementation Method |

|------|------|---------|

| **Outline is the Law** | Follow the outline, do not arbitrarily change it | Context Agent forces loading of chapter outlines |

| **Settings are Physics** | Abide by the settings, do not contradict yourself | Consistency Checker real-time verification |

| **Inventions Must Be Identified** | New entities must be managed in the database | Data Agent automatically extracts and disambiguates |

### Strand Weave Rhythm System

| Strand | Meaning | Ideal Proportion | Explanation |

|--------|------|----------|------|

| **Quest** | Main Storyline | 60% | Drives the Core Conflict |

| **Fire** | Romance | 20% | Character Relationship Development |

| **Constellation** | Worldview Expansion | 20% | Background/Faction/Setting |

Pace Red Lines:

- Quest: No more than 5 consecutive chapters

- Fire: No more than 10 chapter gaps

- Constellation: No more than 15 chapter gaps

## Overall Architecture Diagram

```text

┌───────────────────────────────────────────────────────┐

│ Claude Code │

├─────────────────────────────────────────────────────────┤

│ Skills (7): init / plan / write / review / query / ... │

├───────────────────────────────────────────────────────────┤

│ Agents (8): Context / Data / Multidimensional Checker │

├───────────────────────────────────────────────────────┤

│ Data Layer: state.json / index.db / vectors.db │

└───────────────────────────────────────────────────────┘

```

## Dual Agent Architecture

### Context Agent (Read)

Responsibility: Builds the "creation task book" before writing, providing the chapter's context, constraints, and follow-up strategies.

### Data Agent (Write)

Responsibility: Extracts entities and state changes from the main text, updates `state.json`, `index.db`, ​​and `vectors.db`, ​​ensuring a closed data chain.


## Six-Dimensional Parallel Review

| Checker | Key Check Points |

|---------|---------|

| High-point Checker | Highlights and Quality |

| Consistency Checker | Consistency of Setting (Power/Location/Timeline) |

| Pacing Checker | Strand Ratio and Gaps |

| OOC Checker | Does Character Behavior Deviate from Character Design? |

| Continuity Checker | Scene and Narrative Coherence |

| Reader-pull Checker | Hook Strength, Expectation Management, Reading Comprehension |
