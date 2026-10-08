# NetProbe MCP

**AI-native security observability and defensive automation through Model Context Protocol (MCP).**

NetProbe MCP is a Python/FastMCP security agent for Windows-oriented telemetry, SOC-style evidence collection, explainable MITRE ATT&CK mapping, report generation, and controlled defensive actions. It is designed to make operational security data available to MCP-compatible AI clients through structured tools rather than free-form shell execution.

## What the current repository actually implements

- FastMCP-based MCP server in Python.
- Listening-port and connection inspection.
- Process and security-event telemetry.
- Recording sessions and persisted evidence snapshots.
- Explainable MITRE ATT&CK heuristic mapping.
- SOC-oriented severity scoring and assessment helpers.
- Structured JSON/CSV/HTML export paths.
- Report generation with HTML/PDF-capable components.
- Defensive firewall action tooling.
- Windows / PowerShell execution wrappers with structured return values.
- Public example SOC report and recorded telemetry artifacts.

## Architecture

~~~text
MCP-compatible client / AI agent
            |
            v
        FastMCP server
            |
            +--> telemetry tools
            +--> Windows / PowerShell collectors
            +--> recording sessions
            +--> MITRE mapping + severity logic
            +--> SOC assessment / report generation
            +--> controlled defensive actions
            |
            v
   structured evidence and reports
~~~

## Technology

- Python 3.12+
- FastMCP
- psutil
- PowerShell / Windows system interfaces
- requests
- matplotlib
- fpdf2
- uvicorn

## Quick start

~~~bash
git clone https://github.com/ivin-santhosh/netprobe-mcp.git
cd netprobe-mcp
~~~

Using `uv`:

~~~bash
uv sync
uv run python main.py
~~~

Or with standard Python tooling:

~~~bash
python -m venv .venv
.venv\Scripts\activate
pip install -e .
python main.py
~~~

> Several collectors and defensive actions are Windows-specific and some operations require administrator privileges.

## Public evidence

A generated SOC report is included in the repository:

https://github.com/ivin-santhosh/netprobe-mcp/blob/main/soc_report_v2.html

The repository also includes recorded security snapshots under `recordings/`, allowing the telemetry and assessment output to be inspected directly.

## Security model

NetProbe is intended only for authorized defensive administration and observability. The current implementation favors structured Python/PowerShell wrappers and explicit MCP tools so actions can be validated and results returned as structured data.

Because some tools can change system state (for example firewall actions), they should be used only on systems and networks where the operator has explicit authorization.

## Why it matters

The project demonstrates a practical bridge between agentic AI and operational tooling:

- AI does not need to invent system state; it can query structured tools.
- Security evidence can be persisted and audited.
- MITRE mappings and severity logic can be inspected rather than hidden.
- Defensive actions can be exposed as discrete tools instead of arbitrary shell access.

## Status

NetProbe MCP is an active engineering project. The current repository contains working security-observability and reporting code plus experimental automation material. Roadmap ideas should not be interpreted as completed features unless they are present in the implementation.

## Project URL

https://github.com/ivin-santhosh/netprobe-mcp
