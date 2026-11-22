# Assignment 4 — A Multi-Agent Help Desk

CSCI 395.32: AI Agents · Hunter College, CUNY · Fall 2026

Work in pairs. You build the **Riverview College help desk**, a multi-agent system in LangGraph. A student sends one message that can ask for several things at once: what they still need for their major, and sections of several courses. The system splits the message into parts, sends each part to a specialist agent that works in parallel in its own context, checks the specialists' picks together in plain code, and combines everything into one answer. You write the plan prompt, the routing, the two specialists, the check, and the graph.

Riverview College is fictional. Its data does not describe Hunter College or CUNY policy.

## Start here

1. Follow [`SETUP.md`](SETUP.md) to install the environment (about 15 minutes). This assignment runs locally, not in Colab.
2. Open `Assignment04_Multiagent_Help_Desk.ipynb` and run the setup check, its first code cell.
3. Work through the notebook in order. The LangGraph multi-agent tutorial uses the same patterns; keep it open.

## What is in this folder

| File or folder | Contents |
|---|---|
| `Assignment04_Multiagent_Help_Desk.ipynb` | the notebook you complete and submit |
| `data/` | the Riverview data (`catalog.json`, `sections.json`, `requirements.json`, `students.json`), the public questions (`public_questions.json`), and `README.md` with the rules every tool and answer follows |
| `pyproject.toml`, `uv.lock`, `.python-version` | the environment definition, used by `uv sync` |
| `.env.example` | a template for your `.env` file with your OpenRouter key |
| `SETUP.md` | installation steps and troubleshooting |

Keep the notebook next to the `data/` folder: the notebook reads the data from there.

## What you submit

- The completed notebook, with its saved outputs, named after your team (for example `team_name.ipynb`).
- `results.json`, which the notebook writes in §11, renamed to match (for example `team_name_results.json`).

Do not submit your `.env` file or your API key.
