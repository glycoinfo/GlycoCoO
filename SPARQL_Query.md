# Disease Association part

* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=PREFIX+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0APREFIX+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2008%2F05%2Fskos%23%3E%0D%0APREFIX+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0APREFIX+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fg+%3Fdisease_label+%3Fnotation+%3Funiprot_id%0D%0AWHERE%0D%0A%7B%0D%0A%09%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%3Fglycoconjugate_ref+glycan%3Ahas_association+%3Fassociation+%3B%0D%0Agco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fassociation+sio%3ASIO_000628+%3Fdisease+.%0D%0A%3Fdisease+rdfs%3Alabel+%3Fdisease_label+.%0D%0A%3Fdisease+skos%3Anotation+%7C+rdfs%3AseeAlso+%3Fnotation+.%0D%0A%23+GlyConnect%E3%80%80%26+UniCarbKB%0D%0A%7B%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A%7D%0D%0AUNION%0D%0A%7B%0D%0A%23+GlycoNAVI%0D%0A%09SERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B+++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E++%7D%0D%0A%3Fglycoconjugate_ref+glycan%3Ahas_association+%3Fassociation+%3B%0D%0Agco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fassociation+sio%3ASIO_000628+%3Fdisease+.%0D%0A%3Fdisease+rdfs%3Alabel+%3Fdisease_label+.%0D%0A%3Fdisease+skos%3Anotation+%3Fnotation+.%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A%7D%0D%0A%7D%0D%0AORDER+BY+%3Fg&format=text%2Fhtml&timeout=0&debug=on)

```
PREFIX glycan:<http://purl.jp/bio/12/glyco/glycan#>
PREFIX gco:<http://purl.jp/bio/12/glyco/conjugate#>
PREFIX skos:<http://www.w3.org/2008/05/skos#>
PREFIX dcterms:<http://purl.org/dc/terms/>
PREFIX faldo:<http://biohackathon.org/resource/faldo#>
PREFIX sio:<http://semanticscience.org/resource/>

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
# GlyConnect　& UniCarbKB
{
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
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
?disease skos:notation ?notation .
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

* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Source+Part%0D%0Aprefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+up%3A+%3Chttp%3A%2F%2Fpurl.uniprot.org%2Fcore%2F%3E%0D%0Aselect+distinct+%3Fg+%3Funiprot_id+%3Ftissue+%3Fcell_line+%3Forganism+%0D%0Awhere%0D%0A%7B%0D%0A++++%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%3Fglycoconjugate_ref+glycan%3Ais_from_source+%3Fsource+%3B%0D%0A+++++++++++++++++++++++++++++++++++++gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0Aoptional%7B%3Fsource+glycan%3Ahas_tissue+%3Ftissue+.%7D%0D%0Aoptional%7B%3Fsource+glycan%3Ahas_cell_line+%3Fcell_line+.%7D%0D%0A%23optional%7B%3Fsource+glycan%3Ahas_taxon+%3Ftaxon+.%7D%0D%0A%0D%0A%23+glyconnect%0D%0A%7B%0D%0Aoptional+%7B%0D%0A%3Fsource+glycan%3Ahas_taxon+%3Ftaxon+.%0D%0A%3Ftaxon+rdfs%3Alabel+%3Forganism+.%0D%0A%7D%0D%0A%0D%0A%3Fprotein_part+gco%3Aglycosylated_at+%3Fprotein+.%0D%0A%3Fprotein+faldo%3Alocation+%3Flocation+.%0D%0A%3Flocation+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3FExactPosition+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Flocation+a+faldo%3AExactPosition+.%0D%0AFILTER+CONTAINS+%28str%28%3Funiprot%29%2C+%3Funiprot_id%29%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0Aunion%0D%0A%23+unicarbkb%0D%0A%7B%0D%0Aoptional%7B%0D%0A%3Fsource+glycan%3Ahas_taxon+%3Ftaxon+.%0D%0A%3Ftaxon+up%3AscientificName+%3Forganism+.%0D%0A%7D%0D%0A%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%23+GlycoNAVI%0D%0ASERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B+++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E++%7D%0D%0A%0D%0A%3Fglycoconjugate_ref+glycan%3Ais_from_source+%3Fsource+%3B%0D%0A+++++++++++++++++++++++++++++++++++++gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0Aoptional%7B%3Fsource+glycan%3Ahas_tissue+%3Ftissue+.%7D%0D%0Aoptional%7B%3Fsource+glycan%3Ahas_cell_line+%3Fcell_line+.%7D%0D%0Aoptional%7B%0D%0A%3Fsource+glycan%3Ahas_taxon+%3Ftaxon+.%0D%0A%3Ftaxon+rdfs%3Alabel+%3Forganism+.%0D%0A%7D%0D%0A%0D%0A%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein+.%0D%0A%3Fref_protein+gco%3Aglycosylated_at+%3Fregion+.%0D%0A%3Fregion+faldo%3Alocation+%3Flocation+.%0D%0AOPTIONAL+%7B+%3Flocation+rdfs%3Alabel+%3Flocation_label+.+%7D%0D%0A%3Flocation+faldo%3Aposition+%3Fposition+.%0D%0A%3Fref_protein+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Ftissue+%3Fcell_line+%3Ftaxon&format=text%2Fhtml&timeout=0&debug=on)

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

* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Citation+part%0D%0Aprefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+owl%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2002%2F07%2Fowl%23%3E%0D%0Aprefix+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A%0D%0Aselect+distinct+%3Fg+%3Funiprot_id+%28str+%28%3Fpmid+%29+AS+%3FPMID+%29%0D%0Awhere%0D%0A%7B%0D%0A++++%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E%7D%0D%0A%0D%0A%0D%0A%3Fglycoconjugate_ref+glycan%3Apublished_in+%3Fcitation+.%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%0D%0A%23+glyconnect%0D%0A%7B%0D%0A%3Fprotein_part+gco%3Aglycosylated_at+%3Fprotein+.%0D%0A%3Fprotein+faldo%3Alocation+%3Flocation+.%0D%0A%3Flocation+rdfs%3AseeAlso+%3Funiprot+.%0D%0AFILTER+CONTAINS+%28str%28%3Funiprot%29%2C+%3Funiprot_id%29%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%3Flocation+a+faldo%3AExactPosition+.%0D%0AOPTIONAL+%7B+%0D%0A%3Fcitation+foaf%3AprimaryTopic+%3Fpubmed+.%0D%0ABIND%28REPLACE%28str+%28+%3Fpubmed+%29%2C+%27http%3A%2F%2Fwww.ncbi.nlm.nih.gov%2Fpubmed%2F%27%2C+%27%27%29+AS+%3Fpmid%29%0D%0A%7D%0D%0A%7D%0D%0Aunion%0D%0A%23+unicarbkb%0D%0A%7B%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0AOPTIONAL+%7B+%0D%0A%09%23+citaion+http%3A%2F%2Frdf.unicarbkb.org%2Freference%2F24279413%0D%0A%3Fcitation+owl%3AsameAs+%3Fpubmed+.+%0D%0A%3Fcitation+glycan%3Ahas_pmid+%3Fpmid+.%0D%0A%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%09%23+GlycoNAVI%0D%0ASERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E%7D%0D%0A%3Fglycoconjugate_ref+glycan%3Apublished_in+%3Fcitation+.%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0AOPTIONAL+%7B+%0D%0A%3Fcitation++rdfs%3AseeAlso+%3Fpubmed+.+%0D%0A%3Fpubmed+dcterms%3Aidentifier+%3Fpmid+.%0D%0A%7D%0D%0A%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on)

```
# Citation part
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix foaf:<http://xmlns.com/foaf/0.1/>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix owl: <http://www.w3.org/2002/07/owl#>
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select distinct ?g ?uniprot_id (str (?pmid ) AS ?PMID )
where
{
    {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb>}


?glycoconjugate_ref glycan:published_in ?citation .
?glycoconjugate_ref gco:has_protein_part ?protein_part .

# glyconnect
{
?protein_part gco:glycosylated_at ?protein .
?protein faldo:location ?location .
?location rdfs:seeAlso ?uniprot .
FILTER CONTAINS (str(?uniprot), ?uniprot_id)
VALUES ?uniprot_id { "P00738" }
?location a faldo:ExactPosition .
OPTIONAL { 
?citation foaf:primaryTopic ?pubmed .
BIND(REPLACE(str ( ?pubmed ), 'http://www.ncbi.nlm.nih.gov/pubmed/', '') AS ?pmid)
}
}
union
# unicarbkb
{
?protein_part gco:has_protein ?protein .
?protein dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
OPTIONAL { 
	# citaion http://rdf.unicarbkb.org/reference/24279413
?citation owl:sameAs ?pubmed . 
?citation glycan:has_pmid ?pmid .
}
}
}
    }
    UNION
    {
	# GlycoNAVI
SERVICE <https://sparql.glyconavi.org/sparql> {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconavi>}
?glycoconjugate_ref glycan:published_in ?citation .
?glycoconjugate_ref gco:has_protein_part ?protein_part .

?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
OPTIONAL { 
?citation  rdfs:seeAlso ?pubmed . 
?pubmed dcterms:identifier ?pmid .
}

}
}
    }
}
```

# Glycan Part
* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Glycan+Part%0D%0Aprefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0Aselect+distinct+%3Fg+%3Funiprot_id++%28str+%28%3Fglytoucan_id+%29+AS+%3FGlyTouCan+%29%0D%0Awhere%0D%0A%7B%0D%0A++++++%7B%0D%0Agraph+%3Fg%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E+%7D%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%7B%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_saccharide_part+%3Fref_sac+.%0D%0A%3Fref_sac++glycan%3Ahas_glycan+%3Fsaccharide+.%0D%0A%3Fsaccharide+foaf%3AprimaryTopic+%3Fglytoucan+.%0D%0ABIND%28REPLACE%28str+%28+%3Fglytoucan+%29%2C+%27http%3A%2F%2Fidentifiers.org%2Fglytoucan%2F%27%2C+%27%27%29+AS+%3Fglytoucan_id%29.%0D%0A%7D%0D%0Aunion%0D%0A%7B%0D%0A%3Fprotein_part+glycan%3Ahas_glycan+%3Fglycan+.%0D%0A%3Fglycan+glycan%3Ahas_glytoucan_id+%3Fglytoucan_id+.%0D%0A%7D%0D%0A%23+glyconnect%0D%0A%7B%0D%0A%3Fprotein_part+gco%3Aglycosylated_at+%3Fprotein+.%0D%0A%3Fprotein+faldo%3Alocation+%3Flocation+.%0D%0A%3Flocation+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Flocation+a+faldo%3AExactPosition+.%0D%0AFILTER+CONTAINS+%28str%28%3Funiprot%29%2C+%3Funiprot_id%29%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0Aunion%0D%0A%23+UnicarbKB%0D%0A%7B%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%09%23+GlycoNAVI%0D%0ASERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E+%7D%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_saccharide_part+%3Fref_sac+.%0D%0A%3Fref_sac++glycan%3Ahas_glycan+%3Fsaccharide+.%0D%0A%3Fsaccharide+foaf%3AprimaryTopic+%3Fglytoucan+.%0D%0A%3Fglytoucan+dcterms%3Aidentifier+%3Fglytoucan_id+.%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%09%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Fglytoucan_id&format=text%2Fhtml&timeout=0&debug=on)

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

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=prefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+wfaldo%3A%3Chttp%3A%2F%2Fwww.biohackathon.org%2Fresource%2Ffaldo%2F%3E%0D%0Aprefix+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A%0D%0Aselect+distinct+%3Fg+%3Funiprot_id+%3Flocation_label+%28str%28%3Fposition%29+AS+%3Fsite%29+%0D%0Awhere%0D%0A%7B%0D%0A++++%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%0D%0A%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein.%0D%0A%7B%0D%0A%23+http%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%0D%0A%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein+.%0D%0A%3Fref_protein+gco%3Aglycosylated_at+%3FRegion+.%0D%0A%3FRegion+faldo%3Alocation+%3FExactPosition+.%0D%0A%3FExactPosition+faldo%3Aposition+%3Fposition+.%0D%0A%3FExactPosition+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Flocation+a+faldo%3AExactPosition+.%0D%0AFILTER+CONTAINS+%28str%28%3Funiprot%29%2C+%3Funiprot_id%29%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0AUNION%0D%0A%7B%0D%0A%23+http%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0AFILTER+CONTAINS+%28str%28%3Fref_protein%29%2C+%3Funiprot_id%29%0D%0A%3Fref_protein+gco%3Aglycosylated_at+%3FRegion+.%0D%0A%3FRegion+wfaldo%3AExactPosition+%3FExactPosition+.%0D%0A%3FExactPosition+wfaldo%3Aposition+%3Fposition+.%0D%0AOPTIONAL+%7B+%3FExactPosition++gco%3Ahas_amino_acid+%3Famino_acid+.+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%09%23+GlycoNAVI%0D%0ASERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B+++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E++%7D%0D%0A%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein+.%0D%0A%3Fref_protein+gco%3Aglycosylated_at+%3Fregion+.%0D%0A%3Fregion+faldo%3Alocation+%3Flocation+.%0D%0AOPTIONAL+%7B+%3Flocation+rdfs%3Alabel+%3Flocation_label+.+%7D%0D%0A%3Flocation+faldo%3Aposition+%3Fposition+.%0D%0A%3Fref_protein+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Fposition+&format=text%2Fhtml&timeout=0&debug=on)

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

