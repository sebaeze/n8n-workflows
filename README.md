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

