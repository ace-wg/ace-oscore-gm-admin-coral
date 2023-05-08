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

## Terminology ## {#terminology}

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 {{RFC2119}} {{RFC8174}} when, and only when, they appear in all capitals, as shown here.

Readers are expected to be familiar with the terms and concepts from the following specifications:

* TBD

# TBD

TBD

## TBD

# IANA Considerations # {#iana}

This document has no actions for IANA.

--- back

# Shared item tables for Packed CBOR # {#sec-packed-cbor-tables}

This appendix defines the two shared item tables that the CoRAL examples refer to for using Packed CBOR {{I-D.ietf-cbor-packed}}.

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

# Acknowledgments # {#acknowledgment}
{: numbered="no"}

This specification builds on draft-ietf-ace-oscore-gm-admin co-authored also by Peter van der Stok and Francesca Palombini, where Klaus Hartke contributed in defining the resource model and the interactions using CoRAL originally part of that document.

The authors sincerely thank {{{Christian Amsüss}}}, {{{Carsten Bormann}}} and {{{Jim Schaad}} for their comments and feedback. The work on this document has been partly supported by VINNOVA and the Celtic-Next project CRITISEC; and by the H2020 project SIFIS-Home (Grant agreement 952652).
