# Research Chatbot MCP

A Model Context Protocol (MCP) server for academic paper research, enabling AI assistants to search, retrieve, and analyze academic papers from arXiv.

## Overview

This project implements an MCP server that allows AI assistants to:

- Search for academic papers on arXiv based on specific topics
- Store and organize paper information by topic
- Retrieve detailed information about specific papers
- Generate structured prompts for paper analysis

## Features

- **Paper Search**: Search arXiv for papers on specific topics
- **Information Extraction**: Get detailed information about papers including title, authors, publication date, and summary
- **Topic Organization**: Papers are automatically organized by topic in the filesystem
- **Resource Access**: Access papers by topic through MCP resources
- **Prompt Generation**: Generate structured prompts for AI assistants to analyze papers

## Installation

### Prerequisites

- Python 3.12 or higher
- uv (Python package manager)

### Setup

1. Clone this repository:

   ```bash
   git clone https://github.com/shireen168/research_chatbot_mcp.git
   cd research_chatbot_mcp
   ```

2. Install dependencies using uv:

   ```bash
   uv pip install -e .
   ```

## Usage

### Starting the MCP Server

Run the MCP server using:

```bash
uv run research_server.py
```

Alternatively, you can use the server configuration to run multiple MCP servers:

```bash
clauded --config server_config.json
```

### Available MCP Tools

#### `search_papers(topic: str, max_results: int = 5) -> List[str]`

Searches for papers on arXiv based on a topic and stores their information.

- **Parameters**:
  - `topic`: The topic to search for
  - `max_results`: Maximum number of results to retrieve (default: 5)
- **Returns**: List of paper IDs found in the search

#### `extract_info(paper_id: str) -> str`

Searches for information about a specific paper across all topic directories.

- **Parameters**:
  - `paper_id`: The ID of the paper to look for
- **Returns**: JSON string with paper information if found, error message if not found

### Available MCP Resources

#### `papers://folders`

Lists all available topic folders in the papers directory.

#### `papers://{topic}`

Gets detailed information about papers on a specific topic.

- **Parameters**:
  - `topic`: The research topic to retrieve papers for

### Prompt Templates

#### `generate_search_prompt(topic: str, num_papers: int = 5) -> str`

Generates a prompt for AI assistants to find and discuss academic papers on a specific topic.

## Project Structure

```text
├── README.md               # This file
├── research_server.py      # Main MCP server implementation
├── server_config.json      # Configuration for running multiple MCP servers
├── pyproject.toml          # Python project dependencies
├── papers/                 # Directory where papers are stored by topic
│   └── {topic}/            # Topic-specific directories
│       └── papers_info.json # JSON file containing paper information
```

## Dependencies

- `anthropic`: For AI assistant integration
- `arxiv`: For searching and retrieving papers from arXiv
- `mcp`: Model Context Protocol library
- `nest-asyncio`: For handling async operations
- `python-dotenv`: For environment variable management

## Example Workflow

1. Search for papers on a topic:

   ```python
   paper_ids = search_papers("generative AI", max_results=5)
   ```

2. Extract information about a specific paper:

   ```python
   paper_info = extract_info(paper_ids[0])
   ```

3. Access papers by topic through resources:

   ```text
   papers://generative_ai
   ```

## License

[MIT License](LICENSE)
