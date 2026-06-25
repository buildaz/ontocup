# OntoCup

Ontologia OWL para o domínio da Copa do Mundo de Futebol (FIFA World Cup), desenvolvida para fins experimentais e de apoio a ações de marketing.

**IRI:** `http://www.buildaz.io/ontocup/`

**Autoria:** Lívia Nascimento  
**Contribuições:** Rafaela Moos, João Couto

---

## Visão Geral

O OntoCup representa formalmente entidades, eventos e relações do universo da Copa do Mundo: competições, seleções nacionais, partidas, jogadores, árbitros, localizações e eventos de jogo.

O modelo é fundamentado na **Basic Formal Ontology (BFO 2020)** e no **Information Artifact Ontology (IAO)**, garantindo consistência lógica e alinhamento com padrões ontológicos estabelecidos. Todos os termos são anotados em português e inglês.

---

## Arquivos

| Arquivo | Descrição |
|---|---|
| `ontocup.ttl` | Versão principal — importa BFO e IAO via `owl:imports` |
| `ontocup-v2-standalone.ttl` | Versão standalone — BFO e IAO embutidos inline, sem dependências externas |

Use `ontocup-v2-standalone.ttl` quando o ambiente não tiver acesso à internet ou quando quiser evitar a resolução de imports externos (ex.: Protégé offline, Ontop).

---

## Estrutura da Ontologia

### Agentes e Papéis (Roles — BFO:0000023)

| Classe | Label EN | Descrição |
|---|---|---|
| `jogador` | Player | Papel assumido por uma pessoa convocada para um time |
| `técnico` | Coach | Responsável pela direção técnica e tática do time |
| `árbitro` | Referee | Designado para fiscalizar as regras durante uma partida |
| `goleiro` | Goalkeeper | Jogador que defende a baliza |
| `atacante` | Forward | Jogador que cria e converte oportunidades de gol |
| `meia` | Midfielder | Faz a ligação entre defesa e ataque |
| `zagueiro` | Centre back | Protege a área defensiva |

### Organizações e Times (Object Aggregate — BFO:0000027)

| Classe | Label EN | Descrição |
|---|---|---|
| `organização` | Organization | Classe geral para entidades institucionais do futebol |
| `clube` | Club | Estrutura jurídica com vínculo formal a federações |
| `seleção_nacional` | National selection | Entidade institucional que representa um país |
| `time` | Team | Agregado de pessoas no papel de jogador |
| `seleção_-_time` | National team | Time cujos membros compartilham a mesma nacionalidade |

### Localizações (Site — BFO:0000029)

| Classe | Label EN | Descrição |
|---|---|---|
| `continente` | Continent | Grande divisão territorial da superfície terrestre |
| `país` | Country | Nação soberana, localizada em um continente |
| `estado` | State | Divisão territorial de um país |
| `cidade` | City | Unidade territorial urbana, localizada em um estado |
| `estádio` | Stadium | Estrutura física onde as partidas são realizadas |
| `país_sede` | Host country | Papel assumido por um país que sedia a Copa |
| `cidade_sede` | Host city | Papel assumido por uma cidade que hospeda partidas |

### Processos (Process — BFO:0000015)

| Classe | Label EN | Descrição |
|---|---|---|
| `partida` | Match | Dois times se enfrentam em um estádio em data determinada |
| `marcar_gol` | Score a goal | Jogador introduz a bola na baliza adversária |
| `marcar_cartão` | Issue card | Árbitro aplica penalidade disciplinar |
| `marcar_falta` | Commit foul | Jogador comete infração às regras |
| `fazer_substituição` | Make substitution | Um jogador é trocado por um reserva |

### Entidades Informacionais (Data Item — IAO:0000027)

| Classe | Label EN | Descrição |
|---|---|---|
| `gol` | Goal | Registro da ocorrência de um gol em uma partida |
| `cartão` | Card | Registro da aplicação de penalidade disciplinar |
| `falta` | Foul | Registro de infração às regras do jogo |
| `substituição` | Substitution | Registro da troca de jogadores |
| `placar` | Score | Contagem de gols de cada time na partida |
| `resultado` | Result | Desfecho final de uma partida |
| `temporada` | Season | Edição específica da Copa do Mundo |

### Outras Classes

| Classe | Label EN | Descrição |
|---|---|---|
| `pessoa` | Person | Entidade que persiste no tempo; pode assumir papéis |
| `nacionalidade` | Nationality | Qualidade que determina elegibilidade para representar uma seleção |

---

## Propriedades de Objeto (Object Properties)

| Propriedade | Label EN | Domínio → Range |
|---|---|---|
| `acontece_em` | occurs in | Processo esportivo → Estádio |
| `assistido_por` | assisted by | Gol → Jogador |
| `dirige` | manages | Técnico → Time |
| `empatante` | drawing team | Resultado → Seleção-time |
| `has_member_part` | has member part | Time/Seleção → Pessoa |
| `marcado_por` | marked by | Gol/Falta/Cartão → Agente |
| `participante` | participant | Placar/Resultado → Seleção-time |
| `perdedor` | loser | Resultado → Seleção-time |
| `recebido_por` | received by | Cartão → Jogador |
| `registrado_em` | registered in | Entidade informacional → Partida |
| `sediado` | hosted in | Temporada → País |
| `selecao_mandante` | home team | Placar/Resultado → Seleção-time |
| `selecao_visitante` | away team | Placar/Resultado → Seleção-time |
| `sofrido_por` | suffered by | Falta → Jogador |
| `tem_nacionalidade` | has nationality | Pessoa → Nacionalidade |
| `tem_posição` | has position | Jogador → Papel de posição |
| `vencedor` | winner | Resultado → Seleção-time |

---

## Regras SWRL

**S5** — Valida que todos os membros de uma `seleção_-_time` compartilham a mesma nacionalidade que a seleção:

```
seleção_-_time(?s) ∧ has_member_part(?s, ?p) ∧ pessoa(?p) ∧ tem_nacionalidade(?s, ?n)
  → tem_nacionalidade(?p, ?n)
```

---

## Como usar

### Carregar no Protégé

1. Abra o Protégé
2. `File → Open` → selecione `ontocup.ttl` (requer internet para resolver imports) **ou** `ontocup-v2-standalone.ttl` (sem dependências externas)

### Usar com Ontop (SPARQL over relational DB)

Recomenda-se `ontocup-v2-standalone.ttl` para evitar problemas de resolução de imports em ambientes Ontop. Configure o arquivo como a ontologia base no mapping do Ontop.

---

## Namespaces

```turtle
@prefix :    <http://www.buildaz.io/ontocup/> .
@prefix bfo: <http://purl.obolibrary.org/obo/BFO_> .
@prefix iao: <http://purl.obolibrary.org/obo/IAO_> .
@prefix ro:  <http://purl.obolibrary.org/obo/RO_> .
```

---

## Licença

Desenvolvido por [Buildaz](https://www.buildaz.io). Para uso interno e experimental.