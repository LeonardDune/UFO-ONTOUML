# From the Essence of an Enterprise Towards

# Enterprise Ontology Patterns

```
Tanja Poletaeva1(&), Habib Abdulrab^1 , and Eduard Babkin^2
```
(^1) INSA de Rouen, LITIS Lab, Rouen, France
ta.poletaeva@gmail.com, abdulrab@insa-rouen.fr
(^2) National Research University Higher School of Economics,
Nizhny Novgorod, Russia
eababkin@hse.ru
Abstract. In this paper we partially present an initial version of a Formal
Enterprise Ontology Pattern Language, which has been developed to support
conceptual enterprise modeling and a subsequent construction of different
design and implementation artifacts. The proposed enterprise ontology patterns
address problems related to the correlated modeling of both the intersubjective
world and the production world of an enterprise, as well as the effective con-
junction of the domain knowledge and the operational knowledge of an enter-
prise. The proposed language builds on a synthesis of the Unified Foundational
Ontology (UFO) and the DEMO Enterprise Ontology. We also demonstrate how
the pattern language was applied to the domain-specific enterprise modeling.

## Keywords: Conceptual modeling  Enterprise ontology  Foundational

## ontologyOntology patternOntology pattern language

## 1 Introduction

In recent years, ontologies have been recognized as a powerful instrument for an
explicit and formal representation of conceptualizations of reality, providing theoretical
foundations for conceptual modeling languages [ 1 ]. Particularly, an enterprise ontology
is essential for a deep understanding of the construction and operation of an enterprise
via its coherent, comprehensive, consistent, and concise conceptual models [ 2 ].
However, while being provided with the proper expressive modeling language pre-
serving the enterprise-world semantics, one can experience ambiguous choices when
expressing knowledge additional to the modeled enterprise essence [ 3 – 5 ] or when
constructing design and implementation artifacts upon the created conceptual models
[ 4 , 6 ]. There is a lack of languages that have enough expressivity for enterprise
knowledge, while preserving a formal semantics.
In [ 7 ], the authors proposed the Enterprise Ontology Pattern Language (E-OPL)
aimed at facilitating enterprise conceptual modeling. According to [ 8 ],“an ontology
pattern describes a particular recurring modeling problem that arises in specific
ontology development context and presents a well-proven solution for the problem”.
The patterns of E-OPL were extracted from different enterprise ontologies addressing
five aspects: Organization Arrangement, Team Definition, Institutional Roles,

©Springer International Publishing Switzerland 2016
D. Aveiro et al. (Eds.): EEWC 2016, LNBIP 252, pp. 118–131, 2016.
DOI: 10.1007/978-3-319-39567-8_


Institutional Goals, and Human Resource Management. Moreover, the E-OPL patterns
in [ 7 ] are represented in OntoUML [ 1 ], a UML profile that preserves the ontological
distinctions put forth by the Unified Foundational Ontology (UFO) [ 1 ].
In this paper, we propose an initial version of alternative enterprise ontology pat-
terns which comprise the elements and the axiomatization derived from a synthesis of
(i) the Unified Foundational Ontology (UFO) [ 1 ] and (ii) the enterprise ontology
DEMO–the Design and Engineering Methodology for Organizations [ 2 ]. We have
obtained our synthesis by (i) applying UFO and its well-founded conceptual modeling
language OntoUML to articulate the theory of enterprise ontology in a system of
general categories; (ii) and adding some additional ontological categories based on their
relevance for the theory of enterprise ontology.
The most important property of the DEMO modeling language is that conceptual
models represented in this language are essential, i.e., they show the core enterprise
knowledge. In contrast, the ontology patterns presented in this work are aimed at
expressing the core knowledge in the form that facilitates its extension and integration.
Particularly, the authors focus on the correlated modeling of both the intersubjective
world and the production world of an enterprise. The patterns founded on both the
upper level ontology and the enterprise ontology preserve a formal semantics together
with a real-world semantics in a broad sense. Therefore, this work would hopefully
contribute to the integration of the domain knowledge and the operational knowledge
of an enterprise.
The outline of this paper is organized as follows. First, the theoretical background
of our work is summarized in Sect. 2. In Sect. 3 , we elaborate on the proposed
enterprise ontology patterns. Then, Sect. 4 illustrates the application of the enterprise
ontology patterns for a domain-specific enterprise conceptual modeling. Finally,
Sect. 5 presents thefinal considerations and directions for further research.

## 2 Ontological Foundations of Enterprise Ontology Patterns

In this section, we focus on some important aspects of the underlying ontologies UFO
[ 1 ] and DEMO [ 2 ] of the proposed enterprise ontology patterns.

2.1 The Unified Foundational Ontology (UFO)

The philosophically, linguistically and cognitively well-founded foundational ontology
UFO wasfirst proposed by Guizzardi in [ 1 ] and has been developed in many works
afterwards [ 9 – 15 ]. UFO consists of four main parts: an ontology of endurants (objects,
continuants)–UFO-A [ 1 ], an ontology of perdurants (events, occurrents)–UFO-B
[ 11 ], an ontology of social entities–UFO-C [ 12 ], and an ontology of services–UFO-S
[ 13 ]. Hereafter, we briefly summarize the formal and ontological meta-properties of
some types elaborated in thefirst three parts of UFO. These types are represented by
stereotypes in the OntoUML metamodel.
UFO-A explains a number of distinctions among object types. Whilst all types
carry a principle of application, only sortal types either provide or carry a uniform

```
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 119
```

principle of identity for their instances. In this research, we exploit the following sortal
types:Kind,Subkind,Role,Phase. While Kinds provide a principle of identity for their
instances, Subkinds carry the principle of identity supplied by Kinds. Moreover, Kinds
and Subkinds carry out a meta-property of rigidity being necessarily applied to their
instances in every possible world. In contrast, anti-rigidity characterizes a type whose
instance(s) can cease to be an instance of that type without ceasing to exist and without
altering its identity. For example, a particular individual, which is an instance of type
Studentin one world, can cease to instantiate this type in another world without ceasing
to exist as the same individual of typePerson[ 1 ]. Thus, Roles and Phases are dis-
tinguished as anti-rigid sortals. A Phase is a relationally independent type whose
instantiation is characterized by a change of an intrinsic property of an individual.
A Role is a relationally dependent type whose instantiation is obligatory related to other
entities.
Non-sortals represent an abstraction of properties that are common to multiple
disjoint kinds and, therefore, do not carry a unique principle of identity for their
instances.Categoryrepresents a rigid and relationally-independent non-sortal type that
aggregates essential properties common to different kinds.Role Mixin, in turn, repre-
sents an anti-rigid and relationally dependent non-sortal type that aggregates properties
common to different roles.
Another important distinction in the UFO ontology is within the categories of
relations. It recognizes two broad categories of relations, namely,formal relationsand
material relations.Formal relations hold between two or more entities because of very
nature of these entities, without any further intervening individual. Conversely,
material relations have a material structure of their own, which mediates the connected
entities and inheres in the mereological sum of them [ 14 ]. Such mediating entities
constitute the extension ofRelators. For example, amedical treatmentconnects a
patient with a medical unit; amarriageconnects a wife and a husband [ 1 ]. The formal
relation of mediation between a relator and the entities it connects is a sort of inherence
and, hence, a special type of existential dependence relation. Relators can only exist
while connecting the relata, i.e. they exhibit mutual dependency patterns involving all
arguments, as well as dependencies on external entities besides the arguments [ 14 ].
Axiomatization of situations,events, anddispositionswas summarized in UFO-B.
Situations are special type of endurants. They are complex entities that are constituted
by possibly many endurants (including other situations). In other words, situation is a
portion of reality that can be comprehended as a whole. A relation of“being present at”
is defined between endurants and the situations they constitute [ 12 ]. Situations can be
factual or counterfactual. Factual situations (or Facts) are said to obtain at particular
time points.
Events are perdurants composed by temporal parts and happened in time in the
sense that they extend in time accumulating temporal parts. Events are considered as
possible transformations from one portion of reality to another, i.e. they may change
reality by changing the state of affairs from one situation to another [ 11 ].
Moreover, in the ontology design patterns of the UFO-B ontology, temporal
properties of objects and spatial properties of events are derived from the existential
dependence of events on the objects that participate in them. Properties that are only
manifested in particular situations on the occurrence of certain triggering events are

120 T. Poletaeva et al.


calleddispositions. Dispositions are manifested through the occurrence of resulting
events and state changes [ 15 ].
UFO-C incorporatesintentionalityto the basic core provided by UFO-A and
UFO-B. In this context, UFO distinguishes between Agentive and Non-agentive sub-
stantial individuals, termedagentsandobjects, respectively. As opposed to objects,
agents are capable of bearing special kind of intrinsic properties namedintentional
moments. Intentionality of agents should be understood as the capacity of their prop-
erties to refer to possible situations of reality. Every intentional moment has a type
(e.g.,belief,desire,intention) and a propositional content represented by aproposition.
The latter being an abstract representation of a class of situations referred by that
intentional moment.
Intentionsare desired state of affairs for which the agent commits at pursuing (an
intention is an internal commitment). For this reason, intentions cause the agent to
performactions. Actions are intentional events, i.e., events with the specific purpose of
satisfying the propositional content of some intention of an agent. The propositional
content of an intention is termed agoal. UFO contemplates a relation between situa-
tions and goals such that a situation may satisfy a goal.
Communicative acts(special kinds of actions) can be used to createsocial moments
(commitmentsandclaims). Thus, social moments are types of intentional moments that
are created by the exchange of communicative acts between parties and the conse-
quences of these exchanges. In this view, language not only represents the reality but
also creates a part of reality. The later ontological claim tightly correlates with the LAP
foundations of DEMO (ref. Sect.2.2).

2.2 The DEMO Theory and Methodology of Enterprise Ontology

In the presented work, we employ the OntoUML [ 1 ] conceptual modeling language to
extend real-world semantics of the modeling constructs of the DEMO Theory and
Methodology of Enterprise Ontology [ 2 ]. Based on the strong theoretical basis, the
DEMO methodology facilitates creation of ontological models that are essential,
complete, free from logical contradictions, compact and succinct, independent of their
realization and implementation issues [ 2 ].
The interpretive and intersubjective world view of the methodology results in
considering an enterprise as a discrete dynamic system, of which the elements are
social individuals oractors, capable to negotiate by performingcoordination actsand
to contribute to bringing about the goods or services by performingproduction acts.By
performing coordination acts, actors express theirintensionsand comply withcom-
mitmentstowards each other regarding the performance of production acts [ 2 ]. By
performing both kinds of acts, actors transfer the world into the new states charac-
terized by resultedcoordination factsand (if any)production facts.
The core concept in DEMO is the notion of the uniform communication patterns
between autonomic actors involved in a business deal. These patterns, also called
transaction patterns, always involve twoactor roles(the initiator and the executor) and
consist of certain coordination acts related to one production fact of a particular type.
Transactionis a sequence of acts that is a path through the complete transaction

```
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 121
```

pattern [ 2 ]. It goes off in three consecutive phases: theorder phase, theexecution
phase, and theresult phase[ 2 ].
The DEMO transaction concept distinguishes between the intersubjective (social)
and the objective worlds. Thus, coordination acts and their results (coordination facts)
relate to the intersubjective world. By performing production acts actors change the
states of products or services related to the objective world. The distinction of these two
worlds at the conceptual level gives an opportunity for a coherent modeling of both the
information and the process worldviews on an enterprise.
Finally, the methodology builds a comprehensive view on the interaction and
management processes of an enterprise in four Aspect Models [ 2 ]. Through these
conceptual models expressed in an enterprise-specific modeling language, it is possible
to achieve a solid understanding of business agent roles, their potential communica-
tions and fulfilled changes in the production world, the types of transactions taking
place in an organization and relations between them, as well as the information pro-
cessed and created in the course of transactions execution.

## 3 A Formal Enterprise Ontology Pattern Language

In this section, we elaborate on a set of enterprise ontology patterns built on a synthesis
of UFO and DEMO. Due to lack of space, we left the description of the synthesis out of
the scope of this paper. The patterns described in the following subsections are tightly
interrelated with each other through their elements.

3.1 Participation in a Transaction

Enterprises are social systems whose elements (or social individuals) are human beings
able to enter and comply with commitments [ 2 ]. Granted authority to perform particular
acts in a responsible way, a social individual of an enterprise fulfills anactor role[ 2 ].
In his fulfillment of an actor role, a social individual becomes an actor. Obviously, a
social individual may cease to be an actor without ceasing to exist. Moreover, an actor
role can be instantiated by agents of different kinds, e.g. persons, organizations or
organizational units. Thereby, Actor Role is a Role Mixin stereotyped by
<<roleMixin>> in OntoUML model depicted in Fig. 1.
The notion of transaction discussed in DEMO [ 2 ] is articulated in the UFO cate-
gories as follows. At each time the business relation between two actors holds, the
transactionis constituted by a mereological sum of all mutual commitments made by
actors in their negotiation about a particular change in the production world (i.e., a
production result). Thus, each transaction is arelatormediating two actors (Fig. 1 ).
The actor that initiates a transaction is of the typeInitiator. The actor that carries out a
production act is of the typeExecutor.InitiatorandExecutorare subtypes of the type
Actor Role.
In the broader sense, transactions are mereological sums of all their constituent
relational qualities [ 14 ] inhering in one interacting actor and directly or indirectly
existentially dependent on another one. These qualities and their changes can be

122 T. Poletaeva et al.


specified in conceptual models by attributes of transactions. For example, a yearly
membership registration (Transaction) of a customer (Initiator) in a company
(Executor) can have a particular cost (an attribute), which changes over time.
Moreover, being an endurant, each transaction is an instance of a kind that can be
specialized in various ways along the distinctions proposed by OntoUML (see
Sect.2.1). Hence, for each instance ofTransaction, the phasesTransaction-Order,
Transaction-Execution,orTransaction-Resultcan be specified according to the coor-
dination facts constituting this transaction.
Distinction of actor roles in an organization by means of the method described in
[ 2 ] together with the Organization Arrangement patterns developed in [ 7 , 16 ] could
help the ontology engineer to treat problems related to the definition ofKindsfor
selected actor roles (see also Sect. 4 ).

3.2 Coordination Acts and Facts

Each coordination act performed by an actor towards his addressee contains an
intention and a proposition [ 2 ]. With theintention, an actor proclaims his‘social
attitude’with respect to theproposition. The standard transaction may contain coor-
dination acts with the following intentions: request, promise, state, accept, decline, quit,
reject, and stop [ 2 ]. With the proposition, an actor proclaims an abstract representation
of a class of desired situations [ 1 ]. In accordance with many standards, the portion of
reality which is subject to changes, can be abstracted by the categoryWork Product.
The foregoing definition of coordination acts was formalized by the Coordination
Act pattern. This pattern comprises the types:Actor Role,C-act,C-act Intention,C-act
Proposition,Work Product Disposition, Work Product, as well as their interrelations
depicted in Fig. 2.
We propose to model instances of thePropositiontype as specializations (subtypes)
ofWork Product Disposition, where the extension of the latter is a class of desired
situations such as creation or termination of an object, a relation between objects, or a
qualitative property of an object. For example, the proposition of C-acts and C-facts

```
<<roleMixin>>
Initiator
```
```
<<roleMixin>>
Executor
```
```
<<relator>>
Transaction
```
```
<<mediation>>
involves >
```
```
<<mediation>>
< involves
```
```
<<material>>
```
```
<<roleMixin>>
ActorRole
{disjoint, complete}
```
```
1..*
```
```
11
```
```
<<mediation>> 1..*
< involves 1..*
```
```
1
```
```
<<phase>>
Transaction-Order
```
```
<<phase>>
Transaction-Execution
```
```
<<phase>>
Transaction-Result
```
```
Fig. 1. The pattern of participation in a transaction
```
```
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 123
```

appeared in a transaction of typeMembership Registrationcan be formulated as‘(new)
membership has been started’or simply,‘Membership Started’, where the latter is a
possible specialization ofWork Product Disposition. Thus, thePropositiontype is a
high-order universal (a powertype), i.e. a rigid sortal whose instances are types [ 17 ].
Following [ 7 ], we extended the OntoUML metamodel by introducing the stereo-
type <<hou>> to represent high-order universals.
A coordination actbrings abouta situation, whichtriggersa (social)commitment
of one agent towards another regarding the proclaimed intention and the proposition.
This commitment is acoordination fact(C-fact)[ 2 ]. Examples of coordination facts
are:“membership has been startedis requested asap”,“membership has been startedis
promised asap”, where“membership has been started”is the propositional content of
both C-acts and their resulted C-facts, and“membership”is an identifiable instance of
kindMembership, whereMembershipis a specialization of the categoryWork Product.
For the sake of simplicity, in this version of patterns, we omit from consideration the
time part of propositions.
As a social commitment, aC-fact inheresin one of the negotiating actors per-
forming a C-act, and isexternally dependenton the target actor. Hereby we consider a
C-fact being a relational quality (amode) that contributes to constitute the relationship
between two actors, i.e., eachC-factis always apart ofsometransaction. Moreover,
we assume that each C-fact inherits the (fact part of) C-act proposition from its acti-
vating C-act.
C-acts with particular intention define a partition of the generalization set of C-fact
types (C-factTypepowertype). In other words, all C-facts brought about by C-acts with
particular intention, are instances of particular specialization of theC-facttype. For
instance,Work Product Disposition Requestedcomprises instances ofC-factthat result

```
<<roleMixin>>
ActorRole
```
```
<<roleMixin>>
ActorRole’
```
```
<<relator>>
Transaction
```
```
<<mediation>>
involves >
```
```
<<mediation>>
< involves
1 1..* 1..* 1
```
```
<<mode>>
C-fact
```
```
< partOf
```
```
1..*
```
```
1
```
```
< inheresIn 0..*
```
```
1
```
```
0..* externallyDependentOn >
```
```
1
```
```
<<event>>
C-act
```
```
< brings-about
```
```
1
```
```
1
```
```
< performedBy
0..*
```
```
1
```
```
1
<<mode>>
C-actIntention
```
```
causedBy >
0..*
```
```
<<hou>>
C-act Proposition
```
```
< propositionalContentOf
```
```
< propositionalContentOf
1..*
1
```
```
1..*
```
```
1
```
```
<<category>>
WorkProduct
```
```
<<disposition>>
WorkProductDispositon
inheresIn >
```
```
1 < satisfies
```
```
1
```
```
<<hou>>
C-factType 1
```
```
< defines
1..*
```
```
< instanceOf
```
```
< inheresIn
```
```
1
```
```
0..*
```
```
Fig. 2. The pattern of coordination acts and facts
```
124 T. Poletaeva et al.


C-acts with the intention‘request’,orWork Product Disposition Promisedcomprises
instances resulted C-acts with the intention‘promise’.
The foregoing definition of coordination facts was formalized by the Coordination
Fact pattern. This pattern comprises the types:Actor Role,Transaction,C-fact,C-fact
Type,C-act Proposition,Work Product Disposition,Work Productas well as their
interrelations depicted in Fig. 2.

3.3 Production Acts

By performing material or immaterial production act (P-act), the executor of a trans-
action contributes to bringing about goods and/or services [ 2 ]. Thus, aproduction act
maybring aboutawork product disposition(Fig. 3 ), which is a change of a qualitative
property of an object, creation/termination of an object, or creation/termination of a
relation between objects. A work product disposition inheres in awork product. The
relatorWork Product Participationestablishes the participation of work products in a
P-act [ 18 ]. This relator is modeled with its specializations for creation and change
participation.
When the ontology engineer wants to represent the structure of work products, the
Work Product Composition and the Work Product Nature patterns developed in [ 18 ]
facilitate modeling of work product mereological decomposition and the types of work
products respectively. Moreover, since the patterns in [ 18 ] are constructed using
OntoUML, they can be easily merged with the pattern depicted in Fig. 3.

3.4 Production Facts

As pointed out in DEMO [ 2 ], all changes of a work product that have not been traced
properly in a social world of an enterprise are not considered of being effective or

```
<<roleMixin>>
Executor
```
```
<<roleMixin>>
Initiator
```
```
<<relator>>
Transaction
```
```
<<mediation>> <<mediation>>
1
```
```
0..*
<<category>>
WorkProduct
```
```
<<disposition>>
WorkProductDispositon
```
```
inheresIn >
```
```
<<action>>
P-act
```
```
performedBy >
```
```
brings-about >
```
```
1
```
```
0..
```
```
<<relator>> 0..*
WorkProductParticipation <<mediation>>
participationOf >
```
```
0..*
```
```
1
```
(^1) 1..* 1..* 1
<<mediation>>
actsUpon >
1
0..*
<<material>>
changes >
1 < partOf
0..*
1
<<material>>
creates >
Fig. 3. The pattern of production acts
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 125


usable in this world. Thus, only a work product change, which is stated and accepted
by coordination acts of a particular transaction, becomes aproduction fact(P-fact)of
an enterprise [ 2 ].
To put it more precisely, an individualpis a P-factum iff there is a work product
dispositionpwhich satisfies both the propositional content of thestatementof this
disposition by a C-fact, and the propositional content of theacceptanceof this dis-
position by a C-fact. C-facts stating and accepting the disposition, are parts of the same
transaction and instances of the types (or their specializations)Work Product Dispo-
sition StatedandWork Product Disposition Acceptedrespectively (Fig. 4 ).

Since the conceptual model in Fig. 4 does not precisely express the given defini-
tion, hereafter we specify it more formally infirst order logic. In the definition that
follows, we use the notation x::U to represent the relation of instantiation between an
individual x and a universal U.

```
P-fact pðÞ¼defWorkProductDisposition pðÞK 9 xðsatisfies xðÞ;pKx::C-actPropositionÞ
K 9 !yðpropositionalContentOf xðÞ;yKy::WorkProductDispositionStatedÞK 9 !z
ðpropositionalContentOf xðÞ;zKz::WorkProductDispositionAcceptedÞðÞ 1
```
It is important to highlight that unambiguous articulation of typesC-act Proposition
andWork Product Dispositionas well as their interrelations with the types of the
coordination world and the types of the production world of an enterprise serves to
provide a basis for the coherent modeling of states in both worlds.

## 4 Applying the Enterprise Ontology Patterns: A Case Study

Enterprise ontology patterns are modeling fragments to be used during enterprise
conceptual modeling, and focus only on conceptual aspects, without any concern with
the technology or language [ 8 ]. In this section, we shortly present a case study,
applying the enterprise ontology patterns for the conceptual modeling of pizzas
delivery.
One can imagine a simple Pizzeria where only pizzas are made on receiving a new
order. Customers can have their pizzas delivered home. To realize this service, the
owner of the company hired students, who deliver pizzas on bicycles. However,

```
<<disposition>>
WorkProductDispositon
```
```
<<hou>>
C-act Proposition
```
```
<<mode>>
C-fact
```
```
< propositionalContentOf < satisfies
```
```
<<mode>>
WorkProductDispositionStated
```
```
<<mode>>
WorkProductDispositionAccepted
```
```
Fig. 4. The pattern of production facts
```
126 T. Poletaeva et al.


the students deliver pizzas only in the city region nearby the Pizzeria. For the delivery
of orders to remote locations, the Pizzeria uses the transportation service of a
third-party company. The owner of the Pizzeria decided to control the delivery process
by means of ICT (Information and Communication Technology). He started from the
conceptual modeling stage preliminary to the data modeling. In addition, we suppose
that the owner have already analyzed his business by means of the DEMO method-
ology [ 2 ]. Thus, he analyzed the transactions, the actor roles, and the business pro-
cesses of his company.
Figure 5 presents the conceptual model, which was constructed by applying the
Participation in a Transaction pattern together with the Organization Arrangement
patterns from [ 7 ] to a conceptualization of theDeliverytransaction in the Pizzeria. In
this domain-specific pattern, the rolesInitiatorandExecutorare specified byOrder
ManagerandDelivererrespectively. WhileOrder Manageris a role that can be played
by organizational units of the Pizzeria (instances ofPizzeria Organizational Unit), two
kinds of actors can play a role ofDeliverer, to wit: the Pizzeria’s delivery unit and
third-party delivery companies (instances ofThird-party Delivery Co). Moreover, the
domain-specific facts‘order id of [Delivery] is [ID]’,‘start date of [Delivery] is
[Date]’, ‘end date of [Delivery] is [Date]’were represented respectively by the
attributesOrderId, startDate, andendDateof theDeliveryrelator.

The ontology engineer (the Pizzeria’s owner) might need to track coordination facts
appeared in theDeliverytransactions by means of ICT. The pattern of Coordination
Facts (Fig. 2 ) can be applied at the initial conceptual modeling stage. This pattern leads
to the definition of a work product type, a type of inhered dispositions (Work Product
Disposition), and the instances ofC-act Propositionthat allow making commitments
about the desired disposition(s) before it comes to exist.

```
<<role>>
OrderManager
```
```
<<relator>>
Delivery
```
```
<<roleMixin>>
Deliverer
```
```
<<mediation>> <<mediation>>
```
```
<<material>>
deliveredBy >
```
```
<<datatype>>
ID
```
```
/orderId
```
(^11)
1..* 1..*
1 1
<<role>>
**PizzeriaDeliveryUnit**
<<role>>
**Third-partyDeliveryCo**
<<kind>>
**PizzeriaOrganizationalUnit**
<<kind>>
**Organization**
<<datatype>>
**Date**
/startDate
1
*
<<datatype>>
**Date**
/endDate
*^1
<<kind>>
**OrganizationalUnit**
Fig. 5. Extended conceptual model of theDeliverytransaction
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 127


For the sake of simplicity, we suppose that a work product of theDeliverytrans-
actions is of the typePizza, and the dispositions are instances ofPizza Deliveredwith
the attributeaddress(Fig. 6 ). In Fig. 6 , only one instance ofC-act Propositionis
depicted. According to the proposition made in Sect.3.2, this instance is a type of
dispositions (Pizza Delivered) constituting the fact part of delivery requests. However,
in Fig. 6 , the instance ofC-act Propositionis depicted separately from the typePizza
Delivered. This example illustrates that a number of delivered pizza states (the
instances of Pizza Delivered) may satisfy ‘PizzaDelivered’ instance of C-act
Proposition.
C-facts resulted C-acts with different intentions constitute different phases of a
transaction. Thus, the P-fact typeDelivery Requested(Fig. 6 ) is a part of the order
phase ofDelivery.

We should highlight that consideration of different subtypes ofDeliverercan
require the specialization ofPizza Delivered as well as new instances of C-act
Proposition, e.g. the proposition Pizza Delivered Locally for all requests to the
Pizzeria’s delivery unit responsible for deliveries.
The specification of the Production Acts pattern can be extended by the standard
delivery metadata modeled by the attributes of a work product (Fig. 7 ). Further
specification of the elements of the domain-specific pattern in Fig. 7 may be required to
model special conditions of production acts.
In Fig. 8 , the specification of the Production Fact pattern is depicted together with
one exemplifying instance. For this particular case, the instances of the P-fact com-
ponents were given names reflected their datalogical representations. If the
domain-specific pattern is used for creation of meta-data in Pizzeria’s database, then
these instances illustrate possible data elements.

```
<<datatype>>
AddressDomain /address
```
```
*
```
```
<<role>>
OrderManager
```
```
<<roleMixin>>
Deliverer
```
```
<<phase>>
Delivery-Order
```
```
<<mediation>>
involves >
```
```
<<mediation>>
< involves
11 1..* 1..*
```
```
<<mode>>
DeliveryRequested
```
```
< partOf
```
```
1
```
```
1
```
```
< inheresIn
```
```
0..*
```
```
1
```
```
externallyDependentOn >
```
```
0..*
```
```
1
```
```
<<hou>>
< propositionalContentOf C-act Proposition
```
```
1..*
1
```
```
<<kind>>
Pizza
```
```
<<disposition>>
PizzaDelivered
```
```
< inheresIn
```
```
< satisfies
1
```
```
1
PizzaDelivered
```
```
1
```
```
<<relator>>
Delivery
<<category>>
WorkProduct
```
```
Fig. 6. Conceptual model of the coordination facts of delivery requests
```
128 T. Poletaeva et al.


## 5 Final Considerations

Enterprise conceptual modeling is not an easy task. In this work, we proposed an initial
version of the Formal Enterprise Ontology Pattern Language aimed at facilitating
enterprise conceptual modeling. Since the patterns constituting this language are
expressed in OntoUML, they carry out the ontological and formal semantics of
OntoUML’s modeling constructs inherited from the foundational ontology UFO [ 1 ].
On the other hand, since the proposed patterns were built in accordance with the
DEMO theory of enterprise ontology [ 2 ], they inherit the real-world semantics of the
enterprise domain.
We argue that the proposed enterprise ontology patterns tend to bring the following
benefits for enterprise conceptual modeling: (i) the coherent models of the coordination

```
<<roleMixin>>
Deliverer
```
```
<<role>>
OrderManager
```
```
<<relator>>
Delivery
```
```
<<mediation>> <<mediation>>
```
```
1
```
```
0..*
<<kind>>
Pizza
```
```
<<disposition>>
PizzaDelivered
```
```
inheresIn >
```
```
<<action>>
Delivery-act
```
```
performedBy >
```
```
brings-about >
```
```
1
```
```
0..
```
```
<<relator>> 0..*
PizzaInDelivery <<mediation>>
participationOf >
```
```
0..*
```
```
1
```
(^1) 1..* 1..* 1
<<mediation>>
actsUpon >
1
0..*
<<material>>
changes >
1 < partOf
0..*
1
<<datatype>>
**Mass**
<<datatype>> /mass
**Date**
/creationDate
Fig. 7. Extended conceptual model of theDeliveryproduction acts
SignatureOfCarrierX
SignatureOfConsigneeY
ConsignmentNoteNo
<<disposition>>
**PizzaDelivered**
<<hou>>
**C-act Proposition**
<<mode>>
**C-fact**
< propositionalContentOf < satisfies
<<mode>>
**DeliveryStated**
<<mode>>
**DeliveryAccepted**
Specified pattern of Production Facts
PizzaDelivered DeliveredAt10h
< satisfies
< propositionalContentOf
< propositionalContentOf
Fig. 8. Conceptual model of theDeliveryproduction facts and one exemplifying instance of this
model
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 129


and the production world of an enterprise; (ii) the conceptual modeling process of
particular enterprises tends to be accelerated by reuse of these patterns; (iii) an easy
integration with the domain-specific ontological patterns expressed in OntoUML.
Following the directives on how to map conceptual models in OntoUML to their
implementation and less-expressive computationally-oriented codification languages
[ 19 ], our future research direction is the mapping of the proposed ontology patterns to
the constructs of the Web Ontology Language (OWL) and to the rules expressed in the
Semantic Web Rule Language^1 (SWRL). Codification of the proposed patterns will
result in a core enterprise data metamodel.

Acknowledgments.The reported study was funded by RFBR according to the research project
No16-06-00300 a. This research was also partly funded by the CLASSE (“Les Corridors
Logistiques: Application a la Vallee de la Seine et son Environnement”) project of the Grand
Research Network of in Upper Normandy (Grand Réseaux de Recherche de Haute-Normandie).
The authors would like to express their gratitude to Dr. Giancarlo Guizzardi for his invaluable
advice and inspiring discussions.

## References

1. Guizzardi, G.: Ontological foundations for structural conceptual models. Telematics Instituut
    Fundamental Research Series, No. 015, The Netherlands (2005). ISSN 1388-
2. Dietz, J.L.G.: Enterprise Ontology–Theory and Methodology. Springer, Heidelberg (2006)
3. Barjis, J., Dietz, J.L.G., Liu, K.: Combining the DEMO methodology with semiotic methods
    in business process modeling. In: Liu, K., Clarke, R.J., Andersen, P.B., Stamper, R.K. (eds.)
    Information, Organisation and Technology: Studies in Organisational Semiotics.
    Information and Organization Design Series, vol. 1, pp. 213–246 (2001)
4. de Jong, J.: Designing the Information Organization from Ontological Perspective. In:
    Albani, A., Dietz, J.L., Verelst, J. (eds.) EEWC 2011. LNBIP, vol. 79, pp. 1–15. Springer,
    Heidelberg (2011)
5. de Kinderen, S., Gaaloul, K., Proper, H.A.: Transforming Transaction Models into
    ArchiMate. In: CAiSE 2012 Forum at the 24th International Conference on Advanced
    Information Systems Engineering (CAiSE). CEUR-WS, vol. 855, pp. 114–121 (2012)
6. Krouwel, M.R., Op 't Land, M.: Combining DEMO and Normalized Systems for
    Developing Agile Enterprise Information Systems. In: Albani, A., Dietz, J.L., Verelst,
    J. (eds.) EEWC 2011. LNBIP, vol. 79, pp. 31–45. Springer, Heidelberg (2011)
7. Falbo, R.A., Ruy, F.B., Guizzardi, G., Barcellos, M.P., Almeida, J.P.A.: Towards an
    enterprise ontology pattern language. In: 29th Annual ACM Symposium on Applied
    Computing, pp. 323–330. ACM (2014)
8. de Almeida Falbo, R., Guizzardi, G., Gangemi, A., Presutti, V.: Ontology patterns:
    clarifying concepts and terminology. In: 4th Workshop on Ontology and Semantic Web
    Patterns. Sydney, Australia (2013)

(^1) The Web Ontology Language (OWL) and the Semantic Web Rule Language (SWRL) are Semantic
Web languages recommended by the W3C for knowledge representation.
130 T. Poletaeva et al.


9. Guizzardi, G.: Logical, ontological and cognitive aspects of object types and cross-world
    identity with applications to the theory of conceptual spaces. In: Zenker, F., Gärdenfors, P.
    (eds.) Applications of Conceptual Spaces: The Case for Geometric Knowledge
    Representation, Part III. Synthese Library, vol. 359, pp. 165–186. Springer, Switzerland
    (2015)
10. Guizzardi, G., Wagner, G.: Using the Unified Foundational Ontology (UFO) as a foundation
for general conceptual modeling languages. In: Poli, R., Healy, M., Kameas, A. (eds.)
Theory and Applications of Ontology: Computer Applications, pp. 175–196. Springer,
Netherlands (2010)
11. Guizzardi, G., Wagner, G., de Almeida Falbo, R., Guizzardi, R.S., Almeida, J.P.A.: Towards
ontological foundations for the conceptual modeling of events. In: Ng, W., Storey, V.C.,
Trujillo, J.C. (eds.) ER 2013. LNCS, vol. 8217, pp. 327–341. Springer, Heidelberg (2013)
12. Guizzardi, G., Falbo, R.A., Guizzardi, R.S.S.: Grounding software domain ontologies in the
Unified Foundational Ontology (UFO): the case of the ODE software process ontology. In:
XI Iberoamerican Workshop on Requirements Engineering and Software Environments,
pp. 244–251 (2008)
13. Nardi, J.C., De Almeida Falbo, R., Almeida, J.P.A., Guizzardi, G., Ferreira Pires, L., Van
Sinderen, M.J., Guarino, N., Fonseca, C.M.: A Commitment-based Reference Ontology for
Services. Information Systems, vol. 54, pp. 263–288. Elsevier Ltd. (2015)
14. Guarino, N., Guizzardi, G.:“We need to discuss the relationship”: revisiting relationships as
modeling constructs. In: Zdravkovic, J., Kirikova, M., Johannesson, P. (eds.) CAiSE 2015.
LNCS, vol. 9097, pp. 279–294. Springer, Heidelberg (2015)
15. Guizzardi, G., Wagner, G.: Dispositions and causal laws as the ontological foundation of
transition rules in simulation models. In: 2013 Winter Simulation Conference, pp. 1335–
1346. IEEE (2013)
16. Quirino, G.K., et al.: Towards a service ontology pattern language. In: Johannesson, P., Lee,
M.L., Liddle, S.W., Opdahl, A.L., Pastor López,Ó. (eds.) ER 2015. LNCS, vol. 9381,
pp. 187–195. Springer, Heidelberg (2015). doi:10.1007/978-3-319-25264-3_
17. Guizzardi, G., Almeida, J.P.A., Guarino, N., Carvalho, V.A.: Towards an ontological
analysis of powertypes. In: International Workshop on Formal Ontologies for Artificial
Intelligence (FOFAI 2015), 24th International Joint Conference on Artificial Intelligence
(IJCAI 2015). CEUR-WS, vol. 1517 (2015)
18. Ruy, F.B., Falbo, R.A., Barcellos, M.P., Guizzardi, G.: Towards an ontology pattern
language for harmonizing software process related ISO standards. In: 29th Annual ACM
Symposium on Applied Computing, pp. 388–395 (2015)
19. Guizzardi, G., Zamborlini, V.: Using a trope-based foundational ontology for bridging
different areas of concern in ontology-driven conceptual modeling. In: Science of Computer
Programming, vol. 96, Part 4, pp. 417–443. Elsevier B.V. (2014)

```
From the Essence of an Enterprise Towards Enterprise Ontology Patterns 131
```

