# Pipeline

## Classifier

Il classifier legge testo scritto per umani prendendolo da varie sorgenti e restituisce delle triple che riguardano la persona cercata, le triple sono accompagnate da un punteggio che riguarda l'affidabilità della tripla  (e da un punteggio che quantifica quanto la tripla sia affetta da bias?)

## CDuce

CDuce si occupa di organizzare le triple creando un grafo di conoscenza compatibile con quello di wikidata, in modo che sia integrabile con le informazioni raccolte e formalizzate dallo scrittore dell'articolo.

In particolare CDuce deve:

- stabilire se una tripla è valida (secondo criteri che possono anche essere manipolati);

- stabilire se 2 triple rappresentano la stessa informazione;

- trovare un tipo per la tripla: questo è il centro dell'elaborazione, il tipo rappresenta quali informazioni sono contenute nella tripla, quanto sono affidabili e se sono o meno affette da bias

- costruire con le triple che si sono ritenute valide un'ontologia riguardo la persona cercata, l'ontologia deve potersdi integrare con il grafo di wikidata

#### Tipizzazione delle triple

La tipizzazione di concetti che riguardano l'etica o la morale è particolarmente delicata. Tralasciando gli aspetti correlati alle discipline più filosofiche ci concentriamo sul dare un'idea di come si possa assegnare un tipo ad una tripla che rappresenta informazioni arbitrarie riguardo una persona.

###### Gerarchia di tipi

Una possibile strada è quella di creare una gerarchia di tipi che descrivono gli aspetti della vita di una persona, in base ad informazioni reperite con analisi statistiche o attraverso consulto con esperti alcuni di questi tipi rappresenteranno informazioni che possono essere affette da bias. Quando si riceve una tripla in modo completamente deterministico si trova la collocazione della tripla in un ramo della gerarchia. Questo approccio permette di modellare la conoscenza in modo molto capillare e permette di seguire molto bene il flusso decisionale attraverso il quale vengono filtrate le informazioni; inoltre la base di conoscenza che si può creare una volta filtrate le informazioni in questo modo risulterà molto organizzata. Per contro prevede a monte di modellare tutti i possibili aspetti della vita di una persona. Gli aspetti non presi in considerazione possono comunque essere trattati, ma non saranno organizzati nella gerarchia e di conseguenza nel grafo di conoscenza, inoltre potenzialmente si perderebbero le informazioni riguardo ai bias.

###### Approccio naïf

Senza creare quasi nessuna gerarchia si possono usare esclusivamente le informazioni estratte dal classificatore per creare una base di conoscenza, i controlli sulle informazioni possono essere eseguiti attingendo alle informazioni extra fornite dal classificatore (attendibilità di un informazione e presenza di bias). In questo modo non è necessaria nessuna conoscenza a priori del dominio e si possono comunque suggerire allo scrittore dell'articolo informazioni non presenti nel testo redatto a mano. Ovviamente la base di conoscenza che si crea in questo modo risulta meno strutturata e richiederebbe lavoro da perte dello srittore dell'articolo per essere integrata propriamente nel grafo di wikidata. In ogni caso può essere una strada percorribile, almeno all'inizio per saggiare la bontà del classificatore e di CDuce a interagire, e per provare a costruire delle basi di conoscenza compatibili con wikidata.

## Ad alto livello

<img title="" src="Pictures/pipeline_white.svg" alt="" width="983">
