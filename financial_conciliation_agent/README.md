# Autonomous Financial Auditor (Hybrid Agentic Architecture)

An end-to-end AI Data Agent designed to autonomously reconcile internal rental records against bank statements. This Proof of Concept (PoC) identifies missing payments (defaults), detects hidden bank fees (value discrepancies), and generates a CFO-ready executive report.

## The Problem

Financial reconciliation is typically a manual, error-prone process. While Large Language Models (LLMs) offer great reasoning capabilities, feeding raw financial data into small-parameter local models often leads to "math hallucinations", context bloat, and broken reporting formats.

##  The Solution: Hybrid Engine & Inversion of Control

To ensure **100% deterministic accuracy** while maintaining the natural language synthesis of AI, this project uses a Hybrid Architecture:

1. **Deterministic Layer (Python/Pandas):** Handles all exact data matching (via Regex), mathematical variance calculations, and generates bulletproof UI components (Seaborn charts and pure HTML tables).
2. **Cognitive Layer (Llama 3.2 via Ollama):** Acts strictly as an executive "Ghostwriter". It receives pre-calculated metrics and synthesizes the operational risks into a professional narrative.

### Key Engineering Challenges Overcome

Throughout the development, several limitations of local, small-parameter LLMs (1B/3B) were identified and solved:

* **Context Bloat & Timeouts:** Iterating through hundreds of records using a ReAct loop caused the local server to crash. *Solution:* Shifted bulk data aggregation to Python, passing only final stats to the LLM.
* **MathJax & Markdown Failures:** The LLM's usage of the `$` symbol and complex Markdown tables broke Jupyter's rendering engine. *Solution:* Implemented Python-side HTML table generation (`.to_html()`) and prompt sanitization (replacing `$` with `BRL`).
* **Financial Hallucinations:** The model occasionally invented monetary losses. *Solution:* Enforced strict "Prompt Guardrails" and removed the model's control over the document's structure (Inversion of Control).

##  Project Structure & Custom Tools

To maintain a clean and production-ready architecture, the heavy lifting is modularized outside the main Jupyter Notebook. The project relies heavily on complementary `.py` modules obtain in DeepLearning.ai Agentic AI course:

* **`my_utils.py` & `my_tools.py`**: These files contain essential helper functions and tools for the agents. This includes the deterministic reconciliation logic, console logging mechanisms, and **critical HTML manipulation modules** used to render the final report securely, bypassing Jupyter's Markdown/MathJax constraints. *Note: These files must remain in the same directory as the notebook to run the pipeline.*

##  Tech Stack

* **Language:** Python 3.12+
* **Data Processing & Viz:** Pandas, Matplotlib, Seaborn
* **AI/LLM:** Local Llama 3.2 (1B) running via Ollama / `aisuite`
* **Environment:** Jupyter Lab

##  How to Run

1. Clone the repository:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/autonomous-financial-auditor.git](https://github.com/YOUR_USERNAME/autonomous-financial-auditor.git)
   cd autonomous-financial-auditor
   ```

2. Install the required Python libraries:
   ```bash
   pip install pandas matplotlib seaborn aisuite
   ```

3. Ensure [Ollama](https://ollama.com/) is installed and running the Llama 3.2 model:
   ```bash
   ollama run llama3.2:1b
   ```

4. Open the Jupyter Notebook and execute the cells to run the `run_final_pipeline()`.

## Future Work

* **RAG Integration:** Allow the agent to query actual PDF rental contracts to cross-reference hidden fee clauses.
* **Multi-Agent Orchestration:** Implement an "Email Dispatcher Agent" to automatically draft collection notices to defaulting hosts.
* **Web Dashboarding:** Migrate the Jupyter pipeline into an interactive Streamlit application.
