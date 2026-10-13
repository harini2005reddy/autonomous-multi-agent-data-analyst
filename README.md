# Autonomous Multi-Agent AI Data Analyst & Business Intelligence Platform

### An Agentic AI System for Reliable, Explainable, and Interactive Data Analytics

An AI-powered data analysis platform that enables users to explore CSV datasets using natural language. Built with **LangGraph, FastAPI, Python, and React**, the system combines multi-agent orchestration, deterministic data processing, SQL validation, controlled Python execution, and interactive visualizations to deliver evidence-based business insights.

The platform is designed to transform raw data into actionable intelligence through stateful analytical workflows, conversational memory, automated error recovery, and transparent execution reporting.

**Core capabilities:** Multi-Agent AI · Natural Language Analytics · Validated SQL · Python Execution · Business Intelligence · RAG-Ready Architecture · Observability

---

## Key Features

- **Multi-Agent Orchestration:** A LangGraph supervisor coordinates specialized workers for planning, execution, validation, visualization, and reporting.
- **Natural Language Data Analysis:** Ask questions about uploaded CSV datasets without manually writing SQL or Python.
- **Deterministic Computation:** Use DuckDB, Pandas, and NumPy to calculate results from actual data rather than relying on an LLM to invent numerical answers.
- **SQL Validation:** Validate generated SQL before execution to reduce query errors and restrict unsafe operations.
- **Controlled Python Execution:** Apply Python AST checks and subprocess timeouts to reduce execution risks.
- **Conversational Memory:** Maintain analytical context across follow-up questions using LangGraph checkpointing and PostgreSQL.
- **Automated Error Recovery:** Use validation, reflection, and bounded retries to recover from failed analytical operations.
- **Interactive Visualizations:** Generate charts and explore analytical results through an interactive frontend.
- **Explainable Results:** Present generated queries, execution details, results, and supporting insights.
- **Observability Dashboard:** Track execution latency, success rates, retry behavior, and workflow activity.
- **MCP Tool Integration:** Expose analytical tools through the Model Context Protocol, with local fallback implementations.

## System Architecture

The platform follows a stateful, multi-agent workflow that separates reasoning from computation.

```text
                    User Question
                          |
                          v
                 LangGraph Supervisor
                          |
                          v
                   Analysis Planner
                          |
                          v
                Specialized AI Workers
                          |
           +--------------+--------------+
           |              |              |
           v              v              v
       SQL Agent      Python Agent   Visualization
           |              |              |
           v              v              |
     SQL Validation   AST Validation     |
           |              |              |
           v              v              |
      DuckDB /       Controlled Python  |
     PostgreSQL        Execution         |
           |              |              |
           +--------------+--------------+
                          |
                          v
                  Result Validation
                          |
                  +-------+-------+
                  |               |
                  v               v
               Success       Retry / Recovery
                  |               |
                  v               +----> Planner
             Insight Generation
                  |
                  v
             Final AI Report
                  |
                  v
          Interactive React UI
```

The precise workflow depends on the user's question and the tools selected for execution.

## Analytical Workflow

1. **Dataset ingestion:** Upload a CSV file and inspect its structure, columns, data types, and missing values.
2. **Question understanding:** Interpret the user's natural-language request and identify the required analytical operations.
3. **Planning:** Generate an execution plan using the LangGraph workflow.
4. **Query generation:** Construct SQL or Python code when required.
5. **Validation:** Check generated operations before execution.
6. **Deterministic execution:** Execute approved operations against the dataset.
7. **Result inspection:** Review outputs and recover from failures when possible.
8. **Insight generation:** Generate a report grounded in computed results.
9. **Visualization:** Present charts, metrics, and explanations through the frontend.
10. **Follow-up analysis:** Use persisted conversational context to answer related questions.

## Validation, Safety & Reliability

The system combines LLM-based reasoning with deterministic execution and validation mechanisms.

| Component | Purpose |
|---|---|
| SQL validation | Check generated queries and restrict unsafe operations |
| Python AST checks | Detect disallowed syntax, imports, and operations |
| Subprocess timeouts | Limit execution duration |
| Reflection and retries | Attempt recovery from execution failures |
| Session isolation | Separate dataset analysis sessions |
| Grounded reporting | Generate explanations from actual execution results |
| Workflow monitoring | Record execution metrics and failures |

**Security note:** AST checks and subprocess execution are not equivalent to a hardened security sandbox. Production deployments should add operating-system or container isolation, resource limits, authentication, authorization, and strict database permissions.

## Example Use Cases

### Sales Analytics
- Identify the top seven customers by total sales.
- Analyze monthly sales trends.
- Compare revenue across product categories.
- Calculate the percentage contribution of each segment.

### Statistical Analysis
- Calculate correlations between numerical columns.
- Detect potential outliers.
- Summarize distributions and descriptive statistics.
- Compare groups using appropriate statistical measures.

### Business Intelligence
- Generate executive summaries from analytical results.
- Identify changes in important KPIs.
- Explore follow-up questions without repeating the entire analysis.
- Produce interactive visualizations to support decision-making.

## Example Questions

```text
Show the top 7 customers by total sales.

Show monthly sales trends.

Calculate the correlation between sales and quantity.

Detect outliers in sales.

Show the percentage contribution by deal size.

Compare revenue across product categories.
```

The available operations depend on the uploaded dataset and the implemented analytical tools.

## Technology Stack

| Layer | Technologies |
|---|---|
| Frontend | React, TypeScript, Tailwind CSS, Vite |
| Backend | Python, FastAPI |
| Agent orchestration | LangGraph, LangChain |
| LLM providers | Groq (Llama 3.3 70B), Gemini 2.5 Flash |
| Relational database | PostgreSQL |
| Analytical engine | DuckDB |
| Data processing | Pandas, NumPy |
| Visualization | Plotly |
| Reporting | ReportLab |
| Tool integration | Model Context Protocol (MCP) |
| Deployment | Docker, Docker Compose |

## Project Structure

```text
Autonomous-Multi-Agent-Data-Analyst/
│
├── backend/              # FastAPI and LangGraph workflows
├── frontend/              # React and TypeScript application
├── scratch/               # Supporting development files
├── screenshots/           # Application screenshots
├── uploads/               # Dataset upload directory
├── .env.example           # Environment variable template
├── .gitignore
├── docker-compose.yml     # Service configuration
├── requirements.txt       # Python dependencies
└── README.md
```

## Getting Started

### Prerequisites

Install the following tools:

- Python 3.11 or a compatible version supported by the dependencies
- Node.js and npm
- Git
- Docker Desktop with Docker Compose
- API credentials for a supported LLM provider

### 1. Clone the repository

```bash
git clone https://github.com/harini2005reddy/autonomous-multi-agent-data-analyst.git

cd autonomous-multi-agent-data-analyst
```

### 2. Configure environment variables

Create a local environment file from the supplied template.

**Windows PowerShell:**

```powershell
Copy-Item .env.example .env
```

**Linux / macOS:**

```bash
cp .env.example .env
```

Add the required API keys and database configuration to `.env`. Never commit real secrets to GitHub.

### 3. Start PostgreSQL

```bash
docker compose up -d
```

Check that the configured services are running before starting the backend.

### 4. Set up the Python backend

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

On Linux or macOS:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Start the API server:

```bash
uvicorn backend.main:app --reload
```

Backend URL: `http://localhost:8000`

### 5. Start the frontend

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

Frontend URL: `http://localhost:5173`

**Note:** These commands follow the supplied project documentation. Verify the environment variables, database configuration, available scripts, and backend entry point against the current code before running the application.

## Observability & Explainability

The platform is designed to make analytical execution easier to inspect.

Depending on the workflow and implementation, users can review:

- Generated SQL or Python operations.
- Query and execution results.
- Workflow stages and execution timing.
- Validation failures and recovery attempts.
- Charts, KPIs, and generated summaries.
- Historical execution metrics.

These details help developers debug analytical workflows and understand how reported insights were produced.

##  Current Limitations

- The documented ingestion workflow supports CSV datasets.
- Generated Python runs in subprocess-based isolation rather than a hardened container sandbox.
- MCP communication is documented as using local standard input/output transport.
- Results depend on data quality, available tools, and LLM behavior.
- Generated insights require validation before being used for consequential business decisions.
- Production deployment requires additional security, monitoring, testing, and access-control measures.

##  Potential Future Improvements

- Add multilingual document retrieval and RAG-based research.
- Introduce a dedicated reviewer agent for evidence verification.
- Support additional data sources and file formats.
- Add role-based access control and audit logging.
- Improve automated evaluation of analytical correctness.
- Add integration and regression tests for agent workflows.
- Deploy the application with production-grade isolation and monitoring.

These are proposed extensions, not claims that the features are already implemented.

##  Engineering Concepts Demonstrated

This project provides a practical foundation for exploring:

- Multi-agent orchestration with LangGraph.
- Natural-language-to-SQL workflows.
- Deterministic data processing with DuckDB and Pandas.
- Validation and recovery for LLM-generated operations.
- Persistent conversational state.
- Model Context Protocol tool integration.
- Interactive data visualization.
- API and frontend integration.
- Execution monitoring and explainable analytics.


## Author

**Harini Ravula**

GitHub: [@harini2005reddy](https://github.com/harini2005reddy)

AI Engineering · Multi-Agent Systems · Machine Learning · Backend Development

---

*An evolving project focused on building reliable, explainable, and useful AI-powered data analytics workflows.*