# syAI4ML_PIMA A project by Bukhari Lab

Contributors

- Iram Wajahat
- AmritPal Singh
- Fazel Keshtkar
- Syed Ahmad Chan Bukhari

A Symbolic AI Framework for Enhanced Diabetes Prognosis Accuracy and Explainability

## Tutorial:
To execute the code from scratch, please follow these steps:
1. Create an empty neo4j instance - neo4j is available in multiple distributions ie. Desktop, Web, etc., in our case we used neo4j in a local Docker container instance. Other distributions should work as well, just make sure they support the gds and apoc neo4j libraries which we will be using. For information on how to install these libraries please view the official documentation: GDS documentation [link](https://neo4j.com/docs/graph-data-science/current/installation/), APOC documentation [link](https://neo4j.com/docs/apoc/current/installation/)
2. Execute the cypher queries found as txt files in order. These can be found in the scripts folder. Cypher queries can be executed in many ways as well, we used the query editor in the local web interface for this task
3. Open and run the pimakgcreation notebook. You will need our modified diabetes dataset which has the bucketed features. This can be found under data/diabetes_final.csv. All other files found under the data directory are not necessary if following this workflow from scratch. However, they do contain results generated at different stages of our procedure, allowing you to import them as desired from various parts of the process. At the end of this step you will have your best performing models (both based on buckets and embeddings) saved.
4. Run the embedding generation and prediction notebook. This notebook will generate embeddings using all possible relationship combinations and then predict on the models trained in the previous step
5. Run our embedding analysis notebook, which does statistical and graphical analyses on the scores for the generated relationship embeddings 

For more details about each file in this repository, please refer to the project breakdown below.

## Project Breakdown:
### data:
- diabetes_final.csv: official PIMA diabetes dataset modified using bucketed values specified in paper
- final_df.csv: contains our neo4j fastrp embeddings for each sample (represents our final dataframe at the end of the preprocessing and data aggregation step of pimakgcreation.ipynb) - buckets are one-hot encoded and embedding values are split up
- finalresults.md: has link to csv containing resulting embeddings for each relationship combination
- predicitonscores.md: has link to csv containing predicted scores for each model using combination embeddings

### final_models:
- nbbucket.pkl: best performing naive bayes model trained on bucketed pima data
- nbemb.pkl: best performing naive bayes model trained on knowledge graph embeddings from pima data
- nnbucket.keras: best performing neural network model trained on bucketed pima data
- nnemb.keras: best performing neural network model trained on knowledge graph embeddings from pima data
- rfbucket.pkl: best performing random forest model trained on bucketed pima data
- rfemb.pkl: best performing random forest model trained on knowledge graph embeddings from pima data
- svmbucket.pkl: best performing svm model trained on bucketed pima data
- svmemb.pkl: best performing svm model trained on knowledge graph embeddings from pima data
- xgbbucket.pkl: best performing xgboost model trained on bucketed pima data
- xgbemb.pkl: best performing xgboost model trained on knowledge graph embeddings from pima data

### scripts: 
- 1.txt: contains cypher query to create all medical_concept, definition and synonym nodes in neo4j
- 2.txt: contains cypher query to create all sample nodes in neo4j
- 3.txt: contains cypher query to create all relationships between samples and medical_concept nodes in neo4j

### notebooks: 
- embeddinganalysis.ipynb: contains statistical and graphical analysis done on predictions done on embeddings derived from all possible relationship combinations
- embeddinggenerationandprediction.ipynb: iteratively gathers relationship combination embeddings from neo4j and predicts on models pretrained in pimakgcreation.ipynb
- pimakgcreation.ipynb: creates projected knowledge graph in neo4j, retrieves fastrp embeddings and trains models using said embeddings as well as bucketed pima data
