# Latent Semantic Analysis

## Introduction:

An information retrieval technique patented in 1988. In the context of its application to information retrieval, it is sometimes called Latent Semantic Indexing (LSI).

 LSI allows a search engine to determine what a page is about outside of specifically matching search query text. It looks at  “Themes” instead of “Keywords”.

Linear Algebra techniques used in the project: Singular Value Decomposition, Cosine Similarity, Matrix properties.

### Dataset: 

“Sci.space” news group from 20 news groups dataset, available in the Scikit-Learn library. It contains 400 news articles related to space. 


## SVD (Singular Value Decomposition):

SVD is a matrix decomposition algorithm, it decomposes a matrix into 3 matrices which are a set to transformations. Decomposition leads to an orthogonal matrix U, Diagonal matrix S and a Diagonal Matrix V. This is the best possible transformation of a matrix.
In this decomposition method we are looking for a set of orthonormal basis in the row space that when multiplied by the original matrix goes to an orthonormal basis in the column space.  
Av1 = σ1u1 
Av2 = σ2u2 

These look similar to the eigen vector equation, except that the transformation takes the original vector to another space.
SVD decomposes the original matrix into a rotation followed by a stretching and a rotation. It factorizes the original matrix (A) into 3 separate transformations.
Null space vectors in row space have corresponding 0s in the singular matrix, hence mapping them to 0s. 
A= U*S*VT
A, AT, AT*A, A*AT have the same rank. Columns of A span the image of A*AT and rows of A span the image of AT*A. Therefore, columns of A lie in the space of u’s and rows of A lie in the space spanned by v’s. 
When we apply the transformation A on any vector, we are essentially multiplying it with V and taking it to the row space, stretching it using the singular matrix and taking it to the column space by multiplying it with the U matrix.
Singular Value Decomposition has two interesting properties. First, it exists for any and all matrices: large, small, square, rectangular, singular, non-singular, sparse and dense. So, no matter what kind of term by document matrix, we know it has a singular value decomposition.
The next helpful property is the optimality property. This property basically tells us that, if we would like to find a rank-k approximation of our matrix, the best one can be found using singular value decomposition. 
U matrix is computed by arranging the eigen vectors of A*AT column wise from left to right in the increasing order of the magnitude of eigen values. V matrix is computed by arranging the eigen vectors of AT*A column wise from left to right in the increasing order of the magnitude of eigen values. Singular matrix is obtained by taking square root of the eigen values of A*AT or AT*A and arranging them in decreasing order. 
SVD can be computed using QR decomposition or Power method also.  
For matrix A with rank r. A full rank decomposition of A is usually denoted like this: . We can find a reduced rank approximation (or truncated SVD) to A by setting all but the first k largest singular values equal to zero and using only the first k columns of U and V. 

The K value is selected by taking the Frobenius norm of the the difference of original and reconstructed matrix divided by the norm of the original matrix. This will tell us how much the reconstructed tf-idf matrix will differ from the original matrix. We want a K value for which the change is not more than 40%.  This step will give a good estimate of the original matrix which is not sparse as the original matrix. Dense matrix will help us better in finding similarities between documents or between documents and a query.


This value should be not more than 0.4 for our K.

We multiply the Query with the reconstructed matrix to get a vector of size n. Where n is the number of documents we have in the corpus. This resultant vector contains the scores of each document with respect to each document. We sort this list in descending order to get the relevance ranking of the documents for the given query.

SVD on Text data (Interpretation):

Interpretation of S:
The matrix S is always a diagonal matrix with non-negative descending values, known as the singular values.
Each non zero value represents concepts. There can't be more concepts than there are documents. The magnitude of the values describes how much variance each feature describes in the data.
Interpretation of V
V describes the relationship between concepts and documents. It is a set of column vectors and each eigen vector describes a concept. Components of each vector represent the weightage/contribution that each document has, in describing that particular concept.
The matrix product VS describes the relation between documents (VS's rows) and the features (VS's columns)
plotting the documents in the most important concept space, concept1 vs concept2, we can see the expected separation of documents from each other. I also plotted a 3d plot, considering top 3 concepts.
Interpretation of U
U describes the relationship between concepts and words. It is a set of column vectors and each eigen vector describes a concept. Components of each vector represent the weightage/contribution that each word has, in describing that particular concept.
The matrix product US describes the relation between terms (US's rows) and the features (US's columns). As plotting all the words on a 2d plane is not intuitive, I did not do this plot.
Statistical analysis:
1)	 Document importance based on how many unique words it contains:




This also gives an approximation of the length of the documents.

2)	 Distribution of word count in all the documents:

Words mostly occurs 1-5 times in the corpus and very few words occur 10-15 times.

3)	Most popular words based on occurrence:
(Word, word count)
  [('space', 36),
 ('astronaut', 28),
 ('nasa', 26),
 ('would', 21),
 ('mission', 19),
 ('one', 18),
 ('flight', 16),
 ('april', 14),
 ('candidates', 14),
 ('military', 14),
 ('system', 14),
 ('time', 14),
 ('aviation', 13),
 ('spacecraft', 13),
 ('also', 12),
 ('get', 12),
 ('pilot', 12),
 ('program', 12),
 ('shuttle', 12),
 ('cost', 11),
 ('must', 11),
 ('science', 11),
 ('test', 11),
 ('think', 11),
 ('applicants', 10),
 ('data', 10),
 ('degree', 10),
 ('earth', 10),
 ('may', 10),
 ('selection', 10),
 ('applications', 9),
 ('civilian', 9),
 ('degrees', 9),
 ('experience', 9),
 ('first', 9),
 ('launch', 9),
 ('like', 9),
 ('need', 9),
 ('new', 9),
 ('physical', 9),
 ('see', 9),
 ('support', 9),
 ('years', 9),
 ('astronauts', 8),
 ('candidate', 8),
 ('could', 8),
 ('know', 8),
 ('low', 8),
 ('moscow', 8),

4)	Words that are important based on the tf-idf score.
These are the unique words that determine a doc’s     relevance. 

   [('moments', 0.9027294781610561),
 ('srinivas', 0.9027294781610561),
 ('surreal', 0.9027294781610561),
 ('thanks', 0.8439370341410448),
 ('recent', 0.515845416092032),
 ('allen', 0.4606580952864572),
 ('could', 0.38914460243040633),
 ('rather', 0.3825521626510499),
 ('space', 0.3771718187517582),
 ('article', 0.37514195126797867),
 ('able', 0.3610917912644225),
 ('accept', 0.3610917912644225),
 ('donations', 0.3610917912644225),
 ('nonprofit', 0.3610917912644225),
 ('organisation', 0.3610917912644225),
 ('transferring', 0.3610917912644225),
 ('think', 0.34418138441413415),
 ('one', 0.34316988417885463),
 ('closer', 0.33310701803922),
 ('brains', 0.32826526478583856),
 ('pants', 0.32826526478583856),
 ('pointy', 0.32826526478583856),
 ('reusable', 0.32826526478583856),
 ('stick', 0.32826526478583856),
 ('tool', 0.32826526478583856),
 ('first', 0.3253718950963527),
 ('find', 0.32461844736676126),
 ('cost', 0.32448984966623934),
 ('would', 0.32366359354255514),
 ('operational', 0.3201385333730229),
 ('timer', 0.3155082153896841),
 ('lines', 0.30950724965521925),
 ('response', 0.30950724965521925),
 ('zillion', 0.30950724965521925),
 ('craft', 0.2999730584109118),

These words have high importance in the document. A corpus can contain a word that occurs in almost all the documents, but that is not considered important. As it does not help us in distinguishing the documents from one another. Instead low occurring words that describe the theme of the document are given a higher weightage.


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

I got this result because I ordered the documents based on the score that each document obtains when the query is multiplied with the reconstructed matrix. 



### 2)	Plot documents in 2d


This plot shows the separation of documents in 2d 
Concept 1 is the most important concept
Concept 2 is the second most important concept

I got this 2d plot base on the weights that are assigned to each document in the top 2 resultant vectors (corresponding to top 2 concepts), when V matrix is multiplied with the singular matric S. 


3)	Plot documents in 3d

This plot shows the separation of documents in 3d 
Concept 1 is the most important concept
Concept 2 is the second most important concept
Concept 3 is the third most important concept.

I got this 2d plot base on the weights that are assigned to each document in the top 3 resultant vectors (corresponding to top 3 concepts), when V matrix is multiplied with the singular matric S. 


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

 I got this result using the eigen vectors in U matrix that are arranged in the order of importance from left to right. The left most eigen vector represents the top most concept. This eigen vector is composed of components that are the weights for the words. These weights can be sorted in descending order and printed for each 
concept.

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




I got this result using the eigen vectors in V matrix that are arranged in the order of importance from left to right. The left most eigen vector represents the top most concept. This eigen vector is composed of components that are the weights for the documents. These weights can be sorted in descending order and printed for each 
concept.


Other approaches:
1.	Other algorithms like QR decomposition or Power method can be used to compute the SVD. 

2.	Using a better metric like Local weight functions and global weight functions is considered an improvement to the tf-idf score. 

3.	Regularized latent semantic models take care of sparsity in the tf-idf matrix and also provides better scalability. Scalability is an issue in LSI.

4.	Probabilistic Latent Semantic Indexing is a way to improve LSI by considering the probability of the word occurrences into account.

Bibliography:
https://www.computer.org/csdl/proceedings/hicss/2010/3869/00/03-04-04.pdf
http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.97.4344&rep=rep1&type=pdf
http://theory.stanford.edu/~tim/s16/l/l9.pdf
http://www.math.umn.edu/~lerman/math5467/svd.pdf

