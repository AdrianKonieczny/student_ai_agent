# STUDENT AI AGENT
**Overview**
The Student Agent is an advanced automation tool built in n8n that serves as a personal assistant for students. It streamlines common student tasks by managing emails, calendar events, and responding to academic requests through a Telegram interface. The system uses AI models (primarily GPT-4o-mini) to process natural language requests and perform actions on behalf of the student.

![image](https://github.com/user-attachments/assets/2547cd1d-675a-44b2-826a-b5abed10924c)

## Key Features

![image](https://github.com/user-attachments/assets/33879434-82f2-40d5-890e-e54d34805009)

**Email Management**

- Email Monitoring: Continuously polls the student's inbox for new messages
- Email Summarization: Automatically generates concise summaries of incoming emails
- Response Generation: Creates contextually appropriate email responses when requested
- Draft Creation: Saves email replies as drafts in Outlook for later review and sending

**Calendar Management**

- Event Creation: Creates calendar events with title, start time, and end time
- Event Retrieval: Lists upcoming calendar events in chronological order
- Event Deletion: Removes calendar events when requested

**Task Assistance**

- Academic Support: Processes and responds to various academic requests
- Note Taking: Creates and saves notes to Notion when requested
- Task Documentation: Maintains organized records of completed tasks

_System Architecture_
The Student Agent employs a multi-agent architecture with specialized components:

_Agent Manager_
Routes incoming requests to the appropriate specialized agent

Analyzes user requests to determine whether they require administrative handling or more complex task processing
Makes a clear binary decision: AGENT_ADMINISTRATION or AGENT_TASK


**Administration Agent (AGENT_ADMINISTRATION):**

- Handles email-related queries and management
- Manages calendar scheduling and events (creating, fetching, and deleting events)
- Processes routine administrative requests
- Has access to Microsoft Outlook email and calendar tools


**Task Agent (AGENT_TASK):**

- Handles complex academic tasks and research questions
- Creates formatted content for Notion
- Processes and responds to detailed student queries
- Focuses on producing Notion-compatible formatted responses
- Does not have direct calendar or email management capabilities



**Agent Selection Logic**
The workflow includes a dedicated agent selection process to ensure requests are handled by the most appropriate agent:

![image](https://github.com/user-attachments/assets/618c5be7-50cf-4a1c-98e4-bc37ce5924bf)

**Input Processing**
When a message is received via Telegram, it's first sent to the Agent Manager
Analysis Phase: The Agent Manager analyzes the content using GPT-4o-mini with the instruction to determine which agent is most appropriate
Decision Criteria:

**AGENT_ADMINISTRATION**
Selected for email management, calendar operations, and general administrative tasks
AGENT_TASK: Selected for more complex academic queries, research questions, and content that may need to be saved to Notion


Routing: Based on the Agent Manager's decision, the message is routed to either AGENT_ADMINISTRATION or AGENT_TASK through an "agent selection" If-node
Processing: The selected agent processes the request with its specific tools and capabilities
Response: The agent generates a response which is sent back to the user via Telegram

This clear separation of responsibilities ensures that each request is handled by the agent with the most appropriate tools and capabilities for the specific task.
Workflow Examples
Email Processing Workflow

New email arrives in Outlook inbox
Notification Agent creates a summary of the email
System sends email summary via Telegram
Student decides whether to respond
If responding, student provides message content
System generates an expanded response and confirms with student
Upon confirmation, system creates an email draft in Outlook

Calendar Management Workflow

Student requests to create a new event via Telegram
Agent Manager routes request to Administration Agent
If information is incomplete, system asks follow-up questions
System creates the event in Outlook calendar
Confirmation message sent to student with event details

Task Processing Workflow

Student submits a task via Telegram
Agent Manager routes request to Task Agent
Task Agent processes request and generates response
System offers option to save to Notion
If confirmed, content is saved as a Notion page
Confirmation message sent to student

Technical Specifications
AI Models

Primary LLM: GPT-4o-mini
Secondary LLM (for complex tasks): GPT-4

**Integrations**

Microsoft Outlook: Email and calendar management
Telegram: User interface and communication
Notion: Note-taking and task documentation

**Memory Management**

Context window memory for maintaining conversation history
Session-based memory for tracking user interactions
Custom key-based memory for email threading

**Language Support**

Primary language: English

Security and Privacy
The system maintains connection to the student's accounts via OAuth2 authentication for Microsoft services and API tokens for Telegram and Notion. All data processing occurs within the n8n workflow environment, with no external data storage beyond the integrated services.
Future Enhancements
Potential areas for expansion include:

Integration with learning management systems
File management capabilities
Meeting preparation and follow-up automation
Assignment tracking and deadline reminders
