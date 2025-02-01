+++
title = 'Show me your Identity (Center)'
date = 2025-02-01T16:28:14+01:00
draft = false
tags = [ "AWS", "IAM", "identity center", "cloud", "computing", "security" ]
+++

![Identity Center](/assets/IAM-Identity-center.png)

## Intro

Corporate cloud environments usually consist of multiple accounts. Managing the different users, groups, and access
policies per account can be a complex and daunting process. <abbr title="Identity and Access Management">IAM</abbr>
identity center to the rescue! With IAM identity center we can use <abbr title="Single Sign On">SSO</abbr> effectively
to switch quickly between different <abbr title="Amazon Web Services">AWS</abbr> accounts that we have been given access.

![AWS SSO multiple accounts](/assets/AWS-SSO-multi-account.jpg)

## Managing users and groups

Although we can create users and groups directly in IAM Identity Center and manage them using <abbr title="Infrastructure
as Code">IaC</abbr>, it is more efficient to use an enterprise identity provider (IdP), such as Entra ID, Okta, etc. Using
an IdP, offers the SSO advantage: no need to generate new credentials, the existing credentials used to login to the corporate
account are sufficient.

At Mentech we are using Entra ID, which supports provisioning users and groups to IAM Identity Center. So, the first step is to
define those groups and users and provision them.

![AWS Identity Center provisioned groups](/assets/idc-groups.png)

## Managing account access and permissions

Now that the groups and users are there, it's time to give them the required access to the relevant AWS accounts. That is optimally
done with IaC, and at Mentech we use terraform. The terraform registry has [an identity center
module](https://registry.terraform.io/modules/aws-ia/iam-identity-center/aws/latest), but I prefer using the [official AWS
module](https://github.com/aws-samples/identity-center-with-terraform), currently hosted only on GitHub. The repo contains nice
examples of giving access to accounts and defining permissions, thus I won't repeat that here to keep it short. Leave a comment
below if you need help.

## Caveats

When defining fine-grained permission sets, it is advised to maximise the use of [AWS managed
policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies).
Unfortunately, there is a [hard quota](https://docs.aws.amazon.com/singlesignon/latest/userguide/limits.html#awsaccountlimits) of
20 managed + customer policies per account. For lengthy permission sets that reach this quota, or when there are no suiting managed
policies available (yes, it can happen), the referenced module supports defining an inline policy, as shown below:

```yaml
SampleGroupPermissionSet:
  description: "Permission set of a sample group"
  tags: null
  session_duration: "PT4H"
  inline_policy: "sample-group-perms" # the inline policy is in the file sample-groups-perms.json
  aws_managed_policies:
    - "AmazonEC2ReadOnlyAccess"
    - "AmazonS3ReadOnlyAccess"
  customer_managed_policies: null
  permissions_boundary: null
```
