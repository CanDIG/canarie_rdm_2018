# Scoring Criteria:

> 1.  **What is the extent to which the project makes use of or
>     contributes to digital research infrastructure?**

CHORD builds on previous Canadian software, network, and computational
investments in digital research infrastructure (DRI), to enable a
national data service for privacy-sensitive genomic and related
health data.

CHORD builds on previous software DRI investments by building a
secure, privacy-preserving data back end which which the GenAP
portal will be able to make use of enable analyses of private health
data.

By providing an inherently federated approach to the analysis of 
Canadian health genomic and related data, CHORD builds on the
investments behind Canada's National Education and Research Network
for high-speed, low-latency availability of queries and intermediate
results.

And the computational, storage, and personnel resources at the
participating sites (MUQGIC, HPC4Health, and the BCGSC), will be
the backbone on which initial CHORD services are provided.

Those investments, combined with the services provided in the work
described here, means that CHORD will a truly national data service
for privacy-sensitive genomics and related health data.

> 2.  **What is the extent to which the project creates or contributes to
>     a national data service?**

CHORD will provide four key capabilities which would define a national data service
for privacy-sensitive genomic health data.

CHORD will:
* allow **publishing** genomic and associated clinical and phenotypic data, and making them available for analysis,
* enable **searching** for data, including mechanisms for discovering potential data that a user does not yet have authorization to access, with information about who to contact about authorization,
* support **moving** computation to private data, allowing analyses of sensitive data, and combining intermediate results of computations between sites; and
* facilitate the **linking** of data and literature by providing citable persistent identifiers.

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
CanDIG services (via open, authorized protocols, A1.1, A1.2),
but accessibility (including, for instance, for download) _per se_ had
not been a goal; similarly, data that was not available due whether
due to loss or lack of authorization meant that the metadata was
no longer visible.  CHORD will allow data downloads when so authorized
(A1) and the &ldquo;Censored Discovery&rdquo; will always allow
some degree of accessibility of metadata (A2).

Interoperability of data between similar projects with CanDIG services
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

CanDIG is a driver project for the Global Alliance for Genomics and
Health, an international organization defining standards, APIs,
and, policies for the effective, interoperable, and responsible
sharing of genomic data.  As a driver project, CanDIG both contributes
to the development of standards, and participates in collaborations
between other genomics projects such as Genomics England and the
Australian Genomics Health Alliance.  CHORD will benefit from
CanDIG's participation in GA4GH, ensuring that CHORD services
developed are compatible with new and emerging standards and are
built in collaboration with similar projects around the world.

# System Architecture 

![System Infrastructure](../figures/CANARIE_RDM_Fig_1.png "Fig 1: System Infrastructyre")

**Figure 1**, above, shows an overall system architecture diagram of
the CHORD project.  CHORD is designed as a modern, API-driven,
service-oriented architecture, with genomic data and clinical/phenotypic
metadata services being provided by individual externally-facing
services behind an API gateway, and separate persistence layers for
the small, complex clinical/phenotypic data and the large files
that constitute the genomic data.

Users authenticate via their home institutions or via the proposed
Canadian Access Federation integration (Activity 2.2).  That
authentication is verified upon the requests entry in to the system
at the API gateway layer, and continues to be verified and logged
as the request makes its way through the services.  The API gateway
also provides a useful single point of ingress and egress for logging
and monitoring to provide context to service-level logging, and
will allow load-balancing if needed in the future.

Federated accesses to data are handled above the service level;
federated variants queries (for instance) involve the variants
service fanning out queries to members of the network making
authenticated requests on the users behalf, combining the results,
and return the results.  This low-coupling approach to federation - as
opposed to having, for instance, the clinical/phenotypic data
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
are current or emerging standards developed by the international
GA4GH effort.  Workflow execution and `htsget` for data access
(Activity 1.4.6) are going through the GA4GH standards process
currently, and CHORD will benefit from existing tools which implement
those standards.  CanDIG is working actively with the GA4GH Large
Scale Genomics and Clinical and Phenotypic Capture workstreams to
develop standards for RNA data services, variants, and clinical and
phenotypic metadata.

New single-page applications are proposed for CHORD, for data upload
(Activity 1.4.4) and discovery (Activity 2.1).  The upload portal
will interact with the upoad/download services, view access logs,
and uploaded data will trigger proposed new automated validation,
normalization, and quality control tasks before ingest (Activity 1.2).

For health data and in other privacy-sensitive areas, metadata
itself can be sensitive; simply knowing that there is data in the
system pertaining to a patient of a particular age and gender in a
specific small town with a given condition can be enough to expose
medical information of a patient.  Thus data discovery must proceed
carefully.  The proposed discovery portal will interact with a new
"Censored Discovery" API (Activity 2.1.1) within the clinical and
phenotypic metadata service; this will allow users to be informed
that discoverable data exists which matches their criteria but is
not currently available to them due to lack of authorization, along
with information on who to contact to request access.  This discovery
service would also be made available via the GenAP portal, in
collaboration with the GenAP team.

To allow fine-grained availability of data for analyses - for instance,
to allow aggregations of data to be computed even if researchers do
not have access to row-level data - CHORD will also create new 
capabilities for aggregations, including differential privacy, in
both variants and clinical and phenotypic searches (Activity 3.1).

Also proposed are new services for RNA data, a rapidly growing area
of genomic data (Activity 4.3).

# Software Architecture

![Software Infrastructure](../figures/CANARIE_RDM_Fig_2.png "Fig 2: Software Infrastructure")

**Figure 2**, above, describes in more detail the software stack used 
in CHORD, along with the boundaries between external and internal services
and local resources.

Fundamental to both CanDIG and the proposed CHORD project is that services
will be set up by data stewards at sites across the country; these sites
will have a variety of capabailities and existing installations, and the
CHORD software stack must have a way to interoperate with these different
back ends.  Typical sites would either be traditional HPC-style clusters,
or OpenStack installations.

The different environments on which CHORD services will run informs
several decisions.  Deployment of services on are quite different
between such environments; CHORD will benefit from CanDIG's development
of automated deployments for both bare-metal environments (using
Ansible), and kubernetes-style container-based deployments for cloud
deployments.

The CanDIG stack begins at the genomic data persistence level, where
in-progress work towards a scalable genomic back end data store is
based on [Minio](https://minio.io), an open source package which
exposes an S3-compatible object-store interface to a variety of
data back ends, including OpenStack-style object stores, or HPC
cluster style POSIX file systems.  Minio provides two additional
features of use for the CHORD project - replication for availability
and fault tolerance, allowing us to establish CHORD-wide policies
for replication; and S3-style lambda execution, allowing the proposed
automated validation, quality control, normalization, and ingest of 
data upon upload.

The computational resources of the site, as with the storage
resources, may be of HPC or OpenStack configurations, and automated
execution of the ingest tasks will have to work in either case.  For
this, we are making use of the in-progress workflow execution service,
based on GA4GH standards and using existing tooling which works on
either sort of compute back end.  Singularity containers will be
used, allowing both ease of packaging and interoperability with different
sorts of compute environments.  The proposed CHORD work for this task
(Activity 1.2) is to develop the software which will integrate the 
two services.

Genomic data access by the external services does not directly
interact with Minio, but with a Data Object Service (DOS), with an
API being developed by the GA4GH.  All access to genomic data through
this service - and to clinical/phenotypic metadata as well - must
be authorized in a consistent and auditable fashion. CanDIG is
refactoring authorization out into a single service, managed by a
policy engine [Casbin](http://casbin.org); in Activity 3.3, CHORD
will extend this service to enable the wider range of finer-grained
authorization needed for the broader range of data sets targeted
by CHORD.

Externally facing services are being developed in an API-first
fashion, using [OpenAPI](https://www.openapis.org) to define the
API for new services, and using OpenAPI-based tooling to guide the
development and testing of both clients and servers of the API.
Services will be developed (and extended) in both Python and Go.

Requests entering CHORD will pass through the API Gateway infrastructure
developed by CanDIG, based on [Tyk](https://tyk.io), a feature-rich,
highly-configurable open-source package deployable both as containers
and on bare metal.  Authentication is performed by OpenID connect via
trusted Identity Providers; in Activity 2.2, CHORD will build on GenAP's
work with the Canadian Access Federation to allow authentication into
CanDIG services by the broader Canadian research community.

Portals and other front ends (Activities 1.4.4, 2.1) will be developed
with common web programming frameworks, in particular Reactjs.

# Software Development Summary

> Please provide an overview of the proposed software development.
> Your summary should:
>
> Identify existing software that will be used.
> Describe any modifications that will have to be made to the existing software.
> Describe any new software that will have to be developed.
>
> Max 750 words

CHORD extends the services, data types, and capabilities provided
by the CanDIG project to build a federated, Canadian, national data
service for privacy-sensitive genomic and related health data.
An API-first approach will be taken, with service APIs being defined
in OpenAPI and OpenAPI ecosystem tooling being used for validation,
testing, and implementation of servers and clients.

CHORD software development is organized into four broad activities:
Data Publishing, Findability and Access, Privacy-Preserving Reuse, and
Expanded Health Data Support.

In Activity 1, Data Publishing, an activity owned by the Hospital
for Sick Children, the software infrastructure is built which would
support the ingest, assignment of persistent identifiers, and
publishing of a genomic and related health data.  In activity 1.1,
CanDIG as an in-kind contribution will push forward the development
of a currently prototype data backend which is not currently necessary
for the projects CanDIG is supporting.  This back end is based on
the well-used package Minio, which provides uniform object-store
functionality across a variety of underlying storage types, wrapped
by the Data Object Service, a service standard developed by the
cloud work stream of the GA4GH.  Activity 1.2 consists of developing
automated data normalization and quality control to be run upon uploading;
Activity 1.3 consists of the generation of permanent identifiers and
ingest of the normalized data if it passes QC; and Activity 1.4 consists
of the API-driven development of the user-facing upload process, including
a portal and forms/APIs for entering relevant clinical and phenotypic
metadata.

In Activity 2, Findability and Access, owned by lead contractor
McGill, a data discovery portal (Activity 2.1) will be built which
allows the user to discover data, including data that the user does
not have access to (where possible and made discoverable by the
data owner) but with information about how to find out more about
authorization for that data set.

This data discovery service will integrate with the previously CANARIE-funded GenAP platform, through its 
Portal and APIs. GenAP leverages Compute Canada infrastructure and CANARIE high-speed network to
facilitate bioinformatics analysis by the life science research community. As such, by making CHORD
data discoverable and obtainable through GenAP will enable users to analyse its data
in existing GenAP services, such as the Galaxy web interface. GenAP-Galaxy is a popular framework that allows launching computation
jobs on Compute Canada infrastructure more easily. In addition, Activity 2.2 will build on
the GenAP team's growing experience with using CAF for authentication
to authentication via CAF into CHORD services.

In Activity 3, Privacy Preserving Reuse, owned by the BCGSC with
participation by McGill with participation by BC, we will add
finer-grained levels of authorization and privacy to the CHORD
services.  In Activity 3.1, CHORD will add differentially private
calculations of aggregations to the existing variants, and clinical
and phenotypic, servers, allowing data stewards to not only restrict
authorization to aggregate rather than row-level data, but to require
the addition of noise.  In Activity 3.2, we will add the use of
data use ontologies (such as the [Automatable Discovery and Access
Matrix (ADA-M)](https://github.com/ga4gh/ADA-M)) for describing
allowable data use, reflecting patient and data steward consents,
and make this feature available in discovery APIs.  In Activity
3.3, CanDIG will again contribute in-kind development effort by
pushing forward the deployment of a authorization policy engine
based on Casbin, allow finer-grained authorization than currently
needed by the CanDIG project, to allow the requirement of aggregation,
differentially private aggregation, and data use matching.  Finally,
usage logs will be made available to data owners in Activity 3.4.

Activity 4, Expanded Health Data Support, owned by McGill, will
address the wider range of data types that CHORD users will need
over what CanDIG currently supplies for its driver projects. 
Activity 4.1 will add to the current clinical and phenotypic metadata
server by expanding the data model and API to include FHIR resources
for Observations and Measurements, greatly expanding the range of
patient data that can be stored.  Links to external data sources
such as imaging data will be added to the metadata server in Activity
4.2; and emerging standards for increasingly important RNA data will
be developed into new services in Activity 4.3.  To better incorporate
the addition of these services into CHORD, CanDIG will accelerate the
development of and contribute its integrated testing harness to
the CHORD project.

# Future Customization and/or Extension of Functionality

The CHORD design is targetted towards a rapidly evolving genomics
and health data environment.  CHORD's service-oriented architecture
is designed to enable future scale out, along dimensions of data
volumes, data types, and data services.

By separating the data persistance layer from the data services,
having individual data services contained within their own tools,
and using a reverse proxy API gateway to expose the services, we
incur a modest degree of short-term complexity for future expansion.
For instance, adding the RNA data services proposed in Activity 4.3
does not require modifications to any other services as long as the
existing metdata model is flexible enough to be able to describe
the new data types.

Factoring the clinical and phenotypic metadata storage out from
the genomic data store shifts the coupling betwen metadata access
from code and data models to RESTful API calls, allowing much 
more rapid iteration on each side while greatly reducing the scope
for breaking changes.

Similarly, abstracting the workflow execution and genomic data store
behind existing tooling like Cromwell or Minio allows us the
flexibility to deploy on a wide variety of systems and system types.
