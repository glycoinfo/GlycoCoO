```
# Sample RDF (ttl) 
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xml: <http://www.w3.org/XML/1998/namespace> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix faldo: <http://biohackathon.org/resource/faldo#> .
@prefix glycan: <http://purl.jp/bio/12/glyco/glycan#> .
@prefix up: <http://www.uniprot.org/core/> .
@prefix sio: <http://semanticscience.org/resource/> .
@prefix codao: <http://purl.glycoinfo.org/ontology/codao#> .
@prefix UO: <http://purl.obolibrary.org/obo/uo#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix gco: <http://purl.jp/bio/12/glyco/conjugate#> .

<Glycoconjugate>
        a gco:Referenced_glycoconjugate ;
        rdfs:label "a glycoconjugate"^^xsd:string ;
        gco:has_protein_part <Protein> ;
        gco:has_saccharide_part <Saccharide> ;
        glycan:published_in <Citation> ;
        glycan:has_association <Compound Disease Association> .
        
<Protein>
        a gco:Referenced_protein ;
        rdfs:label "a protein"^^xsd:string ;
        gco:has_attached_referenced_saccharide <Saccharide> ;
        gco:has_protein <Protein/P1> ;
        gco:has_saccharide_set <Set> .

<Protein/P1>
        a glycan:Glycoprotein ;
        rdfs:label "a glycocoprotein"^^xsd:string ;
        rdfs:seeAlso <http://identifiers.org/uniprot/{uniprot_id}> ;
        gco:glycosylated_at <Protein/P1/R> .
        
<Protein/P1/R>
        a faldo:Region ;
        faldo:location <Protein/P1/R/EP> .

<Protein/P1/R/EP>
        a faldo:ExactPosition ;
        rdfs:label "82"^^xsd:string ;
        glycan:has_amino_acid <Protein/P1/R/EP/AA> ;
        faldo:position "82"^^xsd:int .

<Protein/P1/R/EP/AA>
        a glycan:glycosylated_AA ;
        rdfs:label "amino acid of the glycosylation site"^^xsd:string ;
        rdfs:label "N"^^xsd:string ;
        skos:prefLabel "Asn"^^xsd:string .

<Saccharide>
        a glycan:Referenced_saccharide ;
        gco:glycosylates_at <Protein/P1/R> ;
        glycan:has_glycan <Saccharide/S1> .

<Set>
        a sio:SIO_000289 ; # sio:set
        rdfs:label "saccharides"^^xsd:string ;
        gco:glycosylates_at <Protein/P1/R> ;
        sio:SIO_000313 <SetItem/1> . # SIO_000313 is is-component-part-of

<SetItem/1>
        a sio:SIO_001258 ; # sio:set item
        rdfs:label "saccharide"^^xsd:string ;
        owl:sameAs <Saccharide/S1> .

<Saccharide/S1>
        a glycan:Saccharide ;
        rdfs:seeAlso <http://identifiers.org/glytoucan/{GlyTouCan_id}> ;
        foaf:primaryTopic <GlyTouCan/G1> .

<SetItem/1>
        a gco:Relative_abundance ;
        sio:SIO_000300 "50.0"^^xsd:decimal ; # sio:SIO_000300 is sio:has-value
        sio:SIO_000221 UO:0000193 . # sio:SIO_000221 is sio:has-unit; UO:0000193 is UO:purity percentage     
```
