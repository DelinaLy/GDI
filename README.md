# GraphRAG Dialogue Insights
GraphRAG Dialogue Insights (GDI) is a system that enables users to query work items from issue tracking systems in natural language. In addition to a natural language response, GDI returns supporting information for users to understand how the LLM queried the knowledge graph.

GDI is introduced in our submission titled "Navigating through Work Items in Issue Tracking Systems via Natural Language Queries" to Requirements Engineering Conference 2025.

## Overview of the files:
GDI (main folder)
- The knowledge graph folder contains the scripts for the original and improved version of the open-source knowledge graph. These scripts are needed to create the knowledge graphs in Neo4j.
- The prompts folder contains the prompt templates used to create prompts at run-time. The cypher_prompt.py has examples of the user questions asked by participants in the user-centered validation sessions for few-shot prompting.
- GDI.py contains the code of GDI core that falicitates interaction among the components of GDI.
- requirements.txt contains the Python packages that is used to implement GDI.

validation folder
- Questions.docx includes the questions used in the survey and the interviews.
- The onboarding folder consists of the logs of the user-centered validation sessions. The software_engineer folder contains the logs of these sessions. The software_engineer_few_shot folder contains the logs when we rerun the user questions after few-shot prompting.
- The trace link recovery folder contains the informed consent form and protocol used for the user-centered validation sessions.

# Installation Instructions
Please note due to the sensitivity of data and access rights, we used a local instance of [Llama3.1](https://ollama.com/download/windows) and Neo4j desktop to ingest the industry data. You can replace the URL in the Cypher query and directly use the files using the Docker version as well. Please follow the link for: [the installation instructions.](https://neo4j.com/docs/desktop-manual/current/)

## Prerequisites

- Python 3.9
- [Optional] An OpenAI API key: [How to get an OpenAI API key?](https://help.openai.com/en/articles/4936850-where-do-i-find-my-secret-api-key)
- Docker setup for Neo4j
- Docker setup for Ollama

### Docker setup for Neo4j

After installing Docker, run the following command in the terminal to start the Neo4j instance:
```
docker run \
    --name neo4j \
    -p 7474:7474 -p 7687:7687 \
    -d \
    -e NEO4J_AUTH=neo4j/password \
    -e NEO4J_PLUGINS=\[\"apoc\"\]  \
    neo4j:latest
```
- Use the default credits
    + username: neo4j
    + password: password
- Use one of the datasets provided under the src/knowledge graph folder, and run the script in Neo4j. 

### Docker setup for Ollama
- Ollama is an open-source tool that lets you run advanced AI models on your computer. This ensures your data remains private and secure, as it never leaves your device. Running models locally also improves reliability, eliminating the need for internet connectivity.
- For CPU only run the following docker container:
```
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```
- After successfully running the docker container type in the below command in the terminal.
```
ollama run llama3.2
```
To run Ollama using GPU, more steps are needed, please follow the link to setup Ollama: [Run Ollama using GPU Instructions](https://hub.docker.com/r/ollama/ollama)


### Running GDI

- Set up a virtual environment in Python. [Follow this link for instructions.](https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/)
- Clone the repository and switch to the source branch. 
- Run the following command to install the requirements:
```
pip install -r requirements.txt
```
To start GDI,  use the following command inside the src folder:
```
streamlit run GDI.py
```

The source code of GDI is licensed under GNU GPLv3.
