```
<Glycoconjugate>
        a glycan:Referenced_compound ;
        glycan:published_in <Citation> .
        
<Protein>
        a gco:Referenced_protein ;
        gco:has_attached_referenced_saccharide <Saccharide> ;
        gco:has_protein <Protein/P1> ;
        gco:has_saccharide_set <Set> .

glycan:Referenced_protein rdfs:subclassOf glycan:Referenced_compound .

<Protein/P1>
        gco:glycosylated_at <Protein/P1/R> .
        
<Protein/P1/R> faldo:location <Protein/P1/R/EP> .

<Protein/P1/R/EP> faldo:position "82"ˆˆxsd:int .

<Set> sio:is-component-part-of <SetItem> .

<SetItem> owl:sameAs <Saccharide/S1> .

<Saccharide/S1> foaf:primaryTopic <GlyTouCan/G1> .
```
