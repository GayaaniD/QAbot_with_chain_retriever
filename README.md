# QAbot_with_chain_retriever
![image](https://github.com/GayaaniD/QAbot_with_chain_retriever/assets/125920863/272eb519-6935-4e77-ace1-a11e2c754f3b)

This is about building an advanced Q&A chatbot using Langchain’s chain and retriever functionality.
## Chains and Retrievers in Langchain
**Chains** : In Langchain, chains refer to sequences of calls that can involve LLMs, data pre-processing steps, or other tools. Langchain provides support for constructing your own chains using LCEL (Langchain Extended Language), but it also offers pre-built chains that you can use readily.
**Retrievers** : A retriever is an interface that retrieves documents based on an unstructured query. It acts as a more general interface than a vector store, as it does not necessarily need to store documents itself. Vector stores can be used as the underlying data source for retrievers, allowing you to perform similarity search to retrieve relevant documents based on a query vector.

The following steps outline the creation of a Q&A chat bot using chain and retriever functionality in Langchain :
1. **Data Ingestion:**
    - Data ingestion in Langchain refers to the process of importing data into the system. 
    - In the data ingestion process for Langchain, the PyPDFLoader from the langchain_community package is utilized to import the contents of a PDF file. This loader is specifically designed to read PDF files and convert them into a format that Langchain can process. By creating an instance of PyPDFLoader with the target PDF file, and then invoking the load method, the data from the PDF is ingested into Langchain, making it ready for further language processing tasks.

2. **Data Transformation:**
     - After loading the data, want to transform it before feeding it into the LLM.
     - In Langchain’s data transformation step, the RecursiveCharacterTextSplitter from the text_splitter module is employed to divide the text into more manageable segments. This is particularly useful when preparing data for a Language Learning Model (LLM), as it ensures that the text is in optimal-sized chunks. By specifying a chunk size and overlap, the splitter methodically breaks down the text from the loaded documents, resulting in a series of smaller, overlapping text blocks ready for model processing.
   
3. **Vector Embedding and Storing:**
     - The vector embedding and storing phase is crucial in Langchain as it translates text data into a numerical format that the LLM can interpret.
     - For vector embedding and storage in Langchain, specific moduleOpenAIEmbeddings from the langchain_community.embeddings package is used to convert text into vector representations. Additionally, the FAISS module from the langchain_community.vectorstores package is utilized to store these vectors. The process involves initializing the chosen embedding method and then passing the transformed documents to FAISS, which creates a vector store. This store allows for efficient querying and retrieval of data, making it a vital step for preparing text for LLMs by ensuring that the data is in a machine-readable vector format.
       
4. **Creating the Chain and Retriever:**
     - In Langchain, creating the Chain and Retriever involves two key components. The Stuff Documents Chain consolidates a list of documents into a single prompt for the LLM, using the create_stuff_documents_chain function. This chain is tailored to the LLM’s needs, ensuring that the input is structured correctly. The Retriever, on the other hand, is responsible for fetching documents from a data source based on a query. By converting the previously created vector store into a retriever object with the as_retriever() method, it becomes possible to retrieve documents efficiently.
     - This setup is essential for facilitating effective communication between the user’s queries and the LLM’s document-based responses.
       
5. **Combining Retriever and Chain: Retrieval Chain**
     - The Retrieval Chain in Langchain is a sophisticated mechanism that merges the capabilities of both the retriever and the document chain. It begins by taking a user’s query and employing the retriever to fetch pertinent documents from the vector store. These documents are then combined with the original documents and fed into the document chain. The create_retrieval_chain function orchestrates this process, ensuring that the LLM receives a comprehensive prompt that includes both retrieved and original information.
     - This chain is pivotal for leveraging the LLM’s full potential in processing and responding to user queries with contextually relevant information.
       
6. **Invoking the Chain with a User Query :**
    - With the retrieval chain established in Langchain, it’s now ready to address user inquiries. To utilize the chain, simply provide it with a user query. The chain is then invoked with this query, which triggers the retrieval of relevant documents and their subsequent processing. The result is an answer generated by the LLM, which can be displayed.

##  How the Chat bot Responds to a User Query
![image](https://github.com/GayaaniD/QAbot_with_chain_retriever/assets/125920863/12f2f7f0-c4e5-4aa9-a103-c37f3fa97e24)
1. **User Asks a Question:** The user initiates the conversation by asking a question.

2. **Retriever in Action:** The user’s query is directed to the retriever. The retriever acts like a bridge to the vector store. It searches the vector store (which contains documents represented as vectors) for documents most relevant to the query. It calculates the similarity between the query vector and document vectors and retrieves the most relevant documents.

3. **Stuff Document Chain Prepares:** Meanwhile, the stuff document chain takes all the loaded documents and combines them into a single prompt specifically designed for the LLM model.

4. **LLM Model Gets Involved:** The LLM model, a powerful AI trained on massive amounts of text data, is capable of understanding and responding to natural language. In this scenario, the LLM receives the prompt created by the stuff document chain (encompassing all documents).

5. **Combining Information for a Response:** It’s important to note that the LLM doesn’t directly get the user’s query. Instead, it analyzes the prompt (containing all documents) alongside the documents retrieved by the retriever based on the user’s specific question.

6. **Generating a User-Friendly Response:** By considering both the prompt (all documents) and the retrieved documents, the LLM model can generate a comprehensive and informative response tailored to the user’s specific needs. This answer is then included in the response object returned by retrieval_chain.invoke. The final answer is extracted from the response object.

## How to Run the Project
1. Clone the GitHub repository.
2. Rename the `.env.example` file to `.env` and add your API keys.
3. Install the project dependencies by running the `requirements.txt` file. You can do this by opening your terminal and typing:
    ```
    pip install -r requirements.txt
    ```
4. After the dependencies are installed, you can run the project.
