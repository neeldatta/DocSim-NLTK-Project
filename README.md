# Project:
1) JupiterOne policies to Cyber Asset semantic similarity matching.
Main files are: 

- Policy Matching Tool.ipynb => NLTK tool that takes in xml sheet of URLs and tries to match and score all the text from each website to a specific query/queries. 

- DocSim vs. TF-IDF.ipynb => Tested both NLTK tools to see which gave more accurate results.

- 3 Queries + 3 Cyber .ipynb => Tested Tf-IDF tool on three different example cases to make sure the scores were accurate across different queries. 

- 10,000 AWS.ipynb => Tested tool on an xml with 10,000 sub-links and visualized data to find the cut off for scores with meaningful correlations to the queries.
