# Paper Review: Efficient Maximum k-Plex Computation over Large Sparse Graphs

## Introduction

Graph models are widely applied in data analysis fields such as social media, communication networks, collaboration networks, web graphs, and the internet because they naturally capture relationships between entities. The graph data in these applications are typically globally sparse but locally dense. Identifying locally dense subgraphs is important in many applications, such as identifying large-scale community structures in social networks to understand interaction patterns within the network.

A classic concept of dense subgraphs is the clique, which requires that every pair of vertices has an edge between them. However, the concept of a clique is too strict, and large tightly connected communities in real networks rarely manifest as cliques. Therefore, various relaxed clique models have been proposed in the literature, such as the k-plex. A k-plex allows each vertex to miss up to k neighbors. The problem of computing the maximum k-plex and enumerating the maximum k-plex has recently gained increasing attention. However, existing algorithms still have limitations in efficiency, especially when dealing with large sparse graphs.

### Major Contributions

1. **New Framework**: A new framework is designed for computing the maximum k-plex on large sparse graphs by iteratively extracting small dense subgraphs from the graph and solving the problem for each extracted subgraph using a branch-and-bound search.
2. **CTCP Algorithm**: An efficient graph reduction algorithm, CTCP, is proposed to reduce the size of the input graph by pruning vertices and edges. CTCP computes a reduced graph with lower time complexity than existing techniques.
3. **BBMatrix Algorithm**: A new branch-and-bound algorithm, BBMatrix, is developed for the dense subgraphs extracted from the input graph. It uses an adjacency matrix representation of its input graph and utilizes first-order and second-order information for pruning and upper bound estimation.

### Framework Details

- **Framework Description**: The framework is divided into two parts:
  1. **Part One**: Compute an initial larger k-plex and reduce the graph using CTCP. CTCP reduces the graph to its (lb + 1 - k)-core and (lb + 1 - 2k)-truss by removing vertices with degrees less than lb + 1 - k and edges participating in fewer than lb + 1 - 2k triangles.
  2. **Part Two**: Iteratively extract small dense subgraphs from the graph and compute the maximum k-plex containing a specified vertex using BBMatrix.

## kPlexS Algorithm Details

kPlexS is a new algorithm designed for the maximum k-plex computation problem. This algorithm efficiently computes the maximum k-plex on large sparse graphs by combining the core techniques of CTCP and BBMatrix.

#### 1. CTCP Algorithm

CTCP (Core-Truss Co-Pruning) is a graph reduction algorithm aimed at reducing the size of the input graph through the following two steps:
- **Core Pruning**: Remove all vertices with a degree less than lb + 1 - k, reducing the graph to its (lb + 1 - k)-core.
- **Truss Pruning**: Remove all edges participating in fewer than lb + 1 - 2k triangles, reducing the graph to its (lb + 1 - 2k)-truss.

The time complexity of CTCP is O(δ(G) × |E|), where δ(G) is the degeneracy of the graph. CTCP is used not only in the preprocessing step but also iteratively called after each vertex removal to further reduce the graph's size.

#### 2. BBMatrix Algorithm

BBMatrix is a branch-and-bound algorithm specifically designed for the dense subgraphs extracted from the input graph. It uses an adjacency matrix to represent its input graph and utilizes first-order and second-order information for pruning and upper bound estimation. The core techniques of BBMatrix include:

- **Adjacency Matrix Representation**: BBMatrix uses an adjacency matrix to represent its input graph, making it more efficient to incrementally maintain first-order and second-order information.
- **Branching and Pruning Rules**: BBMatrix optimizes the branch-and-bound search process using a set of branching and pruning rules. It leverages first-order and second-order information for upper bound estimation and pruning, enhancing the algorithm's efficiency.
- **Incremental Calculation Techniques**: During the recursive process, BBMatrix employs incremental techniques to efficiently apply upper bound estimations and pruning.

![BBMatrix Algorithm Flow](Paper Review - Efficient Maximum k-Plex Computation over Large Sparse Graphs.assets/image-20240729161621400.png)

The above image illustrates the flow of the BBSearch algorithm, primarily used to compute the maximum k-plex in a graph. The process is as follows:
1. **Start**: Begin with a BBSearch instance (g, k, S, lb), where g is the graph, k is the allowed maximum number of missing neighbors, S is the current partial solution, and lb is the lower bound.
2. **Select Vertex**: Choose a branching vertex u through the branching rules (BR1 and BR2).
3. **Include Vertex u**:
   - Add vertex u to the partial solution S.
   - Apply reduction rules (RR1-RR5) to simplify the instance.
   - Compute the upper bound of the instance (UB1 and UB2). If not pruned, recursively process the new instance.
4. **Exclude Vertex u**:
   - Exclude vertex u from the graph g and the partial solution S.
   - Apply reduction rules (RR1-RR5) to simplify the instance.
   - Compute the upper bound of the instance (UB1 and UB2). If not pruned, recursively process the new instance.

This demonstrates how to recursively select vertices and use reduction rules to compute the maximum k-plex.

### Experimental Results

- **Experimental Setup**: Extensive experiments were conducted on two benchmark graph sets. The results show that the kPlexS algorithm consistently solves more graph instances within the given time limits compared to state-of-the-art algorithms (BnB, Maplex, and KpLeX).

![Experimental Results](Paper Review - Efficient Maximum k-Plex Computation over Large Sparse Graphs.assets/image-20240729162415414.png)

The image above compares the number of instances solved by six algorithms (kPlexS, kPlexF, KpLeX, BnB-ct, Maplex, BnB) on real graph sets. The results show that kPlexS and kPlexF consistently solve the most instances within different time limits, with kPlexS solving more instances within 50 seconds than other algorithms do within 1800 seconds. The superiority of kPlexS comes from its application of second-order techniques in dense subgraph extraction and branch-and-bound search.

![Preprocessing Results](Paper Review - Efficient Maximum k-Plex Computation over Large Sparse Graphs.assets/image-20240729162850707.png)

The table above presents the preprocessing results of four algorithms (kPlexS, KpLeX, Maplex, BnB) on 22 real graphs for k = 5. The data include preprocessing time, the k-plex size computed heuristically (P), and the number of vertices (|Vₖ|) and edges (Eₖ) in the reduced graph. The results show that kPlexS has the fastest preprocessing time on most graphs and significantly reduces the number of vertices and edges in the simplified graph. KpLeX's preprocessing time is comparable to kPlexS, but its performance is slightly lower on some graphs. Maplex and BnB have relatively longer preprocessing times, especially BnB on some graphs.

## Conclusion

This paper proposes a new algorithm, kPlexS, which significantly improves the efficiency of computing the maximum k-plex on large sparse graphs by introducing new frameworks and techniques. Combining the core technologies of CTCP and BBMatrix, kPlexS demonstrates significant performance advantages in experiments and holds substantial practical value in various application domains. Future research can further optimize and extend this algorithm for dynamic graphs, distributed computing, and heterogeneous graphs. Additionally, kPlexS can be widely applied in social network analysis, bioinformatics, communication network optimization, e-commerce and recommendation systems, knowledge graph construction, financial risk management, and cybersecurity. For example, in social network analysis, it can help identify communities and assess influence; in bioinformatics, it can identify functional modules and gene regulatory mechanisms; and in communication networks, it can optimize network topology and traffic management. These applications showcase kPlexS's potential and broad application prospects in handling large-scale graph data.