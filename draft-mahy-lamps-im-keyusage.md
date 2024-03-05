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
 - mimi URL
venue:
  group: LAMPS WG
  type: Working Group
  mail: lamps@ietf.org
  github: rohanmahy/mahy-lamps-im-keyusage
  latest: https://rohanmahy.github.io/mahy-lamps-im-keyusage/draft-mahy-lamps-im-keyusage.html

author:
 -
    fullname: Rohan Mahy
    organization: Unaffiliated
    email: rohan.ietf@gmail.com

normative:
  ITU.X690.2021:
    title: >
      Information Technology — ASN.1 encoding rules:
      Specification of Basic Encoding Rules (BER),
      Canonical Encoding Rules (CER)
      and Distinguished Encoding Rules (DER)
    author:
      org: International Telecommunications Union
    date: 2021
    seriesinfo:
      ITU-T: Recommendation X.690

  ITU.X680.2021:
    title: >
      Information Technology — Abstract Syntax Notation One (ASN.1):
      Specification of basic notation
    author:
      org: International Telecommunications Union
    date: 2021
    seriesinfo:
      ITU-T: Recommendation X.680

informative:


--- abstract

RFC 5280 specifies several extended key purpose identifiers
(KeyPurposeIds) for X.509 certificates.  This document defines
Instant Messaging (IM) identity KeyPurposeId for inclusion in
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
in {{?I-D.barnes-mimi-identity-arch}}. These credentials are expected to be
heavily used in the More Instant Messaging Interoperability (MIMI) Working Group.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# The IM URI Extended Key Usage

This specification defines the KeyPurposeId id-kp-imUri, which is used
for signing messages to prove the identity of an Instant Messaging client.
This Extended Key Usage is optionally critical.

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

| Decimal | Description   | References |
|:--------|:--------------|:-----------|
| TBD1    | id-kp-imUri   | This-RFC   |

IANA is also requested to register the following ASN.1 {{ITU.X690.2021}}
module OID in the "SMI Security for PKIX Module Identifier" registry (1.3.6.1.5.5.7.0). This OID is defined in {{asn1-module}}.

| Decimal | Description   | References |
|:--------|:--------------|:-----------|
| TBD2    | id-kp-im-eku  | This-RFC   |

--- back

# ASN.1 Module {#asn1-module}

The following module adheres to ASN.1 specifications {{ITU.X680.2021}} and
{{ITU.X690.2021}}.

~~~ asn1
<CODE BEGINS>

NF-EKU
  { iso(1) identified-organization(3) dod(6) internet(1)
  security(5) mechanisms(5) pkix(7) id-mod(0)
  id-mod-im-eku (TBD2) }

DEFINITIONS IMPLICIT TAGS ::=
BEGIN

-- OID Arc

id-kp OBJECT IDENTIFIER ::=
  { iso(1) identified-organization(3) dod(6) internet(1)
    security(5) mechanisms(5) pkix(7) kp(3) }

-- Extended Key Usage Values

id-kp-imUri OBJECT IDENTIFIER ::= { id-kp TBD1 }

END


<CODE ENDS>
~~~

# Change log

* added ASN.1 module
* specified that eku is optionally critical
