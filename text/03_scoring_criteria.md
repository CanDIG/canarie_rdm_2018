Scoring Criteria:
=================

> 1.  **What is the extent to which the project makes use of or
>     contributes to digital research infrastructure?**

> 2.  **What is the extent to which the project creates or contributes to
>     a national data service?**

> 3.  **What is the extent to which the project supports FAIR principles?**

The CHORD project aims to expand the FAIRness of the services offered
by CanDIG in two broad ways.

First, CHORD will allow broader adoption of the data and computation
services offered by CanDIG, beyond large national projects, by
making it easier to set up new CHORD sites to support data publishing
and re-use in the broader genomics research community.

Second, CHORD services will strengthen the FAIRness of the current
CanDIG suite of services in specific areas.

While findability of data through CanDIG services is very strong,
with rich metadata indexed in a searchable resource, with metadata
specifying the data identifier (F2,F3, and F4), identifiers are not
now guaranteed to be persistent; CHORD will improve the findability
and citability of Canadian genomic data by allowing it to be published
with a globally unique and persistent identifier (principle F1).

Availability for analysis has been a guiding principle of
CanDIG services (via open, authorized protocals, A1.1, A1.2),
but accessibility (including, for instance, for download) _per se_ had
not been a goal; similarly, data that was not available due whether
due to loss or lack of authorization meant that the metadata was
no longer visible.  CHORD will allow data downloads when so authorized
(A1) and the &ldquo;Censored Discovery&rdquo; will always allow
some degree of accessiblity of metadata (A2).

Interoperability of data betwen similar projects with CanDIG services
is good, with recommended ontologies (I1, I2) and qualified references
between metadata items or data items (I3), and reuse was enabled by
strong community standards (R1.3), provenance information (R1.2), and 
accurate and relevant attributes (R1).  Reuse however remains somewhat
limited by only recent emergence of standards for describing what 
data may be used for (R1.1); data may be consented for reuse only for certain
purposes.  CHORD will implement Data Use Ontologies such as the 
GA4GH [Automatable Discovery and Access Matrix (ADA-M)](https://github.com/ga4gh/ADA-M)
to allow data to be searched by allowable use.

> 4.  **What is the extent to which the project integrates with
>     international digital research infrastructure?**

System Architecture 
====================

> Insert a system architecture diagram outlining the hardware and software components of the proposed project,
> clearly differentiating between parts of the system that already exist and those parts that will have to be added/modified.
> Show how parts would interact with users and other resources, as appropriate.
> 
> Note: Your project should be designed with reuse and extendibility in mind.
> 
> Max. 2 pages

![System Infrastructure](../figures/CANARIE_RDM_Fig_1.png "Fig 1: System Infrastructyre")

*Figure 1*, above, shows an overall system architecture diagram of
the CHORD project.  CHORD is designed as a modern, API-driven,
service-oriented architecture, with genomic data and clinical/phenotypic
metadata services being provided by individual externally-facing
services behind an API gateway, and separate persistence layers for
the small, complex clinical/phenotypic data and the large files
that constitute the genomic data.

Users authenticate via their home institutions or via the proposed
Canadian Access Federation integration.  That authentication is
verified upon the requests entry in to the system at the API gateway
layer, and continues to be verified and logged as the request makes
its way through the services.  The API gateway also provides a
useful single point of ingress and egress for logging and monitoring
to provide context to service-level logging, and will allow
load-balancing if needed in the future.

Federated accesses to data are handled above the service level;
federated variants queries (for instance) involve the variants
service fanning out queries to members of the network making
authenticated requests on the users behalf, combining the results,
and return the results.  This low-coupling approach to federation
- as opposed to having, for instance, the clinical/phenotypic data
federated at the database level - is a necessity for handling private
data; control over, and transparency and auditability of, data
access is paramount, and so must be handled at the application
layer.

Individual services interact with the data persistence layers to
handle user requests; not shown in the diagram is that most requests
to genomic data services will cause those services to also send
requests to the clinical and phenotypic metadata server, meaning
that service will be under heavier load than the others and will
have tighter latency requirements.

Many of the existing, in progress, or proposed services for CHORD
are current or emerging standards developed by the international GA4GH
effort.  Workflow execution and `htsget` for data access are going
through the GA4GH standards process currently, and CHORD will benefit
from existing tools which implement those standards.  CanDIG is working
actively with the GA4GH Large Scale Genomics and Clinical and Phenotypic
Capture workstreams to develop standards for RNA data services, variants,
and clinical and phenotypic metadata.

New single-page applications are proposed for CHORD, for data upload
and discovery.  The upload portal will interact with the upoad/download
services, view access logs, and uploaded data will trigger proposed
new automated validation, normalization, and quality control tasks before
ingest.

For health data and in other privacy-sensitive areas, metadata
itself can be sensitive; simply knowing that there is data in the
system pertaining to a patient of a particular age and gender in a
specific small town with a given condition can be enough to expose
medical information of a patient.  Thus data discovery must proceed
carefully.  The proposed discovery portal will interact with a new
"Censored Discovery" API within the clinical and phenotypic metadata
service; this will allow users to be informed that discoverable
data exists which matches their criteria but is not currently
available to them due to lack of authorization, along with information
on who to contact to request access.  This discovery service would also
be made available via the GenAP portal, in collaboration with the GenAP
team.

To allow fine-grained availablity of data for analyses - for instance,
to allow aggregations of data to be computed even if researchers do
not have access to row-level data - CHORD will also create new 
capabilities for aggregations, including differential privacy, in
both variants and clinical and phenotypic searches.

Also proposed are new services for RNA data, a rapidly growing area
of genomic data.


Software Architecture
=====================

> Insert a high-level architecture diagram of the major functional components of the proposed software,
> illustrating how they would interact with each other, and clearly differentiating between components
> that already exist and those that will have to be added or modified. 
>
> Max. 2 pages

![Software Infrastructure](../figures/CANARIE_RDM_Fig_2.png "Fig 2: Software Infrastructure")

Software Development Summary
============================

> Please provide an overview of the proposed software development.
> Your summary should:
>
> Identify existing software that will be used.
> Describe any modifications that will have to be made to the existing software.
> Describe any new software that will have to be developed.
>
> Max 750 words

Future Customization and/or Extension of Functionality
======================================================

> Describe how your software design allows for future customization and/or extension of functionality.
>
> Max. 500 words.

