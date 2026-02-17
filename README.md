# SemanticBookSearch

## PROBLEM STATEMENT

Traditional keyword-based search fails to capture semantic intent.

For example, a query like:
“something calm to read at night”
may not contain exact keywords present in book descriptions.

This project builds a semantic search system that retrieves relevant books based on meaning, not exact word matches.

## APPROACH OVERVIEW

The system follows a simple semantic retrieval pipeline:

1. Combine book metadata (title, category, description) into a single text field
2. Encode all book texts using a Sentence Transformer model
3. Encode the user query into the same embedding space
4. Compute cosine similarity between query and book embeddings
5. Return the top-k most similar books
6. An optional query enrichment step is added to improve vague or mood-based queries.(Improves results)

## DATASET

The dataset used in this project is publicly available on Kaggle:

- **Book Description Dataset**
  https://www.kaggle.com/datasets/abdallahwagih/books-dataset

  After removing the non required columns ,the dataset looks like :-
                 
1.  `title`         -   The Title of the book.                                                                                         
2.  `categories`    -   One or more genre/category labels associated with the book (e.g., *Fiction*, *Juvenile Fiction*, *Self-Help*).
3.  `description`   -  A short textual summary or blurb describing the book’s content.

### Dataset Size (before cleaning)

- Total rows: ~6,800 books
- Columns: 3

### Dataset Limitations ###

1. Category labels are noisy and not standardized
2. Descriptions vary significantly in length and quality

## PRE-PROCESSING 

1. Removing unecessary columns
2. Handling Missing and Empty Values
3. Merging Required Columns

## EMBEDDING MODEL

This project uses a Sentence Transformer to encode both books and user queries into dense vector representations that capture semantic meaning.
Cosine similarity is used to retrieve the top-k most relevant books

Traditional preprocessing (stemming, stopword removal) is intentionally avoided, as transformer models perform best on raw natural language.

This approach enables semantic matching beyond keyword overlap, allowing the system to retrieve conceptually related books even when exact terms do not match.
   
## QUERY ENRICHMENT

In addition to raw user queries, the system supports an optional query enrichment step to improve retrieval quality.

There were two choices best suited for this :- 1. Using LLM 2. Using a predefined library

In this project I implemented using predefined library on 100 most common words by humans in normal conversation which can help to map them to particular
mood, pace and theme. We can use LLM in future using api key of an llm model

<img width="872" height="315" alt="Screenshot 2026-02-17 at 8 46 21 AM" src="https://github.com/user-attachments/assets/f5a214cf-ef93-4215-a6aa-2f467171d9e7" />


If the query entered by user contain any keyword ,then it adds mood,tone and pace else it behaves as normal an is embedded into vector for similarity function. For eg:-

<img width="853" height="136" alt="Screenshot 2026-02-17 at 8 49 36 AM" src="https://github.com/user-attachments/assets/f0832092-041e-4835-b643-3c29af67a79b" />

## LIMITATIONS

1. Embeddings are generated on-the-fly, which limits scalability for larger datasets.
2. Retrieval is based solely on cosine similarity without reranking or cross-encoder refinement.
3. Evaluation is primarily qualitative; no quantitative IR metrics (e.g., Precision@K) are reported.
4. Query enrichment is heuristic-based and may not consistently improve results.

## FUTURE WORK

1. Persist precomputed embeddings to disk for faster inference.
2. Compare multiple Sentence Transformer models to evaluate retrieval quality.
3. Introduce reranking using cross-encoders or hybrid retrieval approaches.
4. Add quantitative evaluation using standard information retrieval metrics.
5. Extend the system with a lightweight API or user interface for interactive search.
