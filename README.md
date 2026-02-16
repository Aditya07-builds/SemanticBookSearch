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


   
