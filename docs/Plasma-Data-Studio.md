-   Plasma Data Studio

TerraMeta Software, Inc.

PlasmaSDO® and PlasmaQuery® are registered

Trademarks of TerraMeta Software, Inc.

**Introduction**
================

Plasma is a data store agnostic, object mapping and object query framework
written in a Java™ with Maven tools for metadata ingestion and conversion. At
its core, Plasma contains a directed graph or digraph model and a set of
metadata driven graph traversal algorithms. Data Objects under Plasma form a
digraph transparently as a client manipulates the SDO API, graph edges or links
being automatically created and used internally to manage associations between
Data Object nodes. Data store provider implementations are available for Apache
HBase, MAPR-DB (M7) and various relational database vendors.

The Plasma metadata extensions are described in a UML profile which contains UML
stereotypes, enumerations and other elements used to enrich UML models for use
within the Plasma core as well as third party Data Access Service (DAS)
providers. Particular design consideration has been focused on leaving each
stereotype granular with only a few tightly related attributes/tags, rather than
more monolithic stereotype groupings. This approach lets each stereotype convey
far more meaning and maps well to metadata oriented extensions in various target
languages, such as Java™ annotations. This granular approach can however have
the effect of making UML diagrams more cluttered depending on the presentation
settings of the UML diagramming tool.

A single UML logical model fully enriched or annotated with the Plasma UML
profile provides enough context specific information to support various
technology-specific runtime environments and the generation of numerous context
or platform-specific models as well as many other related source-code and other
artifacts.

**Plasma Data Studio**
======================

Plasma Data Studio is an Eclipse based IDE for annotating and integrating UML
models with Maven (M2E) based Java projects. The UML editor is derived from
Eclipse Papyrus components. See <https://www.eclipse.org/papyrus>. It is
centered around a custom Eclipse perspective (Plasma perspective), capability to
create projects and diagrams, and a custom UML palette. UML Models are annotated
using a custom UML profile and datatypes package, both of which are fully
integrated or registered in the IDE. The below screen shot pictures a UML model
being edited in-line with a standard Java Eclipse project.

![](media/6eeda73635c7bf056209be2c73ca30bc.png)

Figure 1 - Plasma Perspective Dialog

![](media/4eebb495fa7ab2cfead10a8a3ffb06c7.png)

Figure 2 - Plasma Data Studio

**Creating a Plasma Model**
===========================

From Plasma Data Studio create a new UML model and diagram into the
src/main/resources directory of your existing maven project.

1.  Right click on the resources directory, then to New-\>Other-\>Plasma as
    below.

2.  Save the model (it will have a .di extension, for diagram) in the resources
    dir of the project.

3.  Select Plasma Class Diagram for the diagram type. Then Finish the wizard.

![](media/9d443af4f9d6e5ee9b87452bd4dc63e9.png)

![](media/1979a9aa7d2221af3f409164f722a134.png)

![](media/15d008fe629a9172d97bbb986c8924c7.png)

![](media/f596aef6700dc9a213abd58f5a392afe.png)

Figure 3 - Create Project Wizard

**Editing a Plasma UML Model**
==============================

First open the Plasma Perspective. The new model can be edited and annotated as
any Papyrus model. See <https://www.eclipse.org/papyrus/> for detailed
documentation on Eclipse Papyrus. Plasma Data Studio however has a custom
pallete which restricts the available UML elements to those applicable to Plasma
structural models. Double click or drag 2 class elements to the diagram and name
one Person and one Organization.

![](media/431c9b614d28f1904fe42176678b54d9.png)

![](media/2c4d5c0b06edaa94e1b9139b6962ddfc.png)

Next add a class called Party and make it anstract, then use generalization
edges to make the Person and Organization classes inherit from Party.

![](media/b3a46b9155e4158e95eccc8d4b9db54d.png)

Next add properties to the Person entity. Before adding properties we need to
import datatypes to use for the property datatypes. Select the root element of
the project in the Model Explorer, then select Import-\>Import Registered
Package. Then select Plasma Data Types and load the package into your model.

![](media/a6aea080f46af5c02891c70bf74f36ca.png)

Next using the plus (+) sign in the properties editor, add 4 properties
firstName, lastName, age and dateOfBirth with datatypes (String, String, Int,
Date) respectively. Note that the Papyres Filters must be used to make the
properties appear in the entity. Right click on the entity and select
Filters-\>Show/Hide Contents.

![](media/c158553ee62afee0210786de65281e1d.png)

Next we will link the Person and Organization entities with an association.
Select Association from the edges palette and link the Person and Organization
entities. Make both ends of the association navigable and owned by the
respective Classifier and make the Multiplicity on the Organization side
zero-to-many as below. And instead of leaving the default names for the
association ends (person, organization) make these more specific to a Human
Resources model such as employer and employee, as below.

![](media/3cb7ffbf84ee94bd1371f948f6b08861.png)

Next add 2 properties to the Organization entity name and category, both with
String datatypes from the Plasma Data Types package. We will enhance the
category property with an enumeration restriction later. Then add a recursive
association to the Organization entity as below, with both sides of the
association owned by the classifier. Note that the Papyres Filters must be used
to make the properties appear in the entity. Right click on the entity and
select Filters-\>Show/Hide Contents.

![](media/c2f8dd15c0cbbbd54b39e680c758bbf8.png)

Nexte add a property to the shared entity we created previously called Party.
Just add 1 property createdDate of data type Date. This property will be
inherited by both the Person and Organization entities.

![](media/4b8f0668701e601f6afbba7ec939f62a.png)

**Enhancing a Plasma UML Model**
================================

After creating a basic model we need to add enhancements using standard UML
Profile mechanisms supported by Eclipse Papyrus, which add “facets” to various
elements. These facets describe restrictions such as String property length
restrictions enumeration restrictions and several others which provide a
complete structural model description. The final model has enough information to
allow us to generate code and persist the entities we created in one or more
physical data stores. (*Note that for big-data stores such as HBase the size of
the physical table is greatly influenced by the size of column names, and the
logical/physical name isolation provided by Plasma is critical for controlling
the size of the physical store while maintaining a readable data model and
generated code*) First select the root package node on the Model Explorer and
rename the package to HumanResources. Then select the Profile editor section and
add the SDOAlias and SDONamespace stereotypes. Assign the SDOAlias physicalName
= ‘’HR’ for the model package and the SDONamespace uri =
‘http://plasma-quickstart-pojo/humanresources’. The URI is critical and is used
to link the model to a specific data store. A large model can of course have
numerous packages and each package can be associated the the same or several
data store providers.

![](media/1eae26ef4c10d0867a696a891928bead.png)

![](media/1ee2b1d8c08882a59ece338ef282d98f.png)

![](media/770344f29f5b993b34d62d6a7ad91593.png)

![](media/485d6bcf180dbcb570dadf3d94214281.png)

Next select the Person entity and edit the Profile section of the property
editor as below. Add the SDOAlias stereotype and assign the physicalName as
‘PERSON’.

![](media/cc47f643b424db2e3ca27eb20c7ce872.png)

![](media/0325095575ec7f6b48d6f30f6856099b.png)

Next assign the Orgaization entity the physicalName of ‘ORG’.

![](media/6ac46aa759212c44b0e22b91c1b05c66.png)

Next for the Person entity firstName property, select the Profile section of the
editor and assign the SDOAlias, SDOKey and SDOValueConstraint stereotypes. Then
assign SDOAlias physicalName = “FN” and SDOKey type=’primary’ and
SDOValueConstraint maxLength=36 as below.

![](media/0ae299ae9aa7127e7845cc0cc4911ba9.png)

![](media/3ec2225b69186f578462928ac46eaacf.png)

![](media/7b9ac1ced20c61a57fa93fb33b8cbd57.png)

![](media/a9c7e3dba9dcdddbc564c3690b9dc81d.png)

Next similarly for the Person entity lastName property, select the Profile
section of the editor and assign the SDOAlias, SDOKey and SDOValueConstraint
stereotypes. Then assign SDOAlias physicalName = “LN” and SDOKey type=’primary’
and SDOValueConstraint maxLength=36.

Next similarly for the Person entity dateOfBirth property, select the Profile
section of the editor and assign the SDOAlias stereotype. Then assign SDOAlias
physicalName = “DOB”.

![](media/5a8d46215bddf1ed6b4159f8b1b6eb54.png)

Next to enhance the Organization entity, we will first create an Enumeration
‘OrgCat’ which will be used to restrict the values of the category property we
added earlier. Add four owned literals to the OrgCat enumeration ‘nonprofit’,
‘government’, ‘retail’, “wholesale” and assign each literal a physicalName which
is the fitst letter i.e. ‘N’, ‘G’, ‘R’ and ‘W’ respectively as below.

![](media/0ee4d02801f48e3c3935748345901d86.png)

Next edit the Organization category property Profile section adding the
SDOAlias, SDOEnumerationConstraint and SDOValueConstraint stereotypes. Assign
the SDOAlias and SDOValueConstraint stereotypes as below and assign the
SDOEnumerationConstraint to the OrgCat enumeration we created previously.

![](media/96901ee608d82ab37f3de52459ceb711.png)

![](media/6f5e557738369bc022c2ca183d68e698.png)

![](media/2ad82d5dc159fef74fb2c4ee903c35d3.png)

![](media/388a53ba229062ca353f15b061c7d78e.png)

![](media/e7bf382eef1239779c00d38bf0437abd.png)

Next for the Organization entity name property, select the Profile section of
the editor and assign the SDOAlias, SDOKey and SDOValueConstraint stereotypes.
Then assign SDOAlias physicalName = “NAME” and SDOKey type=’primary’ and
SDOValueConstraint maxLength=36 similarly.

And finally for the Party entity createdDate property select the Profile section
of the editor and assign the SDOAlias stereotypes Then assign SDOAlias
physicalName = “CRTD_DT” similarly as below.

![](media/821bdf2f70ea88640a38026105d15ca4.png)
