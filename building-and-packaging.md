# Stage 3 : Building and Packaging

In this section, we will cover the best practices related to building and packaging your application.

The project management tools (such as the ones in SHIP-HATS) discussed in [Stage 1: Planning](planning), can help to streamline features tracking and bug fixes that are part of a build.

When developing a feature or fixing a bug, code changes should be tagged to the story card or ticket. For example, while fixing a bug, link the respective ticket ID in the code branch or include it in the title or description of the pull request. This allows the build pipeline to track the changes in the build, and the tickets in the project management tool to track if the pipelines have passed or failed. The pipeline artifacts or results by external tools like SAST scans can be tagged with the ticket ID to link them to the feature/bug.

A CI pipeline should be configured to perform the build based on the feature branches in the repository, or when there is a pull request to merge into a target trunk.

## Automating Pipeline [#8.1/G5, G7]

Configure the CI pipeline to run automatically based on certain triggers. Different portions of the pipeline can be triggered at different times. Examples include:

- Triggering automated unit and integration tests, SAST scans, linting or formatting after every commit so errors can be caught early.
- Triggering slower tests such as UI or end-to-end tests at scheduled timings, such as at the end of each day to avoid impacting the developer's work.
- Triggering automated builds after each pull request has been merged into the main trunk so that the package can be deployed into the QA or UAT environment for testing.

We highly recommend that pipelines are triggered automatically. However, manual triggers are acceptable in certain scenarios, such as to test the configuration of the pipeline itself, or to rerun if something in the pipeline failed.

**Build history:** For audit and tracking purpose, configure the CI pipeline to maintain/keep the execution history and logs for at least one year. By default, CI tools in SHIP-HATS, tracks the history of the pipeline executions. Some CI pipeline tools allow you to save temporary artifacts like test results and log files for each build of the pipeline as well. The CI tools in SHIP-HATS keeps these artifacts for the last 10 builds. These artifacts can also be downloaded and persisted elsewhere for audit and tracking purposes.

## Static Application Security Testing [#8.1/S1, G8, G9]

Static Application Security Testing (SAST) is a testing methodology that analyses source code for vulnerabilities without executing anything and provides feedback early in the development cycle. This helps to reduce the cost of bug fixing. SAST is programming-language dependent.

**When to perform SAST?**

A full SAST scan must be performed on the repositories whenever code is merged into release/production trunk. However, it is recommended to run the full SAST scan at least once a month or in each sprint, especially if the application is not released frequently. After the scan, the results should be reviewed by the team. This is also a good chance for the developers and security engineers to collaborate and discuss [secure coding practices](https://docs.developer.tech.gov.sg/docs/devsecops-playbook/#/development?id=secure-coding-practices) and learn from each other as they review the scan results.

**Tools** : We highly encourage using SAST tools within SHIP-HATS which have been configured for security standards and here are the [languages and frameworks supported](https://www.microfocus.com/en-us/fortify-languages).

**SAST Triage**

- **Scan Review:** After the scan, the developers and the Application Security Engineer should review the scan results. If there are any false positives in the scan results, the developers should justify why it is a false positive. The Application Security Engineer will make the decision on whether the error can be suppressed and mark it as a false positive.
- **Mitigation:** Minimally, the high and critical issues flagged in the scan results should be mitigated as soon as possible (ideally within the sprint itself). Issues flagged as low or medium can be resolved subsequently when there is available time (See [IM8](https://intranet.mof.gov.sg/portal/IM/Themes/IT-Management/Security/Topics/Application-Development-Security.aspx)(5.1/S3) for timeframe for vulnerability management). In the meantime, risk assessment can be performed for the low and medium risks until they are fixed.
- **Technical Debt:** Because the low and medium severity issues are not resolved immediately, do ensure that time is allocated in the subsequent sprints to address and mitigate the remaining issues.


## Software Composition Analysis [#8.1/S2]

Software Composition Analysis (SCA) scans your application on third-party or open-source software components for any known vulnerabilities. It can work on both source code and binaries. Most often the vulnerabilities discovered can be fixed if the team applies the patch or latest version of the third-party libraries. SCA can also flag any unknown or modified components that your application is using, so that you can identify these components as much as possible.

**SCA Triage**

- **Mitigation** : If there are newer versions of the third-party library that have fixed the vulnerabilities, the development team should update to that version as soon as possible. Otherwise, they may also consider downgrading the version of the third-party library, provided that the older version does not have other vulnerabilities as well.

## Risk Assessment

Sometimes, there are vulnerabilities in the SAST or SCA scan that cannot be fixed immediately. For example, a third-party library in SCA scan does not have the fix yet, and hence the team is unable to update the library version.

In such scenarios, the team should perform a risk assessment. The risk should be added into a risk register and the relevant authorities such as the agency should approve and accept the risk. One example of risk acceptance is when the vulnerability in the library lies in a section of the library that is not being actively used by the application, hence it would not impact the application. Public officers can refer to the [IM8 Risk Management](https://intranet.mof.gov.sg/portal/IM/Themes/IT-Management/Set-policies,-standards-and-guidelines-for-ICT-man/Topic/Risk-Management.aspx) in the intranet site for more information and to access the risk register template.

### Digital Signature [#8.1/G11, G12]

Digital signatures are used to verify integrity and ensure security of the artifacts such as executables, code packages, or mobile app binaries such as Android App Bundle (AAB), Android Application Package (APK) and iOS App Store Package (IPA) files. During deployment, verifying a digitally signed artifact will ensure that the artifact was not maliciously edited or changed in any way. A digitally signed artifact also ensures that the artifact was legitimately built/packaged by a known service.

- The digital signature process begins with creating a cryptographic hash of the data (in this case it is the build artifact). This hash value is also known as a [digital fingerprint](https://www.sciencedirect.com/topics/computer-science/digital-fingerprint) and is a unique value. This is then signed with the user&#39;s private key, and the resulting value is appended to the build artifact. This artifact can then be pushed to an artifact repository such as Nexus Repository offered by SHIP-HATS.
- During the build process, only authenticated and authorised users can send software artifacts for the signing process and the team must use the signed certificate which is issued by trusted Certificate Authority.
- During release or deployment, the Release Manager can then verify the authenticity of the artifact by manual or automatic decryption of the digital signature, before approving the artifact for production release.
