# Stage 4: Pre-release Testing

In this section we will look at the best practices for testing before a production release to ensure the previous code and features continues to work as expected.

## Testing Set Up

- Test environments
- Automating testing
- Review triage
- Role separation

## Test environments

Agency should consider establishing minimally two test environments:

1. CI test environment is a short-lived test environment where constant testing happens to support frequent releases. It also includes a sub-set of functional regression testing.
2. QA or Staging environment is a more stable test environment, similar to the production environment, with fewer releases and includes the following:

  - Exploratory testing on new features
  - Full regression testing
  - Dynamic Application Security Testing (DAST)
  - User playground or User Acceptance Testing (UAT)
  - Load &amp; performance testing
  - Accessibility testing

### Automating testing[#9.1/G1]

- As mentioned in [Stage 2: Development – Version Control](https://docs.developer.tech.gov.sg/docs/devsecops-playbook/#/development?id=version-control-71s1), the automated test cases and scripts should be stored in the respective central repositories such as SHIP-HATS, similar to how you maintain the codebase.
- [Peer-review](https://docs.developer.tech.gov.sg/docs/devsecops-playbook/#/development?id=code-merge-71s2-81g3) is recommended for QA engineers to review each other&#39;s test cases and scripts.
- Agencies can use those repositories to run automation and security tests in a CI pipeline.

### Review triage[#9.1/G3]
The automated and manual testing should be followed by a review triage. In this process, the development team looks into the test scan or reports with Application Security Engineer and includes the following

- Assess if the issues are &quot;Confirmed&quot; or &quot;False positives&quot;
- Only the Application Security Engineer can suppress &quot;False positives&quot; flagged during security testing.
- Track the &quot;Confirmed&quot; findings or bugs using an agile tracker tool such as the issue tracker tools in SHIP-HATS with a user story or bug and assign a severity for it.
- Assess the severity and build a mitigation plan. We highly encourage to address issues assigned as high and medium severity as priority before tackling on those tagged as low severity.
- Repeat this review triage in every sprint or after every test cycle.

### Role separation[#9.1/G4]

Here are the recommended roles for different quality checks ensuring there is no conflict of interest:

- Once a code is ready, other developers in the team who understand the context can perform [Peer Review](https://docs.developer.tech.gov.sg/docs/devsecops-playbook/#/development?id=code-merge-71s2-81g3) as described in Stage 2: Development.
- After peer review, the Quality Engineers tests the functionality against quality checks and Application Security Engineer reviews for [secure code practices](https://docs.developer.tech.gov.sg/docs/devsecops-playbook/#/development?id=coding-practices) as part of SAST and regression tests
- Project lead / Scrum masters ensures the process is followed and review outcomes are followed on.

All these processes are moderated by tools such as CODEOWNER which are used to enforce the role separation. CODEOWNER automates code review requests when a developer submits a pull request.

## Three Types of Testing

- Security Testing
- Functional Regression Testing
- Load & Performance Testing

### Security Testing[#9.1/S1]

Security testing uncovers vulnerabilities, threats and risks in an application and its infrastructure and makes the system more resilient to malicious attacks. Security testing types include dynamic application security testing (DAST), vulnerability assessment and penetration testing.

#### Dynamic Application Security Testing (DAST)

- We highly recommend using DAST tool within SHIP-HATS that is preconfigured for OWASP Top 10 standards which is industry standard.
- DAST is recommended for stable and bug-free test environment.
- Product Owner can create a user story for DAST to be conducted on a weekly basis or at the end of each sprint. This ensures security vulnerabilities are flagged earlier in the software development life cycle.
- DAST may not be relevant for commercial-off-the-shelf (COTS) products or software-as-a-service (SaaS) tools.

#### Penetration testing [#4.1/S1 - S8]

Agencies are required to conduct penetration tests for new and existing systems. Public officers can refer to the [IM8](https://intranet.mof.gov.sg/portal/IM/Themes/IT-Management/Security/Topics/Application-Development-Security.aspx) domain on Application Development Security (Standards Clauses following Policy Clause 4.1) for the guidelines, scope and frequency on performing penetration testing.

### Functional Regression Testing[#9.1/S2]

Functional regression testing ensures the new and previously developed features are working as expected. We highly recommend automating regression testing using Selenium and Appium based frameworks which are supported by SHIP-HATS.

Agencies can consider adopting the agile testing pyramid concept. Read [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) for reference.

Include automated security test cases which are not performed by security tools in functional regression testing.

**Best practices for functional regression testing**

#### Initial regression suite

- For every user story or feature, the development team should set a well-defined acceptance criteria. Acceptance criteria is a set of requirements, agreed by users and developers and must be met to mark the user story as complete. These criteria form a subset of the test cases. Every test case should be tagged to a story, forming the initial regression suite.
- Automated testing is highly encouraged, but not all test cases can be automated. If a team has manual test cases, they should create and manage them using SHIP-HATS test management tool for better tracking and reporting.
- This initial automated regression suite can be scheduled at nights or non-peak hours and the development team can look at the test results by the next working day to determine if there are any breaks in the code.
- If your application depends on third-party systems, it is recommended to create mock systems in CI pipeline or QA environments to replace actual third-party systems. For example, if your application requires systems like Singpass (SP) / Corppass (CP) to authenticate logins, consider mocking SP or CP login functionality by creating a stub login page.

#### End-to-End Test Cases

Acceptance criteria in a user story only covers the test cases related to the story. The QA engineer should also design end-to-end test cases and try to automate them as much as possible.

#### Full Regression Suite

End-to-end test cases and the initial regression suite forms the full regression suite. The full regression suite can be executed daily after office hours, to make sure all developed and tested features continue to work as expected. Combined with automated security test cases (if any), this regression suite forms the baseline test. Agency can then define the exit criteria for deploying to higher environments such as staging or production.

### Load & Performance Testing

Load & performing testing identifies bottlenecks in the system and establishes a load baseline for capacity planning. It is recommended for the staging environment and the underlying infrastructure should be similar to production to obtain a conclusive result.

Performance Testing checks if the application response is within the range defined by the team in the non-functional requirements. Hence, ensure response parameters are included in the non-functional requirements.

The performance test results will provide information on system throughput, response time, server utilisation such as CPU and memory. The team can identify the performance bottlenecks of the application by analysing the performance test results against the server logs generated and plan for mitigation.

## Other Test Types

Following are the optional tests agencies can consider based on their needs and resources available.

| **Test Types** | **Description** |
| --- | --- |
| Accessibility testing | Ensures that application can be used by people with disabilities. Agency can utilise SHIP-HATS to perform accessibility testing for web applications. |
| Migration testing | Verifies data integrity and ensures there is no data loss from legacy to new system during migration. |
| Disaster Recovery (DR) testing | Public Officers can refer to [DR Test Plan](https://intranet.mof.gov.sg/portal/getattachment/8a76a670-a486-4faf-a442-6e0d8a2ab381/attachment.aspx)[template](https://intranet.mof.gov.sg/portal/getattachment/8a76a670-a486-4faf-a442-6e0d8a2ab381/attachment.aspx) in the intranet. |
| Chaos testing | Ensures system works and defines a steady state by continuously, but randomly injecting failures in the production system to test the integrity and resiliency of the system and environment. |
