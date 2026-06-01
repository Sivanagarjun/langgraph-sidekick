LangGraph Sidekick — Autonomous Browser AI Agent
A production-grade autonomous AI agent built with LangGraph that browses the web, completes tasks, and self-evaluates its own work quality — replicating OpenAI's Operator functionality.
Live Demo
Run `python app.py` and open `http://127.0.0.1:7860`
What It Does
Autonomously browses any website using PlayWright
Completes tasks described in plain English
Self-evaluates work against user-defined success criteria
Retries automatically if quality criteria not met
Sends push notifications via Pushover API
Architecture — Two Agent System
```
User Request + Success Criteria
          ↓
    Worker Agent (GPT-4o-mini)
    ├── Browses web autonomously
    ├── Reads and extracts content
    └── Completes the task
          ↓
    Evaluator Agent (GPT-4o-mini)
    ├── Checks work against success criteria
    ├── Provides structured feedback
    └── Decides: PASS → END or FAIL → retry
```
Tech Stack
LangGraph — Multi-agent graph orchestration
PlayWright — Autonomous web browsing
GPT-4o-mini — Worker and Evaluator LLMs
Pydantic — Structured evaluator output
MemorySaver — Persistent conversation memory
Gradio — Professional chat UI with gr.Blocks
Key Features
Self-improving — Agent reads evaluator feedback and retries with corrections
Structured evaluation — Evaluator returns typed output (feedback, success_criteria_met, user_input_needed)
Unique session IDs — Each conversation gets UUID thread for isolated memory
Reset functionality — Fresh conversation with new thread ID on demand
Setup
```bash
# Clone the repo
git clone https://github.com/Sivanagarjun/langgraph-sidekick

# Install dependencies
pip install -r requirements.txt
playwright install chromium

# Create .env file
OPENAI_API_KEY=your_key_here
PUSHOVER_TOKEN=your_token (optional)
PUSHOVER_USER=your_user (optional)

# Run
python app.py
```
Example Usage
Request: "Go to bbc.com and find the top 3 news headlines today"
Success Criteria: "Give me exactly 3 headlines with a one sentence summary of each"
Agent Output:
```
1. Headline one — one sentence summary
2. Headline two — one sentence summary  
3. Headline three — one sentence summary

Evaluator: Success criteria met ✅
```
Project Structure
```
├── app.py              # Gradio UI launcher
├── sidekick.py         # Main Sidekick class with Worker + Evaluator
├── sidekick_tools.py   # PlayWright browser tools setup
├── requirements.txt    # Dependencies
└── README.md
```
Skills Demonstrated
Multi-agent LangGraph architecture
Autonomous web browsing with PlayWright
Structured LLM output with Pydantic
Async Python programming
Self-evaluating agent loops
Production Gradio UI with gr.Blocks
