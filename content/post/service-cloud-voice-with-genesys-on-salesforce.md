---
title:       'Service Cloud Voice With Genesys on Salesforce: An Implementation Guide'
subtitle:    "Implementation notes from integrating Genesys CX Cloud for contact centre Voice Cloud integration with Salesforce"
description: "Comprehensive guide to setting up Service Cloud Voice with Genesys Partner Telephony: implementation strategies, technical setup, and common challenges to avoid."
date:        '2025-02-08T15:43:06+13:00'
author: AdroitSF
image:       "/img/service-voice-cloud/bg.jpg"
published: true
tags:        ["Service Cloud", "Genesys", "Voice", "Omni Channel", "Contact Center Integration", "Telephony Integration"]
URL: "/2025/feb/07/service-voice-cloud"
categories:  ["Epic" ]
---

**Please note this document is work in progress; am updating as and when I get time**

#### tl;dr
These are the notes from a recent implementation of Service Cloud Voice.  
Integrating Genesys telephony to an org implementing Industries Finance Cloud.  
The implementation used Genesys Cloud CX to integrate telephony to Salesforce via Omni Channel.

## Introduction

Integrating a telephony system with Salesforce's Service Cloud can significantly improve the agent experience and customer service quality. This article documents our experience implementing Genesys Cloud CX with Salesforce Service Cloud Voice for an insurance client using Industries Finance Cloud. By following this implementation guide, Salesforce consultants can learn how to approach a Genesys integration project, understand key technical considerations, and avoid common pitfalls that might impact deployment. The focus is on practical, field-tested techniques that deliver value quickly without extensive customization.

# Genesys and Salesforce Integration Background

The client is an insurance firm with an ongoing implementation of Industries Finance Cloud.  
The client is familiar with Genesys and has been utilizing them for standalone telephony.  
[Genesys Cloud CX](https://appexchange.salesforce.com/appxListingDetail?listingId=7f59a36f-86c0-4cac-b8af-2c1722ede4d1) installation is in fact a base installation from where four other apps can be installed. The apps provide among others an ability to generate a partner telephony contact centre.  
Routing for the voice channel was by Genesys and hence external.

### Key Genesys-Salesforce Integration Learnings
1. Genesys has the concept of one development org and one production org
2. Genesys is not always opposed to testing on the production org
3. Routing is external and is based on source to queue mapping and queue membership
4. Agents who take calls should thus be configured within Genesys queues to be able to receive the calls

# Service Cloud Voice Implementation Approach

## Voice Cloud Implementation Workshop Strategy

A broad alignment was made with the client on how the team would want to implement the integration. Early on it was called out that the purpose of the project would be to implement the integration without extensive customisation. This was in alignment with what the business thought they wanted when the SOW was signed.

The routing process was external to Salesforce in this example. Since the product softphone and omni-channel were new to the client, the approach taken was a show and collaborate approach.  

This meant that as consultants, we needed to have a view of what the implementation would look like, so there is a way to show what the business might be interested in viewing. This meant an understanding of the motivations of why the project is being implemented would inform on what could be shown. In this particular case the motivation was that the systems were disconnected. The agents were to look at multiple systems to be able to support requests.  

It becomes very important to know how the business works, the process they follow and the 'value chain' for everything that the team does. It is also very important to make sure the business understands we provide better time to value on the project by focusing on the challenges that would give us the maximum upside to the effort. The 80-20 rule would be how we could articulate this.

### Potential Challenges in Genesys-Salesforce Integration

1. Implementation teams are brought in to bring thought leadership.  
Installing the AppExchange product by itself does not need implementation teams.  
One challenge thus is to stand apart and to be seen as bringing in value that the internal teams are not able to bring.  

2. Copy the current syndrome.  
The biggest challenge is users either have a very good sense of what they do not like on the current system or a strong sense of what the like in the current system. There would be resistance to change, mostly driven by not understanding new ways of doing things. If the resistance is due to the lack of feature parity, there should be an analysis on offering alternatives.

## Salesforce-Genesys Development Strategy

### Implementation Context

The client would usually have a reference telephony system that they compare our work with.  
What I have found most beneficial as a start is to understand the scope and workflows of the business. 
Based on which a show and tell approach usually works well.  

The downside to this approach is when we have multiple stakeholders, there is bound to be a certain amount of rework as the team reconciles with how things are done.  
Understanding the workflows would help in articulating why a certain approach is best and also helps guide the development.  
Voice channel also would be an addition on a larger service implementation or even a case management implementation.

### Defining Target User Scope for Voice Integration

Determine from the client the user groups or personas that would be part of this implementation.
Typically the personas would be:
1. Call taking agent
2. Team Manager
3. Workforce Management Team
4. Salesforce admins

Team Managers would have agents reporting into them.
Workforce Management and Salesforce Admins would have responsibility across teams.  

Determine from the client whether these users have a certain Salesforce app that they operate in.  
It is best to take over an existing app when just implementing voice.

Why?  
1. We want to ringfence the area in which we are responsible. Business users are usually very sensitive to UI elements like layouts etc. It's best to reduce the surface area we are responsible for.
2. Voice is just adding one more channel of interaction. We do not want to be on the hook for implementing an entire support strategy. This is primarily so we are able to bring closure to specific features we are responsible for.  
3. Using an existing app makes change management slightly more easier to deal with.

# Genesys CX Cloud Technical Implementation in Salesforce

## Configuring Genesys CX Cloud for Salesforce Integration

### Connected app configuration for Genesys CX Cloud

### Mapping fields between Genesys CX Cloud and Salesforce
*Standard fields cannot be custom mapped; not all standard fields are mapped*

### Understanding Sub Status Functionality on Genesys Cloud

## Salesforce Omni Channel Integration with Genesys

### How Omni Channel works with external telephony

### Addressing routing challenges with Genesys

### Configuring Omni Channel supervisor for voice monitoring

#### Record access considerations for voice calls

### First-phase automation recommendations for voice integration

# Genesys-Salesforce Voice Integration Deployment Strategy

# Reporting and Analytics for Voice Channel Performance

# Voice Cloud Implementation Documentation Requirements

## High Level Design Document for Voice Integration
There was an expectation to document fall back flows where telephony or the softphone fails to work.  

### Automation documentation for voice flows
While the low code tools (Flows) allow for self documentation, the better approach would be to articulate each of the flows and the decision making that is done within these flows.

### Voice Integration Data Model/Data Dictionary

## Genesys CX Cloud App Installation Guide
When installing the app on a sandbox, the behaviour of AppExchange has changed. From what was observed, the installation to a sandbox can only be done using the 'Try It Free' link. In earlier instances of AppExchange installation, using the production credentials allowed for the user to select the sandbox name from the list. This was not available at this time; though not much time was spent in figuring out why that is the case.

## Voice Integration Release Document

## Voice Troubleshooting Reference Document
Common gotchas, how do we troubleshoot

## Genesys-Salesforce User Onboarding Document
Onboarding has to be a collaborative process. There is the Genesys portion of the onboarding and further the Salesforce side of the onboarding. The business would be keen to have a combined document.

# Service Cloud Voice Implementation Patterns

## Validations on Voice Call Object
Achieved with flow automation to update closure status of the Voice Call. Less disruptive in flight, but shows up on Omni channel until it's closed, in accordance with the validation. Additionally, it shows up on the Omni Supervisor view, so managers would have visibility about this.

## Normalized Phone Number Handling in Genesys-Salesforce Integration

## Before Voice Call Trigger Implementation

## Match Account Screen Flow for Caller Identification

## SOSL Search for Voice-Related Records

# Common Gotchas in Genesys-Salesforce Integration

1. **Installing user with Voice Cloud License**  
If there is metadata that references Voice related objects (eg: [Voice Call](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_voicecall.htm)) Salesforce expects the running user to have the Voice Cloud license. It is easy to get caught out since some of the users would be deployment users that are not easily seen or available.

2. **License requirements for Voice Cloud integration**  
Voice Cloud usually is not a stand alone implementation. This is added to existing users in the system. Major consideration would be whether the users have access to all the objects and fields that are to be used in automations asked for. If they don't, make sure this is confirmed and acknowledged by the business before custom access is setup for Voice. In a recent case, the users needed access to Insurance Policy. However, since this is a financial cloud object, access meant the user should have licenses to view the object.

3. **Voice Call Object permissions in Salesforce**  
Voice Call Object does not have object or field access specified in permissionsets or profiles. All you would see is the tab access on permissionsets. **Side Note**: If we edit the permissionset xml, it accepts the object and field permissions, though I don't think it makes a difference.  

4. **Service Presence Status limitations in Omni Channel**  
[Service Presence Status](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_servicepresencestatus.htm) cannot be deleted from the UI once created.  

5. **Report access issues with Service Presence**  
Reports that use the Service Presence status would fail unless the viewing user has developer name view access. This was observed on a dashboard. _unsure as to behaviour when reviewing the report_

6. **Standard Sample permissionsets for Voice**  
These provide voice cloud license.

7. **User configuration in partner contact center**  
Users need to be added to the partner contact centre to be able to access phone calls. The user will show up only once the license is added.

8. **Phone Number Data Format Issues**  
Much of the value that the integration brings would be via the more immersive context available to the agent immediately as a customer with a known phone number lands on the queue. Since Genesys provides the phone number in the [E164 format](https://help.mypurecloud.com/glossary/e-164/), it was called out early that we would search for the match with this number and would not transform this number for searching. **Note** E164 specifies that the number consists of +(plus) and numbers. It does not specify the count of numbers. 
It was observed that Genesys also formats the number with spaces. This makes it difficult to use the number directly on an SOQL query. A callout that the number would be searched for as is, would be an appropriate callout when the scope does not cover data. Any data, transformation aspects would be best addressed as a separate project outside of the Voice scope.

# Future Service Cloud Voice Enhancement Opportunities

# Frequently Asked Questions about Genesys-Salesforce Integration

## How does Genesys call routing work with Salesforce Omni-Channel?
Routing for voice calls is handled by Genesys externally based on source-to-queue mapping and queue membership. Agents must be configured within the appropriate Genesys queues to receive calls, which then appear in their Salesforce Omni-Channel widget.

## What licenses are required for Service Cloud Voice with Genesys?
Users need both the Voice Cloud license in Salesforce and proper queue membership in Genesys. Additionally, if automations involve access to specific objects (like Financial Cloud objects), those license requirements must also be considered.

## How does caller identification work between Genesys and Salesforce?
Genesys provides caller phone numbers in E164 format, which can be used to search for matching contacts or accounts in Salesforce. However, formatting differences may require normalization for reliable matching.

## Can we customize the Genesys softphone interface in Salesforce?
Limited customization is possible. The base installation provides core functionality, while advanced customizations should be approached carefully to maintain supportability.

# Conclusion

Implementing Service Cloud Voice with Genesys provides significant benefits for contact centers using Salesforce, particularly in bringing context and customer information directly to agents during calls. The key to success lies in understanding both systems' capabilities and limitations, focusing on targeted user personas, and addressing potential challenges proactively. This implementation guide highlights practical approaches that prioritize business value while managing technical complexity.

The integration between Genesys and Salesforce continues to evolve, with opportunities for enhancement after the base implementation is complete. By focusing on core functionality first and following the patterns outlined in this guide, implementation teams can deliver a stable, valuable solution that improves both the agent and customer experience.

# References
