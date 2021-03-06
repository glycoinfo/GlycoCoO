# Disease Association part

* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Disease+Association+part%0D%0APREFIX+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0APREFIX+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2008%2F05%2Fskos%23%3E%0D%0APREFIX+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0APREFIX+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fg+%3Fdisease_label+%3Fnotation+%3Funiprot_id%0D%0AWHERE%0D%0A%7B%0D%0A%09%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%23+GlyConnect%E3%80%80%26+UniCarbKB%0D%0A%3Fglycoconjugate_ref+glycan%3Ahas_association+%3Fassociation+%3B%0D%0Agco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fassociation+sio%3ASIO_000628+%3Fdisease+.%0D%0A%3Fdisease+rdfs%3Alabel+%3Fdisease_label+.%0D%0A%3Fdisease+skos%3Anotation+%3Fnotation+.%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0AUNION%0D%0A%7B%0D%0A%23+GlycoNAVI%0D%0A%09SERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B+++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E++%7D%0D%0A%3Fglycoconjugate_ref+glycan%3Ahas_association+%3Fassociation+%3B%0D%0Agco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fassociation+sio%3ASIO_000628+%3Fdisease+.%0D%0A%3Fdisease+rdfs%3Alabel+%3Fdisease_label+.%0D%0A%3Fdisease+skos%3Anotation+%3Fnotation+.%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A%7D%0D%0A%7D%0D%0AORDER+BY+%3Fg&format=text%2Fhtml&timeout=0&debug=on)

```
# Disease Association part
PREFIX glycan:<http://purl.jp/bio/12/glyco/glycan#>
PREFIX gco:<http://purl.jp/bio/12/glyco/conjugate#>
PREFIX skos:<http://www.w3.org/2008/05/skos#>
PREFIX dcterms:<http://purl.org/dc/terms/>
PREFIX faldo:<http://biohackathon.org/resource/faldo#>
PREFIX sio:<http://semanticscience.org/resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?g ?disease_label ?notation ?uniprot_id
WHERE
{
	{
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> }
# GlyConnect　& UniCarbKB
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

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Source+Part%0D%0Aprefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+up%3A+%3Chttp%3A%2F%2Fpurl.uniprot.org%2Fcore%2F%3E%0D%0Aselect+distinct+%3Fg+%3Funiprot_id+%3Ftissue+%3Fcell_line+%3Forganism+%0D%0Awhere%0D%0A%7B%0D%0A++++%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%23+glyconnect+%26+unicarbkb%0D%0A%3Fglycoconjugate_ref+glycan%3Ais_from_source+%3Fsource+%3B+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0Aoptional+%7B+%3Fsource+glycan%3Ahas_tissue+%3Ftissue+.+%7D%0D%0Aoptional+%7B+%3Fsource+glycan%3Ahas_cell_line+%3Fcell_line+.+%7D%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0Aoptional+%7B%0D%0A%3Fsource+glycan%3Ahas_taxon+%3Ftaxon+.%0D%0A+OPTIONAL+%7B+%3Ftaxon+up%3AscientificName++%3Forganism+.+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%23+GlycoNAVI%0D%0ASERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B+++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E++%7D%0D%0A%0D%0A%3Fglycoconjugate_ref+glycan%3Ais_from_source+%3Fsource+%3B%0D%0A+++++++++++++++++++++++++++++++++++++gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0Aoptional%7B%3Fsource+glycan%3Ahas_tissue+%3Ftissue+.%7D%0D%0Aoptional%7B%3Fsource+glycan%3Ahas_cell_line+%3Fcell_line+.%7D%0D%0Aoptional%7B%0D%0A%3Fsource+glycan%3Ahas_taxon+%3Ftaxon+.%0D%0Aoptional+%7B+%3Ftaxon+up%3AscientificName+%3Forganism+.+%7D%0D%0A%7D%0D%0A%0D%0A%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein+.%0D%0A%3Fref_protein+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Ftissue+%3Fcell_line+%3Ftaxon%0D%0A&format=text%2Fhtml&timeout=0&debug=on)

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
# glyconnect & unicarbkb
?glycoconjugate_ref glycan:is_from_source ?source ; gco:has_protein_part ?protein_part .
optional { ?source glycan:has_tissue ?tissue . }
optional { ?source glycan:has_cell_line ?cell_line . }
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }
optional {
?source glycan:has_taxon ?taxon .
 OPTIONAL { ?taxon up:scientificName  ?organism . }
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
optional { ?taxon up:scientificName ?organism . }
}
?ref_conjugate gco:has_protein_part ?ref_protein .
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

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Citation+part%0D%0Aprefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A%0D%0Aselect+distinct+%3Fg+%3Funiprot_id+%28str+%28%3Fpmid+%29+AS+%3FPMID+%29%0D%0Awhere%0D%0A%7B%0D%0A++++%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E%7D%0D%0A%0D%0A%0D%0A%3Fglycoconjugate_ref+glycan%3Apublished_in+%3Fcitation+.%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%0D%0A%0D%0A%23+glyconnect+%26+unicarbkb%0D%0A%0D%0A%3Fcitation++dcterms%3Areferences+%3Fpubmed+.+%0D%0A++++++++++%3Fcitation+glycan%3Ahas_pmid+%3Fpmid+.%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%09%23+GlycoNAVI%0D%0ASERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E%7D%0D%0A%3Fglycoconjugate_ref+glycan%3Apublished_in+%3Fcitation+.%0D%0A%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0AVALUES+%3Funiprot_id+%7B+%22P00738%22+%7D%0D%0A%3Fcitation++dcterms%3Areferences+%3Fpubmed+.+%0D%0A++++++++++%3Fcitation+glycan%3Ahas_pmid+%3Fpmid+.%0D%0A%7D%0D%0A%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Fpmid%0D%0A&format=text%2Fhtml&timeout=0&debug=on)

```
# Citation part
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select distinct ?g ?uniprot_id (str (?pmid ) AS ?PMID )
where
{
    {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb>}


?glycoconjugate_ref glycan:published_in ?citation .
?glycoconjugate_ref gco:has_protein_part ?protein_part .
?protein_part gco:has_protein ?protein .
?protein rdfs:seeAlso ?uniprot .
?uniprot dcterms:identifier ?uniprot_id .
VALUES ?uniprot_id { "P00738" }


# glyconnect & unicarbkb

?citation  dcterms:references ?pubmed . 
          ?citation glycan:has_pmid ?pmid .
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
?citation  dcterms:references ?pubmed . 
          ?citation glycan:has_pmid ?pmid .
}
}
    }
}
order by ?g ?pmid
```

# Glycan Part
* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=%23+Glycan+Part%0D%0Aprefix+glycan%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fglycan%23%3E%0D%0Aprefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+sio%3A%3Chttp%3A%2F%2Fsemanticscience.org%2Fresource%2F%3E%0D%0Aprefix+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0Aselect+distinct+%3Fg+%3Funiprot_id++%3Fglytoucan_id%0D%0Awhere%0D%0A%7B%0D%0A++++++%7B%0D%0A%09%09graph+%3Fg%7B%0D%0A%09%09%09VALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%09%09%09%09%23+GlyConnect+%26+UniCarbKB%0D%0A%09%09%09%09%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%09%09%09%09%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%09%09%09%09%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%09%09%09%09%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0A%09%09%09%09%3Fglycoconjugate_ref+gco%3Ahas_saccharide_part+%3Fref_sac+.%0D%0A%09%09%09%09%3Fref_sac++glycan%3Ahas_glycan+%3Fsaccharide+.%0D%0A%09%09%09%09%3Fsaccharide+foaf%3AprimaryTopicOf+%3Fglytoucan+.%0D%0A%09%09%09%09%3Fglytoucan+dcterms%3Aidentifier+%3Fglytoucan_id+.%0D%0A%09%09%09%7D%0D%0A%09++++%7D%0D%0A%09++++UNION%0D%0A%09++++%7B%0D%0A%09%09%23+GlycoNAVI%0D%0A%09%09SERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0A%09%09%09graph+%3Fg+%7B%0D%0A%09%09%09%09VALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E+%7D%0D%0A%09%09%09%09%3Fglycoconjugate_ref+gco%3Ahas_protein_part+%3Fprotein_part+.%0D%0A%09%09%09%09%3Fprotein_part+gco%3Ahas_protein+%3Fprotein+.%0D%0A%09%09%09%09%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%09%09%09%09%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0A%09%09%09%09%3Fglycoconjugate_ref+gco%3Ahas_saccharide_part+%3Fref_sac+.%0D%0A%09%09%09%09%3Fref_sac++glycan%3Ahas_glycan+%3Fsaccharide+.%0D%0A%09%09%09%09%3Fsaccharide+foaf%3AprimaryTopicOf+%3Fglytoucan+.%0D%0A%09%09%09%09%3Fglytoucan+dcterms%3Aidentifier+%3Fglytoucan_id+.%0D%0A%09%09%09%7D%0D%0A%09%09%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Funiprot_id+%3Fglytoucan_id%0D%0A&format=text%2Fhtml&timeout=0&debug=on)

```
# Glycan Part
prefix glycan:<http://purl.jp/bio/12/glyco/glycan#>
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix sio:<http://semanticscience.org/resource/>
prefix foaf:<http://xmlns.com/foaf/0.1/>
select distinct ?g ?uniprot_id  ?glytoucan_id
where
{
      {
		graph ?g{
			VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> }
				# GlyConnect & UniCarbKB
				?glycoconjugate_ref gco:has_protein_part ?protein_part .
				?protein_part gco:has_protein ?protein .
				?protein rdfs:seeAlso ?uniprot .
				?uniprot dcterms:identifier ?uniprot_id .
				?glycoconjugate_ref gco:has_saccharide_part ?ref_sac .
				?ref_sac  glycan:has_glycan ?saccharide .
				?saccharide foaf:primaryTopicOf ?glytoucan .
				?glytoucan dcterms:identifier ?glytoucan_id .
			}
	    }
	    UNION
	    {
		# GlycoNAVI
		SERVICE <https://sparql.glyconavi.org/sparql> {
			graph ?g {
				VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconavi> }
				?glycoconjugate_ref gco:has_protein_part ?protein_part .
				?protein_part gco:has_protein ?protein .
				?protein rdfs:seeAlso ?uniprot .
				?uniprot dcterms:identifier ?uniprot_id .
				?glycoconjugate_ref gco:has_saccharide_part ?ref_sac .
				?ref_sac  glycan:has_glycan ?saccharide .
				?saccharide foaf:primaryTopicOf ?glytoucan .
				?glytoucan dcterms:identifier ?glytoucan_id .
			}
		}
    }
}
order by ?g ?uniprot_id ?glytoucan_id
```
# Glycosylated sites part

* SPARQL endpoint: https://sparql.glycoinfo.org/sparql

[run](https://sparql.glycoinfo.org/sparql?default-graph-uri=&query=prefix+gco%3A%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F12%2Fglyco%2Fconjugate%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aprefix+faldo%3A%3Chttp%3A%2F%2Fbiohackathon.org%2Fresource%2Ffaldo%23%3E%0D%0Aprefix+dcterms%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0Aselect+distinct+%3Fg+%3Funiprot_id+%28str%28%3Fposition%29+AS+%3Fsite%29+%0D%0Awhere%0D%0A%7B%0D%0A++++%7B%0D%0Agraph+%3Fg+%7B%0D%0AVALUES+%3Fg+%7B++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconnect%3E+%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Funicarbkb%3E+%7D%0D%0A%09%23+GlyConnect+and+UniCarbKB%0D%0A%09%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein.%0D%0A%09%3Fref_protein+gco%3Aglycosylated_at+%3Fregion+.%0D%0A%09%3Fregion+faldo%3Alocation+%3Flocation+.%0D%0A%09%3Flocation+faldo%3Aposition+%3Fposition+.%0D%0A%09%3Fref_protein+gco%3Ahas_protein+%3Fprotein+.%0D%0A%09%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%09%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0A%7D%0D%0A++++%7D%0D%0A++++UNION%0D%0A++++%7B%0D%0A%09%09%23+GlycoNAVI%0D%0A%09%09SERVICE+%3Chttps%3A%2F%2Fsparql.glyconavi.org%2Fsparql%3E+%7B%0D%0A%09%09%09graph+%3Fg+%7B%0D%0A%09%09%09VALUES+%3Fg+%7B+++%3Chttp%3A%2F%2Fglycoinfo.org%2Fglycocoo%2Fglyconavi%3E++%7D%0D%0A%09%09%09%3Fref_conjugate+gco%3Ahas_protein_part+%3Fref_protein+.%0D%0A%09%09%09%3Fref_protein+gco%3Aglycosylated_at+%3Fregion+.%0D%0A%09%09%09%3Fregion+faldo%3Alocation+%3Flocation+.%0D%0A%09%09%09%3Flocation+faldo%3Aposition+%3Fposition+.%0D%0A%09%09%09%3Fref_protein+gco%3Ahas_protein+%3Fprotein+.%0D%0A%09%09%09%3Fprotein+rdfs%3AseeAlso+%3Funiprot+.%0D%0A%09%09%09%3Funiprot+dcterms%3Aidentifier+%3Funiprot_id+.%0D%0A%09%09%09%7D%0D%0A%09%09%7D%0D%0A++++%7D%0D%0A%7D%0D%0Aorder+by+%3Fg+%3Fposition+&format=text%2Fhtml&timeout=0&debug=on)

```
prefix gco:<http://purl.jp/bio/12/glyco/conjugate#>
prefix dcterms:<http://purl.org/dc/terms/>
prefix faldo:<http://biohackathon.org/resource/faldo#>
prefix dcterms:<http://purl.org/dc/terms/>
select distinct ?g ?uniprot_id (str(?position) AS ?site) 
where
{
    {
graph ?g {
VALUES ?g {  <http://glycoinfo.org/glycocoo/glyconnect> <http://glycoinfo.org/glycocoo/unicarbkb> }
	# GlyConnect and UniCarbKB
	?ref_conjugate gco:has_protein_part ?ref_protein.
	?ref_protein gco:glycosylated_at ?region .
	?region faldo:location ?location .
	?location faldo:position ?position .
	?ref_protein gco:has_protein ?protein .
	?protein rdfs:seeAlso ?uniprot .
	?uniprot dcterms:identifier ?uniprot_id .
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
			?location faldo:position ?position .
			?ref_protein gco:has_protein ?protein .
			?protein rdfs:seeAlso ?uniprot .
			?uniprot dcterms:identifier ?uniprot_id .
			}
		}
    }
}
order by ?g ?position 
```

