# ChatGPT FAQ Bot:
Answers about application deadlines, required documents, tuition fees, scholarship opportunities, etc.

## Approach
1. Gathered data from json formatted.
2. Authentication, openai and weaviate.
3. Loaded the data
4. Embedded the extracted data.
5. Stored the embeddings into weaviate vector database.
6. chatgpt will retrieve the relevant chunks given predefined system prompt.
7. It will give answer to user's query as response.

## Challenges and learnings
1. Problem in using JSONLoader: COuldn't install jq in windows. Conbverted json to pd DataFrame then to csv to use CSVLoader. But then 'Document' object was not subscriptable. Extracted data from json with 'columns' format.
2. After keyword search was successfully done, unable to perform semantic search: Without using cohere, we need to make use of embeddings. OpenAi has no attribute 'embed', it requires upgraded openai. Upgraded, but openai.embedding_utils is removed from library following 1.0. Downgraded openai to 0.27.7 then got langchain-openai requires openai<2.0> >= 1.0, 0.27.7 is incompatible.
3. Tried Weaviate hybrid search: v3 client is deprecated. While embedding data into vectorstore, 'dict' method is deprecated, need to use 'model_dump' instead. Upgraded to v4. But langchain_community uses deprecated method from earlier version of Pydantic 2.5.2. Weaviate model_dump depends on Pydantic 3 but langchain does not & there is a conflict.
