---
v: 3

title: Using the Constrained RESTful Application Language (CoRAL) with the Admin Interface for the OSCORE Group Manager
abbrev: CoRAL Admin Interface for the OSCORE GM
docname: draft-ietf-ace-oscore-gm-admin-coral-latest


# stand_alone: true

ipr: trust200902
area: Internet
wg: ACE Working Group
kw: Internet-Draft
cat: std
submissiontype: IETF

coding: utf-8
pi:    # can use array (if all yes) or hash here

  toc: yes
  sortrefs:   # defaults to yes
  symrefs: yes

author:
      -
        ins: M. Tiloca
        name: Marco Tiloca
        org: RISE AB
        street: Isafjordsgatan 22
        city: Kista
        code: SE-16440 Stockholm
        country: Sweden
        email: marco.tiloca@ri.se
      -
        ins: R. Höglund
        name: Rikard Höglund
        org: RISE AB
        street: Isafjordsgatan 22
        city: Kista
        code: SE-16440 Stockholm
        country: Sweden
        email: rikard.hoglund@ri.se

normative:
  I-D.ietf-core-oscore-groupcomm:
  I-D.ietf-ace-key-groupcomm:
  I-D.ietf-ace-key-groupcomm-oscore:
  I-D.ietf-ace-oscore-gm-admin:
  I-D.ietf-core-coral:
  I-D.ietf-core-groupcomm-bis:
  I-D.bormann-cbor-edn-literals:
  I-D.ietf-cbor-packed:
  I-D.ietf-core-href:
  RFC2119:
  RFC3986:
  RFC6690:
  RFC6749:
  RFC7252:
  RFC7641:
  RFC8132:
  RFC8174:
  RFC8613:
  RFC8949:
  RFC9052:
  RFC9053:
  RFC9200:
  RFC9202:
  RFC9203:
  RFC9237:
  CURIE-20101216:
    author:
      -
        ins: M. Birbeck
        name: Mark Birbeck
      -
        ins: S. McCarron
        name: Shane McCarron
    title: CURIE Syntax 1.0 - A syntax for expressing Compact URIs - W3C Working Group Note
    date: 2010-12-16
    target: http://www.w3.org/TR/2010/NOTE-curie-20101216

informative:
  I-D.tiloca-core-oscore-discovery:
  I-D.hartke-t2trg-coral-reef:
  I-D.ietf-cose-cbor-encoded-cert:
  I-D.ietf-core-target-attr:
  RFC5280:
  RFC8392:
  RFC9147:
  RFC9147:

entity:
  SELF: "[RFC-XXXX]"

--- abstract

TBD

--- middle

# Introduction # {#intro}

TBD

The examples presented in this document are expressed in CBOR diagnostic notation, and refer to values from external dictionaries using Packed CBOR {{I-D.ietf-cbor-packed}}. {{notation-coral-examples}} introduces the notation and assumptions used in the examples.

TBD

## Terminology ## {#terminology}

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 {{RFC2119}} {{RFC8174}} when, and only when, they appear in all capitals, as shown here.

Readers are expected to be familiar with the terms and concepts from the following specifications.

* CBOR {{RFC8949}}, Packed CBOR {{I-D.ietf-cbor-packed}}, and COSE {{RFC9052}}{{RFC9053}}.

* The Constrained RESTful Application Language (CoRAL) {{I-D.ietf-core-coral}} and Constrained Resource Identifiers (CRIs) defined in {{I-D.ietf-core-href}}.

* The CoAP protocol {{RFC7252}}, also in group communication scenarios {{I-D.ietf-core-groupcomm-bis}}. These include the concepts of:

   - "application group", as a set of CoAP nodes that share a common set of resources; and of

   - "security group", as a set of CoAP nodes that share the same security material, and use it to protect and verify exchanged messages.

* The OSCORE {{RFC8613}} and Group OSCORE {{I-D.ietf-core-oscore-groupcomm}} security protocols. These especially include the concepts of:

   - Group Manager, as the entity responsible for a set of OSCORE groups where communications among members are secured using Group OSCORE. An OSCORE group is used as security group for one or many application groups.

   - Authentication credential, as the set of information associated with an entity, including that entity's public key and parameters associated with the public key. Examples of authentication credentials are CBOR Web Tokens (CWTs) and CWT Claims Sets (CCSs) {{RFC8392}}, X.509 certificates {{RFC5280}} and C509 certificates {{I-D.ietf-cose-cbor-encoded-cert}}.

* The ACE framework for authentication and authorization {{RFC9200}}. The terminology for entities in the considered architecture is defined in OAuth 2.0 {{RFC6749}}. In particular, this includes Client (C), Resource Server (RS), and Authorization Server (AS).

* The management of keying material for groups in ACE {{I-D.ietf-ace-key-groupcomm}} and specifically for OSCORE groups {{I-D.ietf-ace-key-groupcomm-oscore}}. These include the concept of group-membership resource hosted by the Group Manager, that new members access to join the OSCORE group, while current members can access to retrieve updated keying material.

Readers are also expected to be familiar with the terms and concepts used in {{I-D.ietf-ace-oscore-gm-admin}}, wih particular reference to: "Administrator", "Group name", "Group-collection resource", "Group-configuration resource", and "Admin endpoint".

Note that, unless otherwise indicated, the term "endpoint" is used here following its OAuth definition, aimed at denoting resources such as /token and /introspect at the AS, and /authz-info at the RS. This document does not use the CoAP definition of "endpoint", which is "An entity participating in the CoAP protocol".

## Notation and Assumptions in the Examples ## {#notation-coral-examples}

As per {{Section 2.4 of I-D.ietf-core-coral}}, CoRAL expresses Uniform Resource Identifiers (URIs) {{RFC3986}} as Constrained Resource Identifier (CRI) references {{I-D.ietf-core-href}}.

The examples in this document use the following notation.

When using the CURIE syntax {{CURIE-20101216}}, the following applies.

* 'core.osc.gcoll' stands for http://coreapps.org/core.osc.gcoll#

* 'core.osc.gconf' stands for http://coreapps.org/core.osc.gconf#

* 'linkformat' stands for http://www.iana.org/assignments/linkformat

   This URI is to be defined with IANA, together with other URIs that build on it through further path segments, e.g., http://www.iana.org/assignments/linkformat/rt

When using a URI http://www.iana.org/assignments/linkformat/SEG1/SEG2

* The path segment SEG1 is the name of a web link target attribute.

   Names of target attributes used in Link Format {{RFC6690}} are expected to be coordinated through the "Target Attributes" registry defined in {{I-D.ietf-core-target-attr}}.

* The path segment SEG2 is the value of the target attribute.

The notation cri'' introduced in {{I-D.bormann-cbor-edn-literals}} is used to represent CRIs {{I-D.ietf-core-href}}. This format is not expected to be sent over the network.

Packed CBOR {{I-D.ietf-cbor-packed}} is also used, thus reducing representation size. The examples especially refer to the values from the two shared item tables in {{sec-packed-cbor-tables}}.

Finally, the examples consider a Group Manager with address \[2001:db8::ab\], and use the CoAP Content-Format ID 65087 for the media-type application/coral+cbor.

# Group Administration # {#overview}

TBD

## Managing OSCORE Groups ## {#managing-groups}

TBD

## Collection Representation

TBD

## Discovery

TBD

# Format of Scope # {#scope-format}

TBD

## On Using Group Name Patterns

TBD

# Getting Access to the Group Manager # {#getting-access}

TBD

## Multiple Administrators for the Same OSCORE Group

TBD

# Group Configurations # {#group-configurations}

TBD

## Group Configuration Representation ## {#config-repr}

TBD

### Configuration Properties ### {#config-repr-config-properties}

TBD

### Status Properties ### {#config-repr-status-properties}

TBD

## Default Values {#default-values}

TBD

### Configuration Parameters {#default-values-conf}

TBD

### Status Parameters

TBD

# Interactions with the Group Manager # {#interactions}

The same as defined in {{Section 6 of I-D.ietf-ace-oscore-gm-admin}} holds, with the following differences.

* The Content-Format in messages containing a payload is set to application/coral+cbor, defined in {{Section 7.2 of I-D.ietf-core-coral}}.

* The parameters 'sign_params', 'ecdh_params', 'app_groups' and 'group_policies' are referred to as "structured parameters".

* If a message payload specifies a link element corresponding to a structured parameter, then:

   - The payload MUST NOT include any link element corresponding to an inner information element of that structured parameter.

   - The link element MUST have the link target with value "false" (0xf4) for indicating the structured parameter with no elements.

      Editor's note: this should change to using an empty CBOR array or an empty CBOR map as appropriate, once this is made explicitly possible in the binary format of link items in CoRAL (see Section 3.1.4 of {{I-D.ietf-core-coral}}).

* If a message payload specifies an information element of a structured parameter from the group configuration, then that information element MUST be specified by means of the corresponding link element.

## Retrieve the Full List of Group Configurations ## {#collection-resource-get}

The same as defined in {{Section 6.1 of I-D.ietf-ace-oscore-gm-admin}} holds.

An example of message exchange is shown below.

~~~~~~~~~~~
=> 0.01 GET
   Uri-Path: manage

<= 2.05 Content
   Content-Format: 65087 (application/coral+cbor)

   Payload:

   [
     [1, cri'coap://[2001:db8::ab]/manage'],
     [2, 6(17) / item 50 for core.osc.gcoll:item /, cri'/gp1', [
       [2, simple(6) / item 6 for linkformat:rt /,
        6(-200) / item 415 for cri'http://www.iana.org/assignments
                                   /linkformat/rt/core.osc.gconf' /]
     ]],
     [2, 6(17) / item 50 for core.osc.gcoll:item /, cri'/gp2', [
       [2, simple(6) / item 6 for linkformat:rt /,
        6(-200) / item 415 for cri'http://www.iana.org/assignments
                                   /linkformat/rt/core.osc.gconf' /]
     ]],
     [2, 6(17) / item 50 for core.osc.gcoll:item /, cri'/gp3', [
       [2, simple(6) / item 6 for linkformat:rt /,
        6(-200) / item 415 for cri'http://www.iana.org/assignments
                                   /linkformat/rt/core.osc.gconf' /]
     ]]
   ]
~~~~~~~~~~~

## Retrieve a List of Group Configurations by Filters ## {#collection-resource-fetch}

The same as defined in {{Section 6.2 of I-D.ietf-ace-oscore-gm-admin}} holds, with the following differences.

* The filter criteria are specified in the request payload with top-level link elements, each of which corresponds to an entry of the group configuration (see {{config-repr}}), with the exception of non-empty structured parameters.

* If names of application groups are used as filter criteria, each element of the 'app_groups' array from the status properties is included as a separate link element with name 'app_group'.

* With the exception of the 'app_group' element, a valid request MUST NOT include the same element multiple times. Element values are the ones admitted for the corresponding labels in the POST request for creating a group configuration (see {{collection-resource-post}}).

An example of message exchange is shown below.

~~~~~~~~~~~
=> 0.05 FETCH
   Uri-Path: manage
   Content-Format: 65087 (application/coral+cbor)

   Payload:

   [
     [2, 6(27) / item 70 for core.osc.gconf:group_mode /, true],
     [2, 6(-28) / item 71 for core.osc.gconf:sign_enc_alg /, 10],
     [2, 6(26) / item 68 for core.osc.gconf:hkdf /, 5]
   ]

<= 2.05 Content
   Content-Format: 65087 (application/coral+cbor)

   Payload:

   [
    [1, cri'coap://[2001:db8::ab]/manage'],
    [2, 6(17) / item 50 for core.osc.gcoll:item /, cri'/gp1', [
      [2, simple(6) / item 6 for linkformat:rt /,
       6(-200) / item 415 for cri'http://www.iana.org/assignments
                                  /linkformat/rt/core.osc.gconf' /]
    ]],
    [2, 6(17) / item 50 for core.osc.gcoll:item /, cri'/gp2', [
      [2, simple(6) / item 6 for linkformat:rt /,
       6(-200) / item 415 for cri'http://www.iana.org/assignments
                                  /linkformat/rt/core.osc.gconf' /]
    ]],
    [2, 6(17) / item 50 for core.osc.gcoll:item /, cri'/gp3', [
      [2, simple(6) / item 6 for linkformat:rt /,
       6(-200) / item 415 for cri'http://www.iana.org/assignments
                                  /linkformat/rt/core.osc.gconf' /]
    ]]
   ]
~~~~~~~~~~~

## Create a New Group Configuration ## {#collection-resource-post}

The same as defined in {{Section 6.3 of I-D.ietf-ace-oscore-gm-admin}} holds, with the following differences.

* Each link element of the request payload corresponds to an entry of the group configuration (see {{config-repr}}), with the exception of non-empty structured parameters.

* Each element of the 'app_groups' array from the status properties is included as a separate element with name 'app_group'.

* If the payload of the POST request specifies the 'app_group' link element multiple times, then the Group Manager MUST NOT respond with a 4.00 (Bad Request) response.

* The payload of the response includes one link element for each specified parameter, with the exception of non-empty structured parameters.

* Each element of the 'app_groups' array from the status properties is included as a separate element with name 'app_group'.

* If the Administrator performs the registration of the group-membership resource, the names of the application groups using the OSCORE group MUST take the values possibly specified by the elements of the different 'app_group' link elements in the POST request.

An example of message exchange is shown below.

~~~~~~~~~~~
=> 0.02 POST
   Uri-Path: manage
   Content-Format: 65087 (application/coral+cbor)

   Payload:

   [
     [2, 6(-28) / item 71 for core.osc.gconf:sign_enc_alg /, 10],
     [2, 6(26) / item 68 for core.osc.gconf:hkdf /, 5],
     [2, 6(-31) / item 77 for core.osc.gconf:pairwise_mode /, true],
     [2, 6(-36) / item 87 for core.osc.gconf:active /, true],
     [2, 6(36) / item 88 for core.osc.gconf:group_name /, "gp4"],
     [2, 6(-37) / item 89 for core.osc.gconf:group_title /,
      "rooms 1 and 2"],
     [2, 6(39) / item 94 for core.osc.gconf:app_group /, "room 1"],
     [2, 6(39) / item 94 for core.osc.gconf:app_group /, "room 2"],
     [2, 6(43) / item 102 for core.osc.gconf:as_uri /,
      cri'coap://as.example.com/token']
   ]

<= 2.01 Created
   Location-Path: manage
   Location-Path: gp4
   Content-Format: 65087 (application/coral+cbor)

   Payload:

   [
     [2, 6(36) / item 88 for core.osc.gconf:group_name /, "gp4"],
     [2, 6(-41) / item 97 for core.osc.gconf:joining_uri /,
      cri'coap://[2001:db8::ab]/ace-group/gp4/'],
     [2, 6(43) / item 102 for core.osc.gconf:as_uri /,
      cri'coap://as.example.com/token']
   ]
~~~~~~~~~~~

## Retrieve a Group Configuration ## {#configuration-resource-get}

TBD

## Retrieve Part of a Group Configuration by Filters ## {#configuration-resource-fetch}

TBD

## Overwrite a Group Configuration ## {#configuration-resource-put}

TBD

### Effects on Joining Nodes ### {#sssec-effects-overwrite-joining-nodes}

TBD

### Effects on the Group Members ### {#sssec-effects-overwrite-group-members}

TBD

## Selective Update of a Group Configuration ## {#configuration-resource-patch}

TBD

### Effects on Joining Nodes ###

TBD

### Effects on the Group Members ###

TBD

## Delete a Group Configuration ## {#configuration-resource-delete}

TBD

### Effects on the Group Members ###

TBD

# Supported Top-Level Elements

TBD

# Security Considerations # {#sec-security-considerations}

Security considerations are inherited from the ACE framework for Authentication and Authorization {{RFC9200}}, and from the specific transport profile of ACE used between the Administrator and the Group Manager, such as {{RFC9202}} and {{RFC9203}}.

The same security considerations from {{I-D.ietf-ace-key-groupcomm}} and {{I-D.ietf-ace-key-groupcomm-oscore}} also apply, with particular reference to the process of rekeying OSCORE groups.

The same security considerations from {{I-D.ietf-ace-oscore-gm-admin}} also apply, as well for the security considerations for CoRAL {{I-D.ietf-core-coral}} and Packed CBOR {{I-D.ietf-cbor-packed}}.

# IANA Considerations # {#iana}

This document has no actions for IANA.

--- back

# Shared item tables for Packed CBOR # {#sec-packed-cbor-tables}

This appendix defines the two shared item tables that the examples in this document refer to for using Packed CBOR {{I-D.ietf-cbor-packed}}.

The notation cri'' introduced in {{I-D.bormann-cbor-edn-literals}} is used to represent CRIs {{I-D.ietf-core-href}}.

## Compression of CoRAL predicates

The following shared item table is used for compressing CoRAL predicates, as per {{Section 2.2 of I-D.ietf-cbor-packed}}.

~~~~~~~~~~~
+-------+--------------------------------------------------------+
| Index | Item                                                   |
+-------+--------------------------------------------------------+
| 6     | cri'http://www.iana.org/assignments/linkformat/rt'     |
+-------+--------------------------------------------------------+
| 50    | cri'http://coreapps.org/core.osc.gcoll#item'           |
+-------+--------------------------------------------------------+
| 68    | cri'http://coreapps.org/core.osc.gconf#hkdf'           |
+-------+--------------------------------------------------------+
| 69    | cri'http://coreapps.org/core.osc.gconf#cred_fmt'       |
+-------+--------------------------------------------------------+
| 70    | cri'http://coreapps.org/core.osc.gconf#group_mode'     |
+-------+--------------------------------------------------------+
| 71    | cri'http://coreapps.org/core.osc.gconf#sign_enc_alg'   |
+-------+--------------------------------------------------------+
| 72    | cri'http://coreapps.org/core.osc.gconf#sign_alg'       |
+-------+--------------------------------------------------------+
| 73    | cri'http://coreapps.org/core.osc.gconf#sign_params'    |
+-------+--------------------------------------------------------+
| 74    | cri'http://coreapps.org/core.osc.gconf#sign_params     |
|       |     .alg_capab.key_type'                               |
+-------+--------------------------------------------------------+
| 75    | cri'http://coreapps.org/core.osc.gconf#sign_params     |
|       |     .key_type_capab.key_type'                          |
+-------+--------------------------------------------------------+
| 76    | cri'http://coreapps.org/core.osc.gconf#sign_params     |
|       |     .key_type_capab.curve'                             |
+-------+--------------------------------------------------------+
| 77    | cri'http://coreapps.org/core.osc.gconf#pairwise_mode'  |
+-------+--------------------------------------------------------+
| 78    | cri'http://coreapps.org/core.osc.gconf#alg'            |
+-------+--------------------------------------------------------+
| 79    | cri'http://coreapps.org/core.osc.gconf#ecdh_alg'       |
+-------+--------------------------------------------------------+
| 80    | cri'http://coreapps.org/core.osc.gconf#ecdh_params'    |
+-------+--------------------------------------------------------+
| 81    | cri'http://coreapps.org/core.osc.gconf#ecdh_params     |
|       |     .alg_capab.key_type'                               |
+-------+--------------------------------------------------------+
| 82    | cri'http://coreapps.org/core.osc.gconf#ecdh_params     |
|       |     .key_type_capab.key_type'                          |
+-------+--------------------------------------------------------+
| 83    | cri'http://coreapps.org/core.osc.gconf#ecdh_params     |
|       |     .key_type_capab.curve'                             |
+-------+--------------------------------------------------------+
| 84    | cri'http://coreapps.org/core.osc.gconf#det_req'        |
+-------+--------------------------------------------------------+
| 85    | cri'http://coreapps.org/core.osc.gconf#det_hash_alg'   |
+-------+--------------------------------------------------------+
| 86    | cri'http://coreapps.org/core.osc.gconf#rt'             |
+-------+--------------------------------------------------------+
| 87    | cri'http://coreapps.org/core.osc.gconf#active'         |
+-------+--------------------------------------------------------+
| 88    | cri'http://coreapps.org/core.osc.gconf#group_name'     |
+-------+--------------------------------------------------------+
| 89    | cri'http://coreapps.org/core.osc.gconf#group_title'    |
+-------+--------------------------------------------------------+
| 90    | cri'http://coreapps.org/core.osc.gconf                 |
|       |     #ace_groupcomm_profile'                            |
+-------+--------------------------------------------------------+
| 91    | cri'http://coreapps.org/core.osc.gconf#max_stale_sets' |
+-------+--------------------------------------------------------+
| 92    | cri'http://coreapps.org/core.osc.gconf#exp'            |
+-------+--------------------------------------------------------+
| 93    | cri'http://coreapps.org/core.osc.gconf#gid_reuse'      |
+-------+--------------------------------------------------------+
| 94    | cri'http://coreapps.org/core.osc.gconf#app_group'      |
+-------+--------------------------------------------------------+
| 95    | cri'http://coreapps.org/core.osc.gconf#app_group_del'  |
+-------+--------------------------------------------------------+
| 96    | cri'http://coreapps.org/core.osc.gconf#app_group_add'  |
+-------+--------------------------------------------------------+
| 97    | cri'http://coreapps.org/core.osc.gconf#joining_uri'    |
+-------+--------------------------------------------------------+
| 98    | cri'http://coreapps.org/core.osc.gconf#app_groups'     |
+-------+--------------------------------------------------------+
| 99    | cri'http://coreapps.org/core.osc.gconf#group_policies' |
+-------+--------------------------------------------------------+
| 100   | cri'http://coreapps.org/core.osc.gconf#group_policies  |
|       |     .key_update_check_interval'                        |
+-------+--------------------------------------------------------+
| 101   | cri'http://coreapps.org/core.osc.gconf#group_policies  |
|       |     .exp_delta'                                        |
+-------+--------------------------------------------------------+
| 102   | cri'http://coreapps.org/core.osc.gconf#as_uri'         |
+-------+--------------------------------------------------------+
~~~~~~~~~~~
{: #fig-packed-cbor-table-1 title="Shared item table for compressing CoRAL predicates." artwork-align="center"}

## Compression of Values of the rt= Target Attribute

The following shared item table is used for compressing values of the rt= target attribute, as per {{Section 2.2 of I-D.ietf-cbor-packed}}.

~~~~~~~~~~~
+-------+--------------------------------------------------------+
| Index | Item                                                   |
+-------+--------------------------------------------------------+
| 415   | cri'http://www.iana.org/assignments/linkformat/rt      |
|       |     /core.osc.gconf'                                   |
+-------+--------------------------------------------------------+
~~~~~~~~~~~
{: #fig-packed-cbor-table-2 title="Shared item table for compressing values of the rt= target attribute." artwork-align="center"}

# Document Updates # {#sec-document-updates}

RFC EDITOR: PLEASE REMOVE THIS SECTION.

## Version -00 ## {#sec-00}

* CoRAL content taken out from draft-ietf-ace-oscore-gm-admin-08.

# Acknowledgments # {#acknowledgment}
{: numbered="no"}

Most of the content in this document was originally specified in draft-ietf-ace-oscore-gm-admin, which is co-authored also by Peter van der Stok and Francesca Palombini, and where Klaus Hartke contributed in the initial definition of the resource model and interactions using CoRAL.

The authors sincerely thank {{{Christian Amsüss}}}, {{{Carsten Bormann}}} and {{{Jim Schaad}} for their comments and feedback. The work on this document has been partly supported by VINNOVA and the Celtic-Next project CRITISEC; and by the H2020 project SIFIS-Home (Grant agreement 952652).
