## L2-Memory.ipynb

This repository explores the various memory types available in LangChain for building stateful and contextual conversational applications. Each memory type is designed to handle different scenarios, from simple chat history to complex, long-running conversations.

### **ConversationalBufferMemory**
This is the simplest memory type, storing the complete conversation history in a buffer. It allows for easy access and extraction of past messages.
* **Description:** Stores all messages and can be extracted later using variables.
* **Example:** `conversation.predict(input="Hi, my name is Andrew")`

### **ConversationBufferWindowMemory**
This memory type is useful for managing long conversations by keeping a limited history.
* **Description:** Keeps a list of recent conversation interactions and extracts only the last **$k$** conversations from the list.

### **ConversationTokenBufferMemory**
Similar to `ConversationBufferWindowMemory`, but it manages the buffer based on the number of tokens, which helps control costs and manage context window sizes.
* **Description:** Keeps a buffer of recent interactions and uses the length of tokens instead of the number of last interactions.

### **ConversationSummaryMemory**
For very long conversations, this memory type summarizes the chat history to maintain context without exceeding token limits.
* **Description:** Creates a summary of the conversation over time.

### **Vector Data Memory**
This advanced memory type stores conversation history in a vector database for efficient retrieval of the most relevant information.
* **Description:** Stores conversations into a vector database and retrieves the most relevant block of text.

### **Entity Memory**
This specialized memory uses an LLM to identify and remember specific details about entities mentioned in a conversation.
* **Description:** Uses an LLM to remember the details about a specific entity.

### **Combining Memory Types**
It's possible to use more than one memory type at a time to create a more robust conversational experience.
* For example, you can combine **`ConversationalBufferMemory`** with **`Entity Memory`** to recall individual facts while maintaining recent conversation context.

---

## L3-Chains.ipynb

### **llm chain**
It is a basic chain which takes inputs, formats them into a prompt, sends them to the LLM, and returns the output.

### **SequentialChain**

**Simplesequentialchain**
It takes single input and return single output

**MultiSequentialChain**
It takes the multiple input variables and produces the multiple output.

### **RouterChain**
Instead of always running a fixed sequence of chains (like in SequentialChain), it decides dynamically which chain to run based on the input. Similar switch/case statement but powered by LLM.
If nothing input satisfies the given prompt then it use llm and provide the output

---

## L4-Q&A.ipynb

* Uses embeddings to convert the catalog rows into vectors.
* Stores them in an in-memory vector database for semantic search.
* Takes your query → retrieves relevant rows → passes them to the LLM → gets a Markdown table back.

### **Stuff**
**How it works:**
* Takes all retrieved documents.
* “Stuffs” them directly into the prompt with your question.
* Sends the whole thing to the LLM at once.

**Pros:**
Simple, fast, often works well if docs are short.

**Cons:**
* Breaks if documents are too long (token limit).
* LLM might get distracted by irrelevant info.

Analogy: Like dumping all your notes on a desk and asking GPT, “Answer using everything here.”

### **Map-Reduce**
**How it works:**
Map step: For each retrieved document, the LLM generates a partial answer.
Reduce step: Another LLM call combines those partial answers into a final answer.

**Pros:**
* Scales to large document sets (since each doc is handled separately).
* Prevents token overflow.

**Cons:**
* More LLM calls → slower & costlier.
* Quality depends on how well the “reduce” merges answers.

Analogy: Each student reads one chapter and writes a summary → teacher combines all summaries into one essay.

### **Refine**
**How it works:**
Starts with the first document → generates an initial answer.
Then, for each subsequent document, the LLM updates/refines the answer with new information.

**Pros:**
* Produces high-quality answers that evolve as more docs are read.
* Works well if order of docs makes sense.

**Cons:**
* If an early doc misleads, later ones may not fully “fix” it.
* Sequential → can be slower.

Analogy: Writing an essay draft, then revising it as you read more sources.

### **Map-Rerank**
**How it works:**
For each document, the LLM produces (answer, score) where the score reflects confidence.
The system picks the best answer based on scores.

**Pros:**
* Good when you want just the single most relevant doc answer.
* Helps avoid “hallucinations” from irrelevant docs.

**Cons:**
Discards potentially useful information from other docs.

Analogy: Each student answers a question and rates their confidence → you keep the best-scoring answer.

**👉 In practice:**
* Stuff is great for toy projects and small CSVs (like your clothing catalog).
* Map-Reduce is used when you have hundreds/thousands of long documents.
* Refine is good for research-style tasks where answers get better with context.
* Map-Rerank is best for fact-based QnA (e.g., legal doc lookup, FAQ search).

## 

### **Loaders**
It deals ith accessing and converting data
* Data Access: Website, YouTube, DataBase,..
* Data Types: Pdf, HTML, JSON, Word,..


## **Document Splitting** 

Splitting the data into chuncks and retaining the meaningful relantionship.

Example:

langchain.text_splitter.CharacterTextSplitter(

  chunk_size = n,
  
  chunk_overlap = m,
  
  seperator = '',
  
  length_function = <built-in-function-length>
  
)

### **Types of Splitters**
* RecursiveCharacterTextSplitter -> Recursively tries to split by different character to find one that works
* CharacterTextSplitter -> splitting text that looks at characters
* MarkdownHeadTextSplitter -> Splitting markdown files based on headers
* TokenTextSplitter -> splitting text that looks at token
* SentenceTransformerTokenTextSplitter
* Language() -> for CCP, Python, markdown etc
* SpacyTextSplitter -> splitting text that looks at sentence using spacy
* NLTKTextSplitter
