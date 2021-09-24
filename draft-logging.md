--- 
title: 
abbrev: logging
docname: 
category: info
 
ipr: trust200902
area: 
workgroup: 
keyword: Internet-Draft
stand_alone: yes
pi:
  rfcedstyle: yes
  toc: yes
  tocindent: yes
  sortrefs: yes
  symrefs: yes
  strict: yes
  comments: yes
  inline: yes
  text-list-symbols: -o*+
 
author:
 
-
       ins: F. Last
       name: First Name
       organization: 
       email: 
 
-
       ins: F. Last
       name: First Name
       organization: 
       email: 
 
normative:
 
informative: 
   RFCXXXX:
 
   Title:
     title: ""
     date: 
     author:
        - ins: 
        - ins: 
     target: 
 
--- abstract
 
[abstract text here]
 
--- middle
 
Introduction
============

When setting up network servers on just about any platform, the default
configurations usually include detailed logging that can contain personally
identifying information (PII). And that data is set to kept for long periods of
time.  Many servers do not need to gather any PII at all to achieve their
purpose, so having PII stored is only adding risks for the operator.  There
could be a data breach, which leads to fines from privacy regulators, or other
forms of liability.  There is also the risk of unexpected work, for example,
when a user requests that all of their data is turned over to them or deleted.

The point of this document is to describe a best practice for default logging
configurations in order to minimize these risks while still providing useful
information for troubleshooting, monitoring, etc.  For service that do not need
to gather PII, using this configuration throughout the organization then makes
it possible to use a simple, standardized privacy policy.

For privacy policies to be effective, they need to be easy for both users and
implementers to understand.  Most privacy policies are long and contain lots of
legalese and vague wording that comes across as hand-waving.  There are a lot of
materials to guide people to create a custom privacy policy.  This approach
assumes that users will actually review each site's privacy policy.  That is a
bad assumption to build upon.

There should only be a small set of standardized privacy policies.  Any
privacy-oriented organization can review them and issue statements about which
they will approve.  This approach also then enables automated responses.  If
the privacy policy is at a /.well-known/ link and its contents has a well known
hash, then automated actions based on privacy policy would be easy to implement.
For example, there could be a browser preference of which privacy policies to
automatically accept, and which to automatically refuse to send data to.

There is an analogous situation with free software licenses.  It used to be
quite common for projects and organizations to write their own software
licenses.  That puts the onus on the user to read and understand each one of
them.  There are now many well known licenses, and the clear best practice is to
adopt one of them, and avoid writing a new one.  Then people can go to FSF, OSI,
Debian Legal, FSFE, Creative Commons, or whatever organization they trust and
see which licenses get their stamp of approval.

Apache Foundation takes a similar approach with Contributor License
Agreements (CLAs).  Mostly, companies make their own CLAs.  That means each code
contributor has to review each one of those.  If they all used Apache CLAs, code
contributors would only have to review it once, and then easily decide whether
they are willing to sign the Apache CLA for any given project.

EFF Do-Not-Track Policy is the only standardized, widely applicable privacy policy we've reviewed so far that also includes machine readability as a goal. I just found https://openpd.org/, which has a nice intro about this idea, but they seem to have no actual privacy policies. 


# TODO: Open Questions

* maybe the best approach here is to nail down one specific server config, then show how it maps on to some existing privacy policies?  So like: "if you implement this, you can choose from any of these standard privacy policies".

Standard server logs are usually not designed to include Personally Identifable
Information (PII).  But the metadata inherit to the operation of network servers
can be used to identify and track people.  For example, when a user connects to
a web service that puts login information in the query string of the URL, then
the default webserver configuration will log that full URL along with other
metadata like the IP address, exact time, time zone, language used, the browser
User Agent, etc.  If a user request their data be deleted from a web service,
removing the data from the database will still leave a detailed trail in the
server logs of all the steps that the user made using the web service.




Configuration Recommendations
==============

* stop logging the URL query string and potentially even the URL path, if they contain references to usernames, accounts, or any other PII.
* Configure the server logs to be automatically deleted after a given time period.
* The log retention time should be as short as possible.
* Define a maximum log retention time to be listed in the privacy policy, but then shorten the retention time to a week when the maximum log time is not actively needed.


Subsection header
-----------------

Conclusions
===========

Acknowledgements (optional)
================

### Webserver configuration

* https://f-droid.org/2019/04/15/privacy-preserving-analytics.html
* https://guardianproject.info/2017/06/08/tracking-usage-without-tracking-people/


### Standardized Privacy Policy

* https://standards.ieee.org/project/7012.html - P7012 - Standard for Machine Readable Personal Privacy Terms
* https://www.eff.org/dnt-policy
* https://globalprivacycontrol.org/
* https://openpd.org/


Security Considerations
=======================
 
As this draft concerns an informational document, there are no security considerations.
 
IANA Considerations
===================
 
This document has no actions for IANA.
