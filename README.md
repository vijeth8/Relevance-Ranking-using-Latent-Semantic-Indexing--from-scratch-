# Latent Semantic Analysis

## Introduction:

An information retrieval technique patented in 1988. In the context of its application to information retrieval, it is sometimes called Latent Semantic Indexing (LSI).

 LSI allows a search engine to determine what a page is about outside of specifically matching search query text. It looks at  “Themes” instead of “Keywords”.

Latent Semantic Indexing uses "Singular Value Decomposition" to do this.

### Dataset: 

“Sci.space” news group from 20 news groups dataset, available in the Scikit-Learn library. It contains 400 news articles related to space. 


## SVD (Singular Value Decomposition):

SVD is a matrix decomposition algorithm, it decomposes a matrix into 3 matrices which are a set to transformations. Decomposition leads to an orthogonal matrix U, Diagonal matrix S and an orthogonal Matrix V. This is the best possible transformation of a matrix.
In this decomposition method we are looking for a set of orthonormal basis in the row space that when multiplied by the original matrix goes to an orthonormal basis in the column space.  
Av1 = σ1u1 
Av2 = σ2u2 

These look similar to the eigen vector equation, except that the transformation takes the original vector to another space.
SVD decomposes the original matrix into a rotation followed by a stretching and a rotation. It factorizes the original matrix (A) into 3 separate transformations.

A= U*S*VT

## SVD on Text data (Interpretation):

### Interpretation of S:
The matrix S is always a diagonal matrix with non-negative descending values, known as the singular values.
Each non zero value represents concepts. There can't be more concepts than there are documents. The magnitude of the values describes how much variance each feature describes in the data.
Interpretation of V
V describes the relationship between concepts and documents. It is a set of column vectors and each eigen vector describes a concept. Components of each vector represent the weightage/contribution that each document has, in describing that particular concept.
The matrix product VS describes the relation between documents (VS's rows) and the features (VS's columns)
plotting the documents in the most important concept space, concept1 vs concept2, we can see the expected separation of documents from each other. I also plotted a 3d plot, considering top 3 concepts.
Interpretation of U
U describes the relationship between concepts and words. It is a set of column vectors and each eigen vector describes a concept. Components of each vector represent the weightage/contribution that each word has, in describing that particular concept.
The matrix product US describes the relation between terms (US's rows) and the features (US's columns). As plotting all the words on a 2d plane is not intuitive, I did not do this plot.


## RESULTS: 
### 1)	Search 

Pass the query into the search function, to get the list of relevant documents:

search ("Sky is high.")

Document-15
Document-2
Document-4
Document-32
Document-14
Document-23
Document-29
Document-21


### 2)	Plot documents in 2d


This plot shows the separation of documents in 2d concept space.
Concept 1 is the most important concept
Concept 2 is the second most important concept

### 3)	Plot documents in 3d

This plot shows the separation of documents in 3d concept space.
Concept 1 is the most important concept
Concept 2 is the second most important concept
Concept 3 is the third most important concept.

### 4)	Printing the most important concepts
 concept 1:
melittin
 
methodology
 
legal
 
lyme
 
foundation
 
references
 
tb
 
science
 
source
 
done
 
concept 2:
melittin
 
affected
 
aid
 
air
 
appeared
 
attacking


### 5)printing the most important documents that represent the top   concepts:

Docs which contain most important concepts 1:
18
 
36
 
Docs which contain most important concepts 2:
18
 
19
 
Docs which contain most important concepts 3:
25
 
27
 
Docs which contain most important concepts 4:
25
 
23
