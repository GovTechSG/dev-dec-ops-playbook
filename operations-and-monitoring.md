# Stage 6: Operations & Monitoring

It is vital to implement tools and processes to monitor their production systems and environments for:

- Detecting and responding to operational and security incidents.
- Measuring impact of the systems to the business. 
  >**Note:** Agency can refer to the IM8 on Incident Management to determine the impact of the incidents to the business.

## Factors to evaluate for implementing metrics

There are a few factors which you should evaluate before deciding on the metrics to track:

- **Resources available for tracking** – Scope tracking based on the resources- manpower, budget, and infrastructure available.
- **Usefulness of the metrics** – Track metrics that create value for the team since each additional metric increases the complexity of the system and takes up resources. Use-cases evolve over time, and the agency should constantly evaluate to optimise resources.
- **System criticality** – mission critical systems require a more extensive monitoring to ensure the stability. Less critical systems can afford to adopt a more general metrics monitoring as failure is less costly.

## Monitoring metrics

Agency should consider setting up a telemetry dashboard to setup alerts or notifications on anomalous activities. The list of items to monitor is non-exhaustive and should be considered based on the use-case.

### System monitoring

System monitoring evaluates the performance of underlying infrastructure where the servers are hosted. That includes metrics like server uptime, CPU performance, disk space usage and network performance.

### Application Performance Monitoring (APM)

APM observes how well applications perform given the current state of the environment, and how it interacts with the underlying environment and dependencies. APM metrics include success and error rates, application response rates, resource usage and performance, and latency.

### Security monitoring

Security monitoring evaluates the flow of traffic within the application and servers and detects unusual behaviour. It also detects activities such as unauthorised privileged processes running in the background, changes in OS or system policies as well as failed login attempts and deletion of audit logs.

### Monitoring systems

Agency can consider using the following cutting-edge technologies for their monitoring systems. Metrics mentioned earlier can also be configured in dashboards for both data visualisation and alerting purposes within these monitoring systems.

**StackOps is a monitoring component under SGTS**, that agencies can use to configure their dashboards to monitor the relevant metrics. Agencies interested to pilot StackOps can email [StackOps_SRE@tech.gov.sg](mailto:StackOps_SRE@tech.gov.sg).

|Technology|Description|
|---|---|
|**Elastic stack - Elasticsearch, Logstash, Kibana**|Elasticsearch, Logstash and Kibana are also known as ELK. This comprises of three open-source tools which are integrated to enable users to search, analyse and visualise logs generated from various systems.|
**Collecting data**|ELK uses beats, which are lightweight agents installed on servers to push metrics varying from application and server logs to network traffic and geospatial data. There are also community-contributed beats which gathers information based on specific use-cases.
**Processing data**|Logstash receives logs and events from various sources/beats, where it processes and parses the data according to the requirements.
**Storing data**|Elasticsearch is the core of the ELK stack, where it provides distributed data storage which can be highly available and fault tolerant. It also specialises in offering various query types for different data types.
**Visualising data**|Kibana is the visualisation tool of the stack which allows users to view agreeable data in customised dashboards. It also provides real-time data visualisation in a user-friendly interface and allows users to configure alerts based on the data received in ELK.


<!--

**Elastic stack - Elasticsearch, Logstash, Kibana**

Elasticsearch, Logstash and Kibana are also known as ELK. This comprises of three open-source tools which are integrated to enable users to search, analyse and visualise logs generated from various systems.

**Collecting data**

ELK uses beats, which are lightweight agents installed on servers to push metrics varying from application and server logs to network traffic and geospatial data. There are also community-contributed beats which gathers information based on specific use-cases.

**Processing data**

Logstash receives logs and events from various sources/beats, where it processes and parses the data according to the requirements.

**Storing data**

Elasticsearch is the core of the ELK stack, where it provides distributed data storage which can be highly available and fault tolerant. It also specialises in offering various query types for different data types.

**Visualising data**

Kibana is the visualisation tool of the stack which allows users to view agreeable data in customised dashboards. It also provides real-time data visualisation in a user-friendly interface and allows users to configure alerts based on the data received in ELK.
-->