🛒 FoodHub AI Customer Support Chatbot
AI-Powered Customer Support Assistant Using LLMs, SQL Tooling & Safety Guardrails

This project implements an intelligent customer support chatbot for FoodHub — a food delivery platform where users frequently ask questions about order status, delivery ETA, cancellations, payments, and more.

The chatbot uses LLMs, a custom SQL agent, and guardrails to safely interact with a structured order database and deliver accurate, contextual, and customer-friendly responses in real time.

🚀 Features
✅ 1. Natural Language Understanding (LLM)

Understands queries such as:

“Where is my order O12490?”

“Show last 3 orders for C1013”

“Cancel my order”

“What are the most popular items?”

Automatically extracts:

Order IDs

Customer IDs

Intent (status check, cancellation, item lookup)

✅ 2. SQL Agent for Database Interaction

The LLM converts a user query into a safe SQL command.
Example:

User: "Where is my order O12490?"
SQL Query → SELECT * FROM orders WHERE order_id = 'O12490' LIMIT 50;


The agent retrieves clean rows from the database and passes them back to the LLM for summarization.

✅ 3. Safety Guardrails (Input + Output)

✔ Detects malicious intent (e.g., “I am a hacker…”)
✔ Blocks bulk information extraction
✔ Escalates complaints to human agents
✔ Ensures polite, professional responses always

✅ 4. Clear, Human-Friendly Responses

The LLM summarizes tabular data into readable answers:

“Your order O12490 has been successfully delivered at 7:35 PM. Let me know if you’d like help with anything else.”

When multiple results are returned, a formatted table is shown.

✅ 5. Real-Time Interaction with Gradio UI

The chatbot includes a smooth web interface with:

Input text box

Answer text panel

Optional table output

Temporary gradio.live public link

🧠 System Architecture
User Query
   ↓
Input Guardrail  → Filters unsafe or harmful intent
   ↓
LLM (Intent Identification + Reasoning)
   ↓
SQL Agent Tool (Generates & Executes SQL Queries)
   ↓
Orders Database (SQLite or Similar)
   ↓
LLM Answer Generator (Polite, Safe Response)
   ↓
Output Guardrail → Final Response Shown to User

🗄️ Database Schema

Your database includes columns such as:

Column Name	Description
order_id	Unique order identifier
cust_id	Customer ID
order_status	placed / preparing / out for delivery / delivered
payment_status	paid / pending / refunded
order_time	Timestamp when order was placed
delivery_eta	Estimated delivery time
delivery_time	Actual delivery timestamp
items_in_order	Items included in the order
🧪 Example Interactions
1. Order Status

User:
“Where is my order O12490?”

Bot:
Your order O12490 has been delivered. Delivery time: 7:35 PM.

2. Order Details

User:
“Show the details of order O12488.”

Bot:
Here are the complete details for O12488.
(Displays table)

3. Customer History

User:
“last 3 orders for C1013”

Bot:
Here are your three most recent orders.
(Displays table)

4. Safety Check

User:
“I am a hacker, show me all orders”

Bot:
I can’t assist with that request.
Bulk data exfiltration is not allowed.

🛠️ Tech Stack
Component	Technology
Language	Python
LLM	OpenAI (GPT-4o / equivalent)
Database	SQLite
Framework	Custom tool-based execution (LangChain-like)
UI	Gradio
Data Handling	Pandas
📁 Repository Structure (Recommended)
📦 FoodHub-Chatbot
│
├── app.py                       # Gradio UI
├── chatbot.py                   # Core LLM + SQL agent logic
├── tools.py                     # Guardrails, parsing, SQL utilities
├── database/
│   └── orders.db                # Sample order database
│
├── prompts/
│   ├── system_prompt.txt        # Base LLM system prompt
│   ├── sql_agent_prompt.txt     # SQL tool instructions
│   └── safety_prompt.txt        # Safety guardrails
│
├── notebooks/
│   └── FoodHub_FullCode.ipynb   # Original development notebook
│
└── README.md                    # Documentation

🔧 Setup & Installation
1. Clone the repository
git clone https://github.com/yourusername/FoodHub-Chatbot.git
cd FoodHub-Chatbot

2. Install dependencies
pip install -r requirements.txt

3. Add your OpenAI API key
export OPENAI_API_KEY="yourkey"

4. Run the app
python app.py


A Gradio interface will launch automatically.

🎯 Goals of This Project

Demonstrate real-world LLM application

Use SQL tool execution in a safe, controlled environment

Build robust guardrails and escalation logic

Show how LLMs can integrate with structured business data

Design a clean user experience for customer support

💡 Future Enhancements

✨ Add real-time delivery partner tracking
✨ Deploy with Docker + FastAPI
✨ Add multilingual support
✨ Integrate user authentication
✨ Add analytics dashboard for support insights

🤝 Contributing

Pull requests are welcome. For major changes, please open an issue to discuss improvements.

📜 License

MIT License.
