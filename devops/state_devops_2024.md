# DORA 2024 State of DevOps Report: Briefing Document

This briefing document summarizes key findings and insights from the 2024 DORA State of DevOps Report, an annual, worldwide survey of professionals in technical and adjacent roles. The report utilizes rigorous statistical evaluation and in-depth interviews to understand the relationships between various factors and their contribution to the success of teams and organizations. This year marks the tenth DORA report, drawing insights from over 39,000 professionals globally.

## Executive Summary Highlights

The 2024 DORA report investigates several key accomplishments and outcomes, including:
*   **Reducing Burnout:** A state of emotional, physical, and mental exhaustion caused by prolonged stress.
*   **Organizational Performance:** Measures areas like profitability, market share, customer satisfaction, and ability to achieve goals.
*   **Flow:** The level of focus achieved during development tasks.
*   **Job Satisfaction:** An individual’s overall feeling about their job.
*   **Product Performance:** Measures usability, functionality, value, availability, performance, and security of a product.
*   **Productivity:** The extent to which an individual feels effective and efficient in their work.
*   **Team Performance:** A team's ability to collaborate, innovate, work efficiently, rely on each other, and adapt.

### Key Findings
*   **AI's Broad Impact:** AI adoption offers promising results such as increased flow, productivity, job satisfaction, code quality, internal documentation, review processes, team performance, and organizational performance. However, it also brings detrimental effects, including reductions in software delivery performance, uncertain impact on product performance, and a decrease in time spent on valuable work. Teams are encouraged to continue experimenting with AI.
*   **User-Centricity Drives Performance:** Organizations prioritizing the end-user experience achieve higher quality products, with more productive and satisfied developers who are less prone to burnout.
*   **Transformational Leadership Matters:** This leadership style improves employee productivity, job satisfaction, team performance, product performance, and organizational performance, while also decreasing employee burnout.
*   **Stable Priorities Boost Productivity and Well-being:** Unstable organizational priorities significantly decrease productivity and increase burnout, even with strong leadership, good documentation, and a user-centric approach.
*   **Platform Engineering Can Boost Productivity:** It positively impacts productivity and organizational performance but shows cautionary signals for software delivery performance.
*   **Cloud Enables Infrastructure Flexibility:** Flexible infrastructure can increase organizational performance. However, migrating to the cloud without embracing its flexibility can be more detrimental than remaining in a data center, requiring transformation of approaches, processes, and technologies.
*   **High Software Delivery Performance is Achievable:** The highest-performing teams excel across all four software delivery metrics, with teams from every industry vertical achieving these levels.

## Software Delivery Performance

Technology-driven teams need robust ways to measure performance, and DORA has consistently validated **four software delivery metrics (the "four keys")** that effectively measure the outcomes of the software delivery process:
*   **Change Lead Time:** The time from a code commit to successful deployment in production.
*   **Deployment Frequency:** How often application changes are deployed to production.
*   **Change Fail Rate:** The percentage of deployments causing production failures that require hotfixes or rollbacks.
*   **Failed Deployment Recovery Time:** The time taken to recover from a failed deployment.

Historically, these metrics moved together, but DORA's analysis evolved to better capture software delivery stability. The 2024 report introduced **Rework Rate** (unplanned deployments to address user-facing bugs) to create a more reliable factor for **Software Delivery Stability**, alongside Change Fail Rate. **Software Delivery Throughput** is measured by Change Lead Time, Deployment Frequency, and Failed Deployment Recovery Time. All five metrics collectively describe software delivery performance.

### Performance Levels
DORA identifies four performance clusters based on these metrics: Elite, High, Medium, and Low.
*   **Elite Performers** deploy multiple times a day with lead times less than one day, change fail rates of 5%, and recovery times less than one hour.
*   **Low Performers** deploy once every 1-6 months with lead times of 1-6 months, change fail rates of 40%, and recovery times of 1 week to 1 month.
*   **Elite performers realize 127x faster lead times, 8x lower change failure rates, more deployments per year, and 2293x faster failed deployment recovery times compared to low performers**.

It's important to note that **industry vertical does not meaningfully affect performance levels**; high-performing teams are found across all industries. DORA emphasizes that **improving performance overall is more important than reaching a particular performance level**, fostering a mindset of continuous improvement.

## Artificial Intelligence (AI): Adoption and Attitudes

AI has profoundly impacted software development, moving rapidly from fringe use to ubiquity.
*   **Widespread Adoption:** 81% of organizations have shifted priorities to incorporate AI more deeply into their applications and services, with 49.2% describing this shift as "moderate" or "significant". At the individual level, 75.9% of professionals rely on AI for daily responsibilities.
*   **Common Use Cases:** The most common AI uses include writing code (74.9%), summarizing information (71.2%), explaining unfamiliar code (62.2%), optimizing code (61.3%), and documenting code (60.8%).
*   **Drivers of Adoption:** Competitive pressures and the perception that AI proficiency is "the new bar for entry as an engineer" are significant drivers.
*   **Perceived Productivity Gains:** **75% of respondents reported positive productivity gains from AI**, with over one-third describing them as moderate (25%) or extreme (10%). Only 5% reported AI inhibited their ability to write code, while 67% reported some improvement.
*   **Trust in AI-Generated Code:** While 87.9% reported some trust in AI-generated code quality, the **degree of trust was generally low, with 39.2% reporting little or no trust**. Developers often expect to tweak AI outputs rather than rely on absolute accuracy.
*   **Future Expectations:** Respondents anticipate continued positive impacts of AI on product quality. However, they also expect **net-negative impacts on careers, the environment, and society, fully realized in about five years**.

### Downstream Impact of AI
AI's impact spans individuals, teams, and organizations, presenting both benefits and drawbacks.
*   **Individual Benefits:** AI has a substantial and beneficial impact on **flow, productivity, and job satisfaction**. A 25% increase in AI adoption is associated with an estimated 2.1% increase in individual productivity.
*   **Potential Tradeoffs (Vacuum Hypothesis):** While AI boosts flow, productivity, and job satisfaction, it may **reduce the reported time spent doing valuable work** and appears to leave time spent on toilsome work unaffected. This is hypothesized as AI helping people finish valuable work faster, creating extra time, but not alleviating "drudgery of meetings, bureaucracy, and many other toilsome tasks".
*   **Development Workflow Improvements:** A 25% increase in AI adoption is associated with significant improvements:
    *   **7.5% increase in documentation quality**.
    *   **3.4% increase in code quality**.
    *   **3.1% increase in code review speed**.
    *   **1.3% increase in approval speed**.
    *   **1.8% decrease in code complexity**.
    These gains suggest better code, easier reviews, and reduced bottlenecks.
*   **Negative Impact on Delivery Performance:** **AI adoption is negatively impacting software delivery performance**. A 25% increase in AI adoption is associated with an estimated 1.5% reduction in delivery throughput and a **7.2% reduction in delivery stability**. DORA hypothesizes this is due to larger change batch sizes, as AI allows for faster code generation, potentially leading teams to overlook the importance of small batch sizes and robust testing.
*   **Higher-Level Outcomes:** AI adoption positively impacts **organizational performance (estimated 2.3% increase)** and **team performance (estimated 1.4% increase)**. However, **product performance does not show an obvious association** with AI adoption. This might be because team and organizational factors (communication, knowledge sharing) benefit before product innovation fully realizes AI's potential.

### AI Adoption Strategy
Organizations should adopt a measured, transparent, and adaptable AI strategy:
1.  **Define a Clear AI Mission and Policies:** Provide employees with transparent information about AI goals and plans, addressing procedural concerns.
2.  **Create a Culture of Continuous Learning and Experimentation:** Encourage exploration of AI tools, dedicate time for use case discovery, and build trust through hands-on experience in low-risk environments. Focus on robust test automation and measure downstream impacts, not just adoption.
3.  **Recognize and Leverage AI’s Trade-offs:** Acknowledge potential drawbacks (reduced time on valuable work, over-reliance, negative impacts on software delivery stability/throughput) to avoid pitfalls and shape AI's trajectory positively.

## Platform Engineering

Platform engineering is an emerging discipline focused on improving developer experience by building highly-automated, self-service "golden paths" that abstract away software delivery complexities.
*   **Positive Impact:**
    *   **8% higher individual productivity**.
    *   **10% higher team performance**.
    *   **6% higher organizational performance**.
*   **Unexpected Downside:**
    *   **Approximately an 8% decrease in throughput** when using a platform.
    *   **A surprising 14% decrease in change stability** (increased change failure rate and rework).
    *   Instability in combination with a platform is linked to **higher levels of burnout**.
        *   Hypotheses for instability: Platforms enabling teams to push changes with confidence that bad changes can be quickly remediated (unlocking experimentation), or platforms being ineffective at ensuring quality.
        *   Hypothesis for burnout: Teams with high instability and burnout might create platforms as a solution, making platform engineering symptomatic of existing problems.
*   **Key Success Factors:**
    *   **User-centeredness, developer independence, and a product mindset** are crucial. Without a user-centered approach (developers as users), the platform can be a hindrance.
    *   **Developer independence** (ability to perform tasks without relying on an enabling team) led to a 5% improvement in productivity at both individual and team levels.
    *   **Collecting feedback from users** is essential to understand independence.
*   **Impact of Dedicated Platform Teams:** Negligible impact on individual productivity but resulted in a **6% gain in team-level productivity**, possibly because platforms better support the diverse tasks of a team.

### Balancing Trade-offs
1.  **Prioritize Functionality for Developer Independence and Self-Service:** Balance platform exclusivity with methods for users to "break out" when needed. A dedicated platform team collaborating and collecting feedback can mitigate complexity.
2.  **Carefully Monitor Instability:** Understand if instability is intentional (experimentation) or due to quality issues. Using SLOs and error budgets from SRE can help gauge risk tolerance and platform effectiveness.
3.  **Foster a User-Centered Culture and Continuous Improvement:** Align platform features with individual and team needs to deliver software and business value.

## Developer Experience

The human aspect of technology development is foundational to organizational success.
*   **User-Centricity:** **Prioritizing the end-user experience leads to higher quality products, more productive developers, reduced burnout, and increased job satisfaction**. When organizations understand user needs, high software-delivery speed and stability are not a prerequisite for product quality; user experience at the forefront ensures high quality. This approach also provides developers with a clear sense of purpose and fosters cross-functional collaboration.
*   **Quality Internal Documentation:** When combined with a user-centered approach, **quality internal documentation amplifies the increase in product performance**. It helps propagate user signals and feedback within the team and product. Practices for a healthy documentation culture include documenting critical use cases, training in technical writing, defining ownership and processes for updates, distributing work, maintaining documentation, deleting outdated content, and recognizing documentation work in performance reviews.
*   **Stable Priorities:** **Unstable organizational priorities lead to meaningful decreases in productivity and substantial increases in burnout**. These negative effects are resistant to mitigation by strong leaders, good documentation, or user-centered approaches. The frequency of changes creates chronic stress, uncertainty, and decreased control, leading to burnout.
    *   **Stabilizing priorities, surprisingly, declines software delivery performance (slower and less stable)**. This could be because organizations with stable priorities make changes less frequently or ship in larger batches.
    *   **Adding AI-powered experiences to services or applications creates stability in organizational priorities**, but this clarity, not AI itself, is the driving factor. However, this shift comes with challenges: teams shifting to AI-powered experiences experience a **10% decrease in software delivery stability**.

## Leading Transformations

Successful transformations require a mindset of continuous improvement and strategic leadership.
*   **Transformational Leadership:** Leaders who inspire and motivate by appealing to values and purpose. Key dimensions include vision, supportive leadership, inspirational communication, intellectual stimulation, and personal recognition.
    *   **Benefits:** A 25% increase in transformational leadership leads to a **9% increase in employee productivity**. It also decreases employee burnout and increases job satisfaction, team performance, product performance, and organizational performance.
    *   **Enabler:** Transformational leadership enables the adoption of technical and product-management capabilities by delegating autonomy, providing metrics, and creating value-delivery incentives. Leaders must allocate resources and time for improvement.
*   **Be Relentlessly User-Centric:** Organizations with strong leaders and a user-focused approach develop better products. User-centered teams achieve the highest levels of organizational performance, even without high software velocity and stability.
*   **Become a Data-Informed Organization:**
    *   **Use DORA's four key metrics** at the application and service levels to track continuous improvement, not for comparing teams or individuals.
    *   **User feedback metrics are as important as the four keys**, especially as high performance becomes ubiquitous.
    *   Combine **technical metrics (four keys, reliability) with business metrics** to bridge top-down and bottom-up transformation efforts and quantify ROI.
    *   Metrics facilitate informed decision-making over opinion or intuition.
*   **Be All-In on Cloud or Stay in the Data Center:** Taking advantage of the five characteristics of cloud computing (flexible infrastructure) is linked to successful teams. **Using the cloud without leveraging these characteristics can be detrimental and decrease organizational performance**; radical transformation is required for successful migration.
*   **Embrace Continuous Improvement:** Transformation is a journey, not a destination. Organizations not continuously improving fall behind. Expect an initial drop in performance (a "j-curve") followed by significant gains, which is normal for transformations like DevOps, SRE, and Platform Engineering. The goal is to be "a little better than yesterday".

## A Decade with DORA: Key Insights

Over the past decade, DORA has established itself as a trusted source for research and insights in technology-driven teams and organizations.
*   **Teams Do Not Need to Sacrifice Speed for Stability:** DORA's four keys have repeatedly shown that throughput and stability tend to move together, with high performance achievable across both in all industries.
*   **Software Delivery and Operational Performance Drive Organizational Performance:** The best results are achieved when both software delivery performance (using the four keys) and operational performance (measuring reliability with SLOs) combine to drive organizational performance and employee well-being.
*   **Culture is Paramount to Success:** A high-trust culture that encourages learning and collaboration is one of the clearest predictors of performance, impacting every aspect of DORA's research.
*   **Get Better at Getting Better:** Continuous improvement is a mindset and practice, requiring assessment, prioritization of improvement work, and feedback mechanisms to measure progress. An experimental approach is recommended.

DORA is committed to the fundamental principles of the DevOps movement: culture, collaboration, automation, learning, and using technology to achieve business goals. The term "DevOps" may move out of the spotlight, but the research will continue to investigate emerging technologies like AI and human aspects of technology.

## Methodology Note

DORA's research methodology involves collecting data through an annual worldwide survey, augmented with in-depth interviews for deeper insights and context. Questions are carefully selected based on established literature, community engagement, cognitive interviews, and expert workshops. Data collection uses both organic recruitment (social media, email campaigns) and panel approaches to ensure representativeness, including underrepresented groups. This year, participants were randomly assigned to one of three survey flows (AI, Workplace, Platform Engineering) to allow for deeper dives into each topic. The analysis uses Bayesian statistics to evaluate models, enabling causal inference and quantifying the magnitude and certainty of effects. Interviews provide qualitative data to triangulate, contextualize, and clarify quantitative findings.
