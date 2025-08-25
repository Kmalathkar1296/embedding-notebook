# L2-Memory.ipynb

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

# L3-Chains.ipynb

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

# L4

### **Stuff**

### **Map-Reduce**

### **Refine**

### **Map-Rerank**
