# Dolphin MCP Setup Guide

## ✅ What's Been Installed

- **Dolphin MCP** (v0.1.3) - Python-based MCP client
- **LM Studio SDK** - For local model support
- **MCP Filesystem Server** - For file operations
- **Node.js & npm** - Required for MCP servers

## 📋 Configuration Files Created

1. **`.env`** - API keys and environment variables
2. **`mcp_config.json`** - MCP server configurations

## 🔧 Next Steps to Complete Setup

### Option 1: Use OpenAI (Recommended for Testing)

1. Edit `.env` file and replace `your_openai_api_key_here` with your actual OpenAI API key:
   ```bash
   OPENAI_API_KEY=sk-proj-...your-actual-key...
   OPENAI_MODEL=gpt-4o
   ```

2. Get your API key from: https://platform.openai.com/api-keys

### Option 2: Use Anthropic (Claude)

1. Edit `.env` file and add your Anthropic API key:
   ```bash
   ANTHROPIC_API_KEY=your_anthropic_api_key_here
   ```

2. Get your API key from: https://console.anthropic.com/

### Option 3: Use Local Models (Advanced)

1. Install Ollama: https://ollama.com/download
2. Pull a model: `ollama pull llama2`
3. Use with: `dolphin-mcp-cli --model ollama/llama2 "your question"`

## 🧪 Testing the Setup

Once you've added your API key, test with:

```bash
# Basic test
dolphin-mcp-cli "List the files in the current directory"

# Test with specific model
dolphin-mcp-cli --model gpt-4o "What files are in this project?"

# Interactive mode
dolphin-mcp-cli -i
```

## 📁 Current MCP Server Configuration

The filesystem server is configured to access:
- Directory: `/home/user/web-evolver-pro-1761548143159`

You can modify `mcp_config.json` to add more servers or change directories.

## 🔍 Available Commands

```bash
# Show help
dolphin-mcp-cli --help

# Specify custom config
dolphin-mcp-cli --config custom_config.json "your question"

# Quiet mode (less output)
dolphin-mcp-cli --quiet "your question"

# Log interactions
dolphin-mcp-cli --log-messages interactions.jsonl "your question"
```

## 📚 Adding More MCP Servers

To add more servers, edit `mcp_config.json`:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "/opt/node22/bin/mcp-server-filesystem",
      "args": ["/home/user/web-evolver-pro-1761548143159"],
      "env": {}
    },
    "another-server": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-fetch"],
      "env": {}
    }
  }
}
```

## 🐛 Troubleshooting

### "No suitable model found in config"
- Make sure you've set `OPENAI_API_KEY` in `.env`
- Or specify a model with `--model` flag

### "ModuleNotFoundError"
- All required Python packages are installed
- Try: `pip3 install dolphin-mcp --upgrade`

### MCP Server Issues
- Verify Node.js is installed: `node --version`
- Check server path: `/opt/node22/bin/mcp-server-filesystem`

## 📖 Resources

- Dolphin MCP GitHub: https://github.com/QuixiAI/dolphin-mcp
- MCP Servers: https://github.com/modelcontextprotocol/servers
- MCP Documentation: https://modelcontextprotocol.io/

## ✨ Example Usage

After setting up your API key:

```bash
# Ask about project files
dolphin-mcp-cli "What HTML files are in this project?"

# Check README content
dolphin-mcp-cli "What does the README file say?"

# Interactive exploration
dolphin-mcp-cli -i
> What files are here?
> Show me the contents of index.html
> exit
```
