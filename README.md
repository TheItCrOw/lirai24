<div align="center">
  <h1><b>Finding Needles in Emb(a)dding Haystacks: Legal Document Retrieval via Bagging and SVR Ensembles</b></h1>
  <h3><a href="https://sites.google.com/view/LIRAI-2024">LIRAI'24:The Second Workshop on Legal Information Retrieval meets Artificial Intelligence</a></h3>
  <hr/>
</div>

<i>We introduce a retrieval approach leveraging Support Vector Regression (SVR) ensembles, bootstrap aggregation (bagging), and embedding spaces on the [German Dataset for Legal Information Retrieval (GerDaLIR)](https://github.com/lavis-nlp/GerDaLIR). By conceptualizing the retrieval task in terms of multiple binary needle-in-a-haystack subtasks, we show improved recall over the baselines (**0.849** > 0.803 | 0.829) using our voting ensemble. Our findings demonstrate improvement over two baselines, suggesting promising initial results. Our approach holds potential for further enhancement, particularly through refining the encoding models and optimizing hyperparameters.</i>
<hr/>
<div>
  <a href="https://www.texttechnologylab.org/"> <img src="https://img.shields.io/static/v1?label=&message=Text+Technology+Lab&color=blueviolet&style=for-the-badge&logo=internetarchive" alt="TTLab"></a>
  <a href=""> <img src="https://img.shields.io/static/v1?label=Paper%3A&message=In+Proceedings&color=important&style=for-the-badge&logo=researchgate" alt="Paper: - In Proceedings"></a>
  <br/>
</div>

## About

![architecture (1)](https://github.com/TheItCrOw/lirai24/assets/49918134/c43459f2-e481-4cb2-8e56-0ac28aa81670)

Modeling the complete flow of the needle-in-a-haystack training, we begin by partitioning the collection space into several subsets (bagging), with each subset being assigned a SVR model for training. For each query in a subset, we identify the top 𝑘 nearest passages through their vector spaces and concatenate their embeddings into a single feature embedding. Consequently, each query is associated with 𝑘 − 1 negative labels and one positive label. The SVR model is trained to find this single positive label within the haystack. This process is repeated for each subset and query. During prediction, each model in the group predicts a match for its respective subset. If only one model recognizes a positive match, the corresponding section is marked as relevant and output.

## Results

| **Method**                  | **Mode** | **MRR@10** | **nDCG@20** | **Recall@100** | **Recall@1000** |
|-----------------------------|----------|------------|-------------|----------------|-----------------|
| **TF-IDF**                  | P        | 0.333      | 0.375       | 0.651          | 0.768           |
|                             | D        | 0.336      | 0.386       | 0.701          | 0.809           |
| **BM25 (k1=1.20, b=0.75)**  | P        | 0.365      | 0.409       | 0.693          | 0.800           |
|                             | D        | 0.386      | 0.434       | 0.734          | 0.827           |
| **BM25 tuned (k1=0.51, b=0.72)**  | P        | 0.372      | 0.417       | 0.703          | **0.803**       |
| **BM25 tuned (k1=0.90, b=0.98)**  | D        | 0.391      | 0.439       | 0.737          | **0.829**       |
| **WCS - GloVe**             | P        | 0.242      | 0.278       | 0.539          | 0.695           |
|                             | D        | 0.134      | 0.166       | 0.420          | 0.625           |
| **WCS - fastText**          | P        | 0.257      | 0.295       | 0.582          | 0.726           |
|                             | D        | 0.153      | 0.188       | 0.468          | 0.668           |
| **Neural Re-ranking - BERT**| P        | 0.416      | 0.465       | **0.745**      | 0.789           |
| **Neural Re-ranking - ELECTRA** | P    | **0.436**  | **0.481**   | **0.743**      | 0.789           |

**Our Ensemble:**

| **Method**       | **Mode** | **Recall** |
|------------------|----------|------------|
| **SVR Ensemble** | P        | **0.849**  |

*The baseline measures of the GerDaLIR dataset are compared to our preliminary LIR technique. In this context, Mode P and D refer to passage-wise and document-wise retrieval, respectively. Metrics such as MRR and nDCG have not yet been evaluated on our ensemble. The original authors utilized Recall@100 and Recall@1000 for re-ranking, a restriction that we do not impose. The results indicate that our preliminary ensemble surpasses all baseline measures.*

## Contact

For model weights, please contact the corresponding author listed in the [paper](#).

