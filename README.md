Fashion GNN for Product Recommendations

📌 Project Overview

This project builds a Graph Neural Network (GNN) to generate fashion product recommendations using Pinterest Fashion Data. The model learns meaningful relationships between products and provides recommendations based on embeddings.

✅ Goal: Develop a recommendation system that suggests similar fashion products.
✅ Approach: Construct a graph-based model where nodes represent products and scenes, and edges define relationships like category similarity and scene co-occurrence.
✅ Challenges: Addressed embedding over-smoothing, high similarity issues (~0.999 cosine similarity), and sparse graph connectivity.

📂 Dataset

The dataset consists of:

fashion.json – Defines product-to-scene relationships.

fashion-cat.json – Provides multi-label product category data.

This repository used the Pinterest shop the look data used in the following paper:

Wang-Cheng Kang, Eric Kim, Jure Leskovec, Charles Rosenberg, Julian McAuley (2019). Complete the Look: Scene-based Complementary Product Recommendation. In Proceedings of IEEE Conference on Computer Vision and Pattern Recognition (CVPR'19)