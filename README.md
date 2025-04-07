# SDA-bootcamp-project

Stage 3 - Chatbot with Chat History

A basic chatbot using Streamlit and FastAPI. At this stage, we will store the chat history on the local path and also log the corresponding chat ID, chat name and chat history file path in a database. In this case, every time we open our chatbot, it will automatically load the previous chat history.

In this stage I create a table called `chats` in the database using the following schema:
```
CREATE TABLE IF NOT EXISTS chats (
    id TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    file_path TEXT NOT null,
    last_update TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

Please store your `OPENAI_API_KEY` and **Database Credentials** in `.env` file.

Now the `.env` file should look like:
```
OPENAI_API_KEY=YOUR-OPENAI-API-KEY
DB_NAME = YOUR-DB-NAME
DB_USER = YOUR-DB-USER
DB_PASSWORD = YOUR-DB-PASSWORD
DB_HOST = YOUR-DB-HOST
DB_PORT = YOUR-DB-PORT
```

Start the backend app first using:

```
uvicorn backend:app --reload
```

And then use 
```
streamlit run chatbot.py
```
to run the Streamlit app. Make sure that you always start the backend first!



# SDA-bootcamp-project

Stage 4 - **RAG** Chatbot with Chat history

A RAG chatbot using Streamlit and FastAPI. At this stage, we will add the RAG function to the bot.
Other than creating normal chat, user can upload `pdf` file to the chatbot and ask questions specific to this document 

In this stage, we will create a **new** table called `advanced_chats` in the database using the following schema:
```
CREATE TABLE IF NOT EXISTS advanced_chats (
    id TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    file_path TEXT NOT null,
    last_update TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    pdf_path TEXT,
    pdf_name TEXT,
    pdf_uuid TEXT
)
```
or if you want, you can just add the extra columns in the `chats` database created in stage 3.

Please store your `OPENAI_API_KEY` and **Database Credentials** in `.env` file.

All the requirements are in the `requirements.txt`

To use RAG, we need to start the chromaDB first, using the following command to start the Chroma server:
```
chroma run --path /db_path
```
change `/db_path` to the path you want to store the data, for example: `chromadb`.

Then, start the backend app using:

```
uvicorn backend:app --reload --port 5000
```

> Compared to the last stage, we added a `port` parameter to change the port to `5000`. Since the chromadb will also use port 8000, we added this to avoid port conflict.
And then use 
And then use 
```
streamlit run chatbot.py
```
to run the Streamlit app.
