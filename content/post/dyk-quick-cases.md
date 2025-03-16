---
title:       'Salesforce Service Cloud : How do I create Cases quick?'
subtitle:    "Creating Cases provide visibility over customer interactions; Creating Cases does not have to increase average handling time of agents."
description: "customers usually push back against Cases, indicating that creating a case increases their aht. Creating cases using quick action allows us to create cases quickly on the call without creating custom cases."
date:        '2025-03-15T15:43:06+13:00'
author: AdroitSF
published: true
tags:        ["Service Cloud", "Case Management", "AHT", "Quick Action"]
URL: "/2025/mar/15/case-creation-using-quick-action"
categories:  ["Did You Know?" ]
---

# How do you create a case quickly against a account?
Create a quick action on the Account record.  
Choose create record option, and choose Case.  
Specify a record type, do not select confirmation if speed is a focus.  
Also consider prepopulating fields, even when its available on the layout, so users can override if needed.  
When using industries, consider creating the action on an action deployment. Consider creating specific actions if required.  

# Why does this work?
Quick Actions bypass the UI level field requirements, avoiding many selections and reducing clicks.  
Quick Actions provide an opportunity to prepopulate fields.  
There is an opportunity to have custom actions for common criteria, improving response times.  
Quick actions do not get routed using assignment rules, so the case remains with the agent to update and progress.  

# What else should be considered?
Always attempt to create records automatically. Eg. If possible when recieving a voice call or a chat interaction, cases can be created automatically.  
If the business requirement is not to create a case record, we could make it easier to find case records that can be updated by the user.  
