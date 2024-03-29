---
coding: utf-8

title: "A YANG Data Model for Interface Reference Topology"
abbrev: "Interface Reference Topology YANG Model"
category: std
docname: draft-ietf-ccamp-if-ref-topo-yang-latest
ipr: trust200902
submissiontype: IETF
v: 3
area: Routing
workgroup: CCAMP Working Group
keyword: Internet-Draft
venue:
   group: CCAMP
   type: Working Group
   mail: ccamp@ietf.org
   arch: https://datatracker.ietf.org/wg/ccamp/about/
   github: https://github.com/ietf-ccamp-wg/draft-ietf-ccamp-mw-topo-yang
   latest: https://github.com/ietf-ccamp-wg/draft-ietf-ccamp-mw-topo-yang
pi: [toc, sortrefs, symrefs]

author:
 -
   email: jonas.ahlberg@ericsson.com
   fullname: Jonas Ahlberg
   organization: Ericsson AB
   street: Lindholmspiren 11
   city: Goteborg
   code: 417 56
   country: Sweden
   email: jonas.ahlberg@ericsson.com
 -
   fullname: Scott Mansfield
   organization: Ericsson Inc
   email: scott.mansfield@ericsson.com
 -
   fullname: Min Ye
   organization: Huawei Technologies
   street: No.1899, Xiyuan Avenue
   city: Chengdu
   code: 611731
   country: China
   email: amy.yemin@huawei.com
 -
   fullname: Italo Busi
   organization: Huawei Technologies
   email: italo.busi@huawei.com
 -
   fullname: Xi Li
   organization: NEC Laboratories Europe
   street: Kurfursten-Anlage 36
   city: Heidelberg
   code: 69115
   country: Germany
   email: Xi.Li@neclab.eu
 -
   fullname: Daniela Spreafico
   organization: Nokia - IT
   street: Via Energy Park, 14
   city: Vimercate (MI)
   code: 20871
   country: Italy
   email: daniela.spreafico@nokia.com

normative:

informative:

--- abstract
This document defines a YANG data model to provide a reference from a termination point in a topology model to interface management information.

--- middle

# Introduction

This document defines a YANG data model to provide a reference from a termination point in a topology model to interface management information.  It introduces a way to reference the information in a YANG data model for interface management {{!RFC8343}} that could be useful for all types of termination points.  The model augments "YANG Data Model for Traffic Engineering (TE) Topologies" defined in {{!RFC8795}}, which is based on "A YANG Data Model for Network Topologies" defined in {{!RFC8345}}.

The interface reference model is expected to be used between a Provisioning Network Controller (PNC) and a Multi Domain Service Coordinator(MDSC) {{?RFC8453}}.  Different use cases require access to different attributes and in order not to restrict what use cases can be supported, all attributes supported by the interface management model is with this model made accessible from the topology model.

## Terminology and Definitions
The following acronyms are used in this document:

PNC Provisioning Network Controller

MDSC Multi Domain Service Coordinator

## Tree Structure
A simplified graphical representation of the data model is used in chapter 3.1 of this document.  The meaning of the symbols in these diagrams is defined in {{?RFC8340}}.

# Requirements Language
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 {{!RFC2119}} {{!RFC8174}} when, and only when, they appear in all capitals, as shown here.

# Termination Point to Interface Reference YANG Data Model

## YANG Tree
~~~~ yangtree
{::include ./trees/if.tree}
~~~~
{: artwork-name="if.tree"}

## Termination Point to Interface Reference YANG Data Module
~~~~ yang
{::include ./ietf-tp-interface-reference-topology.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-tp-interface-reference-topology.yang"}

# Security Considerations

   The YANG modules specified in this document define schemas for data
   that is designed to be accessed via network management protocols such
   as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.  The lowest NETCONF layer
   is the secure transport layer, and the mandatory-to-implement secure
   transport is Secure Shell (SSH) {{!RFC6242}}.  The lowest RESTCONF layer
   is HTTPS, and the mandatory-to-implement secure transport is TLS
   {{!RFC8446}}.

   The NETCONF access control model {{!RFC8341}} provides the means to
   restrict access for particular NETCONF or RESTCONF users to a
   preconfigured subset of all available NETCONF or RESTCONF protocol
   operations and content.

   The YANG module specified in this document imports and augments the
   ietf-network and ietf-network-topology models defined in {{!RFC8345}}.
   The security considerations from {{!RFC8345}} are applicable to the
   module in this document.

   There is a data node defined in this YANG module that is
   writable/creatable/deletable (i.e., config true, which is the
   default).  This data node may be considered sensitive or vulnerable
   in some network environments.  Write operations (e.g., edit-config)
   to this data node without proper protection can have a negative
   effect on network operations.  This is the subtrees and data node
   and its sensitivity/vulnerability:

   -  tp-to-interface-path: A malicious client could set an arbitrary
      path that could allow a client to retrieve incorrect information.
      Troubleshooting would be difficult because the bad path would not
      be detectable until the client tries to use the leaf to identify
      to radio link terminal.

# IANA Considerations

   IANA is asked to assign a new URI from the "IETF XML Registry" {{!RFC3688}} as follows:

~~~~
URI: urn:ietf:params:xml:ns:yang:ietf-tp-interface-reference-topology
Registrant Contact: The IESG
XML: N/A; the requested URI is an XML namespace.
~~~~

   It is proposed that IANA should record YANG module names in the "YANG
   Module Names" registry {{!RFC6020}} as follows:

~~~~
    Name: ietf-tp-interface-reference-topology
    Maintained by IANA?: N
    Namespace:
      urn:ietf:params:xml:ns:yang:ietf-interface-reference-topology
    Prefix: ifref
    Reference: RFC XXXX
~~~~

--- back

# Examples of the Interface Reference Topology Model {#examples}

   This appendix provides some examples and illustrations of how the
   Interface Reference Topology Model can be used.  There is one
   extended tree to illustrate the Model and a JSON based instantiation
   of the Interface Reference Model for a small network example.

## A tree for a complete Interface Reference Topology Model

   The tree below shows the leafs for extending a Network Topology Model
   defined in {{!RFC8345}}, Traffic Engineering (TE) Topologies model
   defined in {{!RFC8795}} with a possibility to reference interface
   management information.

~~~~ yangtree
{::include ./trees/full-if.tree}
~~~~
{: artwork-name="full-if.tree"}

## A JSON example
~~~~ json
{::include ./json/exampleInterfRef.json}
~~~~
{: artwork-name="exampleInterfRef.json"}
{: sourcecode-markers="false" sourcecode-name="exampleInterfRef.json"}

{: numbered="false"}
# Acknowledgments
   This document was prepared using kramdown

   The authors would like to thank ...
