# $\mathbb{C}Duce$ as a tool to validate ontologies

### Introduction

$\mathbb{C}$Duce allows the developer to describe the structure of an XML document by designing a type for each kind of node we want to represent, and by describing which nodes can be its children, via a list of the types of admissible children nodes. 

##### Example

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

The example above shows how we describe a class by specifying the tag opening the element, and by supplying a list of possible attributes for the class. Any element that respects such a structure is identified as a class.

## Validation

If we describe the ontology structure of interest with CDuce types, we can start from any XML document and verify if its structure is compatible with the expected one. This verification can be done with a runtime cast. If the cast fails, it raises an exception showing the exact point in the XML document that is incorrect. 

This high-level procedure is then useful to validate any knowledge base expressed in XML, with respect to a given structure described via CDuce types.


## Transformation

We can also be interested in transforming a well-formed XML document [NOTA: ben formato rispetto a cosa? Se fosse rispetto ai tipi dell'ontologia in cui vogliamo trasformarlo non ci sarebbe bisogno di trasformarlo...] into an ontology of a given CDuce type. 

We start from the hypothesis that the document contains both compatible and non-compatible elements with respect the target type. We will then select all the compatible elements by using 'transform' [NOTA: il lettore non sa cos'è...] and/or queries/projections. This selection can be performed at different levels of depth:

- by selecting only classes, individuals and relationships that respects the description given by the CDuce type;

- by selecting only attributes that respects the description given by the CDuce type: in this case, we start from a class/individual/relationship that owns both admissible and non-admissible attributes and we extract a structure containg compatible attributes only;

- by selecting all the elements, compatible and non-compatible, the latter to be made compatible with appropriate transformations.

The procedure of Transformation allows the developer to start from a knowledge base which is not compatible with respect to a CDuce type (partially or totally) and to obtain an ontology matching completely the CDuce type.


## Conclusions

Both Validation and Transformation are supported by the $\mathbb{C}$Duce static type checking, that guarantees a formal soundness with respect to the sought types of the transformations and of the results obtained.


