# Chrome DevTools MCP

## Architecture Overview

```text
+--------------------+       JSON-RPC (MCP)      +------------------------+
|   MCP Client /     | ------------------------> |   Chrome DevTools      |
|    AI Assistant    | <------------------------ |   MCP Server (Daemon)  |
+--------------------+                           +------------------------+
                                                             |
                                                       Puppeteer / CDP
                                                             |
                                                             v
                                                 +------------------------+
                                                 |     Google Chrome      |
                                                 |   (Browser Instance)   |
                                                 +------------------------+
```

## Process Architecture Diagram

```text
+-----------------------------------------------------------+
|                   CLI / MCP Client                        |
|   (Terminal, Claude Code, Cursor, Gemini CLI, etc.)       |
+-----------------------------------------------------------+
                             |
             JSON-RPC via IPC / StdIO / Socket
                             v
+-----------------------------------------------------------+
|             chrome-devtools MCP Daemon                    |
|             (Background Node.js Process)                  |
|  - Manages session state, tab lists, trace data           |
|  - Listens to lifecycle commands (start / stop / status)  |
+-----------------------------------------------------------+
                             |
             Puppeteer / Chrome DevTools Protocol (CDP)
                             v
+-----------------------------------------------------------+
|                 Chrome Browser Instance                   |
|         (Google Chrome or Chrome for Testing)             |
|  - Main Browser Process                                   |
|  - Render & Network Processes                             |
|  - GPU & Utility Sub-processes                            |
+-----------------------------------------------------------+
```
