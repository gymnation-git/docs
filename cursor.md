# MCP Servers Configuration (Windows)

## Prerequisites

1. **Install NVM**: Download from [nvm-windows](https://github.com/coreybutler/nvm-windows)
2. **Install latest LTS Node.js version**:
   ```bash
   nvm install lts
   ```

## How to Configure MCP Settings in Cursor

### Step 1: Access Cursor Settings
1. Open Cursor
2. Press `Ctrl + ,` (Windows/Linux) or `Cmd + ,` (Mac) to open Settings
3. Alternatively, go to **File** → **Preferences** → **Settings**

### Step 2: Navigate to MCP Settings
1. In the Settings search bar, type "mcp" or "model context protocol"
2. Look for **"Mcp: Servers"** setting
3. Click on **"Edit in settings.json"** link

### Step 3: Add MCP Configuration
1. This will open your `settings.json` file
2. Add the `mcpServers` configuration to your settings.json:

### Step 4: Save and Restart
1. Save the `settings.json` file (`Ctrl + S`)
2. Restart Cursor for the changes to take effect
3. The MCP servers should now be available in your Cursor AI chat

## MCP Config File

```json
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-brave-search"
      ],
      "env": {
        "BRAVE_API_KEY": ""
      }
    },
    "tavily-mcp": {
      "command": "tavily-mcp",
      "env": {
        "TAVILY_API_KEY": ""
      },
      "disabled": false,
      "autoApprove": []
    },
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    },
    "mcp-server-fetch": {
      "command": "uvx",
      "args": [
        "mcp-server-fetch"
      ]
    },
    "context7": {
      "command": "npx",
      "args": [
        "-y",
        "@upstash/context7-mcp"
      ]
    }
  }
}
```

## Server Setup Instructions

### Brave Search
**Repository**: [brave-search](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/brave-search)

1. Get API key from [Brave Search API Dashboard](https://api-dashboard.search.brave.com/register) using your personal email and credit card (free tier, but credit card required for API key)
2. Add the API key to your MCP config file as `BRAVE_API_KEY`

### Tavily MCP
**Repository**: [tavily-mcp](https://github.com/tavily-ai/tavily-mcp)

1. Get API key from [Tavily](https://app.tavily.com/) using your personal email (no credit card required)
2. Add it to your MCP config file as `TAVILY_API_KEY`

### Sequential Thinking
**Repository**: [sequential-thinking](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)

- Works out of the box, no additional setup required

### MCP Server Fetch
**Repository**: [fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch)

1. Install UV: Follow [UV installation guide](https://docs.astral.sh/uv/getting-started/installation/#__tabbed_1_2)
2. Restart Cursor. If it doesn't work, restart your PC

### Context7
**Repository**: [context7](https://github.com/upstash/context7)

1. Install globally:
   ```bash
   npm i --global @upstash/context7-mcp
   ```
2. Should work after installation

## Additional Resources

- [MCP Servers (Archived)](https://github.com/modelcontextprotocol/servers-archived)
- [MCP Servers (Current)](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file)
- [Cursor MCP Directory](https://cursor.directory/mcp)
- [Wisprflow](https://wisprflow.ai/)