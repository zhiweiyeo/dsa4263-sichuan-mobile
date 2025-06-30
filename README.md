# DSA4263-project

This is our repository to our project on detecting telecommunication fraud in Sichuan China. The selected dataset originates from the 2020 Digital Sichuan Innovation Competition, organised by the Sichuan Big Data Center. It contains anonymized telecom data from 6,106 subscribers across 23 cities in Sichuan, China, from August 2019 to March 2020.

## Structure
This repository consists of the following files:
```
├── README.md
├── requirements.txt
├── data
│   ├── processed
│   │   └── processed_dataset.csv  # only this file can be downloaded
│   └── raw  # Some files are above 2GB, which resulted in the file being rejected by Git LFS with an error message.
│       ├── test 
│       │   ├── test_app.csv
│       │   ├── test_sms.csv
│       │   ├── test_user.csv
│       │   └── test_voc.csv
│       └── train
│           ├── train_app.csv
│           ├── train_sms.csv
│           ├── train_user.csv
│           └── train_voc.csv
├── notebooks
│   ├── 1.0-data_preprocessing.ipynb
│   ├── 2.0-exploratory_data_analysis.ipynb
│   ├── 3.0-baseline_model_rn.ipynb
│   ├── 4.0-similarity-graph.ipynb
│   ├── 5.0-feature_level_ensemble.ipynb
│   ├── 6.0-care_model.ipynb
│   └── 7.0-care_model_interpretation_with_SHAP.ipynb
└── references
    └── data_dictionary.md
```

## Requirements
To run the notebooks, please install the required packages that can be found in the requirements.txt file.

## Data
This directory consists of the raw and processed datasets of the project. 

In the raw directory, it consists of raw training and testing data for 4 different data subsets, APP (Application usage record), SMS (Short Message Service), VOC (Voice Record) and USER(Consumption Record). Some files in the raw directory are above 2GB, which resulted in the files being rejected by Git LFS with an error message. 

The processed directory consists of the output of `1.0-data_preprocessing`, which is the processed data (`data/processed/processed_dataset.csv`). Please download this file for the implementation of this project.

## Notebooks
1. #### `1.0-data_preprocessing.ipynb`
    This file ingests the raw data from the 2020 Digital Sichuan Innovation Competition, located in the `data/raw` directory. It then performs a series of data cleaning and preprocessing steps to enhance readability and usability. These steps include:

    * Feature engineering and aggregation of app usage, SMS, and call data by phone_no_m to summarize user behavior.

    * Handling missing or null values, either by imputing with 0.

    * Converting data types to ensure numerical fields, dates, and categorical variables are properly formatted.

    The final output is a cleaned csv file that is easier to interpret, ready for analysis, and saved in as `data/processed/processed_dataset.csv`

2. #### `2.0-exploratory_data_analysis.ipynb`
    This notebook performs Exploratory Data Analysis (EDA) on the cleaned dataset (`data/processed/processed_dataset.csv`). The goal is to uncover initial patterns, spot anomalies, and gain insights into the structure of the data. Key components include:

    * Summary statistics for numerical and categorical features.

    * Distribution plots and histograms to understand variable spread.

    * Correlation matrix and heatmap to identify potential relationships.

    * Boxplots and bar charts to compare categories or detect outliers.

    * Time-based or geospatial trends.

    * Observations and notes for guiding further analysis or modelling.

3. #### `3.0-baseline_model_rn.ipynb`

    This notebook implements our baseline model: Relational Neighbour Classifier (RNC). It serves as an initial benchmark to evaluate the predictive power of simple relational heuristics before applying more complex models. Key steps include:

    * Constructing a graph-based structure to capture relationships between entities (e.g., users, phone numbers, transactions).

    * Applying the Relational Neighbour Classifier, which makes predictions based on the labels of neighboring nodes in the graph.

    * Evaluating model performance using standard classification metrics such as accuracy, precision, recall, and F1 score 

4. #### `4.0-similarity_graph.ipynb`
    This notebook constructs a similarity graph where nodes represent entities (such as users, transactions, or phone numbers), and edges represent the similarity between them, measured using cosine similarity.

    Key steps include:

    * Cosine Similarity Calculation: Cosine similarity is used to measure the similarity between entities. 

    * Graph Construction: A graph is constructed where edges represent high similarity between entities. Nodes are connected based on a predefined similarity threshold.

    * Graph Visualization: The graph is visualized to show clusters of similar entities, which may help in identifying fraud patterns or suspicious activities.


5. #### `5.0-feature_level_ensemble.ipynb`
    This notebook implements the feature-level ensemble method for fraud detection. It combines graph node embeddings from multiple Graph Neural Network (GNN) models and uses them to train a Random Forest Classifier for fraud detection.

    Key steps include:

    * Graph Node Embeddings: Node embeddings are generated using different GNN models:

        * GCN: Uses spectral graph convolution to aggregate neighbor features.

        * GAT: Applies attention mechanisms to weigh neighbors' contributions.

        * GraphSage: Samples neighbors to create more generalizable embeddings.

    * Feature Fusion: The embeddings from these models are concatenated into one matrix, which is then used to train a classifier.

    * Evaluating ensemble performance using metrics like accuracy, precision, recall, and F1 score.

6. #### `6.0-care_model.ipynb`
    This notebook implements the CARE-GNN (Context-Aware Relational Graph Neural Network) model for node classification. CARE-GNN is designed to handle heterogeneous graphs with multiple types of relations between nodes—especially useful in fraud detection where nodes may be linked by various behavioral or contextual signals.

    Key steps include:

    * Relation-specific Aggregation: For each node, the model first aggregates information from its neighbors separately for each relation type (e.g., call, SMS, top-up).
    * Cross-relation Combination: The relation-specific features are then combined. A relation-level attention mechanism is applied to assign a learnable weight to each relation, indicating its importance for each individual node.
    * Final Embedding: The model fuses the aggregated multi-relation features with the node’s own features to form the final node embedding.
    * Classification: The resulting embedding is passed through a classification layer to predict whether the node (e.g., phone number) is fraudulent.

7. #### `7.0-care_model_interpretation_with_SHAP.ipynb`
    This notebook provides an interpretation of the CARE-GNN model using SHAP (SHapley Additive exPlanations) and Integrated Gradients (IG) to understand the influence of input features on the model's predictions.

    SHAP is not directly compatible with complex GNN architectures like CARE-GNN due to their non-Euclidean structure. To address this, we adopt a model-agnostic surrogate approach.

    Key steps include:

    * Embedding Extraction: Node embeddings are extracted from CARE-GNN just before the final classification layer.
    * Model Wrapper: A Random Forest is trained to mimic the CARE-GNN's predictions using the same inputs, with target values being the GNN’s predicted outputs.
    * SHAP Value Computation: SHAP values are computed on the surrogate model to estimate the importance of individual features.
    * Summary plot visualizations

# References
This directory consists of `data_dictionary.md` which describe each feature name under the 4 data subsets.
