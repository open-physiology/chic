## queries in vsd meta onto

### list the genders with abbreviation and label

```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX vsd: <http://www.virtualskeleton.ch/vsd#>

SELECT DISTINCT ?uri ?label ?abbr

FROM <http://www.virtualskeleton.ch/data/vsd>

WHERE {
?uri <http://www.w3.org/2000/01/rdf-schema#subClassOf> <http://purl.obolibrary.org/obo/PATO_0000047> .
?uri <http://www.w3.org/2000/01/rdf-schema#label>   ?label .
?uri vsd:abbreviation ?abbr .
}

LIMIT 100
```

### and the modalities

```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX vsd: <http://www.virtualskeleton.ch/vsd#>

SELECT DISTINCT ?uri ?label ?abbr

FROM <http://www.virtualskeleton.ch/data/vsd>

WHERE {
?uri <http://www.w3.org/2000/01/rdf-schema#subClassOf> vsd:mr-sequence-acronym .
?uri <http://www.w3.org/2000/01/rdf-schema#label>   ?label .
?uri vsd:abbreviation ?abbr .
}
```

### list the properties of a class

```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX vsd: <http://www.virtualskeleton.ch/vsd#>

SELECT DISTINCT ?p ?label 

FROM <http://www.virtualskeleton.ch/data/vsd>

WHERE {
vsd:mr-sequence-acronym ?p ?label
}
```

### PRefix list

```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX miaf: <http://www.virtualskeleton.ch/MIAF#>
PREFIX uberon: <http://purl.obolibrary.org/obo/uberon/core#>
PREFIX odrl: <http://www.w3.org/ns/odrl/2/>
PREFIX mrda: <http://neurolog.unice.fr/ontoneurolog/v3.0/ontoneurolog-mr-dataset-acquisition.owl#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
```


### all entries with type and class and uri

```

SELECT DISTINCT *
WHERE {
?individual rdf:type ?type .
OPTIONAL { ?type rdfs:subClassOf ?class }
}
ORDER BY ?class

```

### instances of a class with abbreviation: get all license indstance

```

SELECT DISTINCT ?uri ?abbr

WHERE {

?uri rdf:type odrl:Policy .
?uri uberon:ABBREVIATION ?abbr

}

ORDER BY ?abbr
```

#### Other properties for
- Handedness: `<http://purl.bioontology.org/ontology/SNOMEDCT/57427004>`
- Gender: `obo:PATO_0000047`
- License: `odrl:Policy`
- MR contrast: `mrda:MR-image-contrast`
- segmentation method: `miaf:00000347`
- ethnic group: `obo:ERO_0001972`

### Subclasses with abbreviations: get all mr-sequence acronyms

```
SELECT DISTINCT ?uri ?abbr
WHERE {

?class rdfs:subClassOf* miaf:00000014 .
?uri rdf:type ?class .
?uri uberon:ABBREVIATION ?abbr .

}

ORDER BY ?abbr

## can be use to check if abbr is missing OPTIONal {?uri uberon:ABBREVIATION ?abbr } .
```


#### other properties
- title: foaf:honorificPrefix
- 


### object properties with display label

```
SELECT DISTINCT ?s ?disp ?uri ?label ?abbr 

WHERE {


?s rdf:type owl:DatatypeProperty .
?s rdfs:label ?label .
?s miaf:00000376 ?disp .

OPTIONAL {
    ?s uberon:ABBREVIATION ?abbr .
    }
}

ORDER BY ?disp

## can be use to check if abbr is missing OPTIONal {?uri uberon:ABBREVIATION ?abbr } .
```

### show mappings list

```
SELECT DISTINCT ?pURI ?pLabel ?mURI ?mLabel 

WHERE {

?pURI  miaf:4df62452_761a_4d13_9c77_98e09ab4e66c  ?mURI .
?pURI rdfs:label ?pLabel .
?mURI rdfs:label ?mLabel .
}

ORDER BY ?mLabel
```