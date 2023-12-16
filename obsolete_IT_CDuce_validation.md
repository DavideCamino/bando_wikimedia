# $\mathbb{C}Duce$ come strumento per validare ontologie

### Introduzione

$\mathbb{C}$Duce permette di descrivere la struttura di un documento XML creando un tipo per ogni tipo di nodo che ci interessa rappresentare e descrivendo quali possono essere i figli del nodo specificando la lista dei tipi dei figli ammissibili. 

##### Esempio

```ocaml
type Class = <owl:Class rdf:about=String> [ ClassAtt * ]

type ClassAtt = SubClass | EqClass | Label | Note 
type SubClass = <rdfs:subClassOf rdf:resource=String> []
type EqClass  = <owl:equivalentClass> [ EqAttr ] 
              | <owl:equivalentClass rdf:resource=String> []
type EqAttr   = <owl:Restriction> [ AnyXml* ]
type Label    = <rdfs:label xml:lang=String> String
type Note     = <skos:scopeNote xml:lang=String> String
```

Come si vede descriviamo una classe specificando il tag che apre l’elemento e fornendo una lista di possibili attributi per la classe. Qualsiasi elemento che rispetti questa struttura viene identificato come una classe.

## Validazione

Se descriviamo la struttura dell’ontologia che ci interessa creare possiamo partire da un qualsiasi documento XML e verificare se la struttura di quest’ultimo è compatibile con la struttura che ci aspettiamo, questa verifica può essere fatta con un cast che se fallisce solleva un eccezione e ci evidenzia il punto del documento XML che ha fatto saltare l’eccezione.

Questo procedimento ci permette ad alto livello di validare una qualunque base di conoscenza espressa in XML per valutare se ha la struttura che ci aspettiamo.

## Trasformazione

Possiamo invece essere interessati a trasformare un documento XML ben formato in un ontologia del tipo che ci aspettiamo. Ipotizziamo che il documento di partenza contenga sia elementi compatibili che non, possiamo allora selezionare tutti gli elementi compatibili ricorrendo alla `transform` o alle query/proiezioni; questa selezione può avvenire a diversi livelli di profondità andando a selezionare:

- solo classi, individui e relazioni che rispettino la nostra descrizione;

- solo attributi che rispettino la nostra descrizione, quindi partiamo da una classe/individuo/relazione che possiede sia attributi ammissibili che non ed esportiamo un elemento che contenga solo attributi compatibili

- tutti gli elementi che siamo intenzionati a esportare a prescindere che siano o meno compatibili per poi renderli applicando oppurtune trasformazioni.

Questa seconda procedura ci permette di partire da una base di conoscenza non completamente compatibile (o anche non compatibile affatto) con quella che vorremmo, per poi ottenere un’ontologia che abbia esattamente la struttura che ci aspettiamo.

## Conclusione

Sia il primo procedimento che il secondo sono supportati dal controllo statico sui tipi offerto da $\mathbb{C}$Duce che ci garantisce di operare trasformazioni corrette e di ottenere elementi del tipo che ci aspettiamo. In questo senso lavorare con $\mathbb{C}$Duce ci offre garanzie di correttezza delle trasformazioni che effettuiamo e in ultima analisi anche dei risultati che otteniamo.
