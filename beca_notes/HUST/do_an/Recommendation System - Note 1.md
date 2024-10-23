> [!note] Terminology
> * **Items**: the recommended entities of a  system.
> * **Query/context**: the information used by system to make recommendations.
> 	* Can be combination of user information (user_id, prev_purchases) and additional context (time_day, device_type..)
> * **Embedding**: a mapping from a discrete set (set of queries, set of items to recommend) to a vector space (called "Embedding space")

![[Recommendation System - Note 1-20241004002958245.webp|539]]

Common architecture of a recommendation system is consists of 3 phases:
* _Candidate Generation_: system starts from an enormous collection of items then generates a much smaller, feasible subset of candidates.
	* A model may provide a set of candidate generators, each nominate a different subset of candidates.
* _Scoring_: model scores and ranks the candidates to choose which set will be displayed to the user. 
	* System can use more precise model relying on additional queries.
* _Re-ranking_: take into account additional constraints for the final ranking.
	* Ex: remove explicitly disliked items, boost fresher content
		-> Ensure diversity, freshness and fairness

## Phase 1: Candidate Generation
```text
Input: queries
Output: set of relevant candidates
```

Two main approaches:
* **Content-based filtering**: use the similarity between items and user preferred ones to recommend them to user.
* **Collaborative filtering**: use similarities between queries and items simultaneously to provide recommendations.

* Embedding space for both approach is a $E=R^d$ embedding space which contains vectors mapping between items an query
	* d << size of corpus
	* same items is usually close together in the embedding space.

Measure of similarity between embeddings is q function:
$$
s: E \times E \rightarrow R
$$
> [!note]
> Given a query embedding $q \in E$, the system finds the item embeddings $x \in E$ that has high similarity $s(q,x)$ (= close to $q$)

![[Recommendation System - Note 1-20241004020013604.webp|398]]

To determine the similarity degree, most of rcm sys uses one or more of:
1. **Cosine**: 
	$$
	s(q,x) = cos(q,x)
	$$
2. **Dot product**: 
	$$
	s(q,x) = ||x|| . ||q||.cos(q,x)
	$$
3. **Euclidean distance**:
	$$
	s(q,x) = ||q-x|| = [\, \sum^d_{i=1}(q_i-x_i)^2 ]\,^{1/2}
	$$
> [!warning]
> Dot product similarity is more sensitive to the **norm** of the embedding.
> Ex: if an item is popular, it tends to be assigned with a large norm -> popular items may dominating the feed.

### 1.1 Content-based filtering (CBF)

### 1.2 Collaborative filtering (CF) and matrix factorization (nhân tố ma trận)

> [!warning] Privacy risks for users personal data
> 1. Data reveals the user's personal interests to the recommenders
> 2. Data may be exploited by the recommenders (purchased by third parties)
> 3. Data may be stolen due to security breaches on the recommender side.

> [!note] References
> * [Recommendation systems overview - Google for Developers](https://developers.google.com/machine-learning/recommendation/overview/types)
> * 