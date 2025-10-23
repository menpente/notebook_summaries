# Google’s Engineering Culture Briefing

## 1. Scale and Scope

Google (the biggest part of Alphabet) is one of the largest tech companies globally, potentially the biggest, depending on the metric.

| Metric | Detail | Source(s) |
| :--- | :--- | :--- |
| **Total Employees (Alphabet)** | 182,000 employees. | |
| **Engineers** | Approximately 50,000 engineers as of 2020 (up from 25,000 in 2015). | |
| **Monthly Users** | 3 to 4 billion people use Google services (Search, Gmail, YouTube) monthly. | |
| **Google Search** | More than 1 billion people use Search daily. | |
| **YouTube** | 2.5 billion monthly viewers, with 360 hours of content uploaded every minute. | |
| **Google Workspace** | Over three billion users, holding more than 50% market share. | |
| **Global Presence** | 72 offices in over 50 countries. | |
| **Major Engineering Hubs** | Mountain View (Googleplex HQ), New York, and Seattle/Kirkland (Cloud is largely based here). Zurich is considered Google’s European engineering HQ. Bangalore and Hyderabad are massive and growing engineering centers in India. | |

## 2. Unique Technology Stack and Internal Tools

Google maintains the world's most unique tech stack, building custom tools because existing solutions did not meet their need for "planet scale" speed and reliability from the outset (dating back to the early 2000s). The company is often described as a "tech island" due to its separation from standard industry tooling.

| System Category | Internal Tool(s) | Description and Context | Source(s) |
| :--- | :--- | :--- | :--- |
| **Orchestration/Compute** | **Borg** | Cluster operating system used internally; Kubernetes (open-source) was inspired by lessons learned from Borg. | |
| **Networking/DNS** | **B4** / **Borg Naming Service (BNS)** | B4 is the internal backbone networking infrastructure. BNS is Google's alternative to DNS, necessary because Borg allocates jobs fluidly across machines, requiring a higher level of abstraction than specific IP addresses. | |
| **Storage/Database** | **Google File System (GFS)** / **Colossus** / **Bigtable** / **Spanner** | GFS was developed in 2003, followed by Colossus (used now), offering huge decentralized storage. Bigtable and Spanner are database services built on this stack, optimized for different trade-offs (e.g., consistency vs. latency). | |
| **Source Control/Build** | **Piper** / **Blaze** | Piper is the custom version control system. Blaze (open-sourced as Basil) is the distributed build system, essential for enabling the massive internal monorepo. | |
| **Monorepo** | N/A | Contains billions of files, two billion lines of source code, and processes 40,000 commits every day (2015 figures). | |
| **Development Workflow** | **Critique** / **Code Search** / **Cider** | Critique is the code review tool (using change lists instead of pull requests). Code Search allows rapid searching across all repositories. Cider (a fork of VS Code) is the internal IDE, often used for "clients in the cloud" (citsy) development, meaning code is rarely stored locally. | |
| **Ticketing/Project Mgmt** | **Buganizer** / **Task Flow** / **GUTS** | Buganizer is a custom management tool; Task Flow provides UI boards (like Kanban) on top of Buganizer. GUTS (Google Universal Ticketing System) is for tech support. | |

### Externalization

Google often "externalizes" its internal technology, leading to major open-source contributions. Kubernetes is the externalized version of Borg, and gRPC (internally called Stubby) is their externalized communication protocol used across services.

## 3. Talent, Roles, and Compensation

### Compensation and Perks
Google is recognized for paying at the top tier of the market. A senior software engineer in Silicon Valley can expect around **$450,000 per year in total compensation**, which is composed of base salary (e.g., $220k), vesting stock (e.g., $200k/year), and a cash bonus. Google consistently pays more than local competitors, often offering 10% more than competing offers for senior roles. Perks are extensive, including free food, micro kitchens, and unique office decor.

### Key Roles and Levels (L-Levels)
The main role is Software Engineer (SWE). Google uses an L-level system for Individual Contributor (IC) and Manager tracks.

| Level | Role Title (IC Track) | Notes | Source(s) |
| :--- | :--- | :--- | :--- |
| **L3** | Entry-Level SWE | Starting point for new graduates. | |
| **L4** | Mid-Level SWE | Minimum starting point for PhDs. This is now the "terminal level" (no pressure to advance further). | |
| **L5** | Senior Software Engineer | Promotion from L4 is now challenging, requiring a project demonstrating readiness for senior impact. | |
| **L6** | Staff Engineer | Management track typically starts here. | |
| **L7** | Senior Staff Engineer | Corresponding manager level is Senior Engineering Manager. | |
| **L8** | Principal Engineer | Corresponding manager level is Director. | |
| **L10** | Google Fellow | Highest IC level mentioned. | |

### Tech Lead Manager (TLM)
TLM is a unique hybrid role influenced by Google. It is typically intended for senior ICs (L6+) who act as technical leads but also manage a small number of direct reports (often limited to four or five people) and are not necessarily seeking promotion to the full management ladder.

### On-Call Management
Google actively reduces the burden of on-call duty, making it less stressful than at many other companies.

1.  **SRE Support:** The Site Reliability Engineering (SRE) organization (a role Google invented) builds tooling to mitigate on-call pain.
2.  **Toil SLOs:** Teams must adhere to "Toil Service Level Objectives." If breached, the team stops production work and fixes underlying issues to restore system health.
3.  **Compensation:** Services are assigned tiers (Tier 1 is most critical, Tier 3 is "best effort"). Engineers on call for Tier 1 services receive generous compensation (e.g., 66% of their normal salary if they were on call for the whole month).
4.  **Limits:** Engineers are limited to a maximum of two weeks on call per quarter.

## 4. Performance, Mobility, and Culture

### Performance and Promotions
The performance review process, now called **Grad** (Google Review and Development), runs annually. Ratings are tied to "Impact," ranging from Moderate to Significant, Outstanding (received by about 8% of people), and Transformational (the top tier). A forced distribution ensures ratings fit specific budget buckets set at the director level.

Promotions rely on a **Promotion Committee** consisting of senior engineers and managers from different organizational areas who do not know the candidate. They base their decision on a written packet, aiming to remove manager or peer bias and enforce objectivity. However, this structure often leads to **promotion-driven development**, where engineers prioritize launching high-impact projects that appeal to the committee, rather than focusing on maintenance work or improving struggling projects, contributing to frequent product cancellations (the "Killed by Google" phenomenon).

### Internal Mobility
Internal mobility is very high. Engineers who are not in a bad performance standing can typically switch teams anytime without their current manager's permission.

SWE hiring often uses a **Team Matching** process. Candidates interview generally, and if successful, they must be "claimed" by a team. This period can be frustratingly long and may result in the candidate not receiving an offer if no team matching occurs.

### Culture and Work Style
*   **Googliness:** This cultural concept emphasizes collaboration, teamwork, and valuing feedback. Googlers are expected to thrive in ambiguity due to the frequency of reorgs and changing projects.
*   **Design Docs:** Google has a strong design doc culture. Engineers are required to write comprehensive design documents (covering context, goals, architecture, and alternatives) before starting to code, even for smaller projects.
*   **Transparency:** Historically, communication was extremely transparent, featuring weekly company-wide all-hands meetings (TGIF/TGIT). While transparency has decreased somewhat due to internal leaks and organizational growth, high meeting volume and information overload remain common.
*   **Rewrites:** Non-stop rewrites and migrations are a common part of engineering life due to constantly evolving internal technology, making Googlers adept at large-scale refactoring and data migration.
*   **Pedigree:** Working at Google, even for a short period, is a significant resume builder recognized globally. Many people who leave Google (known as **regoolers** if they return) start hot scaleups or join high-demand startups.
