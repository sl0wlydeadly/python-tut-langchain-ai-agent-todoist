# Todoist + Gemini CLI Assistant

A very small command-line assistant that talks to you and manages your Todoist tasks using Google’s Gemini API via LangChain.

You can:

- **Add tasks** to Todoist in natural language.
- **List your existing tasks** as a bullet list.

---

## Requirements

- Python 3.10+ (recommended)
- A **Todoist API token**
- A **Google API key** with access to **Gemini** models

---

## Setup

1. **Clone this repository**

```bash
git clone <your-repo-url>.git
cd <your-repo-folder>
```

2. **Create and activate a virtual environment (optional but recommended)**

```bash
python -m venv .venv
source .venv/bin/activate      # on macOS / Linux
# .venv\Scripts\activate     # on Windows
```

3. **Install dependencies**

```bash
pip install python-dotenv langchain langchain-core langchain-google-genai todoist-api-python
```

4. **Create a `.env` file in the project root**

```env
TODOIST_API_KEY=your_todoist_api_token_here
GEMINI_API_KEY=your_google_api_key_here
```

---

## Usage

Run the assistant:

```bash
python main.py
```

You’ll see:

```text
Speak and you shall be heard:
```

Now you can type things like:

- `Add a task to buy milk tomorrow morning`
- `Create a task to prepare slides for the meeting`
- `Show my tasks`
- `List my todo list`

The assistant will:

- Decide whether to **add a new task** (and generate a nice description), or  
- **Show your existing tasks** from Todoist in a bullet list.

Press **Ctrl + C** to exit.

---

## How It Works (Very Briefly)

- Uses **LangChain** with `ChatGoogleGenerativeAI` (`gemini-2.5-flash`) as the LLM.
- Defines two LangChain tools:
  - `add_task(task, description=None)` → adds a task to Todoist.
  - `show_tasks()` → returns all task titles from Todoist.
- Uses `create_openai_tools_agent` + `AgentExecutor` to let the model call these tools based on your input.
- Maintains a simple **chat history** so the conversation has context.
