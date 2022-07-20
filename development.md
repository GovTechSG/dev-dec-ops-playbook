# Stage 2: Development (Code)

In this section we will share DevSecOps best practices and guidelines for the development phase. The 2 key areas are:

- [Source Code Management](#source-code-management) - [#7.1, #8.1/G4]
- [Coding Practices](#coding-practices) - [#7.2 ]

## Source Code Management

### Why is source code management important?

Source code management1 (SCM) ensures single source of truth and efficient collaboration with developers. In the government context, it is important for agencies to be able to view the development code changes to **identify any vulnerabilities early on** , even when the project is outsourced. It is highly encouraged to manage the source code in a central repo such as the one hosted by [SHIP-HATS](https://www.developer.tech.gov.sg/singapore-government-tech-stack/toolchain/overview.html) in SGTS so that the Agency has **access to code base anytime**.

If vendors are unable to use the centrally managed code repo in SGTS for any of the existing outsourced projects, they should either allow the agency access to the vendor-managed code repository, or periodically synchronise (like end of each sprint) their code repo to the centrally managed one that the agency has access to.

<sup><i>[1] Source Code Management Mandate - All new and existing GovTech owned systems shall adopt SHIP-HATS for source code management by October FY22 and this was approved by GovTech IDSC in May 2021.</i></sup>

### Version control [#7.1/S1]

Every commit in the code repository that is released to production must be tagged with the version number and should have the supporting logs or commit history, so it is easy to see the changes that were released to production.

Version controlling should also be implemented not just for application codes, but also for:

- Automated test scripts or test cases.
- Scripts such as installation/build/deployment scripts, rollback scripts, migration scripts and CI/CD pipeline scripts.
- Infrastructure as Code (IaC) definitions, Application configurations including prerequisite software details and versions, database details, network details.
- Environment configurations including default settings.
- Project documentations or Standard Operating Procedure (SOP) that require review and/or approval. A good example is the Architecture Decision Record (ADR) - a simple and lightweight method to document any technical and architectural decisions and changes made. You can refer to this [Medium article](https://betterprogramming.pub/here-is-a-simple-yet-powerful-tool-to-record-your-architectural-decisions-5fb31367a7da) to find out how to use ADR, and their [GitHub](https://adr.github.io/) page for more tooling and templates.

### Code Merge [#7.1/S2, #8.1/G3]

**Short-lived branches**

Agencies should check in working source code to a short-lived branch at least once per day and merge to the main repository branch by a pull request at most after a couple of days to keep batch size small and detect merge problems faster.

To use short-lived branches, reduce the user stories into bite-sized tasks or subtasks that can be completed withing a day or two. This will also help to ensure that the pull requests can be reviewed and merged quickly. It is best to submit pull request as and when the code is ready and need not wait until the end of the sprint.

**Pull request to merge**

The production or release trunk should be protected, and code can only be merged to the protected trunk through pull requests.

Note to know more about release trunk, refer to [Understanding DevOps](#understanding-devops).

**Implementing peer reviews**

Peer review all pull requests and approve them before merging into the trunk. Do take note that a self-review of the pull request should not be accepted.

The main objective is to validate the correctness of the code and making sure that the changes implemented are aligned with the story or ticket that it is tagged to. If the reviewer can think of better ways of implementing the change, the reviewer can also make suggestions to improve the code. Once the code has been reviewed, the reviewer approves the changes and merge the changes into the trunk.

**Peer review guidelines**

- A peer reviewer can be another developer in the project, who understands the code base.
- The team should come together to discuss the code architecture and how their features may affect other parts prior to reviewing the code.
- There can be more than one reviewer, and the code review can be done online or offline.
- The batch size should be small to make the review less tedious. The developer can separate the code changes into logical sections (for example: frontend and backend) or separate them based on the tasks and subtasks in the ticket and submit multiple small pull requests for review.
- Review should include the changes in the tests such as what are new tests added or removed.
- Leverage on pull request to enable peer review of the code instead of pushing directly through to the trunk.
- The submitted pull request should pass all automated tests such as unit tests and builds in the CI pipeline before the reviewer can approve and merge the changes into trunk. Fix any failure in the CI pipeline before the pull request can be approved and merged.
- If there is any failure, notify the developer about the corrections to be made. Configure messaging apps to receive notifications so that developers get alerted. Examples of such notifications are automated tests fail, build failed or completed successfully, change in pull requests status such as created, merged, canceled or reviewer(s) adding comments for the code review.

## Coding Practices

### Style Guide

At the start of the project, the team should agree on a coding style guide. The style guide could contain recommendations on crisp and clear commenting &amp; documentation, consistent indentation, code grouping, consistent naming convention, as well as file &amp; folder organization for the application. A linter and formatter should be set up within the Integrated Development Environment (IDE) so that the agreed-upon style will be automatically applied to any code developed. Having a consistent style of code in the application will allow quicker and easier development, and the linter can even help to detect problems or bugs/vulnerabilities in the code. Logs for the application should also follow a fixed format/style so that it is easier for tools to parse and interpret the logs.

### Code "Smells"

Code smells refer to any characteristics in the source codes of a program that possibly indicates a deeper problem. To ensure the source codes are clean and maintainable (or free of &quot;smell&quot;), developers can find and integrate code &quot;smells&quot; plugins for their IDE, which helps to perform code &quot;smells&quot; automatically. One such example of a plugin would be the SonarLint IDE extension provided by SonarQube available within SHIP-HATS.

### Secure Coding Practices

Practicing secure coding reduces vulnerabilities and bugs in the application. There are many comprehensive guides out there and one of highly recommended guides is the [Secure Coding Practices Guide at OWASP.](https://owasp.org/www-pdf-archive/OWASP_SCP_Quick_Reference_Guide_v2.pdf)

Below are some important secure coding practices that agencies are encouraged to incorporate. Do note that this list is not exhaustive:

**Input validation**

- Validate all input data from clients such as parameters, headers, URLs.
- Validate the data types, data range, length, or use regex – regular expression - for each data input.
- Whenever possible, implement whitelisting over blacklisting.

**Authentication and password management**

- It is highly encouraged to use a central authentication service such as Singpass or Corppass, available on SGTS, instead of implementing a proprietary one.
- When the agencies can&#39;t use the central authentication services, at the very least, they should make sure the passwords are stored as cryptographically strong one-way salted hashes, to a table that can only be readable/writable by the application
- It is recommended to implement password complexity/length/non-reuse/expiry best practices.
- Disable the account if the login attempt fails for 10 times consecutively.

**Session management**

- Generate new session identifier for each authentication and implement session expiry and inactivity timeout suitable for the application.
- Do not allow concurrent logins with the same user account and revoke any of the previous sessions unless there is a business requirement to have concurrent logins.

**Access control**

- Periodically audit accounts and disable the inactive accounts and revoke the session identifiers.
- Enable proper access control to all restricted resources by authorised users, use a default deny approach to the restricted resources.

**Error handling and logging**

Errors are often an indication of bugs in the system that may lead-up future vulnerabilities.

- Address all errors and exceptions. There could also be a global exception situated at the top level of the code to catch any stray exceptions.
- Do not display debugging, stack trace or sensitive information in error responses.
- Do not store sensitive information in logs and restrict log access to only authorised individuals.
- Log errors with appropriate details for diagnosis and future mitigation.
- Store error logs on trusted systems.

**System configuration**

- Remove unnecessary system information in HTTP response headers.
- Remove any test code or any functionality not intended for production during deployment.
- Maintain separate configuration files for separate environments.
- Do not keep any secrets or sensitive information in your config files. Keep them in a secrets management service such as AWS Secrets Manager.

**Database security**

- Use strongly typed parameterised queries.
- Ensure application uses the lowest level of privilege when accessing the database.
- Ensure applications use different credentials for different trust distinctions. For example, user, read-only user and administrator.

**File management**

- When uploading files, limit file types by checking the file headers (checking file extensions is not adequate).
- Turn off execution privileges on file upload directories.
- Scan user uploaded files for viruses and malware.

### Unit testing

A unit is the smallest testable part of an application, and unit testing should be written to ensure that unit is meeting its intended design and behaviors. Developers should use a code coverage metric (both line coverage and branch coverage) to assist when writing unit tests. Aim to have a high code coverage like 85% and above but note that achieving 100% coverage might not necessarily mean that all possible test cases have been covered. For example, a code branch that has multiple conditions will report 100% line and branch coverage, if one of the conditions was covered in the unit tests. However, tests should still be written for the remaining conditions as well.

### Code refactoring

Code refactoring is the process of restructuring code without any modifications to external behavior to improve code consistency and make it simple for future developments.

**When to refactor?**

Refactoring can be done during code review to clean up the current code before the system goes live as well as at regular intervals to clean up low-hanging bugs, to remove duplicate codes, or simplify conditional expressions.

Tips for refactoring

- Remove unnecessary code such as unused references or functions and test cases.
- Extract duplicate code into common functions ([Rule of Three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming))).
- If functions or code have high complexity, consider breaking them down into smaller functions, modules or files.

### Software Frameworks

Choose software frameworks for your programming language with the following suggested guidelines:

- The framework is actively maintained
- Use the stable release version of the framework when compared to beta or pre-release versions
- Issues/bugs identified by users or security vulnerabilities that were discovered are frequently patched or fixed by the contributors
- The framework should already have inbuilt security features that will help make your application more secure. For example, automatic CSRF protection and SQL injection protection.
- The framework is an open source and the code is accessible for review.
- Take note of the software license for the framework. Make sure it is appropriate for your project and can be used in accordance with their license policy.


### Third Party or Open Source Libraries

Some suggested guidelines when using third party/open source libraries for your application

- Make sure that the versions of third party or open source libraries or packages are explicitly declared (i.e. version locked). Some package managers such as `npm` for NodeJS offer such capabilities by default, while others such as `pip` for Python require additional configuration or tools.
- When downloading the libraries or packages, it is recommended to use a hosted repository manager such as the one offered in SHIP-HATS. A hosted repository manager helps to cache and speed up downloads, ensures the security of the downloaded packages by verifying checksums and flags out any known vulnerabilities for the libraries.


### Other practices to consider

**Pair Programming**

Pair programming is an [agile software development](https://en.wikipedia.org/wiki/Agile_software_development) technique in which two software engineers work together at one workstation. One, the driver, writes [code](https://en.wikipedia.org/wiki/Source_code) while the other, the observer or navigator, [reviews](https://en.wikipedia.org/wiki/Code_review) each line of code as it is typed in. The two programmers switch roles frequently.

While reviewing, the observer also considers the &quot;strategic&quot; direction of the work, coming up with ideas for improvements and likely future problems to address. The driver can focus on execution details and the &quot;tactical&quot; aspects of the current task, using the observer as a safety net and guide.

**Test Driven Development (TDD)**

Do Test-Driven-Development (TDD) if you can, and you should get a 90%+ code coverage as a bonus. To learn TDD, visit [Scrum.org](https://www.scrum.org/resources/introduction-test-driven-development). Developer should also collaborate with the application security engineer to write automated security unit testing.
