# ChatGPT Code-Interpreter

A multi-agent system built with LangChain to interpret and execute Python code based on user queries. The system integrates multiple agents, including a **Python Agent**, a **CSV Agent**, and a **Router Agent**, to process and respond to natural language input. The agents work together to handle various tasks, such as executing Python code or processing data from a CSV file.

## Features

- **Python Agent**: Transforms natural language into Python code, executes the code in a Python REPL environment, and returns the result.
- **CSV Agent**: Interacts with a CSV file (`episode_info.csv`) to answer questions based on the data using pandas calculations.
- **Router Agent**: Routes queries to the appropriate agent (either Python Agent or CSV Agent) based on the question's nature.
- **QR Code Generation**: Generates QR codes pointing to a URL based on user instructions.
- **Multi-Agent System**: Uses a combination of multiple agents to handle different tasks.

## Project Setup

To run this project locally, follow these steps:

### Prerequisites

Make sure you have the following installed:

- **Python 3.12** (or compatible version)
- **Pipenv** (for managing dependencies)
- **API keys** for services like OpenAI (if required for your model)

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Madhusanka-slc/code-interpreter-genai.git
   ```

2. **Navigate to the project folder**:
   ```bash
   cd code-interpreter-genai

   ```

3. **Install dependencies using Pipenv**:
   ```bash
   pipenv install
   ```

4. **Install development dependencies (if required)**:
   ```bash
   pipenv install --dev


5. **Set up environment variables**:
   - Create a `.env` file in the project directory.
   - Add any necessary environment variables (e.g., API keys) as described in the `.env.example` file.

### Running the Project

1. **Activate the virtual environment**:
   ```bash
   pipenv shell
   ```

2. **Run the project**:
   ```bash
   python main.py
   ```

3. Open your terminal and check the output.

### How to Use

Once the system is running, you can interact with the agents by providing queries in natural language. Some example queries include:

- **Python Agent**:
  - "What is 10 + 20?"
  - "Generate and save 15 QR codes pointing to `www.udemy.com/course/langchain`"
  
- **CSV Agent** (requires the `episode_info.csv` file):
  - "Which season has the most episodes?"
  
The **Router Agent** will automatically route the queries to the appropriate agent based on the nature of the query.

### Technologies Used

- **LangChain**: A framework for building applications using large language models (LLMs).
- **OpenAI GPT-4**: Used as the LLM for generating responses.
- **Pandas**: Used by the CSV Agent for data manipulation and analysis.
- **QR Code Generation**: Uses the `qrcode` library to generate QR codes.
- **Python REPL Tool**: Used to execute Python code dynamically in response to user queries.
- **.env**: For loading environment variables securely.

## Multi-Agent System

This project uses a multi-agent setup with three main agents:

1. **Python Agent**: 
   - Executes Python code and returns the result.
   - Uses the `PythonREPLTool` to run Python code in a REPL environment.

2. **CSV Agent**: 
   - Interacts with a CSV file (`episode_info.csv`).
   - Uses pandas for calculations and analysis based on the data.

3. **Router Agent**: 
   - Routes the user query to the appropriate agent.
   - If the query requires code execution, it directs the query to the **Python Agent**.
   - If the query involves data analysis, it routes to the **CSV Agent**.

## Python REPL Tool

The **Python REPL Tool** is used to dynamically execute Python code in response to user queries. When the Python Agent receives a query, it translates the natural language into Python code, runs the code in the REPL, and returns the result.

Example:

- **Query**: "What is 5 + 5?"
- **Execution**: The agent translates it into Python code (`5 + 5`), executes it, and returns the result (`10`).

### Example Code

Here’s an example of how the **Python Agent** is integrated into the system:

```python
from langchain_experimental.tools import PythonREPLTool
from langchain.agents import create_react_agent
from langchain_openai import ChatOpenAI

tools = [PythonREPLTool()]
python_agent = create_react_agent(
    prompt=prompt,
    llm=ChatOpenAI(temperature=0, model="gpt-4-turbo"),
    tools=tools,
)

python_agent_executor = AgentExecutor(agent=python_agent, tools=tools, verbose=True)
```

### Example Queries

- **Python Agent**: 
  - "What is the sum of 10 and 20?"
  - "Generate 10 QR codes pointing to `www.example.com`"

- **CSV Agent**:
  - "Which season has the most episodes in the `episode_info.csv`?"

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
