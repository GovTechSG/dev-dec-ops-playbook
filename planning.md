# Stage 1: Planning

## When should DevSecOps be adopted?

As per clause 6.1/G1, agencies should consider adopting DevSecOps to:

1. Perform frequent changes (such as quarterly) to the system and regular releases to meet user&#39;s needs.<br>
2. Deliver the system&#39;s features, bug fixes or enhancements faster through CI/CD.<br>
3. Improve quality and security of the system through &quot;shift-left&quot; practices and automated testing.<br>
4. Remove silos and improve the collaboration between the development and operations teams.<br>

DevSecOps may not be relevant for

- Applications that have been rolled out and is in maintenance mode with minimal change
- Commercially Off the Shelf (COTS) or Software as A Service (SaaS) tools without any coding

## Preparing for adoption

Agencies planning to adopt DevSecOps can look at the 3P – Practice, People, Platform – model shown below to achieve success.

![](05-3P-Model.png)

### Platform

Agencies should consider using the central Whole-of-Government (WOG) CI/CD toolchain in Singapore Government Tech Stack (SGTS) such as SHIP-HATS as DevSecOps policy has been co-developed with the central tech stack. If an agency is planning to set up their own platform, they might want to look at the [pricing analysis](https://sgdcs.sgnet.gov.sg/sites/IDA-GoSync/gdspdd-ai/ship/_layouts/15/WopiFrame2.aspx?sourcedoc=%7BACB6DFA8-2433-48B8-9A24-BABA8688B0F6%7D&amp;file=SHIP-HATS%20Competitive%20Pricing%20Assessment.pdf&amp;action=default&amp;IsList=1&amp;ListId=%7B609D81FE-D9DB-4B7D-8D1A-1F02CD38880C%7D&amp;ListItemId=80) that the SHIP-HATS team has prepared for comparison.

### Practice

This playbook will be outlining the necessary and relevant DevSecOps practices and it will also highlight the clauses that agency can fulfil.

### People

People are an important asset, and agency should ensure that the team is equipped with relevant skillsets in terms of automations, system and application security knowledge and an agile mindset. This is not just for practitioners; it extends to Agency leaders and business users so they can get the best out of it.

The table below defines some key roles and responsibilities for the team to consider. Do note that the list is not exhaustive. The development team can also double hat to perform multiple roles, especially for a small development team. For example, the same person can play either:

  - QA and Automation engineer roles; or
  - System and Application security engineer roles

However, agency needs to ensure there is no conflict of interest, that is the developer who wrote the code can't assign themselves as the reviewer.

| **Role** | **Responsibility** |
| :--- | --- |
| Release Manager | <ul><li> Defines security gate requirements and ensures these requirements have been met before any release.</li><br /><li>Plans and manages release activities and release cycles for the system to handle risks and to pre-empt any issues that may impact release scope, schedule and quality.</li><br /> <li> Coordinates release content and manages effort for the service request backlog, pending service requests, third-party applications, or operating system updates, deployment plans and checklists execution.</li><br /><li>Manages release repositories and key information such as build and release procedures, dependencies and notification list to coordinate work across teams.</li><br /><li> Makes continuous improvements in the release process and works with the development team to understand impacts of code branching and merging to ensure alignment across development team.</li></ul> |
| QA Engineer | <ul><li>Creates, executes and maintains automated test strategies and test cases/scripts.</li><br /><li> Ensures all environments required for testing are standardised and automated where possible.</li><br /><li>Performs periodic review of the automated test script/test cases results and provides assessment for the quality of all builds produced by the CI/CD pipeline.</li><br /><li>Continuously improving testing processes, test efficiency and techniques around test automation and integration with CI/CD pipeline.</li></ul> |
| Automation Engineer | <ul><li> Develops scripts and sets up necessary automation tools used to build, integrate, and deploy software releases to various platforms, including development and production environments.</li><br /><li>Automates the configuration management of development, quality assurance, and production workloads as well as the automation of CI of the codebase and the CD of releases.</li><br /><li>Designs, builds, optimises and monitors the automation systems solutions to identify system bottlenecks, production issues to maximise service availability.</li><br /> <li>Builds automation framework for deployment, management, monitoring of applications, as well as maintains the configuration and deployment tools to auto-scale the application platform.</li></ul>|
| System Security Engineer | <ul><li>Plans, implements, monitors and manages the overall system security architecture.</li><br /><li> Performs threat and risk assessments and applies secure configuration profiles to their systems.</li> <br /><li> Performs security checks such as infra level VA and troubleshooting.</li> <br /><li> Employs best practices when implementing security controls within an information system. </li></ul>|
| Application Security Engineer | <ul><li>Plans, implements and manages the overall application security architecture.<br /><li> Performs application threat modelling on their applications</li><br /><li> Confirms all security testing tools must be updated to its latest security checklists before scanning code packages, application and infrastructure components</li><br /><li> Implements and executes automated SCA, SAST and DAST for applications</li><br /><li> Performs triage on application security findings</li><br /><li>Performs penetration testing on the applications </li></ul> |

## Outsourcing Agile Projects

When outsourcing an agile project, do use the [Agile Tender template](https://sgdcs.sgnet.gov.sg/sites/tech/SNDigiGov/Programmes/GovICTProcRes/Pages/BulkTenders/ICTContractTemplates/STANDARD-IT-CONTRACT-TEMPLATE-FOR-PROVISION-OF-AGILEAPPLICATION-MAINTENANCE.aspx) to ensure the requirements and deliverables are written to match agile development. If you are choosing SHIP-HATS as your platform, here is an [AOR template](https://sgdcs.sgnet.gov.sg/sites/IDA-GoSync/gdspdd-ai/ship/_layouts/15/WopiFrame2.aspx?sourcedoc=%7B3F0806F6-0663-4D25-B670-120B87806C49%7D&amp;file=Sample%20AOR%20for%20SHIP-HATS%20Subscription%20(140621).pdf&amp;action=default&amp;IsList=1&amp;ListId=%7B609D81FE-D9DB-4B7D-8D1A-1F02CD38880C%7D&amp;ListItemId=88) that you can include for budget approval.
