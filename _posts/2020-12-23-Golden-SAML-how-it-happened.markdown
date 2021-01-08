---
layout: post
title:  "Golden SAML - How It Happened and What We Can Do About It"
date:   2020-12-23 9:27:00 +0800
categories: learning
comments: true
---

The recent cyber attack involving SolarWinds Orion revealed the weakness in the design of federated identity. Particluarly what is known as Golden SAML.

<!--more-->

## Background
1. Golden SAML exploits the weakness in dseign of the master key to sign the SAML token. This key is usually held in the IDP VM (on-prem)
2. It's a post exploitation attack as confirmed here "Microsoft doesn’t consider this a vulnerability because in order to carry out a Golden SAML attack an adversary must already of compromised a company’s network and have domain admin access." from https://threatpost.com/saml-post-intrusion-attack-mirrors-golden-ticket/128993/
3. This attack is a post exploitation attack and is too late to be dealt with. See below for a sample of the AD misconfigurations attack pathways that allow the Golden SAML Attack to actually occur in the first place
4. It's crucial to remove proactively detect and timely remove configurations that allow Golden SAML attack.

## Proactive prevention of Golden SAML Attack
Consider to review the guidance from [CISA](https://us-cert.cisa.gov/ncas/alerts/aa20-352a) and [NSA](https://media.defense.gov/2020/Dec/17/2002554125/-1/-1/0/AUTHENTICATION_MECHANISMS_CSA_U_OO_198854_20.PDF). These include the following:

1. Validate the ownership of IDP (ADFS) server that may have been changed unknowingly
2. Validate and verify the OU of IDP (ADFS) having un-sanctioned ACEs entries
3. Validate ACEs permission allowing malicious user have access to sensitive info of IDP server (ADFS)
4. Back door through GPO applied on IDS servers (ADFS) – Alsid detect this in real time out of the box at the AD object level in the AD data base
5. Scrutinize the deployment and configuration of Azure AD Connect
6. Rotate the SAML/SSO password - as we regularly do with KRBTGT to prevent Golden Ticket
5. Other type of AD attack chain that may involve your SAML signing server (ADFS, for example)

This proactive attack prevention is precisely what Alsid for AD is for.

## Detection of Golden SAML Attack:
 
1. Detecting the Golden SAML attack as and after it happens is pointless 
2. Saying that, as the Golden SAML attack will be performed on an ADFS server (not AD) Alsid can monitor changes made on ADFS server through the Alsid Trailflow and SIEM to be able to detect it when it happens in real time
3. In addition, Alsid can add the OU containing the IDP such as ADFS into special monitoring group (as if it is an Domain Controller) so we can monitor who has permissions over this ADFS server and provide deeper level of security insights.
4. To confirm, as the Golden SAML Attack is a post domain compromise attack, this (domain compromise) is precisely what Alsid is trying to prevent through our proactive continuous detecting and remediation of the AD misconfigurations attack pathways that allow it to happen.

As attacks are getting more freqeuent, it is always better to employ prevention strategy than (trying to) cure!