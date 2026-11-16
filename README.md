# DS603_DSA_project Spotify Song Clustering Using Union-Find

## Project Overview

This project explores Spotify song data and groups similar songs using a
graph-based clustering approach built around the Union-Find (Disjoint
Set Union) data structure and a Kruskal-style edge-processing strategy.

The project uses standardised audio features to measure similarity
between tracks, constructs a k-nearest-neighbour graph, and merges
connected components according to selected distance and cluster-size
parameters. The resulting clusters are analysed and visualised to
understand patterns in the dataset.

## Live Website

Website link: [Add the live website URL here]

## Project Objectives

-   Clean and prepare Spotify track data for analysis.
-   Select relevant numerical audio features for similarity measurement.
-   Standardise the selected features so they are comparable.
-   Build a k-nearest-neighbour graph using Euclidean distance.
-   Apply Union-Find to form song clusters through graph connectivity.
-   Evaluate clustering quality and compare the results with K-Means.
-   Visualise the resulting clusters and examine parameter sensitivity.

## Dataset

The project uses a Spotify tracks dataset containing track information,
metadata, and audio features.

The notebook reports the following dataset counts:

-   Raw records: 114,000
-   Records after cleaning: 113,386
-   Unique songs after song-level deduplication: 83,337

The nine audio features used for clustering are:

1.  Danceability
2.  Energy
3.  Acousticness
4.  Instrumentalness
5.  Liveness
6.  Speechiness
7.  Valence
8.  Tempo
9.  Loudness

Track metadata, such as track names, artists, popularity, and genre
information, is retained for interpretation and presentation rather than
used as part of the nine-dimensional distance calculation.

## Methodology

1. Data Cleaning and Preparation

The dataset is checked for duplicate records and missing values.
Repeated track entries are handled at the song level, while relevant
genre information can be retained for interpretation. The selected
numerical audio features are prepared for analysis.

2. Feature Standardisation

The nine audio features are standardised using StandardScaler. This
prevents features with larger numerical scales from dominating Euclidean
distance calculations.

3. Distance Calculation and Nearest Neighbours

Euclidean distance is used to measure similarity between songs in the
standardised nine-dimensional feature space. A k-nearest-neighbour graph
is constructed so that each song is connected to its nearest candidate
neighbours. The graph is made symmetric so that neighbour relationships
can be processed as undirected edges.

4. Union-Find

A Union-Find (Disjoint Set Union) data structure is implemented to
maintain connected components efficiently. The implementation uses path
compression/path halving and union by size to improve operation
efficiency.

5. Kruskal-Style Clustering

Candidate edges are processed in ascending order of distance, following
a Kruskal-style approach. Edges are retained according to the selected
distance threshold, and Union-Find merges the components connected by
those edges, subject to the cluster-size rule used in the notebook.

The size parameter is a merge-control rule, not necessarily a strict
maximum cluster size: a component may grow beyond the parameter when it
absorbs a smaller component.

6. Cluster Selection and Evaluation

Candidate parameter settings are evaluated to select a useful clustering
result. Evaluation includes metrics such as:

-   Silhouette Score
-   Davies-Bouldin Index
-   Normalised Mutual Information (NMI), using genre as a comparison
    label

Small clusters may be attached to larger clusters in a separate
post-processing step. This operation is distinct from the Union-Find
edge-merging process.

7. Visualisation

The project uses visualisations to explore the clusters and the
relationships between songs. PCA is used to project the data into two
dimensions for visualisation only. The clustering itself is performed
using all nine standardised audio features.

8. Sensitivity Analysis

Different values of the nearest-neighbour count and distance threshold
are tested to examine how parameter choices affect the number and
quality of clusters.

## Main Results

The notebook reports the following configuration and results:

-   Unique songs clustered: 83,337
-   Number of clusters: 7
-   Nearest-neighbour parameter (K): 20
-   Distance threshold: 2.0
-   Size parameter (M): 228
-   Largest cluster share: approximately 34.9%
-   Union-Find silhouette score: 0.080
-   Union-Find Davies-Bouldin Index: 2.151
-   Union-Find NMI against genre: 0.147

## Reported cluster sizes:

-   Cluster 1: 29,083 songs
-   Cluster 2: 20,566 songs
-   Cluster 3: 14,344 songs
-   Cluster 4: 10,248 songs
-   Cluster 5: 6,399 songs
-   Cluster 6: 1,809 songs
-   Cluster 7: 888 songs

These values are the results reported by the project notebook and may
vary if the dataset or parameters change.

## Comparison with K-Means

The notebook also compares the Union-Find clustering result with a
K-Means result using seven clusters.

  Metric                   Union-Find   K-Means
  ---------------------- ------------ ---------
  Silhouette Score              0.080     0.197
  Davies-Bouldin Index          2.151     1.387
  NMI against genre             0.147     0.178

K-Means obtains stronger scores on these reported evaluation metrics.
The methods have different objectives: K-Means forms centroid-based
groups, while the Union-Find approach forms components through graph
connectivity. Therefore, the comparison should be interpreted in the
context of these different clustering approaches.

## Technologies Used

-   Python
-   Pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   Scikit-learn
-   SciPy
-   Jupyter Notebook
-   Streamlit

## Project Files and Outputs

The main analysis is contained in:

-   Spotify_Clustering_Final.ipynb

The notebook may generate intermediate and final data files during
preprocessing, distance/edge generation, clustering, evaluation, and
visualisation. Ensure the required dataset and generated files are
available at the paths expected by the notebook before running later
stages.

How to Run

1.  Clone the repository:

    git clone https://github.com/devanshi-v/DS603_DSA_project

2.  Open the project folder.

3.  Install the required Python packages used by the notebook. Common
    packages include:

    pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter

4.  Place the dataset in the location expected by the notebook.

5.  Open and run Spotify_Clustering_Final.ipynb in Jupyter Notebook or
    JupyterLab.

Note: Some distance-calculation and graph-processing stages can be
computationally intensive. Runtime and memory requirements depend on the
machine and dataset.

## Limitations and Future Improvements

-   The silhouette score indicates that the resulting clusters are not
    strongly separated under the metric’s assumptions.
-   Graph-based connectivity can produce clusters with shapes that
    differ from compact, centroid-based clusters.
-   Results depend on the selected audio features, nearest-neighbour
    count, distance threshold, and size parameter.
-   PCA plots show a two-dimensional projection and may not display all
    separation present in the original nine-dimensional feature space.
-   Future work could explore alternative distance metrics, approximate
    nearest-neighbour methods, additional parameter searches, and
    further cluster-interpretation techniques.

## Group Members

  Name               Student ID
  ------------------ ------------
  Vrinda Teli        202618050  
  Krishika Lalwani   202618016  
  Devanshi Vora      202618013  
  Dishi Shah         202618051  
  Lakshay Modi       202618009  
  Divyesh Padaliya   202518028  

## Conclusion

This project demonstrates how a Union-Find data structure can be applied
to graph-based song clustering. By combining standardised audio
features, nearest-neighbour relationships, distance-based edge
filtering, and connected-component merging, the project creates groups
of similar Spotify tracks. Evaluation and comparison with K-Means
provide additional insight into the strengths and limitations of the
approach.
