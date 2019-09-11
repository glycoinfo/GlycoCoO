# Disease Association part
```
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix skos_c:<http://www.w3.org/2004/02/skos/core#>
prefix skos:<http://www.w3.org/2008/05/skos#>

prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix sio:<http://semanticscience.org/resource/>
prefix dcterms:<http://purl.org/dc/terms/>

select distinct ?g ?disease_label ?notation ?uniprot_id

where
{
graph ?g {
?glycoconjugate_ref glycan:has_association ?association ;
                                     gco:has_protein_part ?protein_part .
?association  sio:SIO_000628 ?disease .
?disease rdfs:label ?disease_label .
?disease skos_c:notation | skos:notation | rdfs:seeAlso ?notation  . 

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
order by ?g
```

# Source Part
```
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix sio:<http://semanticscience.org/resource/>
prefix dcterms:<http://purl.org/dc/terms/>

select distinct ?g ?tissue ?cell_line ?taxon ?uniprot_id
where
{
graph ?g {
?glycoconjugate_ref glycan:is_from_source ?source ;
                                     gco:has_protein_part ?protein_part .
optional{?source glycan:has_tissue ?tissue .}
optional{?source glycan:has_cell_line ?cell_line .}
optional{?source glycan:has_taxon ?taxon .}

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

# Glycan Part (All)
```
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix sio:<http://semanticscience.org/resource/>
prefix dcterms:<http://purl.org/dc/terms/>
prefix foaf:<http://xmlns.com/foaf/0.1/>

select distinct ?g ?uniprot_id ?glytoucan

where
{
graph ?g{
{
?glycoconjugate_ref gco:has_saccharide_part ?ref_sac ;
                                     gco:has_protein_part ?protein_part .
?ref_sac  glycan:has_glycan ?saccharide .
?saccharide foaf:primaryTopic ?glytoucan .
}
union
{
?glycoconjugate_ref gco:has_protein_part ?protein_part .
?protein_part glycan:has_glycan ?glycan .
?glycan glycan:has_glytoucan_id ?glytoucan .
}
# glyconnect
{
?protein_part gco:glycosylated_at ?protein .
?protein faldo:location ?location .
?location rdfs:seeAlso ?uniprot_id .
?location a faldo:ExactPosition .
}
union
# GlycoNAVI
{
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
}
union
# UnicarbKB
{
?protein_part gco:has_protein ?protein .
?protein dcterms:identifier ?uniprot_id .
}
}}

order by ?g
```
