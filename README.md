FDA Competitive Intelligence Agent
A conversational AI agent that delivers instant competitive intelligence on any FDA-approved drug or pharmaceutical sponsor. Built with the Anthropic Claude API and a custom MCP (Model Context Protocol) server that connects directly to the OpenFDA database, the agent autonomously queries FDA drug approval records, adverse event reports, and clinical trial submissions — then reasons across all three data sources to generate a structured competitive analysis brief.

Demo

📹 Add a screen recording or GIF here showing a search for "keytruda" returning the four-section analysis


Use Case
Pharmaceutical competitive intelligence typically requires analysts to manually cross-reference multiple FDA databases — a time-consuming process that can take hours per drug. This agent automates that workflow end-to-end. Type in any drug name (e.g. keytruda, nivolumab) or sponsor name (e.g. Merck, Pfizer Inc.) and within seconds receive a structured brief covering:

Approval Overview — what has been approved, when, and under which application numbers
Clinical Trial Insights — key FDA-submitted studies and indications
Safety Profile — top adverse events by report volume from the FDA FAERS database
Competitive Takeaways — AI-synthesized strategic observations for competitive positioning


Architecture
Browser (HTML/CSS/JS)
        │
        ▼
Flask Backend (Python)
        │
        ▼
Claude API (claude-sonnet-4-6)
        │
        ▼
Custom OpenFDA MCP Server
        │
        ├── /drug/drugsfda     → Approval records
        ├── /drug/clinicaltrials → Clinical study results
        └── /drug/event        → Adverse event reports

Tech Stack

AI Model — Anthropic Claude (claude-sonnet-4-6)
Agent Framework — Anthropic Python SDK with tool use
MCP Server — Custom Python MCP server using FastMCP
Data Source — OpenFDA API (free, no API key required)
Backend — Flask (Python)
Frontend — HTML, CSS, JavaScript (single file, no framework)


Project Structure
clinical-trials-agent/
├── app.py                 # Flask backend + web UI
├── ct_mcp_server.py       # Custom OpenFDA MCP server
├── test_mcp.py            # MCP server tests
├── test_api.py            # OpenFDA API connectivity test
├── .gitignore
└── README.md

Setup & Installation
Prerequisites

Python 3.8+
An Anthropic API key (console.anthropic.com)

Steps
1 — Clone the repository
bashgit clone https://github.com/mmanjula12/clinical-trial-agent.git
cd clinical-trial-agent
2 — Create and activate a virtual environment
bash# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python -m venv venv
source venv/bin/activate
3 — Install dependencies
bashpip install anthropic mcp httpx flask python-dotenv
4 — Create a .env file
bashANTHROPIC_API_KEY=sk-ant-your-key-here
5 — Run the app
bashpython app.py
6 — Open in browser
http://127.0.0.1:5000

Example Queries
QueryWhat it returnskeytrudaMerck's PD-1 inhibitor approvals, safety profile, competitive positionnivolumabBristol-Myers Squibb Opdivo approval history and trial insightsPfizer Inc.Full portfolio overview across all Pfizer FDA approvalsMerckMerck sponsor-level competitive intelligence brief

How the Agent Works

User enters a drug name or sponsor in the browser
Flask backend receives the query and passes it to Claude
Claude decides which OpenFDA tools to call based on the query
The custom MCP server executes the FDA API calls and returns structured data
Claude reasons across all returned data and generates a four-section intelligence brief
The brief is rendered in the browser as a formatted report


Notes

OpenFDA is a free public API — no API key required
The only credential needed is an Anthropic API key stored in .env
The .env file is excluded from Git via .gitignore — never commit your API key
Analysis typically completes in 30–60 seconds depending on data volume


Author
Built by @mmanjula12 as part of a series of AI agent projects exploring the Anthropic Claude API and MCP server architecture.
