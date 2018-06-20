Project Plan
============

**KEY TASKS LIST**

Gantt Chart available at http://candig.github.io/canarie_rdm_2018/Overview.html

| **Key Task** | **Start Date yyyy-mm-dd** | **End Date yyyy-mm-dd** | **% of total effort required for the project** | **Task Owner (Lead Contractor or Participant)**   | **Milestones / Deliverables - must be tangible and measurable** |
|--------------|---------------------------|-------------------------|-----------------------------------------------|---------------------------------------------------|-----------------------------------------------------------------|
| **Activity 1:**       | 2018-10-01 | 2019-12-16 | 31% | HPC4Health | 1.1 Production DOS/Minio Back End |
| **Data Publishing**   |            |            |     |            | 1.2 Data Ingest                   |                    
|                       |            |            |     |            | 1.3 CanDIG Accession ID           |
|                       |            |            |     |            | 1.4 Data Upload                   |
| **Activity 2:**       | 2019-06-04 | 2020-04-28 | 15% | McGill | 2.1 CAF interoperability |
| **Discovery, Access** |            |            |     |        | 2.2 Data Discovery Portal|                                
| **Activity 3:**       | 2018-10-01 | 2020-03-13 | 26% | BCGSC  | 3.1 Differential Privacy |
| **Private Reuse**     |            |            |     |        | 3.2 Data Use Ontologies  |                    
|                       |            |            |     |        | 3.3 Fine-Grained Authorization Engine |
|                       |            |            |     |        | 3.4 Depositor-Viewable Data Use Logs |
| **Activity 4:**       | 2018-10-01 | 2020-01-29 | 29% | McGill | 4.1 Expanded Clinical/Phenotypic Data |
| **Expanded Data**     |            |            |     |        | 4.2 External Data References |                    
|                       |            |            |     |        | 4.3 Expanded RNA data support |
                                                                                                                                                                                                                                                                                                                                       

**FEATURES LIST**

  **Deliverable**              **Feature \#**   **Feature Description**
  ---------------------------- ---------------- -------------------------
  &lt;First deliverable&gt;    1                
                               2                
                               3                
  &lt;Second deliverable&gt;   1                
                               2                
                               3                
                                                
                                                
                                                
                                                

Risk Assessment and Mitigation Plan
===================================

**Risk Assessment: Development: Unforseen development complexity**
**Mitigation**: The CHORD software development plan consists of
individual activities that describe building features with ample
precedent within either CanDIG, the previous activities of our
participating institutions, or the activities of our GA4GH colleagues.
The novelty consists in the integration of these services into a
well-functioning whole in our genomics and health national context.
While such integration is not without risk, the use of individual
feature sets that have been used successfully elsewhere in the past
offers some confidence in the feasibility of the plan.

**Risk Assessment: Development: Hiring and Retention, in CHORD or CanDIG**
**Mitigation**: The CHORD software development plan describes related
but only loosely coupled activities, with little or no scope for
cascading delays, and CHORD would be in service with only modest,
temporary reduction in functionality if any individual activity or
even two activities were delayed due to staffing issues.  As an
example, even if the most fundamental activity, that describing the
underlying genomic data store (in-kind Activity 1.1) were to be
delayed by the (very real) difficulty in hiring and retaining staff
with strong devops-type backgrounds, work on other activities could
continue with the current production CanDIG genomic data back end.
Even for those activities which seemingly hinge crucially on activity 1.1 -
automated data processing based on Minio lambdas - the interaction
is only an implementation detail, and workflows could be run in an
semi-automated fashion on uploaded data using the current backend
and some temporary scaffolding until the new back end were complete.

**Risk Assessment: Availability: Downtime**
**Mitigation** Individual data stewards may suffer downtime, either
due to operational issues or network connectivity.  CanDIG is
developing across-site operations policies which will describe and
evolve best practices for keeping CHORD sites up, but it is vital
that any one sites downtime does not make federated queries or
analyses involving sites that are up unavailable.  The current
federation approach handles federated queries in a way that degrade
gracefully, informing the user that the federated query is incomplete,
but returning the most complete answer available.  Other, more complete
mitigation approaches (_e.g._, cross-data-center replication) are unavailable
to us.

**Risk Assessment: Availability: Site removes data**
**Mitigation** Fundamental to the approach of both CanDIG and CHORD
is that individual data stewards retain complete control of their
data, and so removal of data is not necessarily inappropriate;
indeed, there are situations where it is required (when, for
instance, a patient withdraws consent for their data to be used in
a particular way).  Transparency, reproducibility, and FAIRness
benefit, however, when data is not removed unnecessarily, and
metadata describing the data, and describing the revocation of the
data, remain available when possible.  CanDIG, under the leadership
of Professor Yann Joly at McGill, is beginning the development of
a governance and policy framework which will address data policies.

**Risk Assessment: Integrity: Data loss/corruption**
**Mitigation** A national data service must make all feasible efforts
to prevent the loss or corruption of data.  CHORD will make use 
of technical, operational, and policy strategies to maintain the
integrity of published data.  The Minio backend will make use
of multiple replicates and erasure codes; CanDIG and CHORD will
develop and exchange operational best practices (including replication
factor and storage requirements); CanDIG sites will make use of
existing encrypted DR capabilities for offsite backup, and will recommend
approaches for new CHORD sites.

**Risk Assessment: Confidentiality: Privacy/Security Breach**
**Mitigation** The most significant risk to a data steward is a
breach concerning data under their stewardship.  As with data
integrity, this must be handled at technical, operational, and policy
levels.  At a technical level, security-sensitive code used by
CHORD services will rely on extremely well-tested external libraries
(such as well-respected OpenID Connect libraries, Casbin as a policy
engine) rather than in-house tools.  We will ensure that the software
we develop and our operations follow the best practices of the 
GA4GH Security workstream, and that of the hospitals that make up
the initial CanDIG sites.  Services will be developed so that they
are logged and fully auditible, and services at our hospital sites
will undergo threat risk assesments (TRAs) and privacy impact
assessments (PIAs).  New services will be extensively tested with
synthetic or open data before used in production with private data.
And all breaches of any kind will be reported following both the
reporting mechanisms of the site(s) in question, and the GA4GH.

Software Provenance
===================

The owner of the integrated testing harness, Pierre-Olivier Quirion
at McGill, will be the release manager for the CHORD package as a
whole, and will authorize updated releases of the suite of services.

Individual service owners will occasionally wish to make releases
of their services available at a more rapid cadence than the suite
as a whole; they may do so after consulting with the CHORD software
release manager and verifying that integration testing is successful,
as described in the testing plan below.

As part of the release of any service or the complete suite, changelogs,
updated documentation, and migration instructions (if necessary) will
be included.

Incorporating updates to upstream dependencies will be triaged by
urgency, impact, and changes necessary to CHORD services.  Security
and privacy issues will be addressed immediately, displacing any
other priorities.  Routine, point-release updates will be addressed
at a lower priority, with latest versions of dependencies being
incorporated into new CHORD service releases on a best-effort basis.
New major releases that introduce breaking changes will be planned
for in advance of the official release of the upstream package, and
adaption and strategies developed.

Testing Plan
============

The CanDIG project uses Travis-CI to perform unit testing of its
individual components, and as the number of services increases, is
moving towards and Jenkins for integration tests of the services.
Defining component APIs using OpenAPI where possible simplifies
this as it enables automatic validation of inputs and outputs.

CHORD will continue this testing approach, with individual components
unit-tested using Travis-CI, with tests written in an OpenAPI testing
framework such as Dredd or Mocha depending on the use case.  CanDIG
will accelerate its development of an integrated testing harness
using Jenkins, and CHORD will adopt that framework for end-to-end
testing.

Unit tests will be run on all component pull requests and commits,
and integration tests will be run routinely as determined by the
release manager.  Integration testing will be a requirement for all
new releases both of the individual components and of the CHORD suite
of services as a whole. 

User Training Plan
==================

Users of CHORD software will include both end users, and systems staff
looking to stand up new CHORD sites.

All CHORD participating sites perform regular bioinformatics training
for both local researchers and researchers across Canada (as with
the Canadian Bioinformatics Workshops).  This training already
covers access to biological data repositories.  CHORD will add units
to this training to include CHORD services, and we will use this
training as an opportunity both to onboard new users and to validate
portal UI/UX with real users.

Outreach to potential sites and system staff at these sites will
focus on technical and bioinformatics conferences, with training
on the installation and maintenance of new CHORD sites will be more
occurring both on-site and online as necessary for those who express
interest.

Maintenance and Support Plan
============================

> Outline your maintenance and support plan for the proposed software post CANARIE funding. Include your plans for:
>
> operations 
> software maintenance
> providing user support
> extending / adding functionality
> facilitating adoption by new users

CHORD services will be integrated into CanDIG, a four-year CFI
cyberinfrastructure project which completed its first annual project
update in April 2018 and funding anticipated to continue until April 2021.

CanDIG is already supporting two national precision oncology projects,
with additional projects being discussed as more and more projects
have both privacy and national data availability needs, and we hope
to continue to obtain development and maintenance funding beyond 2021.



Intellectual Property
=====================

> How do you intend to manage any intellectual property arising from this proposed project?

> Please note: Should commercialization of the IP take place, royalties will be required to accrue 
> to CANARIE to repay some or all of the contribution, and a royalty agreement will be required.

- Owned by service owners?  Lead contractor?
- GPL
- Possibility for service contracts, relicensing for commercial reuse, or development of new features for a fee, but do not anticipate such revenue.

