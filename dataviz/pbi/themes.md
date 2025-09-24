https://youtu.be/eMOPHsD6900

# Power BI Visual Formatting: Using Themes and Style Presets (Briefing Document)

This document provides a summary of techniques for formatting Power BI visuals efficiently using JSON theme files and style presets, drastically reducing the manual effort required of Power BI developers.

## The Problem with Manual Formatting

Power BI developers often find themselves doing **mundane work** formatting visuals individually. Formatting involves applying settings for background, borders, labels, X and Y axis properties, and colors. This process requires clicking on each visual, navigating to the format pane, and applying settings. This can be particularly tough and require significant manual effort when working with multiple reports or **hundreds of visuals**.

## The Solution: Formatting in One Go

It is possible to format multiple visuals in one go, potentially in just one click or within about five seconds, by leveraging theme files and style presets. This method allows for setting a theme file with desired formattings and **reusing it everywhere in all report files**.

## Implementation Steps

The process centers on defining formatting properties within a JSON theme file:

### 1. Saving the Current Theme

1.  Navigate to the **View pane**.
2.  Click on the **Themes drop-down**.
3.  Select **"Save your current theme"**.
    *   This action saves the current default color formattings and properties as a theme file.

### 2. Modifying the JSON Theme File

The saved file is a JSON theme file that contains default data colors and properties. Developers must then modify this file to define custom formatting.

*   **Intellisense Support:** It is recommended to add a schema file location (linked in the video description) to the JSON file to enable Intellisense, which helps list the different properties and settings that can be applied to visuals.
*   **Key Properties:** The implementation requires playing around with the **`visual styles`** object and the **`JSON style presets`** property. The `visual styles` object is what allows defining different format settings and formatting properties for visuals.
*   **Hierarchy for Defining Styles:**
    The style definitions follow a specific hierarchy within the JSON file:
    1.  **`visual styles`**
    2.  **`visuals name`**: Define the specific visual type (e.g., clustered column chart, pie chart, column chart, bar chart).
    3.  **`style preset name`**: Define a default formatting bundle to be applied (e.g., `format one`, `format two`, `format three`). Style presets can be reused for multiple other visuals.
    4.  **Card/Visual Property Definition**: Define the specific properties (e.g., `border`, `legend`, `data labels`, `value access`) and their corresponding values.

**Examples of Defined Properties:**

| Visual | Style Preset | Properties Defined |
| :--- | :--- | :--- |
| **Clustered Column Chart** | `format one` | Border (with radius 30), Legend (to be shown, italic, position drop center), Visual Axis (grid line color), Data labels (defined color). |
| **Clustered Column Chart** | `format two` | Border (different radius), Drop shadow property added, Value Access (grid line with different color), Labels (defined with red color). |
| **Pie Chart** | `format three` | Border, Legend (towards the left), Labels (defined color). |

*   **Other Settings:** Page label settings, which are typically default in the theme, can also be changed as per requirements.
*   **Saving:** Once modifications are complete, the JSON file must be saved.

### 3. Applying the Theme and Presets in Power BI

1.  In the Power BI report, go to **Themes**, scroll down, and select **"Browse for themes"** to import the newly saved JSON theme file.
2.  If the JSON file contains no errors, a successful import message will appear; otherwise, an error message will display at the top right.
3.  After the theme is imported, select an individual visual.
4.  Go to the **Format pane**.
5.  The **`style presets`** property will now be visible (it was not there before the JSON theme was loaded).
6.  Select the desired style preset (e.g., `format one`, `format two`) to instantly apply the formatting defined in the JSON file.

## Benefits

This approach dramatically enhances the efficiency of Power BI development. By defining formattings in a theme file, developers can:

*   Format all visuals quickly, saving manual effort.
*   Ensure that multiple reports or all visuals in a report are formatted in the same manner with similar themes and properties.
*   Make life easier as a Power BI developer.
