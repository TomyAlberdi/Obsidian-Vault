Created: 2024-10-02 15:57
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[DevOps]]
-- -
Monitoring is a systematic process that is responsible for collecting, analyzing and utilizing information in order to optimally maintain computing resources and software according to business requirements.
Monitoring is a key process to ensure that everything works the way we expect and need it to. It gives us information to know if we are moving in the expected direction and alerts us about changes or corrections we should make. In short, it is an indispensable process when implementing a systems project. The bigger the project, the more important it is.
## Objectives
- Avoid and/or prevent problems that may arise AND be able to anticipate them.
- Understand what is happening in real time in our resources and keep them always aligned to our needs.
- Make analysis because it allows us to store events for later review.
- Observe and be accountable by communicating to the personnel involved.
## Benefits
- **Observe infrastructure and applications**:
  Modern applications are built and run on all types of architectures — monolithic, distributed, microservices, among others — that generate large amounts of data in the form of metrics, logs, and events. Through monitoring tools, we can collect, visualize, and correlate all the data from resources, applications, and services operating on cloud servers and data centers in one place.
- **Collect metrics for further analysis**:
  Monitoring resources and applications can be done in real-time and consumed through a centralized console that formats and presents that data in a readable way. It can also be done asynchronously, meaning collection and storage for later use.
- **Achieve specific results**:
  Each project is built under the influence of various interactions. Monitoring is key in managing each project and helps you achieve objectives by considering the context's evolution, strategies, hypotheses, assumptions, etc.
- **Manipulate actionable data**:
  Current monitoring tools allow us to export raw data, also known in English as raw data, to be graphed, stored, and/or processed by other data engines to obtain the visualization we need.
- **Improve operational performance**:
  By being able to set alarms and automate actions based on predefined thresholds, we can know exactly when a resource or series of resources from my operational platform is malfunctioning and take corrective actions to return it to normal.
- **Visibilize daily operations**:
  Having a unified operational view allows us to optimize the performance and use of resources. With detailed, real-time data, project managers, operators, and stakeholders can take actions and make decisions based on the information they receive.
### Infrastructure and Application Monitoring:
Before starting a monitoring process, it’s essential to ask ourselves what we want to observe, analyze, understand, measure, or what we’re interested in being alerted about. Think about it… Measuring hardware resources isn’t the same as measuring software services, processes, or API communications!
When defining the monitoring of our environment, there are two major categories to consider:
1. **Infrastructure:** It’s common to need monitoring for resources like storage systems, networks, databases, servers, etc.
2. **Applications:** Here, we’ll be interested in monitoring elements such as the number of requests, the number of failures produced by a web service, API call events, etc.
## Monitoring Tools:
The market offers a wide variety of products to consider. As we’ve discussed, our decision will depend on what we want to monitor, the cost, complexity, and learning curve.
All monitoring tools will fulfill the same functions across applications and infrastructure.
- Real-time traceability and observability.
- Alerts.
- Data storage for later analysis.
- Integrated metrics.
- Reports.
However, each tool will offer specific features depending on its version. Let’s take a look at the most popular ones and their functionalities.
### Datadog:
Security and monitoring platform for cloud applications. It gathers end-to-end tracking, metrics and logs so that applications, infrastructure and third-party services are fully observable. It is oriented to provide cloud services.
**Advantages**:
- Mature integration with different types of software through the use of APIs
- Great flexibility and versatility to configure dashboards in different ways.
- Extreme granularity on the services to choose to monitor.
### Nagios:
Widely used and open source network monitoring system. It monitors the equipment (hardware) and services (software) that are specified, alerting when the behavior is not as desired. Mostly used in on-premises environments, although it has additional services that aim to have a presence in the cloud.
**Advantages**:
- Automatic discovery of resources without the use of agents.
- Ticketing system.
- Environmental monitoring.
### Prometheus:
Time series database and a monitoring and alerting system. Time series store chronologically ordered data, measuring variables over time. Databases focused on time series are especially efficient in storing and querying this data. Cloud and on-premises functionality is available.
**Advantages**:
- Data modeling.
- PromQL Language.
### Cloudwatch:
Monitoring and management service that provides actionable data and information for on-premises, hybrid and AWS applications and infrastructure resources. It allows you to collect and access all performance and operational data in log and metrics format from a single platform. AWS Native, so it integrates easily and naturally with any AWS service.
**Advantages**:
- Correlation of records with metrics.
- Flow metrics.
- Log analysis using artificial intelligence.
## Metrics
Measurement is the process of comparing a pre-established unit of measurement with the element whose magnitude is to be measured and, in this way, understanding how many times the unit is contained in that magnitude.
We have to define a coherent structure of metrics to monitor in order to manage, optimize and report on all our services on a regular basis.
### Indicators:
They are the result of manipulating metrics to obtain information about behavior based on different variables. Both metrics and indicators can give us information to make business decisions related to the functionalities of the product or the platform where it is located.
What do we propose? Converting raw data into indicators will allow us to know our environment, control it and measure resources efficiently, be able to anticipate the market and optimize the effort in product development.
### Deviation:
It is the deviation from the predefined metrics that is usually manifested by the low performance of a service. Time and usage are factors that directly affect the performance of our environment.
This deviation in the configured metrics will help us to identify problems in our systems with enough time before major problems occur.
#### What to do when our systems have degradation?
- Evaluate the resources available vs. consumed against pre-established limits.
- CDM (CPU, disk and memory) are essential resources to check in our measurements.
- Have architecture maps showing the flow of data within the system.
- Review logs and history of any recent changes.
### Types of metrics:
#### Work metrics:
- **Performance**: The amount of work done by the system per unit time. Performance is usually recorded as an absolute number.
- **Success/Error**: Metrics representing the percentage of work that was executed correctly and those that have failed.
#### Resources metrics:
- **Utilization**: The percentage of time a resource is occupied or in use.
- **Saturation**: It is the measure of the amount of work that the resource is not yet able to handle, often on standby or queue.
- **Availability**: It represents the percentage of time the resource has to offer to requests.
#### Events:
- **Changes in the code**: Involves all types of code changes: modifications, compilations and/or bugs.
- **Alerts**: Events generated according to some pre-established parameter on some resource.
- **Autoscalling**: Automatic addition and/or subtraction of resources based on load or other pre-established configuration.