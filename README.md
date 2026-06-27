# 🤖 Text-to-SQL RAG Chatbot

A Generative AI-powered chatbot that lets non-technical users query a database using plain English — no SQL knowledge required.

---

## 📌 About the Project

This project implements a **Text-to-SQL chatbot** that bridges the gap between natural language and database queries. Users simply ask a question in plain English, and the system:

1. Converts it into a valid SQL query using an LLM
2. Executes the query directly against the database
3. Returns the result in a clear, readable format

The architecture is **completely domain-agnostic** and can be adapted for any industry — retail, healthcare, sales, marketing, and more.

---

## 🏗️ Architecture & Workflow

```
User Question (Natural Language)
        │
        ▼
Schema Extraction (SQL Chain Retriever)
        │
        ▼
Prompt Formulation (Question + Schema Context)
        │
        ▼
SQL Generation (Google Gemini LLM)
        │
        ▼
Query Execution (MySQL Database)
        │
        ▼
Result (e.g., "$1.5 million" or "15 orders")
        │
        ▼
[Optional] Natural Language Response Layer
```

| Step | Description |
|------|-------------|
| **1. Data Ingestion & Storage** | Raw data from Excel sheets is pre-processed and loaded into a MySQL database |
| **2. Schema Extraction** | A SQL chain retriever fetches table names, column names, and entity relationships (PKs/FKs) |
| **3. Prompt Formulation** | User input is combined with the extracted schema in a prompt template to provide LLM context |
| **4. SQL Generation** | Google Gemini parses the context and user intent to generate an accurate SQL query |
| **5. Query Execution** | The generated SQL is parsed and executed on the MySQL database |
| **6. Response (Optional)** | An additional LLM layer can reformat raw output into a conversational sentence |

---

## 💻 Tech Stack

| Component | Technology |
|-----------|------------|
| **Language** | Python (Jupyter Notebooks) |
| **Database** | MySQL & MySQL Workbench |
| **LLM** | Google Gemini 2.0 Flash API *(production used AWS Bedrock with Nova Pro)* |
| **Frameworks** | LangChain (`SQLDatabase`, `create_sql_query_chain`, `langchain_google_genai`) |
| **Evaluation** | RAGAS + Hugging Face Embeddings |

---

## 📊 Dataset

This project uses a dummy **retail and sales dataset** simulating a relational database across interconnected Excel sheets.

| Table | Key |
|-------|-----|
| `customers` | Primary Key: `customer_index` |
| `sales_orders` | Primary Key: `order_number` — linked to customers & products |
| `products` | — |
| `regions` | — |
| `state_regions` | — |
| `budgets` | — |

---

## 🧪 Evaluation

Generated SQL queries are evaluated using the **RAGAS framework**, tested against a ground-truth dataset of pre-written questions and queries built from domain knowledge.

| Metric | Description |
|--------|-------------|
| **Context Precision** | Measures the relevance of the retrieved schema and context |
| **Helpfulness** | Evaluates whether the response meets user expectations (adapted Google helpfulness rubric) |

---

## 🚀 Future Enhancements

- [ ] **Multi-LLM Benchmarking** — Test against OpenAI, Llama (Tiny Llama), and Anthropic Claude; compare performance across models
- [ ] **Advanced NLP Metrics** — Add BLEU, ROUGE, and METEOR scores to the evaluation pipeline
- [ ] **Frontend Application** — Build a web UI using Flask or Streamlit
- [ ] **Cloud Deployment** — Deploy to AWS, Azure, GCP, or Heroku for public access

---

## 📁 Project Structure

```
text-to-sql-rag-chatbot/
├── notebooks/          # Jupyter notebooks for development & experimentation
├── data/               # Raw Excel datasets
├── evaluation/         # RAGAS evaluation scripts and ground-truth datasets
└── README.md
```

---

## 🛠️ Getting Started

### Prerequisites

- Python 3.8+
- MySQL Server & MySQL Workbench
- Google Gemini API key

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/text-to-sql-rag-chatbot.git
cd text-to-sql-rag-chatbot

# Install dependencies
pip install langchain langchain-google-genai sqlalchemy pymysql ragas

# Set your API key
export GOOGLE_API_KEY="your-api-key-here"
```

### Usage

Open the Jupyter notebooks in the `notebooks/` directory and follow the step-by-step instructions to connect your database, configure the LLM, and start querying in natural language.
