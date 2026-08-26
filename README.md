# 🌊 JalSaathi: AI Chatbot for Groundwater Data (INGRES)

> **Making India's groundwater data accessible through natural language.**

JalSaathi is an **AI-powered conversational interface for groundwater resource data from INGRES (India Ground Water Resource Estimation System)**. It allows users to query complex groundwater datasets using natural language and receive structured answers, statistical insights, comparisons, and visualizations without manually navigating large datasets.

---

## 🎥 Project Demo

> **Demo video below...**

<div align="center">

📹 **JalSaathi — Product Walkthrough**


[▶️ **Watch JalSaathi Demo**](src/jalsaathi-demo_iUvfpDXe.mp4)

</div>

<!-- Replace this placeholder with the actual demo once uploaded -->

```text
docs/
└── demo.mp4
```

---

# 📖 Background

The **Assessment of Dynamic Ground Water Resources of India** is conducted annually by the **Central Ground Water Board (CGWB)** and State/UT Ground Water Departments under the coordination of the **Central Level Expert Group (CLEG), DoWR, RD & GR, MoJS**.

The assessment is managed through **INGRES (India Ground Water Resource Estimation System)**, a GIS-based web application developed by **CGWB and IIT Hyderabad**.

🔗 [INGRES Portal](https://ingres.iith.ac.in/home)

INGRES provides groundwater-resource information including:

* 💧 Annual groundwater recharge
* 💧 Extractable groundwater resources
* 📊 Total groundwater extraction
* 📈 Stage of groundwater extraction
* 🗺️ Assessment-unit level information
* 📅 Historical assessment data

Assessment units such as **Blocks, Mandals, and Taluks** are categorized according to their groundwater extraction status:

| Category              | Description                                         |
| --------------------- | --------------------------------------------------- |
| 🟢 **Safe**           | Groundwater resources are within sustainable limits |
| 🟡 **Semi-Critical**  | Groundwater development indicates increasing stress |
| 🟠 **Critical**       | Groundwater resources are under significant stress  |
| 🔴 **Over-Exploited** | Groundwater extraction exceeds sustainable limits   |

While the information is available through the INGRES ecosystem, extracting specific insights from large historical and current datasets can be difficult without technical knowledge of the underlying data.

---

# 💡 The Problem

Groundwater datasets contain large amounts of information distributed across multiple dimensions:

* States
* Districts
* Blocks / Mandals / Taluks
* Assessment years
* Groundwater recharge
* Extractable resources
* Groundwater extraction
* Extraction percentages
* Resource availability
* Assessment categories

Answering a seemingly simple question can therefore require manually filtering large datasets or understanding their database structure.

For example:

> **"Which districts in Rajasthan had the highest groundwater extraction in the latest assessment?"**

or:

> **"How has groundwater extraction in Maharashtra changed between 2020 and 2024?"**

or:

> **"Which assessment units are classified as over-exploited?"**

JalSaathi addresses this problem by providing a **natural-language interface over the groundwater data**.

---

# 🤖 The Solution — JalSaathi

JalSaathi acts as a conversational data assistant that translates natural-language questions into structured database queries and converts the retrieved results into understandable responses.

```text
                         USER
                           │
                           ▼
                 Natural Language Query
                           │
                           ▼
                  ┌─────────────────┐
                  │   JalSaathi AI  │
                  │  Query Engine   │
                  └────────┬────────┘
                           │
                           ▼
                 Schema Understanding
                           │
                           ▼
                    SQL Generation
                           │
                           ▼
                   Query Validation
                           │
                           ▼
                  INGRES Groundwater
                       Database
                           │
                           ▼
                 Result Processing
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
        Structured Answer        Visualization
              │                         │
              └────────────┬────────────┘
                           ▼
                          USER
```

The objective is to bridge the gap between **large-scale groundwater datasets and human-readable insights**.

---

# ✨ Key Features

## 🤖 Natural Language Querying

Users can ask questions about groundwater data using everyday language.

There is no requirement to manually write SQL queries or understand the underlying database schema.

---

## 📊 Groundwater Data Exploration

JalSaathi provides conversational access to groundwater information such as:

* Groundwater recharge
* Extractable resources
* Groundwater extraction
* Stage of groundwater extraction
* Assessment categories
* Regional statistics
* Historical comparisons

---

## 📅 Historical Data Analysis

Users can query groundwater information across assessment years and perform historical comparisons.

For example:

```text
User:
"Compare groundwater extraction in Maharashtra
between 2020 and 2024."

JalSaathi:
[Historical comparison + data visualization]
```

---

## 📈 Interactive Visualizations

Depending on the query, results can be represented through:

* Tables
* Charts
* Trend analysis
* Rankings
* Comparisons
* Regional summaries

This makes large datasets easier to interpret.

---

## 💬 Conversational Follow-Up Queries

JalSaathi maintains the context of a conversation, allowing users to progressively refine their questions.

```text
User:
"Show groundwater extraction in Maharashtra."

JalSaathi:
[Data + visualization]

User:
"Which district has the highest extraction?"

JalSaathi:
[District ranking]

User:
"How has it changed since 2020?"

JalSaathi:
[Historical trend]
```

This allows users to explore the dataset naturally instead of starting a new search for every question.

---

## 🌍 Multilingual Accessibility

JalSaathi is designed with **Indian-language accessibility** in mind, enabling groundwater information to become more accessible to users who may prefer interacting in regional languages.

---

# 🧠 AI Query Architecture

The core of JalSaathi is its natural-language-to-SQL query pipeline.

```text
                 User Question
                       │
                       ▼
            Natural Language Input
                       │
                       ▼
              Schema / Context
                  Understanding
                       │
                       ▼
                SQL Generation
                       │
                       ▼
               Query Validation
                       │
                       ▼
                Database Query
                       │
                       ▼
               Result Processing
                       │
                       ▼
             Response Generation
                       │
                       ▼
              Answer / Chart / Table
```

The query engine is designed to work with a **deterministic database schema**, significantly reducing ambiguity during SQL generation.

---

# 🗂️ Canonical Header Names

One of the key technical challenges with the INGRES datasets is the complexity of the original column headers.

Source headers may contain:

* Multiple hierarchical levels
* Dimensions
* Units
* Special characters
* Long descriptions
* Similar field names

To make SQL generation more reliable, JalSaathi derives **deterministic, human-readable canonical column names** from the original headers.

### Generator

```text
src/utils/generate_canonical_header_map.py
```

### Generated Mapping

```text
header_flat_csv/INGRES_header_canonical_map.json
```

---

## Canonical Naming Convention

Original header components are converted into a consistent `snake_case` representation.

The naming convention follows:

```text
<original_header_parts>_<dimension>_<unit>
```

### Dimension suffixes

```text
_c
_nc
_pq
_total
```

### Unit suffixes

```text
_mm
_ha_m
_percent
```

This produces predictable names that are easier for both developers and the AI query engine to interpret.

For example:

```text
annual_recharge_total_ha_m
groundwater_extraction_percent
```

---

# 🗄️ Runtime Database Views

At runtime, JalSaathi creates:

```text
v_<table>
```

SQLite views containing the canonical column aliases.

The AI query engine is instructed to **prefer these canonical views** when generating SQL queries.

This helps reduce errors caused by:

* Long source column names
* Multi-level headers
* Inconsistent naming
* Embedded units
* Special characters
* Similar field names
* Ambiguous schema descriptions

The canonical mapping therefore acts as an abstraction layer between the **raw INGRES schema** and the **AI query engine**.

---

# 🔄 End-to-End Data Flow

```text
                         INGRES DATA
                              │
                              ▼
                      Data Preparation
                              │
                              ▼
                    Header Normalization
                              │
                              ▼
                  Canonical Header Mapping
                              │
                              ▼
                       SQLite Tables
                              │
                              ▼
                       SQLite Views
                      (v_<table>)
                              │
                              ▼
                     JalSaathi AI Engine
                              │
                 ┌────────────┴────────────┐
                 │                         │
                 ▼                         ▼
          Schema Understanding       Query Generation
                 │                         │
                 └────────────┬────────────┘
                              ▼
                       Query Validation
                              │
                              ▼
                        SQL Execution
                              │
                              ▼
                       Result Processing
                              │
                 ┌────────────┴────────────┐
                 │                         │
                 ▼                         ▼
             Data Table              Visualization
                 │                         │
                 └────────────┬────────────┘
                              ▼
                       Natural Language
                           Response
```

---

# 🧩 System Components

## 1. Data Preparation Layer

Responsible for preparing INGRES data for efficient querying.

Responsibilities include:

* Dataset collection
* Data cleaning
* Dataset structuring
* Header normalization
* Canonical header generation
* Historical and current assessment preparation

---

## 2. Database Layer

Provides structured access to the groundwater datasets.

Responsibilities include:

* Data storage
* Table creation
* SQLite view generation
* Canonical column aliases
* SQL query execution
* Historical data access

---

## 3. AI Query Engine

The AI query engine converts user questions into executable database queries.

Responsibilities include:

* Natural-language understanding
* Schema interpretation
* SQL generation
* Query validation
* Query execution
* Result interpretation
* Conversational context handling

---

## 4. Chat Interface

The frontend provides the conversational interface through which users interact with JalSaathi.

It supports:

* Natural-language questions
* Follow-up queries
* Structured responses
* Data tables
* Visualizations
* Conversational exploration

---

## 5. Visualization Layer

Retrieved groundwater data can be transformed into visual representations including:

```text
Tables
Charts
Trend Lines
Rankings
Comparisons
Regional Summaries
```

This enables users to understand patterns within the data rather than simply receiving raw database results.

---

# 🌟 Impact

JalSaathi is designed to make India's groundwater information more accessible to users across different domains.

### 👨‍🔬 Researchers

Explore historical groundwater patterns, regional differences, and resource trends without manually processing large datasets.

### 🏛️ Policymakers & Planners

Quickly access groundwater indicators and regional statistics to support evidence-based planning and decision-making.

### 🌾 Communities & Stakeholders

Understand groundwater conditions through a simple conversational interface rather than technical datasets.

### 🎓 Students & Educators

Explore India's groundwater data interactively for research, learning, and analysis.

---

# 🛠️ Technology Stack

| Component        | Technology                  |
| ---------------- | --------------------------- |
| AI / Query Layer | LLM-based Query Engine      |
| Backend          | FastAPI                     |
| Database         | SQLite                      |
| Data Processing  | Python                      |
| Frontend         | Web-based Chat Interface    |
| Visualization    | Interactive Charts & Tables |
| Data Source      | INGRES                      |
| Query Language   | SQL                         |

---

# 📌 Project Status

🟢 **Completed & Functional**

JalSaathi provides an end-to-end working system for conversational groundwater data exploration.

### Implemented

* ✅ INGRES dataset integration
* ✅ Current and historical groundwater data
* ✅ Data preparation and structuring
* ✅ Header normalization
* ✅ Canonical header generation
* ✅ SQLite database integration
* ✅ Canonical database views
* ✅ Natural-language query processing
* ✅ AI-powered SQL generation
* ✅ SQL query validation
* ✅ Database query execution
* ✅ Conversational follow-up queries
* ✅ Structured data responses
* ✅ Interactive visualizations
* ✅ Groundwater comparisons and analysis
* ✅ Web-based chatbot interface

---

# 🚀 Getting Started

## Prerequisites

Make sure the following are installed:

* Python 3.x
* SQLite
* Required Python dependencies
* Configured AI/API credentials

---

## Clone the Repository

```bash
git clone <repository-url>
cd JalSaathi
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Configure Environment Variables

Create the required environment configuration based on the project's environment template.

```bash
cp .env.example .env
```

Add the required API and application credentials.

> **Never commit API keys, secrets, or production credentials to the repository.**

---

## Run the Application

Follow the project-specific startup configuration to launch the backend and frontend components.

Once running, open the JalSaathi web interface and begin querying the groundwater dataset using natural language.

---

# 🤝 Contributing

Contributions are welcome.

```bash
# Fork the repository

# Create a feature branch
git checkout -b feature/your-feature

# Commit your changes
git commit -m "Add your feature"

# Push the branch
git push origin feature/your-feature
```

Then open a Pull Request.

---

# 📜 License

This project is intended for **research and educational purposes**.

Any production deployment or public-facing integration involving INGRES data should follow the applicable policies, licensing requirements, and guidelines of the relevant authorities, including **MoJS, CGWB, and IIT Hyderabad**.

---

# 🌊 JalSaathi

> **Ask the data. Understand the water.**

**JalSaathi — making India's groundwater data conversational.**

<div align="center">

🌊 **AI × Data × Groundwater**

</div>
