This playbook outlines the implementation of a robust data quality management system within Power BI, leveraging Power Query error handling, advanced DAX scripting (often via Tabular Editor), and strategic report design, based on the techniques presented by Bernat Agulló.

## Data Quality Management Playbook in Power BI

### I. Core Objectives and Challenges

The primary goal of this implementation is **proactive data quality management** to ensure reliable Power BI reporting and analysis.

The implementation specifically addresses four core challenges:

1.  **Loadability:** Ensuring data loads correctly and preventing refresh failure despite inconsistencies (e.g., wrong data types, incorrect headers, duplicate keys in dimension tables).
2.  **Referential Integrity:** Validating relationships between fact and dimension tables (e.g., identifying sales records referencing product IDs not found in the product dimension).
3.  **Business Rule Compliance:** Detecting violations of predefined business logic, such as ensuring a column only contains allowed values or verifying consistency between different data tables.
4.  **User Awareness:** Implementing a clear and effective mechanism to alert users promptly when data problems arise.

### II. Phase 1: Power Query Error Handling (Loadability Checks)

The recommended approach uses a **branching strategy in Power Query** to separate clean data from problematic rows, ensuring the dataset always loads successfully.

| Step | Technique/Action | Source Reference |
| :--- | :--- | :--- |
| **1. Identify Risk Point** | Identify steps in Power Query where errors are likely to occur (e.g., combining files, changing data types, or checking for duplicate keys in dimension tables). | |
| **2. Create Clean Branch** | At the identified risk step, **create two references (branches)** to the query. In the "clean data" branch, use "Remove Errors" to discard problematic rows and continue adding steps. **This ensures the final report table is clean and always loads**. | |
| **3. Create Error Capture Branch** | In the second branch, perform the opposite action: **keep the errors**. | |
| **4. Capture Details** | Apply the `try ... otherwise` function as a custom column to the error capture branch to retrieve the error details. Expand the resulting record column to extract `Reason`, `Message`, and `Detail` of the error. | |
| **5. Unify Error Data** | Add a custom column (`Error Type`) to categorize the errors (e.g., "Sales File Errors," "Sales Data Errors"). Combine all individual error tables (from various files and data quality checks) into **one unified Error Table** using `Append Queries as New`. | |
| **6. Disable Load** | Ensure that all intermediate error capture tables (but not the final unified Error Table or the final clean data table) have **"Enable Load" disabled**. | |

### III. Phase 2: Scripting and Measure Generation

Utilize scripting, typically within Tabular Editor, to automate the creation of quality check measures across the model.

| Step | Technique/Action | Source Reference |
| :--- | :--- | :--- |
| **1. Script Measures for Load Errors** | Create a base measure (e.g., `Errors` = `COUNTROWS('Error Table')`). Use an M script to generate calculated measures based on the `Error Type` column in the Error Table. This generates individual measures counting errors for each type (e.g., `Errors By error type (Sales Data Errors)`). | |
| **2. Script Measures for Referential Integrity** | Use a dedicated script that iterates through all **one-to-many relationships** in the model. The script generates measures that count the values in the fact table column that have a blank value on the dimension side (unmapped). Store these measures in a dedicated table (e.g., `Referential Integrity`). | |
| **3. Script Measures for Business Logic** | Define DAX measures to check specific business rules (e.g., counting rows where two consistency checks, like sales vs. deliveries, return different values). | |
| **4. Organize Measures** | Place all defined quality check measures into specific **Display Folders**. Use folder prefixes (e.g., `checks Logic`, `checks Referential Integrity`, `checks Data Errors`) to distinguish and organize them. | |
| **5. Generate Summary Alerts** | Use a specialized script (often involving a Dynamic Measure Calculation Group) that scans the measures stored in the prefixed display folders to automatically create a **Total Alert Count** measure. This measure aggregates all identified quality issues across the model. | |

### IV. Phase 3: Error Visualization and User Interface

Implement a dedicated page and a **dynamic alert mechanism** to inform users about data issues.

| Step | Technique/Action | Source Reference |
| :--- | :--- | :--- |
| **1. Create Detail Page** | Create a dedicated report page, often named "Data Problems". | |
| **2. Visualize Errors** | Populate the detail page with visuals and detailed error tables. Show source names, columns, problematic values, and error messages from the unified Error Table. | |
| **3. Visualize Referential Integrity** | Create small tables displaying the unmapped values found in the fact table (e.g., `Back ID 3`). Use **dynamic titles** generated by the integrity script to explain the context of the error (e.g., "One Back ID not mapped in sales"). | |
| **4. Implement Dynamic Button** | Implement a **dynamic button** on the main report page, which serves as the primary user alert mechanism. | |
| **5. Control Button Visibility and Color** | Use DAX measures (derived from the scripts, such as `Total Alert Value`) and conditional formatting/actions to control the button's appearance. **If everything is fine, the button is transparent/not visible**. If data problems exist, the button "pops" and shows in red. | |
| **6. Set Dynamic Text and Navigation** | The button text should display the measure counting the total number of data problems (e.g., "There are 10 data problems"). Use a DAX measure to set the navigation action: direct the user to the "Data Problems" page only if errors exist, otherwise do nothing. | |

### V. Key Takeaways and Resources

*   **Priority:** The most critical step is implementing the Power Query branching part, as it prevents your report refresh from breaking and ensures you know about data that fails to load.
*   **Automation:** Combining Power Query techniques, scripting (using M/DAX), and thoughtful report design enables comprehensive validation and error reporting.
*   **Resources:** Leverage scripts provided by the author on his blog or GitHub repository to implement robust checks, even without extensive scripting experience.
