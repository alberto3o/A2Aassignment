# A2Aassignment
# Multi-Agent Customer Service System
**Using MCP, A2A Protocol, and LangGraph**

A production-ready multi-agent system demonstrating Agent-to-Agent (A2A) communication protocol with Model Context Protocol (MCP) for database operations. Built with official SDKs and LangGraph for agent orchestration.

## 🏗️ System Architecture
```
User Query
    ↓
[A2A Client] (JSON-RPC)
    ↓
[Router Agent] ← Analyzes & coordinates
    ↓
[Data Agent] ← MCP Server ← SQLite Database
    ↓
[Support Agent] ← Generates responses
```

**Components:**
- **MCP Server**: 5 tools for customer/ticket operations
- **Data Agent**: Executes database operations via MCP
- **Support Agent**: Provides customer assistance
- **Router Agent**: Orchestrates multi-agent workflows
- **SQLite Database**: 30 customers, 60+ tickets

## 📋 Prerequisites

- Python 3.10 or higher
- pip package manager
- Virtual environment support

## 🚀 Setup Instructions

### 1. Create Virtual Environment
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Set Up API Key

Create a `.env` file or set environment variable:
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

Or in Google Colab, use Secrets (🔑 icon) to add `ANTHROPIC_API_KEY`.

### 4. Initialize Database
```bash
python database_setup.py
```

This creates `support.db` with sample customer and ticket data.

### 5. Run the System
```bash
python main.py
```

The system will start three A2A servers on ports 10101-10103.

## 📦 Requirements

See `requirements.txt` for complete list:
```
anthropic>=0.40.0
mcp>=1.0.0
a2a-sdk>=0.1.0
langgraph>=0.2.0
langgraph-cli>=0.1.0
langchain-core>=0.3.0
langchain-anthropic>=0.2.0
starlette>=0.37.0
uvicorn>=0.30.0
httpx>=0.27.0
python-dotenv>=1.0.0
asyncclick>=8.1.0
rich>=13.0.0
```

## 🧪 Test Scenarios

The system handles 5 required test scenarios:

**1. Simple Query**
```
"Get customer information for ID 5"
→ Data Agent → MCP get_customer → Response
```

**2. Coordinated Query**
```
"I'm customer 5 and need help upgrading my account"
→ Router → Data Agent (fetch) → Support Agent (help)
```

**3. Complex Query**
```
"Show me all active customers who have open tickets"
→ Router → Multiple data operations → Synthesis
```

**4. Escalation**
```
"I've been charged twice, please refund immediately!"
→ Router (detects urgency) → Priority routing
```

**5. Multi-Intent**
```
"Update my email to new@email.com for customer 2 and show my ticket history"
→ Router → Parallel execution → Combined response
```

## 🔧 MCP Tools

Five database operations available:

1. **get_customer(customer_id)** - Retrieve customer details
2. **list_customers(status, limit)** - List customers with filters
3. **update_customer(customer_id, data)** - Update customer info
4. **create_ticket(customer_id, issue, priority)** - Create support ticket
5. **get_customer_history(customer_id)** - Get ticket history

## 🌐 A2A Protocol

**Agent Cards:** Each agent exposes capabilities via `.well-known/agent-card.json`

**Communication:** JSON-RPC 2.0 protocol with `message/send` method

**Endpoints:**
- Data Agent: `http://localhost:10101/a2a`
- Support Agent: `http://localhost:10102/a2a`
- Router Agent: `http://localhost:10103/a2a`

## 📊 Database Schema

**customers table:**
- id, name, email, phone, status, created_at, updated_at

**tickets table:**
- id, customer_id, issue, status, priority, created_at

## ✅ Verification

Run the test suite:
```bash
python test_scenarios.py
```

Expected output: **5/5 tests passing**

## 🎯 Key Features

- ✅ Official MCP SDK integration
- ✅ A2A protocol compliance (JSON-RPC)
- ✅ LangGraph state management
- ✅ Multi-agent coordination
- ✅ Agent Cards for capability discovery
- ✅ Async task execution
- ✅ Context sharing between agents

## 📚 Project Structure
```
.
├── README.md
├── requirements.txt
├── .env
├── database_setup.py      # Initialize SQLite database
├── mcp_server.py          # MCP tools implementation
├── agents.py              # LangGraph agents (Data, Support, Router)
├── a2a_server.py          # A2A server setup
├── main.py                # Start all servers
├── test_scenarios.py      # Run 5 test scenarios
└── support.db             # SQLite database (generated)
```

## 🐛 Troubleshooting

**Port already in use:**
```bash
# Change ports in a2a_server.py (lines with port numbers)
```

**API Key error:**
```bash
# Verify ANTHROPIC_API_KEY is set correctly
echo $ANTHROPIC_API_KEY
```

**Import errors:**
```bash
# Ensure virtual environment is activated
# Reinstall dependencies
pip install -r requirements.txt --force-reinstall
```

## 📝 Assignment Requirements Met

- ✅ MCP Server with 5 tools
- ✅ Three LangGraph agents with proper state
- ✅ A2A protocol implementation
- ✅ Agent Cards for discovery
- ✅ All 5 test scenarios passing
- ✅ Multi-agent coordination demonstrated

## 🔗 References

- [MCP Documentation](https://github.com/anthropics/mcp)
- [A2A Protocol Spec](https://github.com/a2aproject/a2a-samples)
- [LangGraph Docs](https://python.langgraph.com/)

---

**Built with:** Python 3.12 | MCP SDK | A2A SDK | LangGraph | Claude Sonnet 4
