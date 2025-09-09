[!INCLUDE [header_file](../../../includes/sol-idea-header.md)]

This architecture showcases how to build a scalable, secure, and intelligent real-time analytics solution using Azure Service Bus and Microsoft Fabric Real-Time Intelligence (RTI). Designed for cloud architects, data engineers, and retail solution strategists, it enables actionable insights from high-velocity data streams - ideal for scenarios like personalised product recommendations, dynamic pricing, and inventory optimisation. 

### Scenario: Personalized Recommendations

Imagine a customer browsing a retail app. As they interact—clicking on products, adding items to their cart, or scanning loyalty cards in-store—these events are streamed in real time. The system analyses this behaviour instantly to recommend complementary products, apply targeted discounts, or alert staff to restock shelves. 

## Architecture

:::image type="content" source="../media/fabric-rti-service-bus.png" alt-text="Diagram that shows an architecture for implementing near real-time analytics in Fabric with Azure Service Bus." lightbox="../media/analytics-service-bus.png" border="false":::

*Download a [Visio file](../media/MicrosoftFabricRTIServiceBus.vsdx) of this architecture.*

## Architecture Components 

### Data Ingestion
**1. Azure Service Bus (Integration in Preview)**
The Service Bus receives discrete, transactional events such as inventory updates, purchase transactions, loyalty program updates and customer feedback submissions.  
_Example: A customer redeems loyalty points at checkout—this triggers a Service Bus message updating their profile and inventory._

**2. High velocity data ingestion**
High velocity data that is continuous can be ingested directly into the Eventstream with a sub-second latency. 
_Example: A user browses 20 products in 30 seconds – clickstream data flows into Eventstream for immediate analysis._

**3. Microsoft Fabric Eventstream**
The Eventstream allows you to bring real-time events into Fabric, transform them, and then route them to various destinations without writing any code. 
_Example: Automatically enrich clickstream data with product metadata before routing to analytics._

### Storage and Querying
**4. Eventhouse**
Real-time event data is stored here and queried using the Kusto Query Language (KQL).  
_Example: Query all purchases of “wireless headphones” in the last 5 minutes across Melbourne stores._

**5. Lakehouse (optional)**
Data is made available for additional use cases such as synching to external systems or SQL endpoint compatibility via the Lakehouse. 
_Example: Run monthly sales trend analysis using SQL on historical data._

### Action Systems
**6. KQL Queryset**
KQL Analytics supports data discovery through time-series analysis, text parsing, geospatial queries, vector similarity search, anomaly detection, outlier detection, pattern discovery, creation of statistical models and more.   
_Example: Detect anomalies in checkout behaviour – eg sudden cart abandonment spikes_

**7. Real-time Dashboards and Power BI**
Visualise insights and actions in near real time.   
_Example: Store managers view live dashboards showing top-selling items and customer sentiment._ 

**8.Data Activator**
Monitors live streams and triggers actions based on patterns. Data Activator can monitor at various stages including from the Eventstream as part of ingestion or from the reporting layer. Actions include Teams notifications, email, Fabric items (such as running a pipeline or notebook) or Power Automate flows. 
_Example: If a product’s stock drops below threshold, trigger a restock workflow._

### AI Capabilities
**9. AI Data Agent**
Data Agents expose the data connected to Eventhouse for conversational experience against real time data. Copilot Studio can be leveraged to expose this chat experience directly in Teams, or AI Foundry can be used for app-based chat experiences.  
_Example: Provide natural language interface for store managers to ask “What are the top selling items in the last 5 minutes?”_

### Security and Governance
Security and governance are foundational to this architecture: 
* **Microsoft Purview Integration**
  Apply data classification, lineage tracking, and access policies across Fabric workloads. 
* **Role-Based Access Control (RBAC)**
  Ensure only authorised users can access sensitive data streams and dashboards. 
* **Data Encryption**
  All data in transit and at rest is encrypted using Azure-native mechanisms. 
* **Audit Logging**
  Monitor access and transformations for compliance and operational transparency. 
* **Event-Level Filtering**
  Use Activator to suppress or redirect sensitive events based on business rules. 
* **Conditional Access and Private Networking**

## Common Challenges Resolved
**1. Latency and Scalability Bottlenecks**
RTI enables sub-second latency for streaming analytics, allowing organisations to ingest and process billions of events per day without manual scaling.  It supports automatic scaling and low-latency ingestion from diverse sources like IoT devices, telemetry systems, and customer interactions. 

**2. Fragmented Data Streams**
RTI unifies internal and external streaming sources into a central Real-Time hub, eliminating silos and enabling holistic operational visibility. 

**3.Delayed Decision-Making**
Real-time dashboards and alerting mechanisms (e.g. via Power BI, Teams, or automated workflows) empower instant responses to anomalies, SLA breaches, or operational triggers.  

**4. Observability and Monitoring Gaps**
RTI supports open telemetry standards, enabling cost-effective observability. 


## Example use cases 
### E-commerce 
* Monitor performance metrics and user behaviour across platforms. 
* Detect anomalies in transactions, page load times, and conversion funnels. 
* Enable proactive issue resolution and personalised experiences. 

### Education 
* Stream data from campus transport systems, security cameras, and access control points. 
* Monitor student safety, optimise shuttle routes, and respond to incidents in real time. 

### Financial Services 
* Handle high-throughput transaction events from ATMs, mobile apps, and payment gateways. 
* Use anomaly detection models to minimise fraud, improve compliance, and enhance trust. 

### Healthcare 
* Transmit telemetry data from IoT-enabled medical devices to backend systems. 
* Analyse data streams for anomalies and trigger alerts for proactive care. 
* Improve patient outcomes through real-time monitoring and intervention. 

### Hospitality 
* Stream booking, occupancy, and housekeeping data to optimise room allocation and cleaning schedules. 
* Enhance guest experience through real-time service coordination. 

### Manufacturing 
* Stream telemetry from factory floor equipment to detect anomalies in vibration, temperature, and pressure. 
* Enable predictive maintenance to reduce downtime and improve worker safety. 
* Apply AI-powered video/image analysis to live camera feeds for defect detection and quality assurance. 
* Monitor production metrics and defect reports to detect bottlenecks and optimise throughput. 

### Quality & Safety Compliance 
* Detect unsafe worker behaviour, PPE violations, and hazardous conditions via environmental sensors and video feeds. 
* Trigger real-time alerts and automate incident reporting for regulatory compliance. 

### Site Reliability & Software Engineering 
* Stream deployment telemetry and error logs to detect regressions and failed rollouts. 
* Unify application, infrastructure, and user telemetry into real-time dashboards. 
* Monitor system health, detect bottlenecks, and correlate incidents. 
* Expose real-time data streams via Fabric Eventstreams and KQL for dynamic user experiences and operational insights. 

### Social Media Monitoring 
* Ingest and analyse real-time social media streams to detect sentiment shifts, trending topics, and brand mentions. 
* Trigger alerts for PR crises, customer complaints, or viral content. 
* Support dynamic engagement strategies and campaign optimisation. 
 
### Transportation 
* Stream GPS and sensor data from vehicles, planes, and ships. 
* Optimise routes, traffic, weather schedules, and fuel efficiency. 
* Enhance customer experience through real-time updates and coordination. 

### Utilities & Energy 
* Collect smart meter data to identify outages, consumption anomalies, and peak load patterns. 
* Enable dynamic pricing and predictive infrastructure maintenance. 

## Next steps

- [Azure Service Bus samples](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-samples)
- [Microsoft Fabric Real-Time Intelligence End-to-End Sample](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/sample-end-to-end) 
- [Explore Real-Time Analytics in Microsoft Fabric](https://learn.microsoft.com/en-us/training/paths/explore-real-time-analytics-microsoft-fabric/)

## Related resources

- [Microsoft Fabric Real-Time Intelligence](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/)
- [Microsoft Fabric Real-Time Hub - Azure Service Bus](https://learn.microsoft.com/en-us/fabric/real-time-hub/add-source-azure-service-bus)
- [Microsoft Fabric Eventstream - Azure Service Bus](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/event-streams/add-source-azure-service-bus)
- [Alerting and acting on data from the Real-Time Hub](https://blog.fabric.microsoft.com/en-ca/blog/alerting-and-acting-on-data-from-the-real-time-hub)
- [How to create a data agent](https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent)
