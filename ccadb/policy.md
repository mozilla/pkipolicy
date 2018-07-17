# Common CCADB Policy #

*Version 1.0.4*

Several Web PKI root store operators (“Stores”) have collaborated to create
the Common Certificate Authority Database (CCADB), a data repository of
certificate and Certificate Authority (CA) information. CAs who wish to be
included in participating stores will need to maintain certain information in
the CCADB. This document explains what is required of CAs who are required by
Store policy to use the CCADB.

Stores may have their own additional CCADB-related requirements. For each root
certificate, CAs must comply with the additional requirements pertaining to the
Stores which contain that certificate.

This document does not cover how to obtain write access to the CCADB or how to
use the CCADB’s web interface. Those topics are outside its scope. CAs should
contact an appropriate Store for assistance.

## 1. General Provisions ##

Regardless of more specific provisions in these requirements, CAs have an
overarching responsibility to keep the information in the CCADB about
themselves, their operations and their certificates accurate, and make updates
in a timely fashion.

All data in the CCADB may be made public or semi-public in a variety of forms;
CAs should not place any information in the CCADB which they wish to keep
confidential. However, Stores are not obliged to publish any CCADB information.

All client devices that are used to download Personally Identifiable Information 
from the CCADB must employ disk based encryption.

## 2. Contact Information ##

CAs are required to provide the following information for a Primary Point of
Contact (POC), and at least one other POC, who may or may not be Primary:

* Name
* Office email address
* Office hours phone number

CAs may optionally designate further POCs, supplying at least one contact
method for each. CAs must also supply one or two non-personal contact email
aliases which are more likely to continue working as personnel change; these
are maintained as part of the CA’s organizational entry.

All Primary POCs should be authorized to speak for and to bind the CA that they
represent. At least one of the Primary POCs will hold a CA Community license;
other POCs may also apply to a Store to be issued one. Those Primary POCs with
a CA Community license are ultimately responsible for keeping CCADB data
up-to-date for their CA.

Notification of security and audit-related issues will be emailed to all
Primary POCs and the first email alias. CAs are advised to make sure those
addresses reach sufficient people such that they can respond to an issue
in an appropriate timeframe.

If POC or email alias information needs to be updated, the CA should notify one
of the Stores containing their root certificates, because this information may
only be edited by Stores. See the Store policy documents for Store contact
information.

## 3. Root Certificates ##

A root certificate is a certificate which is capable of issuing new
certificates, which a CA designates as a trust anchor. It will usually be
self-signed. CAs are required to maintain correct and current information about
their root certificates.

If root certificate information needs to be updated, the CA should notify one of 
the Stores containing the certificate, because this information may only be edited 
by Stores. See the Store policy documents for Store contact information.

To update audit information for a root certificate, create an [Audit Case][CCADB-Audit-Case].

## 4. Intermediate Certificates ##

An intermediate certificate is a certificate capable of issuing new
certificates that is not a root certificate. To determine which intermediate 
certificates must be entered into the CCADB, refer to the individual Store policy 
documents. This includes certificates that are revoked. For
newly-created intermediate certificates, this must happen before the
certificate begins issuing publicly-trusted certificates.

Each instance (i.e. PEM data) of an intermediate certificate only needs to be 
included in the CCADB once, even if it chains up to two root certificates.

If an intermediate certificate is revoked, the CCADB must be updated to mark it 
as revoked, giving the reason why, within 24 hours for a security incident, and 
within 7 days for any other reason.

## 5. Policies, Practices and Audit Information ##

In the records for both root certificates and intermediate certificates, CAs
are required to provide details of the Certificate Policy (CP) and/or
Certificate Practice Statement (CPS) documents relating to that certificate,
and also statements of attestation of their conformance to various requirements
and other operational criteria (“audits”), those statements being made by a
competent independent party or parties. These documents are hosted elsewhere
and the URLs are stored in the CCADB. The URLs to such CPs, CPSes and audits,
and any metadata about them such as the name of the auditor or the date of the
audit, need to be updated as new information become available. For technical
reasons, URLs to audit statements need to point to a PDF file.

The entry for each intermediate certificate has "Audits Same as Parent" and
"CP/CPS Same as Parent" checkboxes. When those are checked, the details do not
need to be duplicated from the parent cert. However, the intermediate
certificate must be specifically listed in the audit statements of the parent
certificate.

URLs for the following documents are required for each certificate:

* Certificate Policy (CP)
* Certificate Practice Statement (CPS)
* Standard audit (WebTrust or ETSI)
* Baseline Requirements (BR) audit (if the certificate is capable of issuing
  TLS/SSL server certificates)
* Extended Validation (EV) SSL and/or Code Signing audit (if applicable)

CAs must provide English versions of any Certificate Policy, Certification
Practice Statement and Audit documents which are not originally in English,
with version numbers matching the document they are a translation of. The
English version is not required to be authoritative in all cases of dispute,
but the CA must attest that the translation is not materially different to the
original.

## 6. Mailshots ##

From time to time, a Store may use the CCADB to send information to CAs.
Mailshots will be sent to at least the Primary POC and the email aliases, and
may also go to one or more of the other POCs; the exact recipient list is
defined by the Store sending the information.

-----

Any copyright in this document is
[dedicated to the Public
Domain](http://creativecommons.org/publicdomain/zero/1.0/).

[CCADB-Audit-Case]:    https://ccadb.org/cas/updates
