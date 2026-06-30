# Construction de Graphes de Connaissances avec des LLM

> Projet de recherche mené au **LIP6 — Sorbonne Université**, au sein de l’équipe **Bases de Données**.  
> L’objectif est d’explorer l’utilisation des **Large Language Models**, ou **LLM**, pour automatiser la construction de graphes de connaissances à partir de corpus historiques complexes.

---

## Présentation du projet

Un **graphe de connaissances** permet de représenter l’information sous forme d’entités, d’attributs et de relations interconnectées.  
Dans ce projet, les LLM sont utilisés pour transformer des données textuelles historiques en représentations structurées exploitables par des outils de graphes comme **Neo4j**, **RDF** ou **SPARQL**.

Contrairement aux pipelines classiques d’extraction d’information, souvent rigides et fortement dépendants de règles manuelles, cette approche s’appuie sur les capacités génératives et de raisonnement des LLM afin de produire une extraction plus flexible, adaptable et interprétable.

---

## Contexte scientifique

Le stage porte sur les données de **Studium**, un corpus historique couvrant la période du **XIIe au XVIe siècle**.  
Ce corpus regroupe environ **15 000 fiches** décrivant des membres de l’Université de Paris.

Chaque fiche peut contenir des informations variées, par exemple :

- noms et variantes de noms ;
- lieux d’origine ;
- statuts universitaires ;
- fonctions ou titres ;
- dates ;
- relations avec des institutions ou d’autres personnes ;
- événements biographiques.

L’enjeu principal est de transformer ces informations semi-structurées ou textuelles en un graphe de connaissances exploitable pour l’analyse historique.

---

## Objectifs

Le projet vise à construire un pipeline d’extraction et de structuration de connaissances à partir de textes historiques.

Les principaux objectifs sont :

### 1. Extraction flexible des connaissances

Utiliser des techniques de **Prompt Engineering** pour identifier automatiquement :

- les entités ;
- les attributs ;
- les relations ;
- les événements ;
- les informations incertaines ou ambiguës.

Les stratégies étudiées incluent notamment :

- le **Few-Shot Prompting** ;
- le **Chain-of-Thought Reasoning** ;
- l’**auto-réflexion** ;
- la génération de sorties structurées.

### 2. Comparaison de deux approches de structuration

Deux stratégies sont étudiées :

#### Approche guidée par une ontologie

Cette approche s’appuie sur un schéma explicite de type **OWL/RDF** afin de contraindre et normaliser les entités et les relations extraites.

#### Approche sans schéma fixe

Cette approche laisse davantage de liberté au LLM pour proposer les entités et relations pertinentes, puis applique une phase de normalisation, notamment à l’aide de ressources externes comme **DBpedia**.

### 3. Consolidation du graphe

Après extraction, les connaissances doivent être nettoyées, fusionnées et consolidées.

Cette étape inclut :

- la fusion des entités équivalentes ;
- la résolution d’ambiguïtés ;
- la gestion des variantes de noms ;
- l’attribution de scores de confiance ;
- la pondération des relations ;
- la suppression ou correction d’incohérences.

### 4. Exploitation du graphe

Le graphe final est destiné à être exploité avec :

- **Neo4j** pour la visualisation et l’interrogation ;
- **Cypher** pour les requêtes sur graphe ;
- **RDF/SPARQL** pour l’interopérabilité sémantique ;
- des outils existants comme le **Neo4j LLM Knowledge Graph Builder** afin de comparer les résultats obtenus.

---

## Méthodologie

Le pipeline proposé suit plusieurs étapes.

### 1. Prétraitement des données

Les fiches historiques sont préparées avant l’extraction :

- nettoyage du texte ;
- segmentation des fiches ;
- normalisation minimale ;
- identification des champs disponibles ;
- préparation des prompts.

### 2. Extraction des entités

Les LLM sont utilisés pour détecter les principales entités présentes dans les fiches :

- personnes ;
- lieux ;
- institutions ;
- titres ;
- fonctions ;
- diplômes ;
- dates ;
- événements ;
- sources ou références.

Une stratégie d’**auto-réflexion** est utilisée afin d’améliorer la couverture des informations extraites.

### 3. Extraction des relations

Les relations entre les entités sont ensuite identifiées, par exemple :

- une personne est originaire d’un lieu ;
- une personne appartient à une institution ;
- une personne détient un titre ;
- une personne exerce une fonction ;
- un événement est associé à une date ;
- une personne est liée à une autre personne.

Le raisonnement de type **Chain-of-Thought** est étudié pour améliorer la cohérence des relations générées.

### 4. Structuration des résultats

Les sorties du LLM sont transformées en formats exploitables :

- JSON structuré ;
- triplets sujet-prédicat-objet ;
- RDF ;
- nœuds et relations Neo4j.

### 5. Consolidation du graphe

Les entités et relations extraites sont consolidées afin de produire un graphe cohérent :

- détection de doublons ;
- alignement d’entités ;
- normalisation des noms ;
- résolution des ambiguïtés ;
- calcul de scores de confiance.

### 6. Évaluation

La qualité de l’extraction est évaluée à l’aide de métriques classiques :

- **Précision** ;
- **Rappel** ;
- **F1-score**.

Ces métriques permettent de comparer les différentes stratégies de prompt et les différentes approches de structuration.

---

## Architecture générale

```text
Corpus Studium
      |
      v
Prétraitement des fiches
      |
      v
Extraction par LLM
      |
      +--> Entités
      +--> Attributs
      +--> Relations
      |
      v
Structuration
      |
      +--> JSON
      +--> RDF / OWL
      +--> Neo4j
      |
      v
Consolidation du graphe
      |
      v
Évaluation et exploitation
```

---

## Stack technique

### Langage et traitement de données

- Python
- Pandas
- JSON
- Scripts d’intégration API

### IA et NLP

- OpenAI API
- Hugging Face
- Prompt Engineering
- Few-Shot Prompting
- Chain-of-Thought
- Auto-réflexion

### Graphes et Web sémantique

- Neo4j
- Cypher
- RDF
- SPARQL
- OWL

### Normalisation et enrichissement

- DBpedia
- Ontologies OWL
- Alignement d’entités
- Détection de doublons

---

## Visualisations et résultats intermédiaires

### Couverture des clés principales

<img width="989" height="490" alt="Top-level key coverage" src="https://github.com/user-attachments/assets/2ae3b6d5-b06c-4a43-9cbe-09722ee4bdd4" />

---

### Exemple d’extraction corrigée

<img width="536" height="373" alt="nicaulaus_p3_corrige_italie" src="https://github.com/user-attachments/assets/41793a9d-9933-4178-8988-7364328e0b33" />

---

### Exemple de graphe final

<img width="470" height="297" alt="final_p3" src="https://github.com/user-attachments/assets/201f2020-7500-4022-882d-e125f500ff61" />

---

### Visualisation intermédiaire

<img width="503" height="375" alt="p3" src="https://github.com/user-attachments/assets/ad14d580-d445-4916-ae31-05f0c4b4a9a6" />

---

### Exemple de prompt appliqué

<img width="801" height="739" alt="nicaulas_errer_italie_prompt2" src="https://github.com/user-attachments/assets/1b521e68-b54e-4a1a-a7a2-e1d026f8c08a" />

---

## Exemple de sortie attendue

Une sortie simplifiée peut prendre la forme suivante :

```json
{
  "entities": [
    {
      "id": "person_001",
      "type": "Person",
      "label": "Nicolaus",
      "attributes": {
        "origin": "Italie",
        "period": "XVe siècle"
      }
    }
  ],
  "relations": [
    {
      "source": "person_001",
      "target": "place_001",
      "type": "originates_from",
      "confidence": 0.87
    }
  ]
}
```

---

## Exemple de requête Cypher

Une fois les données importées dans Neo4j, il est possible d’interroger le graphe avec Cypher :

```cypher
MATCH (p:Person)-[:ORIGINATES_FROM]->(l:Place)
RETURN p.name, l.name
LIMIT 20;
```

Exemple de requête pour identifier les personnes liées à une même institution :

```cypher
MATCH (p:Person)-[:AFFILIATED_WITH]->(i:Institution)
RETURN i.name, collect(p.name) AS members
ORDER BY size(members) DESC;
```

---

## Structure possible du dépôt

```text
.
├── data/
│   ├── raw/
│   ├── processed/
│   └── examples/
│
├── prompts/
│   ├── entity_extraction.md
│   ├── relation_extraction.md
│   └── self_reflection.md
│
├── src/
│   ├── preprocessing/
│   ├── extraction/
│   ├── normalization/
│   ├── graph_builder/
│   └── evaluation/
│
├── notebooks/
│   └── experiments.ipynb
│
├── results/
│   ├── json/
│   ├── rdf/
│   └── neo4j/
│
├── README.md
└── requirements.txt
```

---

## Installation

Créer un environnement virtuel :

```bash
python -m venv venv
source venv/bin/activate
```

Installer les dépendances :

```bash
pip install -r requirements.txt
```

Configurer les variables d’environnement nécessaires :

```bash
export OPENAI_API_KEY="your_api_key"
```

---

## Utilisation

Exemple d’exécution du pipeline d’extraction :

```bash
python src/extraction/run_extraction.py --input data/raw/sample.json --output results/json/output.json
```

Exemple de construction du graphe Neo4j :

```bash
python src/graph_builder/import_to_neo4j.py --input results/json/output.json
```

---

## Évaluation

Les performances du système sont évaluées selon trois métriques :

| Métrique | Description |
|---|---|
| Précision | Proportion des éléments extraits qui sont corrects |
| Rappel | Proportion des éléments attendus qui ont été extraits |
| F1-score | Moyenne harmonique entre précision et rappel |

L’évaluation peut être réalisée sur :

- les entités extraites ;
- les relations extraites ;
- les triplets générés ;
- la cohérence globale du graphe.

---

## Encadrement

Projet réalisé au **LIP6 — Sorbonne Université**.

Encadrants :

- **Camelia CONSTANTIN** — Équipe Bases de Données
- **Raphaël FOURNIER-S'NIEHOTTA** — Équipe ComplexNetworks

---

## Mots-clés

`Knowledge Graph` · `LLM` · `Neo4j` · `RDF` · `OWL` · `SPARQL` · `Prompt Engineering` · `Historical Data` · `Entity Extraction` · `Relation Extraction`

---

## Statut du projet

Projet réalisé dans le cadre d’un stage de recherche à **Sorbonne Université**.

---

## Licence

À compléter selon les conditions de diffusion du projet et des données Studium.
