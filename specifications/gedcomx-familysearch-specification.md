# FamilySearch GEDCOM X Extensions

## Status

This document specifies FamilySearch extensions to GEDCOM X, and requests
discussion and suggestions for improvements.

The current state of this document is as a DRAFT, and as such, the document
may be subject to changes, including backwards-incompatible changes, according to the
discussion and suggestions for improvement.

## Copyright Notice

Copyright 2011-2016 Intellectual Reserve, Inc.

## License

This document is distributed under a Creative Commons Attribution-ShareAlike license.
For details, see:

http://creativecommons.org/licenses/by-sa/3.0/

<a name="intro"/>

# 1. Introduction

This project contains the specifications that extend [GEDCOM X](http://www.gedcomx.org)
to support the proprietary application requirements for [FamilySearch](https://familysearch.org).

A set of data types are defined as extensions to the [core GEDCOM X specification set](https://github.com/FamilySearch/gedcomx/blob/master/specifications/),
the [GEDCOM X Record Extension](https://github.com/FamilySearch/gedcomx-record/blob/master/specifications/record-specification.md),
and the [GEDCOM X Atom Extensions](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md).

## Table Of Contents

* [1. Introduction](#intro)
  * [1.1 Identifier, Version and Dependencies](#id-and-version)
  * [1.2 Notational Conventions](#notational-conventions)
    * [1.2.1 Keywords](#keywords)
    * [1.2.2 Compliance](#compliance)
    * [1.2.3 Namespace Prefixes](#namespace-prefixes)
  * [1.3 Concepts and Definitions](#concepts-definitions)
* [2. Data Type Extensions](#datatypes)
  * [2.1 The "ArtifactMetadata" Data Type](#artifact-metadata)
  * [2.2 The "ChangeInfo" Data Type](#change-info)
  * [2.3 The "ChildAndParentsRelationship" Data Type](#child-and-parents-relationship)
  * [2.4 The "Comment" Data Type](#comment)
  * [2.5 The "Discussion" Data Type](#discussion)
  * [2.6 The "DiscussionReference" Data Type](#discussion-reference)
  * [2.7 The "MatchInfo" Data Type](#match-info)
  * [2.9 The "MergeAnalysis" Data Type](#merge-analysis)
  * [2.10 The "MergeConflict" Data Type](#merge-conflict)
  * [2.11 The "NameFormInfo" Data Type](#nameform-info)
  * [2.12 The "SearchInfo" Data Type](#search-info)
  * [2.13 The "Reservation" Data Type](#reservation)
  * [2.14 The "Ordinance" Data Type](#ordinance)
  * [2.15 The "Tag" Data Type](#tag)
  * [2.16 The "User" Data Type](#user)
  * [2.17 The "Error" Data Type](#error)
  * [2.18 The "Feature" Data Type](#feature)
  * [2.19 The "FeedbackInfo" Data Type](#feedback-info)
  * [2.20 The "FamilySearchPlatform" XML Data Type](#fsp-xml)
  * [2.21 The "FamilySearchPlatform" JSON Data Type](#fsp-json)


<a name="id-and-version"/>

## 1.1 Identifier, Version, and Dependencies

The identifier for this specification is:

`http://familysearch.org/v1/`

This specification references the GEDCOM X Conceptual Model specification identified
by [`http://gedcomx.org/conceptual-model/v1`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md).

This specification references the GEDCOM X XML specification identified
by [`http://gedcomx.org/xml/v1`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md).

This specification references the GEDCOM X JSON specification identified
by [`http://gedcomx.org/json/v1`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md).

This specification references the GEDCOM X Atom Extensions specification identified
by [`http://gedcomx.org/atom-extensions/v1`](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md).

This specification references the GEDCOM X Record Extensions specification identified
by [`http://gedcomx.org/records/v1`](https://github.com/FamilySearch/gedcomx-record/blob/master/specifications/record-specification.md).

This specification references the GEDCOM X RS specification identified
by [`http://gedcomx.org/rs/v1`](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/rs-specification.md).


<a name="notational-conventions"/>

## 1.2 Notational Conventions

<a name="keywords"/>

### 1.2.1 Keywords

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in BCP 14,
[RFC2119](http://tools.ietf.org/html/rfc2119), as scoped to those conformance
targets.

<a name="compliance"/>

### 1.2.2 Compliance

An implementation of FamilySearch Extensions is "non-compliant" if it fails to satisfy
one or more of the MUST or REQUIRED level requirements. An implementation that satisfies all of
the  MUST or REQUIRED and all of the SHOULD level requirements is said to be "unconditionally
compliant"; and implementation that satisfies all of the MUST level requirements but not all of the
SHOULD level requirements is said to be "conditionally compliant".

<a name="namespace-prefixes"/>

### 1.2.3 Namespace Prefixes

This specification uses the same namespace prefix conventions that are used by the
[GEDCOM X XML](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md)
specification.

In addition to those prefixes, the following namespace prefixes are used:

prefix | namespace
-------|----------
fs | `http://familysearch.org/v1/`

<a name="concepts-definitions"/>

## 1.3 Concepts and Definitions

This specification leverages the concepts and definitions as specified by its
dependencies.

<a name="datatypes"/>

# 2. Data Type Extensions

This section defines a set of extensions to the [GEDCOM X Conceptual Model](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md),
the [GEDCOM X Record Extension](https://github.com/FamilySearch/gedcomx-record/blob/master/specifications/record-specification.md),
and the [GEDCOM X Atom Extensions](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md)
and provides the representations of those data types in both XML and JSON as extensions to
[GEDCOM X JSON](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md) and
[GEDCOM X XML](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md).

<a name="artifact-metadata"/>

## 2.1 The "ArtifactMetadata" Data Type

The `ArtifactMetadata` data type defines a representation of metadata about an artifact
such as a memory.

Instances of `ArtifactMetadata` can be reasonably expected as extension elements to the [`SourceDescription` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#source-description).

### identifier

The identifier for the `ArtifactMetadata` data type is:

`http://familysearch.org/v1/ArtifactMetadata`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
filename | Name of the file of the artifact, if the artifact were provided as a file on a filesystem. | string | OPTIONAL.
qualifiers | Qualifiers to add additional details about the artifact. | List of [http://gedcomx.org/v1/Qualifier](#qualifier) | OPTIONAL. If present, use of a [known artifact qualifier](#known-artifact-qualifier) is RECOMMENDED.
width | Width of the artifact, if applicable. | integer | OPTIONAL.
height | Height of the artifact, if applicable. | integer | OPTIONAL.
size | Size of the artifact in number of bytes. | long | OPTIONAL.
screeningState | Screening state of the artifact, if applicable. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, use of a [known screening state](#known-screening-state) is RECOMMENDED.
editable | Whether the artifact is editable by the current user. | boolean | OPTIONAL.


### 2.1.1 The "ArtifactMetadata" XML Type and Element

The `fs:ArtifactMetadata` XML type is used to (de)serialize the `http://familysearch.org/v1/ArtifactMetadata` data type.
The `fs:artifactMetadata` XML element is used to provide instances of the `fs:ArtifactMetadata` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
filename | Name of the file of the artifact, if the artifact were provided as a file on a filesystem. | fs:filename | xsd:string.
qualifiers | Qualifiers to add additional details about the artifact. | fs:qualifier | [`gx:Qualifier`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#qualifier)
width | Width of the artifact, if applicable. | fs:width | xsd:integer
height | Height of the artifact, if applicable. | fs:height | xsd:integer
size | Size of the artifact in number of bytes. | fs:size | xsd:long
screeningState | Screening state of the artifact, if applicable. | screeningState (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
editable | Whether the artifact is editable by the current user. | fs:editable | xsd:boolean

### 2.1.2 The "ArtifactMetadata" JSON Type

The `ArtifactMetadata` JSON type is used to (de)serialize the `http://familysearch.org/v1/ArtifactMetadata` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
filename | Name of the file of the artifact, if the artifact were provided as a file on a filesystem. | filename | string.
qualifiers | Qualifiers to add additional details about the artifact. | qualifiers | array of [`Qualifier`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#qualifier)
width | Width of the artifact, if applicable. | width | number
height | Height of the artifact, if applicable. | height | number
size | Size of the artifact in number of bytes. | size | number
screeningState | Screening state of the artifact, if applicable. | screeningState | string
editable | Whether the artifact is editable by the current user. | editable | boolean

<a name="known-artifact-qualifier"/>

### 2.1.3 Known Artifact Qualifiers

The following artifact qualifiers are defined by FamilySearch Extensions:

name | value
-----|-------
`http://familysearch.org/v1/Document`| The artifact is a document.
`http://familysearch.org/v1/Obituary`| The artifact is a obituary.
`http://familysearch.org/v1/Photo`| The artifact is a photo.
`http://familysearch.org/v1/Story`| The artifact is a story.

<a name="known-screening-state"/>

### 2.1.3 Known Screening State

The following screening states are defined by FamilySearch Extensions:

name | value
-----|-------
`http://familysearch.org/v1/Pending`| The artifact is pending a screening.
`http://familysearch.org/v1/Accepted`| The artifact has been screened and is accepted.
`http://familysearch.org/v1/Restricted`| The artifact has been screened and is restricted.

<a name="change-info"/>

## 2.2 The "ChangeInfo" Data Type

The `ChangeInfo` data type defines a representation of information about data changes.

Instances of `ChangeInfo` can be reasonably expected as extension elements to the [`Entry` Data Type](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md#atom-entry-extensions).

### identifier

The identifier for the `ChangeInfo` data type is:

`http://familysearch.org/v1/ChangeInfo`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
operation | The operation performed for the change. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, use of a [known change operation](#known-change-operation) is RECOMMENDED.
objectType | The type of object to which the change was applicable. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL.
objectModifier | An additional modifier applicable to the type of object to which the change was applicable. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL.
reason | A statement about the reason for the change, as supplied by the current user. | string | OPTIONAL.
parent | A reference to the change that triggered the change. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Entry`](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md#atom-entry-extensions).
resulting | A reference to the object that was a result of the change. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).
original | A reference to the object that was the original subject of the change. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).
removed | A reference to the object that was removed by the change. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).

### 2.2.1 The "ChangeInfo" XML Type and Element

The `fs:ChangeInfo` XML type is used to (de)serialize the `http://familysearch.org/v1/ChangeInfo` data type.
The `fs:changeInfo` XML element is used to provide instances of the `fs:ChangeInfo` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
operation | The operation performed for the change. | operation (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
objectType | The type of object to which the change was applicable. | objectType (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
objectModifier | An additional modifier applicable to the type of object to which the change was applicable. | objectModifier (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
reason | A statement about the reason for the change, as supplied by the current user. | reason (attribute) | xsd:string
parent | A reference to the change that triggered the change. | fs:parent | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
resulting | A reference to the object that was a result of the change. | fs:resulting | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
original | A reference to the object that was the original subject of the change. | fs:original | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
removed | A reference to the object that was removed by the change. | fs:removed | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)

### 2.2.2 The "ChangeInfo" JSON Type

The `ChangeInfo` JSON type is used to (de)serialize the `http://familysearch.org/v1/ChangeInfo` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
operation | The operation performed for the change. | operation | string
objectType | The type of object to which the change was applicable. | objectType | string
objectModifier | An additional modifier applicable to the type of object to which the change was applicable. | objectModifier | string
reason | A statement about the reason for the change, as supplied by the current user. | reason | string
parent | A reference to the change that triggered the change. | parent | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
resulting | A reference to the object that was a result of the change. | resulting | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
original | A reference to the object that was the original subject of the change. | original | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
removed | A reference to the object that was removed by the change. | removed | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)

<a name="known-change-operation"/>

### 2.2.3 Known Change Operation

The following artifact qualifiers are defined by FamilySearch Extensions:

name | value
-----|-------
`http://familysearch.org/v1/Create`| A "create" operation.
`http://familysearch.org/v1/Read`| A "Read" operation.
`http://familysearch.org/v1/Update`| A "update" operation.
`http://familysearch.org/v1/Delete`| A "delete" operation.
`http://familysearch.org/v1/Merge`| A "merge" operation.
`http://familysearch.org/v1/Unmerge`| A "unmerge" operation.
`http://familysearch.org/v1/Restore`| A "restore" operation.


<a name="child-and-parents-relationship"/>

## 2.3 The "ChildAndParentsRelationship" Data Type

The `ChildAndParentsRelationship` data type defines a representation of the relationship between a child and two parents.

### identifier

The identifier for the `ChildAndParentsRelationship` data type is:

`http://familysearch.org/v1//ChildAndParentsRelationship`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
father | A reference to the father. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).
mother | A reference to the father. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).
child | A reference to the father. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).
fatherFacts | The facts about the relationship between the child and the father.| List of [`http://gedcomx.org/v1/Fact.`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#fact-conclusion) Order is preserved. | OPTIONAL.
motherFacts | The facts about the relationship between the child and the mother.| List of [`http://gedcomx.org/v1/Fact.`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#fact-conclusion) Order is preserved. | OPTIONAL.


### 2.3.1 The "ChildAndParentsRelationship" XML Type and Element

The `fs:ChildAndParentsRelationship` XML type is used to (de)serialize the `http://familysearch.org/v1/ChangeInfo` data type.
The `fs:childAndParentsRelationship` XML element is used to provide instances of the `fs:ChildAndParentsRelationship` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
father | A reference to the father. | fs:father | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
mother | A reference to the mother. | fs:mother | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
child | A reference to the child. | fs:child | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
fatherFacts | The facts about the relationship between the child and the father.| fs:fatherFact | [gx:Fact](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#fact-conclusion)
motherFacts | The facts about the relationship between the child and the mother.| fs:motherFact | [gx:Fact](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#fact-conclusion)

### 2.3.2 The "ChildAndParentsRelationship" JSON Type

The `ChildAndParentsRelationship` JSON type is used to (de)serialize the `http://familysearch.org/v1/ChildAndParentsRelationship` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
father | A reference to the father. | father | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
mother | A reference to the mother. | mother | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
child | A reference to the child. | child | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
fatherFacts | The facts about the relationship between the child and the father.| fatherFacts | array of [Fact](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#fact-conclusion)
motherFacts | The facts about the relationship between the child and the mother.| motherFacts | array of [Fact](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#fact-conclusion)

<a name="comment"/>

## 2.4 The "Comment" Data Type

The `Comment` data type defines a comment submitted by a user.

### identifier

The identifier for the `Comment` data type is:

`http://familysearch.org/v1/Comment`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
text | The text of the comment. | string | REQUIRED.
contributor | A reference to the contributor of the comment. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Agent`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#agent).
created | Timestamp of when the comment was created. | timestamp | OPTIONAL.

### 2.4.1 The "Comment" XML Type and Element

The `fs:Comment` XML type is used to (de)serialize the `http://familysearch.org/v1/Comment` data type.
The `fs:comment` XML element is used to provide instances of the `fs:Comment` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
text | The text of the comment. | fs:comment | xsd:string
contributor | A reference to the contributor. | fs:contributor | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
created | Timestamp of when the comment was created. | fs:created | xsd:dateTime

### 2.4.2 The "Comment" JSON Type

The `Comment` JSON type is used to (de)serialize the `http://familysearch.org/v1/Comment` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
text | The text of the comment. | comment | string
contributor | A reference to the contributor. | contributor | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
created | Timestamp of when the comment was created. | created | number (milliseconds since epoch)

<a name="discussion"/>

## 2.5 The "Discussion" Data Type

The `Discussion` data type defines a comment submitted by a user.

### identifier

The identifier for the `Discussion` data type is:

`http://familysearch.org/v1/Discussion`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
title | The title of the discussion. | string | REQUIRED.
details | Any details about the discussion. | string | OPTIONAL.
contributor | A reference to the contributor of the comment. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Agent`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#agent).
created | Timestamp of when the discussion was created. | timestamp | OPTIONAL.
modified | Timestamp of when the discussion was last modified. | timestamp | OPTIONAL.
numberOfComments | The number of comments associated with the discussion. | integer | OPTIONAL.
comments | The comments of the discussion | List of [`http://familysearch.org/v1/Comment`](#comment) | OPTIONAL.

### 2.5.1 The "Discussion" XML Type and Element

The `fs:Discussion` XML type is used to (de)serialize the `http://familysearch.org/v1/Discussion` data type.
The `fs:discussion` XML element is used to provide instances of the `fs:Discussion` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
title | The title of the discussion. | fs:title | xsd:string
details | The details of the discussion. | fs:details | xsd:string
contributor | A reference to the contributor. | fs:contributor | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
created | Timestamp of when the discussion was created. | fs:created | xsd:dateTime
modified | Timestamp of when the discussion was modified. | fs:modified | xsd:dateTime
numberOfComments | The number of comments associated with the discussion. | fs:numberOfComments | xsd:integer
comments | The comments of the discussion | fs:comment | [`http://familysearch.org/v1/Comment`](#comment)

### 2.5.2 The "Discussion" JSON Type

The `Discussion` JSON type is used to (de)serialize the `http://familysearch.org/v1/Discussion` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
title | The title of the discussion. | title | string
details | The details of the discussion. | details | string
contributor | A reference to the contributor. | contributor | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
created | Timestamp of when the discussion was created. | created | number (milliseconds since epoch)
modified | Timestamp of when the discussion was modified. | modified | number (milliseconds since epoch)
numberOfComments | The number of comments associated with the discussion. | numberOfComments | number
comments | The comments of the discussion | fs:comment | array of [`http://familysearch.org/v1/Comment`](#comment)

<a name="discussion-reference"/>

## 2.6 The "DiscussionReference" Data Type

The `DiscussionReference` data type defines a reference to a discussion.

Instances of `DiscussionReference` can be reasonably expected as extension elements to the [`Person` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri).

### identifier

The identifier for the `DiscussionReference` data type is:

`http://familysearch.org/v1/DiscussionReference`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
resource | Reference to the discussion. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. MUST resolve to an instance of `http://familysearch.org/v1/Discussion`.
attribution | The attribution of the discussion reference. | [`Attribution`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#attribution) | OPTIONAL.
resourceId | Id of the discussion being referenced | string | OPTIONAL.

### 2.6.1 The "DiscussionReference" XML Type and Element

The `fs:DiscussionReference` XML type is used to (de)serialize the `http://familysearch.org/v1/DiscussionReference` data type.
The `fs:discussionReference` XML element is used to provide instances of the `fs:DiscussionReference` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
resource | Reference to the discussion. | resource (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
attribution | The attribution of the discussion reference. | fs:attribution | [`gx:Attribution`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#attribution)
resourceId | Id of the discussion being referenced | resourceId (attribute) | xsd:string

### 2.6.2 The "DiscussionReference" JSON Type

The `DiscussionReference` JSON type is used to (de)serialize the `http://familysearch.org/v1/DiscussionReference` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
resource | Reference to the discussion. | resource | string
attribution | The attribution of the discussion reference. | attribution | [`Attribution`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#attribution)
resourceId | Id of the discussion being referenced | resourceId | string

<a name="match-info"/>

## 2.7 The "MatchInfo" Data Type

The `MatchInfo` data type defines a representation of information about a match.

Instances of `MatchInfo` can be reasonably expected as extension elements to the [`Entry` Data Type](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md#atom-entry-extensions).

### identifier

The identifier for the `MatchInfo` data type is:

`http://familysearch.org/v1/MatchInfo`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
collection | The collection in which the match was found. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL.
status | The staus of the match. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, use of a [known match status](#known-match-status) is RECOMMENDED.

### 2.7.1 The "MatchInfo" XML Type and Element

The `fs:MatchInfo` XML type is used to (de)serialize the `http://familysearch.org/v1/MatchInfo` data type.
The `fs:matchInfo` XML element is used to provide instances of the `fs:MatchInfo` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
collection | The collection in which the match was found. | collection (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
status | The staus of the match. | status (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)

### 2.7.2 The "MatchInfo" JSON Type

The `MatchInfo` JSON type is used to (de)serialize the `http://familysearch.org/v1/MatchInfo` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
collection | The collection in which the match was found. | collection | string
status | The staus of the match. | status | string

<a name="known-match-status"/>

### 2.7.3 Known Match Status

The following match statuses are defined by FamilySearch Extensions:

name | value
-----|-------
`http://familysearch.org/v1/Pending`| The match hasn't been accepted or rejected by a user.
`http://familysearch.org/v1/Accepted`| The match was accepted by a user.
`http://familysearch.org/v1/Rejected`| The match was rejected by a user.

<a name="merge"/>

## 2.8 The "Merge" Data Type

The `Merge` data type defines a representation of a merge operation.

### identifier

The identifier for the `Merge` data type is:

`http://familysearch.org/v1//Merge`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
resourcesToDelete | The resources to delete on a merge. | List of [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).
resourcesToCopy | The resources to copy on a merge. | List of [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).


### 2.8.1 The "Merge" XML Type and Element

The `fs:Merge` XML type is used to (de)serialize the `http://familysearch.org/v1/Merge` data type.
The `fs:merge` XML element is used to provide instances of the `fs:Merge` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
resourcesToDelete | The resources to delete on a merge. | resourceToDelete | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference) 
resourcesToCopy | The resources to copy on a merge. | resourceToCopy | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)


### 2.8.2 The "Merge" JSON Type

The `Merge` JSON type is used to (de)serialize the `http://familysearch.org/v1/Merge` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
resourcesToDelete | The resources to delete on a merge. | resourcesToDelete | array of [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
resourcesToCopy | The resources to copy on a merge. | resourcesToCopy | array of [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)

<a name="merge-analysis"/>

## 2.9 The "MergeAnalysis" Data Type

The `MergeAnalysis` data type defines a representation of a merge analysis.

### identifier

The identifier for the `MergeAnalysis` data type is:

`http://familysearch.org/v1//MergeAnalysis`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
survivor | Reference to the survivor of the merge. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. MUST resolve to an instance of [`Subject`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#subject).
duplicate | Reference to the duplicate of the merge. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. MUST resolve to an instance of [`Subject`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#subject).
survivorResources | The resources on the survivor that should be preserved during a merge operation. | List of [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).
duplicateResources | The resources on the duplicate that should be preserved during a merge operation. | List of [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).
conflictingResources | The resources that conflict. | List of [`MergeConflict`](#merge-conflict) | OPTIONAL.

### 2.9.1 The "MergeAnalysis" XML Type and Element

The `fs:MergeAnalysis` XML type is used to (de)serialize the `http://familysearch.org/v1/MergeAnalysis` data type.
The `fs:mergeAnalysis` XML element is used to provide instances of the `fs:MergeAnalysis` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
survivor | Reference to the survivor of the merge. | fs:survivor | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
duplicate | Reference to the duplicate of the merge. | fs:duplicate | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
survivorResources | The resources on the survivor that should be preserved during a merge operation. | fs:survivorResource | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
duplicateResources | The resources on the duplicate that should be preserved during a merge operation. | fs:duplicateResource | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
conflictingResources | The resources that conflict. | fs:conflictingResource | [`MergeConflict`](#merge-conflict)

### 2.9.2 The "MergeAnalysis" JSON Type

The `MergeAnalysis` JSON type is used to (de)serialize the `http://familysearch.org/v1/MergeAnalysis` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
survivor | Reference to the survivor of the merge. | survivor | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
duplicate | Reference to the duplicate of the merge. | duplicate | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
survivorResources | The resources on the survivor that should be preserved during a merge operation. | survivorResources | array of [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
duplicateResources | The resources on the duplicate that should be preserved during a merge operation. | duplicateResources | array of [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
conflictingResources | The resources that conflict. | conflictingResources | array of [`MergeConflict`](#merge-conflict)

<a name="merge-conflict"/>

## 2.10 The "MergeConflict" Data Type

The `MergeConflict` data type defines a representation of a merge conflict.

### identifier

The identifier for the `MergeConflict` data type is:

`http://familysearch.org/v1//MergeConflict`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
survivorResource | Reference to the resource on the survivor that conflicts. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).
duplicateResource | Reference to the resource on the duplicate that conflicts. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. MUST resolve to an instance of [`Conclusion`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).

### 2.10.1 The "MergeConflict" XML Type and Element

The `fs:MergeConflict` XML type is used to (de)serialize the `http://familysearch.org/v1/MergeConflict` data type.
The `fs:mergeConflict` XML element is used to provide instances of the `fs:MergeConflict` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
survivorResource | Reference to the resource on the survivor that conflicts. | fs:survivorResource | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
duplicateResource | Reference to the resource on the duplicate that conflicts. | fs:duplicateResource | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)

### 2.10.2 The "MergeConflict" JSON Type

The `MergeConflict` JSON type is used to (de)serialize the `http://familysearch.org/v1/MergeConflict` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
survivorResource | Reference to the resource on the survivor that conflicts. | survivorResource | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
duplicateResource | Reference to the resource on the duplicate that conflicts. | duplicateResource | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)

<a name="nameform-info"/>

## 2.11 The "NameFormInfo" Data Type

The `NameFormInfo` data type defines extra information about a name form.

### identifier

The identifier for the `NameFormInfo` data type is:

`http://familysearch.org/v1//NameFormInfo`

Instances of `NameFormInfo` can be reasonably expected as extension elements to the [`NameForm` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#name-form).

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
order | The order of the name form. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. Use of a [known name order](#known-name-order) is RECOMMENDED.

### 2.11.1 The "NameFormInfo" XML Type and Element

The `fs:NameFormInfo` XML type is used to (de)serialize the `http://familysearch.org/v1/NameFormInfo` data type.
The `fs:NameFormInfo` XML element is used to provide instances of the `fs:NameFormInfo` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
order | The order of the name form. | order (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)

### 2.11.2 The "NameFormInfo" JSON Type

The `NameFormInfo` JSON type is used to (de)serialize the `http://familysearch.org/v1/NameFormInfo` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
order | The order of the name form. | order | string

<a name="known-name-order"/>

### 2.11.3 Known Name Order

The following name orders are defined by FamilySearch Extensions:

name | value
-----|-------
`http://familysearch.org/v1/Eurotypic`| Eurotypic name order.
`http://familysearch.org/v1/Sinotypic`| Sinotypic name order.

<a name="search-info"/>

## 2.12 The "SearchInfo" Data Type

The `SearchInfo` data type defines a representation of information about a search.

Instances of `SearchInfo` can be reasonably expected as extension elements to the [`Entry` Data Type](https://github.com/FamilySearch/gedcomx-rs/blob/master/specifications/atom-model-specification.md#atom-entry-extensions).

### identifier

The identifier for the `SearchInfo` data type is:

`http://familysearch.org/v1/SearchInfo`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
totalHits | The total number of hits in the search results. | integer | OPTIONAL.
closeHits | The total number of "close" hits in the search results. | integer | OPTIONAL.

### 2.12.1 The "SearchInfo" XML Type and Element

The `fs:SearchInfo` XML type is used to (de)serialize the `http://familysearch.org/v1/SearchInfo` data type.
The `fs:searchInfo` XML element is used to provide instances of the `fs:SearchInfo` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
totalHits | The total number of hits in the search results. | fs:totalHits | xsd:integer
closeHits | The total number of "close" hits in the search results. | fs:closeHits | xsd:integer

### 2.12.2 The "SearchInfo" JSON Type

The `SearchInfo` JSON type is used to (de)serialize the `http://familysearch.org/v1/SearchInfo` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
totalHits | The total number of hits in the search results. | totalHits | number
closeHits | The total number of "close" hits in the search results. | closeHits | number

<a name="reservation"/>

## 2.13 The "Reservation" Data Type

The `Reservation` data type defines a representation of an ordinance reservation

Instances of `Reservation` can be reasonably expected as extension elements to the [`Person` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri).

### extension

The `Reservation` data type extends the [`Conclusion` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion).

### identifier

The identifier for the `Reservation` data type is:

`http://familysearch.org/v1/Reservation`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
type | The type of the ordinance reservation. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED. Use of a [known ordinance type](#known-ordinance-type) is RECOMMENDED.
status | The status of the ordinance reservation. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL.
spouse | A reference to the spouse. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).
father | A reference to the father. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).
mother | A reference to the father. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).
assignee | A reference to the father. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If present, MUST resolve to an instance of [`Person`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#person).

### 2.13.1 The "Reservation" XML Type and Element

The `fs:Reservation` XML type is used to (de)serialize the `http://familysearch.org/v1/Reservation` data type.
The `fs:reservation` XML element is used to provide instances of the `fs:Reservation` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
type | The type of the ordinance reservation. | type (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri) 
status | The status of the ordinance reservation. | status (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
spouse | A reference to the spouse. | fs:spouse | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
father | A reference to the father. | fs:father | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
mother | A reference to the mother. | fs:mother | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
assignee | A reference to the assignee. | fs:assignee | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)

### 2.13.2 The "Reservation" JSON Type

The `Reservation` JSON type is used to (de)serialize the `http://familysearch.org/v1/Reservation` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
type | The type of the ordinance reservation. | type | string
status | The status of the ordinance reservation. | status | string
spouse | A reference to the spouse. | spouse | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
father | A reference to the father. | father | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
mother | A reference to the mother. | mother | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)
assignee | A reference to the assignee. | assignee | [ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#resource-reference)

<a name="known-ordinance-type"/>

### 2.13.3 Known Ordinance Types

The following ordinance types are defined by FamilySearch Extensions:

name | value
-----|-------
`http://lds.org/Baptism`| Baptism
`http://lds.org/Confirmation`| Confirmation
`http://lds.org/Initiatory`| Initiatory
`http://lds.org/Endowment`| Endowment
`http://lds.org/SealingToSpouse`| Sealing to Spouse
`http://lds.org/SealingChildToParents`| Sealing to Parents

<a name="ordinance"/>

## 2.14 The "Ordinance" Data Type

The `Ordinance` data type defines a representation of an ordinance.

Instances of `Ordinance` can be reasonably expected as extension elements to the [`Person` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri).

### extension

The `Ordinance` data type extends the [`Reservation` Data Type](#reservation).

### identifier

The identifier for the `Ordinance` data type is:

`http://familysearch.org/v1/Ordinance`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
living | Indicator of a living ordinance. | boolean | OPTIONAL.
date | The date of the ordinance. | [`http://gedcomx.org/v1/Date`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#conclusion-date) | OPTIONAL
templeCode | Id of the temple in which the ordinance was performed. | string | OPTIONAL.

### 2.14.1 The "Ordinance" XML Type and Element

The `fs:Ordinance` XML type is used to (de)serialize the `http://familysearch.org/v1/Ordinance` data type.
The `fs:ordinance` XML element is used to provide instances of the `fs:Ordinance` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
living | Indicator of a living ordinance. | living (attribute) | xsd:boolean
date | The date of the ordinance. | fs:date | [`gx:Date`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#date)
templeCode | Id of the temple in which the ordinance was performed. | fs:templeCode | xsd:string

### 2.14.2 The "Ordinance" JSON Type

The `Ordinance` JSON type is used to (de)serialize the `http://familysearch.org/v1/Ordinance` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
living | Indicator of a living ordinance. | living | boolean
date | The date of the ordinance. | date | [`Date`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/json-format-specification.md#date)
templeCode | Id of the temple in which the ordinance was performed. | templeCode | string

<a name="tag"/>

## 2.15 The "Tag" Data Type

The `Tag` data type defines a source reference tag.

Instances of `Tag` can be reasonably expected as extension elements to the [`SourceReference` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#source-reference).

### identifier

The identifier for the `Tag` data type is:

`http://familysearch.org/v1/Tag`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
resource | Reference to the tag. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | REQUIRED.

### 2.15.1 The "Tag" XML Type and Element

The `fs:Tag` XML type is used to (de)serialize the `http://familysearch.org/v1/Tag` data type.
The `fs:tag` XML element is used to provide instances of the `fs:Tag` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
resource | Reference to the tag. | resource (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)

### 2.15.2 The "Tag" JSON Type

The `Tag` JSON type is used to (de)serialize the `http://familysearch.org/v1/Tag` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
resource | Reference to the tag. | resource | string

<a name="user"/>

## 2.16 The "User" Data Type

The `User` data type defines a FamilySearch user.

### identifier

The identifier for the `User` data type is:

`http://familysearch.org/v1/User`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
contactName| Contact name of the user. | string | OPTIONAL.
helperAccessPin| Helper access pin of the user. | string | OPTIONAL.
fullName| Full name of the user. | string | OPTIONAL.
givenName| Given name of the user. | string | OPTIONAL.
familyName| Given name of the user. | string | OPTIONAL.
email| Email of the user. | string | OPTIONAL.
alternateEmail| Alternate email of the user. | string | OPTIONAL.
country|Country of the user. | string | OPTIONAL.
gender|Gender of the user. | string | OPTIONAL.
birthDate|Birth date of the user. | string | OPTIONAL.
phoneNumber| Phone number of the user. | string | OPTIONAL.
mobilePhoneNumber| Mobile phone number of the user. | string | OPTIONAL.
mailingAddress| Mailing address of the user. | string | OPTIONAL.
preferredLanguage| Preferred language of the user. | string | OPTIONAL.
displayName| Display name of the user. | string | OPTIONAL.
personId| Tree person id of the user. | string | OPTIONAL.
treeUserId| Tree user id of the user. | string | OPTIONAL.

### 2.16.1 The "User" XML Type and Element

The `fs:User` XML type is used to (de)serialize the `http://familysearch.org/v1/User` data type.
The `fs:user` XML element is used to provide instances of the `fs:User` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
contactName | Contact name of the user. | fs:contactName | xsd:string
helperAccessPin| Helper access pin of the user. | fs:helperAccessPin | xsd:string
fullName| Full name of the user. | fs:fullName | xsd:string
givenName| Given name of the user. | fs:givenName | xsd:string
familyName| Given name of the user. | fs:familyName | xsd:string
email| Email of the user. | fs:email | xsd:string
alternateEmail| Alternate email of the user. | fs:alternateEmail | xsd:string
country|Country of the user. | fs:country | xsd:string
gender|Gender of the user. | fs:gender | xsd:string
birthDate|Birth date of the user. | fs:birthDate | xsd:string
phoneNumber| Phone number of the user. | fs:phoneNumber | xsd:string
mobilePhoneNumber| Mobile phone number of the user. | fs:mobilePhoneNumber | xsd:string
mailingAddress| Mailing address of the user. | fs:mailingAddress | xsd:string
preferredLanguage| Preferred language of the user. | fs:preferredLanguage | xsd:string
displayName| Display name of the user. | fs:displayName | xsd:string
personId| Tree person id of the user. | fs:personId | xsd:string
treeUserId| Tree user id of the user. | fs:treeUserId | xsd:string

### 2.16.2 The "User" JSON Type

The `User` JSON type is used to (de)serialize the `http://familysearch.org/v1/User` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
contactName | Contact name of the user. | contactName | string
helperAccessPin| Helper access pin of the user. | helperAccessPin | string
fullName| Full name of the user. | fullName | string
givenName| Given name of the user. | givenName | string
familyName| Given name of the user. | familyName | string
email| Email of the user. | email | string
alternateEmail| Alternate email of the user. | alternateEmail | string
country|Country of the user. | country | string
gender|Gender of the user. | gender | string
birthDate|Birth date of the user. | birthDate | string
phoneNumber| Phone number of the user. | phoneNumber | string
mobilePhoneNumber| Mobile phone number of the user. | mobilePhoneNumber | string
mailingAddress| Mailing address of the user. | mailingAddress | string
preferredLanguage| Preferred language of the user. | preferredLanguage | string
displayName| Display name of the user. | displayName | string
personId| Tree person id of the user. | personId | string
treeUserId| Tree user id of the user. | treeUserId | string

<a name="error"/>

## 2.17 The "Error" Data Type

The `Error` data type defines an error that occurred.

Instances of `Error` can be reasonably expected as extension elements to the [`FamilySearchPlatform` XML Data Type](#fsp-xml) and the [`FamilySearchPlatform` JSON Data Type](#fsp-json).

### identifier

The identifier for the `Error` data type is:

`http://familysearch.org/v1/Error`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
code | The error code. | integer | OPTIONAL.
label | The error label. | string | OPTIONAL.
message | The error message. | string | OPTIONAL.
stacktrace | The error stack trace. | string | OPTIONAL.

### 2.17.1 The "Error" XML Type and Element

The `fs:Error` XML type is used to (de)serialize the `http://familysearch.org/v1/Error` data type.
The `fs:error` XML element is used to provide instances of the `fs:Error` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
code | The error code. | fs:code | xsd:integer
label | The error label. | fs:label | xsd:string
message | The error message. | fs:message | xsd:string
stacktrace | The error stack trace. | fs:stacktrace | xsd:string

### 2.17.2 The "Error" JSON Type

The `Error` JSON type is used to (de)serialize the `http://familysearch.org/v1/Error` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
code | The error code. | code | number
label | The error label. | label | string
message | The error message. | message | string
stacktrace | The error stack trace. | stacktrace | string

<a name="feature"/>

## 2.18 The "Feature" Data Type

The `Feature` data type defines an feature of the FamilySearch API.

### identifier

The identifier for the `Feature` data type is:

`http://familysearch.org/v1/Feature`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
name | The feature name. | string | OPTIONAL.
description | The feature description. | string | OPTIONAL.
enabled | Whether the feature is enabled. | boolean | OPTIONAL.
activationDate | The feature activation date. | timestamp | OPTIONAL.

### 2.18.1 The "Feature" XML Type and Element

The `fs:Feature` XML type is used to (de)serialize the `http://familysearch.org/v1/Feature` data type.
The `fs:feature` XML element is used to provide instances of the `fs:Feature` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
name | The feature name. | fs:name | xsd:string
description | The feature description. | fs:description | xsd:string
enabled | Whether the feature is enabled. | fs:enabled | xsd:boolean
activationDate | The feature activation date. | fs:activationDate | xsd:dateTime

### 2.18.2 The "Feature" JSON Type

The `Feature` JSON type is used to (de)serialize the `http://familysearch.org/v1/Feature` data type.

#### properties

name | description | JSON member | JSON object type
-----|-------------|--------------|---------
name | The feature name. | name | string
description | The feature description. | description | string
enabled | Whether the feature is enabled. | enabled | boolean
activationDate | The feature activation date. | activationDate | number (milliseconds since epoch)

<a name="feedback-info"/>

## 2.19 The "FeedbackInfo" Data Type

The `FeedbackInfo` data type defines a representation of feedback that can be submitted to
the FamilySearch places database.

Instances of `FeedbackInfo` can be reasonably expected as extension elements to the [`PlaceDescription` Data Type](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#place-description).

### identifier

The identifier for the `FeedbackInfo` data type is:

`http://familysearch.org/v1/FeedbackInfo`

### properties

name  | description | data type | constraints
------|-------------|-----------|------------
resolution | Resolution of the feedback. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL.
status | Status of the feedback. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL.
place | Reference to the place that was created as a result of this feedback, if applicable. | [`URI`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#uri) | OPTIONAL. If provided, MUST resolve to an instance of [`PlaceDescription`](https://github.com/FamilySearch/gedcomx/blob/master/specifications/conceptual-model-specification.md#place-description).
details | Any notes or details provided as part of the feedback. | string | OPTIONAL.


### 2.19.1 The "FeedbackInfo" XML Type and Element

The `fs:FeedbackInfo` XML type is used to (de)serialize the `http://familysearch.org/v1/FeedbackInfo` data type.
The `fs:feedbackInfo` XML element is used to provide instances of the `fs:FeedbackInfo` XML type as extension elements.

#### properties

name | description | XML property | XML type
-----|-------------|--------------|---------
resolution | Resolution of the feedback. | resolution (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
status | Status of the feedback. | status (attribute) | [anyURI](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#uri)
place | Reference to the place that was created as a result of this feedback, if applicable. | fs:place | [gx:ResourceReference](https://github.com/FamilySearch/gedcomx/blob/master/specifications/xml-format-specification.md#resource-reference)
details | Any notes or details provided as part of the feedback. | fs:details | xsd:string

### 2.19.2 The "FeedbackInfo" JSON Type

The `ArtifactMetadata` JSON type is used to (de)serialize the `http://familysearch.org/v1/ArtifactMetadata` data type.

<a name="fsp-xml"/>

## 2.20 The "FamilySearchPlatform" XML Data Type

The `gx:FamilySearchPlatform` XML type is used as a container for a set of FamilySearch data.

### extension

The `gx:FamilySearchPlatform` XML type extends the `gx:Gedcomx` data type.

### properties

name | description | XML property | XML type | constraints
-----|-------------|--------------|----------|------------
mergeAnalyses | The list of merge analysies contained in the data set. | fs:mergeAnalysis | [fs:MergeAnalysis](#merge-analysis) | OPTIONAL.
merges | The list of merges contained in the data set. | fs:merge | [fs:Merge](#merge) | OPTIONAL.
childAndParentsRelationships | The list of child-and-parents relationships contained in the data set. | fs:childAndParentsRelationship | [fs:ChildAndParentsRelationship](#child-and-parents-relationship) | OPTIONAL.
discussions | The list of discussions contained in the data set. | fs:discussion | [fs:Discussion](#discussion) | OPTIONAL.
users | The list of users contained in the data set. | fs:user | [fs:User](#user) | OPTIONAL.
features | The list of features contained in the data set. | fs:feature | [fs:Feature](#feature) | OPTIONAL.

<a name="fsp-json"/>

## 2.21 The "FamilySearchPlatform" JSON Data Type

The `FamilySearchPlatform` JSON type is used as a container for a set of FamilySearch data.

### extension

The `FamilySearchPlatform` JSON type extends the `Gedcomx` data type.

### properties

name | description | JSON property | JSON type | constraints
-----|-------------|--------------|----------|------------
mergeAnalyses | The list of merge analysies contained in the data set. | mergeAnalyses | array of [MergeAnalysis](#merge-analysis) | OPTIONAL.
merges | The list of merges contained in the data set. | merges | array of [Merge](#merge) | OPTIONAL.
childAndParentsRelationships | The list of child-and-parents relationships contained in the data set. | childAndParentsRelationships | array of [ChildAndParentsRelationship](#child-and-parents-relationship) | OPTIONAL.
discussions | The list of discussions contained in the data set. | discussions | array of [Discussion](#discussion) | OPTIONAL.
users | The list of users contained in the data set. | users | array of [User](#user) | OPTIONAL.
features | The list of features contained in the data set. | features | array of [Feature](#feature) | OPTIONAL.
