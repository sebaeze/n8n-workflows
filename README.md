# N8N Workflows

This repository stores a collection of N8N workflows in JSON format, focused on automating tasks using Artificial Intelligence (AI). The workflows are designed to be easily imported into N8N, allowing users to streamline their workflows and leverage the power of AI in their automation projects.

The repository is organized to facilitate collaboration and sharing of AI-driven automation workflows. Feel free to contribute your own workflows, modify existing ones, or use them as inspiration for your own projects.

## Features:
- N8N workflows in JSON format for easy import
- Focus on AI-driven automation tasks
- Collaborative repository for sharing and improving workflows

## Getting Started:
1. Clone or fork this repository to access the workflows.
2. Import the desired workflow JSON files into your N8N instance.
3. Customize and modify the workflows as needed to suit your automation needs.

## [Basic AI Agent with memory](./0_BASIC_AI_AGENT_WITH_POSTGRES_MEMORY.json)

This N8N workflow demonstrates how to create an AI Agent capable of responding to user queries about films and series, while maintaining context through Postgres-based memory. It integrates multiple nodes to process chat messages and deliver intelligent responses.

### Workflow Overview

1. Chat Trigger:
The When chat message received node listens for incoming chat messages and initiates the workflow.

2. AI Agent:
The AI Agent node processes user inputs using an expert system message. It is configured to respond only to queries about films or series. If the input is unrelated, it replies: "I can not help you since I only talk about movies and series."

3. Google Gemini Chat Model:
The Google Gemini Chat Model node provides advanced language understanding to generate responses for the AI Agent.

4. Postgres Chat Memory:
The Postgres Chat Memory node stores conversation context in a PostgreSQL database, enabling the agent to maintain a memory window of 3 previous interactions.

5. Connections
The Chat Trigger connects to the AI Agent for processing user messages.
The AI Agent integrates with the Google Gemini Chat Model for language processing and the Postgres Chat Memory for context retention.

6. Key Features
Context-aware responses using Postgres memory.
Restricted to film/series-related queries for focused expertise.
This workflow is ideal for creating specialized chatbots with persistent memory and advanced language capabilities.

## [JIRA to Excel](./1_jira_to_excel.json)

This N8N workflow  is designed to extract data from Jira based on specific criteria, convert it into an Excel file format, and save it to a specified location on disk. Below is a detailed explanation of the nodes used and how the workflow operates.

### Nodes Overview

1. **Manual Trigger (`n8n-nodes-base.manualTrigger`)**  
   - **Purpose**: Acts as the starting point of the workflow. This node allows the user to manually trigger the execution of the workflow by clicking the "Test workflow" button.

2. **Jira Software (`n8n-nodes-base.jira`)**  
   - **Purpose**: Queries Jira issues using JQL (Jira Query Language). In this example, it retrieves all issues created within the last 5 days that match specific statuses and issue types. The data fetched includes all navigable fields.

3. **Convert to File (`n8n-nodes-base.convertToFile`)**  
   - **Purpose**: Converts the JSON data retrieved from Jira into a file format. In this workflow, the data is converted into an Excel file (`.xlsx`).

4. **Read/Write Files from Disk (`n8n-nodes-base.readWriteFile`)**  
   - **Purpose**: Saves the generated Excel file to the local file system. The file is written to the path `/mnt/c/n8n_data/jira.xlsx`.

### Workflow Process

1. The **Manual Trigger** starts the workflow when the user clicks the "Test workflow" button.
2. The **Jira Software** node queries Jira for issues based on the specified JQL criteria and retrieves all relevant fields.
3. The retrieved data is passed to the **Convert to File** node, which converts the JSON data into an Excel file.
4. The Excel file is saved to the local disk using the **Read/Write Files from Disk** node.

### Use Case

This workflow is ideal for exporting Jira issues into an Excel file for reporting, analysis, or sharing purposes. It provides a practical example of how to integrate Jira with file operations in n8n.
