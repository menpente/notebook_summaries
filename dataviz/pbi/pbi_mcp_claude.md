Standard Operating Procedure: Power BI Model Refinement via Claude MCP
This Standard Operating Procedure (SOP) outlines the professional standards for utilizing the Claude Model Context Protocol (MCP) to refine, optimize, and document Power BI semantic models.
1. Technical Initialization & Connection
Before refinement begins, developers must establish a secure bridge between the Power BI Desktop environment and the Claude AI engine.
• Environment Setup: Ensure Visual Studio Code and the Power BI Modeling MCP Server extension are installed.
• Claude Configuration: Install Claude Desktop and update the claude_desktop_config.json file with the MCP server path, ensuring all file path backslashes are converted to double slashes (\\) to prevent connection failures.
{
  "mcpServers": {
    "powerbi-modeling-mcp": {
      "command": "C:\\Users\\YOURUSERNAME\\.vscode\\extensions\\analysis-services.powerbi-modeling-mcp-0.1.9-win32-x64\\server\\powerbi-modeling-mcp.exe",
      "args": ["--start"],
      "type": "stdio"
    }
  }
}

• Model Connection: Open the target Power BI .pbix file and initiate the session in Claude using the prompt: "Connect to the open Power BI desktop file".
3. Schema Cleaning & Naming Standardization
To maintain a professional snowflake or star schema, developers should use Claude to enforce model-wide naming conventions.
• Analysis: Instruct Claude to analyze existing naming conventions to identify inconsistencies such as mixed prefixing styles (e.g., using both 0 and _), inconsistent casing, or unclear column purposes.
• Bulk Renaming: Execute a global rename command. Claude will update table names, column names, and—crucially—automatically update all DAX measure references to reflect the new table names, preserving model integrity.
• Key Management: Prompt the agent to hide all foreign key columns and IDs that are not required for end-user reporting to simplify the field list.
4. Automated DAX Creation & Organization
Developers should automate the creation of standard calculation patterns to ensure mathematical consistency.
• Calculation Tables: Direct Claude to create a dedicated, empty table to house all model measures.
• Measure Suites: Use natural language to generate complex measure sets, including:
    ◦ Base Aggregations: Amounts sold, returned, or net sales.
    ◦ Time Intelligence: Automated creation of Month-to-Date (MTD), Year-to-Date (YTD), and Previous Month comparisons.
• Nested Display Folders: To maintain a professional UI, instruct Claude to organize fields into nested display folders (e.g., grouping "Time Intelligence" separately from "Base Measures").
5. Performance Compression Audit
Optimizing data types is critical for reducing model size and increasing query speed.
• Optimization Prompt: Direct Claude to "analyze data types and optimize them for better compression and performance".
• Impact Verification: Review the Claude-generated summary, which can identify potential memory compression improvements (up to 15% model size reduction) and 2x to 3x faster join performance.
• Data Integrity Check: After optimization, developers must trigger a model refresh to resolve any pending metadata changes and ensure no data loss occurred during type conversion.
6. Metadata & Professional Documentation
A refined model must include a comprehensive data dictionary to support long-term data governance.
• Field Descriptions: Use Claude to bulk-populate the "Description" property for every table, column, and measure. The AI should be instructed to explain the DAX logic in simple business terms.
• Synonyms for Q&A: Ensure Claude populates synonyms for all fields to enhance the model's compatibility with natural language AI tools.
• Markdown Data Dictionary: Generate a final Markdown documentation artifact. This document should include:
    ◦ An executive summary of the model.
    ◦ A Mermaid diagram illustrating table relationships.
    ◦ A full data dictionary containing every DAX expression and its associated business logic.
7. Validation Standards
• Real-time Verification: After every major automated change, developers must verify results by checking the Claude processing summary, which lists every updated column and measure.
• DAX Error Check: If renaming occurs, developers should confirm that Claude has successfully validated the new DAX syntax across all dependent measures.
