https://openvisualizationacademy.beehiiv.com/p/friends-of-the-open-visualization-academy-nina-krug

# Briefing Document: Friends of the Open Visualization Academy featuring Nina Krug

## I. Open Visualization Academy (OVA) & New Video Series

The **Friends of the Open Visualization Academy** is a new video series hosted by Alberto Cairo, featuring in-depth conversations with data designers, artists, and journalists. This series is a follow-up idea to Cairo’s book, *The Art of Insight*.

*   The series is currently published in a newsletter but will become a section of the **Open Visualization Academy’s (OVA) website** when the OVA officially launches.
*   The OVA is actively preparing for its launch on **January 31st, 2026**.
*   Alberto Cairo noted he still needs to record his course for the OVA.
*   The first episode features German data journalist **Nina Krug**.
*   *Related Update:* The **Computation+Journalism Symposium** is scheduled for December 11-12.
*   *Related Project:* Alberto Cairo participated in and funded the **Trans News Initiative (TNI)**, a collaboration involving the University of Miami’s School of Communication, the Trans Journalists Association, and Polygraph (the creators of *The Pudding*).

## II. Featured Guest Profile: Nina Krug

Nina Krug is the first guest in the *Friends of the Open Visualization Academy* series. She is an information and communication designer working from **Hamburg, Germany**.

*   **Mission:** Krug pursues the mission of making complex topics accessible and easy to understand.
*   **Education & Teaching:** She completed her bachelor's degree in 2021 and subsequently her master's degree at the renowned **Bauhaus University**. In summer 2022, she taught the class ‘Good News Flash – Information Design in an Editorial Context’ at the Bauhaus University Weimar. This class focused on creating **creative infographics** using more analog methods, such as paper collages and acrylic paintings.
*   **Current Role:** Since **October 2023**, Nina Krug has been a permanent member of the **Data & Visualizations department at the news magazine DER SPIEGEL**.
*   **Der Spiegel Team Structure:** The Data & Visualizations team at *Der Spiegel* consists of approximately **25 people**. Profiles within the team include:
    *   Graphic and communication designers (like Krug).
    *   Visual coding people.
    *   Data journalists.
*   **Department Culture:** The department has shifted to being regarded as its **own unit** within the magazine, working mostly independently as a **content production unit** that proposes stories with visual potential, rather than purely operating as a service department fulfilling requests.

## III. Highlighted Project: German Election Campaign Speeches

Krug discussed her popular visualization project concerning the **sentiments expressed in public speeches by candidates in the recent German federal election**. The project, which was different from usual election coverage, aimed to show *how* the politicians said what they said, focusing on emotions.

### A. Data and Analysis

*   **Source Material:** Sentences were transcribed from videos of the campaign speeches.
*   **Emotion Classification:** An **AI was trained** to match the sentences to corresponding emotions.
*   **Verification:** The team recognized the sensitivity of the task and performed manual hand-checking (up to 10 times) after the AI matching to classify emotions correctly, sometimes agreeing on the most common answer among the team members.

### B. Visualization and Encoding

The project utilized creative encodings, moving beyond traditional elements like color and position, to make the experience both informative and evocative.

| Encoding Type | Information Conveyed | Details |
| :--- | :--- | :--- |
| **Color** | **Topics** (e.g., economy, debate culture, migration) | Stacked bar graphs displayed the relative proportions (percentages) of topics discussed in the speeches. |
| **Shape/Line Work** | **Emotions** (Sentiment) | Shapes were used as a categorical encoding to represent emotions. The lines were initially **hand-drawn** by Nina Krug. |

*   **Emotion Shape Examples:**
    *   **Zigzag line:** Represented anger. Far-right candidate Alice Weidel was shown to be "very angry" (zigzag line).
    *   **Little slopes:** Represented hope.
    *   **Neutral lines:** Used if no strong emotion applied.
    *   **Spiky shapes** generally conveyed anger, while **smoother shapes** suggested a calming experience.
*   **Annotation Importance:** The team ensured the interactive piece included a **visible legend** and annotations on every sentence to overcome potential misinterpretations of the non-traditional encoding, listing the specific emotion conveyed.

### C. Technology and Timeline

The project required a variety of tools, merging hand-crafted ideas with modern technology.

*   **Design & Iteration:** Ideas for the line shapes were developed through analog methods (hand-drawing in a notebook). Layouts and ideas were tried out in **Figma**.
*   **Digitalization:** The final hand-drawn lines were digitized in **Illustrator** and converted into **SVGs** (vector graphics) for the coding team.
*   **Coding:** A colleague coded the large interactive part.
*   **Animation:** The intro animation used tiny **PNGs** put together in **After Effects**.
*   **Timeline:** The project took approximately **three months** (started late November, elections were end of February). Visualization started in early January. The most labor-intensive parts were getting the speeches transcribed and the classification/manual checking finalized.
