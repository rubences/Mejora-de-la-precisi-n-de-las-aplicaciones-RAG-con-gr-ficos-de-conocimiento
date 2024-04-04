# Enhancing the Accuracy of RAG Applications With Knowledge Graphs

**A practical guide to constructing and retrieving information from knowledge graphs in RAG applications with Neo4j and LangChain**

*Tomaz Bratanic*  
Neo4j Developer Blog

---

**Published in** Neo4j Developer Blog  
**8 min read**  
**5 days ago**  
285 views

---

![Image created by DALL-E.](#)

Graph retrieval-augmented generation (GraphRAG) is gaining momentum and becoming a powerful addition to traditional vector search retrieval methods. This approach leverages the structured nature of graph databases, which organize data as nodes and relationships, to enhance the depth and contextuality of retrieved information.

### Example of a knowledge graph.

Graphs are great at representing and storing heterogeneous and interconnected information in a structured manner, effortlessly capturing complex relationships and attributes across diverse data types. In contrast, vector databases often struggle with such structured information, as their strength lies in handling unstructured data through high-dimensional vectors. In your RAG application, you can combine structured graph data with vector search through unstructured text to achieve the best of both worlds. That’s what we will demonstrate in this blog post.

## Knowledge Graphs Are Great, But How Do You Create One?

Constructing a knowledge graph is typically the most challenging step. It involves gathering and structuring the data, which requires a deep understanding of both the domain and graph modeling.

To simplify this process, we have been experimenting with LLMs. With their profound understanding of language and context, LLMs can automate significant parts of the knowledge graph creation process. By analyzing text data, these models can identify entities, understand their relationships, and suggest how they might be best represented in a graph structure.

As a result of these experiments, we have added the first version of the graph construction module to LangChain, which we will demonstrate in this blog post.

The code is available on GitHub.

### Neo4j Environment Setup

You need to set up a Neo4j instance. Follow along with the examples in this blog post. The easiest way is to start a free instance on Neo4j Aura, which offers cloud instances of Neo4j database. Alternatively, you can also set up a local instance of the Neo4j database by downloading the Neo4j Desktop application and creating a local database instance.

```python
os.environ["OPENAI_API_KEY"] = "sk-"
os.environ["NEO4J_URI"] = "bolt://localhost:7687"
os.environ["NEO4J_USERNAME"] = "neo4j"
os.environ["NEO4J_PASSWORD"] = "password"

graph = Neo4jGraph()
