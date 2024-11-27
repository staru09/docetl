# Playground

The playground is a web app that allows you to interactively build DocETL pipelines. The playground is built with Next.js and TypeScript. We use the `docetl` Python package (built from this source code) to process the data with a FastAPI server. We stream out the logs from the FastAPI server to the frontend so you can see the pipeline execution progress and outputs in real time.

## Why an interactive playground?

Often, unstructured data analysis tasks are fuzzy and require iteration. You might start with a prompt, see the outputs for a sample, then realize you need to tweak the prompt or change the definition of the task you want the LLM to do. Or, you might want to create a complex pipeline that involves multiple operations, but you are unsure of what prompts you want to use for each step, so you want to build your pipeline one operation at a time.

The playground allows you to do just that.

## Installation

There are two ways to run the playground:

### 1. Using Docker (Recommended for Quick Start)

The easiest way to get started is using Docker:

1. Create the required environment files:

Create `.env` in the root directory:
```bash
OPENAI_API_KEY=your_api_key_here
BACKEND_ALLOW_ORIGINS=
BACKEND_HOST=localhost
BACKEND_PORT=8000
BACKEND_RELOAD=True
FRONTEND_HOST=localhost
FRONTEND_PORT=3000
```

Create `.env.local` in the `website` directory:
```bash
OPENAI_API_KEY=sk-xxx
OPENAI_API_BASE=https://api.openai.com/v1
MODEL_NAME=gpt-4o-mini

NEXT_PUBLIC_BACKEND_HOST=localhost
NEXT_PUBLIC_BACKEND_PORT=8000
```

2. Run Docker:
```bash
make docker
```

This will:
- Create a Docker volume for persistent data
- Build the DocETL image
- Run the container with the UI accessible at http://localhost:3000 and API at http://localhost:8000

To clean up Docker resources (note that this will delete the Docker volume):
```bash
make docker-clean
```

### 2. Running Locally (Development Setup)

For development or if you want to run the UI locally:

1. Clone the repository:
```bash
git clone https://github.com/ucbepic/docetl.git
cd docetl
```

2. Set up environment variables in `.env` in the root directory:
```bash
OPENAI_API_KEY=your_api_key_here
BACKEND_ALLOW_ORIGINS=
BACKEND_HOST=localhost
BACKEND_PORT=8000
BACKEND_RELOAD=True
FRONTEND_HOST=0.0.0.0
FRONTEND_PORT=3000
```

Create `.env.local` in the `website` directory:
```bash
OPENAI_API_KEY=sk-xxx
OPENAI_API_BASE=https://api.openai.com/v1
MODEL_NAME=gpt-4o-mini

NEXT_PUBLIC_BACKEND_HOST=localhost
NEXT_PUBLIC_BACKEND_PORT=8000
```

!!! note
    Note that the OpenAI API key, base, and model name in the `.env.local` file are only for the UI assistant functionality, not the DocETL pipeline execution engine.

3. Install dependencies:
```bash
make install      # Install Python package
make install-ui   # Install UI dependencies
```

4. Start the development server:
```bash
make run-ui-dev
```

5. Navigate to http://localhost:3000/playground to access the playground.

### Setting up the AI Assistant

The UI offers an optional chat-based assistant that can help you iteratively develop your pipeline. It is currently very experimental. It can't write to your pipeline, but you can bounce ideas off of it and get it to help you iteratively develop your pipeline.

To use the assistant, you need to set your OpenAI API key in the `.env.local` file in the website directory. You can get an API key [here](https://platform.openai.com/api-keys). The API key should be in the following format: `sk-proj-...`. We only support the openai models for the assistant.

## Complex Tutorial

See this [YouTube video](https://www.youtube.com/watch?v=IlgueVqtHGo) for a more in depth tutorial on how to use the playground.