# Mozilla PKI Policy

This repository contains documents relating to Mozilla's PKI policies, such as
its [certificate root program](https://wiki.mozilla.org/CA). The
owner of these documents is the Module Owner of the "[Mozilla CA Certificate
Policy](https://wiki.mozilla.org/Modules/Activities#Mozilla_CA_Certificate_Policy)"
module. Mozilla's PKI policies can be discussed in https://groups.google.com/a/mozilla.org/g/dev-security-policy.
Archives of previous discussions are in https://www.mozilla.org/about/forums/#dev-security-policy.

## Root Program ##

You can find out [how to apply to be included in Mozilla's root
program](https://wiki.mozilla.org/CA/Application_Process). There is also a
[list of included roots](https://wiki.mozilla.org/CA/Included_Certificates).

### Using Mozilla's Root Store ###

The decisions Mozilla makes with regards to the inclusion or exclusion of CA
certificates in its root store are directly tied to the capabilities and
behaviours of the software Mozilla distributes. Sometimes, a security change
is made wholly or partly in the software instead of the root store. Further,
Mozilla does not promise to take into account the needs of other users of its
root store when making such decisions.

Therefore, anyone considering bundling [Mozilla's root store](https://wiki.mozilla.org/CA/Included_Certificates) with other
software needs to be aware of the issues surrounding providing a root store,
and committed to making sure that they maintain security for their users by
carefully observing Mozilla's actions and taking appropriate steps of their
own. On a best-efforts basis, Mozilla maintains a
[list of additional things](https://wiki.mozilla.org/CA/Additional_Trust_Changes)
users of our store might need to consider. 

[Data Usage Terms](https://www.ccadb.org/rootstores/usage#ccadb-data-usage-terms)
