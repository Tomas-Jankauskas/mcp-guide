# Model Context Protocol (MCP) Setup Guide

## What is MCP?

The Model Context Protocol (MCP) is an open protocol that standardizes how applications provide context and tools to LLMs. It functions as a plugin system for Cursor, extending the Agent's capabilities by connecting it to various data sources and tools through standardized interfaces.

# Part 1: Step-by-Step Setup Guide

Follow these steps to set up MCP in Cursor:

## Step 1: Install Cursor
If you haven't already, download and install Cursor from the [official website](https://cursor.com).

## Step 2: Choose Your MCP Server
Decide which MCP server you want to use. You have two main options:

### Option A: Use an Existing MCP Server (Recommended)
The easiest approach is to use pre-built servers from these sources:
- **[Official MCP Servers Repository](https://github.com/modelcontextprotocol/servers/)**: Contains reference implementations and community-built servers
- **[Smithery](https://smithery.ai/)**: A registry of MCP servers to find the right tools for your LLM agents
- **[Glama](https://glama.ai/)**: Platform for discovering and using MCP servers

For TypeScript-based servers from the official repository, you can use them with npx:
```bash
npx -y @modelcontextprotocol/server-memory
```

> **What is npx?** npx is a package runner tool that comes with npm (Node Package Manager). It allows you to execute Node.js packages without installing them globally. When you run the command above, npx automatically downloads the specified package temporarily, executes it, and then removes it from your system afterward. This makes it convenient for running MCP servers without permanently installing them on your machine.

### Option B: Create Your Own Custom MCP Server (Advanced)
If you can't find an existing server that meets your needs, you can create your own custom server. This is an advanced option that requires programming knowledge using the official SDKs:

- **[TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)** - For creating servers in JavaScript/TypeScript
- **[Python SDK](https://github.com/modelcontextprotocol/python-sdk)** - For creating servers in Python

This option is only recommended if you have specific requirements that aren't met by existing servers.

## Step 3: Create Configuration File
You can create or edit your MCP configuration directly through Cursor's interface:
1. Go to Settings
2. Navigate to the MCP settings page
3. Click "+ Add new global MCP server"

<!-- <img src="/images/add-mcp-cursor.png" alt="Adding MCP server in Cursor" width="600" /> -->

This will create or edit the `~/.cursor/mcp.json` file with your MCP server configuration.

Alternatively, you can manually create an MCP configuration file in one of two locations:
- **Project-specific**: Create `.cursor/mcp.json` in your project directory
- **Global**: Create `~/.cursor/mcp.json` in your home directory

## Step 4: Configure Your MCP Server
Add the server configuration to your MCP config file. For example:

```json
{
  "mcpServers": {
    "my-github-server": {
      "command": "npx",
      "args": ["-y", "@mcp/github-tools"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```

## Step 5: Restart Cursor
After creating or updating your MCP configuration, restart Cursor to apply the changes.

## Step 6: Verify Setup
Check that your MCP tools appear in Cursor:
1. Open Cursor
2. Go to Settings
3. Navigate to the MCP settings page
4. Verify your tools are listed under "Available Tools"

Your properly connected MCP tools should display with a green dot indicator. If the green status indicator is missing, you may need to debug your setup.

To debug MCP connection issues, open your terminal and run Cursor with the MCP debug flag:
```bash
cursor mcp
```

This will show the connection status and any error messages from your MCP servers:

<!-- <img src="/images/mcp-output.png" alt="MCP debug output in terminal" width="600" /> -->

## Common Setup Issues

If you encounter issues with your MCP setup, check these common problems:

### Path Resolution for npx
In some cases, Cursor might not be able to find the `npx` command in your system path, especially if you have multiple Node.js installations or are using version managers like nvm. If your MCP server fails to start with commands using npx, try specifying the full path to npx in your configuration:

```json
{
  "mcpServers": {
    "my-github-server": {
      "command": "/usr/local/bin/npx",
      "args": ["-y", "@mcp/github-tools"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```

You can find the full path to npx by running `which npx` in your terminal.

### Tools Not Appearing in Cursor
- Verify your configuration file is in the correct location
- Check for JSON syntax errors in your configuration file
- Ensure Cursor has been restarted after configuration changes
- Check that the command/path to your MCP server is correct

### Permission Issues
- Make sure your MCP server has the necessary permissions to execute
- For SSE servers, verify network connectivity and firewall settings
- Check that environment variables with API tokens are correctly set

### Server Errors
- Look for error messages in the Cursor logs
- If using a custom MCP server, verify it correctly implements the protocol
- For stdio servers, ensure they properly output data to stdout
- For SSE servers, confirm they're correctly serving the `/sse` endpoint

### Agent Not Using Tools
- Check if the tools are visible in the MCP settings page
- Ensure you're clearly instructing the agent to use the tool
- Verify that you've approved tool usage if not using Yolo mode

# Part 2: Additional Information

This section contains conceptual information and references for those who want to learn more about MCP.

## Use Cases

MCP allows you to connect Cursor to external systems and data sources, integrating with your existing tools and infrastructure. MCP servers can be written in any language that can print to `stdout` or serve an HTTP endpoint.

### Example Integrations
- **Databases**: Allow Cursor to query your databases directly
- **Notion**: Read data from Notion to guide implementation
- **GitHub**: Create PRs, branches, find code, etc.
- **Memory**: Enable Cursor to remember and recall information
- **Stripe**: Create customers, manage subscriptions, etc.

## Architecture

MCP servers are lightweight programs that expose specific capabilities through the standardized protocol. Cursor supports two transport types:

### 💻 stdio Transport
- Runs on your **local machine**
- Managed automatically by Cursor
- Communicates directly via `stdout`
- Only accessible by you locally
- **Input:** Valid shell command that is run by Cursor automatically

### 🌐 SSE Transport
- Can run **locally or remotely**
- Managed and run by you
- Communicates **over the network**
- Can be **shared** across machines
- **Input:** URL to the `/sse` endpoint of an MCP server external to Cursor

## Advanced Configuration Options

### Setting Up an SSE Server

If you prefer to use the SSE transport method (which can run locally or remotely), you can configure it as follows:

```json
{
  "mcpServers": {
    "my-sse-server": {
      "url": "http://localhost:8000/sse",
      "env": {
        "API_KEY": "your-api-key"
      }
    }
  }
}
```

This approach is particularly useful for:
- Teams that want to share MCP tools across multiple developers
- Scenarios where the MCP server needs to run continuously
- Integration with existing services already running on HTTP

## Using MCP Tools with Agent

The Composer Agent automatically uses any MCP tools listed under `Available Tools` on the MCP settings page when relevant. You can prompt tool usage by telling the agent to use the tool by name or description.

### Tool Approval

By default, when Agent wants to use an MCP tool, it will ask for your approval. You can expand the message to see what arguments the Agent is calling the tool with.

### Yolo Mode

You can enable Yolo mode to allow Agent to automatically run MCP tools without requiring approval.

## Limitations

- **Tool Quantity**: Cursor will only send the first 40 tools to the Agent.
- **Remote Development**: MCP servers may not work properly when accessing Cursor over SSH or other remote development environments.
- **Resources**: MCP servers offer tools and resources. Currently, only tools are supported in Cursor.

## Creating Your Own MCP Server

If you want to create your own MCP server, here are the details for using the official SDKs:

### TypeScript SDK
The [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) provides a complete framework for building MCP servers in TypeScript/JavaScript.

Installation:
```bash
npm install @modelcontextprotocol/sdk
```

Basic server example:
```typescript
import { McpServer, Tool } from '@modelcontextprotocol/sdk';

const server = new McpServer();

server.addTool({
  name: 'hello_world',
  description: 'Says hello to a person',
  parameters: {
    type: 'object',
    properties: {
      name: { type: 'string', description: 'The name to say hello to' }
    },
    required: ['name']
  },
  handler: async ({ name }) => {
    return `Hello, ${name}!`;
  }
});

server.start();
```

### Python SDK
The [Python SDK](https://github.com/modelcontextprotocol/python-sdk) provides a framework for building MCP servers in Python.

Installation:
```bash
pip install mcp-python-sdk
```

Basic server example:
```python
from mcp import McpServer, Tool

server = McpServer()

@server.tool
def hello_world(name: str) -> str:
    """Says hello to a person
    
    Args:
        name: The name to say hello to
    """
    return f"Hello, {name}!"

server.start()
```

### Server Frameworks
Several high-level frameworks make it even easier to build MCP servers:

- **FastMCP** (TypeScript) - Simplified TypeScript server creation
- **EasyMCP** (TypeScript) - User-friendly TypeScript framework
- **MCP-Framework** - Build MCP servers with elegance in TypeScript
- **Quarkus MCP Server SDK** (Java) - For Java developers

---

For more detailed information, visit the [official MCP documentation](https://docs.cursor.com/context/model-context-protocol). 