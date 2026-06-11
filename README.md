#Pizza Chatbot - Local AI RAG Prototype

A simple Python-based chatbot that answers questions about a pizza restaurant. 

Instead of letting the AI guess the answers, this project uses **RAG (Retrieval-Augmented Generation)**. When a user asks a question, the system searches a local database for real restaurant reviews, hands them to a local AI model (**Llama 3.2** via Ollama), and forces the AI to answer using *only* those real facts.

---

## 🛠️ How it Works (Data Flow)

```text
[User asks a question] ──► [System finds matching reviews] ──► [AI reads reviews] ──► [AI prints true answer]
User Input: The user types a question into the terminal (e.g., "Do people like the pepperoni pizza?").

Context Retrieval: The script searches a pre-built vector database of restaurant reviews to find relevant matches.

AI Injection: The script plugs those specific reviews and the original question into a template.

Local Response: The local AI model (Llama 3.2) reads the reviews and generates an answer grounded strictly in reality.

🚀 Key Features
No Hallucinations: Because the AI is forced to read specific reviews before answering, it won't make up fake information about the restaurant.

100% Free & Private: Runs entirely on your local computer using Ollama. No data is sent to the cloud, and there are no API costs.

Interactive Loop: A simple terminal loop allows users to continuously ask questions until they type q to quit.

📂 Project Structure
main.py – The file containing your interface loop and prompt assembly logic.

vector.py – The background script that sets up the database retriever.

README.md – This project documentation file.

1. The Prompt Template
This sets the rules for the AI. The curly braces {reviews} and {question} are placeholders that get filled with real data dynamically.

Python
template = """You are an expert in answering questions about a pizza restaurant.

Here are some relevant reviews: {reviews}

Here is the question to answer: {question}"""
2. The Chain and Execution Loop
We link the prompt and the AI model together using LangChain's pipeline operator (|). The code repeats continuously, pulling matching reviews and printing answers.

Python
# Fetches the relevant reviews from the database
reviews = retriever.invoke(question)

# Feeds the reviews and question into the AI pipeline
result = chain.invoke({"reviews": reviews, "question": question})
print(result)
⚡ Setup & Quick Start
1. Install Requirements
Make sure you have Ollama installed on your computer, then download the model:

Bash
ollama pull llama3.2
2. Install Libraries
Bash
pip install langchain-ollama langchain-core
3. Run the App
Bash
python main.py
