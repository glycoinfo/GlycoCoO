```
<Glycoconjugate>
        a gco:Referenced_glycoconjugate ;
        gco:has_protein_part <Protein> ;
        gco:has_saccharide_part <Saccharide> ;
        glycan:published_in <Citation> ;
        glycan:has_association <Compound Disease Association> .
        
<Protein>
        a gco:Referenced_protein ;
        gco:has_attached_referenced_saccharide <Saccharide> ;
        gco:has_protein <Protein/P1> ;
        gco:has_saccharide_set <Set> .

<Protein/P1>
        a glycan:Glycoprotein ;
        gco:glycosylated_at <Protein/P1/R> .
        
<Protein/P1/R>
        a faldo:Region ;
        faldo:location <Protein/P1/R/EP> .

<Protein/P1/R/EP>
        a faldo:ExactPosition ;
        faldo:position "82"ˆˆxsd:int .

<Saccharide>
        a glycan:Saccharide ;
        glycan:has_glycan <Saccharide/S1> ;


<Set>
        a SIO:000289 ;
        sio:is-component-part-of <SetItem> .

<SetItem>
        a sio:SIO_001258 ;
        owl:sameAs <Saccharide/S1> .

<Saccharide/S1> foaf:primaryTopic <GlyTouCan/G1> .
```
