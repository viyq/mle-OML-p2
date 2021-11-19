# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
The project main goals are to deploy Azure ML best models, to consume the model and automation of pipelines.

## Summary

In this project, the Bank Marketing dataset is used. The data is related with direct marketing campaigns of a bank. The client answers will be used to decide if the product (bank term deposit) 
would be ('yes') or not ('no') subscribed. The classification goal is to predict if the client will subscribe (yes/no) a term deposit (variable y).

AzureML will be used to configure a cloud-based machine learning production model, deploy it, and consume it. 

The project includes the following parts/steps:

    1. Authentication
    2. Automated ML Experiment
    3. Deploy the best model
    4. Enable logging
    5. Swagger
    6. Consume model endpoints
    7. Create and publish a pipeline
    
## Architectural diagram

An image "architectural diagram.png" shows the design of the project as general overview. 

## Steps 1 to 3

The Azure credentials to be use in ML are stored in the config.json file. The AutoML of the dashboard can be used to create an AutoML experiment
that will later allow to select the best model. Once the best model is selected, the model can be deployed.

# Screenshots

Service principal created and associated with workspace
https://github.com/viyq/mle-OML-p2/blob/main/sp%20screenshot.jpg

AutoML experiment completed 
https://github.com/viyq/mle-OML-p2/blob/main/AutoML%20experiment%20completed.jpg

Bankmarketing as registered dataset 
https://github.com/viyq/mle-OML-p2/blob/main/bankmarketing%20as%20registered%20dataset.jpg

Best model 
https://github.com/viyq/mle-OML-p2/blob/main/best%20model%20VotingEnsemble.jpg

Best model deployment 
https://github.com/viyq/mle-OML-p2/blob/main/best%20model%20deployment.jpg

## Steps 4 to 6

Once the best model has been deployed, the file logs.py is used to enable Application Insights and retrieve logs. The next step is to consume the deployed model
using Swagger. Docker is invoked to pull an image and to run a port with "serve.py". After Swagger is deployed and the server is up, a swagger.json file will be 
called with the url in the swagger-ui:    http://localhost:8000/swagger.json

The display of the json file using Swagger gives examples of how to interact with the model. The file endpoints.py contains two examples of data that can be posted
to the URL of the web service via requests to get the response of the model.

Step 6 also includes the results of benchmarking the endpoint with Apache bench.

### Screenshots

Bank model app insight enabled
https://github.com/viyq/mle-OML-p2/blob/main/bank%20model%20app%20insight%20enabled.jpg

Logging is enabled by running logs.py
https://github.com/viyq/mle-OML-p2/blob/main/running%20logspy%20app%20insights.jpg

Swagger runs in local host
https://github.com/viyq/mle-OML-p2/blob/main/swagger%20API%20bank%20model%2001.jpg

Model consumption with endpoint.py 
https://github.com/viyq/mle-OML-p2/blob/main/consume%20model%20endpoint.jpg

Benchmarking with Apache
https://github.com/viyq/mle-OML-p2/blob/main/benchmark%20endpoint.jpg

## Step 7: Automated ML and pipeline publication

Step 7 includes a complete pipeline creation to allow automation and publication. The second part of the project (notebook) will publish a pipeline after implementation of AutoML

### Screenshots

The Bankmarketing dataset with the AutoML module
https://github.com/viyq/mle-OML-p2/blob/main/bank%20dataset%20with%20pipeline%20overview.jpg

Screenshot of the Jupyter Notebook with “Use RunDetails Widget” with the step runs completed
https://github.com/viyq/mle-OML-p2/blob/main/AutoML%20widget%20run%20completed.jpg

ML studio showing the pipeline endpoint as Active, "Completed" status of the pipeline
https://github.com/viyq/mle-OML-p2/blob/main/pipeline%20rest%20endpoint.jpg

Published Pipeline overview, showing a REST endpoint and a status of ACTIVE
https://github.com/viyq/mle-OML-p2/blob/main/published%20pipeline%20active.jpg

ML studio showing the scheduled run
https://github.com/viyq/mle-OML-p2/blob/main/ML%20scheduled%20pipeline%20run.jpg

## Pipeline architecture

The Pipeline class in the notebook file is defined by the variable steps. Where steps is an AutoMLStep object type that includes the AutoML configuration of the model (automl_config), 
and the outputs (metrics_data and model_data).

After running the pipeline, the best model can be selected based on the primary metric.

## Publish and run from REST endpoint

The pipeline run can be identified by a run_id and publishing it with pipeline_run.publish_pipeline() will enable a REST endpoint to rerun the pipeline from any HTTP library on any platform.

## Future work

Now that the foundation (model creation, deployment and consumption) is in place most of the future work may involve interacting with the model in real applications.
Testing data fed into the model and getting predictions will be the best way to prove if the model is intelligent enough or if it needs new data to be trained. 
The pipelines above will allow a smooth retraining process. Consuming the model in diferent applications may also help to identify problems with the response time and 
allow more benchmarking.
 
## Screencast link

Screencast Project Operationalizing ML
https://youtu.be/HvzKVQKsayw

