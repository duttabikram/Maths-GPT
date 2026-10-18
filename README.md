# Maths-GPT

An AI-powered **Mathematics Problem Solver and Information Assistant** built using **LangChain, Groq, and Streamlit**.

Maths-GPT uses an LLM-powered agent that can select between different tools depending on the user's question. It can solve mathematical calculations, handle logic-based reasoning, and retrieve additional information from Wikipedia.

---

## 🚀 Features

- 🧮 **Mathematical Problem Solving**
- 🧠 **Logic & Reasoning**
- 🔢 **Calculator Tool**
- 📚 **Wikipedia Information Search**
- 🤖 **LLM-powered Agent**
- 💬 Interactive chatbot-style interface
- 🔐 Secure Groq API key input through the Streamlit sidebar
- ⚡ Real-time response generation through Streamlit callbacks

The application uses LangChain's agent framework to decide which tool is appropriate for a given question.

---

## 🧠 How It Works

Maths-GPT is built around an **AI agent with multiple tools**.

```text
                    User Question
                         │
                         ▼
                  ┌─────────────┐
                  │  Groq LLM   │
                  │   Gemma     │
                  └──────┬──────┘
                         │
                         ▼
                  ┌─────────────┐
                  │ LangChain   │
                  │    Agent    │
                  └──────┬──────┘
                         │
              ┌──────────┼──────────┐
              │          │          │
              ▼          ▼          ▼
        ┌──────────┐ ┌────────┐ ┌────────────┐
        │Calculator│ │Reasoning│ │ Wikipedia  │
        │   Tool   │ │  Tool   │ │    Tool    │
        └────┬─────┘ └────┬───┘ └──────┬─────┘
             │            │             │
             └────────────┼─────────────┘
                          ▼
                    Final Answer
                          │
                          ▼
                    Streamlit UI
```

---

## 🔧 Tools Used by the Agent

### 1. 🧮 Calculator

The Calculator tool is implemented using LangChain's `LLMMathChain`.

It is designed to handle mathematical expressions and calculations.

```text
User:
What is 25 × 48?

        ↓

Calculator Tool

        ↓

1200
```

The project creates the mathematical tool using `LLMMathChain.from_llm()`.

---

### 2. 🧠 Reasoning Tool

The Reasoning Tool uses an `LLMChain` with a custom prompt.

It is designed to handle logic-based questions and provide a detailed, point-wise explanation of the solution.

For example:

```text
User:
I have 5 bananas and 7 grapes.
I eat 2 bananas and give away 3 grapes.
How many fruits remain?

        ↓

Reasoning Tool

        ↓

Detailed step-by-step explanation
```

---

### 3. 📚 Wikipedia Tool

The project also integrates a Wikipedia search tool using LangChain's `WikipediaAPIWrapper`.

This allows the agent to retrieve information about general topics when additional knowledge is required.

---

## 🤖 LLM

The application uses **Groq** through LangChain's `ChatGroq` integration.

The current code initializes the model as:

```python
llm = ChatGroq(
    model="Gemma2-9b-It",
    groq_api_key=groq_api_key
)
```

The Groq API key is entered securely through the Streamlit sidebar rather than being hard-coded into the application.

> **Note:** If the configured model has been deprecated by Groq, replace it with a currently supported Groq model before running the application.

---

## 🔄 Agent Workflow

The core of the application is the LangChain agent.

The agent receives the user's question and determines which available tool should be used.

```text
1. User enters a question
            ↓
2. Streamlit receives the input
            ↓
3. Question is passed to the LangChain agent
            ↓
4. Agent analyzes the question
            ↓
5. Appropriate tool is selected
            ↓
6. Tool processes the request
            ↓
7. Agent generates the final response
            ↓
8. Response is displayed in Streamlit
```

The agent is initialized with three tools:

```text
Wikipedia
Calculator
Reasoning Tool
```

and uses the `ZERO_SHOT_REACT_DESCRIPTION` agent type.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Core programming language |
| **Streamlit** | Web application interface |
| **LangChain** | LLM orchestration and agent framework |
| **Groq** | LLM inference |
| **Gemma** | Language model |
| **Wikipedia API** | Information retrieval |
| **LLMMathChain** | Mathematical calculations |
| **LLMChain** | Reasoning workflow |

The repository's dependency file includes LangChain, LangChain Community, LangChain Groq, Streamlit, Wikipedia, OpenAI integrations, Hugging Face packages, ChromaDB, FAISS, and other supporting libraries.

---

## 📂 Project Structure

```text
Maths-GPT/
│
├── app.py
│   └── Main Streamlit application
│
├── requirements.txt
│   └── Python dependencies
│
├── Screenshot 2025-08-16 020351.png
│   └── Application screenshot
│
├── README.md
│   └── Project documentation
│
└── LICENSE
    └── GPL-3.0 License
```

The repository currently contains `app.py`, `requirements.txt`, a screenshot, `README.md`, and the GPL-3.0 license.

---

## ⚙️ Installation

### 1. Clone the Repository

```bash
git clone https://github.com/duttabikram/Maths-GPT.git
```

### 2. Navigate to the Project

```bash
cd Maths-GPT
```

### 3. Create a Virtual Environment

```bash
python -m venv venv
```

### 4. Activate the Environment

**Windows:**

```bash
venv\Scripts\activate
```

**Linux / macOS:**

```bash
source venv/bin/activate
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 🔑 Groq API Key

The application requires a **Groq API key**.

When the application starts, enter your API key in the sidebar.

```text
┌──────────────────────────┐
│       Maths-GPT          │
├──────────────────────────┤
│ Groq API Key             │
│ ●●●●●●●●●●●●             │
└──────────────────────────┘
```

The application stops and displays a message if an API key is not provided.

**Do not commit your API key to GitHub.**

---

## ▶️ Run the Application

Start the Streamlit application:

```bash
streamlit run app.py
```

After starting the application, open the URL provided by Streamlit in your browser.

---

## 💡 Example Questions

### Mathematical Calculation

```text
Calculate the compound interest on ₹50,000
at an annual interest rate of 8% for 5 years.
```

### Logical Reasoning

```text
A train travels 120 km in 2 hours.
What is its average speed?
Explain step by step.
```

### General Knowledge

```text
What is the history of the Pythagorean theorem?
```

The agent can determine whether the question is better handled by the calculator, reasoning, or Wikipedia tool.

---

## 🖥️ Application Screenshot

![Maths-GPT Application](Screenshot%202025-08-16%20020351.png)

---

## 🔐 Security

The Groq API key is requested through Streamlit's password-type sidebar input.

For production deployments, it is recommended to use environment variables or a secrets-management mechanism instead of entering credentials manually.

Example:

```text
GROQ_API_KEY=your_api_key_here
```

Never upload API keys or other credentials to a public GitHub repository.

---

## 🚀 Future Improvements

- Add conversation memory for longer mathematical discussions.
- Add support for mathematical diagrams and graphs.
- Add step-by-step equation rendering using LaTeX.
- Add support for uploading mathematical PDFs or images.
- Add OCR for handwritten mathematical problems.
- Improve tool selection with modern LangChain agent architectures.
- Add more specialized mathematical tools.
- Add a dedicated RAG pipeline for mathematical textbooks.
- Deploy the application publicly.
- Add user authentication and usage limits.

---

## ⚠️ Limitations

LLM-generated mathematical explanations may occasionally contain incorrect reasoning or calculations.

For important mathematical work, verify the generated solution independently.

---

## 📜 License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

See the `LICENSE` file for details.

---

## 👨‍💻 Author

**Bikram Dutta**

GitHub: [duttabikram](https://github.com/duttabikram)

---

## ⭐ Support

If you found this project useful, consider giving the repository a ⭐ on GitHub.
