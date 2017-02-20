# Mozilla CA Certificate Policy #

*Version 2.4 (draft)*

When distributing binary and source code versions of Firefox, Thunderbird, and
other Mozilla-related software products, Mozilla may include with such software
a default set of X.509v3 certificates for various Certification Authorities
(CAs). The certificates included by default have their "trust bits" set for
various purposes, so that the software in question can use the CA certificates
to verify certificates for SSL servers and S/MIME email users without having
to ask users for further permission or information.

This is the official Mozilla policy for CA certificates that are distributed
with Mozilla software products. This policy consists of the following
sections:

* [Audit Requirements](audit-requirements)

    Before being included and periodically thereafter, CAs are required to
    obtain certain audits. This section describes the requirements for those
    audits.

* [Applying for Inclusion of Root Certificates in Mozilla Products](#applying-for-inclusion-of-root-certificates-in-mozilla-products)

    This section describes the obligations of Certification Authorities
    applying for inclusion of their root certificates in Mozilla Products.
    This includes considerations that are taken into account such as the CA’s
    publicly available documentation about their policies, and audits of the
    CA’s operations in support of the documented policies.

* [Maintaining Confidence in Included Root Certificates](#maintaining-confidence-in-included-root-certificates)

    This section describes the obligations of Certification Authorities for
    maintaining confidence in their root certificates that are included in
    Mozilla Products. This includes regular auditing of the CA’s policies and
    practices; conforming to current CA industry standards and recommended
    best practices; and making changes to included root certificates.

* [Enforcing the Mozilla CA Certificate Policy](#enforcing-the-mozilla-ca-certificate-policy)

    This section describes the steps that Mozilla may take in order to enforce
    this policy. This includes evaluation of security concerns, and removing
    or disabling a root certificate.

In addition, Mozilla manages its root store using the Common CA Database
(CCADB). CAs in the program are required to use the CCADB, and are bound by the
[Common CCADB Policy v1.0](../ccadb/policy.md) and the
[Mozilla CCADB Policy v1.0](../ccadb/mozilla.md), which are incorporated here
by reference.

This policy applies only to software products distributed by Mozilla,
including the Mozilla Foundation and its subsidiaries. Other entities
distributing such software are free to adopt their own policies. In
particular, under the terms of the relevant Mozilla license(s) distributors
of such software are permitted to add or delete CA certificates in the
versions that they distribute, and are also permitted to modify the values of
the "trust bits" on CA certificates in the default CA certificate set. As with
other software modifications, by making such changes a distributor may affect
its ability to use Mozilla trademarks in connection with its versions of the
software; see the Mozilla trademark policy for more information.

This policy applies, as appropriate, to certificates matching any of the
following:

1. CA certificates applying for inclusion in, or included in, Mozilla Products.

2. Intermediate certificates which have at least one valid, unrevoked chain up
   to such a CA certificate and which are not technically constrained such
   that they are unable to issue working server or email certificates. Such
   technical constraints could consist of either:
   * an Extended Key Usage (EKU) extension which does not contain either of the
     id-kp-serverAuth and id-kp-emailProtection EKUs; or:
   * name constraints which do not allow SANs of any of the following types:
     dNSName, iPAddress, SRVName, rfc822Name

3. End-entity certificates which have at least one valid, unrevoked chain up to
   such a CA certificate through intermediate certificates which are all in
   scope, such end-entity certificates having either:
   * an Extended Key Usage (EKU) extension which contains one or more of the
     id-kp-serverAuth and id-kp-emailProtection EKUs; or:
   * no EKU extension.

Please contact Mozilla at
[certificates@mozilla.org](mailto:certificates@mozilla.org) for more
information about this policy and answers to related questions.

We reserve the right to change this policy in the future. We will do so only
after consulting with the public Mozilla community, in order to ensure that
all views are taken into account.


## Audit Requirements ##

Before being included and periodically thereafter, CAs are required to
obtain certain audits. This section describes the requirements for those
audits.

1. We consider the criteria for CA operations published in any of the
   following documents to be acceptable:
   -   WebTrust ["Principles and Criteria for Certification
       Authorities 2.0"][WebTrust-2.0] or later and ["WebTrust Principles and
       Criteria for Certification Authorities – SSL Baseline with Network
       Security – Version 2.0"][WebTrust-BRs] or later (as applicable to SSL
       certificate issuance) in [WebTrust Program for Certification
       Authorities][WebTrust-For-CAs];
   -   WebTrust ["Principles and Criteria for Certification Authorities -
       Extended Validation SSL 1.4.5”][WebTrust-EV] or later in
       [WebTrust Program for Certification Authorities][WebTrust-For-CAs];
   -   "Requirements on CA practice", in ETSI TS 101 456 V1.4.3 or
       later version, [Policy requirements for certification authorities issuing
       qualified certificates][ETSI-101-456] (only applicable to electronic
       signature certificate issuance; applicable to either the "QCP public" or
       "QCP public + SSCD" certificate policies);
   -   "Requirements on CA practice", in ETSI TS 102 042
       V2.3.1 or later version, [Policy requirements for certification
       authorities issuing public key certificates][ETSI-102-042]
       (as applicable to the "EVCP" and "EVCP+" certificate policies,
       DVCP and OVCP certificate policies for publicly trusted
       certificates - baseline requirements, and any of the "NCP",
       "NCP+", or "LCP" certificate policies);
   -   “Trust Service Providers practice” in ETSI EN 319 411-1 v1.1.1 or
       later version [Policy and security requirements for Trust Service Providers
       issuing certificates; Part 1: General requirements][ETSI-319-411-1],
       specifying a policy or policies appropriate to the trust bit(s) being
       applied for;
   -   “Trust Service Providers practice” in ETSI EN 319 411-2 v2.1.1 or
       later version [Policy and security requirements for Trust Service Providers
       issuing certificates; Part 2: Requirements for trust service providers
       issuing EU qualified certificates][ETSI-319-411-2], specifying a
       policy or policies appropriate to the trust bit(s) being applied for.

   We reserve the right to accept other criteria in the future.

2. CA operations relating to issuance of certificates capable of being used for
   SSL-enabled servers must also conform to the latest version of the
   [CA/Browser Forum Baseline Requirements for the Issuance and
   Management of Publicly-Trusted
   Certificates.](https://cabforum.org/baseline-requirements-documents/) In the
   event of inconsistency between Mozilla’s CA Certificate Policy
   requirements and the Baseline Requirements, Mozilla’s CA Certificate Policy
   takes precedence. Below is a list of known places where this policy takes
   precedence over the Baseline Requirements. If you find an
   inconsistency that is not listed here, notify Mozilla by sending
   email to certificates@mozilla.org so the item can be considered.
   -   Mozilla’s CA Certificate Policy defining a competent and
       independent auditor is a superset of section 8.2 of the
       Baseline Requirements, and takes precedence over it.

3. By "competent party" we mean a person or other entity who is
   authorized to perform audits according to the stated criteria (e.g.,
   by the organization responsible for the criteria or by a relevant
   government agency) *or* for whom there is sufficient public
   information available to determine that the party is competent to
   judge the CA’s conformance to the stated criteria. In the latter
   case the "public information" referred to should include information
   regarding the party’s
   -   knowledge of CA-related technical issues such as public key
       cryptography and related standards;
   -   experience in performing security-related audits, evaluations,
       or risk analyses; *and*
   -   honesty and objectivity.

4. By "independent party" we mean a person or other entity who is not
   affiliated with the CA as an employee or director *and* for whom at
   least one of the following statements is true:
   -   the party is not financially compensated by the CA;
   -   the nature and amount of the party’s financial compensation by
       the CA is publicly disclosed; *or*
   -   the party is bound by law, government regulation, and/or a
       professional code of ethics to render an honest and objective
       judgement regarding the CA.

5. We reserve the right to designate our own representative(s) to act
   as the competent independent party or parties described above,
   should that prove to be necessary and appropriate.

6. The burden is on the CA to prove that it has met the above
   requirements. However the CA may request a preliminary determination
   from us regarding the acceptability of the criteria and/or the
   competent independent party or parties by which it proposes to meet
   the requirements of this policy.

7. The publicly-available documentation relating to each audit must contain at
   least the following clearly-labelled information:

   - a list of the CA policy documents (with version numbers) referenced during
     the audit;
   - whether the audit is for a period of time or point in time;
   - the start date and end date of the period, for those that cover a period
     of time;
   - the point in time date, for those that are for a point in time;
   - the date the report was issued (which will necessarily be after the end
     date or point in time date).

   For audit reports which are being supplied to maintain a certificate within
   the Mozilla root program, they must be provided to Mozilla within three
   months of the point in time date or the end date of the period.


## Applying for Inclusion of Root Certificates in Mozilla Products ##

This is the official Mozilla policy for Certification Authorities
applying for inclusion of their CA Certificates to be distributed in
Mozilla products:

1.  We will determine which CA certificates are included in software
    products distributed by Mozilla, based on the benefits and risks of
    such inclusion to typical users of those products.
2.  We will make such decisions through a public process, based on
    objective and verifiable criteria as described below.
3.  We will not charge any fees to have a CA’s certificate(s)
    distributed with our software products.
4.  We reserve the right to not include a particular CA certificate in
    our software products. This includes (but is not limited to) cases
    where we believe that including a CA certificate (or setting its
    "trust bits" in a particular way) would cause undue risks to users’
    security, for example, with CAs that
    -   knowingly issue certificates without the knowledge of the
        entities whose information is referenced in the certificates;
        *or*
    -   knowingly issue certificates that appear to be intended for
        fraudulent use.

    This also includes (but again is not limited to) cases where we
    believe that including a CA certificate (or setting its "trust bits"
    in a particular way) might cause technical problems with the
    operation of our software, for example, with CAs that issue
    certificates that have
    -   ASN.1 DER encoding errors;
    -   invalid public keys (e.g., RSA certificates with public exponent
        equal to 1);
    -   duplicate issuer names and serial numbers (except that a Certificate
        Transparency pre-certificate is allowed to match the corresponding
        certificate);
    -   incorrect extensions (e.g., SSL certificates that exclude SSL
        usage, or authority key IDs that include both the key ID and the
        issuer’s issuer name and serial number); *or*
    -   cRLDistributionPoints or OCSP authorityInfoAccess extensions for
        which no operational CRL or OCSP service exists.

5.  We will consider adding additional CA certificates to the
    default certificate set upon request only by an authorized
    representative of the subject CA.
6.  We require that all CAs whose certificates are distributed with our
    software products:
    -   provide some service relevant to typical users of our software
        products;
    -   enforce multi-factor authentication for all accounts capable of
        directly causing certificate issuance or implement technical
        controls operated by the CA to restrict certificate issuance
        through the account to a limited set of pre-approved domains or
        email addresses;
    -   maintain a certificate hierarchy such that the included
        certificate does not directly issue end-entity certificates to
        customers (e.g., the included certificate signs intermediate
        issuing certificates), as described in section 6.1.7 of the
        [CA/Browser Forum Baseline
        Requirements](https://cabforum.org/baseline-requirements-documents/);
    -   prior to issuing certificates, verify certificate signing
        requests in a manner that we deem acceptable for the stated
        purpose(s) of the certificates;
    -   verify that all of the information that is included in SSL
        certificates remains current and correct at time intervals of
        thirty-nine months or less; and
    -   otherwise operate in accordance with published criteria that we
        deem acceptable.

7.  We consider verification of certificate signing requests to be
    acceptable if it meets or exceeds the following requirements:
    -   all information that is supplied by the certificate subscriber
        must be verified by using an independent source of information
        or an alternative communication channel before it is included in
        the certificate;
    -   for a certificate capable of being used for digitally signing or encrypting
        email messages, the CA takes reasonable measures to verify that
        the entity submitting the request controls the email account
        associated with the email address referenced in the certificate
        *or* has been authorized by the email account holder to act on
        the account holder’s behalf;
    -   for a certificate capable of being used for SSL-enabled servers, the CA
        takes reasonable measures to verify that the entity submitting
        the certificate signing request has registered the domain(s)
        referenced in the certificate *or* has been authorized by the
        domain registrant to act on the registrant’s behalf;
    -   for certificates marked as Extended
        Validation, the CA complies with the latest version of the
        [Guidelines for the Issuance and Management of Extended Validation
        Certificates](https://cabforum.org/extended-validation/).

    We reserve the right to use other requirements in the future.

8.  All certificates that are capable of being used to issue new
    certificates, and which directly or transitively chain to a
    certificate included in Mozilla’s CA Certificate Program, MUST be
    operated in accordance with Mozilla’s CA Certificate Policy
    and MUST either be **technically constrained** or be **publicly
    disclosed and audited.**
    -   A certificate is deemed as capable of being used to issue new
        certificates if it contains an [X.509v3 basicConstraints
        extension,](http://tools.ietf.org/html/rfc5280#section-6.1.4)
        with the cA boolean set to true. The term "subordinate CA" below
        refers to any organization or legal entity that is in possession
        or control of a certificate that is capable of being used to
        issue new certificates.
    -   These requirements include all cross-certified certificates
        which chain to a certificate that is included in Mozilla’s CA
        Certificate Program.

9.  We encourage CAs to technically constrain all subordinate CA
    certificates. For a certificate to be considered **technically
    constrained,** the certificate MUST include an [Extended Key Usage
    (EKU)](http://tools.ietf.org/html/rfc5280#section-4.2.1.12)
    extension specifying all extended key usages that the subordinate CA
    is authorized to issue certificates for. The anyExtendedKeyUsage
    KeyPurposeId MUST NOT appear within this extension.
    -   If the certificate includes the id-kp-serverAuth extended key usage,
        then the certificate must be Name Constrained as described in section
        7.1.5 of version 1.3 or later of the [CA/Browser Forum Baseline
        Requirements for the Issuance and Management of Publicly-Trusted
        Certificates](https://cabforum.org/baseline-requirements-documents/).
    -   If the certificate includes the id-kp-emailProtection extended
        key usage, then all end-entity certificates MUST only include
        e-mail addresses or mailboxes that the issuing CA has confirmed
        (via technical and/or business controls) that the subordinate CA
        is authorized to use.

10. We recognize that technically constraining subordinate CA
    certificates as described above may not be practical in some cases.
    All certificates that are capable of being used to issue new
    certificates, that are not technically constrained, and that
    directly or transitively chain to a certificate included in
    Mozilla’s CA Certificate Program MUST be audited in accordance with
    Mozilla’s CA Certificate Policy and MUST be publicly disclosed in the
    CCADB by the CA that has their certificate
    included in Mozilla’s CA Certificate Program. The CA with a
    certificate included in Mozilla’s CA Certificate Program MUST
    disclose this information before any such subordinate CA is allowed
    to issue certificates. All disclosure MUST be made freely available
    and without additional requirements, including, but not limited to,
    registration, legal agreements, or restrictions on redistribution of
    the certificates in whole or in part.

17. We rely on publicly disclosed documentation (e.g., in a Certificate
    Policy and Certification Practice Statement) and publicly disclosed
    audit statements to ascertain that the above requirements are met.
    Therefore, inclusion requests will only be considered if the
    following are true:
    -   the publicly disclosed documentation provides sufficient
        information for Mozilla to determine whether and how the CA
        complies with this policy, including a description of the steps
        taken by the CA to verify certificate signing requests;
    -   the documentation is available from the CA’s official website;
    -   CPs and CPSes are made available to Mozilla under one
        of the following Creative Commons licenses (or later versions):
        * Attribution ([CC-BY](https://creativecommons.org/licenses/by/4.0/)) 4.0
        * Attribution-ShareAlike ([CC-BY-SA](https://creativecommons.org/licenses/by-sa/4.0/)) 4.0
        * Attribution-NoDerivs ([CC-BY-ND](https://creativecommons.org/licenses/by-nd/4.0/)) 4.0
        * Public Domain Dedication ([CC-0](https://creativecommons.org/publicdomain/zero/1.0/)) 1.0

        or a set of equally permissive licensing terms accepted by Mozilla in
        writing. If no such license is indicated, the fact of application is
        considered as permission from the CA to allow Mozilla and the public to
        deal with these documents, and any later versions for root certificates
        which are included in Mozilla's trust store, under CC-BY-ND.

18. To request that its certificate(s) be added to the default set a CA
    should submit a formal request by submitting a [bug
    report](https://bugzilla.mozilla.org/enter_bug.cgi?product=mozilla.org&amp;component=CA%20Certificates)
    into the mozilla.org Bugzilla system, filed against the "CA
    Certificates" component of the "mozilla.org" product. Mozilla’s wiki
    page, [Applying for root inclusion in Mozilla
    products](https://wiki.mozilla.org/CA:How_to_apply), provides
    further details about how to submit a formal request. The request
    must be made by an authorized representative of the subject CA, and
    should include the following:
    -   the certificate data (or links to the data) for the CA
        certificate(s) requested for inclusion;
    -   for each CA certificate requested for inclusion, whether or not
        the CA issues certificates for each of the following purposes
        within the certificate hierarchy associated with the CA
        certificate:
        -   SSL-enabled servers, *or*
        -   digitally-signed and/or encrypted email;
    -   for each CA certificate requested for inclusion, whether the CA
        issues Extended Validation certificates within the certificate hierarchy
        associated with the CA certificate *and*, if so, the EV policy
        OID associated with the CA certificate;
    -   a Certificate Policy and Certification Practice Statement (or
        links to a CP and CPS) *or* equivalent disclosure document(s)
        for the CA or CAs in question; *and*
    -   information as to how the CA has fulfilled the requirements
        stated above regarding its verification of certificate signing
        requests and its conformance to a set of acceptable operational
        criteria.

    We will reject requests where the CA does not provide such
    information within a reasonable period of time after submitting its
    request.

19. We have appointed a [CA certificate "module
    owner"](https://wiki.mozilla.org/Modules/Activities#Mozilla_CA_Certificate_Policy)
    and (optionally) one or more "peers" to evaluate CA requests on our
    behalf and make decisions regarding all matters relating to CA
    certificates included in our products. CAs or others objecting to a
    particular decision may appeal to the [Mozilla governance module
    owner or
    peer(s)](https://wiki.mozilla.org/Modules/Activities#Governance),
    who will make a final decision.


## Maintaining Confidence in Included Root Certificates ##

This section of the Mozilla CA Certificate Policy
describes the obligations of Certification Authorities for maintaining
confidence in their root certificates that are included in Mozilla
Products. This includes regular auditing of the CA’s policies and
practices; conforming to current CA industry standards and recommended
best practices; and making changes to included root certificates.

This is the official Mozilla policy for Certification Authorities to
maintain their CA Certificates that are distributed in Mozilla products:

1.  CAs are expected to maintain the level of service that was
    established in the [Inclusion Section of the Mozilla CA Certificate
    Policy](#inclusion).
2.  CAs must revoke Certificates that they have issued upon the
    occurrence of any of the following events:
    -   the subscriber indicates that the original certificate request
        was not authorized and does not retroactively grant
        authorization;
    -   the CA obtains reasonable evidence that the subscriber’s private
        key (corresponding to the public key in the certificate) has
        been compromised or is suspected of compromise (e.g. Debian weak
        keys), or that the certificate has been used for a purpose outside
        of that indicated in the certificate or in the CA's subscriber
        agreement;
    -   the CA receives notice or otherwise becomes aware that a
        subscriber has violated one or more of its material obligations
        under the subscriber agreement;
    -   the CA receives notice or otherwise becomes aware of any
        circumstance indicating that use of the domain name in the
        certificate is no longer legally permitted (e.g. a court or
        arbitrator has revoked a subscriber’s right to use the domain
        name listed in the certificate, a relevant licensing or services
        agreement with the registrant has terminated, or the registrant
        of the domain name has failed to renew it);
    -   the CA receives notice or otherwise becomes aware of a material
        change in the information contained in the certificate;
    -   a determination, in the CA’s sole discretion, that the
        certificate was not issued in accordance with the CA’s
        Certificate Policy or Certification Practice Statement;
    -   the CA determines that any of the information appearing in the
        certificate is not accurate, with the exception of the
        organizationalUnitName field, if present.
    -   the CA ceases operations for any reason and has not arranged for
        another CA to provide revocation support for the certificate;
    -   the CA private key used in issuing the certificate is suspected
        to have been compromised; or
    -   such additional revocation events as the CA publishes in its
        policy documentation.

3.  CAs must maintain an online 24x7 repository mechanism whereby
    application software can automatically check online the current
    status of all unexpired certificates issued by the CA.

    For end-entity certificates, CRLs must be updated and reissued at least
    every seven days, and the value of the nextUpdate field shall not be
    more than ten days beyond the value of the thisUpdate field.

    For end-entity certificates, if the CA provides revocation information
    via an Online Certificate Status Protocol (OCSP) service:
    - it must update that service at least every four days; and
    - responses must have a defined value in the nextUpdate field, and it
      must be no more than ten days after the thisUpdate field; and
    - the value in the nextUpdate field must be before or equal to the
      notAfter date of all certificates included within the
      BasicOCSPResponse.certs field or, if the certs field is omitted,
      before or equal to the notAfter date of the CA certificate which
      issued the certificate that the BasicOCSPResponse is for.

5.  We require that all CAs whose certificates are distributed with our
    software products notify us when the ownership control of the CA’s
    certificate(s) changes, or when ownership control of the CA’s operations
    changes. To notify us, send email
    to [certificates@mozilla.org](mailto:certificates@mozilla.org).

7.  A failure to provide notifications or updates in the CCADB or
    as otherwise required in a timely manner shall be grounds for
    disabling a CA’s root certificates or removing them from Mozilla
    products. For this policy and the CCADB policies, "a timely manner" means
    within 30 days of when the appropriate data or documentation becomes
    available to the CA.

8.  We consider the following algorithms and key sizes to be acceptable in
    root certificates in our root program, and in any certificate which
    chains up to them:

    - RSA keys whose modulus size in bits is divisible by 8, and is at
    least 2048.
    - Digest algorithms: SHA-256, SHA-384, or SHA-512.
    - ECDSA keys using one of the following curve-hash pairs:
      * P‐256 with SHA-256
      * P‐384 with SHA-384

9.  We expect CAs to maintain current best practices to prevent
    algorithm attacks against certificates. As such, the following steps
    will be taken:
    -   software published by Mozilla will return
        an error when a certificate with an MD2, MD4 or MD5-based signature is used;
    -   software published by Mozilla will return an error when the
        SSL/TLS certificate has an RSA key size smaller than 2048 bits; and
    -   all new certificates must have a serial number greater than zero
        (0) containing at least 64 bits of output from a CSPRNG.

10. Changes may be made to root certificates that are included in
    Mozilla products as follows:
    -   root changes that are motivated by a serious security concern
        such as a major root compromise should be treated as a
        security-sensitive bug, and the [Mozilla Policy for Handling Security
        Bugs](https://www.mozilla.org/about/governance/policies/security-group/bugs/)
        should be followed;
    -   enabling a trust bit in a root certificate that is currently
        included, may only be done after careful consideration of the
        CA’s current policies, practices, and audits, according to the
        [Inclusion Section of the Mozilla CA Certificate Policy](#inclusion),
        and may be requested by a representative of the CA or a
        representative of Mozilla by submitting a bug report into the
        mozilla.org Bugzilla system, as described in Mozilla’s wiki
        page, [Applying for root inclusion in Mozilla
        products](https://wiki.mozilla.org/CA:How_to_apply#Enable_Additional_Trust_Bits_for_an_included_root);
    -   enabling EV in a root certificate that is currently included,
        may only be done after careful consideration of the CA’s current
        policies, practices, and audits, according to the [Inclusion
        Section of the Mozilla CA Certificate
        Policy](#inclusion),
        and may be requested by a representative of the CA or a
        representative of Mozilla by submitting a bug report into the
        mozilla.org Bugzilla system, as described in Mozilla’s wiki
        page, [Applying for root inclusion in Mozilla
        products](https://wiki.mozilla.org/CA:How_to_apply#Enable_Additional_Trust_Bits_for_an_included_root);
    -   disabling a root is the act of turning off one or more of the
        trust bits (Websites, Email), and may be
        requested by a representative of the CA or a representative of
        Mozilla by submitting a bug report into the mozilla.org Bugzilla
        system, as described in the [Root Change
        Process](https://wiki.mozilla.org/CA:Root_Change_Process);
    -   a representative of the CA or a representative of Mozilla may
        request that a root certificate be removed by submitting a bug
        report into the mozilla.org Bugzilla system, as described in the
        [Root Change
        Process](https://wiki.mozilla.org/CA:Root_Change_Process).


## Enforcing the Mozilla CA Certificate Policy ##

This section of the Mozilla CA Certificate Policy
describes the steps that Mozilla may take in order to enforce this
policy. This includes evaluation of security concerns, and removing or
disabling a root certificate.

This is the official Mozilla policy for enforcing the Mozilla CA
Certificate Policy:

1.  When a serious security concern is noticed, such as a major root
    compromise, it should be treated as a security-sensitive bug, and
    the [Mozilla Policy for Handling Security
    Bugs](https://www.mozilla.org/about/governance/policies/security-group/bugs/) should
    be followed.

2.  Mozilla may, at its sole discretion, disable (partially or fully) or
    remove a certificate at any time and for any reason. Mozilla will
    disable or remove a certificate if the CA demonstrates ongoing or
    egregious practices that do not maintain the level of service that
    was established in the [Inclusion Section of the Mozilla CA
    Certificate Policy](#inclusion)
    or that do not comply with the requirements of the [Maintenance
    Section of the Mozilla CA Certificate Policy](#maintenance).

3.  Mozilla will take any steps we deem appropriate to protect our users
    if we learn that a CA has knowingly or intentionally mis-issued one
    or more certificates. This may include, but is not limited to
    disablement (partially or fully) or removal of all of the CA’s
    certificates from Mozilla’s products. A certificate that includes
    domain names that have not been verified according to section 3.2.2.4 of the
    [CA/Browser Forum’s Baseline
    Requirements](https://cabforum.org/baseline-requirements-documents/) is
    considered to
    be mis-issued. A certificate that is intended to be used only as an
    end entity certificate but includes a keyUsage extension with values
    keyCertSign and/or cRLSign or a basicConstraints extension with the
    cA field set to true is considered to be mis-issued.

4.  A certificate is disabled by turning off one or more of the
    trust bits (Websites, Email). Disablement or removal
    of a certificate may be initiated by submitting a bug report to the
    mozilla.org Bugzilla system, as described in the [Root Change
    Process](https://wiki.mozilla.org/CA:Root_Change_Process) or the
    [Mozilla Policy for Handling Security
    Bugs](https://www.mozilla.org/about/governance/policies/security-group/bugs/).

5.  If Mozilla disables or removes a CA’s certificate(s) from Mozilla’s
    products based on a CA’s actions (or failure to act) that are
    contrary to the Mozilla CA Certificate Policy,
    Mozilla shall publicize that fact in newsgroups on the
    news.mozilla.org server, on Web pages in the www.mozilla.org and
    www.mozilla.com domains, in news releases sent to organizations
    specializing in computer and Internet news, or as an alert to the
    US-CERT organization of the U.S. Department of Homeland Security.

-----

Any copyright in this document is
[dedicated to the Public Domain](http://creativecommons.org/publicdomain/zero/1.0/).

[ETSI-101-456]: http://www.etsi.org/deliver/etsi_ts/101400_101499/101456/01.04.03_60/ts_101456v010403p.pdf
[ETSI-102-042]: http://www.etsi.org/deliver/etsi_ts/102000_102099/102042/02.03.01_60/ts_102042v020301p.pdf
[ETSI-319-411-1]: http://www.etsi.org/deliver/etsi_en/319400_319499/31941101/01.01.01_60/en_31941101v010101p.pdf
[ETSI-319-411-2]: http://www.etsi.org/deliver/etsi_en/319400_319499/31941102/02.01.01_60/en_31941102v020101p.pdf
[WebTrust-2.0]: http://www.webtrust.org/homepage-documents/item54279.pdf
[WebTrust-BRs]: http://www.webtrust.org/homepage-documents/item79806.pdf
[WebTrust-For-CAs]: http://www.webtrust.org/homepage-documents/item27839.aspx
[WebTrust-EV]: http://www.webtrust.org/homepage-documents/item79807.pdf
