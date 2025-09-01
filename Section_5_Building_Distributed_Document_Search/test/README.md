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
  
### TF-IDF Algorithm
- Term Frequency - Inverse Document Frequency(tf-idf)
- Measures how much information each term in the search query provedes us. 
- Common terms that appear in many documents do not provide us any value, and get lower weight.
- Terms that are more rare across all documents, get higher weight.
- 