 PDF To Markdown Converter
Debug View
Result View
DEMOSL-4.7.2
The DEMO Specification Language v4.
Abstract. Conceptual models must be expressed in a suitable language in order
to communicate them. To avoid misunderstandings, this language should allow
for formulating clear, unambiguous expressions. First order logic is a language
that has all the properties one needs and wants, but it has the drawback that its
common Peano-Russell notation puts off people who lack a background in logic
and mathematics. The DEMO Specification Language (DEMO-SL) offers a
user-friendly look, although it is firmly based on first order logic. The syntax of
DEMO-SL is defined in Extended Backus-Naur Form (EBNF) or, alternatively,
in syntax diagrams. In addition to formal textual expressions, it allows for
graphical representations. Three aspect models, the Cooperation Model, the
Process Model, and the Fact Model, are represented in diagrams. The diagrams
are kept simple, which means that what cannot be expressed in a diagram,
should be expressed in formal text. The Action Model is only expressed in
formal text. In addition to the explanation and illustration of DEMO-SL, the
meta model or schema of each of the four aspect models is presented and dis-
cussed, as well as the schema of each of the diagrams kinds and table kinds.
2 The DEMO Specification Language v4.7.

Ownership and authorship
The ownership of the DEMO Specification Language, abbreviated to DEMO-SL, lies
with the Enterprise Engineering institute. Ownership implies the responsibility re-
garding the correctness of the content of this document.
The version of this document is 4.7.2. Major changes to the content will result into
version 4.8, 4.9, etc. Minor changes, notably error corrections, will result into version
4.7.3, 4.7.4, etc.
The most recent version, as well as a selected number of earlier versions, can al-
ways be downloaded from http://www.ee-institute.org.

The authorship of version 4.7.2 lies with Jan Dietz (jan.dietz@sapio.nl)

3
1 Introduction
In this document, the formal language is presented in which the essential models of
DEMO-4 (Design and Engineering Methodology for Organisations), as defined in [1],
Chap. 12, are expressed. The language is called DEMO Specification Language, or
DEMO-SL for short.
The distinction between models on the one side and the diagrams, tables and form-
alised texts in which they are expressed on the other side, is crucial: they constitute
respectively the semantics and the syntax of DEMO-SL (cf. [1] Chap. 6).
Expressions in DEMO-SL are basically formal textual expressions in first order
logic [2]. Many textual expressions have also a graphical or tabular equivalent, be-
cause the appreciation of formal text in current practice is generally low, particularly

by people who lack a logical/mathematical background. Consequently, one should
understand the DEMO diagrams as graphical representations of logical formulas. The
same holds for the tabular expressions.
Despite the current preference for diagrams to formal text, there are limits to the
expressive power of diagrams: they can easily become impractical if one has to re-
member (too) many shapes, symbols and constructs. Therefore, the diagrams in
DEMO-SL are kept simple; they have a limited set of shapes, symbols and constructs.
What cannot be expressed in a diagram, should be expressed in a formal text. To illus-
trate the point: the graphical process modelling language BPMN 2.02^1 comprises over
100 symbols, and the graphical data modelling language ORM 2^2 several dozens. This
makes it hard to keep up, both in producing diagrams and in reading them.
In Chap. 2, the basics of DEMO-SL are presented: the definition of terms, refer-
ences, variables and assertions, the declaration and the derivation of types, and the
ways in which time values are represented. In Sect. 2.6, the four aspect models of
DEMO are discussed, thus the Cooperation Model (CM), the Action Model (AM), the
Process Model (PM) and the Fact Model (FM). In Chaps. 3 through 7, the various
ways in which they can be expressed, are presented. Appendix A contains the meta
model or schema of the four aspect models, as well as the schema’s of the diagrams
and tables in which they are expressed. In appendix B, the Extended Backus-Naur
Form (EBNF) is explained. It is the primary formalism for expressing the syntax of
DEMO-SL. In appendix C, the syntax diagram is presented as an alternative way to
formally express the syntax of DEMO-SL. Syntax diagrams are applied in Chap. 5.
The attentive reader will notice that there are minor differences between the syn-
tactic expressions in this document and the ones in [1], Chap.6, where they are based
on. What is presented in the document in hand is leading, the ones in the book Enter-
prise Ontology need to be corrected.

(^1) https://www.omg.org/spec/BPMN/2.0.2/PDF
(^2) http://www.orm.net/pdf/ORM2_TechReport1.pdf

4 The DEMO Specification Language v4.7.

2 The basics of DEMO-SL
2.1 References, variables and assertions
reserved term = coordination act name | coordination fact name | special term;

coordination act name = “request” | “promise” | “declare” | “accept” | “decline” | “re-
ject” | “revoke” | “allow” | “refuse”;

coordination fact name = “requested” | “promised” | “declared” | “accepted” | “de-
clined” | “rejected” | “revoked” | “allowed” | “refused”;

shorthand C-act/fact name = “rq” | “pm” | “da” | “ac” | “dc” | “rj” | “rv” | “al” | “rf”;

special term = “performer” | “addressee” |
“et” % event time % |
“ot” % operative time; it may be preceded by a coordination fact name, like “reques-
ted” or “declared” % |
“now” % at any moment, the value of the variable now is the current time % |
“set of” % to specify that a thing is a set of things % |
“is in” % to specify that a thing is a member of a set %;

transaction kind id = “TK”, {digit}-; Examples: TK7, TK
multiple transaction kind id = “MTK”, {digit}-; Examples: MTK2, MTK
product kind id = “PK”, {digit}-; Examples: PK3, PK
actor role id = “AR”, {digit}-; Examples: AR8, AR
transactor role id = “TAR”, {digit}-; Examples: TAR17, TAR
composite transactor role id = “CTAR”, {digit}-; Examples: CTAR01, CTAR
entity name = {letter | digit}-; Examples: John, Mary
value name = {letter | digit}-; Examples: sedan, 2827ET

shorthand C-act kind id = “[“ transaction kind id, “/“, shorthand C-act/fact name, “]”;
Examples: [TK01/rq], [TK17/da]
shorthand C-fact kind id = “(“ transaction kind id, “/“, shorthand C-act/fact name, “)”;
Examples: (TK01/rq), (TK17/da)

transaction kind name = entity type name, present continuous tense of a verb
(in lower case);
Examples: rental completing, deposit paying
product kind name = “[“, entity type name, “]”, “ is ”, event type name
(in lower case);
Examples: [rental] is completed, [rental] is deposit paid

5
actor role name = entity type name, nominal form of a verb (in lower case);
Examples: rental completer, deposit payer
entity type name = noun or nominal phrase (in lower case);
Examples: rental, deposit paid rental
entity class name = noun or nominal phrase (in upper case);
Examples: RENTAL, DEPOSIT PAID RENTAL
value type name = noun or nominal phrase (in lower case);
Examples: pizza kind, car group
value class name = noun or nominal phrase (in upper case) between “{“ and “}”;
Examples: {PIZZA KIND}, {CAR GROUP}
property type name = noun or nominal phrase (in lower case);
Examples: renter, pick-up branch
attribute type name = noun or nominal phrase (in lower case);
Examples: age, daily rental rate
event type name = perfect tense of a verb (in lower case);
Examples: completed, paid

As discussed in the FI theory ([3] Chap. 5), the signifier of a conceptual thing can
be a name, a noun or a sentence, depending on the kind of thing. Moreover, a name
can be a proper name, like ‘John’ or ‘John Smith’ for a person, or an identifier like
‘TK01’ for a transaction kind, ‘2272BP’ for a postal area, and ‘069684996’ for a
Dutch Citizen ( the so-called BSN, similar to the SSN in the USA).
To avoid confusion, we put signifiers between single quotation marks, as we did
above already. For example, we write “value type ‘car group’” instead of “value type
car group”, and “car group ‘sedan’” instead of “car group sedan”.

entity reference = definite entity reference | indefinite entity reference | indirect entity
reference;
definite entity reference = entity type name, entity name;
Examples: rental ‘1089’, car ‘387462’, citizen ‘069684996’

indefinite entity reference = “ a ” | “ some^3 ”, entity type name;
Examples: a person, some car

indirect entity reference = [“ the ”], property type name, {“ of ” entity reference }- ,
[“ in ” | “ on ”, time reference];
Examples: the renter of rental ‘1089’,
the mother of the member of membership ‘387’,
the car of some rental in year ‘2019’

entity variable = “[“, entity type name , “]”;
Examples: [person], [car], [rental]

(^3) the word “some” is used here solely in its meaning of reference to an unknown thing

6 The DEMO Specification Language v4.7.

value reference = definite value reference | indefinite value reference | indirect value
reference;
definite value reference = value type name, value name;
Examples: number ‘1089’, day ‘2458270’, car group ‘sedan’

indefinite value reference = “ a ” | “ some ”, value type name;
Examples: a number, some day, a car group

indirect value reference = “ the ”, attribute type name, {“ of ” entity reference | value
reference}- , [“ in ” | “ on ”, time reference];

Examples: the weight of car ‘387462’,
the weight of the car of rental ‘1089’,
the daily rental rate of car group ‘sedan’ in the year ‘2’
value variable = “[“, value type name , “]”;
Examples: [day], [car group]

Time values are a subclass of values. Because of their special role in (entity or
value) references, they deserve special attention.

time type name = noun or nominal phrase (in lower case);
Examples: day, year
time class name = noun or nominal phrase (in upper case) between “{“ and “}”;
Examples: {DAY}, {YEAR}

time reference = definite time reference | indefinite time reference | indirect time ref-
erence;

definite time reference = time type name, time instance name;
Examples: day ‘2458270’, year ‘2000’, week ’34’

indefinite time reference = “ a ” | “ some ”, time type name;
Examples: a day, some month, a week

indirect time reference = (“ the ” time type name, {“ of ” entity reference |
value reference} | “ that ”, product kind formulation) |
“ each ” time type name “ between ” time reference “ and ” time reference;
Examples: the year of the starting day of rental ‘1089’,
the week of the ending day of rental ‘1089’,
each day between the starting day of [rental] and
the ending day of [rental]

property variable = “ the ”, property type name, {“ of ”, entity reference | property ref-
erence | value reference | attribute reference }- , [“ in ” | “ on ”, time reference];

7
Examples: the renter of [rental],
the father of the renter of [rental],
the renter of some rental on day ‘2458270’,
the month in which the car of rental ‘1089’ is taken,
the book of some loan on the ending day of rental ’12’
property assertion = property variable, “ is ” | “ is not ”, property variable | entity refer-
ence;
Examples: the renter of [rental] is the driver of [rental],
the driver of [rental] is not person ‘92637’,
the father of the driver of [rental] is not person ‘92637’

attribute variable = “ the ”, attribute type name, {“ of ”, entity variable | property vari-
able | value variable | attribute variable}- , [“ in ” | “ on ”, time reference];

Examples: the age of [person],
the daily rental rate of [car group] in [year]
the deposit amount of rental ’1089’ on day ‘2458270’,
the penalty of loan ’13901’ on the ending day of
rental ’1089’
attribute assertion = attribute variable, “ is equal to ” | “ is unequal to ” | “ is greater
than ” | “ is less than ” | “ is equal to or greater than ” | “ is equal to or less than ” ,
attribute variable | definite value reference;

Examples: the ending day of [rental] is equal to or greater than
the starting day of [rental],
the number of free cars of the car group of [rental]
on each day between the starting day of [rental]
and the ending day of [rental] is greater than
the number ‘0’

NOTE. Attribute assertions can only apply to instances of value types (or scale types)
of the sorts Ordinal, Interval, Rational and Absolute (cf. Chap. 2.4).

boolean assertion = [“ not ”], property assertion | attribute assertion;
boolean expression = boolean assertion, {“ and ” | “ or ”, boolean assertion}-;

Example:
(( the article kind of [sale] is ‘alcoholic’) and ( the age of the customer of [sale] on
the day of [sale] is equal to or greater than the minimal age for alcoholics in the
year of [sale])) or ( the article kind of [sale] is not ‘alcoholic’)

8 The DEMO Specification Language v4.7.

The logical operators not , and and or have their common meanings. In order to
avoid confusion about the order in which the parts of a boolean expression are evalu-
ated, it is recommended to use brackets.

set membership assertion = (entity reference, [“ not ”] “is in”, entity set reference) |
(value reference, [“ not ”] “is in”, value set reference);

entity set reference = entity reference, where the referred entity is a set of entity refer-
ence;

value set reference = value reference, where the referred value is a set of value refer-
ence;

Examples: person is in members
person not is in members
number is in even numbers
2.2 Declaration of types
Fact types (or types for short) can be specified graphically and textually, both on the
schema level and on the meta schema level. The graphical specification is discussed
in Chaps. 3 thru 6. Below, the textual specification is presented.

type declaration = entity type declaration | value type declaration | property type de-
claration | attribute type declaration | event type declaration;

entity type declaration = “entity type”, entity type name, “ exists ”;
Example: entity type ‘rental’ exists
value type declaration = “value type”, value type name, “ exists ”;
Example: value type ‘car group’ exists
property type declaration = “property type”, property type name, “ exists ”;
Example: property type ‘renter’ exists
attribute type declaration = “attribute type”, attribute type name, “ exists ”;
Example: attribute type ‘starting day’ exists
event type declaration = “event type”, event type name, “ exists ”;
Example: event type ‘completed’ exists

2.3 Derivation of types
Derived types can be specified graphically or textually. Examples of graphically spe-
cified derived types are discussed in Chap. 6. Examples of textually specified derived
fact types are provided below (Note: the symbol “≡” must be read as “is defined as”).
If the base type of the specified type is integer or real (cf. Sect. 2.4), the common
arithmetic operations are applicable (like addition and subtraction).

9
If the base type is boolean, thus {true, false}, boolean expressions may be con-
structed by using the logical operators and , or and not.
If the value of a derived type is a choice out of a number of values, dependent on
the current value of some variable, the case construct is used.

Examples of specifications with arithmetic operations:
the rental charge of [rental] ≡ the duration of [rental] times the daily rental rate of
the car group of [rental] in the year of the starting day of [rental],
the duration of [rental] ≡ the ending day of [rental] minus the starting day of [rental]
plus 1,

the actual duration of [rental] ≡ the day of the et of (car returning for [rental] is ac-
cepted) minus the starting day of [rental] plus 1,

the late return penalty of [rental] ≡ ( the actual duration of [rental] minus the duration

of [rental]) times ( the late return penalty in the year of the starting day of [rental])
Example of a specification with choice:
the discount percentage of [sale] ≡
case customer of [sale] is ‘golden customer’: 20
customer of [sale] is ‘silver customer’: 10
customer of [sale] is ‘incidental customer’: 0

2.4 Value types - dimensions, units and sorts
Values of variables, like the day of birth of a person, her/his length or weight, or the
sort of a transaction kind (original, informational or documental), are basically meas-
urements on a (measurement) scale.
In measure theory, these six scale sorts are commonly distinguished: Ordinal (O),
Interval (I), Rational (R), Categorial (C), Absolute (A) and Boolean (B).

Ordinal scales have no zero point and no measuring unit, they are only orderings
from less to more. A well-known example is the hardness of rocks: it is only possible
to determine that the one rock is harder than an other rock.
Interval scales do have a measuring unit but no zero point. The measuring unit can
be chosen freely. A well-known value type in this scale sort is temperature (Note, the
temperature in degrees Kelvin does have a physical zero point but it is still considered
an interval scale). Another example is time. Because of the very natural unit of a day,
all calendars are based on this measuring unit.
Rational scales have also a freely choosable measuring unit but a fixed zero point.
Well-known value types in this scale sort are length, surface, volume and velocity.

10 The DEMO Specification Language v4.7.

Categorial scales (also called nominal scales) are actually not measurement scales,
because there is no measurement unit and no zero point. They are (basically arbitrary)
distinctions. Examples are product categories in shops (like fruit, vegetables, dairy,
etc.) and car groups in a car rental company (like sedan, mini, sports car, etc.).
The Absolute scale is actually not a measurement scale. It is just counting, like the
number of apples in the basket and the number of persons in a car. Considered as a
scale, it has a fixed zero point and a fixed measuring unit.
The Boolean scale consists of the two (logical) boolean values true and false.
In Table 2.1, the standard value types are presented. One may assume that they are
always present. So, there is no need to define them explicitly in a DEMO model.

value dimension measuring base scale
type unit type sort

time TIME Julian day, hour, minute... integer I
duration TIME number of days, .. integer A
amount MONEY dollar ($), euro (€), ... real R
mass MASS ... kg, g, mg, ... real R
length LENGTH ... m, cm, mm, ... real R
area LENGTH^2 ... m^2 , cm^2 , mm^2 , ... real R
volume LENGTH^3 ... m^3 , cm^3 , mm^3 , ... real R
velocity LENGTH/TIME ... m/s, ... real R
temperature TEMPERATURE oC, oF, K real I
number NUMBER < not applicable > integer A
truth value BOOLEAN < not applicable > {true, false} B
sort SORTAL < not applicable > {O, I, D} C

Table 2.1 Dimensions, units and sorts of value types
Value classes are formulated as follows in BNF: “{“, dimension name, “ : ”, unit
name, “}”. Examples are {MONEY : euro}, {MONEY : €}, {TEMPERATURE :
oC}, {TEMPERATURE : K}. It is allowed to omit the unit, and thus to only indicate

the dimension. For example: amount {MONEY}. It is also allowed to abbreviate
to if no confusion can arise. Then, the unit is written in
capitals. For example: {JULIAN: day} may be abbreviated to {DAY}.
The value type ‘sort’ regards the sort of organisation according to the ALPHA the-
ory [3], so the distinction between the O-, I- and D-organisation.

2.5 Representing time values
Time values, like the day of birth of a person and the starting day of a car rental, are
basically measured on the Julian time scale. Next to this scale, time units from the
Gregorian Calendar, like year and month, may be used. The conversion between the

11
Julian scale and the Gregorian Calendar is based on the converter of the US Navy^4.
So, in expressions like “the first day of the next month (from now)” and “the year of
the starting day of [rental]”, the values of month and year on the Julian time scale are
calculated by means of this converter. Note that the value of the universal variable
‘now’ is also a value on the Julian time scale.
The preciseness with which time values are measured and represented depends on
the situation at hand. In normal enterprise situations, the smallest unit is probably the
second. For example, the Julian value of ’30 April 2019 12:00 hours, 0 minutes and 0
seconds’ is ‘2458604.000000’, and the Julian value of ’30 April 2019 12:00 hours, 0
minutes and 1 second’ is ‘2458604.000012’.

2.6 The four aspect models
The essential model of an enterprise in DEMO consists of the integrated whole of
four aspect models, each taking a specific view on the enterprise’s O-organisation: the
Cooperation Model, the Action Model, the Process Model and the Fact Model. The
relationships between the four models is illustrated in Fig. 2.1. Instead of enterprise,
we will use the notion of Scope of Interest (SoI). A SoI may be a part of an enterprise,
but it may also comprise (parts of) several enterprises. Within a SoI, one may choose
a focus. It is the part of the SoI of which one wants to produce the complete essential
model. It includes in particular all action rules of the contained actor roles.

Fig. 2.1 The integrated four DEMO aspect models
The Cooperation Model (CM) of a SoI is a model of the cooperation between its
actors (cf. [3] Chap. 10), or, following Chap. 9 in [3]), the construction of the SoI, i.e.
of the transactor roles and the coordination structures among them.

(^4) https://aa.usno.navy.mil/data/docs/JulianDate.php

12 The DEMO Specification Language v4.7.

The Action Model (AM) of a SoI is a model of its operation , i.e. the manifestation
of the construction in the course of time (cf. [3] Chaps. 8 and 9). It comprises action
rules and work instructions.
The Process Model (PM) of a SoI is a model of the (business) processes (consist-
ing of transaction steps and process links between them) that take place as the effect
of the activity of actors (cf. [3] Chap. 8). In systemic terms, it is a specification of the
state space and the transition space of the coordination world (cf. [3] Chap. 9).
The Fact Model (FM) of a SoI is a model of the products (clusters of independent
fact types and their dependent fact types) of the SoI that actors bring about (cf. [3]
Chap. 8). In systemic terms, it is a specification of the state space and the transition
space of the production world (cf. [3] Chap. 9).
As illustrated by the triangular shape in Fig. 2.1, and the division of this shape in
the four aspect models, the CM and the AM cover both coordination and production,
the PM regards only coordination and the FM only production. The PM connects the
CM and the AM, as far as the coordination between actors is concerned. The FM does
so as far as production is concerned. The AM constitutes the solid basis on which the
other three models are firmly standing. As a matter of fact, the CM, PM and FM are
already ‘contained’ in the AM, they only need to be ‘extracted’ from it. Lastly, there is
nothing ‘above’ the CM. Figs. A.1 through A.3 contain the combined conceptual
schemata of the CM, the AM and the PM, expressed in GOSL (cf. [3] Chap. 6). Fig.
A.2 contains the meta schema of the FM. Every instance of the meta schema, so every
FM, is itself a schema, namely of the production world of the modelled SoI. The CM,
PM, and AM are formally defined in Figs. 17 through 25.

Fig. 2.2 Ways of expressing the four aspect models
Fig. 2.2 presents the ways in which the aspect models are expressed, in diagrams,
tables and formal textual expressions. The Bank Access Table (BAT) is an alternative
way of expressing the interstriction structure (cf. Chap. 3). Therefore it is put on the

Object Fact
Diagram
OFD
DFS
Derived Fact
Specifications
Process Structure
Diagram
PSD
TPD
Transaction Process
Diagram
CUT
Create Use Table
TPT Transactor Product Table
BCT Bank Contents Table
ADT
Authorisation Delegation Table
Coordination Structure Diagram
CSD
ARS
Action Rule
Specifications
WIS
Work Instruction
Specifications
BAT Bank Access Table
13
left side of Fig. 2.2. The other tables, shown on the right side, are so-called cross
model tables: each of them represents a specific relationship between two aspect
models. The set of cross-model tables is by no means exhaustive: one may freely
define new ones if there is a need. The presented tables are just the ones that are
commonly used in practice. In addition, alternative diagrams may be developed to
express the four models. The ADT is a special kind of table; it connects the AM to the
implementation of the SoI. It regards specifically the assignment of actor roles to de-
partments or functionaries.

14 The DEMO Specification Language v4.7.

3 Expressing the Cooperation Model (CM)
3.1 The Coordination Structure Diagram
The Coordination Structure Diagram (CSD) is the graphical way of expressing the
CM of a SoI. Its legend is exhibited in Figs. 3.1 and 3.2. The upper left part of Fig.
3.1 shows the elementary and the self-activating transactor roles. The shapes and con-
structs in the lower part of Fig. 3.1 are considered to be sufficiently explained in the
figure. The constructs hold for each of the three sorts of organisations as distinguished
in Chap. 11 of [3]: O-organisations, I-organisations, and D-organisations.

Fig. 3.1 Legend of the Coordination Structure Diagram (1)
The focus within a SoI is indicated in a CSD by colouring the actor role shapes
outside the focus light-grey. The transactor roles inside the focus are called internal ,
and the transactor roles outside are called environmental (if there is interaction with
an internal actor role) or external otherwise (cf. [3] Chap. 9). There are three coordin-
ation structures among transactor roles: the interaction structure, the interstriction
structure, and the interimpediment structure.
The interaction structure consists of initiator links, represented by solid lines from
actor role shapes to transactions kind shapes. A cardinality range (k..n) may apply.
Through this structure, trees of transactor roles emerge, as illustrated by Fig. 3.3. It is
the CSD of the case GloLog (cf. [3], Chap. 18). By definition, the top of such an in-
teraction tree is a self-activating transactor role (cf. [3], Chap. 10). The organisation
of a SoI, often contains only subtrees of such trees. Then, the cut-off upper part is
represented by a composite transactor role.
The interimpediment structure consists of wait links from transaction kinds to actor
roles. A wait link expresses that actors in the connected actor role have to wait for a
specific progress in transactions of the connected transaction kind before they can
proceed their work (in their own transactions). In other words, the initiators or ex-
ecutors of these transactions impede actors in the connected actor role to carry on as
long as the wait condition holds. A wait link is indicated by a dotted arrow from a

15
transaction kind shape to the shape of the impeded actor role. The interimpediment
structure constitutes the process dependencies among the corresponding transaction
processes: the acts of the connected actors depend on the progress of the connected
transaction processes.
If one abstracts from the realisation of the O-organisation of a SoI, and thus aims at
producing its essential model (cf. [3], Chap. 11), a third coordination structure comes
on the scene. This interstriction^5 structure consists of access links from actor roles to
transaction kinds, which are now conceived as transaction banks. Access links are the
ontological abstraction of the sharing transaction kinds between the O-organisation
and the I-organisation of the SoI (cf. [3], Chap. 11). An access link expresses that act-
ors in the connected actor role have reading access to the contents of the transaction
bank (both to the C-facts and to the P-facts). Access links are indicated by dashed
lines between actor role shapes and transaction kind shapes. The interstriction struc-
ture constitutes the state dependencies among the corresponding transaction pro-
cesses: the acts of the connected actors depend on the current state of the connected
transaction processes, represented by the facts in the transaction bank. Actors have
always access to the banks of transaction kinds in which they are initiator or executor.
The other transaction kinds between the O- and the I-organisation, so the remem-
bering transaction kinds are abstracted from by considering the facts that are created
by the initiator and the executor of a transaction to be stored in the transaction bank.
On the right side of Fig. 3.1, it is shown how external and environmental transactor
roles are indicated, namely by colouring the shapes light-grey. The right side of Fig.
3.2 shows how external (multiple) transaction kinds are indicated.

Fig. 3.2 Legend of the Coordination Structure Diagram (2)
(^5) “restriction” originates from the Latin verb “stringere”, meaning trimming, curtailing. The
word “interstriction” expresses that actors restrict each others decision freedom or ‘play area’.
j j
actors ARiare executor of
original transactions TKj
j j
actors ARiare executor of
informational transactions TKj
j j
documental transactions actors ARiare executor ofTKj
j
transaction kind multiple originalMTKj
j
multiple informational
transaction kind MTKj
j
transaction kind multiple documentalMTKj
j
j
j
j
external multiple original
transaction kind MTKj
j
k k
j
there are several actor
roles inside CTARk
there is an elementary
actor role ARjinside CTARk
k external compositetransactor role CTARk
j
composite
transactorrole CTARk
a CTAR comprises a networkof interlinked transactorroles
k

16 The DEMO Specification Language v4.7.

Fig. A.5 shows the fact types in the schema of the CM of which instances are ex-
pressed in a CSD: the entity types ‘transaction kind’, ‘actor role’, their combination in
the concept of ‘transactor role’, as well as the entity types ‘composite transactor role’
and ‘multiple transaction kind’, and the property types ‘executor link’, ‘initiator link’,
‘access link’, ‘wait link’ and ‘is part of’.
As an example, the CSD in Fig. 3.3 contains 18 transactor roles. Three of them are
self-activating: TAR11, TAR12 and TAR13. There is one composite transactor role:
CTAR01. The fourteen initiator links constitute the interaction structure. Next, there
are four wait links: one from TK02 to AR10, one from TK03 to AR14, one from
TK07 to AR15, and one from TK15 to AR17, together constituting the interimpedi-
ment structure. Lastly, there are three access links: one from AR11 to TK01, one from
AR12 to TK03, and one from AR13 to TK14, together constituting the interstriction
structure. Note that the access links to external information sources are omitted. Oth-
erwise, there would have been many more access links.

Fig. 3.3 The three coordination structures in the GloLog enterprise
3.2 The Bank Access Table
A CSD may be supplemented by a Bank Access Table (BAT), as the alternative rep-
resentation of the interstriction structure of a SoI. A BAT is particularly suitable if
there are many access links, whose expressions in a CSD would lead to a mess of
crossing dashed lines. Table 3.1 shows the BAT of the Library organisation (cf. [3],
Chap. 16). A “U” (from Uses) indicates that there is an access link from the actor role
(in the row) to the transaction bank (in the column). The access links from the execut-
or and initiator roles to transaction kinds are indicated respectively by “Ex” and “In”.
As said, both the initiator and the executor of a transaction have access to the facts
that are produced in transaction process of the transaction kinds in which they fill the
initiator role or the executor role.
Fig. A.11 shows the fact types in the schema of the CM of which instances are ex-

pressed in a BAT: the entity types ‘transaction kind’, ‘multiple transaction kind’, ‘act-
or role’ and ‘composite actor role, and the property types that determine the existence
of executor links, initiator links and access links. The executor links and initiator links
are included because they imply the existence of an access link.

completersale
CTAR
client
transportersale
purchase completer
purchase
11
controller
01
10
02
purchaseloader purchaseshipper
03 17 07
containercontent
transporter
containercontent
loader
16 08
13
containercontent
unloader
09
land transport completer
15
land transport
controller
purchasereleaser contentship
loader
contentship
unloader
contentship
transporter
sea transport
controller
04
12
05 06
sea transport completer
14
1..*
0..* 0..* 0..*
1..*
17
Table 3.1 BAT of the Library organisation
Library: Bank Access Table
Bank
Actor

TK01 TK02 TK03 TK04 TK05 TK06 TK07 TK08 TK09 MTK01 MTK02 MTK
AR01 Ex In U U U
AR02 Ex U
AR03 U In In, Ex U U U
AR04 U Ex U U U U
AR05 U In In, Ex U U
AR06 U U Ex In In In U U U
AR07 Ex U
AR08 Ex U
AR09 Ex U
CTAR01 In In U
CTAR02 In U

18 The DEMO Specification Language v4.7.

4 Expressing the Process Model (PM)
4.1 The Transaction Pattern Diagram
The Transaction Pattern Diagram (TPD) is the graphical way of expressing the struc-
ture of transactions of some transaction kind. The legend of the TPD is exhibited in
Fig. 4.1.

Fig. 4.1 Legend of the Transaction Pattern Diagram (TPD)
Fig. 4.2 contains the TPD of the Complete Transaction Pattern (CTP), as presented
and discussed in [3], Chap. 8.

19
Fig. 4.2 TPD of the complete transaction pattern (CTP)
4.2 The Process Structure Diagram
The Process Structure Diagram (PSD) is the graphical way of expressing the structure
of a business process kind. The legend of the PSD is exhibited in Fig. 4.3. It also
shows the general shape of a transaction kind in a Process Structure Diagram (PSD).

Fig. 4.3 Legend and general shape of the PSD
The sausage-like shape arises from stretching the disk shape horizontally. One
must imagine that there is a (non-proportional) linear time axis from left to right. The
sort of the shown transaction kind is original, indicated by the red diamond (cf. Fig.
4.3). As discussed in [3], Chap. 8, a transaction proceeds in three phases: the order
phase (to the left of the diamond), the execution phase (the diamond), and the result
phase (to the right of the diamond). The state “in” is the initial state of the transaction
process; it is some state in some transaction process. The indicators of the other states,

initiator
executor
rq+
?
rf
al
rvrq
rf
al
in
rvrq
>
rf rf
al
initiator
?
al
rvac
da
rvac
>
ac
executor
executor
initiator
pm+
?
al
rf
pmrv
al
rf
pmrv
rq
>
al al
rf
executor
?
rf
rvda rvda
initiator
da+
pm
>
dc
rq
rq
pm
pm da
ac da
in
initiator
executor
ac rj
dc rj
0..
0..
rv: revoke(d)
al: allow(ed)
rf: refuse(d)
rv: revoke(d)
al: allow(ed)
rf: refuse(d)
20 The DEMO Specification Language v4.7.

as well as the indicators of the presented C-acts, are arbitrarily chosen letters. In order
to show that response links and wait links can apply both to the order phase and to the
result phase, they are drawn on both sides (u, v, w for the order phase, and x, y, z for
the result phase). The P-act (named TKi/ex, “ex” from “execute”) is indicated by a
grey-coloured small box.
In a PSD, only those C-act kinds and C-fact kinds are shown that are connected to
other transaction processes by means of response links or wait links (cf. Fig. 4.3). The
shapes of C-act kinds (the small boxes) that are performed by the initiator are drawn
on top of the ‘sausage’, so within the responsibility area of the initiator, whereas the
shapes of C-act kinds that are performed by the executor are drawn at the bottom, so
within the responsibility area of the executor, as is the shape of the P-fact kind (the
small grey box). In principle, the same rule holds for the shapes of C-fact kinds (the
small disks). So, the shapes of C-fact kinds created by the initiator are drawn on the
top of the ‘sausage’, and the shapes of C-fact kinds created by the executor are drawn
at the bottom. However, to avoid that the drawing of response links and wait links
become a mess, it is allowed to put the shapes of C-fact kinds on either side. For the
same reason, one may duplicate the shapes of C-act and C-fact kinds. The states xx
and yy represent states from which the revoke request or revoke promise, and the re-
voke declare or revoke accept are performed respectively.
The response links in Fig. 4.3 from C-fact kinds to (unspecified) C-act kinds are
called initiation links. By definition, they start from the shape of a C-fact kind and end
in the shape of the request act of some transaction kind. A C-fact kind may have sev-
eral outgoing initiation links, meaning that transactions of several transaction kinds
are initiated from it. Similarly, a C-fact kind may have several outgoing wait links. It
means that the occurrence of an event of the C-fact kind is a wait condition for the
performance of acts of several C-act kinds. Likewise, a P- or C-act kind may have
several incoming wait links. It means that performing the act has to wait for the oc-
currence of all of these coordination events.
Cardinality ranges apply to response links and to wait links. A cardinality range
k .. n for a response link means that the C-act at the arrow side is performed a minim-
um number of times k and a maximum number of times n. The default value of k and
n is 1; default values are commonly omitted in a PSD. Likewise, a cardinality range
k .. n for a wait link means that performing the C- or P-act at the arrow side is post-
poned until a minimum number of k and a maximum number of n C-events at the
shaft side have occurred. The default value of k and n is again 1; default values are
commonly omitted in a PSD.
In order to illustrate the cardinality ranges in a PSD, Fig. 4.4 exhibits one of the
PSDs from the case Rent-A-Car (cf. [3], Chap. 15). It shows in addition how self-ac-
tivation is expressed in a PM, namely by a response link from the state requested (rq)
to the act request [rq]. It means that the request for the next carrying out of a transac-
tion TK07 is created immediately after the initiation of the current one. In this way,
the self-activation of actor AR07 is not dependent on the carrying out of any of the
enclosed transactions TK08.

21
Fig. 4.4 PSD of the car transportation process in the case Rent-A-Car
Fig. A.7 shows the fact types in the schema of the PM of which instances are ex-
pressed in a PSD: the entity types ‘transaction kind’, ‘actor role’, ‘transaction kind
step kind’ and ‘general step kind’, as well as the property types ‘executor link’, ‘initi-
ator link’, ‘response link’ and ‘wait link’. One should always keep in mind that every
‘sausage’ contains the complete transaction pattern.
In order to show precisely the connections to and from other transaction kinds, the
PSD of a SoI may be supplemented by a number of Transaction Process Diagrams
(TPD). An example of the use of a TPD in the case Volley is exhibited in Fig. 4.5. It
shows precisely the connections between the transaction kinds TK01 and TK02. To
save space, only the standard pattern of TK01 is shown. The connections between the
patterns of transaction kinds TK01 and TK02 are indicated in orange. In response to
the event (TK01/pm), the act [TK02/rq] is performed. The performing of the P-act
[TK01/ex] has to wait for the occurrence of the C-event (TK02/ac).

Fig. 4.5 The use of a TPD as a supplement to a PSD
From the PM of a SoI, one can derive the skeleton or template of every applicable
Action Rule Specification (ARS), to be discussed in Chap. 5. For example, one can
drive from the PSD in Fig. 4.3 that there is an ARS of which the event part contains a
when clause concerning the C-event (TK07/pm) and the response part contains the
performance of a number of C-acts [TK06/rq], possibly zero; there is no else clause.
As another example, to be derived from the TPD in Fig. 10, is that there are two
ARSs with (TK01/pm) in the when clause, of which one has an additional while
clause regarding (TK02/ac).

rq
rq pm 07
06 ac
0..* 0..*
06
completertransport
transport
manager
07
transportmanager
rq pm
transport completing
transport managing
dc
rq
rq
pm
pm da
ac da
in
initiator
executor
ac rj
dc rj
0..1
0..1
TK02ac
TK02rq
22 The DEMO Specification Language v4.7.2

5 Expressing the Action Model (AM)
5.1 The Action Rule Specification (ARS)
Action rules guide actors in responding to coordination events. In principle, there is
an Action Rule Specification (ARS) for every combination of a coordination event
kind (whose occurrences have to be responded to) and a specific wait condition (if
applicable). As an example from the case Rent-A-Car (cf. [3], Chap. 15), the action
rule specifications ARS-3, ARS-7 and ARS-9 all apply to the event kind TK01/pm,
but with different additional while-conditions.
An ARS specifies the facts in the production world and/or the coordination world
whose presence or absence in the current state of the world must be assessed, as well
as the (production and/or coordination) acts that must be performed, depending on the
outcome of the assessment. As discussed in [4], action rules are imperative business
rules that operationalise declarative business rules, which are the existence laws in the
PM and the FM, thus the rules that determine the state space of the world of the SoI.
An action rule consists of three sequential parts: the event part, the assess part and
the response part. As an example, Fig. 5.1 shows the specification of the action rule
from the case Volley (cf. [3], Chap. 12), in which the request for membership starting
is dealt with. The three parts are highlighted by background colours.

Fig. 5.1 Example of an Action Rule Specification (ARS)
According to the syntax diagram in Fig. 5.2, the assess part comprises three sub
parts: the rightness condition, the sincerity condition, and the truth condition. Each of
them consists of a number of assertions, separated by the symbol “;”. An assertion is
either a property assertion or an attribute assertion (cf. Chap. 2.1)).
In the rightness condition, the assertions regard the two participants in the coordin-
ation event, thus the performer and the addressee. Assertions in the sincerity condition
regard only the performer. Assertions in the truth condition regard the state of the
production world and/or the coordination world. The formula example above regards
the production world of the Volley organisation.

23
Action rules are specified in Action Rule Specifications (ARSs). Figs. 5.2 through
5.4 contain the syntax diagrams that define the syntax of an ARS.
Fig. 5.2 Syntax diagram of the event part of an action rule
Fig. 5.3 Syntax diagram of the assess part of an action rule (1)
24 The DEMO Specification Language v4.7.2

Fig. 5.4 Syntax diagram of the assess part of an action rule (2)
Fig. 5.5 Syntax diagram of the assess part of an action rule (3)
Fig. 5.6 Syntax diagram of the response part of an action rule
NOTE. For the sincerity division (cf. Fig. 5.4), there is only one option: * no specific
condition *. This expresses the practical impossibility to specify in advance what the
addressee should check.
With “performer of C-event reference in when clause” in the last line in Fig. 5.6,
we refer to the actor who has performed the C-act that resulted in the C-event in the
when clause, as specified in Fig. 5.2. It is recommended to refer to this performer by
“the performer of the”, followed by the event kind (request, promise, etc.).

25
As said before, whether the response part of an action rule may contain the else
clause, is determined by the CTP (cf. Fig. 4.2). It only occurs if the C-event in the
when clause is a request, a declare, a revoke-request, a revoke-promise, a revoke-de-
clare, or a revoke-accept.

5.2 The Work Instruction Specification (WIS)
Work instructions guide the executor of a transaction in performing the production
act. They can be expressed in natural language or e.g. in work flows. Note that such
work flows do not represent business processes but processes in the production world.
If there are no WISs for a SoI, it means that the actors are supposed to use their pro-
fessional knowledge and skills in bringing about the products.

26 The DEMO Specification Language v4.7.2

6 Expressing the Fact Model (FM)
6.1 The Object Fact Diagram (OFD)
The Object Fact Diagram (OFD) is the graphical way to express the FM of a SoI. In
order to understand the relationships between the schema level and the instance level
of the conceptual model of a world, we start this chapter with presenting a few basic
notions from mathematical set theory, notably the notion of (mathematical) function.
The common way of representing sets in set theory is the Venn Diagram. In such a
diagram, the shape of a set is an oval; symbols within the oval represent elements of
the set (cf. Fig. 11). The common way of representing functions (or binary relations in
general) is to extend the Venn Diagram with connections between the elements of two
(not necessarily different) sets. One set is called the domain of the function, the other
one the range. A function maps the elements in the domain to the elements in the
range. Fig. 6.1 exhibits an extended Venn Diagram, representing the function ‘has as
renter’, having as domain the class RENTAL and as range the class PERSON.

Fig. 6.1 Extended Venn diagram of a (mathematical) function
The OFD is derived from this extended Venn Diagram: it consists of classes and of
mappings between them. The classes are either entity classes (i.e. sets of concrete
entities of the same type) or value classes (i.e. sets of values of the same type, cf. [3],
Chap. 5). The shape of a set or class in an OFD is a roundangle (the name is a con-
traction of “rounded rectangle”). The mappings between these classes represent prop-
erty types or attribute types.
Property types are indicated by directed lines between entity classes. As an ex-
ample in Fig. 12, the property type ‘the member of [membership] is [person]’ is a
function that maps the class MEMBERSHIP to the class PERSON. One should ima-
gine that the line between the roundangles represents the set of connections between
elements in MEMBERSHIP and elements in PERSON. The “>” indicates that MEM-
BERSHIP is the domain of the function and PERSON the range.

RENTAL PERSON
r 1
r 2
r 3
p 2
p 1
p 3
has as renter: RENTAL -> PERSON
has as renter(r 1 )=p 1
has as renter(r 2 )=p 2
has as renter(r 3 )=p 2
>
>
>
p 4
The FM and set theory (2)
27
Attribute types are indicated in a simpler way. This is possible because they are
always pure (mathematical) functions, i.e. functions of which the cardinality range at
the domain side is 0..*, and at the range side 1..1. The name of the attribute type is
written in the roundangle of the (entity or value) class that is its domain. To the right
of it, the name of the value class that is the range. To avoid confusion, the name of a
value class is written, between “{“ and “}”. The name of the class and the list of at-
tribute types of which it is the domain, is separated by a dotted line (cf. Fig. 12).

Fig. 6.2 OFD of the Volley organisation
Production event types are indicated by diamonds, the universal symbol of produc-
tion (cf. [3], Chap. 8). They are expressed as a unary predicate concerning an entity
class. For example, the event type ‘the first fee of [membership] is paid’ concerns the
entity type membership (or the entity class MEMBERSHIP). An event type in the FM
is identical to a product kind in the CM. Therefore, the numeral part of the product
kind identifier (e.g. 02) is written in the diamond of the event type.
The entity class that an event type concerns may be an aggregation of two or more
entity types. This the way to deal in DEMO with seemingly binary event types (or
event types of an even higher arity). An example of it can be found in the case Library
(cf. [3], Fig. 16.9).
Derived entity types can often be specified graphically. It is done in Fig. 6.2 for
‘started membership’ and ‘paid membership’, in order to specify very precisely the
attribute types ‘starting day’ and ‘amount paid’: both are functions with as domain the
entity classes STARTED MEMBERSHIP and PAID MEMBERSHIP respectively.
Standard value classes like DAY and MONEY are assumed to be implicitly present in
every OFD (cf. Chap. 2.3). The value class YEAR is explicitly included in the OFD in
Fig. 6.2 for specifying the attribute types that have YEAR as their domain: ‘minimal
age’, ‘annual fee ‘ and ‘max members’.
In Fig. 6.3, a part of the OFD of the GloLog organisation ([3], Chap. 18) is exhib-
ited in order to show how sets are graphically specified. The entity class SET OF
SALE id graphically specified by drawing a roundangle around the roundangle of

MEMBERSHIP PERSON
02
day of birth {DAY}
amount paid {MONEY}
PAID MEMBERSHIP {YEAR}
minimal age {NUMBER}
annual fee {MONEY}
max members {NUMBER}
the member of
>
[membership] is [person]
the first fee of
[membership] is paid
01 [membership] is started
the payer of
>
[membership] is [person]
starting day {DAY}
amountopay{MONEY}
STARTED MEMBERSHIP
28 The DEMO Specification Language v4.7.2

SALE. Conversely, every individual sale is a member of a purchase. Another example
of the use of the set-of construct can be found in Fig. A.4.

Fig. 6.3 part of the OFD of the GloLog organisation
An OFD also exhibits the existence laws that can conveniently be specified graph-
ically (cf. [3], Chap. 6). For example, the OFD in Fig. 6.2 shows that the domain of
the property type ‘the member of [membership] is [person]’ is the class MEMBER-
SHIP and that the range is PERSON. In addition it shows that every membership has
exactly one person as its member, whereas a person can be member in 0, 1 or more
memberships. This follows from the (default) cardinality range.
External entity classes, like PERSON, are coloured light-grey. It means that per-
sons are ‘created’ outside the focus of the SoI. But it must be possible to inspect their
existence and to use their properties and attributes. All standard value classes are ex-
ternal, as discussed before, and thus also coloured light-grey. For the complete legend
of the OFD, the reader is referred to [3] Sect. 6.3.3. Fig. A.4 presents the meta schema
of the FM. As one may expect, it is identical to the general meta schema in conceptual
modelling (cf. [3], Chap. 6).

6.2 Derived Fact Specification and Existence Law Specification
As said, derived fact types (of all kinds) that cannot be specified graphically, must be
specified textually. In the case Volley, there are three attribute types that have to be
specified textually. It is done in Fig. 6.4. Days are values in the Julian time dimension
(cf. Table 1). So, the age of a person is expressed in the number of days that the per-
son exists. If needed, it can be transformed to years in the Gregorian calendar or in
any other calendar (cf. Chap. 2.4).
Fig. 6.4 also contains the existence laws that apply to Volley. Existence laws are
the declarative counterparts of the (imperative) business rules or action rules that are
discussed in Chap. 4. Action rules, or imperative business rules in general, are the
operationalisation of declarative business rules, which are first order logical formulas
concerning the production world of a SoI [4]. Existence laws that cannot be specified
graphically, should be specified as formal texts.

[sale]
is completed
the client < of SALE
[sale] is [client]
CLIENT
ARTICLE
the article of
<
[sale] is [article]
PURCHASE
[sale]
is transported
[purchase]
is completed
[purchase]
is loaded
[purchase] contains
<
[set ofsale]
01 10 02 03
[purchase]
is shipped
[purchase]
(^1707) is released

29
An example of such an existence law in the Volley organisation is that members
must at least have the age of 12 years. This is formally expressed in Fig. 6.4 in the
second existence law.
As discussed in [3], Chap. 12, the state space and the transition space of the co-
ordination world of a SoI are fully determined by its PM. Moreover, the transition
space of the production world of a SoI is fully determined by the transition space of
the corresponding coordination world: a P-fact starts to exist at the time that the ac-
cept act in the corresponding transaction is performed.

Fig. 6.4 Derived Fact and Existence Law Specifications of the Volley organisation
30 The DEMO Specification Language v4.7.2
7 Cross-Model Tables
Cross-Model Tables are tables that represents a specific relationship between two as-
pect models. In this chapter, we present and discuss the cross-model tables that are
shown in Fig. 2.2. This set is by no means exhaustive: one may freely define new
cross-model tables if need be.
7.1 The Transactor Product Table (TPT)
According to the OER method ([3], Chap. 12), the CSD of a SoI is mandatorily sup-
plemented by a Transactor Product Table (TPT), for the sake of formulating product
kinds formally and properly. A TPT is a table of transaction kinds with their corres-
ponding product kinds and executing actor roles. It connects the CM and the FM of a
SoI. The syntax of a TPT entry is specified as follows in EBNF:
TPT entry = (transaction kind id, transaction kind name), (product kind id, product
kind formulation), (actor role id, actor role name);
product kind formulation= entity variable | property variable | attribute variable, “ is ”,
perfect tense verb;
Examples of product kind formulations are:
[rental] is contracted
the car of [rental] is returned
the fee of [membership] in [year] is paid
Fig. A.9 shows the fact types in the schema of the CM of which instances are ex-
pressed in a TPT: the entity types ‘transaction kind’, ‘product kind’ and ‘actor role’,
and the property types that determine the product kind of each transaction kind as
well as its executing actor role. Because the product kinds are identical to the P-event
types in the FM, the TPT is called a cross-model table; it bridges the CM and the FM.
Table 7.1 exhibits the TPT of the case Rent-A-Car (cf. [3], Chap. 15).
Table 7.1 TPT of the Rent-A -Car organisation
7.2 The Bank Contents Table (BCT)
A Bank Contents Table (BCT) connects the CM and the FM of a SoI. It shows the
fact types of which instances are contained in the corresponding transaction banks.
The order in which the fact types are listed is: entity class (if not already existing), the
P-event type that concerns the class, corresponding property types and attribute types.
DEMOSL 4.4 slide 14 ©2019

Legend of the Transactor Product Table
The TransactorProduct Table (TPT) is a table of transaction kinds with the corresponding product kinds and
executor roles. The syntax of a TPT entry is specified in EBNF as follows:
TPT entry = transaction kind id, transaction kind name, product kind id, product kind formulation, actor role id,
actor role name;
product kind formulation= entity variable | property variable | attribute variable, “ is ”, perfect tense verb;
Example: [rental] is contracted
Example: the car of [rental] is returned
Example: the fee of membership in [year] is paid
Example TPT (from case Rent-A-Car):
transaction kind product kind executor role
TK01 rental completing
TK02 car taking
TK03 car returning
TK04 deposit paying
TK05 invoice paying
PK01 [rental] is completed
PK02 the car of [rental] is taken
PK03 the car of [rental] is returned
PK04 the deposit of [rental] is paid
PK05 the invoice of [rental] is paid
AR01 rental completer
AR02 car taker
AR03 car returner
AR04 deposit payer
AR05 invoice payer
31
The syntax of a BCT entry is specified as follows in EBNF:
BCT entry = (transaction kind id, transaction kind name) | (multiple transaction bank
id, multiple transaction bank name), (entity class name | product kind formulation |
property variable | attribute variable);

Table 7.2 BCT of the Volley organisation
Table 7.2 exhibits the BCT of the case Volley (cf. [3], Chap. 12). The fact types are
grouped according to the transaction banks in which their instances are stored. P-fact
types whose instances are used within the SoI but created outside it, are also listed in
the BCT. Because one commonly doesn’t know the specific transaction kind in whose
instances they are created, a multiple transaction bank is conceived. Fig. A.10 shows

the fact types in the schema of the CM of which instances are expressed in a BCT: the
entity types ‘transaction kind’, ‘multiple transaction kind’ and ‘P-fact type,’ and the
property type that determines which facts are contained in which transaction bank.

7.3 The Create Use Table (CUT)
A Create Use Table (CUT) is a cross-model table that connects the PM and the FM. It
shows in which transaction steps instances of the fact types in the FM are created and
in which steps they are used. The contents of a CUT is fully determined by the AM of
the considered SoI.
The syntax of a CUT entry is specified as follows in EBNF:

CUT entry = entity class | value class | P-fact type, C-act kind | “” | “” | “” , [C-fact kind];

As an example, Table 7.3 shows the CUT of the case Volley. All fact types, so en-
tity types, value types, event types, property types and attribute types, that are spe-
cified in the FM, are listed in the first column of the table. In the second column one
indicates the acts by which facts of the type in the left column are created. For fact

bank independent/dependent facts
TK01 membership starting
TK02 membership paying
MTK01 persons facts
MTK02 Volley facts
MEMBERSHIP
[membership] is started
the starting day of [membership]
the member of [membership]
the amount to pay of [membership]
the first fee of [membership] is paid
the amount paid of [membership]
PERSON
the day of birth of [person]
YEAR
the minimal age in [year]
the annual fee in [year]
the max members in [year]
32 The DEMO Specification Language v4.7.2
types whose instances are contained in external transaction banks, the indication is
“<given externally>”. For fact types whose instances are provided as input values in
the with-clause of the when-clause of an action rule concerning the C-event type in
the third column, the indication in the second column is “<provided as input>”. De-
rived fact types are indicated by “<derived>”. They must be included in the Derived
Fact Specifications, as part of the FM. In the third column one indicates the C-event-
type during the settlement of whose instances, facts of the type in the left column are
used.
Table 7.3 CUT of the Volley organisation
Concerning the creation of entities, like memberships in the Volley organisation,
some additional explanation is needed. A new instance of membership is created as
soon as an act [TK01/rq] is performed (cf. [3], Chap. 8). It happens at the moment
that the addressee of the act has understood the message up to the performs level (cf.
[3], Fig. 8.5). It is the addressee who then creates a new membership, together with
the properties and attributes that are provided as input: the member, the payer and the
starting day. Note that no new membership is created when the request is performed
as a consequence of settling a revoke; the membership then exists already, only some
properties or attributes may change.
7.4 The Authorisation Delegation Table (TPT)
In order to show precisely the delegations of authority (cf. [3], Chap. 8), one may
produce an Authorisation Delegation Table (ADT). An ADT bridges the AM and the
implementation of the SoI, in particular the assignment of tasks (T) to task performers
(P). The definition of the ADT is presented in Fig. A.13.
DEMO-SL v4.8 slide 23 ©2021

P-fact type created in performing used when settling
MEMBERSHIP
PAID MEMBERSHIP
PERSON
YEAR
[membership] is started
the first fee of [membership] is paid
the member of [membership]
the payer of [membership]
the starting day of [membership]
the day of birth of [person]
the minimal age in [year]
the max members in [year]
the annual fee in [year]
the amount to pay of [membership]
the amount paid of [membership]
the first fee of [membership]
the number of members on [day]
the age of [person] on [day]
TK01/rq
<derived>
<given externally>
<given externally>
TK01/ac
TK02/ac
<provided as input>
<provided as input>
<provided as input>
<given externally>
<given externally>
<given externally>
<given externally>
TK02/rq
TK02/da
<derived>
<derived>
<derived>
TK01/pm
TK01/rq, TK01/pm
TK01/rq, TK01/pm, TK01/da
TK01/rq
TK01/rq
TK01/rq
TK01/rq
TK01/rq
TK02/da
TK01/rq, TK02/da
TK01/rq
TK01/rq
PM: legend of the Create Use Table
33
A distinction is made between a global and a detailed ADT. The columns of an
ADT represent tasks (T), ranging from coordination acts to actor roles. The rows rep-
resent the task performers (P), ranging from functionaries to complete enterprises. An
“A” at the crossing of a column and a row indicates that the performer is authorised to
perform the task, a “D” that he/she has delegated authority.
Table 7.4 exhibits the detailed ADT of the case Volley [3]. It shows that the func-
tionary Secretary has delegated the authority to perform C-act kinds TK01/dc, TK01/
da and TK02/rq to the functionary Administrator.

Table 7.4 Detailed ADT of the case Volley
T/P TK01/dc TK01/da TK02/rq
Secretary A A A
Administrator D D D
34 The DEMO Specification Language v4.7.2

35
Appendix A
This appendix contains the figures that could not be inserted easily in the previous
chapters. The colours in the figures have a specific meaning:
green means that the indicated parts belong to a schema,
blue means that the indicated parts belong to a diagram (or to an ARS),
purple means that the indicated parts belong to a table (or to a WIS).

36 The DEMO Specification Language v4.7.2

Fig. A.0 General schema
The diagram above is an expression in GOSL (cf. MU theory in [3]) of the schema
that specifies the state space of the ‘world’ that is covered by the CM, the AM and the
PM of a SoI. The FM has a separate schema (Fig. A.4). The next explanation applies
to the general schema (in addition to the common knowledge from [3]):

The default cardinality ranges of property types are 1..1 at the side of the range
and 0..* at the side of the domain. Default ranges are not indicated in the diagram.
There is always an access link from an actor role to the transaction kind in
whose transactions actors in this role are the executor, and there is always an ac-
cess link from an actor role to the transaction kind in whose transactions actors in
37
this role are an initiator. This clarifies the cardinality ranges that belong to the
property type ‘there is an access link from[ar] to [tk]’.
Although the definition of the type ‘transactor role’ as the aggregation of the
types ‘transaction kind’ and ‘actor role’ is basically correct, the extension of the
type ‘transactor role’ is limited, as specified in the diagram.
From the OMEGA theory it follows that the initiation link of a transaction kind
is one of the instances of the property type ‘there is a response link from [tksk] to
[tksk]’. Consequently, the external event type ‘in’ in Figs 4.2, 4.3 and 4.5, is just a
transaction kind step kind.
Every action rule applies to exactly one transaction kind step kind. Conversely,
to a transaction kind step kind, several action rules may apply. They differ how-
ever in the while clause.
In the next pages, the parts of the diagram that are covered by the distinct models
and their ways of representations, are indicated by bold coloured lines.

38 The DEMO Specification Language v4.7.2

Fig. A.1 Schema of the CM
The diagram above is an expression in GOSL (cf. MU theory in [3]) of the schema
that specifies the state space of the ‘world’ that is covered by the CM, the AM and the
PM of a SoI.

The green coloured and bold-lined parts collectively define the CM of a SoI.
Recall that the default cardinality range of a property type at the domain side is 0..*
and at the range side 1..1. Default values are commonly not indicated in a schema.

39
Fig. A.2 Schema of the PM
The diagram above is an expression in GOSL (cf. MU theory in [3]) of the schema
that specifies the state space of the ‘world’ that is covered by the CM, the AM and the
PM of a SoI.

The green coloured and bold-lined parts collectively define the PM of a SoI.
Recall that the default cardinality range of a property type at the domain side is 0..*
and at the range side 1..1. Default values are commonly not indicated in a schema.

40 The DEMO Specification Language v4.7.2

Fig. A.3 Schema of the AM
The diagram above is an expression in GOSL (cf. MU theory in [3]) of the schema
that specifies the state space of the ‘world’ that is covered by the CM, the AM and the
PM of a SoI.

The green coloured and bold-lined parts collectively define the AM of a SoI. The
transaction kind step kind to which an action rule applies, is the C-event reference in
the when clause (cf. Fig. 5.2). For the sake of simplicity, we ignore the other parts of
the schema that may also be covered by an AM.

Recall that the default cardinality range of a property type at the domain side is 0..*
and at the range side 1..1. Default values are commonly not indicated in a schema.

41
Fig. A.4 Schema of the FM
The diagram above is the expression, in GOSL, of the schema of the production world
of a SoI. An example of such a schema is the one that is exhibited in Fig. 6.2.
The property types are formulated in a concise form: the references to the elements in
the domain and the range are omitted. Note that the instances of ENTITY TYPE and
VALUE TYPE may be sets of respectively entities and values (cf. Sec. 2.1). Con-
sequently, an event may concern a set of entities.

Recall that the default cardinality range of a property type at the domain side is 0..*
and at the range side 1..1. Default values are commonly not indicated in a schema.

42 The DEMO Specification Language v4.7.2

Fig. A.5 Definition of the Coordination Structure Diagram (CSD)
The blue coloured and bold-lined parts above collectively define the (semantic) con-
tents of a Coordination Structure Diagram (CSD). Thus, every CSD represents the
existence, in the chosen SoI, of a number of transaction kinds, actor roles (and con-
sequently transactor roles) as well as composite transactor roles and multiple transac-
tion kinds. In addition, it represents the existence of a number of executor links, initi-
ator links, access links and wait links. Note that a transactor role is the combination of
a transaction kind and the actor role that has its executor role.
The instances of the property type ‘is part of’ (which exist between transaction
kinds and multiple transaction kinds, as well as between transactor roles and compos-
ite transactor roles) may be implicitly given. It is important yet to know that a mul-
tiple transaction kind is a collection of transaction kinds, and that a composite trans-
actor role is a collection of transactor roles. Fig. 3.3 exhibits an example of a CSD.

43
Fig. A.6 Position of the action rules and the work instructions
The meaning of the blue coloured and bold-lined parts above is that every action rule
applies to one transaction kind step kind, but there may be several action rules that
apply to the same transaction kind step kind (or coordination event kind). They differ
however in the while clause. There is a separate action rule for every combination of a
coordination event kind and a wait condition. Action rules are expressed in Action
Rule Specifications (ARS).
The meaning of the dark blue coloured and bold-lined parts above is that every
work instruction applies to one product kind, and vice versa. Work instructions are
expressed in Work Instruction Specifications (WIS).

44 The DEMO Specification Language v4.7.2

Fig. A.7 Definition of the Process Structure Diagram (PSD)
The blue coloured and bold-lined parts above collectively define the (semantic) con-
tents of a Process Structure Diagram (PSD). Thus, every PSD represents the exist-
ence, in the chosen SoI, of a number of transaction kinds and actor roles, as well as
transaction kind step kinds, where every transaction kind step kind (e.g. TK04/da) is
defined as the aggregation of a general step kind (e.g. ‘da’) and a transaction kind
(e.g. TK01). In addition, it represents the existence of a number of executor links and
initiator links, as well as a number of wait links between transaction kind step kinds.
Fig. 4.4 exhibits an example of a PSD.

45
Fig. A.8 Definition of the Transaction Process Diagram (TPD)
The blue coloured and bold-lined parts above collectively define the (semantic) con-
tents of a Transaction Process Diagram (TPD). Fig. 4.2 shows the complete transac-
tion pattern (CTP) expressed in a TPD. A typical use of this TPD is discussed in the
case Fixit (cf. [3], Chap. 13). Another typical use is to show precisely the interrela-
tionships of transactions. An example of this way of using the TPD is exhibited in
Fig. 4.5.

46 The DEMO Specification Language v4.7.2

Fig. A.9 Definition of the Transactor Product Table (TPT)
The purple coloured and bold-lined parts above collectively define the (semantic)
contents of a Transactor Product Table (TPT). Thus, every TPT represents the exist-
ence, in the chosen SoI, of a number of transaction kinds, actor roles, and product
kinds. In addition, it expresses which actor role is the executor role of a transaction
kind, and which product kind is associated with the transaction kind. Table 7.1 shows
an example of a TPT.

47
Fig. A.10 Definition of the Bank Contents Table (BCT)
The purple coloured and bold-lined parts above collectively define the (semantic)
contents of a Bank Contents Table (BCT). Thus, every BCT represents the existence,
in the chosen SoI, of a number of transaction kinds, multiple transaction kinds, and P-
fact types. In addition, it represents for every P-fact type in which transaction kind
(now interpreted as a transaction bank) instances of it are contained.
The instances of the property type ‘is part of’ (between transaction kind and mul-
tiple transaction kind) may be implicitly given. It is important yet to understand that a
multiple transaction kind is a collection of transaction kinds. Table 7.2 contains an
example of a BCT.

48 The DEMO Specification Language v4.7.2

Fig. A.11 Definition of the Bank Access Table (BAT
The purple coloured and bold-lined parts above collectively define the (semantic)
contents of a Bank Access Table (BAT). Thus, a BAT represents the existence, in the
chosen SoI, of transaction kinds, multiple transaction kinds, and actor roles, as well as
of access links from actor roles to transaction banks, including the executor role and
the initiator roles. To clarify this, the entity type ‘composite actor role’ is added to the
schema (which can be fully deduced from the composite transactor role).
A BAT represents the interstriction structure of a SoI, as an alternative to drawing
access links in the CSD. Access links may also exist between actor roles and multiple
transaction kinds, and between composite actor roles and (multiple) transaction kinds.
An example of a BAT is presented in Table 3.1.

49
Fig. A.12 Definition of the Create Use Table (CUT)
The purple coloured and bold-lined parts above collectively define the (semantic)
contents of a Create Use Table (CUT). Thus, every CUT represents the existence, in
the chosen SoI, of a number of transaction kind step kinds and P-fact types. In addi-
tion, it expresses for every P-fact type, in which transaction kind step kind its in-
stances are created and in which transaction kind step kind its instances are used.
Table 7.3 contains an example of a CUT.

50 The DEMO Specification Language v4.7.2

Fig. A.13 Definition of the Authorisation Delegation Table (ADT)
The purple coloured and bold-lined parts above collectively define the (semantic)
contents of the Authorisation Delegation Table (ADT). Note that the entity class
PERFORMER is added to the schema, to make the definition possible.
The columns of an ADT represent tasks (T), ranging from single process steps (in a
detailed ADT) to the responsibility ranges of actor roles (in a global ADT). The rows
represent the task performers (P), ranging from functionaries to complete enterprises.
An “A” at the crossing of a column and a row indicates that the performer is author-
ised to perform the task, a “D” that he/she has delegated authority. In a global ADT,
only A’s can occur since it is by definition not possible to delegate a complete actor
role (cf. PSI theory in [3]). Table 7.4 contains an example of a detailed ADT.

51
Appendix B
The Extended Backus-Naur Form
In this document, the Extended Backus-Naur Form (EBNF)^6 , the international stand-
ard syntactic meta language, defined in ISO/IEC 14977^7 , is applied to define in a
formal way the syntax of DEMOI-SL. To improve readability, English words, like
articles and prepositions are added, which make the logical formulas look like struc-
tured English sentences, quite unlike the common Peano-Russell notation^8. These
added words are printed in bold in order to distinguish them clearly from the formal
text. They are just ignored by formal analysis tools.
In EBNF, names are put between double quotation marks (“ and ”). The symbol “|”
stands for “exclusive or”. The symbol “,” means “followed by”; the EBNF brackets
“{“ and “}” enclose symbols that may be repeated an unlimited number of times; “}-“
as the closing bracket means that there is at least one occurrence. Where considered
helpful, comments are inserted between “%” and “%”. The end of a definition is
marked by “;”.

(^6) https://en.wikipedia.org/wiki/Extended_Backus–Naur_form
(^7) https://www.cl.cam.ac.uk/~mgk25/iso-14977.pdf
(^8) https://en.wikipedia.org/wiki/Peano–Russell_notation

52 The DEMO Specification Language v4.7.2

Appendix C
The syntax diagram
The syntax diagram is a graphical language for defining the syntax of a language in a
formal way. Syntax diagrams are, for example, used to define the syntax of Pascal^9
and CANDE^10. We will use them particularly for defining the syntax of action rule
specifications. They are discussed in Sect. 5.
The easiest way to explain syntax diagrams is by means of the example below. An
arrow indicates the direction of reading. The bar at the far right side indicates the end
of the definition.

According to the defined syntax, the following (not exhaustive) set of sentences
can be produced:

ROW THE BOAT GENTLY DOWN-STREAM
ROW, ROW THE BOAT GENTLY DOWN-STREAM
ROW, ROW, ROW THE BOAT GENTLY DOWN-STREAM
ROW YOUR BOAT GENTLY DOWN-STREAM
ROW THE BOAT DOWN-STREAM
ROW THE BOAT GENTLY DOWN THE STREAM
ROW THE BOAT GENTLY DOWN THE OLD STREAM
(^9) https://www.cs.rice.edu/~javaplt/311/Readings/CPSyntax.pdf
(^10) http://bitsavers.org/pdf/burroughs/B6500_6700/5000318_B6700_CANDE_Oct72.pdf
ROW THE BOAT GENTLY DOWN - STREAM
YOUR THE OLD
,0..2

53
References
Dietz, J.L.G. and H.B.F. Mulder, Enterprise Ontology: A Human-Centric Approach to Un-
derstanding the Essence of Organisation. 2020, Springer International Publishing.
Sowa, J.F., Knowledge representation: logical, philosophical, and computational founda-
tions. 2000, Pacific Grove: Brooks/Cole. xiv, 594 p.
Dietz, J.L.G., On the nature of business rules , in Advances in Enterprise Engineering I.
2009, Springer: Berlin-Heidelberg.
This is a offline tool, your data stays locally and is not send to any server!
Feedback & Bug Reports