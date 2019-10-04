# Mozilla Root Store Policy #

*Version 2.7*

*[Effective <TBD>][Policy-Archive]*

## 1. Introduction ##

When distributing binary and source code versions of Firefox, Thunderbird, and
other Mozilla-related software products, Mozilla includes with such software
a set of X.509v3 root certificates for various Certification
Authorities (CAs). The included certificates have their "trust bits"
set for various purposes, so that the software in question can use the CA
certificates to anchor a chain of trust for certificates used by SSL servers
and S/MIME email users without having to ask users for further permission or
information.

This policy covers how the default set of certificates and associated trust
bits is maintained for software products distributed by Mozilla. Other entities
distributing software based on ours are free to adopt their own policies. In
particular, under the terms of the relevant Mozilla license(s) distributors of
such software are permitted to add or delete CA certificates and modify the
values of the trust bits in the versions that they distribute. However,
as with other software modifications, by making such changes a distributor MAY
well affect its ability to use Mozilla trademarks in connection with its
versions of the software. See the Mozilla trademark policy for more
information.

### 1.1 Scope ###

This policy applies, as appropriate, to certificates matching any of the
following (and the CAs which control or issue them):

1.  CA certificates included in, or under consideration for inclusion in, the
    Mozilla root program.

2.  Intermediate certificates which have at least one valid, unrevoked chain up
    to such a CA certificate and which are technically capable of issuing 
    working server or email certificates. Intermediate certificates that are not 
    considered to be technically capable will contain either:

    * an Extended Key Usage (EKU) extension which does not contain any of
      these KeyPurposeIds: anyExtendedKeyUsage, id-kp-serverAuth,
      id-kp-emailProtection; and/or:
    * name constraints which do not allow Subject Alternative Names (SANs) of
      any of the following types: dNSName, iPAddress, SRVName, rfc822Name

3.  End-entity certificates which have at least one valid, unrevoked chain up
    to such a CA certificate through intermediate certificates which are all in
    scope, such end-entity certificates having either:

    * an Extended Key Usage (EKU) extension which contains one or more of these
      KeyPurposeIds: anyExtendedKeyUsage, id-kp-serverAuth,
      id-kp-emailProtection; or:
    * no EKU extension.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in RFC 2119.

### 1.2 Policy Ownership ###

Mozilla has appointed a [CA Certificate module owner][CA-Cert-Module]
and peers to evaluate new CA requests on our behalf and make decisions
regarding all matters relating to CA certificates included in our root program.

Further, Mozilla has appointed a [Mozilla CA Certificate Policy module
owner][CA-Policy-Module] and peers to maintain this policy. The policy will
only be changed after public consultation with the Mozilla community, in order
to ensure that all views are taken into account. You can contact the Mozilla CA
Certificate Policy module team at [certificates@mozilla.org][Email-Us] if you
have questions about this policy.

CAs or others objecting to a particular decision by either team MAY appeal to
the [Firefox Technical Leadership Module Committee][Gov-Module] who will make a final
decision.

## 2. Certificate Authorities ##

### 2.1 CA Operations ###

CAs whose certificates are included in Mozilla's root program MUST:

1.  provide some service relevant to users of our software
    products;
2.  follow industry best practice for securing their networks, for example
    by conforming to the [CAB Forum Network Security Guidelines][NSGs] or a
    successor document;
3.  enforce multi-factor authentication for all accounts capable of causing
    certificate issuance or performing Registration Authority or Delegated
    Third Party functions, or implement technical controls operated by the CA
    to restrict certificate issuance through the account to a limited set of
    pre-approved domains or email addresses;
4.  prior to issuing certificates, verify certificate
    requests in a manner that we deem acceptable for the stated
    purpose(s) of the certificates;
5.  verify that all of the information that is included in SSL
    certificates remains current and correct at time intervals of
    825 days or less; and
6.  otherwise operate in accordance with published criteria that we
    deem acceptable.

CAs MUST follow and be aware of discussions in the
[mozilla.dev.security.policy][MDSP] forum, where Mozilla's root program is
coordinated. They are encouraged, but not required, to contribute to those
discussions.

### 2.2 Validation Practices ###

We consider verification of certificate signing requests to be acceptable if it
meets or exceeds the following requirements:

1.  All information that is supplied by the certificate subscriber
    MUST be verified by using an independent source of information
    or an alternative communication channel before it is included in
    the certificate.
2.  For a certificate capable of being used for digitally signing or encrypting
    email messages, the CA takes reasonable measures to verify that
    the entity submitting the request controls the email account
    associated with the email address referenced in the certificate
    *or* has been authorized by the email account holder to act on
    the account holder’s behalf. The CA's CP/CPS must clearly specify the 
    procedure(s) that the CA employs to perform this verification.
3.  For a certificate capable of being used for SSL-enabled servers, the CA
    must ensure that the applicant has registered all domain(s) referenced
    in the certificate or has been authorized by the domain registrant to
    act on their behalf. This must be done using one or more of the
    methods documented in section 3.2.2.4 of the CA/Browser Forum Baseline Requirements. The CA's
    CP/CPS must clearly specify the procedure(s) that the CA employs, and
    each documented procedure should state which subsection of 3.2.2.4 it is
    complying with. CAs are not permitted to use 3.2.2.5 (4) ("any other method") 
    to fulfill the requirements of method 3.2.2.4.8 (IP Address).
4.  For a certificate capable of being used for SSL-enabled servers, the CA
    must ensure that the applicant has control over all IP Address(es) referenced
    in the certificate. This must be done using one or more of the
    methods documented in section 3.2.2.5 of the CA/Browser Forum Baseline Requirements. The CA's
    CP/CPS must clearly specify the procedure(s) that the CA employs, and
    each documented procedure should state which subsection of 3.2.2.5 it is
    complying with.
5.  For certificates marked as Extended Validation, the CA MUST comply with the
    latest version of the [Guidelines for the Issuance and Management of
    Extended Validation Certificates][EVGLs].

Validation methods are occasionally found to contain security flaws. When this happens, 
Mozilla expects CAs to evaluate their practices and respond appropriately to mitigate the risk. 
Mozilla may require CAs to make disclosures or modifications, up to and including 
immediately discontinuing use of a method.

### 2.3 Baseline Requirements Conformance ###

CA operations relating to issuance of certificates capable of being used for
SSL-enabled servers MUST also conform to the latest version of the [CA/Browser
Forum Baseline Requirements for the Issuance and Management of Publicly-Trusted
Certificates][BRs] ("Baseline Requirements"). In the event of inconsistency
between Mozilla’s Root Store Policy requirements and the Baseline Requirements,
Mozilla’s Root Store Policy takes precedence. The following is a list of known
places where this policy takes precedence over the Baseline Requirements. If
you find an inconsistency that is not listed here, notify Mozilla so the item
can be considered for addition or clarification.

*   Insofar as the Baseline Requirements attempt to define their own scope, the
    scope of this policy (section 1.1) overrides that. Mozilla thus requires CA
    operations relating to issuance of **all** SSL certificates in the scope of
    this policy to conform to the Baseline Requirements.

*   Mozilla reserves the right to accept audits by auditors who do not meet the
    qualifications given in section 8.2 of the Baseline Requirements, or refuse
    audits from auditors who do.
    
*   Mozilla may restrict permitted algorithms to a subset of those allowed by the 
    Baseline Requirements.

### 2.4 Incidents ###

When a CA fails to comply with any requirement of this policy - whether it be a misissuance, a procedural or operational issue, or any other variety of non-compliance - the event is classified as an incident. At a minimum, CAs MUST promptly report all incidents to Mozilla in the form of an [Incident Report][Incident-Report], and MUST regularly update the Incident Report until the corresponding bug is resolved by a Mozilla representative. CAs SHOULD cease issuance until the problem has been prevented from reoccurring.

## 3. Documentation ##

### 3.1 Audits ###

Before being included and periodically thereafter, CAs MUST obtain certain
audits for their root certificates and all of their intermediate certificates
that are technically capable of issuing working server or email certificates. 
This section describes the requirements for those audits.

#### 3.1.1 Audit Criteria ####

We consider the criteria for CA operations published in the
following documents to be acceptable:

*   WebTrust "[Principles and Criteria for Certification Authorities - Version
    2.0][WebTrust-2.0]" or later in [WebTrust Program for Certification
    Authorities][WebTrust-For-CAs];
*   WebTrust "[Principles and Criteria for Certification Authorities – SSL
    Baseline with Network Security - Version 2.2][WebTrust-BRs]" or later in
    [WebTrust Program for Certification Authorities][WebTrust-For-CAs];
*   WebTrust "[Principles and Criteria for Certification Authorities -
    Extended Validation SSL 1.6.0][WebTrust-EV]" or later in
    [WebTrust Program for Certification Authorities][WebTrust-For-CAs];
*   “Trust Service Providers practice” in ETSI EN 319 411-1 v1.1.1 or
    later version [Policy and security requirements for Trust Service Providers
    issuing certificates; Part 1: General requirements][ETSI-319-411-1],
    specifying a policy or policies appropriate to the trust bit(s) being
    applied for;
*   “Trust Service Providers practice” in ETSI EN 319 411-2 v2.1.1 or
    later version [Policy and security requirements for Trust Service Providers
    issuing certificates; Part 2: Requirements for trust service providers
    issuing EU qualified certificates][ETSI-319-411-2], specifying a
    policy or policies appropriate to the trust bit(s) being applied for.

#### 3.1.2 Required Audits ####

##### 3.1.2.1 WebTrust #####

If being audited to the WebTrust criteria, the following audit requirements
apply (see section 3.1.1 for specific version numbers):

*   For the SSL trust bit, a CA and all subordinate CAs technically capable
    of issuing server certificates must have all of the following audits:

    * [WebTrust for CAs][WebTrust-2.0]
    * [WebTrust for CAs - SSL Baseline with Network Security][WebTrust-BRs]
    * [WebTrust for CAs - EV SSL][WebTrust-EV] (if issuing EV certificates)

*   For the email trust bit, a CA and all subordinate CAs technically capable
    of issuing email certificates must have all of the following audits:

    * [WebTrust for CAs][WebTrust-2.0]

##### 3.1.2.2 ETSI #####

If being audited to the ETSI criteria, the following audit requirements apply
(see section 3.1.1 for version numbers):

*   For the SSL trust bit, a CA and all subordinate CAs technically
    capable of issuing server certificates must have one of the
    following audits, with at least one of the noted policies or sets of
    policies:

    * [ETSI EN 319 411-1][ETSI-319-411-1] (LCP and (DVCP or OVCP)) and/or (NCP
      and EVCP)
    * [ETSI EN 319 411-2][ETSI-319-411-2] (QCP-w)

    An audit showing conformance with the EVCP policy is required if issuing EV
    certificates.

*   For the email trust bit, a CA and all subordinate CAs technically
    capable of issuing email certificates must have one of the
    following audits, with at least one of the noted policies:

    * [ETSI EN 319 411-1][ETSI-319-411-1] (LCP, NCP, or NCP+)
    * [ETSI EN 319 411-2][ETSI-319-411-2] (QCP-l, QCP-l-qscd, QCP-n, or
      QCP-n-qscd)

#### 3.1.3 Audit Parameters ####

Full-surveillance period-of-time audits MUST be conducted and updated audit
information provided no less frequently than **annually**. Successive audits
MUST be contiguous (no gaps).

Point-in-time audit statements may be used to confirm that all of the problems
that an auditor previously identified in a qualified audit statement have been
corrected. However, a point-in-time audit does not replace the
period-of-time audit.

Audit reports which are being supplied to maintain a certificate within the
Mozilla root program MUST be provided to Mozilla via the CCADB within three
months of the point-in-time date or the end date of the period.

#### 3.1.4 Public Audit Information ####

The publicly-available documentation relating to each audit MUST contain at
least the following clearly-labelled information:

1.  name of the company being audited;
2.  name and address of the organization performing the audit;
3.  Distinguished Name and SHA256 fingerprint of each root and intermediate
    certificate that was in scope;
4.  audit criteria (with version number) that were used to audit each of
    the certificates;
5.  a list of the CA policy documents (with version numbers) referenced during
    the audit;
6.  whether the audit is for a period of time or a point in time;
7.  the start date and end date of the period, for those that cover a period
    of time;
8.  the point-in-time date, for those that are for a point in time;
9.  the date the report was issued (which will necessarily be after the end
    date or point-in-time date); and
10. For ETSI, a statement to indicate if the audit was a full audit, and which
    parts of the criteria were applied, e.g. DVCP, OVCP, NCP, NCP+, LCP, EVCP,
    EVCP+, QCP-w, Part1 (General Requirements), and/or Part 2 (Requirements for
    trust service providers).

An authoritative English language version of the publicly-available audit information MUST be supplied by the Auditor.

### 3.2 Auditors ###

In normal circumstances, Mozilla requires that audits MUST be performed
by a Qualified Auditor, as defined in the Baseline Requirements section 8.2.

If a CA wishes to use auditors who do not fit that definition, they MUST
receive written permission from Mozilla to do so in advance of the start
of the audit engagement. Mozilla will make its own determination as to
the suitability of the suggested party or parties, at its sole discretion.

### 3.3 CPs and CPSes ###

We rely on publicly disclosed documentation (e.g., in a Certificate Policy and
Certification Practice Statement) to ascertain that our requirements are met.
Therefore, the following MUST be true:

1.  the publicly disclosed documentation provides sufficient
    information for Mozilla to determine whether and how the CA
    complies with this policy, including a description of the steps
    taken by the CA to verify certificate requests;

2.  the documentation is available from the CA’s official website;

3.  CPs and CPSes are made available to Mozilla under one
    of the following Creative Commons licenses (or later versions):

       * Attribution ([CC-BY]) 4.0
       * Attribution-ShareAlike ([CC-BY-SA]) 4.0
       * Attribution-NoDerivs ([CC-BY-ND]) 4.0
       * Public Domain Dedication ([CC-0]) 1.0

    or a set of equally permissive licensing terms accepted by Mozilla in
    writing. If no such license is indicated, the fact of application is
    considered as permission from the CA to allow Mozilla and the public to
    deal with these documents, and any later versions for root certificates
    which are included in Mozilla's trust store, under CC-BY-ND 4.0.

4.  CPs and CPSes MUST be reviewed and updated as necessary at least once every
year, as required by the Baseline Requirements. CAs MUST indicate that this has
happened by incrementing the version number and adding a dated changelog entry,
even if no other changes are made to the document.

5.  Effective for versions dated after 30-September, 2019, CPs and CPSes MUST be 
structured according to RFC 3647 and MUST:
*   Include at least every section and subsection defined in RFC 3647; and,
*   Only use the words "No Stipulation" to mean that the particular document 
imposes no requirements related to that section; and,
*   Contain no sections that are blank and have no subsections.

6.  CAs must provide a way to clearly determine which CP and CPS 
applies to each of its root and intermediate certificates.
    
## 4. Common CA Database ##

Mozilla manages its root program using the Common CA Database (CCADB). CAs with
certificates in Mozilla’s root program MUST use the CCADB, and are bound by the
latest published version of the [Common CCADB Policy][CCADB-Policy], which is
incorporated here by reference.

When required by the CCADB Policy, Mozilla’s root program may be contacted
[by email][Email-Us].

Mozilla has requirements for the use of the CCADB above and beyond those in the
CCADB Policy, as follows:

### 4.1 Additional Requirements ###

* If the revocation of an intermediate certificate chaining up to a root in
Mozilla’s root program is due to a security concern, as well as performing the
actions defined in the CCADB Policy, a [security bug must be filed in
Bugzilla][Sec-Bugs].

### 4.2 Surveys ###

Mozilla may conduct a survey of CAs from time to time using the CCADB. CAs are
required to respond to the surveys with accurate information, within the
timescale defined in the survey.

## 5. Certificates ##

### 5.1 Algorithms ###

Root certificates in our root program, and any certificate which
chains up to them, MUST use only algorithms and key sizes from the following
set:

*   RSA keys whose modulus size in bits is divisible by 8, and is at
    least 2048.
*   ECDSA keys using one of the following curves:
    * P-256
    * P-384

The following sections detail encoding and signature algorithm requirements for
each of these keys. The encoding requirements on signature algorithms apply to
any contexts where the algorithm is encoded as an AlgorithmIdentifier,
including:

* The signatureAlgorithm field of a Certificate
* The signature field of a TBSCertificate
* The signatureAlgorithm field of a CertificateList
* The signature field of a TBSCertList
* The signatureAlgorithm field of a BasicOCSPResponse


#### 5.1.1 RSA

When RSA keys are encoded in a SubjectPublicKeyInfo structure, the algorithm
field MUST consist of an rsaEncryption OID (1.2.840.113549.1.1.1) with a NULL
parameter, as specified by [RFC 8017, Appendix A.1](https://tools.ietf.org/html/rfc8017#appendix-A.1)
and [RFC 3279, Section 2.3.1](https://tools.ietf.org/html/rfc3279#section-2.3.1).
The encoded AlgorithmIdentifier for an RSA key MUST match the
following hex-encoded bytes:
`300d06092a864886f70d0101010500`.

CAs MUST NOT use the id-RSASSA-PSS OID (1.2.840.113549.1.1.10) within a
SubjectPublicKeyInfo to represent a RSA key.

When a root or intermediate certificate's RSA key is used to produce a
signature, only the following algorithms may be used, and with the following
encoding requirements:

* RSASSA-PKCS1-v1_5 with SHA-1.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:
  `300d06092a864886f70d0101050500`.

  See section 5.1.3 for further restrictions on the use of SHA-1.

* RSASSA-PKCS1-v1_5 with SHA-256.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:
  `300d06092a864886f70d01010b0500`.

* RSASSA-PKCS1-v1_5 with SHA-384.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:
  `300d06092a864886f70d01010c0500`.

* RSASSA-PKCS1-v1_5 with SHA-512.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:
  `300d06092a864886f70d01010d0500`.

* RSASSA-PSS with SHA-256, MGF-1 with SHA-256, and a salt length of 32 bytes.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:

  ```
  304106092a864886f70d01010a3034a00f300d0609608648016503040201
  0500a11c301a06092a864886f70d010108300d0609608648016503040201
  0500a203020120
  ```

* RSASSA-PSS with SHA-384, MGF-1 with SHA-384, and a salt length of 48 bytes.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:

  ```
  304106092a864886f70d01010a3034a00f300d0609608648016503040202
  0500a11c301a06092a864886f70d010108300d0609608648016503040202
  0500a203020130
  ```

* RSASSA-PSS with SHA-512, MGF-1 with SHA-512, and a salt length of 64 bytes.

  The encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:

  ```
  304106092a864886f70d01010a3034a00f300d0609608648016503040203
  0500a11c301a06092a864886f70d010108300d0609608648016503040203
  0500a203020140
  ```

The above RSASSA-PKCS1-v1_5 encodings consist of the corresponding OID,
e.g. sha256WithRSAEncryption (1.2.840.113549.1.1.11), with an explicit NULL
parameter, as specified in [RFC 3279, Section 2.2.1](https://tools.ietf.org/html/rfc3279#section-2.2.1).
Certificates MUST NOT omit this NULL parameter. Note this differs
from ECDSA, which omits the parameter.

The above RSASSA-PSS encodings consist of the RSASSA-PSS OID
(1.2.840.11.3549.1.1.10) with a corresponding RSASSA-PSS-params structure as
parameter. The trailerField MUST be omitted, as it is unchanged from the default
value. The AlgorithmIdentifier structures describing the hash functions in the
hashAlgorithm field and in the maskGenAlgorithm's parameter MUST themselves
include an explicit NULL in the parameter field, as specified by [RFC 4055, Section 6](https://tools.ietf.org/html/rfc4055#section-6)

#### 5.1.2 ECDSA

When ECDSA keys are encoded in a SubjectPublicKeyInfo structure, the algorithm
field MUST be one of the following, as specified by [RFC 5480, Section 2.1.1](https://tools.ietf.org/html/rfc5480#section-2.1.1):

* The encoded AlgorithmIdentifier for a P-256 key MUST match the following
  hex-encoded bytes: `301306072a8648ce3d020106082a8648ce3d030107`.

* The encoded AlgorithmIdentifier for a P-384 key MUST match the following
  hex-encoded bytes: `301006072a8648ce3d020106052b81040022`.

The above encodings consist of an ecPublicKey OID (1.2.840.10045.2.1) with a
named curve parameter of the curreponding curve OID. Certificates MUST NOT use
the implicit or specified curve forms.

When a root or intermediate certificate's ECDSA key is used to produce a
signature, only the following algorithms may be used, and with the following
encoding requirements:

* If the signing key is P-256, the signature MUST use ECDSA with SHA-256. The
  encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:
  `300a06082a8648ce3d040302`.

* If the signing key is P-384, the signature MUST use ECDSA with SHA-384. The
  encoded AlgorithmIdentifier MUST match the following hex-encoded bytes:
  `300a06082a8648ce3d040303`.

The above encodings consist of the corresponding OID with the parameters field
omitted, as specified by [RFC 5758, Section 3.2](https://tools.ietf.org/html/rfc5758#section-3.2).
Certificates MUST NOT include a NULL parameter. Note this differs from
RSASSA-PKCS1-v1_5, which includes an explicit NULL.

#### 5.1.3 SHA-1 ####

CAs MAY sign SHA-1 hashes over end-entity certificates which chain
up to roots in Mozilla's program only if all the following are true:

1. The end-entity certificate:

   *   is not within the scope of the Baseline Requirements;
   *   contains an EKU extension which does not contain either of the
     id-kp-serverAuth or anyExtendedKeyUsage key purposes;
   *   has at least 64 bits of entropy from a CSPRNG in the serial number.

2. The issuing certificate:

   *   contains an EKU extension which does not contain either of the
     id-kp-serverAuth or anyExtendedKeyUsage key purposes;
   *   has a pathlen:0 constraint.

Point 2 does not apply if the certificate is an OCSP signing certificate
manually issued directly from a root.

CAs MAY sign SHA-1 hashes over intermediate certificates which
chain up to roots in Mozilla's program only if the certificate to be signed
is a duplicate of an existing SHA-1 intermediate certificate with the
only changes being all of:

*   a new key (of the same size);
*   a new serial number (of the same length);
*   the addition of an EKU and/or a pathlen constraint to meet the
    requirements outlined above.

CAs MAY sign SHA-1 hashes over OCSP responses only if the signing
certificate contains an EKU extension which contains only the
id-kp-ocspSigning EKU.

CAs MAY sign SHA-1 hashes over CRLs for roots and intermediates
only if they have issued SHA-1 certificates.

CAs MUST NOT sign SHA-1 hashes over other data, including CT pre-certificates.

### 5.2 Forbidden and Required Practices ###

CA operations MUST at all times be in accordance with the applicable CP
and CPS.

CAs MUST maintain a certificate hierarchy such that the included
certificate does not directly issue end-entity certificates to
customers (i.e. the included certificate signs intermediate
issuing certificates), as described in section 6.1.7 of the
[Baseline Requirements][BRs].

CAs MUST maintain current best practices to prevent
algorithm attacks against certificates. As such, all new certificates
MUST have a serial number greater than zero, containing at least 64 bits of
output from a CSPRNG.

CAs MUST NOT issue certificates that have:

*   ASN.1 DER encoding errors;
*   invalid public keys (e.g., RSA certificates with public exponent
    equal to 1);
*   duplicate issuer names and serial numbers (except that a Certificate
    Transparency pre-certificate is allowed to match the corresponding
    certificate);
*   incorrect extensions (e.g., SSL certificates that exclude SSL
    usage, or authority key IDs that include both the key ID and the
    issuer’s issuer name and serial number); *or*
*   cRLDistributionPoints or OCSP authorityInfoAccess extensions for
    which no operational CRL or OCSP service exists.
    
CAs MUST NOT generate the key pairs for end-entity certificates that have an
EKU extension containing the KeyPurposeIds id-kp-serverAuth or anyExtendedKeyUsage.

Effective for certificates with a notBefore date of April 1, 2020 or later, 
end-entity certificates MUST include an EKU extension containing KeyPurposeId(s) 
describing the intended usage(s) of the certificate, and the EKU extension MUST NOT 
contain the KeyPurposeId anyExtendedKeyUsage.

### 5.3 Intermediate Certificates ###

All certificates that are capable of being used to issue new certificates, and
which directly or transitively chain to a certificate included in Mozilla’s CA
Certificate Program, MUST be operated in accordance with this policy and MUST
either be technically constrained or be publicly disclosed and audited.

A certificate is deemed as capable of being used to issue new
certificates if it contains an [X.509v3 basicConstraints extension][5280-6.1.4]
with the cA boolean set to true. The term "subordinate CA" in this section
refers to any organization or legal entity that is in possession
or control of a certificate that is capable of being used to
issue new certificates.

These requirements include all cross-certificates which chain to a certificate 
that is included in Mozilla’s CA Certificate Program.

Intermediate certificates created after January 1, 2019, with the exception of cross-certificates that share a private key with a corresponding root certificate:

*   MUST contain an EKU extension; and,
*   MUST NOT include the anyExtendedKeyUsage KeyPurposeId; and,
*   MUST NOT include both the id-kp-serverAuth and id-kp-emailProtection KeyPurposeIds in the same certificate.

#### 5.3.1 Technically Constrained ####

We encourage CAs to technically constrain all intermediate
certificates. For a certificate to be considered technically
constrained, the certificate MUST include an [Extended Key Usage
(EKU)][5280-4.2.1.12] extension specifying all extended key usages that the
subordinate CA is authorized to issue certificates for. The anyExtendedKeyUsage
KeyPurposeId MUST NOT appear within this extension.

If the certificate includes the id-kp-serverAuth extended key usage,
then to be considered technically
constrained, the certificate MUST be Name Constrained as described in section
7.1.5 of version 1.3 or later of the [Baseline Requirements][BRs]. 
The conformance requirements defined in section 2.3 of this policy also apply to 
technically constrained intermediate certificates.

If the certificate includes the id-kp-emailProtection extended key
usage, then to be considered technically
constrained, it MUST include the Name Constraints X.509v3 extension with
constraints on rfc822Name, with at least one name in permittedSubtrees,
each such name having its ownership validated according to section
3.2.2.4 of the [Baseline Requirements][BRs].

#### 5.3.2 Publicly Disclosed and Audited ####

We recognize that technically constraining intermediate
certificates as described above may not be practical in some cases.
All certificates that are capable of being used to issue new
certificates, that are not technically constrained, and that
directly or transitively chain to a certificate included in
Mozilla’s root program:

* MUST be audited in accordance with Mozilla’s Root Store Policy. 
If the CA has a currently valid audit report at the time of creation 
of the certificate, then the new certificate MUST appear on the 
CA's next periodic audit reports.
* MUST be publicly disclosed in the CCADB by the CA that has their certificate
included in Mozilla’s root program. The CA with a certificate included in Mozilla’s 
root program MUST disclose this information within a week of certificate creation, 
and before any such subordinate CA is allowed
to issue certificates. All disclosure MUST be made freely available
and without additional requirements, including, but not limited to,
registration, legal agreements, or restrictions on redistribution of
the certificates in whole or in part.

## 6. Revocation ##

CAs MUST maintain an online 24x7 repository mechanism whereby
application software can automatically check online the current
status of all unexpired certificates issued by the CA.

For end-entity certificates, CRLs MUST be updated and reissued at least
every seven days, and the value of the nextUpdate field MUST NOT be
more than ten days beyond the value of the thisUpdate field.

For end-entity certificates, if the CA provides revocation information
via an Online Certificate Status Protocol (OCSP) service:

*   it MUST update that service at least every four days; and
*   responses MUST have a defined value in the nextUpdate field, and it
    MUST be no more than ten days after the thisUpdate field; and
*   the value in the nextUpdate field MUST be before or equal to the
    notAfter date of all certificates included within the
    BasicOCSPResponse.certs field or, if the certs field is omitted,
    before or equal to the notAfter date of the CA certificate which
    issued the certificate that the BasicOCSPResponse is for.

### 6.1 SSL ###

For any certificate in a hierarchy capable of being used for 
SSL-enabled servers, CAs MUST revoke certificates that they have 
issued upon the occurrence of any event listed in the appropriate 
subsection of section 4.9.1 of the Baseline Requirements, 
according to the timeline defined therein.

### 6.2 S/MIME ###

For any certificate in a hierarchy capable of being used for 
S/MIME, CAs MUST revoke certificates in accordance with the 
requirements in the following subsections:

#### 6.2.1 Reasons for Revoking a Subscriber Certificate ####

The CA SHALL revoke a Certificate within 24 hours if one or more 
of the following occurs: 

1. The Subscriber requests in writing that the CA revoke the Certificate;
2. The Subscriber notifies the CA that the original certificate request 
was not authorized and does not retroactively grant authorization;
3. The CA obtains evidence that the Subscriber's private key corresponding 
to the public key in the certificate suffered a key compromise; or
4. The CA obtains evidence that the validation of email address or 
domain authorization or control for any email address or domain name 
in the certificate should not be relied upon.

The CA SHOULD revoke a certificate within 24 hours and MUST revoke 
a certificate within 5 days if one or more of the following occurs:

1. The CA obtains evidence that the Certificate was misused;
2. The CA is made aware that a Subscriber has violated one or more of 
its material obligations under the subscriber agreement or terms of use;
3. The CA is made aware of any circumstance indicating that use of an 
email address or domain name in the certificate is no longer legally permitted 
(e.g. a court or arbitrator has revoked a domain name registrant's 
right to use the domain name, a relevant licensing or services agreement 
between the domain name registrant and the applicant has terminated, 
or the domain name registrant has failed to renew the domain name);
4. The CA is made aware of a material change in the information 
contained in the certificate;
5. The CA is made aware that the certificate was not issued in accordance 
with the CA's CP or CPS;
6. The CA determines or is made aware that any of the information 
appearing in the certificate is inaccurate;
7. The CA's right to issue certificates expires or is revoked or terminated, 
unless the CA has made arrangements to continue maintaining the 
CRL/OCSP repository;
8. Revocation is required by the CA's CP and/or CPS; or
9. The CA is made aware of a demonstrated or proven method that exposes the 
Subscriber's private key to compromise, methods have been developed that 
can easily calculate it based on the public key, or if there is clear evidence 
that the specific method used to generate the private key was flawed.

### 6.2.2 Reasons for Revoking a Subordinate CA Certificate ###

The issuing CA SHALL revoke a subordinate CA Certificate within 
seven (7) days if one or more of the following occurs:

1. The subordinate CA requests revocation in writing;
2. The subordinate CA notifies the issuing CA that the original 
certificate request was not authorized and does not 
retroactively grant authorization;
3. The issuing CA obtains evidence that the subordinate CA's private key 
corresponding to the public key in the Certificate suffered a 
key compromise;
4. The issuing CA obtains evidence that the certificate was misused;
5. The issuing CA is made aware that the certificate was not issued 
in accordance with or that subordinate CA has not complied with the 
applicable CP or CPS;
6. The issuing CA determines that any of the information appearing 
in the certificate is inaccurate or misleading;
7. The issuing CA or subordinate CA ceases operations for any reason 
and has not made arrangements for another CA to provide revocation 
support for the certificate;
8. The issuing CA's or subordinate CA's right to issue certificates 
expires or is revoked or terminated, unless the issuing CA has made 
arrangements to continue maintaining the CRL/OCSP repository; or
9. Revocation is required by the issuing CA's CP and/or CPS.

## 7. Root Store Changes ##

Changes that are motivated by a security concern such as certificate
misissuance or a root or intermediate compromise MUST be treated as a
security-sensitive, and a [secure bug filed in Bugzilla][Sec-Bugs].

### 7.1 Inclusions ###

We will determine which CA certificates are included in Mozilla's root program
based on the risks of
such inclusion to typical users of our products. We will consider adding
additional CA certificates to the default certificate set upon request only by
an authorized representative of the subject CA. We will make such decisions
through a public process.

We will not charge any fees to have a CA’s certificate(s)
included in Mozilla's root program.

We reserve the right to not include certificates from a particular CA in
our root program. This includes (but is not limited to) cases
where we believe that a CA has caused undue risks to users’
security, e.g. by knowingly issuing certificates without the knowledge of the
entities whose information is referenced in those certificates ('MITM certificates'). 
Mozilla is under no obligation to explain the reasoning behind any inclusion decision.

Before being included, CAs MUST provide evidence that their CA certificates have continually, from the time of creation, complied with the then-current Mozilla Root Store Policy and Baseline Requirements.

To request that its certificate(s) be added to Mozilla's root program a CA
SHOULD submit a formal request by submitting a [bug report][CA-Cert-Bug]
into the mozilla.org Bugzilla system, filed against the "CA
Certificate Root Program" component of the "NSS" product. Mozilla’s wiki
page, "[Applying for root inclusion in Mozilla products][How-To-Apply]", provides
further details about how to submit a formal request. The request
MUST be made by an authorized representative of the subject CA, and
MUST include the following:

1.  the certificate data (or links to the data) for the CA
    certificate(s) requested for inclusion;
2.  for each CA certificate requested for inclusion, whether or not
    the CA issues certificates for each of the following purposes
    within the certificate hierarchy associated with the CA
    certificate:
    * SSL-enabled servers
    * digitally-signed and/or encrypted email;
3.  for each CA certificate requested for inclusion, whether the CA
    issues Extended Validation certificates within the certificate hierarchy
    associated with the CA certificate and, if so, the EV policy
    OID associated with the CA certificate;
4.  a Certificate Policy and Certification Practice Statement (or
    links to a CP and CPS) or equivalent disclosure document(s)
    for the CA or CAs in question; *and*
5.  information as to how the CA has fulfilled the requirements
    stated above regarding its verification of certificate signing
    requests and its conformance to a set of acceptable operational
    criteria.

We will reject requests where the CA does not provide such
information within a reasonable period of time after submitting its
request.

### 7.2 Updates ###

Changes MAY be made to root certificates that are included in
Mozilla's root program as follows:

1.  enabling a trust bit in a root certificate that is currently
    included, may only be done after careful consideration of the
    CA’s current policies, practices, and audits,
    and may be requested by a representative of the CA or a
    representative of Mozilla by submitting a bug report into the
    mozilla.org Bugzilla system, as described in Mozilla’s wiki
    page, "[Applying for root inclusion in Mozilla products][How-To-Apply]";
2.  enabling EV in a root certificate that is currently included,
    may only be done after careful consideration of the CA’s current
    policies, practices, and audits,
    and may be requested by a representative of the CA or a
    representative of Mozilla by submitting a bug report into the
    mozilla.org Bugzilla system, as described in Mozilla’s wiki
    page, "[Applying for root inclusion in Mozilla products][How-To-Apply]";
3.  disabling a root is the act of turning off one or more of the
    trust bits (SSL or email), and may be
    requested by a representative of the CA or a representative of
    Mozilla by submitting a bug report into the mozilla.org Bugzilla
    system, as described in the [Root Change Process][Root-Changes];
4.  a representative of the CA or a representative of Mozilla may
    request that a root certificate be removed by submitting a bug
    report into the mozilla.org Bugzilla system, as described in the
    [Root Change Process][Root-Changes].

### 7.3 Removals ###

Mozilla MAY, at its sole discretion, decide to disable (partially or fully) or
remove a certificate at any time and for any reason. This may happen
immediately or on a planned future date. Mozilla will
disable or remove a certificate if the CA demonstrates ongoing or
egregious practices that do not maintain the expected level of service
or that do not comply with the requirements of this policy.

Mozilla will take any steps we deem appropriate to protect our users
if we learn that a CA has knowingly or intentionally mis-issued one
or more certificates. This may include, but is not limited to
disablement (partially or fully) or removal of all of the CA’s
certificates from Mozilla’s root program.

The category of mis-issued certificates includes (but is not limited to) those
issued to someone who should not have received them, those containing
information which was not properly validated, those having incorrect technical
constraints, and those using algorithms other than those permitted.

A failure to provide notifications or updates in the CCADB or
as otherwise required in a timely manner SHALL also be grounds for
disabling a CA’s root certificates or removing them from Mozilla's root
program. For this policy and the CCADB policies, "a timely manner" means
within 30 days of when the appropriate data or documentation becomes
available to the CA, unless a Mozilla policy document specifies a different
rule.

If Mozilla disables or removes a CA’s certificate(s) from Mozilla’s
root program based on a CA’s actions (or failure to act) that are
contrary to the Mozilla Root Store Policy, Mozilla will publicize 
that fact (for example, in newsgroups on the
news.mozilla.org server, and on our websites) and may also alert 
relevant news or government organizations such as US-CERT.

## 8. CA Operational Changes ##

CAs SHOULD NOT assume that trust is transferable. All CAs whose certificates
are included in Mozilla's root program MUST [notify Mozilla][Email-Us] if:

* ownership or control of the CA’s certificate(s) changes, or
* an organization other than the CA obtains control of an unconstrained 
intermediate certificate (as defined in section 5.3.2 of this policy) that 
directly or transitively chains to the CA's included certificate(s); or,
* ownership or control of the CA’s operations changes; or
* there is a [material change][Material-Change] in the CA's operations.

CAs should err on the side of notification if there is any doubt. Mozilla will
normally keep commercially sensitive information confidential. Throughout any
change, CA operations MUST continue to meet the requirements of this policy. If
one of the above events occurs, Mozilla MAY require additional audit(s) as a
condition of remaining in the root program. CAs are encouraged to notify in
advance in order to avoid unfortunate surprises.

In addition, one or more of the following sections MAY apply.

### 8.1 Change in Legal Ownership ###

This section applies when one company buys or takes a controlling stake in
a CA, or when an organization buys the private key of a CA certificate that is 
within the scope of Mozilla's root program, unless it is constrained in 
compliance with section 5.3.1 of this policy.

Mozilla MUST be notified of any resulting changes in the CA's CP or CPS.

If the receiving or acquiring company is new to the Mozilla root program, 
it must demonstrate compliance with the entirety of this policy and there
MUST be a public discussion regarding their admittance to the root program,
which Mozilla must resolve with a positive conclusion in order for the 
affected certificate(s) to remain in the root program. If the entire 
CA operation is not included in the scope of the transaction, issuance is not
permitted until the discussion has been resolved with a positive conclusion.

### 8.2 Change in Operational Personnel ###

This section applies when operation of a CA certificate that is within the 
scope of Mozilla's root program and not constrained in compliance with section 
5.3.1 of this policy is transferred to a different organization, 
whether by acquisition or contract.

The transferor MUST ensure that the transferee is able to fully comply with
this policy. The transferor will continue to be responsible for the root
certificate's private key until Mozilla has been provided with an audit
statement (or opinion letter) confirming successful transfer of the root
certificate and key. Issuance MUST NOT occur until the transferee
has provided all the information required by the CCADB, and demonstrated to
Mozilla that they have all the appropriate audits, CP/CPS documents and other
systems in place.

The transferor MUST notify Mozilla about any necessary changes to EV status or
trust bits in Mozilla's root store. If the transferee is receiving the (right
to use the) associated EV policy OID(s), the transferor MUST confirm that the
transferee has or will get the relevant audits before issuing EV certificates.

### 8.3 Change in Secure Location ###

The section only applies when section 8.1 and/or section 8.2 applies, and when the
cryptographic hardware related to a CA certificate that is within the scope of 
Mozilla's root program and not constrained in compliance with section 
5.3.1 of this policy is consequently moved from one secure location to another.

This policy and the relevant WebTrust or ETSI requirements apply at all times,
even during the physical relocation of a CA's online operations to a new data
center and moving parts of an offline root certificate from one location to
another. As such, a CA MUST always ensure that physical access to CA equipment
is limited to authorized individuals, the equipment is operated under multiple
person control, and unauthorized CA system usage is able to be detected at all
times. The auditor MUST confirm that there are appropriate procedures in place
to ensure that the requirements are met and that those procedures are followed.

The following steps MUST be taken by the organization(s) concerned:

* Make sure the annual audit statements are current.
* Notify Mozilla of the pending change.
* Create a transfer plan (and legal agreement if more than one organization is
involved) and have it reviewed by the auditors.
* Stop new certificate issuance at the current site before the transfer begins.
* Have an audit performed at the current site to confirm when the root
certificate is ready for transfer, and to make sure the key material is
properly secured.
* The transfer ceremony should be witnessed by auditors and video recorded,
with a physical exchange of the HSM or ciphertext containing the associated key
material and certificates, and the multi-party authorization keys.
* At the new site perform an audit to confirm that the transfer was successful,
that the private key remained secure throughout the transfer, and that the root
certificate is ready to resume issuance. This requirement may be met by
including the transferred root certificate and key in the new owner's regular
audits or by getting a point-in-time audit.
* Send links to the updated CP/CPS and the updated audit statements, opinion
letter, or point-in-time audit statement to Mozilla.

The regular annual audit statements MUST still happen in a timely manner.

The organization(s) concerned MUST immediately [send a security report to
Mozilla][Sec-Bugs] if a problem occurs.

-----

Any copyright in this document is [dedicated to the Public Domain][CC-0].

[Email-Us]:         mailto:certificates@mozilla.org
[CA-Cert-Module]:   https://wiki.mozilla.org/Modules/Activities#CA_Certificates
[CA-Policy-Module]: https://wiki.mozilla.org/Modules/Activities#Mozilla_CA_Certificate_Policy
[Gov-Module]:       https://wiki.mozilla.org/Modules/Firefox_Technical_Leadership
[MDSP]:             https://www.mozilla.org/about/forums/#dev-security-policy
[EVGLs]:            https://cabforum.org/extended-validation/
[BRs]:              https://cabforum.org/baseline-requirements-documents/
[NSGs]:             https://cabforum.org/network-security/
[ETSI-319-411-1]:   http://www.etsi.org/deliver/etsi_en/319400_319499/31941101/01.01.01_60/en_31941101v010101p.pdf
[ETSI-319-411-2]:   http://www.etsi.org/deliver/etsi_en/319400_319499/31941102/02.01.01_60/en_31941102v020101p.pdf
[WebTrust-2.0]:     http://www.webtrust.org/homepage-documents/item54279.pdf
[WebTrust-BRs]:     http://www.webtrust.org/principles-and-criteria/docs/item83987.pdf
[WebTrust-For-CAs]: http://www.webtrust.org/homepage-documents/item27839.aspx
[WebTrust-EV]:      http://www.webtrust.org/principles-and-criteria/docs/item83989.pdf
[CC-BY]:            https://creativecommons.org/licenses/by/4.0/
[CC-BY-SA]:         https://creativecommons.org/licenses/by-sa/4.0/
[CC-BY-ND]:         https://creativecommons.org/licenses/by-nd/4.0/
[CC-0]:             https://creativecommons.org/publicdomain/zero/1.0/
[CCADB-Policy]:     http://ccadb.org/policy
[5280-6.1.4]:       http://tools.ietf.org/html/rfc5280#section-6.1.4
[5280-4.2.1.12]:    http://tools.ietf.org/html/rfc5280#section-4.2.1.12
[CA-Cert-Bug]:      https://bugzilla.mozilla.org/enter_bug.cgi?product=NSS&component=CA%20Certificate%20Root%20Program
[How-To-Apply]:     https://wiki.mozilla.org/CA/Application_Process
[Root-Changes]:     https://wiki.mozilla.org/CA/Certificate_Change_Process
[Sec-Bugs]:         https://bugzilla.mozilla.org/enter_bug.cgi?product=NSS&component=CA%20Certificate%20Mis-Issuance&groups=crypto-core-security
[Material-Change]:  http://legal-dictionary.thefreedictionary.com/Material+Changes
[Policy-Archive]:   https://wiki.mozilla.org/CA/Root_Store_Policy_Archive
[Incident-Report]:  https://wiki.mozilla.org/CA/Responding_To_An_Incident
