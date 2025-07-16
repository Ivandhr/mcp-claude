# MCP Claude

Local MCP server integrated with Claude Desktop MCP client.

## What is MCP?

The Model Context Protocol (MCP) is an open standard that enables AI assistants to securely access external data and tools. It allows Claude Desktop to connect to various services and resources through standardized servers.

## Setup Instructions

### 1. Install Claude Desktop

Download and install Claude Desktop from the official Anthropic website.

### 2. Configure MCP Server

Claude Desktop uses a configuration file to manage MCP servers. The configuration file location depends on your operating system:

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

### 3. Configuration File

Create or edit the `claude_desktop_config.json` file with the following configuration:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_GITHUB_PAT_HERE"
      }
    }
  }
}
```

### 4. Create GitHub Personal Access Token

1. Go to [GitHub Settings > Developer settings > Personal access tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Set an appropriate expiration date
4. Select the following scopes:
   - `repo` (Full control of private repositories)
   - `user` (Read user profile data)
   - `workflow` (Update GitHub Action workflows)
5. Click "Generate token"
6. Copy the token and replace `YOUR_GITHUB_PAT_HERE` in the configuration

### 5. Restart Claude Desktop

After saving the configuration file, restart Claude Desktop to load the new MCP server.

## Features

Once configured, Claude Desktop will have access to GitHub functionality including:

- Repository management
- File operations
- Issue tracking
- Pull request management
- Code search
- User and organization management

## Troubleshooting

### Common Issues

1. **Configuration file not found**: Ensure the file is in the correct location for your OS
2. **Invalid token**: Verify your GitHub PAT is valid and has the correct permissions
3. **Server not loading**: Check that Node.js is installed and npx is available
4. **Permission denied**: Ensure the PAT has the necessary scopes for the operations you want to perform

### Verification

To verify the setup is working:

1. Open Claude Desktop
2. Start a new conversation
3. Try asking Claude to help with GitHub operations
4. You should see GitHub-related tools available in Claude's responses

## Security Notes

- Keep your GitHub Personal Access Token secure
- Never commit the token to version control
- Consider using environment variables for sensitive data
- Regularly rotate your tokens for better security

## Additional MCP Servers

This configuration can be extended to include other MCP servers. Popular options include:

- Filesystem server for local file access
- Database servers for data management
- API servers for external service integration

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is open source and available under the MIT License.
