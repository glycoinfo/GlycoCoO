# Disease Association part
* SPARQL endpoint: https://sparql.glycoinfo.org/sparql
```
PREFIX glycan:<http://purl.jp/bio/12/glyco/glycan#>
PREFIX gco:<http://purl.jp/bio/12/glyco/conjugate#>
PREFIX skos_c:<http://www.w3.org/2004/02/skos/core#>
PREFIX skos:<http://www.w3.org/2008/05/skos#>
PREFIX dcterms:<http://purl.org/dc/terms/>
PREFIX faldo:<http://biohackathon.org/resource/faldo#>
PREFIX sio:<http://semanticscience.org/resource/>
PREFIX dcterms:<http://purl.org/dc/terms/>

SELECT DISTINCT ?g ?disease_label ?notation ?uniprot_id
WHERE
{
	{
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> }
?glycoconjugate_ref glycan:has_association ?association ;
gco:has_protein_part ?protein_part .
?association sio:SIO_000628 ?disease .
?disease rdfs:label ?disease_label .
?disease skos:notation | rdfs:seeAlso ?notation .
# GlyConnect
{
?protein_part gco:glycosylated_at ?protein .
?protein faldo:location ?location .
?location rdfs:seeAlso ?uniprot .
FILTER CONTAINS (str(?uniprot), ?uniprot_id)
?location a faldo:ExactPosition .
VALUES ?uniprot_id { "P00738" }
}
UNION
# UniCarbKB
{
?protein_part gco:has_protein ?protein .
?protein dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
}
}
UNION
{
# GlycoNAVI
	SERVICE <https://sparql.glyconavi.org/sparql> {
graph ?g {
VALUES ?g {   <http://glycoinfo.org/glycocoo/glyconavi>  }
?glycoconjugate_ref glycan:has_association ?association ;
gco:has_protein_part ?protein_part .
?association sio:SIO_000628 ?disease .
?disease rdfs:label ?disease_label .
?disease skos_c:notation ?notation .
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
}
}
}
ORDER BY ?g
```

# Source Part
```
# Source Part
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix sio:<http://semanticscience.org/resource/>
prefix dcterms:<http://purl.org/dc/terms/>
prefix up: <http://purl.uniprot.org/core/>
select distinct ?g ?uniprot_id ?tissue ?cell_line ?organism 
where
{
    {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> }
?glycoconjugate_ref glycan:is_from_source ?source ;
                                     gco:has_protein_part ?protein_part .
optional{?source glycan:has_tissue ?tissue .}
optional{?source glycan:has_cell_line ?cell_line .}
#optional{?source glycan:has_taxon ?taxon .}

# glyconnect
{
optional {
?source glycan:has_taxon ?taxon .
?taxon rdfs:label ?organism .
}

?protein_part gco:glycosylated_at ?protein .
?protein faldo:location ?location .
?location rdfs:seeAlso ?uniprot .
?ExactPosition rdfs:seeAlso ?uniprot .
?location a faldo:ExactPosition .
FILTER CONTAINS (str(?uniprot), ?uniprot_id)
VALUES ?uniprot_id { "P00738" }
}
union
# unicarbkb
{
optional{
?source glycan:has_taxon ?taxon .
?taxon up:scientificName ?organism .
}

?protein_part gco:has_protein ?protein .
?protein dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
}
    }
    UNION
    {
# GlycoNAVI
SERVICE <https://sparql.glyconavi.org/sparql> {
graph ?g {
VALUES ?g {   <http://glycoinfo.org/glycocoo/glyconavi>  }

?glycoconjugate_ref glycan:is_from_source ?source ;
                                     gco:has_protein_part ?protein_part .
optional{?source glycan:has_tissue ?tissue .}
optional{?source glycan:has_cell_line ?cell_line .}
optional{
?source glycan:has_taxon ?taxon .
?taxon rdfs:label ?organism .
}

?ref_conjugate gco:has_protein_part ?ref_protein .
?ref_protein gco:glycosylated_at ?region .
?region faldo:location ?location .
OPTIONAL { ?location rdfs:label ?location_label . }
?location faldo:position ?position .
?ref_protein gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
}
    }
}
order by ?g ?tissue ?cell_line ?taxon
```

# Citation Part
```
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix foaf:<http://xmlns.com/foaf/0.1/>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix dcterms:<http://purl.org/dc/terms/>

select distinct ?g ?pubmed ?uniprot_id
where
{
graph ?g {
{
?glycoconjugate_ref glycan:published_in ?citation ;
                                     gco:has_protein_part ?protein_part .
?citation foaf:primaryTopic | owl:sameAs | rdfs:seeAlso ?pubmed .

# glyconnect
{
?protein_part gco:glycosylated_at ?protein .
?protein faldo:location ?location .
?location rdfs:seeAlso ?uniprot_id .
?location a faldo:ExactPosition .
}
union
# unicarbkb
{
?protein_part gco:has_protein ?protein .
?protein dcterms:identifier ?uniprot_id .
}
union
# GlycoNAVI
{
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
}
}
}
}
```

# Glycan Part
* SPARQL endpoint: https://sparql.glycoinfo.org/sparql
```
# Glycan Part
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix sio:<http://semanticscience.org/resource/>
prefix dcterms:<http://purl.org/dc/terms/>
prefix foaf:<http://xmlns.com/foaf/0.1/>
select distinct ?g ?uniprot_id  (str (?glytoucan_id ) AS ?GlyTouCan )
where
{
      {
graph ?g{
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> <http://glycoinfo.org/glycocoo/glyconavi> }
?glycoconjugate_ref gco:has_protein_part ?protein_part .
{
?glycoconjugate_ref gco:has_saccharide_part ?ref_sac .
?ref_sac  glycan:has_glycan ?saccharide .
?saccharide foaf:primaryTopic ?glytoucan .
BIND(REPLACE(str ( ?glytoucan ), 'http://identifiers.org/glytoucan/', '') AS ?glytoucan_id).
}
union
{
?protein_part glycan:has_glycan ?glycan .
?glycan glycan:has_glytoucan_id ?glytoucan_id .
}
# glyconnect
{
?protein_part gco:glycosylated_at ?protein .
?protein faldo:location ?location .
?location rdfs:seeAlso ?uniprot .
?location a faldo:ExactPosition .
FILTER CONTAINS (str(?uniprot), ?uniprot_id)
VALUES ?uniprot_id { "P00738" }
}
union
# UnicarbKB
{
?protein_part gco:has_protein ?protein .
?protein dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
}
    }
    UNION
    {
	# GlycoNAVI
SERVICE <https://sparql.glyconavi.org/sparql> {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconavi> }
?glycoconjugate_ref gco:has_saccharide_part ?ref_sac .
?ref_sac  glycan:has_glycan ?saccharide .
?saccharide foaf:primaryTopic ?glytoucan .
?glytoucan dcterms:identifier ?glytoucan_id .
?glycoconjugate_ref gco:has_protein_part ?protein_part .
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
	}
    }
}
order by ?g ?glytoucan_id

```
# Glycosylated sites part
* SPARQL endpoint: https://sparql.glycoinfo.org/sparql
```
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix wfaldo:<http://www.biohackathon.org/resource/faldo/>
prefix sio:<http://semanticscience.org/resource/>
prefix dcterms:<http://purl.org/dc/terms/>
prefix foaf:<http://xmlns.com/foaf/0.1/>

select distinct ?g ?uniprot_id ?location_label (str(?position) AS ?site) 
where
{
    {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> }

?ref_conjugate gco:has_protein_part ?ref_protein.
{
# http://glycoinfo.org/glycocoo/glyconnect
?ref_conjugate gco:has_protein_part ?ref_protein .
?ref_protein gco:glycosylated_at ?Region .
?Region faldo:location ?ExactPosition .
?ExactPosition faldo:position ?position .
?ExactPosition rdfs:seeAlso ?uniprot .
?location a faldo:ExactPosition .
FILTER CONTAINS (str(?uniprot), ?uniprot_id)
VALUES ?uniprot_id { "P00738" }
}
UNION
{
# http://glycoinfo.org/glycocoo/unicarbkb
VALUES ?uniprot_id { "P00738" }
FILTER CONTAINS (str(?ref_protein), ?uniprot_id)
?ref_protein gco:glycosylated_at ?Region .
?Region wfaldo:ExactPosition ?ExactPosition .
?ExactPosition wfaldo:position ?position .
OPTIONAL { ?ExactPosition  gco:has_amino_acid ?amino_acid . }
}
}
    }
    UNION
    {
	# GlycoNAVI
SERVICE <https://sparql.glyconavi.org/sparql> {
graph ?g {
VALUES ?g {   <http://glycoinfo.org/glycocoo/glyconavi>  }
?ref_conjugate gco:has_protein_part ?ref_protein .
?ref_protein gco:glycosylated_at ?region .
?region faldo:location ?location .
OPTIONAL { ?location rdfs:label ?location_label . }
?location faldo:position ?position .
?ref_protein gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
}
}
    }
}
order by ?g ?position 
```

