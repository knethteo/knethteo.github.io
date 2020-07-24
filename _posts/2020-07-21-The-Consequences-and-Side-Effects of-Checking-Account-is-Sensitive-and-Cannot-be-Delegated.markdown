---
layout: post
title:  "The Consequences and Side-Effects of Checking “Account is Sensitive and Cannot be Delegated” "
date:   2020-07-21 15:10:00 +0800
categories: sharing
comments: true
---
## The Introduction
Kerberos Delegation is the feature that allows an application (service account, or computer) to act on behalf of another user. [More information is provided by Microsoft][sensitive-cannotdelegate-Link].To protect sensitive accounts, such as Domain Admins, Enterprise Admins, etc., Active Directory administrators can selectively set an account to “Account is sensitive and cannot be delegated” (as you can see in Figure 1),  this will prevent a user’s credentials (TGT) from being reused. 


## The Problem
Azure supports [tagging][Tagging-Link] of resources for the longest time; However, one of the complaints I have with this feature is: there is no easy way to separate them into their own column when exporting the usage details (see exhibit 1).

Tagging can be done at resource group or individual resource. The purpose of tags is loosely defined. Most often than not, an organization uses it to tag for cross-charge purposes.

![itemized usage][itemizedUsage-Link]
Notice that the Tags column is very messy/unorganized when you have multiple tags.

<!--more-->

##The Solution
If you have worked with JSON on a project or dueled with it extensively, you may have noticed the Tags column in the screenshot above is actually in JSON format.

Enter the Powerful _Power BI Desktop_...

I am not going to write a long-a** essay to tell you what's [Power BI][PowerBI-Link], you will be able to find online articles written by experts with better ability to explain it than I am. I'll leave you with this though: Power BI is an online service that transforms your data into rich visuals [blah blah blah].

Power BI also has a **free** for download desktop client, go ahead download and install it, I'll wait.

1. Launch Power BI Desktop
2. Import the usage data, either download from account.windowsazure.com or ea.azure.com and click “edit” in the import wizard (and since I am such a good person, I have attached a sample usage data at the end of this guide for your convenience) ![Imported to PowerBI][powerbi-tagscolumnclicked-Link]
⋅⋅1. Select _Tages column_
⋅⋅2. Click on _Transform_
⋅⋅3. Click on _Parse_
3. Once you have parsed it, click on the small expand icon at the corner in the top cell, like following 
![Expand][powerbi-tagsexpand-Link] expand it. ![Expanded][powerbi-tagsexpanded-Link]
4. That's it!

If you have any questions, feel free to comment below.

## Appendix
* The sample usage details file: https://1drv.ms/x/s!AthVHX51HSt1n9UXaFIiywn2SDtsvw


[sensitive-cannotdelegate-Link]: https://docs.microsoft.com/en-us/archive/blogs/poshchap/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts "account is sensitive and cannot be delegated"
