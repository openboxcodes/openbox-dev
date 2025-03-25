  # openbox-dev - Graph-Based Editor for LLM Workflows



# 🕸️ Why openbox-dev?

- 🖐️ **Drag-and-drop**: Visually build and test workflows in seconds.
- 🧪 **Evals**: Quickly test and refine agent steps interactively.
- 🧰 **Tools**: Connect to Slack, Google Sheets, GitHub, and more.
- 🗃️ **RAG**: Parse, chunk, embed, and upsert data into a vector DB in a few clicks.
- 🚀 **1-Click Deploy**: Publish as an API and integrate wherever you want.
- 🤖 **Multi-agent**: Orchestrate and manage conversations across multiple agents.
- 🐍 **Python-based**: Add new nodes by creating a single Python file.
- 🎛️ **Flexible**: Agnostic to LLMs, embedders, and vector databases.

# ⚡ Quick start

You can launch openbox-dev using pre-built docker images in the following steps:

1. **Clone the repository:**
    ```sh
    git clone https://github.com/openbox/openbox-dev
    cd openbox-dev
    ```

2. **Create a .env file:**

    Create a `.env` file at the root of the project. You may use `.env.example` as a starting point.
    ```sh
    cp .env.example .env
    ```
    **Please go through the .env file and change configs wherver necessary**
    **If you plan to use third party model providers, please add their API keys in the .env file in this step**.

3. **Start the docker services:**

    ```sh
    docker compose -f ./docker-compose.prod.yml up --build -d
    ```

    This will start a local instance of openbox-dev that will store spurs and other state information in a postgres database. A local postgres service is used by default. Override `POSTGRES_*` variables in the `.env` file to use an external postgres database.

4. **Access the portal:**

    Go to `http://localhost:6080/` in your browser.


Set up is completed. Click on "New Spur" to create a workflow, or start with one of the stock templates.


# 🛠️ openbox-dev Development Setup
#### [ Instructions for development on Unix-like systems. Development on Windows/PC not tested ]

The steps for dev setup are same as above, except for step 3: we launch the app in the dev mode instead

3. **Start the docker services:**

    ```sh
    docker compose up --build -d
    ```

    This will start a local instance of openbox-dev that will store spurs and other state information in a postgres database. A local postgres service is used by default. Override `POSTGRES_*` variables in the `.env` file to use an external postgres database.


# 🦙 Using openbox-dev with Ollama (Local Models)

openbox-dev can work with local models served using Ollama.

Steps to configure openbox-dev to work with Ollama running on the same host.

### 1. Configure Ollama
To ensure Ollama API is reachable from openbox-dev, we need to start the Ollama service with environment variable `OLLAMA_HOST=0.0.0.0` . This allows requests coming from openbox-dev docker's bridge network to get through to Ollama.
An easy way to do this is to launch the ollama service with the following command:
```sh
OLLAMA_HOST="0.0.0.0" ollama serve
```

### 2. Update the openbox-dev .env file
Next up we need to update the `OLLAMA_BASE_URL` environment value in the `.env` file.
If your Ollama port is 11434 (the default port), then the entry in `.env` file should look like this:
```sh
OLLAMA_BASE_URL=http://host.docker.internal:11434
```
(Please make sure that there is no trailing slash in the end!)

In openbox-dev's set up, `host.docker.internal` refers to the host machine where both openbox-dev and Ollama are running.

### 3. Launch the openbox-dev app
Follow the usual steps to launch the openbox-dev app, starting with the command:
```sh
docker compose -f docker-compose.prod.yml up --build -d
```

If you wish to do openbox-dev development with ollama please run the following command instead of above:
```sh
docker compose -f docker-compose.yml up --build -d
```


### 4. Using Ollama models in the app
You will be able to select Ollama models [`ollama/llama3.2`, `ollama/llama3`, ...] from the sidebar for LLM nodes.
Please make sure the model you select is explicitly downloaded in ollama. That is, you will need to manually manage these models via ollama. To download a model you can simply run `ollama pull <model-name>`.

## Note on supported models
openbox-dev only works with models that support structured-output and json mode. Most newer models should be good, but it would still be good to confirm this from Ollama documentation for the model you wish to use.

# ⭐ Support us

You can support us in our work by leaving a star! Thank you!

# 🗺️ Roadmap

- [X] Canvas
- [X] Async/Batch Execution
- [X] Evals
- [X] Spur API
- [x] Support Ollama
- [ ] New Nodes
    - [X] LLM Nodes
    - [X] If-Else
    - [X] Merge Branches
    - [X] Tools
    - [ ] Loops
- [X] RAG
- [ ] Pipeline optimization via DSPy and related methods
- [ ] Templates
- [ ] Compile Spurs to Code
- [ ] Multimodal support
- [ ] Containerization of Code Verifiers
- [ ] Leaderboard
- [ ] Generate Spurs via AI
