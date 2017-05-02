# Mozilla Root Store Policy #

*Version 2.5 (draft)*

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
particular, under the terms of the relevant Mozilla license(s) distributors
of such software are permitted to add or delete CA certificates in the
versions that they distribute, and are also permitted to modify the values of
the trust bits on CA certificates in the default CA certificate set. However,
as with other software modifications, by making such changes a distributor MAY
well affect its ability to use Mozilla trademarks in connection with its
versions of the software. See the Mozilla trademark policy for more
information.

### 1.1 Scope ###

This policy applies, as appropriate, to certificates matching any of the
following (and the CAs which control or issue them):

1.  CA certificates applying for inclusion in, or included in, the Mozilla root
    store.

2.  Intermediate certificates which have at least one valid, unrevoked chain up
    to such a CA certificate and which are not technically constrained such
    that they are unable to issue working server or email certificates. Such
    technical constraints could consist of either:

    * an Extended Key Usage (EKU) extension which does not contain either of
      the id-kp-serverAuth and id-kp-emailProtection EKUs; or:
    * name constraints which do not allow SANs of any of the following types:
      dNSName, iPAddress, SRVName, rfc822Name

3.  End-entity certificates which have at least one valid, unrevoked chain up
    to such a CA certificate through intermediate certificates which are all in
    scope, such end-entity certificates having either:

    * an Extended Key Usage (EKU) extension which contains one or more of the
      id-kp-serverAuth and id-kp-emailProtection EKUs; or:
    * no EKU extension.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in RFC 2119.

### 1.2 Policy Ownership ###

Mozilla has appointed a [CA Certificate module owner][CA-Cert-Module]
and peers to evaluate new CA requests on our behalf and make decisions
regarding all matters relating to CA certificates included in our products.

The CA Certificate module team may change this policy in the future. We will do
so only after consulting with the public Mozilla community, in order to ensure
that all views are taken into account. CAs or others objecting to a particular
decision MAY appeal to the [Mozilla governance module owner][Gov-Module]
who will make a final decision.

You can contact the CA Certificate module team at
[certificates@mozilla.org][Email-Us] if you have questions about this policy.

## 2. Certificate Authorities ##

### 2.1 CA Operations ###

CAs whose certificates are distributed with our software products MUST:

1.  provide some service relevant to typical users of our software
    products;
2.  enforce multi-factor authentication for all accounts capable of
    directly causing certificate issuance, or implement technical
    controls operated by the CA to restrict certificate issuance
    through the account to a limited set of pre-approved domains or
    email addresses;
3.  prior to issuing certificates, verify certificate
    requests in a manner that we deem acceptable for the stated
    purpose(s) of the certificates;
4.  verify that all of the information that is included in SSL
    certificates remains current and correct at time intervals of
    thirty-nine months or less; and
5.  otherwise operate in accordance with published criteria that we
    deem acceptable.

CAs MUST follow and be aware of discussions in the
[mozilla.dev.security.policy][MDSP] forum, where Mozilla's root program is
coordinated. They are encouraged, but not required, to contribute to those
discussions.

### 2.2 Validation Practices ###

We consider verification of certificate signing requests to be acceptable if it
meets or exceeds the following requirements:

1.  all information that is supplied by the certificate subscriber
    MUST be verified by using an independent source of information
    or an alternative communication channel before it is included in
    the certificate;
2.  for a certificate capable of being used for digitally signing or encrypting
    email messages, the CA takes reasonable measures to verify that
    the entity submitting the request controls the email account
    associated with the email address referenced in the certificate
    *or* has been authorized by the email account holder to act on
    the account holder’s behalf;
3.  for a certificate capable of being used for SSL-enabled servers, the CA
    takes reasonable measures to verify that the entity submitting
    the certificate signing request has registered the domain name(s)
    referenced in the certificate *or* has been authorized by the
    domain registrant to act on the registrant’s behalf;
4.  for certificates marked as Extended
    Validation, the CA MUST comply with the latest version of the
    [Guidelines for the Issuance and Management of Extended Validation
    Certificates][EVGLs].

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

*   Mozilla reserves the right to accept audits by auditors who do not meet the
    qualifications given in section 8.2 of the Baseline Requirements, or refuse
    audits from auditors who do.

## 3. Documentation ##

### 3.1 Audits ###

Before being included and periodically thereafter, CAs MUST obtain certain
audits. This section describes the requirements for those audits.

#### 3.1.1 Audit Criteria ####

We consider the criteria for CA operations published in the
following documents to be acceptable:

*   WebTrust "[Principles and Criteria for Certification Authorities - Version
    2.0][WebTrust-2.0]" or later in [WebTrust Program for Certification
    Authorities][WebTrust-For-CAs];
*   WebTrust "[Principles and Criteria for Certification Authorities – SSL
    Baseline with Network Security - Version 2.0][WebTrust-BRs]" or later in
    [WebTrust Program for Certification Authorities][WebTrust-For-CAs];
*   WebTrust "[Principles and Criteria for Certification Authorities -
    Extended Validation SSL 1.4.5][WebTrust-EV]" or later in
    [WebTrust Program for Certification Authorities][WebTrust-For-CAs];
*   Requirements on CA practice", in ETSI TS 101 456 V1.4.3 or later version,
    [Policy requirements for certification authorities issuing qualified
    certificates][ETSI-101-456] (only applicable to electronic signature
    certificate issuance; applicable to either the "QCP public" or
    "QCP public + SSCD" certificate policies);
*   "Requirements on CA practice", in ETSI TS 102 042 V2.3.1 or later version,
    [Policy requirements for certification authorities issuing public key
    certificates][ETSI-102-042] (as applicable to the "EVCP" and "EVCP+"
    certificate policies, DVCP and OVCP certificate policies for publicly
    trusted certificates - baseline requirements, and any of the "NCP",
    "NCP+", or "LCP" certificate policies);
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

If being audited to the WebTrust criteria, the following audits are required
(see section 3.1.1 for specific version numbers):

*   For the SSL trust bit, a CA and all subordinate CAs technically capable
    of issuing server certificates must have all of the following:

    * [WebTrust for CAs][WebTrust-2.0]
    * [WebTrust for CAs - SSL Baseline with Network Security][WebTrust-BRs]
    * [WebTrust for CAs - EV SSL][WebTrust-EV] (if applying for EV recognition)

*   For the email trust bit, a CA and all subordinate CAs technically capable
    of issuing email certificates must have all of the following:

    * [WebTrust for CAs][WebTrust-2.0]

##### 3.1.2.2 ETSI #####

If being audited to the ETSI criteria, the following audits are required
(see section 3.1.1 for version numbers):

*   For the SSL trust bit, a CA and all subordinate CAs technically capable
    of issuing server certificates must have either of the following:

    * [ETSI TS 102 042][ETSI-102-042] - DVCP, OVCP, PTC-BR
    * [ETSI EN 319 411-1][ETSI-319-411-1] - DVCP, OVCP, PTC-BR

*   For the email trust bit, a CA and all subordinate CAs technically capable
    of issuing email certificates must have either of the following sets of
    audits:

    * [ETSI TS 101 456][ETSI-101-456]
      and [ETSI TS 102 042][ETSI-102-042] - LCP, NCP, NCP+
    * [ETSI EN 319 411-1][ETSI-319-411-1]
      and [ETSI EN 319 411-2][ETSI-319-411-2] - LCP, NCP, NCP+

#### 3.1.3 Public Audit Information ####

The publicly-available documentation relating to each audit MUST contain at
least the following clearly-labelled information:

1.  name of the company being audited;
2.  name and address of the organization performing the audit;
3.  DN and SHA256 fingerprint of each root and intermediate certificate that
    was in scope;
4.  audit criteria (with version number) that were used to audit each of
    the certificates;
5.  a list of the CA policy documents (with version numbers) referenced during
    the audit;
6.  whether the audit is for a period of time or point in time;
7.  the start date and end date of the period, for those that cover a period
    of time;
8.  the point in time date, for those that are for a point in time;
9.  the date the report was issued (which will necessarily be after the end
    date or point in time date); and
10. For ETSI, a statement that the audit was a full audit, and which parts
    of the criteria were applied, e.g. DVCP, OVCP, NCP, NCP+, LCP, EVCP,
    EVCP+, Part1 (General Requirements), and/or Part 2 (Requirements for
    trust service providers).

For audit reports which are being supplied to maintain a certificate within
the Mozilla root program, they MUST be provided to Mozilla within three
months of the point in time date or the end date of the period.

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

CPs and CPSes MUST be reviewed and updated as necessary at least once every
year, as required by the Baseline Requirements. CAs MUST indicate that this has
happened by incrementing the version number and adding a dated changelog entry,
even if no other changes are made to the document.

## 4. Common CA Database ##

Mozilla manages its root store using the Common CA Database (CCADB). CAs in the
program MUST use the CCADB, and are bound by the [Common CCADB Policy
v1.0](../ccadb/policy.md) and the [Mozilla CCADB Policy
v1.0](../ccadb/mozilla.md), which are incorporated here by reference.

## 5. Certificates ##

### 5.1 Algorithms ###

Root certificates in our root program, and any certificate which
chains up to them, MUST use only algorithms and key sizes from the following
set:

*   RSA keys whose modulus size in bits is divisible by 8, and is at
    least 2048.
*   Digest algorithms: SHA-1 (see below), SHA-256, SHA-384, or SHA-512.
*   ECDSA keys using one of the following curve-hash pairs:
    * P‐256 with SHA-256
    * P‐384 with SHA-384

#### 5.1.1 SHA-1 ####

CAs MAY sign SHA-1 hashes over end-entity certificates which chain
up to roots in Mozilla's program only if all the following are true:

1. The end-entity certificate:

   * is not within the scope of the Baseline Requirements;
   * contains an EKU extension which does not contain either of the id-kp-
     serverAuth or anyExtendedKeyUsage key purposes;
   * has at least 64 bits of entropy from a CSPRNG in the serial number.

2. The issuing certificate:

   * contains an EKU extension which does not contain either of the id-kp-
     serverAuth or anyExtendedKeyUsage key purposes;
   * has a pathlen:0 constraint.

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

These requirements include all cross-certified certificates
which chain to a certificate that is included in Mozilla’s CA
Certificate Program.

#### 5.3.1 Technically Constrained ####

We encourage CAs to technically constrain all subordinate CA
certificates. For a certificate to be considered technically
constrained, the certificate MUST include an [Extended Key Usage
(EKU)][5280-4.2.1.12] extension specifying all extended key usages that the
subordinate CA is authorized to issue certificates for. The anyExtendedKeyUsage
KeyPurposeId MUST NOT appear within this extension.

If the certificate includes the id-kp-serverAuth extended key usage,
then the certificate MUST be Name Constrained as described in section
7.1.5 of version 1.3 or later of the [Baseline Requirements][BRs].

If the certificate includes the id-kp-emailProtection extended
key usage, then all end-entity certificates MUST only include
e-mail addresses or mailboxes that the issuing CA has confirmed
(via technical and/or business controls) that the subordinate CA
is authorized to use.

#### 5.3.2 Publicly Disclosed and Audited ####

We recognize that technically constraining subordinate CA
certificates as described above may not be practical in some cases.
All certificates that are capable of being used to issue new
certificates, that are not technically constrained, and that
directly or transitively chain to a certificate included in
Mozilla’s CA Certificate Program MUST be audited in accordance with
Mozilla’s Root Store Policy and MUST be publicly disclosed in the
CCADB by the CA that has their certificate
included in Mozilla’s CA Certificate Program. The CA with a
certificate included in Mozilla’s CA Certificate Program MUST
disclose this information within a week of certificate creation, and
before any such subordinate CA is allowed
to issue certificates. All disclosure MUST be made freely available
and without additional requirements, including, but not limited to,
registration, legal agreements, or restrictions on redistribution of
the certificates in whole or in part.

## 6. Revocation ##

CAs MUST revoke Certificates that they have issued upon the
occurrence of any of the following events:

1.  the subscriber indicates that the original certificate request
    was not authorized and does not retroactively grant
    authorization;
2.  the CA obtains reasonable evidence that the subscriber’s private
    key (corresponding to the public key in the certificate) has
    been compromised or is suspected of compromise (e.g. Debian weak
    keys);
3.  the CA obtains reasonable evidence that the certificate has been used for a
    purpose outside of that indicated in the certificate or in the CA's
    subscriber agreement;
4.  the CA receives notice or otherwise becomes aware that a
    subscriber has violated one or more of its material obligations
    under the subscriber agreement;
5.  the CA receives notice or otherwise becomes aware of any
    circumstance indicating that use of the domain name in the
    certificate is no longer legally permitted (e.g. a court or
    arbitrator has revoked a subscriber’s right to use the domain
    name listed in the certificate, a relevant licensing or services
    agreement with the registrant has terminated, or the registrant
    of the domain name has failed to renew it);
6.  the CA receives notice or otherwise becomes aware of a material
    change in the information contained in the certificate;
7.  a determination, in the CA’s sole discretion, that the
    certificate was not issued in accordance with the CA’s
    Certificate Policy or Certification Practice Statement;
8.  the CA determines that any of the information appearing in the
    certificate is not accurate, with the exception of the
    organizationalUnitName field, if present;
9.  the CA ceases operations for any reason and has not arranged for
    another CA to provide revocation support for the certificate;
10. the CA private key used in issuing the certificate is suspected
    to have been compromised; or
11. such additional revocation events as the CA publishes in its
    policy documentation.

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

## 7. Root Store Changes ##

Changes that are motivated by a serious security concern
such as a major root compromise SHOULD be treated as a
security-sensitive bug, and the [Mozilla Policy for Handling Security
Bugs][Sec-Bugs] SHOULD be followed.

### 7.1 Inclusions ###

We will determine which CA certificates are included in software
products distributed by Mozilla, based on the benefits and risks of
such inclusion to typical users of those products. We will consider adding
additional CA certificates to the default certificate set upon request only by
an authorized representative of the subject CA. We will make such decisions
through a public process, based on objective and verifiable criteria.

We will not charge any fees to have a CA’s certificate(s)
distributed with our software products.

We reserve the right to not include certificates from a particular CA in
our software products. This includes (but is not limited to) cases
where we believe that a CA has caused undue risks to users’
security, for example, by:

*   knowingly issue certificates without the knowledge of the
    entities whose information is referenced in the certificates; or
*   knowingly issue certificates that appear to be intended for
    fraudulent use.

To request that its certificate(s) be added to the default set a CA
SHOULD submit a formal request by submitting a [bug report][CA-Cert-Bug]
into the mozilla.org Bugzilla system, filed against the "CA
Certificates" component of the "mozilla.org" product. Mozilla’s wiki
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
Mozilla products as follows:

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
    trust bits (Websites, Email), and may be
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
certificates from Mozilla’s products. A certificate that includes
domain names that have not been verified according to section 3.2.2.4 of the
[Baseline Requirements][BRs] is considered to be mis-issued. A certificate
that is intended to be used only as an end entity certificate but includes a
keyUsage extension with values keyCertSign and/or cRLSign or a basicConstraints
extension with the cA field set to true is considered to be mis-issued.

A failure to provide notifications or updates in the CCADB or
as otherwise required in a timely manner SHALL also be grounds for
disabling a CA’s root certificates or removing them from Mozilla
products. For this policy and the CCADB policies, "a timely manner" means
within 30 days of when the appropriate data or documentation becomes
available to the CA, unless a policy specifies a different rule.

If Mozilla disables or removes a CA’s certificate(s) from Mozilla’s
products based on a CA’s actions (or failure to act) that are
contrary to the Mozilla Root Store Policy,
Mozilla will publicize that fact in newsgroups on the
news.mozilla.org server, on Web pages in the mozilla.org and
mozilla.com domains, in news releases sent to organizations
specializing in computer and Internet news, and/or as an alert to the
US-CERT organization of the U.S. Department of Homeland Security.

## 8. CA Operational Changes ##

CAs SHOULD NOT assume that trust is transferable. All CAs whose certificates
are included in Mozilla's root program MUST [notify Mozilla][Email-Us] if:

* ownership or control of the CA’s certificate(s) changes, or
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
a CA, or when an organization buys the private key of a certificate in
Mozilla's root program.

Mozilla MUST be notified of any resulting changes in the CA's CP or CPS.

If the receiving or acquiring company is new to the Mozilla root program, there
MUST be a public discussion regarding their admittance to the root program,
which Mozilla must resolve with a positive conclusion before issuance is
permitted.

### 8.2 Change in Operational Personnel ###

This section applies when operation of a certificate in Mozilla's root program
is transferred to a different organization, whether by acquisition or contract.

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

The section applies when section 8.1 and/or section 8.2 applies, and when the
cryptographic hardware related to a certificate in Mozilla's root store is
consequently moved from one secure location to another.

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
audits or by getting a PITRA.
* Send links to the updated CP/CPS and the updated audit statements, opinion
letter, or PITRA statement to Mozilla.

The regular annual audit statements MUST still happen in a timely manner.

The organization(s) concerned MUST immediately [send a security report to
Mozilla][Sec-Bugs] if a problem occurs.

-----

Any copyright in this document is [dedicated to the Public Domain][CC-0].

[Email-Us]:         mailto:certificates@mozilla.org
[CA-Cert-Module]:   https://wiki.mozilla.org/Modules/Activities#Mozilla_CA_Certificate_Policy
[Gov-Module]:       https://wiki.mozilla.org/Modules/Activities#Governance
[MDSP]:             https://www.mozilla.org/about/forums/#dev-security-policy
[EVGLs]:            https://cabforum.org/extended-validation/
[BRs]:              https://cabforum.org/baseline-requirements-documents/
[ETSI-101-456]:     http://www.etsi.org/deliver/etsi_ts/101400_101499/101456/01.04.03_60/ts_101456v010403p.pdf
[ETSI-102-042]:     http://www.etsi.org/deliver/etsi_ts/102000_102099/102042/02.03.01_60/ts_102042v020301p.pdf
[ETSI-319-411-1]:   http://www.etsi.org/deliver/etsi_en/319400_319499/31941101/01.01.01_60/en_31941101v010101p.pdf
[ETSI-319-411-2]:   http://www.etsi.org/deliver/etsi_en/319400_319499/31941102/02.01.01_60/en_31941102v020101p.pdf
[WebTrust-2.0]:     http://www.webtrust.org/homepage-documents/item54279.pdf
[WebTrust-BRs]:     http://www.webtrust.org/homepage-documents/item79806.pdf
[WebTrust-For-CAs]: http://www.webtrust.org/homepage-documents/item27839.aspx
[WebTrust-EV]:      http://www.webtrust.org/homepage-documents/item79807.pdf
[CC-BY]:            https://creativecommons.org/licenses/by/4.0/
[CC-BY-SA]:         https://creativecommons.org/licenses/by-sa/4.0/
[CC-BY-ND]:         https://creativecommons.org/licenses/by-nd/4.0/
[CC-0]:             https://creativecommons.org/publicdomain/zero/1.0/
[5280-6.1.4]:       http://tools.ietf.org/html/rfc5280#section-6.1.4
[5280-4.2.1.12]:    http://tools.ietf.org/html/rfc5280#section-4.2.1.12
[CA-Cert-Bug]:      https://bugzilla.mozilla.org/enter_bug.cgi?product=mozilla.org&amp;component=CA%20Certificates
[How-To-Apply]:     https://wiki.mozilla.org/CA:How_to_apply
[Root-Changes]:     https://wiki.mozilla.org/CA:Root_Change_Process
[Sec-Bugs]:         https://www.mozilla.org/about/governance/policies/security-group/bugs/
[Material-Change]:  http://legal-dictionary.thefreedictionary.com/Material+Changes
