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

> Describe any risks (including non-HR risks) that could reasonably arise during development, and outline a mitigation strategy for each risk.

- Issues in securty sensitive code
- Data loss
- Braking changes/incompatability
- Hiring

Software Provenance
===================

> Please address the following questions:
> 
> Who would authorize software releases? 
> What validation procedures would be completed prior to release?
> What documents would be provided as part of the release package?
> How would you deal with upgrades / patches to third party software packages that you might use?

The owner of the integrated testing harness, Pierre-Olivier Quirion
at McGill, will be the release manager for the CHORD package as a
whole, and will authorize updated releases of the suite of services.
Individual service owners may wish to make releases of their services
available at a more rapid cadence than the suite as a whole; they may
do so after consulting with the CHORD sofware release manager and
verifying that integration testing is successful as below.

As part of the releae of any service or the complete suite, changelogs,
updated documentation, and migration instructions (if necessary) will
be included.

Updates to dependencies 


Testing Plan
============

> CANARIE strongly encourages the use of dedicated software testing resources. Outline how you intend to test your software to ensure it:
> meets the requirements that guided its design and development
> is usable and performs its intended function(s)
> can be installed and run in its intended environment

The CanDIG project uses Travis-CI to perform unit testing of its
individual components, and as the number of services increases, is
moving towards and Jenkins for integration tests of the services.
Defining component APIs using OpenAPI where possible simplifies
this as it enables autmoatic validation of inputs and outputs.

CHORD will continue this testing approach, with individual components
unit-tested using Travis-CI, with tests written in an OpenAPI testing
framework such as Dredd or Mocha depending on the use case.  CanDIG
will accellerate its development of an integrated testing harness
using Jenkins, and CHORD will adopt that framework for end-to-end
testing.

Unit tests will be run on all component pull requests and commits,
and integration tests will be run routinely as determined by the
release manager.  Integration testing will be a requirement for all
new releases both of the individual components and of the CHORD suite
of services as a whole.


User Training Plan
==================

> How do you intend to train / onboard new users?

Users of CHORD software will include both end users, and systems staff
looking to stand up new CHORD sites.

All CHORD participating sites perform regular bioinformatics training
for both local researchers and researchers across Canada (as with
the Canadian Bioinformatics Workshops).  This training covers access
to biological data repositories.  CHORD will add units to this
training to include CHORD services, and we will use this training
as an opportunity both to onboard new users and to validate portal
UI/UX with real users.

Training on the installation and maintenance of new CHORD sites will
be more ad hoc


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
update in April 2018 and funding anticpated to continue until April
2021.  CanDIG is already supporting two national precision oncology
projects, with additional projects being discussed as more and more
projects have both privacy and national data availabity needs.

**MORE NEEDED**

Intellectual Property
=====================

> How do you intend to manage any intellectual property arising from this proposed project?

> Please note: Should commercialization of the IP take place, royalties will be required to accrue 
> to CANARIE to repay some or all of the contribution, and a royalty agreement will be required.

- Owned by service owners?  Lead contractor?
- GPL
- Possibility for service contracts, relicensing for commerical reuse, or development of new features for a fee, but do not anticipate such revenue.

