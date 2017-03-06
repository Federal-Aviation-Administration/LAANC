  ----------------------------------------------------------------------------------- ------------------------------------------
  ![](media/image1.png){width="1.7541666666666667in" height="1.6770833333333333in"}   **\
                                                                                      FAA\
                                                                                      Office of Information Technology (AIT)**
  ----------------------------------------------------------------------------------- ------------------------------------------

REST Service Description Document (RSDD)

for

[[[]{#_Toc476142642 .anchor}]{#_Toc475620615 .anchor}]{#_Toc475620548
.anchor}Low Altitude Authorization and Notification Capability (LAANC)

[[[]{#_Toc476142643 .anchor}]{#_Toc475620616 .anchor}]{#_Toc475620549
.anchor}and Third Party Providers

**Version 1.0**

**3/1/2017**

REST Service Description Document

LAANC

Approval Signatures

  Name   Organization   Signature   Date Signed
  ------ -------------- ----------- -------------
                                    
                                    
                                    
                                    

REST Service Description Document

LAANC

Revision Record

  -------------------------------------------------------------------------------------------------------------
  Revision\   Description                                                          Revision Date   Entered By
  Letter                                                                                           
  ----------- -------------------------------------------------------------------- --------------- ------------
  .1          Initial version                                                      1/27/2017       W.Larson

  .2          FIXM added                                                           2/23/2017       A.Bacarra

  .3          Webhooks added                                                       2/27/2017       A.Bacarra

  .4          Removed data model and data dictionary (will be in separate files)   3/1/2017        A.Bacarra
  -------------------------------------------------------------------------------------------------------------

Table of Contents

**Low Altitude Authorization and Notification Capability (LAANC)** i

**and Third Party Providers** i

1 [Scope](#scope)

1.1 [Background](#background)

2 [Applicable Documents](#applicable-documents)

2.1 [Government Documents](#government-documents)

2.2 [Non-Government Standards and Other Publications](#non-government-standards-and-other-publications)

3 [Definitions](#definitions)

3.1 [Terms and Definitions](#terms-and-definitions)

3.2 [Acronyms](#acronyms)

4 [Service Properties and Capabilities](#service-properties-and-capabilities)

4.1 [Service Profile](#service-profile)

4.1.1 [Service Properties](#service-properties)

4.1.2 [Service Provider](#service-provider)

4.1.2.1 [Service Points of Contact](#service-points-of-contact)

4.1.3 [Service Consumers](#service-consumers)

4.1.4 [Service Functionality](#service-functionality)

4.1.5 [Service Security](#service-security)

4.1.6 [API Protocol and Webhooks](#api-protocol-and-webhooks)

4.1.6.1 [API Protocol](#api-protocol)

4.1.6.2 [Webhooks](#webhooks)

4.1.7 [Message Queuing Protocol](#message-queuing-protocol)

4.1.8 [Message Format](#message-format)

4.1.8.1 [UASs in FIXM](#uass-in-fixm)

4.1.8.1.1 [Data already covered in FIXM](#data-already-covered-in-fixm)

4.1.8.1.1.1 [Operator contact information](#operator-contact-information)

4.1.8.1.1.2 [Flight plan](#flight-plan)

4.1.8.1.1.2.1 [Lat Lon](#lat-lon)

4.1.8.1.1.2.2 [Time](#time)

4.1.8.1.1.2.3 [Altitude](#altitude)

4.1.8.1.1.2.4 [Proposal Submission Date](#proposal-submission-date)

4.1.8.1.1.2.5 [Proposal FAA response time](#proposal-faa-response-time)

4.1.8.1.1.2.6 [Closest Airport](#closest-airport)

4.1.8.1.1.2.7 [Flight Plan Version](#flight-plan-version)

4.1.8.1.1.2.8 [Proposed Speed](#proposed-speed)

4.1.8.1.1.3 [ATC Authorization](#atc-authorization)

4.1.8.1.1.3.1 [Planning Status](#planning-status)

4.1.8.1.1.3.2 [Operational Acceptability](#operational-acceptability)

4.1.8.1.2 5.2. [Data not yet covered in FIXM](#data-not-yet-covered-in-fixm)

4.1.8.1.2.1 [Potential Extensions to FIXM](#potential-extensions-to-fixm)

4.1.8.1.2.1.1 [Permissions](#permissions)

4.1.8.1.2.1.2 [UAS operator](#uas operator)

4.1.8.1.2.1.3 [AirClass](#airclass)

4.1.8.1.2.1.4 [Flight Radius](#flight radius)

4.1.8.1.2.1.5 [VLOS Indicator](#vlos-indicator)

4.1.8.1.2.1.6 [Operation over people indicator](#operation-over-people-indicator)

4.1.9 [Qualities of Service](#qualities-of-service)

4.2 [Service Interfaces & Data Model](#service-interfaces-&-data-model)

4.2.1 [Resources](#resources)

4.2.2 [Methods](#methods)

4.2.3 [Resource Representations](#resource-representation)

4.2.3.1 [Resource Name](#resource-name)

4.2.4 [Sample Payloads](#sample-payloads)

4.2.4.1 [Sample Payload](#sample-payload)

4.3 [Service Implementation](#service-implementation)

4.3.1 [Endpoints](#endpoints)

4.3.1.1 [Endpoint 1 Name](#endpoint-1-name)

4.3.1.1.1 [Supported Data Formats](#supported-data-formats)

4.3.1.1.2 [Network Address](#network-address)

4.3.1.1.3 [End Point-Specific Qualities of Service](#end-point-specific-qualities-of-service)

5 [Appendix A Example FIXM messages](#appendix-a-example-fixm-messages)

5.1 [A.1 Operator to TPP Proposed Flight Plan](#a1-operator-to-tpp-proposed-flight-plan)

5.2 [A.2 TPP to Operator: Accept/Reject](#a2-tpp-to-operator-accept-reject)

5.3 [A.3 TPP to ATC: Notification](#a3-tpp-to-atc-notification)

5.4 [A.4 TPP to ATC: Authorization Request](#a4-tpp-to-atc-authorization-request)

5.5 [A.5 ATC to TPP: Accept – Authorization Granted](#a5-atc-to-tpp-accept-authorization)

5.6 [A.6 ATC to TPP: Reject with Minor Modifications](#a6-atc-to-tpp-reject-with-minor-modifications)

5.7 [A.7 ATC to TPP: Reject](#a7-atc-to-tpp-reject)

6 [Appendix B Message Collections](#appendix-b-message-collections)

## Scope
=====

This REST Service Description Document (RSDD) provides information to
describe and document the LAANC service, which has been designed using
the Representational State Transfer (REST) architectural style for
services. In this style, requests and responses between clients and
servers focus on the transfer of representations of resources. A
resource can be any entity identifiable by a Uniform Resource Identifier
(URI), about which information can be exchanged. A representation of a
resource is typically a document that captures the current or intended
state of a resource.

This document provides basic information about the service and its
provider, and describes in detail the resources that the service can
access and the RESTful Hypertext Transfer Protocol (HTTP) methods that
the service supports for each resource.

## Background
----------

The Federal Aviation Administration (FAA) has been tasked with
implementing notification and authorization (N&A) processes as defined
in the Federal Aviation Regulations, Parts 101 and 107 respectively.
These new regulations provide the needed rules to govern the use of both
model aircraft and unmanned aircraft system (UAS) flight operations
(unmanned aviation activities) throughout the airspace governed by the
FAA.

The FAA is in the process of determining its approach and business plan
to integrate UAS into the National Airspace System (NAS). As part of
that approach, the FAA is dedicated to ensuring safety requirements are
met for integration of UAS into the NAS, where UAS are able to operate
safely in the same airspace with manned aircraft. To this end, the FAA
must ensure that integrated UAS operations meet appropriate performance
standards and access requirements (e.g., SC-228, Minimum Operational
Performance Standards for Unmanned Aircraft Systems). The FAA seeks to
ensure reduced barriers to access and to avoid monopolization of public
resources. The FAA challenge is to foster equitable access for all users
and providers while ensuring critical air traffic control (ATC)
technical and safety requirements are met for NAS operations. In
addition, FAA seeks to foster a competitive environment for providers of
UAS and related services. As the FAA and industry move toward
integration of all types of UAS into the NAS, two rules have recently
been introduced governing the requirements for small UAS (sUAS), defined
as UAS that weigh less than 55 pounds.

The development of a fully functioning and streamlined, user friendly
N&A process is complex and subject to a variety of inputs and
coordination points across the UAS community landscape. This document
will give stakeholders and leadership the necessary background and
contextual information to understand and provide input on the FAA’s
LAANC demonstration planned in 2017. It is expected that this document
will provide stakeholders an understanding of the FAA’s approach to
working with industry to develop streamlined processes for model
aircraft and UAS stakeholders to comply with the law and conduct
operations safely.

The LAANC Third Party Providers (TPP) will send authorization,
notification, re-consideration requests, re-consideration answers, and
denial records to the FAA for FAA display. The TPP will manage Part 107
operator secondary requests for authorization once automatic denial has
been provided.

## Applicable Documents
====================

The documents or information sources in the following sub-sections are
relevant to this document:

-   Federal Aviation Administration, Advisory Circular: 107-2, Small
    Unmanned Aircraft Systems (sUAS), 21 June 2016

-   Federal Aviation Administration, *“Integration of Unmanned Aircraft
    Systems into the National Airspace System, Concept of Operations
    v2.0”*, September, 2012

-   U.S. Government Publishing Office, Code of Federal Regulations,
    Title 14, Part 107, Small Unmanned Aircraft Systems, Web 29 December
    2016

<!-- -->

-   Airman’s Information Manual (AIM)

## Government Documents
--------------------

-   &lt;SLA document(s) for the Service, when completed&gt;

-   FAA-STD-066, Web Service Taxonomies

## Non-Government Standards and Other Publications
-----------------------------------------------

-   Authentication Protocol: <https://oauth.net/2/>

-   Access Protocol: <https://wadl.java.net/>

-   Message Queuing Protocol: <https://www.amqp.org/>

-   Message Format: <http://www.json.org/>

## Definitions
===========

## Terms and Definitions
---------------------

  Name           Definition
  -------------- ------------------------------------------------------------------------------------------------------------------------------------------------------
  REST Service   A RESTful web service (also known as a RESTful web Application Programming Interface (API)) is a service implemented using HTTP and REST principles.
  Resource       A resource is an individual data entity that is identifiable by a URI.

## Acronyms
--------

  Name   Full Spelling
  ------ -----------------------------------
  AIT    Office of Information Technology
  API    Application Programming Interface
  FAA    Federal Aviation Administration
  HTTP   Hypertext Transfer Protocol
  JSON   JavaScript Object Notation
  REST   Representational State Transfer
  RSDD   REST Service Description Document
  SDLC   System Development Lifecycle
  SLA    Service Level Agreement
  SOA    Service Oriented Architecture
  SSA    Service Security Agreement
  URI    Uniform Resource Identifier

## Service Properties and Capabilities
===================================

## Service Profile
---------------

### Service Properties

  Profile Item                                    Value
  ----------------------------------------------- -------
  Service Name                                    
  Registered FAA Namespace                        
  Description                                     
  Version                                         
  Service Category (per FAA-STD-066)              
  Lifecycle Stage (per FAA-STD-066)               
  Criticality for the Service (per FAA-STD-066)   

### Service Provider

  Organization Name   FAA ADE-320
  ------------------- ------------------------
  Description         FAA, Solution Delivery
  Web Page URL        

#### Service Points of Contact

  POC Function   Name               Org       Phone          Email
  -------------- ------------------ --------- -------------- --------------------------
  AIT SOA lead   Jill Longenecker   ADE-320                  Jill.Longenecker@faa.gov
  Manager, EIM   Robert Fernandez   ADE-220   301.427.5085   Robert.Fernandez@faa.gov
  EIM            Wayne Larson       ADE-220   202.267.7210   Wayne.Larson@faa.gov

### Service Consumers

Specific consumers of this service are managed by the AIT SOA team and
its associated infrastructure and governance processes. Contact the AIT
SOA team for more information about the current consumers of this
service.

### Service Functionality

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Business Function                      Practical Effect
  -------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------
  UAS Flight Notification                -   FAA receives record of a voluntary notification from TPP (class G airspace)
                                         
                                         -   FAA receives record of a notification from TPP (class C airspace)
                                         

  UAS Flight Authorization               -   FAA receives record of a authorization from TPP (class B and below ATC preapproved altitude)
                                         

  UAS Flight Re-Consideration            -   FAA receives record from TPP of a reconsideration request that was made from a UAS operator (class B above pre-approved sUAS altitude
                                         

  UAS Flight Re-Consideration response   -   FAA receives record from TPP of a reconsideration response given from ATC
                                         

  UAS Flight Denial                      -   FAA receives denial record from TPP (for all denied flights)
                                         
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Service Security

Application authentication through OAuth-2.0 (<https://oauth.net/2/>)

### API Protocol and Webhooks

#### API Protocol

APIs shall be REST APIs that support Web Application Description
Language (WADL) (https://wadl.java.net/) documentation

#### Webhooks

Webhooks shall play an important within the system. Below is a
description of Webhooks.

A webhook is an event triggered mechanism of a web application to
deliver data. Also called a web callback or HTTP push API, a webhook is
a way for an app to deliver data to other applications as events occur.
An example of an event that triggers a webhook is a user submitting a
web form. Therefore, webhooks provide the ability to immediately react
respond to given events. Webhooks are intended to primarily receive data
and respond accordingly or receive data, process it and pass it on.

A Webhook is a Post request (HTTP callback) that is submitted to a URL.
The designated URL is configured to receive the Post and process it in a
specific way. When a web application implements webhooks, users are
given the ability to create their own URLs to integrate their app with
the web application implementing the webhook. Data from webhooks are
either in JSON or XML format or transmitted as form data.

APIs are an alternate mechanism to webhooks for application interaction.
API excel at exchanging data between separate applications. However,
APIs are more cumbersome when change notifications are involved. That is
where webhooks come into play. Webhooks are better suited to react to
system changes. API require constant monitoring of a system in order to
react systems change. This can involve more computing resources than is
necessary. Because webhooks operate with an event-based mechanism,
webhooks are simpler and more efficient in this case. The key is the
configuration of the webhook. Webhooks are ideal with the handling of
real-time notifications of events.

### Message Queuing Protocol

APIs shall support the Advanced Message Queuing Protocol (AMQP)
(https://www.amqp.org/) message queuing protocol

### Message Format

APIs shall format data as XML
(<https://www.w3.org/XML/Core/#Publications)>

#### UASs in FIXM

Within this document, we discuss the data which is required to be
transmitted to and from air traffic control and UAS operators. It is
based upon the Low Altitude Authorization and Notification Capability
(LAANC) data model and the LAANC Concept of Operations document.
Specifically, we outline those data which may be expressed using the
core of the FAA standard messaging framework (Flight Information
eXchange Model; FIXM). For the data which cannot be expressed with the
FIXM core framework, we propose extensions to current FIXM data classes
which may encompass necessary UAS data.

UASs are not regular, commercial aircraft. Nor are they model aircraft.
Rule 107 encompasses proposed regulations on UAS operation for
commercial and recreational use. The nature of UASs require data not yet
present within current FIXM schema. We follow the LAANC proposed data
model, and discuss parts of the data model which fit into the existing
FIXM core schema and parts of the data model which will require
extensions.

Most of the data needed to track and regulate UASs exists already in
FIXM. UASs are piloted aircraft, after all. As such, a flight plan may
be submitted either to notify flights nearby or to request authorization
to fly in certain regions.

The operator must provide their contact information: postal address,
phone number, email.

Any proposed flight plan will consist of one or more points, for which
the geographical location (latitude and longitude), the proposed time of
the flight, the altitude, and the flight radius needs to be given. A
flight may only be performed within visible line of sight during daytime
and twilight hours (with proper lights), so a flight proposal class will
have permissions or indicators. LAANC includes both the proposed
altitude of the flight and the flight radius. **Note: it is advised to
maintain using decimal degrees to specify the latitude/longitude
location. The sexagesimal standard has limited resolution (0.1 km),
which may create conflicts between multiple UAS flights. Otherwise, when
specifying the nearest airport, we require both a distance AND a
bearing, to pinpoint the location.**

The TPP should send a message to the operator via the front end
interface. The TPP should also generate a FIXM-formatted message
containing the same information to be recorded by ATC for reference by
other operators/ATC. The FIXM format is required for consistency, to
ease any subsequent analysis of the messages (require less code to input
all the messages) and to boost readability.

##### Data already covered in FIXM

###### Operator contact information

&lt;contact&gt;

&lt;address&gt;

…

&lt;/address&gt;

&lt;onlineContact&gt;

…

&lt;/onlineContact&gt;

&lt;/contact&gt;

Most of the contact information necessary is already covered in FIXM.
The XML fields listed above cover two contact methods. Phone/fax number
may also be given. For automated response messages, the email should be
used, or else a third party provider should take the response and send a
notification to the operator via email or mobile message/SMS (whichever
option is covered and preferred). If the TPP has a mobile app or web
interface, notifications can be sent this way.  

###### Flight plan

[]{#_Toc475620573 .anchor}We cover latitude, longitude, time, altitude,
proposal submission datetime, accept/reject datetime, closest airport,
flight plan version, and proposed speed. In the following, fb refers to
the FIXM base namespace, and fx refers to the FIXM flight namespace.
Setting these references can be found in the appendices, where (ns2 =
fb) and (ns3 = fx).

###### lat lon

[]{#_Toc475620574 .anchor}Specify a flight route as a single segment
with a single point of reference

&lt;fx:point&gt;

    &lt;fb:location srsName="urn:ogc:def:crs:EPSG::4326"&gt;

        &lt;fb:pos&gt; &lt;/fb:pos&gt;

    &lt;/fb:location&gt;

&lt;/fx:point&gt;

The srsName is the coordinate reference system. The FIXM documentation
states, FIXM uses only "urn:ogc:def:crs:EPSG::4326", which refers to the
WGS84 standard. If coordinates are input in a different coordinate
reference system, the third party provider must convert to WGS84
coordinates for the FIXM message. However, this may be modified in the
future to facilitate further coordinate updates and international
communication.

There are several ways of specifying location. E.g. referencePoint or
significantPoint, which may be used to specify a location within the
flight plan or the location of the departure/arrival aerodrome. The
point4D or trajectoryPoint4D. The 4D point specifies the latitude,
longitude, altitude, and time. These data may also be specified
elsewhere.

###### Time

Covers planned launch/landing times.

> &lt;fx:estimatedDepartureTime&gt;dateTime&lt;/fx:estimatedDepartureTime&gt;
>
> &lt;fx:estimatedArrivalTime&gt;dateTime&lt;/fx:estimatedArrivalTime&gt;

Inputs are dateTime objects in Greenwich Mean Time.

###### Altitude

&lt;fx:level&gt;

    &lt;fx:altitude ref="SFC" uom="FT"&gt;200&lt;/fx:altitude&gt;

&lt;/fx:level&gt;

The ref (reference: SFC = above ground level, MSL = above mean sea
level, STD = barometric altitude from standard 1 atm pressure, and W84 =
height above WGS84 ellipsoid) and uom (Unit Of Measure; can be “FT” or
“M”) attributes are required.

###### Proposal Submission Date

When the proposal was submitted. The accepted class is a receipt that
the ATC received the proposal.

&lt;fx:filing&gt;

    &lt;fx:accepted&gt;&lt;/fx:accepted&gt;

    &lt;fx:filingTime&gt;&lt;/fx:filingTime&gt;

&lt;/fx:filing&gt;

Accepted field may be “ACCEPTED”, “REJECTED”, or “MANUAL”. The last
choice represents a negotiation between the operator and air traffic
control. The filingTime field must be a datetime object.

###### Proposal FAA Response Time

&lt;fx:flightPlanNegotiationStatus&gt;

    &lt;fx:operationalAcceptability status=""
statusReason=""&gt;&lt;/…&gt;

    &lt;fx:planningStatus status=””
statusReason=””&gt;&lt;/fx:planningStatus&gt;

&lt;/fx:flightPlanNegotiationStatus&gt;

Under operationalAcceptability, the status may be “Acceptable” or “Not
Acceptable”, and the statusReason is a textual description for the
decision. The planningStatus status attribute may be “CONCUR”,
“NON\_CONCUR”, or “NEGOTIATE”, and the statusReason attribute is a
textual description of the decision.

These decisions may be automated, based upon regulation as determined by
air traffic control or a third party provider. If so, then statusReason
may simply quote the regulations violated by the flight plan, and the
result will require the operator to submit a revised flight plan.

###### Closest Airport

Use the nearest airport as a reference point in departure aerodrome. We
assume arrival aerodrome is the same as the departure; only the time
will differ.

&lt;fb:otherReference iataDesignator="" name=""&gt;

    &lt;fb:referencePoint&gt;

        &lt;fb:distance uom:”FT”&gt;&lt;/fb:distance&gt;

        &lt;fb:pos&gt;&lt;/fb:pos&gt;

    &lt;/fb:referencePoint&gt;

&lt;/fb:otherReference&gt;

UASs flying within 5 miles of an airport require notification (not
necessarily authorization). May also be used to determine the message
recipient.

###### Flight Plan Version

The flight plan version, which may go under the "flight" data class,
details the version of the flight plan under consideration. This allows
for a more extensive negotiation related to the flight plan, if the ATC
determines that slight modifications to the flight plan are necessary to
grant a waiver or authorization. The operator, TPP, and ATC all require
this data.

&lt;version&gt;

    &lt;aspFlightPlanVersion&gt;&lt;!-- Unique ID for flight plan. Given
by ASP. --&gt; &lt;/aspFlightPlanVersion&gt;

    &lt;auFlightPlanVersion&gt;&lt;!-- Unique ID for flight plan. Given
by airspace user (operator). --&gt; &lt;/auFlightPlanVersion&gt;

&lt;/version&gt;

ASP = ?, AU = airspace user. Only one or the other need to be given; the
TPP may be considered an ASP for these purposes when relaying messages
to/from ATC and the operator.

###### Proposed Speed

The proposed (maximum) speed of the flight.

&lt;fx:airspeed uom="KM\_H"&gt;10&lt;/ns3:airspeed&gt;

This specified the maximum or proposed average airspeed of the flight.
It is called within a single segment. The the case of a flight specified
by waypoints, each segment (the space connecting each waypoint) has a
proposed speed, or else the speed applies equally to each segment. The
units may be KM\_H for kilometers per hour, KT for knots, or MACH for
mach number. 

###### ATC Authorization

Latitude, longitude, time, altitude, flight start, flight end (times),
time of decision, and flight plan version. These data in the FAA
authorization message are covered above in the flight plan data. ATC
authorization will mostly send flightPlanNegotiationStatus. This data
class allows ATC to give a full-text explanation for
acceptance/rejection. Within flightPlanNegotiationStatus, there are
objects for planningStatus and operationalAcceptability, which give
reasons for the status of the proposed route and the status of the
message, respectively.

###### Planning Status

This class is optional, and outlines the status of the message. This is
depreciated in favor of 5.1.3b. 

&lt;operationalAcceptability status="" statusReason=""/&gt;

status is either 'Ack' (acknowledge), 'Accept', or 'Reject'. The
statusReason is a string of indeterminate length explaining the status.
It will be necessary for a 'Reject' status. A reason may or may not be
given for an acknowledge/accept message.

###### Operational Acceptability

This class is for a response to a proposed flight plan and outlines the
status of the proposed flight plan.

&lt;planningStatus status="" statusReason=""/&gt;

The status attribute may be 'Ack', 'Accept', or 'Reject'. The
statusReason is a string of indeterminate length explaining the status.
It will be necessary for a 'Reject' status. A reason may or may not be
given for an acknowledge/accept message.

##### Data not yet covered in FIXM

-   Operator: UAS class/code, descriptions

-   Aircraft: make, model, registration number

-   Flight plan: flight radius, waivers (over people indicator,
    airspeed, altitude, etc.), description, airspace class, nearest
    airport

-   FAA Authorization: waivers (airspace, time, etc.), “ATC approved
    specific conditions”, authorization acknowledgement & time.

-   Airspace class (needs to be attached to the flight plan, not the
    operator; add into point, region classes?). And airspace permission
    is for a single flight. 

-   VLOS and operation over people indicators.

###### Potential Extensions to FIXM

In this document, we do not give the XML schema which will define these
data types. However, we give sample XML code and potential inputs which
help clarify the necessary data types and their relationships.

###### Permissions

Class, within operator details -- specifies previous permissions held.
This is an optional class, and there can be any number of permissions
given for a particular operator. The waiver indicators should default to
False (0), and the airspaceClassPermission should default to G, prior to
air traffic control response and modification.

> &lt;fb:permissions&gt;
>
>    &lt;fb:airspaceClassPermission&gt;G&lt;/fb:airspaceClassPermission&gt;
>
>    &lt;fb:permissionWaiverID&gt;\_\_\_\_&lt;/fb:permissionWaiverID&gt;
>
>    &lt;fb:permissionWaiverSignatory&gt;\_\_\_\_&lt;/fb:permissionWaiverSignatory&gt;
>
>    &lt;fb:permissionAcceptDate&gt;&lt;/fb:permissionAcceptDate&gt;
>
>    &lt;fb:permissionStartDate&gt;&lt;/fb:permissionStartDate&gt;
>
>    &lt;fb:permissionEndDate&gt;&lt;/fb:permissionEndDate&gt;
>
>     &lt;fx:operationOverPeople&gt;True&lt;/fx:operationOverPeople&gt;
>
>    &lt;fx:altitudeWaiver&gt;True/False&lt;/fx:altitudeWaiver&gt;
>
>    &lt;fx:VLOSwaiver&gt;True/False&lt;/fx:VLOSwaiver&gt;
>
>    &lt;fx:speedWaiver&gt;True/False&lt;/fx:speedWaiver&gt;
>
>    &lt;!-- add whichever other waivers are necessary --&gt;
>
> &lt;/fb:permissions&gt;

Required:

permissionWaiverID, permissionWaiverSignatory (ID of who authorized
waiver, characterType), permissionAcceptDate (date of authorization,
datetime type), permissionStartDate (date the authorization begins,
datetime type), permissionEndDate (date the authorization expires,
datetime type)

Optional:

The authorization indicators are optional. The airspace class permission
defaults to G, and every other permission indicator defaults to False.
The following indicate which rules the authorization cover

airspaceClassPermission (character: B, C, D, E, G), overPeople
(boolean), altitudeWaiver (boolean), VLOSwaiver (boolean), speedWaiver
(boolean).

###### UAS operator

Class: covers the operator class code and operator type, specified in
LAANC data model.

> &lt;fb:UASOperator&gt;
>
>    &lt;fb:classCode ns2:uasCode=""&gt;Description&lt;/fb:classCode&gt;
>
>    &lt;fb:uasOperatorType
> ns2:uasType=""&gt;Description&lt;/fb:uasOperatorType&gt;
>
> &lt;/fb:UASOperator&gt;

Both are required for commercial flights and accepts all characters
(from CharacterStringType). UAS operator type may be COMMERCIAL, PUBLIC,
HOBBYIST, or OTHER. The OTHER would require a description, COMMERCIAL
would also require a description, and PUBLIC and HOBBYIST would not
require a description.

###### Air Class

Attribute, within the region class. Points may have FAA designations to
help identify where the aircraft is. Now, each point also has an
airspace classification. This proposed attribute is optional, and mostly
applicable to UASs.

> &lt;fx:region airClass="G"&gt;&lt;/fx:region&gt;

airClass (optional) = {‘B’, ‘C’, ‘D’, ‘E’, ‘G’, ‘R’, ‘T’}, where ‘R’ =
restricted, ‘T’ temporarily unrestricted for certain types of activity
(after checking the NOTAMs). Input is optional, and may be a ICAO
location designation (e.g., airport code) and accepts
CharacterStringType.

###### Flight Radius

Class. A proposed flight may only fly up to 400 ft (without a waiver),
however, the average person can technically resolve a 2 ft object at
more than half a mile. An operator must maintain enough visual
resolution of the aircraft in order to maintain operations (including
seeing orientation \[yaw, pitch, roll\]). It is not clear how far this
can be, but let us be more generally allow for a flight ellipsoid:
define two distances (altitude \[vertical\] & flight radius
\[horizontal\]).

> &lt;fx:flightRadius uom="FT"&gt;200&lt;/fx:flightRadius&gt;

Unit of measure = feet or meters, specify. Input is a lengthType.

###### VLOS Indicator

A proposed flight is required to operate within visible line-of-sight of
the operator. This data is a boolean, indicating whether the operator
will maintain visible line-of-sight for the duration of the flight. If
FALSE, then the ATC may grant a waiver after clarifications.

&lt;fx:VLOSIndicator&gt;True/False&lt;/ns3:VLOSIndicator&gt;

###### Operation over people indicator

A proposed flight is not allowed to operate over people (though I do not
know what the actual definition is). The datum is a boolean, indicating
whether the UAS is going to operate over people. A waiver may be granted
by ATC (e.g., news casting).

&lt;fx:operationOverPeople&gt;True/False&lt;/fx:operationOverPeople&gt;

### Qualities of Service

Qualities of Service (QoS) is addressed by Service Level Agreements
(SLAs) developed for this service.

Service Interfaces & Data Model
-------------------------------

REST is a style of software architecture that provides a convenient and
consistent approach to requesting and modifying data. In the context of
FAA REST services, it refers to using HTTP verbs to retrieve and modify
representations of data stored by FAA.

In a RESTful system, resources are stored in a data store; a client
sends a request that the server perform a particular action (such as
creating, retrieving, updating, or deleting a resource), and the server
performs the action and sends a response, often in the form of a
representation of the specified resource.

In RESTful services, the client specifies an action using an HTTP verb
such as POST, GET, PUT, or DELETE. It specifies a resource by a
globally-unique URI of the following form:

### Resources

A resource is an individual data entity with a unique identifier. A REST
service can operate on one or more types of resources based on that
service’s data model.

A service data model can be based on groups of resources, called
collections.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Class Name**                **Class Description**
  ----------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Airport                       Vendor created table containing all Airport information obtained from FAA.

  Airspace                      Vendor created table\
                                \
                                containing all Airspace information\
                                \
                                obtained from FAA.\
                                \
                                Class B, C, D, E & G Airspace\
                                \
                                \
                                \
                                The TPP planning tool would also depict features relevant to UAS flight such as classes of airspace, any active temporary flight restriction (TFR), obstacles, or other restricted airspace (e.g., public utilities).\
                                \
                                \
                                \
                                Each TPP will use authorized FAA airport, SUA, and locality map data to automatically provide, where feasible, confirmations of notification and authorizations to UAS operators.\
                                \
                                Class E Airspace\
                                \
                                TFR Airspace\
                                \
                                Restricted Airspace

  Airspace Authorization        Airspace Authorization Association\
                                \
                                The Assumption is that an Authorized UAS operation may occur in multiple Airspaces.\
                                Either transitioning from one Airspace to another or operating in overlapping Airspaces.

  Authorization                 Authorizations are the result of data sent from ATC to an operator regarding a specific request received asking permission to operate in a particular airspace. Authorizations in the context of LAANC shall not be confused with ATC permissions provided in-flight via radio between a pilot in command and ATC to enter airspace requiring two-way communication with ATC.

  Proposed Operation            Flight Specifics of Proposed Operation

  Proposed Operation Airspace   Proposed Operation Airspace Association\
                                \
                                The Assumption is that a proposed UAS operation may occur in multiple Airspaces.\
                                Either transitioning from one Airspace to another or operating in overlapping Airspaces.

  Reference Request Type        Reference Request Type

  Reference Timeframe           Reference Timeframe

  Request                       A request is the result of data sent from a UAS operator to ATC providing key parameters about an operation which must be approved or denied.\
                                \
                                A Request may also be for Notification purposes only where no authorization is required.

  UAS Operator Class            UAS Operator Class

  UAS Operator Type             UAS Operator Type
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Methods

The following table lists the HTTP methods that are generally applicable
to the LAANC RESTful services.

  Method   Description                                                      REST HTTP Mappings
  -------- ---------------------------------------------------------------- ----------------------------------------------------------------------
  Get      Gets a specific resource or lists a specified set of resources   GET on resource URI
  Put      Updates a specific resource                                      PUT on resource URI, where you pass in data for the updated resource
  Post     Creates a resource                                               
  Delete   At present, there is no intent to delete in this system          

Of the candidate methods in the table above, the following table
indicates which HTTP methods are supported for each resource.

  Resource Name                 Supported Methods
  ----------------------------- ------------------- ------ ----- --------
                                Get                 Post   Put   Delete
  Airport                       Yes                 Yes    Yes   No
  Airspace                      Yes                 Yes    Yes   No
  Airspace Authorization        Yes                 Yes    Yes   No
  Authorization                 Yes                 Yes    Yes   No
  Proposed Operation            Yes                 Yes    Yes   No
  Proposed Operation Airspace   Yes                 Yes    Yes   No
  Reference Request Type        Yes                 Yes    Yes   No
  Reference Timeframe           Yes                 Yes    Yes   No
                                                                 

### Resource Representations

This section define how each resource is represented.

&lt;For each resource for the service, include a subsection below
describing the resource representation.&gt;

#### Resource Name

The data dictionary is now a separate document in the FAA LAANC Github
repository. “LAANC (Class) Data Dictionary 2017-02-27.xlsx”

### Sample Payloads

&lt;For each data format supported, include a subsection below
(entitled, for example, “Sample XML Payload”, “Sample JSON Payload”)
with one or more sample payloads in each format. If the payloads differ
significantly across resources, include samples for all such
resources.&gt;

#### Sample Payload

&lt;Sample Payload for the Service in format 1.&gt;

&lt;Request&gt;

&lt;Phone\_Number&gt;&lt;/Phone\_Number&gt;

&lt;Request\_Type\_Code&gt;&lt;/Request\_Type\_Code&gt;

&lt;Request\_Status\_Acknowledged\_Indicator&gt;&lt;/Request\_Status\_Acknowledged\_Indicator&gt;

&lt;Request\_Status\_Acknowledged\_Timestamp&gt;&lt;/Request\_Status\_Acknowledged\_Timestamp&gt;

&lt;Request\_Status\_Authorized\_Indicator&gt;&lt;/Request\_Status\_Authorized\_Indicator&gt;

&lt;Request\_Status\_Authorized\_Timestamp&gt;&lt;/Request\_Status\_Authorized\_Timestamp&gt;

&lt;Request\_Status\_Denied\_Indicator&gt;&lt;/Request\_Status\_Denied\_Indicator&gt;

&lt;Request\_Status\_Denied\_Timestamp&gt;&lt;/Request\_Status\_Denied\_Timestamp&gt;

&lt;ATC\_Denied\_Comments&gt;&lt;/ATC\_Denied\_Comments&gt;

&lt;Request\_Status\_Terminated\_Indicator&gt;&lt;/Request\_Status\_Terminated\_Indicator&gt;

&lt;Request\_Status\_Terminated\_Timestamp&gt;&lt;/Request\_Status\_Terminated\_Timestamp&gt;

&lt;Request\_Hazard\_Indicator&gt;&lt;/Request\_Hazard\_Indicator&gt;

&lt;Notification\_Required\_Indicator&gt;&lt;/Notification\_Required\_Indicator&gt;

&lt;Authorization\_Required\_Indicator&gt;&lt;/Authorization\_Required\_Indicator&gt;

&lt;Prior\_Waiver\_Number&gt;&lt;/Prior\_Waiver\_Number&gt;

&lt;Prior\_Authorization\_Number&gt;&lt;/Prior\_Authorization\_Number&gt;

&lt;Prior\_Letters\_Of\_Agreement\_Number&gt;&lt;/Prior\_Letters\_Of\_Agreement\_Number&gt;

&lt;UAS\_Operator\_Class\_Code&gt;&lt;/UAS\_Operator\_Class\_Code&gt;

&lt;UAS\_Operator\_Type\_Code&gt;&lt;/UAS\_Operator\_Type\_Code&gt;

&lt;Notification\_Acknowledgement\_Indicator&gt;&lt;/Notification\_Acknowledgement\_Indicator&gt;

&lt;Nearest\_Airport&gt;&lt;/Nearest\_Airport&gt;

&lt;UAV\_Registration\_Number&gt;&lt;/UAV\_Registration\_Number&gt;

&lt;Third\_Party\_Provider\_Key&gt;&lt;/Third\_Party\_Provider\_Key&gt;

&lt;Create\_Timestamp&gt;&lt;/Create\_Timestamp&gt;

&lt;/Request&gt;

&lt;Proposed\_Operation&gt;

&lt;Operation\_Description&gt;&lt;/Operation\_Description&gt;

&lt;Timeframe\_Code&gt;&lt;/Timeframe\_Code&gt;

&lt;Maximum\_Altitude&gt;&lt;/Maximum\_Altitude&gt;

&lt;Latitude\_Degrees&gt;&lt;/Latitude\_Degrees&gt;

&lt;Latitude\_Minutes&gt;&lt;/Latitude\_Minutes&gt;

&lt;Latitude\_Seconds&gt;&lt;/Latitude\_Seconds&gt;

&lt;Latitude\_Direction&gt;&lt;/Latitude\_Direction&gt;

&lt;Longitude\_Degrees&gt;&lt;/Longitude\_Degrees&gt;

&lt;Longitude\_Minutes&gt;&lt;/Longitude\_Minutes&gt;

&lt;Longitude\_Seconds&gt;&lt;/Longitude\_Seconds&gt;

&lt;Longitude\_Direction&gt;&lt;/Longitude\_Direction&gt;

&lt;VLOS\_Indicator&gt;&lt;/VLOS\_Indicator&gt;

&lt;Operations\_Over\_People\_Indicator&gt;&lt;/Operations\_Over\_People\_Indicator&gt;

&lt;Flight\_Radius&gt;&lt;/Flight\_Radius&gt;

&lt;Flight\_Start\_Timestamp&gt;&lt;/Flight\_Start\_Timestamp&gt;

&lt;Flight\_End\_Timestamp&gt;&lt;/Flight\_End\_Timestamp&gt;

&lt;Operation\_Status\_Denied\_Indicator&gt;&lt;/Operation\_Status\_Denied\_Indicator&gt;

&lt;Operation\_Status\_Denied\_Timestamp&gt;&lt;/Operation\_Status\_Denied\_Timestamp&gt;

&lt;Create\_Timestamp&gt;&lt;/Create\_Timestamp&gt;

&lt;/Proposed\_Operation&gt;

&lt;Authorization&gt;

&lt;Authorization\_FAA\_Acknowledgement\_Indicator&gt;&lt;/Authorization\_FAA\_Acknowledgement\_Indicator&gt;

&lt;Authorization\_FAA\_Acknowledgement\_Timestamp&gt;&lt;/Authorization\_FAA\_Acknowledgement\_Timestamp&gt;

&lt;ATC\_Approved\_Specific\_Conditions&gt;&lt;/ATC\_Approved\_Specific\_Conditions&gt;

&lt;Timeframe\_Code&gt;&lt;/Timeframe\_Code&gt;

&lt;Maximum\_Altitude&gt;&lt;/Maximum\_Altitude&gt;

&lt;Latitude\_Degrees&gt;&lt;/Latitude\_Degrees&gt;

&lt;Latitude\_Minutes&gt;&lt;/Latitude\_Minutes&gt;

&lt;Latitude\_Seconds&gt;&lt;/Latitude\_Seconds&gt;

&lt;Latitude\_Direction&gt;&lt;/Latitude\_Direction&gt;

&lt;Longitude\_Degrees&gt;&lt;/Longitude\_Degrees&gt;

&lt;Longitude\_Minutes&gt;&lt;/Longitude\_Minutes&gt;

&lt;Longitude\_Seconds&gt;&lt;/Longitude\_Seconds&gt;

&lt;Longitude\_Direction&gt;&lt;/Longitude\_Direction&gt;

&lt;VLOS\_Indicator&gt;&lt;/VLOS\_Indicator&gt;

&lt;Operations\_Over\_People\_Indicator&gt;&lt;/Operations\_Over\_People\_Indicator&gt;

&lt;Flight\_Radius&gt;&lt;/Flight\_Radius&gt;

&lt;Flight\_Start\_Timestamp&gt;&lt;/Flight\_Start\_Timestamp&gt;

&lt;Flight\_End\_Timestamp&gt;&lt;/Flight\_End\_Timestamp&gt;

&lt;Create\_Timestamp&gt;&lt;/Create\_Timestamp&gt;

&lt;/Authorization&gt;

Service Implementation
----------------------

### Endpoints

The following subsections provide information about the base service
endpoints that are used to reference and access the resources.

&lt;For each base service endpoint, include a subsection below
describing the endpoint.&gt;

#### Endpoint 1 Name

&lt;Brief description of endpoint 1.&gt;

##### Supported Data Formats

  Protocol:                 XML
  ------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Description:              []{#abstract .anchor}The Extensible Markup Language (XML) is a subset of SGML that is completely described in this document. Its goal is to enable generic SGML to be served, received, and processed on the Web in the way that is now possible with HTML. XML has been designed for ease of implementation and for interoperability with both SGML and HTML.
  Specification Location:   https://www.w3.org/XML/Core/\#Publications

##### Network Address

The network address for this endpoint is:

##### End Point-Specific Qualities of Service

Please refer to the SLA document(s) for the service for QoS details.

The data model is now a separate document in the FAA LAANC Github
repository. “LAANC (Class) 2017-02-27.pdf”

**Data Model**

Appendix A Example FIXM messages
================================

A.1 Operator to TPP: Proposed Flight Plan
-----------------------------------------

&lt;?xml version="1.0" encoding="UTF-8" standalone="yes"?&gt;

&lt;!-- In order to determine the airspace permissions, we need airspace
codes and aircraft 4D location: latitude, longitude, altitude, and time.
Only comment needs to be:  --&gt;

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>"
 xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>"

   xmlns:ns2="<http://www.fixm.aero/base/4.0>"
xmlns:ns3="<http://www.fixm.aero/flight/4.0>"

   xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance>
<http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

   

&lt;metadata&gt;

   &lt;gumi&gt;urn:[fixm.aero](http://fixm.aero):asa:ods:20130203T022530:000001&lt;/gumi&gt;

&lt;/metadata&gt;

 &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

&lt;flight&gt;

   &lt;ns3:gufi&gt;au.asa.20130203T022530a.000001&lt;/ns3:gufi&gt;

   &lt;ns3:activeFlightPlan ns3:flightPlanIdentifier="1"&gt;

       &lt;ns3:aircraftIdentity&gt;

           &lt;ns3:acid&gt;FFFF&lt;/ns3:acid&gt;

       &lt;/ns3:aircraftIdentity&gt;

       &lt;ns3:aircraftDescription&gt;

           &lt;ns3:capabilities ns3:standard="STANDARD"&gt;

               &lt;ns3:communication&gt;

                   &lt;ns3:communicationCodes&gt;N&lt;/ns3:communicationCodes&gt;

                   &lt;ns3:dataLinkCodes&gt;&lt;/ns3:dataLinkCodes&gt;

                   &lt;ns3:selectiveCallingCodes&gt;&lt;/ns3:selectiveCallingCodes&gt;

               &lt;/ns3:communication&gt;

                &lt;ns3:surveillance&gt;

                   &lt;ns3:surveillanceCodes&gt;N&lt;/ns3:surveillanceCodes&gt;

               &lt;/ns3:surveillance&gt;

               &lt;ns3:navigation&gt;

                   &lt;ns3:navigationCodes&gt;N&lt;/ns3:navigationCodes&gt;

                   &lt;ns3:performanceBasedCodes&gt;&lt;/ns3:performanceBasedCodes&gt;

               &lt;/ns3:navigation&gt;

           &lt;/ns3:capabilities&gt;

           &lt;ns3:registration&gt;\_\_\_&lt;/ns3:registration&gt;

               &lt;!-- aircraftCategory is new. The make/model of a UAS
must be

                       included in a waiver request. It is provided here
under

                       the aircraft description.

               --&gt;

           &lt;ns3:aircraftCategory&gt;

               &lt;ns3:model&gt;\_\_\_&lt;/ns3:model&gt;

               &lt;ns3:manufacture&gt;\_\_\_&lt;/ns3:manufacture&gt;

           &lt;/ns3:aircraftCategory&gt;

       &lt;/ns3:aircraftDescription&gt;

       &lt;ns3:formationAircraftCount&gt;1&lt;/ns3:formationAircraftCount&gt;

       &lt;ns3:filing&gt;

           &lt;ns3:accepted&gt;ACCEPTED&lt;/ns3:accepted&gt;

           &lt;ns3:filingTime&gt;2013-02-03T02:25:30.890Z&lt;/ns3:filingTime&gt;

       &lt;/ns3:filing&gt;

       &lt;ns3:departure&gt;

       &lt;!-- Already included in FIXM: reference Aerodrome. This
includes

               geographical location of reference point (nearest
aerodrome)

               and the distance between reference point and operator.

        --&gt;

           &lt;ns2:OtherReference iataDesignator="" name=""&gt;

               &lt;ns2:referencePoint&gt;

                   &lt;ns2:distance
uom="FT"&gt;\_\_&lt;/ns2:distance&gt;

                   &lt;ns2:pos&gt;\_\_ \_\_&lt;/ns2:pos&gt;

               &lt;/ns2:referencePoint&gt;

           &lt;/ns2:OtherReference&gt;

          &lt;ns3:estimatedDepartureTime&gt;

               2013-02-02T04:00:00.000Z

           &lt;/ns3:estimatedDepartureTime&gt;

       &lt;/ns3:departure&gt;

       &lt;ns3:arrival&gt;

           &lt;ns3:estimatedArrivalTime&gt;

               2013-02-02T05:00:00.000Z

           &lt;/ns3:estimatedArrivalTime&gt;

       &lt;/ns3:arrival&gt;

       &lt;ns3:route&gt;

           &lt;ns3:text&gt;2704N11627W&lt;/ns3:text&gt;

           &lt;ns3:segment xsi:type="ns3:BasicSegmentType"
xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>"&gt;

               &lt;ns3:level&gt;

                   &lt;ns3:altitude ref="SFC"
uom="FT"&gt;200&lt;/ns3:altitude&gt;

               &lt;/ns3:level&gt;

               &lt;ns3:airspeed uom="KM\_H"&gt;10&lt;/ns3:airspeed&gt;

               &lt;ns3:airway xsi:nil="true"/&gt;

               &lt;ns3:point&gt;

                   &lt;ns2:location
srsName="urn:ogc:def:crs:EPSG::4326"&gt;

                       &lt;!-- How many decimal places are valid? Is
there a standard? --&gt;

                       &lt;ns2:pos&gt;27.066667
-116.453328&lt;/ns2:pos&gt;

                   &lt;/ns2:location&gt;

               &lt;/ns3:point&gt;

               &lt;!-- Proposed extension specifies the flight radius.
When

                       combined with the altitude, this forms an semi-

                       ellipsoid, centered at ground level.

               --&gt;

               &lt;ns3:flightRadius
uom="FT"&gt;200&lt;/ns3:flightRadius&gt;

               &lt;!-- Proposed extension is the "airClass" attribute to
the

                       region class. This specifies the airspace
classification

                       of the proposed flight, and helps determine the

                       accept/reject status of the proposed flight.

               --&gt;

               &lt;ns3:region airClass="G"&gt;&lt;/ns3:region&gt;

               &lt;fx:VLOSIndicator&gt;True&lt;/ns3:VLOSIndicator&gt;

             
 &lt;fx:operationOverPeople&gt;True/False&lt;/fx:operationOverPeople&gt;

           &lt;/ns3:segment&gt;

       &lt;/ns3:route&gt;

       &lt;ns3:flightType&gt;SCHEDULED&lt;/ns3:flightType&gt;

   &lt;/ns3:activeFlightPlan&gt;

   &lt;version&gt;

       &lt;aspFlightPlanVersion&gt;&lt;!-- Unique ID for flight plan.
Given by ASP. --&gt; &lt;/aspFlightPlanVersion&gt;

       &lt;auFlightPlanVersion&gt;&lt;!-- Unique ID for flight plan.
Given by airspace user (operator). --&gt; &lt;/auFlightPlanVersion&gt;

   &lt;/version&gt;

&lt;/flight&gt;

&lt;/message&gt;

&lt;recipient&gt;

     &lt;!-- who gets the message. See contact, under operating
Organization. Recipient = TPP →

&lt;/recipient&gt;

&lt;messageOriginator&gt;

    &lt;!-- Information about who sent this message. See contact, under
operating Organization. Originator = operating organization. →

&lt;/messageOriginator&gt;

&lt;ns3:operatingOrganization&gt;

   &lt;!-- UAS Operator class, includes the operator class code and the

           type and the respective descriptions.

   --&gt;

   &lt;ns2:UASOperator&gt;

       &lt;ns2:classCode
ns2:uasCode=""&gt;Description&lt;/ns2:classCode&gt;

       &lt;ns2:uasOperatorType
ns2:uasType=""&gt;Description&lt;/ns2:uasOperatorType&gt;

   &lt;/ns2:UASOperator&gt;

   &lt;ns2:contact name="B" title="Dr."&gt;

       &lt;ns2:address&gt;

           &lt;ns2:administrativeArea&gt;STATE/PROVINCE&lt;/ns2:administrativeArea&gt;

           &lt;ns2:city&gt;CITY NAME&lt;/ns2:city&gt;

           &lt;ns2:countryCode&gt;USA&lt;/ns2:countryCode&gt;

           &lt;ns2:countryName&gt;United States of
America&lt;/ns2:countryName&gt;

           &lt;ns2:deliveryPoint&gt;StreetAddress&lt;/ns2:deliveryPoint&gt;

           &lt;ns2:postalCode&gt;10001&lt;/ns2:postalCode&gt;

       &lt;/ns2:address&gt;

       &lt;ns2:onlineContact&gt;

           &lt;ns2:email&gt;\_\_\_@[ata-llc.com](http://ata-llc.com)&lt;/ns2:email&gt;

       &lt;/ns2:onlineContact&gt;

       &lt;ns2:phoneFax&gt;

           &lt;ns2:voice&gt;PhoneNumber&lt;/ns2:voice&gt;

       &lt;/ns2:phoneFax&gt;

   &lt;/ns2:contact&gt;

   &lt;!-- Proposed extension to operatingOrganization or organization
class

       (or both): permissions. This lists the permissions the
organization

       already has. This helps determine the accept/reject status of the

       proposed flight.

   --&gt;

    &lt;!-- If, for example, the operator has a overPeople waiver, the
following

                 permission would be granted.

    --&gt;

    &lt;ns2:permissions&gt;

     
 &lt;ns2:permissionWaiverID&gt;\_\_\_\_&lt;/ns2:permissionWaiverID&gt;

       &lt;ns2:permissionWaiverSignatory&gt;\_\_\_\_&lt;/ns2:permissionWaiverSignatory&gt;

       &lt;ns2:permissionAcceptDate&gt;&lt;/ns2:permissionAcceptDate&gt;

       &lt;ns2:permissionStartDate&gt;&lt;/ns2:permissionStartDate&gt;

       &lt;ns2:permissionEndDate&gt;&lt;/ns2:permissionEndDate&gt;

       &lt;ns2:operationOverPeople
xsi:type="waiverType"&gt;True&lt;/ns2:operationOverPeople&gt;

   &lt;/ns2:permissions&gt;

&lt;/ns3:operatingOrganization&gt;

&lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/FlightMessage&gt;

A.2 TPP to Operator: Accept/Reject.
-----------------------------------

This message is sent from the TPP to the operator once the TPP has
decided the status of the flight based upon the rules stated in part 107
OR the ATC has responded to the TPP about authorization. Important
information includes the planningStatus data class within the
flightPlanNegotiationStatus data class. If the status returns "Rejected"
the statusReason will contain information about the rules in violation.
Note: with an "Accepted" status, the statusReason may still contain the
rules in violation as long as the proper waivers have been obtained. The
statusReason will include information about these waivers.

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" \
xmlns:ns2="<http://www.fixm.aero/base/4.0>" xmlns:ns3="<http://www.fixm.aero/flight/4.0>" \
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance> <http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt;

        &lt;ns3:planningStatus status="Accepted" statusReason=""/&gt;

        &lt;!-- OR &lt;ns3:planningStatus status="Rejected"
statusReason="part 107, rule 1: airspace class A. part 107 rule \_\_:
nighttime operation"/&gt; →

        &lt;!-- OR &lt;ns3:planningStatus stauts="Rejected"
statusReason=""/&gt; — this means that no modification will get a
waiver. --&gt;

    &lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Specifically, will contain the flight plan VERSION. No
need to reiterate the entire flight plan. This saves space and
prevents bloat in order to improve readability. A relational database
should have no problems, given the proper message IDs, message
collection IDs, and flight plan versions. --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt;

        &lt;!-- who gets the message: operator, specified in operating
oranization, or the official contact for this flight plan. →

    &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message: TPP --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt;

        &lt;!-- Information about UAS operator ... who is flying the
UAS. If the status is Accepted after ATC has granted a waiver, the
operatingOrganization field will be updated. An example is as follows:

        --&gt;

        &lt;ns2:permissions&gt;

         
 &lt;ns2:permissionWaiverID&gt;\_\_\_\_&lt;/ns2:permissionWaiverID&gt;

         
 &lt;ns2:permissionWaiverSignatory&gt;\_\_\_\_&lt;/ns2:permissionWaiverSignatory&gt;

         
 &lt;ns2:permissionAcceptDate&gt;&lt;/ns2:permissionAcceptDate&gt;

         
 &lt;ns2:permissionStartDate&gt;&lt;/ns2:permissionStartDate&gt;

           &lt;ns2:permissionEndDate&gt;&lt;/ns2:permissionEndDate&gt;

           &lt;ns2:speedWaiver
xsi:type="waiverType"&gt;True&lt;/ns2:speedWaiver&gt;

       &lt;/ns2:permissions&gt;

    &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

A.3 TPP to ATC: Notification
----------------------------

This message occur when a proposed flight plan is otherwise authorized,
except for operating within 5 miles of an airport. The full flight plan
is to be submitted, as the ATC requires the information to render a
decision. Notice the planningStatus data class: notification. The
important indicator within the flight plan is the airClass attribute
(within the region data class) and the distance data class, within the
(arrival) aerodrome.

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" \
xmlns:ns2="<http://www.fixm.aero/base/4.0>" xmlns:ns3="<http://www.fixm.aero/flight/4.0>" \
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance> <http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;!--  And acknowledge status with a notification reason: notifies
ATC of proposed flight. This will be sent simultaneously with a
message of "accepted" to the operator.

    --&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt;

        &lt;ns3:planningStatus status="Acknowledge"
statusReason="Notification"/&gt;

        &lt;!-- OR &lt;ns3:planningStatus status="Rejected"
statusReason="part 107, rule 1: airspace class A. part 107 rule \_\_:
nighttime operation"&gt; --&gt;

    &lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Contains information about departure/arrival
times/locations and flight radius and location and time: full flight
plan. And will contain the flight plan VERSION. Give the proper message
IDs, message collection IDs, and flight plan versions.

         --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message: ATC
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message: TPP --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

A.4 TPP to ATC: Authorization Request
-------------------------------------

This message is sent from the TPP to ATC if authorization to waive some
part 107 rules is required.

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" \
xmlns:ns2="<http://www.fixm.aero/base/4.0>" xmlns:ns3="<http://www.fixm.aero/flight/4.0>" \
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance> <http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt;

        &lt;ns3:planningStatus status="Acknowledge"
statusReason="Authorization Request"&gt;

        &lt;!-- The following authorizationRequest is a proposed
extension to the planning status data class. Add indicators as
necessary.  --&gt;

            &lt;ns3:VLOSIndicator
requestDateTime=""&gt;Boolean&lt;/ns3:VLOSIndicator&gt;

            &lt;ns3:overPeopleIndicator requestDateTime=""&gt;Boolean,
optional&lt;/ns3:overPeopleIndicator&gt;

        &lt;!-- ... Add additional indicators (authorization request
indicators) as needed ... --&gt;

        &lt;/ns3:planningStatus&gt;

    &lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Contains information about departure/arrival
times/locations and flight radius and location and time: full flight
plan. And will contain the flight plan version. Give the proper message
IDs, message collection IDs, and flight plan versions. This information
will be used by ATC to determine authorization status.

         --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message: ATC
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message: TPP --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

A.5 ATC to TPP: Accept – Authorization Granted
----------------------------------------------

This message is sent from the ATC to the TPP after the ATC has recieved
an authorization request. This response includes the waiver ID, the
acceptance date, and the start/expiration date for the waiver along with
the waiver-type indicator. The full flight plan does not need to be
included, as the waiver is granted with no modifications.

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" \
xmlns:ns2="<http://www.fixm.aero/base/4.0>" xmlns:ns3="<http://www.fixm.aero/flight/4.0>" \
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance> <http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt;

        &lt;ns3:planningStatus status="Accept" statusReason="Waiver
granted for part 107 rule \_\_\_."&gt;

        &lt;/ns3:planningStatus&gt;

    &lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Full flight plan not returned to TPP, only the flight
plan version. Give the proper message IDs, message collection IDs, and
flight plan versions.

         --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message: TPP
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message: ATC --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS. With ATC authorization, the permissions
section here can be updated once the TPP notifies the operator in the
next step, or the ATC can update the permissions now. The first case is
covered in Appendix A.2 --&gt;  

           &lt;ns2:permissions&gt;

             
 &lt;ns2:permissionWaiverID&gt;\_\_\_\_&lt;/ns2:permissionWaiverID&gt;

             
 &lt;ns2:permissionWaiverSignatory&gt;\_\_\_\_&lt;/ns2:permissionWaiverSignatory&gt;

             
 &lt;ns2:permissionAcceptDate&gt;&lt;/ns2:permissionAcceptDate&gt;

             
 &lt;ns2:permissionStartDate&gt;&lt;/ns2:permissionStartDate&gt;

             
 &lt;ns2:permissionEndDate&gt;&lt;/ns2:permissionEndDate&gt;

               &lt;ns2:speedWaiver
xsi:type="waiverType"&gt;True&lt;/ns2:speedWaiver&gt;

           &lt;/ns2:permissions&gt;

    &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

A.6 ATC to TPP: Reject with Minor Modifications
-----------------------------------------------

This message is sent if it is determined that a slight modification to
the flight plan will get a waiver or make a waiver unnecessary. Note the
words "Modify ..." within the statusReason in the planningStatus data
class. In this case, "slight" means lowering maximum altitude or moving
the operating location(s) within one (this number can be changed) flight
radius. Flight information is not returned; the flight plan version
number is given so the operator may reference the correct flight plan
proposal. The quantity which needs to be modified is given within the
statusReason of the planningStatus (rule number violation), and ATC does
not need to determine in which direction to modify the given quantity.
That is left to the operator.

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" \
xmlns:ns2="<http://www.fixm.aero/base/4.0>" xmlns:ns3="<http://www.fixm.aero/flight/4.0>" \
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance> <http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt;

        &lt;ns3:planningStatus status="Reject" statusReason="Part 107
rule \_\_ violation. Modify (altitude/location)."&gt;

        &lt;/ns3:planningStatus&gt;

    &lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Full flight plan not returned to TPP, only the flight
plan version. Give the proper message IDs, message collection IDs, and
flight plan versions.

         --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message: ATC
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message: TPP --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

A.7 ATC to TPP: Reject
----------------------

The ATC determines that the flight cannot be modified in order to be
granted a waiver. E.g., proposal to take real estate photographs within
a no-fly zone.

&lt;message xmlns="<http://www.fixm.aero/messaging/4.0>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" \
xmlns:ns2="<http://www.fixm.aero/base/4.0>" xmlns:ns3="<http://www.fixm.aero/flight/4.0>" \
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance> <http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt;

        &lt;ns3:planningStatus status="Reject" statusReason=""&gt;

        &lt;/ns3:planningStatus&gt;

    &lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Full flight plan not returned to TPP, only the flight
plan version. Give the proper message IDs, message collection IDs, and
flight plan versions.

         --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message: ATC
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message: TPP --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

Appendix B Message Collections
==============================

A message collection is an object which contains a number of FIXM
messages. The following messages will be grouped based upon UAS flight
plan – each flight plan will be a message collection consisting of the
proposed flight plan(s) and any response from the third party providers
or air traffic control (ATC). If ATC conditionally rejects a flight
plan, the operator must file a modified or new flight plan, to be
approved by the ATC again. An example abbreviated message collection
follows.

&lt;messageCollection xmlns="<http://www.fixm.aero/messaging/4.0>"
xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>"\
xmlns:ns2="<http://www.fixm.aero/base/4.0>"
xmlns:ns3="<http://www.fixm.aero/flight/4.0>"\
xsi:schemaLocation="<http://www.w3.org/2001/XMLSchema-instance>
<http://www.fixm.aero/fixm/4.0/Fixm.xsd>"&gt;

&lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;!-- Message 1: flight plan proposal, see Appendix A.1 --&gt;

&lt;message&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt; ...
&lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Contains information about departure/arrival
times/locations and flight radius and location and time. --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

&lt;!-- Message 2: notification of flight to FAA/ATC. See Appendix A.3
--&gt;

&lt;message&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt; ...
&lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Contains information about departure/arrival
times/locations and flight radius and location and time. --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

&lt;!-- Message 3: TPP notification of acceptance of flight plan to
operator. See Appendix A.2 --&gt;

&lt;message&gt;

    &lt;messageDateTime timeReference="UTC"&gt;&lt;/messageDateTime&gt;

    &lt;ns3:flightPlanNegotiationStatus&gt; ...
&lt;/ns3:flightPlanNegotiationStatus&gt;

    &lt;flight&gt;

        &lt;!-- Contains information about departure/arrival
times/locations and flight radius and location and time. --&gt;

    &lt;/flight&gt;

    &lt;recipient&gt; &lt;!-- who gets the message
--&gt; &lt;/recipient&gt;

    &lt;messageOriginator&gt;  &lt;!-- Information about who sent this
message --&gt; &lt;/messageOriginator&gt;

    &lt;operatingOrganization&gt; &lt;!-- Information about UAS operator
... who is flying the UAS --&gt;  &lt;/operatingOrganization&gt;

    &lt;uniqueMessageIdentifier codeSpace=""/&gt;

&lt;/message&gt;

&lt;!-- End of message collection. Flight plan approved. --&gt;

&lt;/messageCollection&gt;
