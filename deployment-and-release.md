# Stage 5: Deployment & Release

In this section we will look at the best practices on deployment and release safeguards, including the strategies.

## Safeguards [#10.1/S1, G1]

### Automate DevOps processes

If you have read this playbook so far, you would understand that automating DevOps is fundamental to a secure and good quality development.

- **Practicing Shift Left:** Agency should use automated tools for source code analysis, configuration management, patching and deployment, and secrets management as it minimises the risk of human error which can lead to deployment downtime, as well as potential security breaches. Using automated tools enable the &#39;Shift Left&#39; practice that identifies and prevents defects early in the software delivery process. If an agency doesn&#39;t have automated tools, they should ensure that their pipelines are manually reviewed by a release manager before proceeding to deployment. Refer to [Development](development), [Building and Packaging](building-and-packaging) and [Pre-release Testing](pre-release-testing) chapters on how SHIP-HATS supports automation.
- **Reducing Downtime:** Automating your deployments can also prevent unnecessary downtime since you can rollback based on the previous successful pipeline. Refer to [versioning](https://docs.developer.tech.gov.sg/docs/devsecops-playbook/#/development?id=version-control-71s1) on how to use it to manage different versions of an application.

### Handle secrets securely within a pipeline

- **Storing Secrets:** Do not hardcode secrets as plaintext within code, scripts, files, or service accounts. Minimally, inject secrets using CI variables and mark them as sensitive and write-only. This ensures that no one can view the contents of secrets, including those with view permissions to the pipelines and prevents contents of secrets from appearing in the build logs.
- **Rotation:** Agencies are strongly encouraged to rotate secrets periodically (between 6 - 12 months). Most of the leading cloud providers support automatic rotation of secrets. Alternatively, agencies can use a central secrets management service offered by GIG for a customised solution.

### Understand Identity and Access Management (IAM)

- **Least Privileged Model:** Enforce least privilege access rights to reduce the risk of internal or external attackers running bad code or gaining unauthorised access to cloud resources. Only designated personnel such as DevOps or Automation Engineers should have privileged access to create, edit, delete, and run deployment plans based on their deployment model. Only designated release managers should have the permission to approve deployment in production environment. Consider creating a service account with least privilege access rights when handling deployments within CI environment.
- **Review Privileges:** We recommend agencies to periodically review all privileged actions and validate they are legitimate and adhere to the compliance mandates.

### Securing production workloads [#10.1/G5]

- **Runtime Application Self-Protection** (RASP) is an application protection technology which resides within the application&#39;s runtime environment. It secures the application by intercepting all traffic from the app, validating those requests, and ensuring that potential attacks on underlying vulnerabilities are blocked before they are addressed. RASP provides visibility to security teams on the attackers, techniques used, and the applications targeted. RASP tools are easy to include in the pipeline and can be deployed along with the application without additional coding.

## Strategies [#10.1/G2, G3]

The list of deployment strategies is non-exhaustive, and agencies can consider other deployment strategies that may fit their specific use-cases.

| **Strategy** | How it works | Pros & Cons |
| --- | --- | --- |
| **Recreate Deployment** | A rudimentary form of deployment where older version of the application is stopped before deploying the new version. | ✓ Simple and cheaper to execute<br />✓ Works well in limited infrastructure <br /><br>☓ Incurs downtime until the new deployment is complete|
| **Rolling deployment** | A basic deployment strategy where all the instances or nodes within the target environment are incrementally updated with the newer version until completion. | ✓ No downtime for deployment<br />✓ Cloud providers offer automatic roll back for failed deployments<br />✓ Less risky as it is easy to rollback<br />✓ Works well for less complex deployments that do not require capacity testing in production<br /><br>☓ Takes a longer time to complete since it is done incrementally |
| **Canary releases** | This deployment rolls out new version in the same production environment as the current version and load balancer routes to a subset of users test it and then roll the changes out to the rest of the users. For example, route it to 2%, 25%, 75% and 100% of users in phases. | ✓ Allows verification and testing on live users<br /><br>☓ Potentially complex depending on the duration required for verification and testing in the production environment |
| **Blue-Green deployment** | This strategy runs two identical production environments, Blue and Green. At a time, only one environment is live and serves production traffic. By default, Blue contains the current application version serving production traffic while Green will contain the newer version which is currently idle. Upon passing a series of customised tests, the Green replaces the Blue and handles production traffic and finally the Blue gets destroyed. | ✓ Reduces the risk of deployment failure and downtime if executed properly<br /><br>☓ Running two identical environments can be costly<br />☓ Additional configuration to maintain data consistency across the two environments |
