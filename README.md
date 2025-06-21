# n8n AI Customer Support Agent
An AI Agent workflow developed in n8n that identifies if incoming emails are customer support related, and if they are, the agent will draft a response for you in the email thread so all you have to do is review it and send it off. The agent accesses your policies and FAQs via a Pinecone vector database so you know you can trust its response.

![image](https://github.com/user-attachments/assets/dc4e82f0-8535-407b-83e4-8c8bc15289aa)


## Workflow
### Step 1: Triggering the workflow
Gmail Trigger: Monitors your Gmail inbox for incoming emails and triggers the workflow whenever a new email arrives.

Google Drive Trigger: Detects when new files (e.g., updated FAQs or policy documents) are added to a designated Google Drive folder.

### Step 2: Email preprocessing 
Edit Fields Node: Extracts and formats key details from the incoming email (e.g., sender, subject, body) to prepare for analysis.

OpenAI Message Model Node: Analyzes the email content to determine if it is related to customer support and outputs a classification result.

Switch Node: Routes the workflow; If the email is customer support-related, the workflow continues. If not, the workflow ends.

### Step 3: Document Preparation
Google Drive Download Node: Downloads the latest FAQs and policy documents from Google Drive.

Pinecone Vector Store Node: Breaks the downloaded documents into smaller, manageable chunks for efficient processing (Recursive Charecter Text Splitter). 
Uses OpenAI to generate embeddings for each document chunk, creating a vector representation (Embeddings OpenAI).
Updates the Pinecone vector database with new embeddings, ensuring the AI Agent has the latest information.

### Step 4: Generating AI-Powered Response 
AI Agent Node: Combines the email content and vector search results to generate a context-aware draft response by ensures that the response aligns with FAQs and policies.
Leverages Pinecone to search and retrieve the most relevant FAQ or policy content (Answer Questions with a Vector Store).
Fine-tunes the generated draft email response based on retrieved information (OpenAI Chat Model).

### Step 5: Drafting and Finalizing Emails
Gmail Draft Email Node: Creates a draft email in Gmail with the AI-generated response and allows you to review and send the email manually, ensuring human oversight.

![image](https://github.com/user-attachments/assets/2b0d5934-d4c9-4a8e-a1e3-f2976c1fcfa7)


The AI generated draft response aligns with the uploaded FAQ and policy document as shown in the snippet below.


![Screenshot 2025-06-21 164802](https://github.com/user-attachments/assets/de867bf0-f009-4a07-857d-82f13bdd75ed)


