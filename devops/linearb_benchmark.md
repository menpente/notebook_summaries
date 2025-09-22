# 2025 Software Engineering Benchmarks Report: Key Briefing

This briefing document synthesizes the core findings and benchmarks from the 2025 Software Engineering Benchmarks Report, focusing on key metrics, investment profiles, and data-driven insights.

## I. Report Scope and Methodology

The 2025 Software Engineering Benchmarks Report is the fourth annual edition, focusing research on **Developer Experience (DevEx)** and **Developer Productivity (DevProd)**.

### Data Context
The report’s analysis spans:
*   **6.1 million+** Pull Requests (PRs).
*   **3,000+** engineering teams.
*   **167k+** active contributors.
*   **32** countries.
The sample size this year has doubled from the previous year.

### Key Definitions
*   **Developer Experience (DevEx):** A development team’s overall morale and engagement when interacting with their organization’s tools, processes, and environments.
*   **Developer Productivity (DevProd):** How effectively and efficiently developers can complete meaningful tasks quickly and with minimal waste.

LinearB recommends balancing both DevEx and DevProd outcomes. There is a misconception that investing in DevEx—such as improving tools or enhancing workflows—takes effort away from new value delivery; however, it often leads to sustained Developer Productivity gains by reducing toil and burnout.

### Performance Levels
Metrics are organized into four levels of performance, aggregated using the P75 (75th percentile) calculation to ensure reliability against outliers:
*   **ELITE:** Top 10% of the LinearB community.
*   **GOOD:** Top 30% of the LinearB community.
*   **FAIR:** Top 60% of the LinearB community.
*   **NEEDS FOCUS:** Bottom 40% of the LinearB community.

---

## II. New Metrics Introduced

The 2025 report includes seven brand-new metrics:

### New DevProd and DevEx Metrics
These new metrics split **Review Time** into two sub-segments for more accurate diagnosis of code review bottlenecks:
*   **Approve Time:** Measures the time from the first comment on a PR to when the PR is first approved.
*   **Merge Time:** Measures the time from first approval to when the PR is merged.
*   **PR Maturity:** The ratio between the total changes added to a PR branch *after* the PR was published and the total changes in the PR. It gives a unique view into the impact of code reviews, highlighting ineffective review (very high maturity) or premature review (low maturity).

### New Project Management (PM) Hygiene Metrics
These metrics serve as proxies for traceability and help ensure alignment with planned work:
*   **Issues Linked to Parents:** The percentage of issues or tickets with active work linked to a parent issue (like an epic or story), excluding subtasks.
*   **Branches Linked to Issues:** The percentage of code branches containing a reference to specific PM issues, providing visibility into the alignment of code changes with planned tasks.
*   **In Progress Issues with Estimation:** The proportion of ongoing PM tasks that have time or effort estimates assigned, aiding predictability.
*   **In Progress Issues with Assignees:** The percentage of active PM tasks with a designated team member responsible, helping with accountability and workload management.

---

## III. Engineering Investment Benchmarks

The Investment Benchmarks represent the **average investment split across many organizations**. These benchmarks are useful for aligning R&D resource investment with executive goals.

| Category | Average Investment Split | Definition/Activities |
| :--- | :--- | :--- |
| **New Value** | **55%** | Actions performed to invest in new features that increase revenue and growth (e.g., adding a new feature, implementing roadmap work). |
| **Feature Enhancements** | **20%** | Actions taken to enhance features or deliver a product that ensures customer satisfaction (e.g., customer requested improvements, improved performance/reliability). |
| **Developer Experience (DevEx)** | **15%** | Actions to improve productivity and overall experience (e.g., code restructuring, testing automation, better developer tooling). |
| **KTLO (Keeping the Lights On)** | **10%** | Minimum tasks required to stay operational daily and maintain a stable service level (e.g., maintaining security posture, monitoring & troubleshooting). |

---

## IV. Key Insights and Correlations

The report highlights critical correlations between various engineering metrics:

### A. PR Lifecycle Insights: PR Size Drives Velocity
**PR Size is the most significant driver of velocity across the PR lifecycle**. When pull requests are small, they are generally less complex and lower risk, leading to faster review, approval, and merge times.
*   **Larger PRs wait longer** to get picked up for review. This is because large PRs present a daunting task for reviewers, often involving multiple files or systems, increasing cognitive load and the chance of needing external review.
*   **Larger PRs have longer Cycle Times**. They are harder to review, difficult to merge, and riskier to deploy.
*   **Larger PRs take longer to approve**. Reviewers must dedicate more time to comprehend the scope and potential impact, often leading to more detailed scrutiny and a higher likelihood of issues or questions.
*   **PRs that wait longer for review to start (longer Pickup Time) also take longer from approval to merge (longer Merge Time)**. The initial delay can disrupt workflow momentum and increase the likelihood of code conflicts or dependency changes requiring rework before merging.
*   **Larger PRs are modified more heavily during review** (resulting in lower PR Maturity Ratio).

### B. PM Hygiene Insights: Speed vs. Process
Paradoxically, **poor PM hygiene may correlate with shorter cycles**, as moving fast can be synonymous with forgoing formal process and overhead.
*   When a high percentage of **Branches are not Linked to Issues**, **Coding Time is shorter**. Developers focus solely on coding without administrative tasks, but this lack of structure risks lacking context, misalignment, and future technical debt.
*   Similarly, a lack of linked issues correlates with **shorter Review Time** and **shorter Merge Time**. Reviewers may adopt a more cursory, code-only approach, but this speed may result in less stable integrations. The reduced visibility and tracking often leads to impaired predictability.

### C. DORA Insights: Longer Cycles, Higher Failure Rate
**Organizations with longer Cycle Times have a higher rate of failures in production**. Teams that ship many small changes in short cycles have lower risk and can fix production issues faster.
*   **The longer the Cycle Time, the higher the Change Failure Rate (CFR)**. Extended cycles often stem from large or intricate code changes, increasing the likelihood of conflicts, outdated code, and missed opportunities to catch errors early.
*   **The longer the Deploy Time, the higher the Change Failure Rate (CFR)**. This can be due to larger deploy batches, higher risk of drift/conflict the longer the time gap after merge, and a lower sense of ownership when developers writing the code are detached from deployment.

### D. Quality Insights: PR Maturity and Velocity
The maturity of a team’s PRs indicates how efficiently code moves through the pipeline, as developers ensuring PRs are thoroughly prepared upfront reduces delays caused by fixes and additional reviews.
*   **The higher the PR Maturity Ratio, the higher the Merge Frequency**. Well-prepared PRs are higher quality and are more likely to be approved and merged quickly.
*   **The higher the PR Maturity Ratio, the shorter the Pickup Time**. Reviewers tend to prioritize quickly starting reviews on well-polished PRs.

---

## V. Organizational Size Insights

**Start-up engineering organizations (0-200 Employees) tend to ship code at a faster rate than Scale-ups (200-1000 Employees) and Enterprises (1000+ Employees)**.

| Metric | Start-up Trend (0-200 Employees) | Rationale |
| :--- | :--- | :--- |
| **Merge Frequency** | Higher than Enterprises and Scale-ups. | Start-ups have less formalized processes, minimal bureaucracy, and prioritize speed and market validation over extensive review standards. |
| **Deploy Frequency** | Higher than Enterprises and Scale-ups. | They benefit from leaner infrastructure and agile methodologies. Larger organizations must manage legacy systems, complex coordination, and rigorous testing for stability, which slows deployments. |

---

## VI. Bot-Generated PR Research

Special research revealed a surge in bot-created PRs, reflecting a shift toward automation.

### Key Findings on Bot PRs
*   Bot PRs have risen from 5% to **15%** in key open-source repositories over the last two years.
*   Bot-generated PRs make up **13.3%** of the average number of code submissions at organizations using tools like Renovate (**16.8%**) or Dependabot (**10.5%**).
*   Future prediction: The percentage of bot-authored code could rise from 15% today to **50% or more** due to advancements in AI agents and machine learning (Agentic AI).

### PM Hygiene and Toil Risks
*   **Untraceability Risk:** **96.2%** of all bot-created PRs are **not linked to a PM issue**. This poses a major risk to PM hygiene, traceability, and compliance (e.g., SOC 2).
*   **Developer Toil:** A large volume of bot PRs is ignored or deleted, indicating toil. Over **37.5%** of Dependabot updates are deleted and never acted upon, and **16.4%** are stale. Ignoring or stalling these PRs defeats the purpose of the dependency bots, resulting in longer periods with deprecated or vulnerable dependencies.

### Automation Opportunity
*   **Up to 84%** of bot PRs (patch and minor updates) can be safely **auto-approved**.
    *   Patch updates (41.3% of Dependabot PRs) typically address bug fixes and security vulnerabilities and can generally be **auto-merged**.
    *   Minor updates (42.96% of Dependabot PRs) usually introduce features and enhancements and can be **auto-approved**.
*   Major updates often introduce breaking changes and need thorough review and testing.
