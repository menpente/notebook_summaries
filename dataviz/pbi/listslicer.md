## Process Documentation: Creating Next-Level Power BI Navigation with the List Slicer

This documentation outlines the steps for creating sophisticated navigation menus using the enhanced Power BI List Slicer visual, a method that significantly reduces development time compared to older, bookmark-heavy workarounds.

### I. Prerequisites and Setup

1.  **Power BI Version Check:** Ensure you are using the Power BI version published after at least **May 18, 2025**.
2.  **Visual Selection:** Utilize the standard **List Slicer** visual, which now supports images and advanced settings for states.
3.  **Data Structure:** The navigation requires data structured hierarchically, typically with a top-level category (e.g., `milestones info category` like "Call Out Visuals" or "Cartisians") containing lower-level items (e.g., `features` like "card" or "gauge").

### II. Image and Icon Data Preparation

Since the List Slicer supports images, icons must be converted and stored within the data model:

1.  **Static Images (PNGs):** Convert static icons (PNGs) into **Base 64 images**.
    *   Use a suitable conversion website to drop the image in and copy the resulting Base 64 text.
    *   Paste the Base 64 text directly into the data model as new columns (e.g., for selected and unselected icons).
2.  **Animated Icons (GIFs):** If using animated icons, convert them to Base 64.
    *   Due to the resulting large number of characters, which Power Query may not support for direct semantic model loading, store the Base 64 GIF text inside **measures** (e.g., `call out GIF`). Measures can store significantly more characters.
3.  **Conditional Logic Measures:** Create simple measures to control which icon or color applies based on the selected category (e.g., if the category is "Cartisians," give this icon; otherwise, give that icon).

### III. Slicer Configuration and Layout

1.  **Insert Slicer:** Place a new List Slicer visual onto the report.
2.  **Define Hierarchy:** Drag the highest level of the navigation (e.g., `milestones info category`) into the slicer field well, followed by the lower level (e.g., `features`).
3.  **Manage Interactions (Optional):** If you have other slicers, check "Edit interactions" and ensure they are not unnecessarily interacting with the new List Slicer.
4.  **Filter Blanks (Optional):** Filter out blank categories if the data set is incomplete.
5.  **Remove Title:** Turn off the visual title.
6.  **Force Selection:** Navigate to Slicer settings and click **force selection** to ensure one item is always selected when the report opens.
7.  **Layout/Button Count:**
    *   Determine if you want a **fixed number of buttons shown**. Keeping this on ensures all buttons maintain the same size, which may be preferable.
    *   Alternatively, turn off the fixed number and set a maximum number of buttons (e.g., 10).
8.  **Expand/Collapse Icon (Arrow):**
    *   Set the expand/collapse icon to be **invisible** for the lowest level (`feature`).
    *   For the higher level (`category`), set the layout position of the icon to the **right** for improved visual appearance.

### IV. Styling and Conditional Color Application (Features)

This section focuses on styling the lower-level navigation buttons (`feature`):

1.  **Disable Category Selection Icon:** Go to the Selection Icon panel and turn off the icon for the `category` level, as custom images will replace it. Keep the selection icons on for the `feature` level.
2.  **Apply Background Colors (via Measures):**
    *   Under Selection Icon, choose the `feature` series.
    *   Use conditional formatting (Field Value) to apply a background color measure (e.g., light blue for "Cartisians" and dark blue for "Call Out Visuals").
3.  **Set State Colors (Rest, Hover, Selected):**
    *   Open the Buttons panel and select the `feature` series.
    *   For the **Rest** state, set the desired background and text color (e.g., dark gray background).
    *   For the **Selected** state, set the background color to the field value from the background color measure.
    *   For the **Hover** state, set the background color using a measure (often a lighter shade) and ensure the text value changes (e.g., text becomes **white**).
4.  **Advanced State Overrides (Text):**
    *   To prevent the text of an already selected item from changing color on hover, use the **Advanced** section.
    *   Apply settings to the combination of **Selection State: Selected** and **Interaction State: Hover**.
    *   Set the text color to its resting color (e.g., black) to override the white hover text setting applied to the general 'hover' state.
5.  **Shape Modification:** Under the Shape panel, apply a **rounded rectangle** shape and set a size (e.g., 12) for a "nice hill shape" effect.

### V. Image and Animation Implementation (Category)

This section focuses on adding the custom icons and animations to the upper-level navigation buttons (`category`):

1.  **Initial Static Icon Setup (Unselected):**
    *   Go to the Images panel and apply settings to the `category` series.
    *   Set the image for the **Selection State: Unselected** using the Base 64 measure for the *unselected* category icon.
    *   Set the **Image fit** to **Normal** to preserve aspect ratios.
    *   Set the image area size (e.g., 10% to 15%).
2.  **Selected Static Icon Setup:**
    *   Set the image for the **Selection State: Selected** using the Base 64 measure for the *selected* category icon.
    *   Ensure the **Image fit** is set to **Normal**.
3.  **Handling Mixed State (Partial Selection):**
    *   If only lower-level items are selected (a "partially selected" or **mixed state**), the icon needs to be explicitly set to the selected icon.
    *   Set the image for the **Selection State: Mixed** to the *selected* category icon.
4.  **Implementing Hover Animation (GIFs):**
    *   To show animated GIFs on hover, the GIF measure must be applied to the **Hover** interaction state across *every* selection state used.
    *   Go into the images section and apply the GIF measure to the **Interaction State: Hover** for the following three selection states:
        *   **Selection State: Unselected** + **Interaction State: Hover**.
        *   **Selection State: Mixed** + **Interaction State: Hover**.
        *   **Selection State: Selected** + **Interaction State: Hover**.

### VI. Final Category Text Styling

1.  **Category Hover Effect (Unselected):** To make the unselected category text change color on hover, navigate to the `category` series and set the font color for the **Unselected** state combined with the **Hover** interaction state.
2.  **Bolding:** Make the text **bold** for the **Selected** state, and optionally for the **Mixed** state, to increase prominence.
