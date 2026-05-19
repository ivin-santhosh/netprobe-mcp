<p align="center">
  <h1 align="center">🌐 Netprobe MCP</h1>
  <p align="center">
    <strong>The AI-Native Cyber Intelligence & Observability Platform</strong>
    <br />
    Bridging the gap between cognitive Large Language Models and core network execution.
  </p>
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/badge/version-1.0.0-blue.svg?cacheSeconds=2592000" />
  <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  <img alt="Protocol: MCP" src="https://img.shields.io/badge/Protocol-Model_Context_Protocol-purple.svg" />
  <img alt="Platform: Node.js | Rust" src="https://img.shields.io/badge/Platform-Node.js_%7C_Rust-green.svg" />
</p>

---

## 📖 Table of Contents
- [About the Project](#-about-the-project)
- [The Problem vs. The Solution](#-the-problem-vs-the-solution)
- [Core Architecture & Features](#-core-architecture--features)
- [Getting Started](#-getting-started)
- [Usage & Integration](#-usage--integration)
- [Security & Validation](#-security--validation)
- [Roadmap](#-roadmap)
- [Disclaimer](#-disclaimer)
- [Contributing](#-contributing)

---

## ⚡ About the Project

**Netprobe MCP** (the foundational architecture of **Protocol AETHER**) is an open-source, Model Context Protocol (MCP) server engineered to transform conversational AI from a passive advisory tool into an active, intelligent orchestrator of system defense.

Traditionally, an AI can recommend a network scan or a firewall rule but cannot execute it. Netprobe provides a highly secure, deterministic translation layer that allows LLMs (like Claude) to safely invoke command-line network diagnostic tools (e.g., Masscan), parse the raw output into structured JSON, and deliver immediate, autonomous insights.

## 🎯 The Problem vs. The Solution

### The Problem: The "Brain in a Vat"
Security analysts suffer from "alert fatigue" and highly fragmented workflows. When an anomaly occurs, an analyst must swivel between standalone utilities (Masscan, Wireshark, SIEMs). When asking an AI for help, the human becomes a biological API—manually copying AI commands to a terminal, and pasting massive walls of raw output back to the AI. This loop drastically inflates response times and nullifies autonomous threat neutralization.

### The Solution: Agentic Infrastructure
Netprobe MCP acts as the "hands" for the AI's "brain." By establishing a secure bidirectional communication layer (via stdio or SSE), it exposes complex network utilities as native capabilities. The AI determines *what* needs scanning, Netprobe handles the *how* (safely executing child processes and parsing stdout), and the AI returns the *why* (natural language threat analysis).

---

## 🧠 Core Architecture & Features

Netprobe is designed as a modular cyber operating system. 

* **📡 Telemetry Collection:** Ingests raw data via high-speed asynchronous network probes (focusing initially on Masscan).
* **🛡️ Intent Translation & Validation:** Converts natural language LLM intent into strict JSON-RPC requests, sanitizing all IPs and port ranges to prevent command injection.
* **📊 Structured Output Parsing:** Intercepts messy terminal output and structures it into deterministic JSON schemas, preventing AI data hallucination.
* **🧠 Explainable AI Analysis:** Feeds structured network state back to the LLM for behavioral analytics and plain-English threat explanations.
* **⚡ Automated Response Orchestration:** Lays the groundwork for autonomous playbooks—isolating hosts or blocking IPs dynamically based on correlated alerts.

---

## 🚀 Getting Started

### Prerequisites

To run Netprobe MCP, ensure you have the following installed on your host machine or containerized environment:

* **Node.js** (v18+) or **Rust** toolchain
* **Masscan** (Must be installed and accessible in your system `$PATH`)
* **Network Interface Card (NIC)** with permissions for raw socket access (e.g., `CAP_NET_RAW` on Linux).

### Installation

1. Clone the repository:
   ```bash
   git clone [https://github.com/yourusername/netprobe-mcp.git](https://github.com/yourusername/netprobe-mcp.git)
   cd netprobe-mcp
   ```

2. Install dependencies:
   ```bash
   npm install
   # or 'cargo build --release' if using the Rust implementation
   ```

3. Build the server:
   ```bash
   npm run build
   ```

---

## 🔌 Usage & Integration

Netprobe is designed to integrate seamlessly with MCP-compliant AI clients, such as **Claude Desktop**.

### Configuring Claude Desktop

Add the Netprobe server to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "netprobe": {
      "command": "node",
      "args": [
        "/absolute/path/to/netprobe-mcp/build/index.js"
      ],
      "env": {
        "ALLOWED_SUBNETS": "192.168.1.0/24,10.0.0.0/8"
      }
    }
  }
}
```

### Example AI Interaction

Once connected, simply talk to your AI:

> **User:** *"Are there any exposed web servers on the 192.168.1.0/24 subnet?"*
> 
> **AI:** *(Seamlessly calls Netprobe MCP in the background)* "I have executed a network probe. I found an exposed web server running on port 80 and 443 at 192.168.1.50. Would you like me to analyze its vulnerability profile?"

---

## 🔒 Security & Validation

Because Netprobe executes raw system commands, security is the highest priority:
- **Strict Input Schemas:** All AI requests must conform to rigid JSON validation formats.
- **Subnet Allowlisting:** The server will categorically reject scan requests against IPs outside of the administrator-defined `ALLOWED_SUBNETS` environment variable.
- **Command Sanitization:** No direct shell execution. Commands are spawned as secure child processes using tightly parameterized arguments to prevent arbitrary code execution (ACE).

---

## 🗺️ Roadmap

- [x] Core MCP Server Architecture (stdio/SSE)
- [x] Masscan Adapter & JSON Parser Integration
- [ ] Nmap Integration (for deep service fingerprinting & script scanning)
- [ ] Wireshark / TShark Adapter for PCAP analysis
- [x] Integration with MITRE ATT&CK framework mapping
- [x] Active Remediation Orchestrator (Firewall/EDR hooks)

---

## ⚠️ Disclaimer

**Netprobe MCP is a powerful tool designed strictly for authorized network administration, educational purposes, and defensive cybersecurity operations.** Users must ensure they have explicit, documented permission to scan and probe target networks. The developers and contributors of this repository assume no liability and are not responsible for any misuse, damage, or unauthorized access caused by utilizing this software.

---

## 🤝 Contributing

We welcome contributions from the community! If you are a security researcher, systems engineer, or AI enthusiast, please feel free to submit a Pull Request, open an Issue, or suggest a new tool adapter.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="center">
  <i>"Transforming passive monitoring into active, intelligent system defense."</i>
</p>
