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
[Genesys Cloud
CX](https://appexchange.salesforce.com/appxListingDetail?listingId=7f59a36f-86c0-4cac-b8af-2c1722ede4d1)
 installation is infact a base installation from where four
other apps can be installed. The apps provide among others an ability to
generate a partner telephony contact centre.  
Routing for the voice channel was by Genesys and hence external.

### Key learnings
1. Genesys has the concept of one development org and one production org
2. Genesys is not always opposed to testing on the production org
3. Routing is external and is based on source to queue mapping and queue membership
4. Agents who take calls should thus be configured within Genesys queues to be
   able to receive the calls

# How may we run a Voice Cloud Implementation Workshop
A broad alignment was made with the client on how the team would want to
implement the integration. Early on it was called out that the purpose of the
project would be to implement the integration without extensive customisation.
This was in alignment with what the business thought they wanted when the SOW
was signed.

The routing process was external to Salesforce in this example. Since the
product softphone and omni-channel were new to the client, the approach taken
was a show and collaborate approach.  

This meant that as consultants, we needed to have a view of what the
implementation would look like, so there is a way to show what the business
might be interested in viewing. This meant an understanding of the motivations
of why the project is being implemented would inform on what could be shown. In
this particular case the motivation was that the systems were disconnected. The
agents were to look at multiple systems to be able to support requests.  

It becomes very important to know how the business works, the process they
follow and the 'value chain' for everything that the team does. It is also very
important to make sure the business understands we provide better time to value
on the project by focusing on the challenges that would give us the maximum
upside to the effort. The 80-20 rule would be how we could articulate this. 

### Potential Challenges

1. Implementation teams are brought in to bring thought leadership.  
Installing the AppExchange product by itself does not need implementation teams.  
One challenge thus is to stand apart and to be seen as bringing in value that
the internal teams are not able to bring.  

2. Copy the current syndrome.  
The biggest challenge is users either have a very good sense of what they do not
like on the current system or a strong sense of what the like in the current
system. There would be resistance to change, mostly driven by not understanding
new ways of doing things. If the resistance is due to the lack of feature
parity, there should be an analysis on offering alternatives.

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
When installing the app on a sandbox, the behaviour of AppExchange has changed.
From what was observed, the installation to a sandbox can only be done using the
'Try It Free' link. In earlier instances of AppExchange installation, using the
production credentials allowed for the user to select the sandbox name from the
list. This was not available at this time; though not much time was spent in
figuring out why that is the case.

### Release Document


### Reference Document
Common gotchas, how do we troubleshoot

### User onboarding Document
Onboarding has to be a collaborative process. There is the Genesys portion of
the onboarding and further the Salesforce side of the onboarding. The business
would be keen to have a combined document. 

# Gotchas
1. Installing user with Voice Cloud License  
If there is metadata that references Voice related objects (eg: [Voice
Call](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_voicecall.htm)) 
Salesforce expects the running user to have the Voice Cloud license. It is easy
to get caught out since some of the users would be deployment users that are not
easily seen or available.

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

3. [Service Presence Status](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_servicepresencestatus.htm)
 cannot be deleted from the UI once created.  

4. Reports that use the Service Presence status would fail unless the viewing
   user has developer name view access. This was observed on a dashboard.
_unsure as to behaviour when reviewing the report_

5. Standard Sample permissionsets provide voice cloud license  

6. Users need to be added to the partner contact centre to be able to access
   phone calls. The user will show up only once the license is added.

7. Data Issues - much of the value that the integration brings would be via the
   more immersive context available to the agent immediately as a customer with
a known phone number lands on the queue. Since Genesys provides the phone number
in the [E164 format](https://help.mypurecloud.com/glossary/e-164/), it was
called out early that we would search for the match with this number and would
not transform this number for searching. **Note** E164 specifies that the number
consists of +(plus) and numbers. It does not specify the count of numbers. 
It was observed that Genesys also formats the number with spaces. This makes it
difficult to use the number directly on an SOQL query. A callout that the number
would be searched for as is, would be an appropriate callout when the scope does
not cover data. Any data, transformation aspects would be best addressed as a
separate project outside of the Voice scope.

# Patterns explored for this implementation

### Validations on Voice call
achieved with flow automation to update closure
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

