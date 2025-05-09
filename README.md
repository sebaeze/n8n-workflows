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

## [Basic AI Agent with memory](./0_basic_ai_agent_with_postgres_memory.json)

This N8N workflow demonstrates how to create an AI Agent capable of responding to user queries about films and series, while maintaining context through Postgres-based memory. It integrates multiple nodes to process chat messages and deliver intelligent responses.

### Nodes Used

1. **Chat Trigger (`@n8n/n8n-nodes-langchain.chatTrigger`)**  
   - **Purpose:** This node triggers the workflow whenever a chat message is received from a user. It serves as the entry point for user interaction.

2. **AI Agent (`@n8n/n8n-nodes-langchain.agent`)**  
   - **Purpose:** This node acts as the core of the workflow, processing user input messages and generating context-aware responses. It is configured to answer questions about films and series and to reject unrelated queries with a predefined response.

3. **Google Gemini Chat Model (`@n8n/n8n-nodes-langchain.lmChatGoogleGemini`)**  
   - **Purpose:** This node provides advanced language modeling capabilities through the Google Gemini Chat Model. It powers the AI agent's responses with natural language understanding and generation.

4. **Postgres Chat Memory (`@n8n/n8n-nodes-langchain.memoryPostgresChat`)**  
   - **Purpose:** This node enables memory storage for chat conversations using a Postgres database. It helps the AI agent maintain context over multiple messages by storing and retrieving recent chat history.

### Workflow Operation

1. The **Chat Trigger** node listens for incoming chat messages from users.
2. The message is passed to the **AI Agent**, which interprets the input and determines the appropriate response based on its configuration. If the input is unrelated to films or series, it provides the response: *"I can not help you since I only talk about movies and series."*
3. The **Google Gemini Chat Model** processes the user input, providing intelligent and contextually relevant responses for the AI agent.
4. The **Postgres Chat Memory** node stores the chat context in a Postgres database, allowing the AI agent to refer back to previous messages for continuity in conversations.
5. The workflow completes by delivering the AI agent's response to the user.


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

## [AI Agent Gemini Google Sheet](./2_ai_agent_gemini_google_sheet.json)

This N8N workflow is designed to create an AI agent that interprets user queries to identify the appropriate AI model. The workflow integrates with a Google Sheet to retrieve information about AI models and uses a Google Gemini Chat Model for natural language processing. Below is a detailed explanation of the nodes used and how the workflow operates.

### Nodes Overview
1. **Chat Trigger (`@n8n/n8n-nodes-langchain.chatTrigger`)**  
   - **Purpose**: Serves as the entry point of the workflow. It listens for user messages and initiates the workflow when a user query is received.
   - **Functionality**: Captures the user's input (`chatInput`) for processing.

2. **AI Agent (`@n8n/n8n-nodes-langchain.agent`)**  
   - **Purpose**: Acts as the main AI agent to interpret the user's message and respond accordingly.
   - **Functionality**:  
     - Receives the user's query from the Chat Trigger node.
     - Uses the Google Gemini Chat Model for language understanding and the Google Sheet (`lista_modelos_gemini`) for retrieving AI model information.
     - Responds in the same language as the user and ensures responses are concise (less than 100 words).  
     - If no information is found in the Google Sheet, it informs the user with the message: "*** I didn't find information about AI Models in my Database."

3. **Google Gemini Chat Model (`@n8n/n8n-nodes-langchain.lmChatGoogleGemini`)**  
   - **Purpose**: Provides advanced natural language processing capabilities to interpret and generate responses based on the user's input.
   - **Functionality**: Processes the user's query and assists the AI Agent in generating a meaningful response.

4. **Google Sheets Tool (`n8n-nodes-base.googleSheetsTool`)**  
   - **Purpose**: Connects to a Google Sheet (`lista_modelos_gemini`) that contains information about various AI models.
   - **Functionality**:  
     - Reads data from the specified Google Sheet to fetch details about AI models.
     - Provides data to the AI Agent for responding to user queries.

### Workflow Process
1. The **Chat Trigger** node starts the workflow when a user sends a message.
2. The **AI Agent** processes the user's query by leveraging the Google Gemini Chat Model for natural language understanding.
3. The **Google Sheets Tool** fetches relevant information about AI models from the connected Google Sheet (`lista_modelos_gemini`).
4. The **AI Agent** formulates a response based on the retrieved data or informs the user if no relevant information is found.

### Use Case
This workflow is ideal for scenarios where users need assistance in selecting the right AI model for their needs. It combines AI-driven natural language processing with structured data retrieval from a Google Sheet to provide accurate and concise responses. The multilingual capability ensures accessibility for users in different languages.

### Configuration
- **Google Sheet**: Ensure the sheet contains up-to-date information about AI models and is accessible via the specified document ID and sheet name.
- **Language**: The AI Agent dynamically responds in the user's language, enhancing usability for a global audience.

### Limitations
- If the Google Sheet does not contain information about a specific AI model, the workflow will notify the user that no relevant data was found.

This workflow demonstrates how to integrate AI capabilities with structured data sources in n8n to create a powerful and user-friendly solution for AI model selection.
