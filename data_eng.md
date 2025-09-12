Here is a briefing document in Markdown format on building reliable data products, drawing from the provided sources:

---

# Briefing Document: Building Reliable Data Products

## 1. Foreword and Introduction

Building and scaling data products is a complex and challenging endeavor, yet data has evolved from a "nice-to-have" to a critical component of core business processes. Modern data stacks are increasingly intricate, with some dbt projects having over 1,000 models, leading to slower velocity, harder collaboration, and increased errors. Many data teams lack a clear framework to address these growing expectations and struggles, often leading to sporadic testing, unclear ownership, alert overload, and a loss of trust in data.

**The Definitive Guide to Data Products** provides a practical guide and clear framework to help data engineers, analytics managers, and broader data teams design, build, deploy, and operate data systems that reliably drive meaningful business value. The core recommendation is a **5-step framework called The Data Product Reliability Workflow** to think systemically about data stack reliability.

## 2. The Data Product Reliability Workflow

This framework outlines actionable steps to define data use cases as products, set ownership and severity, deploy strategic tests and monitors, and establish quality metrics.

The five chapters (and their corresponding steps in the workflow) are:

*   **Chapter 1: Introduction**: Outlining the clear relationship between data reliability and business impact.
*   **Chapter 2: Setting Expectations**: A framework to define data products to manage tiers of data assets and Service Level Agreements (SLAs) for maintenance.
*   **Chapter 3: Proactive Testing & Monitoring**: Building a testing and monitoring framework that maximizes error detection and minimizes alerts.
*   **Chapter 4: Ownership with Rapid Response**: Developing scalable ownership and efficient incident management processes to quickly resolve issues.
*   **Chapter 5: Continuous Improvement**: Establishing feedback loops and learning processes to continuously enhance data reliability practices.

**Reliable data is not just an operational requirement but a competitive advantage**, fostering trust and enabling faster, more critical processes.

## 3. Setting Expectations (Chapter 2 Summary)

### 3.1 What is a Data Product?
A **data product is a group of data assets structured based on their use case**. Well-defined data products clarify ownership, guide testing and monitoring strategies, and enable consistent SLA management aligned with consumer expectations. They often rely on input from other data products or operational systems, so their expectations should consider the entire lineage.

Benefits of defining data products include:
*   **Untangling Lineage**: Helps understand dependencies across complex data stacks, speeding up root cause analysis and system design decisions.
*   **Clear Ownership**: Makes it easier to trace issues to faulty upstream data products and identify owners for escalation.

### 3.2 Identifying Data Products
**Focus on the most critical business processes your data team supports**. Signals for critical data products include those impacted in recent failures or assets with high company-wide usage.

Examples of data products:
*   A set of dbt models and metrics in a specific dbt folder (e.g., a finance mart).
*   A group of dbt models linked by an exposure (e.g., models for a customer lifetime value (CLTV) model powering marketing automation).
*   A collection of dashboards in a BI tool (e.g., core KPI reporting).

Data products can be classified as **producer data products** (read from operational systems, owned by data/platform engineers) or **consumer data products** (expose data to consumers, read from other data products, owned by data analysts/scientists). Start by identifying a handful of the most important ones and expand from there. Granularity is key; for example, "Attribution data product within Marketing" is more impactful than a high-level "Marketing" data product.

### 3.3 Defining Data Products
Once identified, data products should be defined following five steps:
1.  **Close to use**: Reflect the data consumer's experience.
2.  **Upstream dependencies**: Account for dependencies as far upstream as possible for a complete overview.
3.  **Owner**: Assign a responsible owner for continuous monitoring and lifecycle operations.
4.  **Priority**: Assign an importance level (e.g., P1, P2).
5.  **Description**: Provide context for people with less background.

Group data products into domains (e.g., Sales, Finance, Marketing, Core, API) to manage them more easily and map priorities. Definitions should align with existing workflows for ownership and priority. Automated lineage tools (data catalog, dbt, data reliability platform) are recommended for managing dependencies rather than manual tracking.

### 3.4 Determining the Priority of Data Products
Priority guides workflows such as issue response time and SLA requirements. Defining data products at the right granularity makes priority assignment easier (e.g., Attribution Reporting vs. Market Research within Marketing).

Example priority levels:
*   **P1 (Critical)**: Product operations, user-facing systems, direct impact on product functionality.
*   **P2 (Business Critical)**: Client exports (direct customer impact, non-operational), analytical data feeding operational systems with indirect customer impact (e.g., marketing automation, critical business decisions).
*   **P3 (Important)**: Business intelligence (standardized reports for strategic/tactical decisions).
*   **P4 (Exploratory)**: Every other use case.

It's crucial to **get executive buy-in for priority definitions**, as not everything can be P1, especially in larger teams.

### 3.5 Establishing SLAs for Data Products
An **SLA (Service Level Agreement)** defines expected service levels, including remedies for unmet expectations. For data products, SLAs can specify uptime, response times, and resolution times based on priority (e.g., P1 dashboard: 99.9% uptime, 30 min response, 2-hour resolution; P3 dashboard: 95% uptime, 48-hour resolution).

**Measuring data product SLAs directly ties to the experience of data consumers**, making it a more effective quality metric than general test coverage. Two key metrics are recommended:
*   **Coverage**: Percentage of assets with required data controls.
*   **Quality Score/SLA**: Percentage of controls passing successfully, based on Service Level Indicators (SLIs).

Both metrics should be monitored across the entire data product lineage, including upstream dependencies. Example coverage expectations for P1 data products include freshness checks on all sources, accuracy checks on key metrics, row count tests before/after joins, and not_null/uniqueness tests on key fields.

**SLIs** group data controls into meaningful areas to identify problematic areas:
1.  **Accuracy**: Does data reflect real-world facts?.
2.  **Completeness**: Is all required data present and available?.
3.  **Consistency**: Is data uniform across systems/sources?.
4.  **Uniqueness**: Are there no duplicate records?.
5.  **Timeliness**: Is data updated and fresh?.
6.  **Validity**: Does data conform to required formats and rules?.

SLA is calculated as `sum(errored SLIs) / sum(SLIs)`. Automated grouping of SLIs is highly beneficial. Setting explicit **Service Level Objectives (SLOs)** for each SLI can be useful if a data product has different sensitivities (e.g., an ML model training set might prioritize accuracy/completeness over timeliness).

**SLA levels and remediation expectations** for 1,000 data checks:
*   **99.9% reliability**: 1 failure (43 minutes downtime).
*   **99.5% reliability**: 5 failures (3.6 hours downtime).
*   **99% reliability**: 10 failures (7.2 hours downtime).
*   **95% reliability**: 50 failures (1.5 days downtime).
*   **90% reliability**: 100 failures (3 days downtime).

SLAs can be contractual (e.g., for customer-facing dashboards) or serve as internal guidelines to align teams. Incident management processes should be aligned with data product priority and SLA.

## 4. Proactive Testing & Monitoring (Chapter 3 Summary)

### 4.1 Anti-Patterns in Testing
Common suboptimal approaches to testing and monitoring include:
*   **Redundant Testing**: Applying tests (e.g., `unique`, `not_null` in dbt) without considering the broader data pipeline. This often means re-testing conditions that cannot possibly change downstream, leading to unnecessary computing costs, a false sense of safety, and alert clutter.
*   **Disconnected Tools**: Using multiple disparate tools for data quality (dbt for testing, separate anomaly monitoring, ETL pipeline monitoring) leads to fragmentation and unactionable alerts, especially when a single upstream failure can trigger hundreds of downstream alerts.
*   **'Test/Monitor All'**: Attempting to test or monitor every table or anomaly pattern, which often results in noisy alerts, cascading anomalies, and a higher volume of alerts without increased urgency to fix them. A wholly tested data stack is academic given varying reliability expectations across use cases.
*   **Focus on Models**: Prioritizing 'every model should be tested' without distinguishing between production-critical and experimental code. Unlike software engineering, analytics systems often mix experimental code with critical data in the same DAG, leading to a need for more nuanced testing based on use case criticality. This often means many data platforms feed into dozens or hundreds of use cases with vastly different reliability guarantees.
*   **Alert Overload**: The culmination of these anti-patterns leads to teams "drowning in large volume of hard-to-action, unclear, or unimportant alerts".

A better, more strategic approach is needed to minimize alerts, reduce complexity/cost, and maximize issue detection.

### 4.2 Designing a Testing Strategy
The recommended approach shifts from model-centric to **pipeline-centric testing**.

#### 4.2.1 Testing Pipelines, Not Models
A **data product pipeline is a direct acyclic graph of its upstream dependencies**, encompassing all models, tables, and processes from source to product. This approach offers several benefits:
*   **Severity Back-Propagates**: Models feeding a P1 data product must be treated with P1 priority.
*   **Clearer Impact Assessment**: Failures are directly linked to the product, improving cross-team communication.
*   **Feedback on Architecture**: Helps identify how much use cases are tangled across different priorities, highlighting risks of impacting critical systems.
*   **Focus**: Concentrates efforts on pipelines feeding highly critical products.

To enable pipeline-centric testing, new tools are needed to:
1.  **Anchor data product definitions into observability and catalogs**, using lineage to identify dependency chains.
2.  **Create pipeline automation workflows** to govern, monitor, and test specific pipelines, and improve system architecture.
3.  **Establish data product pipeline oversight** by reasoning about failure rates, SLAs, and incidents by pipeline, not just overall test coverage.

#### 4.2.2 Testing Layers
Testing should also be structured in **layers**, similar to data architecture (raw, staging, mart layers; or bronze/silver/gold). This helps:
*   **Alignment**: Slices the testing problem into smaller parts, clarifying expectations for data assets.
*   **Common Standard**: Classifies testing decisions by strategy, aligning the team.
*   **Removing Redundancies**: Eliminates retesting the same context across layers, aiming for a **"minimum, ideally one, test or monitor to fail"** for any potential failure mode.

SYNQ's layered approach:
1.  **Pipelines**: From data source to analytical system (first layer of tables, ETL, raw data lakes, streaming).
2.  **Sources**: First layer of data in the data warehouse where SQL transformations/tests can be applied (e.g., dbt sources).
3.  **Transformations**: Layers for cleaning, modeling business concepts, creating core data models.
4.  **Marts**: The final layer where data leaves the platform for specific use cases.

The strategic approach combines data testing and anomaly monitors, minimizes redundancy, and designs tests to complement each other.

### 4.3 Testing Sources
A **source** is the collection of data assets ingested from third-party or internal systems, representing **the first layer of data under the data team's control**. This often aligns with dbt sources.

**Why invest in testing sources?**:
*   **Interface**: It acts as an interface separating data team systems from upstream business systems.
*   **Early Detection**: Detects issues in input data, verifying assumptions about data arriving from sources.
*   **Ownership Alignment**: Clearly distinguishes ownership between data analytics teams (downstream) and data engineering/operations teams (upstream).
*   **High-Leverage Activity**: Verifies the quality of data that feeds every other model in the system, impacting the largest number of downstream dependencies.
*   **Starting Point**: **"When in doubt about where to start with testing, start with sources."**.

**What does a well-tested source look like?**:
*   **Data Presence and Completeness**: `not_null` and empty value checks.
*   **Uniqueness**: `unique` tests on primary keys and combinations of columns.
*   **Testing Values**: Explicit `accepted_values` for low cardinality fields to catch deviations.
*   **Testing Format of Values**: Min/max logic for numeric values or regex for string formats (e.g., email) to detect corrupted records at scale.
*   **Monitoring Ingests of Data**: Critical for detecting broken data flows:
    *   **Freshness Testing**: Deterministic tests for strict SLAs (e.g., dbt source freshness).
    *   **Freshness Monitoring**: Anomaly monitoring for sources with less specific, seasonal, or complex update frequencies, learning from historical patterns.
    *   **Volume Monitoring**: Anomaly monitoring for data volume fluctuations, especially with business growth and change.
    *   **Monitoring Deeper**: Segment-level volume monitoring (e.g., per event for website traffic) to catch nuanced changes unnoticed by table-level checks.

This approach is more extensive than "one test per model" but can be scaled with automation once the strategy is defined.

**Role of Data Contracts**: Data contracts define the structure, format, semantics, quality, and terms of use for data exchange. Well-tested sources and data contracts are **complementary techniques**. Contracts define *what* should be tested, while tools like dbt or SYNQ serve as the execution environment for these tests.

### 4.4 Testing Transformations
With a robust source testing strategy, **transformation layers can have much lighter testing suites, focusing only on what has changed**. This differs from model-centric testing by considering upstream tests.

Key types of transformations prone to errors and essential to test include:
1.  **Data Cleaning and Normalization**: Simple logic, but often a source of redundancy if retested after being covered at the source.
2.  **New Combined/Derived Columns**: Introduce new business logic; treat the model creating them as their "source" and test deeply, proportional to logic complexity. Unit testing (seeding data, executing logic, asserting output) can be beneficial for complex derived columns, but be mindful of higher maintenance costs.
3.  **Table Joins**: Notoriously error-prone, especially due to unexpected duplicates leading to "fanout". Strategies include:
    *   **Row Count Validation**: Comparing row counts before and after a join to ensure no unexpected rows were created, especially for enrichment joins.
    *   **Verify Cardinality of Join Keys**: Using tests like `dbt_utils.cardinality_equality` to ensure distinct values in joining columns match expectations.
4.  **Data Aggregation**: Changes row counts and creates new measures. Can be complex due to grouping granularities and window functions.
5.  **Data Structuring and Reshaping**: Fundamental regrouping of table structure.

### 4.5 Testing Products
The final layer, often called data mart, contains data products ready for business consumption. Testing here shifts focus: **"Instead of focusing on technical aspects of data, when testing data products, we verify the logic encoded in SQL transformations."**.

This approach is akin to **integration testing** in software engineering, where large pieces of software are tested together. For data products, this means **mimicking real-world queries specific to the use case and asserting the correct response**.

Types of tests for data products include:
*   **Regression and Business Logic Tests**: Using dbt singular tests (SQL queries to isolate faulty data) to catch logical issues anywhere in the system, mimicking actual business queries. Examples include checking for negative time-to-resolution or percentage values outside 0-100. These also serve as **regression guards** by replicating and testing against past issues.
*   **Historical Consistency Testing**: Verifying that historical data (e.g., number of resolved incidents) remains consistent over time by comparing live queries against historical snapshots. Use with caution, as it can be expensive to maintain if calculations legitimately change.

This end-to-end verification complements source and transformation testing by providing final confirmation of system reliability.

## 5. Ownership with Rapid Response (Chapter 4 Summary)

As data stacks grow, clear ownership and efficient incident management become crucial to **reduce time to resolution, ease debugging, prompt upstream teams to improve data quality, and systematically enhance domains**.

### 5.1 Getting Started with Ownership
Key steps to implement ownership:
1.  **Integrate Metadata**: Use a central place (dbt metadata, data catalog) to define ownership.
2.  **Define Data Products**: Start with the most important data products, where stakes are highest.
3.  **Assign Ownership**: Based on responsible teams or individuals, ideally using existing groups (e.g., Google Groups).
4.  **Deploy Data Controls**: Strategically place monitors based on owners' domain knowledge.
5.  **Notify Relevant Owners**: Activate ownership through targeted alerting or escalation to incident management tools.

### 5.2 Defining Ownership
Ownership should ideally be defined across the entire data lifecycle, from input layers to consumer-facing marts:
*   **Input Layer**: Clear ownership at sources for unambiguous escalation paths to upstream engineering teams.
*   **Staging and Transformation Layer**: Analytics engineers assign ownership of models using dbt metadata (owner tags, dbt groups).
*   **Consumer-Facing Marts**: Organized by use case, with relevant stakeholders (e.g., Technical Account Management) assigned as owners.

**"More than 50% of our data assets above are already encapsulated into data products making the ownership seamless to define."**.
Use **existing owner groups** (e.g., Google Groups, Slack channels) for scalability and auto-updates. Ownership definitions should closely follow data product definitions (e.g., Marketing Attribution Data Product owned by marketing data). Set ownership at the **team level** for scalability, rather than too high (e.g., "data-team") or too granular (individual level).

Methods for defining ownership:
*   **Existing Folder Structures**: If dbt projects or data warehouse schemas are already organized by ownership (e.g., marketing, finance).
*   **dbt Owner Meta Tags**: Built-in support for `meta: owner` tag in dbt, visible in dbt Docs. Can be extended to dbt sources and enforced with CI checks.
*   **dbt Groups**: Encapsulates internal logic, useful for larger dbt projects, enabling private access to models within a group.
*   **Cross-Tool Ownership**: For managing ownership across databases, data warehouses, and dashboarding tools, data catalogs or data reliability platforms are suitable.

### 5.3 Notifying the Right People
**A common pitfall is defining ownership without active notification**.

Methods for notification:
*   **Within the Data Team**: Tag owners with Slack handles or route alerts to relevant team-specific Slack channels. This is most impactful once teams grow beyond a handful of people.
*   **Upstream Teams**:
    *   **Technical Teams**: Alerts similar to data team alerts, with context linking source issues to error messages.
    *   **Non-Technical Teams**: Bringing ownership to non-technical teams (e.g., SalesOps for Salesforce data) can reduce the data team's burden. Requires executive buy-in for consistent action.
*   **Stakeholders**:
    *   For **data-savvy teams**, direct alerts can work.
    *   For **non-technical stakeholders**, the data owner should notify directly and link to an incident page. Displaying issues directly in dashboards is possible but risky.

**Beware of alert overload**: Spamming channels leads to ignored alerts. Be deliberate; less critical issues can go to different channels or be managed in backlog reviews.

### 5.4 Adopting Incident Management
Combining incident management with ownership definitions offers benefits like **reduced resolution time, prioritized issues, clearer ownership, and institutionalized learning**.

Five steps for adopting incident management:
1.  **Getting the Data Team On Call**: Define expectations for on-call duties, whether it's a dedicated "data responder" or predefined SLAs for owners. Consider out-of-hours coverage.
2.  **Detecting Issues**: Incidents begin when something goes wrong (job failure, data not updating, test breaking). The goal is prompt detection through tests/monitors, alerting the right person (via ownership), and providing context. **"Without sufficient testing and monitoring in place, you’ll be caught on the backfoot..."**.
3.  **Triaging Issues**: When an alert triggers, assess the situation by asking three questions:
    *   **Scope**: Is it isolated or related to other issues?
    *   **Impact**: What is the potential effect on critical data products/assets?
    *   **Severity**: Is data unavailable, corrupted, or unreliable?
    This provides context for urgency and decides if a full incident response is needed. Linking incidents to data products automatically identifies affected datasets and streamlines triage. Establish clear Mean Time to Detect (MTTD) and Mean Time to Resolve (MTTR) benchmarks based on severity (e.g., P1 MTTD 1h, MTTR hours; P4 MTTD 24h, MTTR 7d). Integrate with existing incident management tools (PagerDuty, Opsgenie).
4.  **Handling the Incident**: A structured, documented process improves response effectiveness. Declare incidents for all issues, even minor ones, to create a traceable log. Create a dedicated communication space (document, Slack channel, external tool). Steps include informing stakeholders, organizing team efforts, tracking fixes (GitHub PRs), looking for similar past incidents, and documenting root cause analysis.
5.  **Post-Incident Analysis**: Essential for learning and preventing recurrence. For low-severity issues, follow-up checklists help. For critical incidents, a postmortem review offers deeper insights. Review incident trends to identify patterns or imbalances (e.g., recurring errors, disproportionate issues from certain upstream teams). Track metrics like Mean Time to Resolution, Number of Issues/Incidents by team, and Issue-to-Incident Rate.

## 6. Continuous Improvement (Chapter 5 Summary)

Establishing feedback loops and learning processes is vital for continuously enhancing data reliability. Metrics are crucial for business-critical data products, assessing quality perception, ensuring consistent standards, demonstrating external accountability (e.g., to regulators), and improving signal-to-noise ratios of controls.

### 6.1 Picking the Right Metrics
**Avoid measuring metrics like test model coverage without a clear end goal**, as this can create a false sense of security. Group metrics into key areas:
*   **High-Level Metrics**:
    *   **Coverage**: % of assets with required data controls.
    *   **Quality Score / SLA**: % of SLIs passing.
*   **Specific Quality (SLIs)**: Accuracy, Completeness, Consistency, Uniqueness, Timeliness, Validity.
*   **Usability Metrics**: % Ownership Defined, % Priority Level, % Data Product Association, % Description, Active Users, Dashboard Load Time.
*   **Operational Metrics**: Mean Time to Resolution, Mean Time to Detection, Number of Incidents, Number of Issues, Issue-to-Incident Rate.

**North Star metrics** should be chosen based on use case; for critical data products, Coverage and Quality Score/SLA are essential. Decompose these metrics into dimensions (e.g., SLA by data product) to identify areas for focus.

### 6.2 Establishing Service Level Indicators (SLIs)
SLIs are groups of data quality controls that help pinpoint areas causing SLA deficiencies. The six recommended SLI areas are:
*   **Accuracy**: Verifies data reflects real-world facts (e.g., `accepted_values`, custom SQL checks).
*   **Completeness**: Confirms all necessary data is present (e.g., `not_null`, row count checks).
*   **Consistency**: Verifies uniform data across sources (e.g., `relationships`, `unique` across datasets).
*   **Uniqueness**: Ensures no duplicate entries (e.g., `unique` on primary keys).
*   **Timeliness**: Checks data freshness and update frequency (e.g., dbt source freshness, timestamp lag checks).
*   **Validity**: Confirms data adheres to formats and rules (e.g., `accepted_values`, regex tests).

SLIs can be weighted differently based on the data product's sensitivity (e.g., ML model prioritizing completeness/accuracy over timeliness).

### 6.3 Tracking and Obtaining the Metrics
Metrics should be built with four principles in mind:
1.  **Metrics**: Select those fitting the business outcome.
2.  **Action**: Insights should lead to action.
3.  **Segment**: Metrics should be segmentable (by owner, data product).
4.  **Trend**: Measured consistently and over time.

Data can be obtained from dbt artifacts, data observability tools, dbt test results, data catalogs, manual assessments, usage logs, and incident management tools. Automated tracking of SLA, coverage, and SLIs is highly effective for regular review.

### 6.4 Operationalizing Insights
Putting insights into action involves:
*   **Automated Accountability (Weekly Email Digest)**: Shares quality scores per owner/data product, fostering accountability without direct confrontation.
*   **Religious Metadata Inclusion**: Enforce metadata (data product definitions, owner, domain) using CI checks (e.g., `check-model tags`) to ensure accountability.
*   **Beware of the Broken Windows Theory**: Address failing tests promptly (e.g., "fix-it Fridays") to prevent widespread apathy towards data quality. Remove low signal-to-noise tests.
*   **Present Metrics to Stakeholders with a Regular Cadence**: Establish benchmarks and track systemic improvements by sharing KPI progress regularly (e.g., quarterly C-level meetings).
*   **Create Run Books for Data Quality**: Provide clear steps for addressing each data quality dimension (e.g., how to address low Timeliness scores) for larger teams.

Maintaining a reliable, high-quality data platform is an **ongoing investment**, requiring continuous evaluation of new use cases, tests, and monitors based on quality metrics, and holding teams accountable.

---
