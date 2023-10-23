---
title: "X.509 Certificate Extended Key Usage (EKU) for Instant Messaging URIs"
abbrev: "extendedKeyUsage for IM URIs"
category: info

docname: draft-mahy-lamps-im-keyusage-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: SEC
workgroup: LAMPS WG
keyword:
 - x.509
 - certificate
 - extended key usage
 - eku
 - instant messaging
 - im URI
venue:
  group: LAMPS WG
  type: Working Group
  mail: lamps@ietf.org
  github: rohan-wire/mahy-lamps-im-keyusage
  latest: https://example.com/LATEST

author:
 -
    fullname: Rohan Mahy
    organization: Wire
    email: rohan.mahy@wire.com

normative:

informative:


--- abstract

RFC 5280 specifies several extended key purpose identifiers
(KeyPurposeIds) for X.509 certificates.  This document defines
Instant Messaging (IM) identity KeyPurposeIds for inclusion in
the Extended Key Usage (EKU) extension of X.509 v3 public key
certificates


--- middle

# Introduction

Instant Messaging (IM) systems using the Messaging Layer Security (MLS)
{{?RFC9420}} protocol can incorporate per-client identity certificate
credentials. The subjectAltName of these certificates can be an IM URI, for
example. Since IM clients could be very numerous, operators are
reticent to issue certificates for these users that might accidentally be used
to validate a TLS connection because it has the KeyPurposeId `id-kp-serverAuth` or
`id-kp-clientAuth`.

An explanation of MLS credentials as they apply to Instant Messaging is described
in {{?I-D.barnes-mimi-identity-arch}}.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# The IM URI Extended Key Usage

This specification defines the KeyPurposeId id-kp-imUri, which is used
for signing messages to prove the identity of an Instant Messaging client. 

~~~
id-kp  OBJECT IDENTIFIER  ::= {
  iso(1) identified-organization(3) dod(6) internet(1)
  security(5) mechanisms(5) pkix(7) kp(3) }

id-kp-imUri OBJECT IDENTIFIER ::= { id-kp TBD }
~~~

# Security Considerations

The Security Considerations of {{!RFC5280}} are applicable to this
   document.  This extended key purpose does not introduce new security
   risks but instead reduces existing security risks by providing means
   to identify if the certificate is generated to sign IM credentials.

# IANA Considerations

IANA is requested to register the following OIDs in the "SMI Security
for PKIX Extended Key Purpose" registry (1.3.6.1.5.5.7.3).  These
OIDs are defined in Section 4.

   +=========+===============================+============+
   | Decimal | Description                   | References |
   +=========+===============================+============+
   | TBD     | id-kp-imUri                   | This-RFC   |

--- back
