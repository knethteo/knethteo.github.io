---
layout: post
title:  "The Consequences and Side-Effects of Checking “Account is Sensitive and Cannot be Delegated” "
date:   2020-07-21 15:10:00 +0800
categories: sharing
comments: true
---
## The Introduction
Kerberos Delegation is the feature that allows an application (service account, or computer) to act on behalf of another user. [More information is provided by Microsoft][sensitive-cannotdelegate-Link].To protect sensitive accounts, such as Domain Admins, Enterprise Admins, etc., Active Directory administrators can selectively set an account to “Account is sensitive and cannot be delegated” (as you can see in Figure 1),  this will prevent a user’s credentials (TGT) from being reused. 

![image-title-here](https://kennethteo.blob.core.windows.net/blogimages/account_is_sen_cant_be_delegated.png){:class="img-responsive"}
Figure 1. Checkbox to tag an account to be sensitive and cannot be delegated


The idea of this setting is to limit scope of attack, particularly those categorized as privilege of escalation. Without this, sensitive credential may be harvested from compromised servers/service accounts where Kerberos delegation is enabled.

With this setup, attacks such as credential harvesting, the [“printer bug”](https://adsecurity.org/?p=4056) and others can be partially mitigated by simply switching on “Account is sensitive and cannot be delegated”.

## The Problem
However, if this setting can mitigate attacks, why aren't it widely adopted, and turned on by default?
The reality, there may be instances where users need this for certain operations and depending on your organization this may or may not be an essential setting. However, security experts can agree on one thing, it is dangerous to leave this unchecked for privileged accounts and "shadow" privileged account.

It then begs the question, what are the possible side-effects of setting the “Account is sensitive and cannot be delegated” flag.

Indeed, setting this flag may prevent some day-to-day operations that may require Kerberos delegation. One such example is Live Migration for Hyper-V Virtual Machines, which you can read more at [Live Migration via Constrained Delegation](https://docs.microsoft.com/en-us/virtualization/community/team-blog/2017/20170201-live-migration-via-constrained-delegation-with-kerberos-in-windows-server-2016).

<!--more-->

## The Solution
This flag is used primarily to protect privileged accounts on the assumption that these privileged accounts are also not being used as a day-to-day account as well (which they are not supposed to anyway).

Even though there may be some unexpected consequences from turning this setting on, I’d still strongly recommend Active Directory administrators to continuing enforce “Account is sensitive and cannot be delegated” on all privileged account and only grant exception on case-by-case basis (such as for Hyper-V Manager role and other privileged role) as required. This will promote the principal of least privilege, which is always the best configuration. 

## Appendix
none


[sensitive-cannotdelegate-Link]: https://docs.microsoft.com/en-us/archive/blogs/poshchap/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts "account is sensitive and cannot be delegated"
[screenshot-accountProp]: https://kennethteo.blob.core.windows.net/blogimages/account_is_sen_cant_be_delegated.png
