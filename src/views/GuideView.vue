<script setup lang="ts">
// No imports needed for direct HTML approach
</script>

<template>
  <div class="guide-container">
    <div class="header-wrapper">
      <header class="header">
        <div class="header-content">
          <h1>MCP Setup Guide</h1>
          <p>A comprehensive guide to set up Model Context Protocol in Cursor</p>
        </div>
      </header>
    </div>
    <main class="content-wrapper">
      <div class="content">
        <!-- Direct HTML content -->
        <div class="guide-content">
          <h1>Model Context Protocol (MCP) Setup Guide</h1>
          
          <h2>What is MCP?</h2>
          <p>The Model Context Protocol (MCP) is an open protocol that standardizes how applications provide context and tools to LLMs. It functions as a plugin system for Cursor, extending the Agent's capabilities by connecting it to various data sources and tools through standardized interfaces.</p>
          
          <h1>Part 1: Step-by-Step Setup Guide</h1>
          <p>Follow these steps to set up MCP in Cursor:</p>
          
          <h2>Step 1: Install Cursor</h2>
          <p>If you haven't already, download and install Cursor from the <a href="https://cursor.com" target="_blank">official website</a>.</p>
          
          <h2>Step 2: Choose Your MCP Server</h2>
          <p>Decide which MCP server you want to use. You have two main options:</p>
          
          <h3>Option A: Use an Existing MCP Server (Recommended)</h3>
          <p>The easiest approach is to use pre-built servers from these sources:</p>
          <ul>
            <li><strong><a href="https://github.com/modelcontextprotocol/servers/" target="_blank">Official MCP Servers Repository</a></strong>: Contains reference implementations and community-built servers</li>
            <li><strong><a href="https://smithery.ai/" target="_blank">Smithery</a></strong>: A registry of MCP servers to find the right tools for your LLM agents</li>
            <li><strong><a href="https://glama.ai/" target="_blank">Glama</a></strong>: Platform for discovering and using MCP servers</li>
          </ul>
          
          <p>For TypeScript-based servers from the official repository, you can use them with npx:</p>
          <pre><code>npx -y @modelcontextprotocol/server-memory</code></pre>
          
          <blockquote>
            <p><strong>What is npx?</strong> npx is a package runner tool that comes with npm (Node Package Manager). It allows you to execute Node.js packages without installing them globally. When you run the command above, npx automatically downloads the specified package temporarily, executes it, and then removes it from your system afterward. This makes it convenient for running MCP servers without permanently installing them on your machine.</p>
          </blockquote>
          
          <h3>Option B: Create Your Own Custom MCP Server (Advanced)</h3>
          <p>If you can't find an existing server that meets your needs, you can create your own custom server. This is an advanced option that requires programming knowledge using the official SDKs:</p>
          <ul>
            <li><strong><a href="https://github.com/modelcontextprotocol/typescript-sdk" target="_blank">TypeScript SDK</a></strong> - For creating servers in JavaScript/TypeScript</li>
            <li><strong><a href="https://github.com/modelcontextprotocol/python-sdk" target="_blank">Python SDK</a></strong> - For creating servers in Python</li>
          </ul>
          <p>This option is only recommended if you have specific requirements that aren't met by existing servers.</p>
          
          <h2>Step 3: Create Configuration File</h2>
          <p>You can create or edit your MCP configuration directly through Cursor's interface:</p>
          <ol>
            <li>Go to Settings</li>
            <li>Navigate to the MCP settings page</li>
            <li>Click "+ Add new global MCP server"</li>
          </ol>
          
          <div class="image-container">
            <img src="https://github.com/Tomas-Jankauskas/mcp-guide/raw/main/images/add-mcp-cursor.png" alt="Adding MCP server in Cursor" width="600" />
          </div>
          
          <p>This will create or edit the <code>~/.cursor/mcp.json</code> file with your MCP server configuration.</p>
          
          <p>Alternatively, you can manually create an MCP configuration file in one of two locations:</p>
          <ul>
            <li><strong>Project-specific</strong>: Create <code>.cursor/mcp.json</code> in your project directory</li>
            <li><strong>Global</strong>: Create <code>~/.cursor/mcp.json</code> in your home directory</li>
          </ul>
          
          <h2>Step 4: Configure Your MCP Server</h2>
          <p>Add the server configuration to your MCP config file. For example:</p>
          
          <pre><code>{
  "mcpServers": {
    "my-github-server": {
      "command": "npx",
      "args": ["-y", "@mcp/github-tools"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}</code></pre>
          
          <h2>Step 5: Restart Cursor</h2>
          <p>After creating or updating your MCP configuration, restart Cursor to apply the changes.</p>
          
          <h2>Step 6: Verify Setup</h2>
          <p>Check that your MCP tools appear in Cursor:</p>
          <ol>
            <li>Open Cursor</li>
            <li>Go to Settings</li>
            <li>Navigate to the MCP settings page</li>
            <li>Verify your tools are listed under "Available Tools"</li>
          </ol>
          
          <p>Your properly connected MCP tools should display with a green dot indicator. If the green status indicator is missing, you may need to debug your setup.</p>
          
          <p>To debug MCP connection issues, open your terminal and run Cursor with the MCP debug flag:</p>
          <pre><code>cursor mcp</code></pre>
          
          <p>This will show the connection status and any error messages from your MCP servers:</p>
          
          <div class="image-container">
            <img src="https://github.com/Tomas-Jankauskas/mcp-guide/raw/main/images/mcp-output.png" alt="MCP debug output in terminal" width="600" />
          </div>
          
          <h2>Common Setup Issues</h2>
          <p>If you encounter issues with your MCP setup, check these common problems:</p>
          
          <h3>Path Resolution for npx</h3>
          <p>In some cases, Cursor might not be able to find the <code>npx</code> command in your system path, especially if you have multiple Node.js installations or are using version managers like nvm. If your MCP server fails to start with commands using npx, try specifying the full path to npx in your configuration:</p>
          
          <pre><code>{
  "mcpServers": {
    "my-github-server": {
      "command": "/usr/local/bin/npx",
      "args": ["-y", "@mcp/github-tools"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}</code></pre>
          
          <p>You can find the full path to npx by running <code>which npx</code> in your terminal.</p>
          
          <h3>Tools Not Appearing in Cursor</h3>
          <ul>
            <li>Verify your configuration file is in the correct location</li>
            <li>Check for JSON syntax errors in your configuration file</li>
            <li>Ensure Cursor has been restarted after configuration changes</li>
            <li>Check that the command/path to your MCP server is correct</li>
          </ul>
          
          <h3>Permission Issues</h3>
          <ul>
            <li>Make sure your MCP server has the necessary permissions to execute</li>
            <li>For SSE servers, verify network connectivity and firewall settings</li>
            <li>Check that environment variables with API tokens are correctly set</li>
          </ul>
          
          <h3>Server Errors</h3>
          <ul>
            <li>Look for error messages in the Cursor logs</li>
            <li>If using a custom MCP server, verify it correctly implements the protocol</li>
            <li>For stdio servers, ensure they properly output data to stdout</li>
            <li>For SSE servers, confirm they're correctly serving the <code>/sse</code> endpoint</li>
          </ul>
        </div>
      </div>
    </main>
    <footer>
      <div class="footer-content">
        <p>Model Context Protocol (MCP) Documentation - Designed with Vue.js</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.guide-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100vw;
}

.header-wrapper {
  background-color: #0366d6;
  width: 100%;
  padding: 3rem 0;
  color: white;
}

.header {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.header-content {
  width: 100%;
  padding: 0 2rem;
}

.header h1 {
  font-size: 3rem;
  margin: 0;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.header p {
  margin-top: 0.8rem;
  font-size: 1.4rem;
  opacity: 0.85;
  max-width: 700px;
  line-height: 1.5;
}

.content-wrapper {
  flex: 1;
  background-color: #f6f8fa;
  padding: 3rem 0;
  width: 100%;
}

.content {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.07);
  overflow: hidden;
  padding: 2rem;
}

.guide-content {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  line-height: 1.7;
  color: #24292e;
}

.guide-content h1 {
  padding-bottom: 0.4em;
  font-size: 2.2em;
  border-bottom: 1px solid #eaecef;
  margin-top: 32px;
  margin-bottom: 20px;
  font-weight: 600;
  line-height: 1.25;
  letter-spacing: -0.5px;
}

.guide-content h1:first-child {
  margin-top: 0;
}

.guide-content h2 {
  padding-bottom: 0.3em;
  font-size: 1.65em;
  border-bottom: 1px solid #eaecef;
  margin-top: 32px;
  margin-bottom: 20px;
  font-weight: 600;
  line-height: 1.25;
  letter-spacing: -0.3px;
}

.guide-content h3 {
  font-size: 1.35em;
  margin-top: 28px;
  margin-bottom: 18px;
  font-weight: 600;
  line-height: 1.25;
}

.guide-content p {
  margin-top: 0;
  margin-bottom: 18px;
  font-size: 1.05em;
}

.guide-content a {
  color: #0366d6;
  text-decoration: none;
  transition: color 0.2s ease;
}

.guide-content a:hover {
  text-decoration: underline;
  color: #0078ff;
}

.guide-content ul, 
.guide-content ol {
  padding-left: 2em;
  margin-top: 0;
  margin-bottom: 20px;
}

.guide-content li {
  margin-top: 0.35em;
  margin-bottom: 0.35em;
}

.guide-content li p {
  margin-top: 10px;
  margin-bottom: 10px;
}

.guide-content pre {
  padding: 18px;
  overflow: auto;
  font-size: 90%;
  line-height: 1.5;
  background-color: #f6f8fa;
  border-radius: 6px;
  margin-top: 0;
  margin-bottom: 20px;
  font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, monospace;
}

.guide-content code {
  padding: 0.2em 0.4em;
  margin: 0;
  font-size: 90%;
  background-color: rgba(27, 31, 35, 0.05);
  border-radius: 4px;
  font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, monospace;
}

.guide-content pre code {
  padding: 0;
  margin: 0;
  background-color: transparent;
  border: 0;
  display: inline;
  overflow: visible;
  line-height: inherit;
  word-wrap: normal;
}

.guide-content blockquote {
  padding: 0 1.2em;
  color: #6a737d;
  border-left: 0.3em solid #dfe2e5;
  margin: 0 0 20px 0;
}

.image-container {
  text-align: center;
  margin: 30px 0;
}

.image-container img {
  max-width: 100%;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

footer {
  background-color: #24292e;
  padding: 2rem 0;
  text-align: center;
  color: rgba(255, 255, 255, 0.7);
  font-size: 1rem;
  width: 100%;
}

.footer-content {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (max-width: 768px) {
  .header-wrapper {
    padding: 2rem 0;
  }
  
  .header-content {
    padding: 0 1.5rem;
  }
  
  .header h1 {
    font-size: 2.5rem;
  }
  
  .header p {
    font-size: 1.2rem;
  }
  
  .content-wrapper {
    padding: 1.5rem 0;
  }
  
  .content {
    border-radius: 0;
    box-shadow: none;
    padding: 1.5rem;
  }
  
  .footer-content {
    padding: 0 1.5rem;
  }
  
  .image-container img {
    width: 100%;
  }
}
</style> 