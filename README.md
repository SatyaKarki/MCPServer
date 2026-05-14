# MCP Server and Client Development in .NET

A comprehensive learning project demonstrating the **Model Context Protocol (MCP)** implementation with .NET 10. This solution includes an MCP Server with real-world tools, an MCP Client library, a Console Host application, and a **Blazor Web UI** for interactive tool exploration.

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Running the Demo](#running-the-demo)
- [Blazor Web UI](#blazor-web-ui)
- [Available Tools](#available-tools)
- [Testing](#testing)
- [Integration with AI Assistants](#integration-with-ai-assistants)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

The **Model Context Protocol (MCP)** is an open protocol that standardizes how AI applications and tools communicate. This project demonstrates:

- Building an MCP Server that exposes tools to AI assistants
- Creating an MCP Client to connect to servers
- Building a modern Blazor Web UI for interactive tool exploration
- Real-world use cases including weather, calculator, todo management, and text utilities

## 🏗️ Architecture

```
┌─────────────────┐     stdio     ┌─────────────────┐
│   MCP Client    │◄────────────►│   MCP Server    │
│    (Host)       │   transport   │    (Tools)      │
└─────────────────┘               └─────────────────┘
        │                                  │
        │                                  ▼
        │                         ┌───────────────────┐
        │                         │  Weather Tool     │
        │                         │  Calculator Tool  │
        │                         │  Todo Tool        │
        │                         │  Text Utility     │
        │                         └───────────────────┘
        ▼
┌─────────────────┐
│  AI Assistant   │
│  (Claude, etc)  │
└─────────────────┘
```

## 📁 Project Structure

```
MyFirstMCPDemo/
├── src/
│   ├── MCP.Shared/           # Common types and models
│   │   └── Models/
│   │       ├── WeatherInfo.cs
│   │       ├── TodoItem.cs
│   │       └── CalculationResult.cs
│   │
│   ├── MCP.Server/           # MCP Server with tools
│   │   ├── Tools/
│   │   │   ├── WeatherTool.cs
│   │   │   ├── CalculatorTool.cs
│   │   │   ├── TodoTool.cs
│   │   │   ├── TextUtilityTool.cs
│   │   │   ├── ProductTool.cs
│   │   │   └── ProductCatalogTool.cs
│   │   └── Program.cs
│   │
│   ├── MCP.Client/           # MCP Client library
│   │   └── Program.cs
│   │
│   ├── MCP.Host/             # Console demo application
│   │   └── Program.cs
│   │
│   ├── MCP.BlazorUI/         # Blazor Web UI for MCP
│   │   ├── Components/
│   │   │   └── Pages/
│   │   │       └── Home.razor
│   │   ├── Services/
│   │   │   └── McpClientService.cs
│   │   └── Program.cs
│   │
│   └── MCP.ProductApi/       # Sample API for product tools
│       └── Program.cs
│
├── tests/
│   └── MCP.Tests/            # Unit tests
│       └── UnitTest1.cs
│
├── MyFirstMCPDemo.sln
└── README.md
```

## ✅ Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/download) or later
- A code editor (VS Code, Visual Studio, Rider, etc.)

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/rijwanansari/MyFirstMCPDemo.git
cd MyFirstMCPDemo
```

### 2. Build the Solution

```bash
dotnet build
```

### 3. Run Tests

```bash
dotnet test
```

## 🎮 Running the Demo

### Run the Host Application

The host application demonstrates connecting to the MCP Server and invoking tools:

```bash
dotnet run --project src/MCP.Host
```

This will:
1. Start the MCP Server
2. Connect to it via stdio transport
3. List all available tools
4. Run interactive demos for each tool

### Run the Server Standalone

To run the MCP Server in standalone mode (for integration with AI assistants):

```bash
dotnet run --project src/MCP.Server
```

## 🌐 Blazor Web UI

The solution includes a modern **Blazor Web UI** that provides an interactive, user-friendly interface for connecting to the MCP Server and invoking tools.

### Features

✨ **Connection Management**
- Easy server connection with auto-detected server path
- Real-time connection status indicator
- One-click connect/disconnect

🔧 **Tool Explorer**
- Browse all 35+ available tools
- View tool descriptions
- Interactive tool selection

💬 **Conversational Interface**
- JSON-based parameter input
- Real-time tool invocation
- Formatted response display
- Complete conversation history

### Screenshots

#### Initial View (Disconnected)
![Blazor UI Disconnected](https://github.com/user-attachments/assets/96587e7b-c03c-4f38-a358-741f5d829827)

#### Connected with Tools Listed
![Blazor UI Connected](https://github.com/user-attachments/assets/73219578-134a-40a0-ba72-d06cb1af02cc)

#### Tool Invocation with Results
![Blazor UI Tool Invocation](https://github.com/user-attachments/assets/fd27382b-4341-438e-9361-d39a6d620011)

#### Multiple Tool Calls in Conversation
![Blazor UI Multiple Tools](https://github.com/user-attachments/assets/74557959-08a9-4310-ae80-b365f9af68c8)

### Running the Blazor UI

1. **Build the solution** (if not already done):
   ```bash
   dotnet build
   ```

2. **Run the Blazor UI**:
   ```bash
   dotnet run --project src/MCP.BlazorUI
   ```

3. **Access the UI**:
   - Open your browser to `http://localhost:5233`
   - The server path should be auto-detected
   - Click "Connect" to connect to the MCP Server
   - Browse available tools and start invoking them!

### Using the Blazor UI

1. **Connect to Server**: Enter the path to MCP.Server.dll (or use the auto-detected path) and click "Connect"
2. **Select a Tool**: Click on any tool from the "Available Tools" panel
3. **Enter Parameters**: Use JSON format to provide tool parameters, e.g., `{"location": "Tokyo", "unit": "celsius"}`
4. **Invoke Tool**: Click "Invoke Tool" to execute the tool and see results
5. **View History**: All tool calls and responses are logged in the "Conversation History" panel

## 🛠️ Available Tools

### 🌤️ Weather Tool

Get simulated weather information for any location.

| Tool | Description | Parameters |
|------|-------------|------------|
| `GetWeather` | Get current weather | `location` (string), `unit` (celsius/fahrenheit) |
| `GetForecast` | Get multi-day forecast | `location` (string), `days` (1-7) |

### 🔢 Calculator Tool

Perform mathematical calculations.

| Tool | Description | Parameters |
|------|-------------|------------|
| `Add` | Add two numbers | `a`, `b` |
| `Subtract` | Subtract numbers | `a`, `b` |
| `Multiply` | Multiply numbers | `a`, `b` |
| `Divide` | Divide numbers | `a`, `b` |
| `Power` | Raise to power | `baseNumber`, `exponent` |
| `SquareRoot` | Calculate square root | `number` |
| `Percentage` | Calculate percentage | `part`, `whole` |
| `Modulo` | Calculate remainder | `a`, `b` |

### 📝 Todo Tool

Manage a task list.

| Tool | Description | Parameters |
|------|-------------|------------|
| `CreateTodo` | Create new task | `title`, `description?`, `priority?` |
| `GetTodos` | List tasks | `filter?`, `priority?` |
| `CompleteTodo` | Mark task done | `id` |
| `UpdateTodo` | Modify task | `id`, `title?`, `description?`, `priority?` |
| `DeleteTodo` | Remove task | `id` |
| `GetTodoStats` | Get statistics | - |
| `ClearCompleted` | Remove done tasks | - |

### 📄 Text Utility Tool

Text manipulation and analysis.

| Tool | Description | Parameters |
|------|-------------|------------|
| `AnalyzeText` | Count words, chars, lines | `text` |
| `ConvertCase` | Change text case | `text`, `caseType` |
| `ReverseText` | Reverse characters | `text` |
| `RemoveDuplicateLines` | Deduplicate lines | `text`, `caseSensitive?` |
| `ExtractEmails` | Find email addresses | `text` |
| `ExtractUrls` | Find URLs | `text` |
| `Slugify` | Create URL-friendly string | `text` |
| `Truncate` | Shorten text | `text`, `maxLength`, `addEllipsis?` |

## 🧪 Testing

Run the test suite:

```bash
# Run all tests
dotnet test

# Run tests with detailed output
dotnet test --logger "console;verbosity=detailed"

# Run specific test class
dotnet test --filter "FullyQualifiedName~CalculatorToolTests"
```

## 🤖 Integration with AI Assistants

### Claude Desktop Configuration

Add this to your Claude Desktop configuration file (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "mcp-demo": {
      "command": "dotnet",
      "args": ["run", "--project", "/path/to/MyFirstMCPDemo/src/MCP.Server"]
    }
  }
}
```

### VS Code Extension Configuration

For VS Code with Copilot:

```json
{
  "github.copilot.chat.mcpServers": {
    "mcp-demo": {
      "command": "dotnet",
      "args": ["run", "--project", "/path/to/MyFirstMCPDemo/src/MCP.Server"]
    }
  }
}
```

## 📚 Learning Resources

- [MCP Specification](https://modelcontextprotocol.io/specification)
- [MCP .NET SDK](https://github.com/modelcontextprotocol/csharp-sdk)
- [MCP Documentation](https://modelcontextprotocol.io/docs)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Rijwan Ansari**

---

⭐ If you found this project helpful, please give it a star!
