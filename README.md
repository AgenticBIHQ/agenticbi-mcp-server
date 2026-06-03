# AgenticBI MCP Server

| Field | Value |
|---------|--------|
| Product | AgenticBI MCP Server |
| Purpose | Connect Claude, Cursor, VS Code, ChatGPT, Codex CLI, and other MCP-enabled AI clients directly to business data |
| Endpoint | `https://app.agenticbi.com/api/2.0/mcp` |
| Protocol | MCP 2024-11-05 |
| Transport | Streamable HTTP (POST) with SSE |
| Authentication | OAuth 2.1 with PKCE |
| Tools Available | 33 |
| GitHub | `https://github.com/AgenticBIHQ/agenticbi-mcp-server` |

## Prerequisites

| Requirement |
|-------------|
| MCP-compatible AI client (Claude Desktop, Claude Code, Cursor, VS Code, ChatGPT, Codex CLI) |

## Client Setup

### Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "agenticbi": {
      "url": "https://app.agenticbi.com/api/2.0/mcp"
    }
  }
}
```

**File locations:**

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

On first use, your browser opens to AgenticBI login. Sign in or create an account to authorize.

**Full Guide:** https://app.agenticbi.com/docs/mcp-server.html

---

### Claude Code

```bash
claude mcp add agenticbi --transport http https://app.agenticbi.com/api/2.0/mcp
```

1. Run the command above in your terminal.
2. Exit and relaunch Claude Code.
3. Run `/mcp`, select **agenticbi**, and click **Enable**.
4. Click the authentication button — your browser opens to AgenticBI login.
5. Sign in or create an account and authorize access.
6. Verify by asking:

   > What AgenticBI tools are available?

#### Alternative: Manual Token Authentication

Generate a token in **AgenticBI → Settings → AI Settings → MCP Token**, then run:

```bash
claude mcp add agenticbi https://app.agenticbi.com/api/2.0/mcp \
  --transport http \
  --header "Authorization: Bearer YOUR_MCP_TOKEN"
```

**Full Guide:** https://app.agenticbi.com/docs/claude-code-setup.html

---

### Cursor

> Requires Cursor v0.45 or later.

1. Open **Settings → Cursor Settings**
2. Select **Tools & Integrations → New MCP Server**
3. Add the following to your `mcp.json`:

```json
{
  "mcpServers": {
    "agenticbi": {
      "url": "https://app.agenticbi.com/api/2.0/mcp"
    }
  }
}
```

4. Save the file. Your browser opens to AgenticBI login on first use.

#### Alternative: Manual Token Authentication

```json
{
  "mcpServers": {
    "agenticbi": {
      "url": "https://app.agenticbi.com/api/2.0/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_MCP_TOKEN"
      }
    }
  }
}
```

**Full Guide:** https://app.agenticbi.com/docs/cursor-mcp-setup.html

---

### VS Code

#### Option A — Command Palette (Recommended)

1. Open Command Palette:
   - macOS: `Cmd + Shift + P`
   - Windows: `Ctrl + Shift + P`
2. Search for **MCP: Add Server**
3. Select **HTTP** as the server type
4. Enter:

   ```
   https://app.agenticbi.com/api/2.0/mcp
   ```

5. Name it `agenticbi`
6. Save
7. Authorize via browser on first use

#### Option B — Configuration File

Add to `settings.json`:

```json
{
  "mcp": {
    "servers": {
      "agenticbi": {
        "type": "http",
        "url": "https://app.agenticbi.com/api/2.0/mcp"
      }
    }
  }
}
```

Or add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "agenticbi": {
      "type": "http",
      "url": "https://app.agenticbi.com/api/2.0/mcp"
    }
  }
}
```

#### Alternative: Manual Token Authentication

```json
{
  "mcp": {
    "servers": {
      "agenticbi": {
        "type": "http",
        "url": "https://app.agenticbi.com/api/2.0/mcp",
        "headers": {
          "Authorization": "Bearer YOUR_MCP_TOKEN"
        }
      }
    }
  }
}
```

**Full Guide:** https://app.agenticbi.com/docs/vscode-mcp-setup.html

---

### ChatGPT

1. Click **+** in the message input and select **Connectors**, or go to **Settings → Connected Apps**
2. Choose **Add Custom Connector**
3. Name it **AgenticBI**
4. Enter the server URL:

   ```
   https://app.agenticbi.com/api/2.0/mcp
   ```

5. Select **OAuth 2.0** authentication
6. Click **Save**
7. On first use, ChatGPT opens your browser for AgenticBI sign-in and authorization

#### Alternative: Manual Token Authentication

1. Generate a token in **AgenticBI → Settings → AI Settings → MCP Token**
2. Repeat steps 1–4 above
3. Select **Bearer Token** authentication
4. Paste your token
5. Click **Save**

**Full Guide:** https://app.agenticbi.com/docs/chatgpt-mcp-setup.html

---

### Codex CLI

Add to `~/.codex/config.json`:

```json
{
  "mcpServers": {
    "agenticbi": {
      "type": "http",
      "url": "https://app.agenticbi.com/api/2.0/mcp"
    }
  }
}
```

On first use, your browser opens to AgenticBI login for authorization.

#### Alternative: Manual Token Authentication

```json
{
  "mcpServers": {
    "agenticbi": {
      "type": "http",
      "url": "https://app.agenticbi.com/api/2.0/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_MCP_TOKEN"
      }
    }
  }
}
```

**Full Guide:** https://app.agenticbi.com/docs/codex-mcp-setup.html

## Authentication Endpoints

| Endpoint | URL |
|------------|-----|
| Authorization | `https://app.agenticbi.com/oauth/mcp/authorize` |
| Token | `https://app.agenticbi.com/oauth/mcp/token` |
| Registration | `https://app.agenticbi.com/oauth/mcp/register` |

## Tool Categories

| Category | Tool Count |
|-----------|------------|
| Ask & Query | 6 |
| Dashboards & Exports | 4 |
| Insights & Alerts | 3 |
| Documents | 2 |
| Create & Manage | 16 |
| Destructive | 2 |
| **Total** | **33** |

## Ask & Query Tools

| Tool | Description |
|--------|-------------|
| `ask` | Ask a data question in natural language |
| `get_data` | Retrieve full dataset or widget data |
| `search` | Search AgenticBI assets |
| `find_widget` | Find widgets by name |
| `get_details` | Retrieve asset details |
| `explain_lineage` | Trace how an answer was built |

## Dashboard & Export Tools

| Tool | Description |
|--------|-------------|
| `list_dashboards` | List dashboards |
| `get_embed_url` | Generate embed links |
| `export_pdf` | Export dashboards/widgets as PDF |
| `export_csv` | Export data as CSV |

## Insights & Alerts Tools

| Tool | Description |
|--------|-------------|
| `get_insights` | Generate AI-powered insights |
| `list_alerts` | List alerts |
| `cloud9ql_assist` | Generate, fix, explain, convert, validate or preview Cloud9QL |

## Document Tools

| Tool | Description |
|--------|-------------|
| `ask_document` | Ask questions against ingested documents |
| `list_documents` | List ingested documents |

## Create & Manage Tools

| Tool | Description |
|--------|-------------|
| `do` | Execute operations in natural language |
| `push_data` | Push rows into datasets |
| `run` | Execute saved queries/reports |
| `create_datasource` | Create a datasource connection |
| `create_query` | Create a query |
| `create_widget` | Create a visualization |
| `update_widget` | Update a visualization |
| `layout_dashboard` | Arrange dashboard widgets |
| `import_file` | Import CSV, JSON, XML, or Excel |
| `create_report` | Create scheduled reports |
| `update_report` | Update reports |
| `create_alert` | Create alerts |
| `test_alert` | Test alerts |
| `update_alert` | Update alerts |
| `ingest_document` | Ingest documents |
| `extract_document_data` | Extract structured data from documents |

## Destructive Tools

| Tool | Description |
|--------|-------------|
| `delete` | Delete AgenticBI assets |
| `delete_document` | Delete ingested documents |

## Health & Limits

| Setting | Value |
|----------|--------|
| Health Endpoint | `GET /api/2.0/mcp/health` |
| Session Header | `Mcp-Session-Id` |
| Idle Timeout | 30 minutes |
| Max Concurrent Sessions | 1,000 |
| Default Rows (`ask`) | 500 |
| Default Rows (`get_data`) | 10,000 |
| Max Rows | 200,000 |

  ## Example Prompts
  
  | Example |
  |----------|
  | What were our top 10 customers by revenue last quarter? |
  | Why did churn spike in March? |
  | Which marketing channels drove the most pipeline this month? |
  | Create a dashboard showing weekly signups by source. |
  | Alert me when MRR drops more than 5% week over week. |
  | Pull our call transcripts and summarize the top objections from lost deals. |
  | Upload this PDF and extract the key metrics into a dataset. |
  | Export the Q3 revenue dashboard as a PDF and email it to the team. |

## Important Links

| Resource | URL |
|-----------|-----|
| Website | `https://www.agenticbi.com` |
| MCP Docs | `https://app.agenticbi.com/docs/mcp-server.html` |
| Privacy Policy | `https://www.agenticbi.com/privacy` |
| Terms of Service | `https://www.agenticbi.com/terms` |

## Support

| Contact |
|----------|
| support@agenticbi.com |
