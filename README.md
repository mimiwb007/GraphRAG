### **Why GraphRAG over Naive RAG?**

**Struggles with Information Scattered Across Different Sources**. Traditional Retrieval-Augmented Generation (RAG) faces challenges when it comes to synthesizing information scattered across multiple sources. It struggles to identify and combine insights linked by subtle or indirect relationships, making it less effective for questions requiring interconnected reasoning. 

**Lacks in Capturing Broader Context.** Traditional RAG methods often fall short in capturing the broader context or summarizing complex datasets. This limitation stems from a lack of deeper semantic understanding needed to extract overarching themes or accurately distill key points from intricate documents. When we execute a query like "What are the main themes in the dataset?", it becomes difficult for traditional RAG to identify relevant text chunks unless the dataset explicitly defines those themes. In essence, this is a query-focused summarization task rather than an explicit retrieval task in which the traditional RAG struggles with.

### **How does Microsoft’s GraphRAG work?**

GraphRAG extends the capabilities of traditional Retrieval-Augmented Generation (RAG) by incorporating a two-phase operational design: an indexing phase and a querying phase. During the indexing phase, it constructs a knowledge graph, hierarchically organizing the extracted information. In the querying phase, it leverages this structured representation to deliver highly contextual and precise responses to user queries.

**Indexing Phase**

Indexing phase comprises of the following steps - 

1. We start with splitting the input texts into manageable chunks for processing
2. Entities and relationships are then extracted across the different chunks
3. Post this, the entities and  relationships are summarized into a structured format from which a knowledge graph is constructed. The nodes of the knowledge graph represent entities and edges represent their relationships. 
4. Post the knowledge graph generation, communities are identified using an algorithm like the [Leiden algorithm](https://en.wikipedia.org/wiki/Leiden_algorithm) by identification of the closely related entities leading to the formation of a hierarchical community structure.
5. Summaries in GraphRAG are generated for each community, starting at the bottomest level. It begins by summarizing individual entities and their relationships within smaller communities and then advances hierarchically. As it progresses, higher-level summaries are created for larger, aggregated communities, forming an interconnected, multi-layered depiction of the data.

**Querying Phase**

Equipped with a knowledge graph and detailed community summaries, GraphRAG can then respond to user queries with good accuracy leveraging the different steps present in the Querying phase.

**Global Search -** For inquiries that demand a broad analysis of the dataset, such as “What are the main themes discussed?”, GraphRAG utilizes the ***compiled community summaries***. This approach enables the system to integrate insights across the dataset, delivering thorough and well-rounded answers.

**Local Search -** For queries targeting a specific entity, GraphRAG leverages the interconnected structure of the knowledge graph. By navigating the entity’s immediate connections and examining related claims, it gathers pertinent details, enabling the system to deliver accurate and context-sensitive responses.
