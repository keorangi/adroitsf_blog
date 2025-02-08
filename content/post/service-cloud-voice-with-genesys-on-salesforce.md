---
title:       'Service Cloud Voice With Genesys on Salesforce'
subtitle:    "Implementation notes from implementing the Genesys CX Cloud for contact centre Voice Cloud integration"
description: "Setup Service Cloud Voice with Partner Telephony"
date:        '2025-02-08T15:43:06+13:00'
author: AdroitSF
image:       "/img/service-voice-cloud/bg.jpg"
published: true
tags:        ["Service Cloud", "Genesys", "Voice", "Omni Channel"]
URL: "/2025/feb/07/service-voice-cloud"
categories:  ["Service Cloud" ]
---

#### tl;dr
These are the notes from a recent implementation of Service Cloud Voice.  
Integrating Genesys telephony to an org implementing Industries Finance Cloud.  

The implementation used Genesys Cloud CX to integrate telephony to Salesforce
via Omni Channel  

# Background
The client is an insurance firm with an ongoing implementation of Industries
Finance Cloud.  
The client is familiar with Genesys and has been utilizing them for standalone
telephony.  
Genesys Cloud CX installation is infact a base installation from where four
other apps can be installed. The apps provide among others an ability to
generate a partner telephony contact centre.  
Routing for the voice channel was by Genesys and hence external.

### Key learnings
1. Genesys has the concept of one development org and one production org
2. Genesys is not always opposed to testing on the production org
3. Routing is external and is based on source to queue mapping and queue membership
4. Agents who take calls should thus be configured within Genesys queues

# How may we run a Voice Cloud Implementation Workshop

### Potential Challenges

Implementation teams are brought in to bring thought leadership.  
Installing the AppExchange product by itself does not need implementation teams.  
One challenge thus is to stand apart and to be seen as bringing in value that
the internal teams are not able to bring.  

# How may we approach Voice Cloud Implementation development?

# How may we approach Voice Cloud Implementation deployment?

# Other technical details

### How does omni channel work?


### How do we address routing?


### How does omni channel supervisor work?

##### Record access considerations

### What automations may be consider in the first phase implementation?

### Configuring Genesys CX Cloud

#### Connected app created for Genesys CX Cloud

##### Mapping fields in Genesys CX Cloud
*Standard fields cannot be custom mapped; not all standard fields are mapped*

### Concept of Sub Status on Genesys Cloud

# Reporting and Analytics

# Documenting the implementation

### High Level Design Document
There was an expectation to document fall back flows where telephony or the
softphone fails to work.  

##### Automation documentation
While the low code tools (Flows) allow for self documentation, the better
approach would be to articulate each of the flows and the decision making that
is done within these flows.

##### Data Model/Data Dictionary


### App Installation Guide


### Release Document


### Reference Document
Common gotchas, how do we troubleshoot

### User onboarding Document
Onboarding has to be a collaborative process. There is the Genesys portion of
the onboarding and further the Salesforce side of the onboarding. The business
would be keen to have a combined document. 

# Gotchas
1. Voice Cloud usually is not a stand alone implementation. This is added to
   existing users in the system. Major consideration would be whether the users
have access to all the objects and fields that are to be used in automations
asked for. If they don't, make sure this is confirmed and acknowledged by the
business before custom access is setup for Voice. In a recent case, the users
needed access to Insurance Policy. However, since this is a financial cloud
object, access meant the user should have licenses to view the object.

2. Voice Call Object does not have object or field access specified in
   permissionsets or profiles. All you would see is the tab access on
permissionsets. **Side Note** : If we edit the permissionset xml, it accepts the
object and field permissions, though I dont think it makes a difference.  

3. Service Presence cannot be deleted from the UI once created.  

4. Reports that use the Service Presence status would fail unless the viewing
   user has developer name view access. This was observed on a dashboard.
_unsure as to behaviour when reviewing the report_

5. Standard Sample permissionsets provide voice cloud license  

6. Users need to be added to the partner contact centre to be able to access
   phone calls. The user will show up only once the license is added.

7. 
# Patterns explored for this implementation

1. Validations on Voice call - achieved with flow automation to update closure
   status of the Voice Call. Less disruptive in flight, but shows up on Omni
channel until its closed, in accordance with the validation. Additionally, it
shows up on the Omni Supervisor view, so managers would have visibility about
this.

### Normalized phone numbers

### Before Voice Call trigger

### Match Account Screen Flow

### SOSL Search for records

# How may be extend Voice Cloud Implementation Enhancements?


# References

