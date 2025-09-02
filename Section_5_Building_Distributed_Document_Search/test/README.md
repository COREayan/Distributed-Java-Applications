## Section 5 : Building Distributed Document Search

### Distributed Search - Inputs
- We have a large number documents
    - Books
    - Academic Articles
    - Legal Documents
    - Websites
- Search Query from the user

### Distributed Search - Output
- Most Relevant documents to the user's search.

### Search Algorithms - Attempt 1
- Word Count of the search terms
    - For every document, count how many times each search term appears in the document.
    - The documents with the highest count are the most relevant!
    - The document with the lowest count are going to rank lower.
- search query = [term1, term2, term3]
- term1_count + term2_count + term3_count
- score(document) = term1_count + term2_count + term3_count
- sort(documents, by score) -> list of relevant documents in a descending order.
- Problem - The algorithms favors larger documents.
- Search Term : "car"

### search Algorithm - Attempt 2
- score(doc1) = tf(term1, doc1) + tf(term2, doc1) + tf(term2, doc1)
  
### TF-IDF Algorithm
- Term Frequency - Inverse Document Frequency(tf-idf)
- Measures how much information each term in the search query provedes us. 
- Common terms that appear in many documents do not provide us any value, and get lower weight.
- Terms that are more rare across all documents, get higher weight.
 idf(term) = log(N / nt)
    N - Number of documents
    nt - Number of documents containing the term

Notes on TF-IDF
- TF-IDF is a statistical algorithm and requires a large enough set of documents to give good results.
- Search Term : "car"
- The algorithm works well with high number of documents and is highly parallelizable.
- Perfect fit for building a distributed system.

Term Frequency - Inverse Document Frequency
 tf("term1", doc_i) = term1_count/words_count
 idf("term1") = log(N/nt)
    N - Number of documents
    nt - Number of documents containing the term

Parallelizing TF-IDF
- Problems Dimensions
    - D - Number of documents
    - T - Number of Search Terms
- Decide on which dimension we want to parallelize the algorithm

### Deciding how to Parallelize the workload
- The decision on how to parallelize the algorithm is critical to make the algorithm scalable.
- We need to choose the dimension on which the input to our system is expected to grow the most.
- If/When the data does grow, then we can simply add more machines to the cluster, and the system will easily scale.

### Choosing the Dimension for Data Partitioning
- Do we expect the number of terms in the query to grow significantly?
    - No!
- Do we expect the number of documents to grow over time?
  - Yes!
- Then we choose to parallelize the TF-IDF algorithm by the documents
- This is an engineering problem!

### Aggregation - by the Leader
- Calculate all the idf for all the terms (easy to derive from the term frequencies)
- Score the documents
- Sort the document by relevance

### Worker-Node's Components
- Service Registry 
  - Registration
- Document Storage
  - Reading documents from the File System
- Communication with the Search Coordinator
  - Data Model (Task, Result)
- Calculation of the Term Frequencies for all the search terms in the allocated documents
  - Using the TF-IDF algorithm
- 