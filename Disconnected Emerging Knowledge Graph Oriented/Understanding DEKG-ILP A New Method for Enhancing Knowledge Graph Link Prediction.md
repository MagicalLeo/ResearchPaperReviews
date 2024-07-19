### Understanding DEKG-ILP: A New Method for Enhancing Knowledge Graph Link Prediction

## Background

A Knowledge Graph (KG) is a structured representation of data through nodes (entities) and edges (relationships). Common knowledge graphs include Freebase, NELL, and DBpedia. They play a crucial role in applications such as information retrieval, recommendation systems, and question answering. An essential task in knowledge graphs is link prediction, which aims to predict missing links in the graph. This task has seen significant success, primarily due to recent advancements in knowledge graph embedding methods.

However, knowledge graphs are not static; they evolve dynamically. For instance, DBpedia saw around 200 new entities emerging daily from late 2015 to early 2016. Traditional embedding methods are inefficient in handling these new entities because they are unseen during training. Although retraining the entire graph can address this issue, it is time-consuming and computationally expensive in real-world applications. Therefore, Inductive Link Prediction (ILP) has become an important research direction, aiming to predict links for new entities in emerging knowledge graphs.

## Why is the DEKG-ILP Model Needed?

Existing methods mainly focus on predicting enclosing links within new knowledge graphs. However, in many real-world applications, there are missing bridging links between new and original graphs that carry crucial evolutionary information. For example, in predicting drug interactions, bridging links may contain vital information. Current methods, such as Grail and TACT, fail to effectively predict bridging links in Disconnected Emerging Knowledge Graphs (DEKGs). The DEKG-ILP model was proposed to fill this gap.

![圖片](Disconnected Emerging Knowledge Graph Oriented.assets/圖片.png)

The image above illustrates an example of a DEKG and an original KG, explaining the concepts of bridging and enclosing links. The dashed lines indicate missing links.

## Main Functions and Goals of the DEKG-ILP Model

The DEKG-ILP model aims to predict missing links in DEKGs, including both enclosing and bridging links. The model consists of two main modules:

1. **CLRM (Contrastive Learning-based Relation-specific Feature Modeling)**

   Extracts global, relation-based semantic features shared between original KGs and DEKGs.

2. **GSM (GNN-based Subgraph Modeling)**

   Extracts local topological information around each link.

## Implementation of the DEKG-ILP Model

The diagram below shows the architecture of the DEKG-ILP model, including the workflows of the CLRM and GSM modules.

![Diagram](Disconnected%20Emerging%20Knowledge%20Graph%20Oriented.assets/图片-1721387643544-2.png)

1. **CLRM Module**

   - **Relation-specific Feature Modeling**: Extracts and represents the semantic features of each relation, combining them to represent entities.
   - **Contrastive Learning**: Optimizes relation-specific features by generating positive and negative samples.

2. **GSM Module**

   - **Subgraph Extraction**: Extracts subgraphs around target links. Single subgraphs are used for enclosing links, while two disconnected subgraphs are used for bridging links.
   - **Node Labeling**: Labels each node in the subgraph based on their distance to the head and tail entities of the target link.
   - **GNN (R-GCN)**: Processes the subgraphs using relational graph convolutional networks to extract topological features.

3. **Comprehensive Scoring**

   Combines the semantic score from CLRM and the topological score from GSM to derive the final score for the target link.

## Experimental Results

Experiments on multiple benchmark datasets (e.g., FB15k-237, NELL-995, and WN18RR) show that the DEKG-ILP model significantly outperforms existing methods in predicting both enclosing and bridging links. Notably, DEKG-ILP exhibits substantial improvements in bridging link prediction, demonstrating its effectiveness in handling DEKGs.

The image below compares the performance of the DEKG-ILP model with other baseline models across three datasets.

![Diagram](Disconnected%20Emerging%20Knowledge%20Graph%20Oriented.assets/图片-1721387697034-4.png)

Here are some explanations for the contents of the figure:

### Datasets

- **FB15k-237**
- **NELL-995**
- **WN18RR**

### Models

- **TransE**: An embedding method based on translation.
- **RotatE**: An embedding method modeling rotation in complex space.
- **ConvE**: An embedding method based on convolutional neural networks.
- **GEN**: A method based on graph neural networks.
- **RuleN**: A method based on rule mining.
- **Grail**: A subgraph reasoning method specifically designed for DEKGs.
- **TACT**: A subgraph reasoning method focused on relation prediction.
- **DEKG-ILP**: The newly proposed model in this paper.

### Evaluation Metrics

- **MRR (Mean Reciprocal Rank)**
- **Hits@1**
- **Hits@5**
- **Hits@10**

## Future Research Directions and Impact

1. **Further Model Optimization**: Explore more effective contrastive learning strategies or more powerful graph neural network structures.
2. **Application Expansion**: Apply DEKG-ILP to more real-world scenarios, such as predicting drug interactions in medical knowledge graphs.
3. **Cross-Graph Applications**: Study how to predict links between knowledge graphs in different domains to enhance cross-domain knowledge integration and utilization.

The DEKG-ILP model not only addresses the limitations of existing methods but also provides an effective approach to handling complex and dynamically evolving knowledge graphs. It holds broad application prospects and research value.

## Conclusion

The DEKG-ILP model combines global and local information to effectively predict missing bridging and enclosing links in knowledge graphs, thereby enhancing the completeness and reasoning capability of knowledge graphs. This model stands out among existing methods and offers new ideas and directions for future knowledge graph research and applications.

[Paper Link](https://www.computer.org/csdl/proceedings-article/icde/2023/222700a381/1PByD9gXXKE)