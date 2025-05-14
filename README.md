### 👗 Graph Neural Networks for Fashion Product Recommendations

**1. Introduction**
Fashion discovery on platforms like Pinterest thrives on recommendation systems that help users find relevant products based on visual and contextual cues.
In this project, we build a Graph Neural Network (GNN) that learns product relationships and generates meaningful recommendations.


🎯 Goal: Explore and develop a recommendation system that suggests similar fashion products based on learned embeddings.

**2. Data**
The dataset used in this project is based on the Pinterest Fashion Data, which includes product metadata, images, and scene-product relationships.

**Citation:**

Wang-Cheng Kang, Eric Kim, Jure Leskovec, Charles Rosenberg, Julian McAuley (2019).
Complete the Look: Scene-based Complementary Product Recommendation.
In Proceedings of CVPR 2019.

**2.1 Files Used**
fashion.json – Contains product-to-scene mappings.

fashion-cat.json – Contains product category labels (multi-label).

**2.2 Data Description**
| **Feature**      | **Description**                                                       |
|------------------|------------------------------------------------------------------------|
| **Product ID**   | Unique identifier for each fashion product                            |
| **Scene ID**     | Unique identifier for scenes containing multiple products             |
| **Bounding Box** | (x, y, w, h) coordinates for product location in scene images         |
| **Category**     | Multi-label category for each product (e.g., "Shoes \| Sneakers")     |
| **Image URL**    | Direct URL to product images                                          |

**2.3 Data Processing**
Removed the broad category "Apparel & Accessories" to improve distinctiveness.

Extracted scene-product relationships to build the graph.

Normalized product embeddings.

One-hot encoded product categories.

**3. Feature Engineering**

**3.1 Node Features**
- Category Vector: One-hot encoding of product categories.

**3.2 Graph Edges**
| **Edge Type**                                    | **Description**                                              |
|--------------------------------------------------|--------------------------------------------------------------|
| **Product ↔ Scene**                              | Links a product to the scenes it appears in.                |
| **Product ↔ Product (Category Similarity)**      | Connects products that share the same category.             |
| **Product ↔ Product (Object Similarity)**        | Links products with similar detected objects.               |
| **Scene ↔ Scene**                                | Connects scenes with overlapping products.                  |

**3.3 Graph Stats**
- Total Nodes: 67,549 (Products + Scenes)
- Total Edges: 72,198 (All relationship types)


**4. Exploratory Data Analysis (EDA)**
- Plotted product category distribution.
- Visualized scene-product co-occurrence.
- Analyzed bounding box coverage for localization accuracy.
- Applied PCA and t-SNE to explore product embedding space.

**🔍 Key Findings**
- Product categories were imbalanced, a few categories dominated.
- Category-based edges led to over-similarity in embeddings.
- Scene-based edges introduced better diversity.

**5. Modeling & Hyperparameter Tuning**
We trained a Graph Attention Network (GAT) using PyTorch Geometric (PyG).

**5.1 Why GAT?**
Graph Attention Networks dynamically assign weights to neighboring nodes using attention scores, allowing the model to learn the importance of different relationships — helpful in heterogeneous graphs.

**5.2 Model Architecture**
2-layer GAT with residual connections

*Dropout:* 0.3 to reduce overfitting
*Loss Function:* Contrastive Loss to promote meaningful separation

**📉 Contrastive Loss**
Encourages similar products to cluster in embedding space while pushing apart dissimilar products — leading to clearer, structured recommendation boundaries.

**6. Evaluation**
Since this is an unsupervised model, we used custom metrics:

- Loss Curve: Tracked contrastive loss over training
- K-Means + PCA: Verified clustering of similar products
- Cosine Similarity: Measured product alignment
- Top-5 Recommendations: Visually inspected retrievals

**🚨 Observations**
- Cosine similarity scores were too high (~0.999) → Over-smoothing
- Embedding clusters overlapped → Poor class separation
- Scene-based edges added helpful variance

**7. Results & Summary**
- Model successfully learned structure in product-scene relationships.
- Scene edges improved the variety of recommendations.
- K-Means clustering revealed latent structure.

**⚠️ Limitations**
- High cosine similarity (~0.999) suggests over-smoothing
- Some product distinctions were lost
- Final cosine similarity score: 1.9299 → Needs reduction

**8. Future Work**
- Replace GAT with GraphSAGE to reduce over-smoothing
- Switch to Triplet or InfoNCE Loss for more effective separation
- Improve Edge Features using BERT/CLIP-based text/image similarity
- Use Larger Dataset to enhance graph variety
- Integrate YOLO Object Detection for fine-grained image-based edges

**✨ Final Takeaway**
If a user pins a product on Pinterest, our GNN-based model can recommend items that are visually and categorically aligned, with room to improve distinctiveness and control embedding smoothness.


