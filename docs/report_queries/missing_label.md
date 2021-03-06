# Missing Label

Problem: An entity does not have a label. This may cause confusion or misuse.

Solution: Add a label.

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?entity ?property ?value
WHERE {
 ?entity ?any ?o .
 BIND ("rdfs:label" AS ?property) .
 FILTER NOT EXISTS {?entity rdfs:label ?value}
 FILTER NOT EXISTS {?entity a owl:Ontology}
 FILTER NOT EXISTS {
   ?entity owl:deprecated ?dep .
   FILTER regex(str(?dep), "true")
 }
 FILTER (!isBlank(?entity))
}
```
