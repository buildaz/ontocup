# OntoCup

OWL ontology for the FIFA World Cup domain, developed for experimental purposes.

**IRI:** `http://www.buildaz.io/ontocup/`

**Author:** Lívia Nascimento  
**Contributors:** Rafaela Moos, João Couto

---

## Overview

OntoCup formally represents entities, events, and relations in the FIFA World Cup universe: competitions, national teams, matches, players, referees, locations, and game events.

The model is grounded in **Basic Formal Ontology (BFO 2020)** and the **Information Artifact Ontology (IAO)**, ensuring logical consistency and alignment with established ontological standards. All terms are annotated in both Portuguese and English.

---

## Files

| File | Description |
|---|---|
| `ontocup.ttl` | Main version — imports BFO and IAO via `owl:imports` |
| `ontocup-standalone.ttl` | Standalone version — BFO and IAO inlined, no external dependencies |

Use `ontocup-standalone.ttl` when the environment has no internet access or when you want to avoid resolving external imports (e.g., offline Protégé, Ontop).

---

## Ontology Structure

### Agents and Roles (BFO:0000023)

| Class | Label | Description |
|---|---|---|
| `jogador` | Player | Role assumed by a person called up to a team |
| `técnico` | Coach | Responsible for the technical and tactical management of the team |
| `árbitro` | Referee | Designated to oversee rule compliance during a match |
| `goleiro` | Goalkeeper | Player who defends the goal |
| `atacante` | Forward | Player who creates and converts goal-scoring opportunities |
| `meia` | Midfielder | Links defense and attack |
| `zagueiro` | Centre back | Protects the defensive area |

### Organizations and Teams (Object Aggregate — BFO:0000027)

| Class | Label | Description |
|---|---|---|
| `organização` | Organization | General class for institutional entities in football |
| `clube` | Club | Legal structure with formal ties to federations |
| `seleção_nacional` | National selection | Institutional entity representing a country |
| `time` | Team | Aggregate of persons in the role of players |
| `seleção_-_time` | National team | Team whose members share the same nationality |

### Locations (Site — BFO:0000029)

| Class | Label | Description |
|---|---|---|
| `continente` | Continent | Major territorial division of the Earth's surface |
| `país` | Country | Sovereign nation, located within a continent |
| `estado` | State | Territorial division of a country |
| `cidade` | City | Urban territorial unit, located within a state |
| `estádio` | Stadium | Physical structure where matches are held |
| `país_sede` | Host country | Role assumed by a country hosting the World Cup |
| `cidade_sede` | Host city | Role assumed by a city hosting official matches |

### Processes (BFO:0000015)

| Class | Label | Description |
|---|---|---|
| `partida` | Match | Two teams compete against each other in a stadium on a given date |
| `marcar_gol` | Score a goal | Player drives the ball into the opposing goal |
| `marcar_cartão` | Issue card | Referee applies a disciplinary penalty |
| `marcar_falta` | Commit foul | Player commits an infraction of the rules |
| `fazer_substituição` | Make substitution | A player is replaced by a substitute |

### Information Entities (Data Item — IAO:0000027)

| Class | Label | Description |
|---|---|---|
| `gol` | Goal | Record of a goal occurrence in a match |
| `cartão` | Card | Record of a disciplinary penalty applied |
| `falta` | Foul | Record of a rule infraction |
| `substituição` | Substitution | Record of a player exchange |
| `placar` | Score | Goal count for each team in a match |
| `resultado` | Result | Final outcome of a match |
| `temporada` | Season | A specific edition of the World Cup |

### Other Classes

| Class | Label | Description |
|---|---|---|
| `pessoa` | Person | Entity that endures through time; can assume roles |
| `nacionalidade` | Nationality | Quality that determines eligibility to represent a national team |

---

## Object Properties

| Property | Label | Domain → Range |
|---|---|---|
| `acontece_em` | occurs in | Sporting process → Stadium |
| `assistido_por` | assisted by | Goal → Player |
| `dirige` | manages | Coach → Team |
| `empatante` | drawing team | Result → National team |
| `has_member_part` | has member part | Team/Selection → Person |
| `marcado_por` | marked by | Goal/Foul/Card → Agent |
| `participante` | participant | Score/Result → National team |
| `perdedor` | loser | Result → National team |
| `recebido_por` | received by | Card → Player |
| `registrado_em` | registered in | Information entity → Match |
| `sediado` | hosted in | Season → Country |
| `selecao_mandante` | home team | Score/Result → National team |
| `selecao_visitante` | away team | Score/Result → National team |
| `sofrido_por` | suffered by | Foul → Player |
| `tem_nacionalidade` | has nationality | Person → Nationality |
| `tem_posição` | has position | Player → Positional role |
| `vencedor` | winner | Result → National team |

---

## SWRL Rules

**S5** — Validates that all members of a `seleção_-_time` share the same nationality as the team they represent:

```
seleção_-_time(?s) ∧ has_member_part(?s, ?p) ∧ pessoa(?p) ∧ tem_nacionalidade(?s, ?n)
  → tem_nacionalidade(?p, ?n)
```

---

## Usage

### Loading in Protégé

1. Open Protégé
2. `File → Open` → select `ontocup.ttl` (requires internet to resolve imports) **or** `ontocup-standalone.ttl` (no external dependencies)

### Using with Ontop (SPARQL over relational DB)

Use `ontocup-standalone.ttl` to avoid import resolution issues in Ontop environments. Set it as the base ontology in your Ontop mapping configuration.

---

## Namespaces

```turtle
@prefix :    <http://www.buildaz.io/ontocup/> .
@prefix bfo: <http://purl.obolibrary.org/obo/BFO_> .
@prefix iao: <http://purl.obolibrary.org/obo/IAO_> .
@prefix ro:  <http://purl.obolibrary.org/obo/RO_> .
```

---

Developed by [Buildaz](https://www.buildaz.io).