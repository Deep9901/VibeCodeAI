# VibeCodeAI – AI-Powered Web IDE

VibeCodeAI is a full-stack, web-based integrated development environment built with Next.js and Monaco Editor. It features real-time code execution using WebContainers, AI-powered code suggestions via locally running Ollama models, multi-stack templates, an integrated terminal, and a developer-focused UI for seamless coding directly in the browser.

## Key Features

- **OAuth Authentication** – Secure login with Google and GitHub via NextAuth
- **Modern Developer Interface** – Built with TailwindCSS and ShadCN UI components
- **Theme Support** – Toggle between dark and light modes
- **Project Templates** – Start quickly with React, Next.js, Express, Hono, Vue, or Angular templates
- **File System Management** – Create, rename, delete, and organize files and folders
- **Advanced Code Editor** – Monaco Editor with syntax highlighting, formatting, and custom keybindings
- **AI-Powered Autocomplete** – Code suggestions powered by local Ollama models (trigger with Ctrl+Space or double Enter)
- **In-Browser Code Execution** – Run frontend and backend applications instantly using WebContainers
- **Integrated Terminal** – Full terminal experience with xterm.js
- **AI Chat Assistant** – Share files with AI for explanations, refactoring suggestions, and debugging help

## Tech Stack

| Layer         | Technology                                   |
|---------------|----------------------------------------------|
| Framework     | Next.js 15 (App Router)                      |
| Styling       | TailwindCSS, ShadCN UI                       |
| Language      | TypeScript                                   |
| Auth          | NextAuth (Google + GitHub OAuth)             |
| Editor        | Monaco Editor                                |
| AI Suggestion | Ollama (LLMs running locally via Docker)     |
| Runtime       | WebContainers                                |
| Terminal      | xterm.js                                     |
| Database      | MongoDB (via DATABASE_URL)                   |

## Getting Started

### Prerequisites

- Node.js 18+ 
- MongoDB instance
- Docker (for Ollama)
- Ollama installed locally
- Google/GitHub OAuth credentials

### Installation

1. Clone the repository:
```bash
git clone https://github.com/your-username/vibecodeai.git
cd vibecodeai
```

2. Install dependencies:
```bash
npm install
```

3. Configure environment variables:
Create a `.env.local` file with the following variables:
```
AUTH_SECRET=your_generated_auth_secret
AUTH_GOOGLE_ID=your_google_client_id
AUTH_GOOGLE_SECRET=your_google_client_secret
AUTH_GITHUB_ID=your_github_client_id
AUTH_GITHUB_SECRET=your_github_client_secret
DATABASE_URL=your_mongodb_connection_string
NEXTAUTH_URL=http://localhost:3000
```

4. Start the Ollama model:
```bash
ollama run codellama
```

5. Run the development server:
```bash
npm run dev
```

The application will be available at `http://localhost:3000`.

## Project Architecture

```
vibecodeai/
├── app/                    # Next.js App Router pages and API routes
├── components/             # Reusable UI components
├── editor/                # Core editor components (Monaco, File Explorer, Terminal)
├── lib/                   # Utility functions and shared logic
├── utils/                 # AI integration and WebContainer utilities
├── public/                # Static assets
└── types/                 # TypeScript type definitions
```

## Development Workflow

### Setting Up AI Features

1. Install Ollama from [ollama.com](https://ollama.com)
2. Pull a code-capable model:
```bash
ollama pull codellama
```
3. Ensure Ollama is running before starting the development server

### Building for Production

```bash
npm run build
npm start
```

## Key Technical Implementation Details

### WebContainers Integration
- Utilizes StackBlitz's WebContainers API for secure, in-browser Node.js environments
- Supports npm package installation and script execution
- Provides isolated filesystem for each project session

### Monaco Editor Customization
- Custom language support and syntax highlighting
- Integrated formatting with Prettier
- Custom keybindings and command palette
- File-based persistence and state management

### AI Integration Architecture
- Local Ollama instance communicates via REST API
- Context-aware code suggestions based on current file content
- File sharing capability for AI-assisted debugging
- Fallback mechanisms for offline/error scenarios

### Authentication Flow
- NextAuth.js with JWT session strategy
- Database sessions stored in MongoDB
- Protected API routes and editor access
- User-specific project isolation

## Design Decisions

### Why Local LLMs?
- Privacy: Code never leaves your machine
- Offline capability: Work without internet connectivity
- Cost: No API usage fees
- Customization: Use specialized models for different tasks

### Why WebContainers?
- Zero-setup development environment
- Consistent runtime across user machines
- Secure sandboxing of code execution
- Support for full-stack applications

### Why Next.js App Router?
- Server-side rendering for improved performance
- Built-in API routes for backend functionality
- Simplified data fetching patterns
- Optimized client-side navigation

## Challenges and Solutions

### Challenge: In-Browser Filesystem Management
**Solution**: Implemented virtual file system with WebContainer's filesystem API, providing create/read/update/delete operations with proper error handling and state synchronization.

### Challenge: Real-time AI Suggestions
**Solution**: Debounced API calls to Ollama with context window optimization, caching frequent patterns, and implementing graceful degradation when AI is unavailable.

### Challenge: Multi-stack Template System
**Solution**: Created template abstraction layer with configuration files for each stack, allowing dynamic project scaffolding with appropriate dependencies and boilerplate.

## Future Enhancements

1. **Collaborative Editing** – Real-time multiplayer code editing
2. **Plugin System** – Extensible architecture for custom tools and integrations
3. **Advanced AI Features** – Code review, automated testing, and deployment assistance
4. **Cloud Sync** – Project synchronization across devices
5. **Additional Runtimes** – Support for Python, Go, and other languages

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- Monaco Editor by Microsoft for the core editing experience
- Ollama for making local LLMs accessible
- WebContainers by StackBlitz for in-browser execution
- NextAuth for authentication infrastructure
- The open-source communities behind Next.js, TailwindCSS, and ShadCN