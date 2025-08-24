# L2-Memory.ipynb

## ConversationalBufferMemory:
Allows storing the message and the extract later using variables
eg: conversation.predict(input="Hi, my name is Andrew")

## ConversationBufferWindowMemory
Keeps the list of intersation of conversation over time and extract only last k conversation from the list.

## ConverserationTokenBufferMemory
Keeps the buffer of recent interaction in memory and use length of tokens instead of number of last interaction.

## ConversationSummaryMemory
Create summary of conversation over time.

## Vector Data Memory
Stores conversation into vector database and retrieve the most relevant block of text

## Entity Memory
Using an LLM, it remembers the details about specific entity

We can use more than one more memory at a time. For example converstaion+entity -> recall individual
