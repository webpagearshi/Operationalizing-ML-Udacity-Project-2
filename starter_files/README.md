
# Operationalizing Machine Learning

Project Overview: In this project we have used the Bank Marketing Dataset which I have downloaded from the link provided in the project information.
In the project I have used Azure to configure a cloud based machine learning production model, deployed it and then consumed it. I have also created, published and consumed a pipeline using Python SDK.

Project Link: https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv

## Table of Content
* [Architectural Diagram](#architectural-diagram)

* [Key Steps](#key-steps)
  * [Authentication](#auth)
  * [Create and run Auto ML Experiment](#auto)
  * [Deploy the Model](#deploy)
  * [Enable Application Insights and retrieve logs](#app)
  * [Swagger Documentation](#swagger)
  * [Consume Model Endpoints and Benchmark the endpoint using Apache Benchmark](#consume)
  * [Create , Publish and Consume a Pipeline](#pipeline)
    
* [Screen Recording](#screen-recording)

* [Standout Suggestions](#standout-suggestions)

## Architectural Diagram
 ![Architectural Diagram](Images-Review/Architectural%20Diagram.png "Architectural Diagram")

## Key Steps
In the first section we will configure a cloud based machine learning production model, deployed it and then consumed it

<a name="auth"></a>
*Step 1*: Authentication
Since I have used the Udacity workspace to complete this project I skipped this step as I did not have authorization to create a service principal.

<a name="auto"></a>
*Step 2*: Create and run Auto ML Experiment

a. Uploaded the dataset into the Azure Studio and created a Registered Dataset

**Registered Dataset**

![Registered Dataset](Images/Step1-Registered%20Dataset.JPG "Registered Dataset")

b. Configured a new compute cluster (VM size is Standard_VS12_v2 and minimum nodes is 1) and created a new Automated ML Run. Once the Experiment is completed you can see the Best Model.

**AutoML Experiment Completed**

![AutoML Experiment Completed](Images/Step1-Experiment%20Completed.JPG "AutoML Experiment Completed")


**Best Model**

![Best Model](Images/Step1-Best%20Model.JPG "Best Model-Voting Ensemble")

<a name="deploy"></a>
*Step 3*: Deploy the Model

Select the Best Model for Deployment, enabled authentication and deployed the model using Azure Container Instance.

**Deployment Settings**

![Deployment Settings](Images/Step3-Deploying%20the%20Model%20Settings.JPG "Deploying the Best Model")


<a name="app"></a>
*Step 4*: Enable Application Insights and retrieve logs

a. Enabled Application Insights using Python SDK

**Application Insights enabled by running logs.py script**

![Application Insights](Images/Step4-Application%20Insights-Enabled.JPG "Application Insights")

b. View the logs in the terminal after executing the logs.py script

**Logs**

![Logs](Images/Step4-Logs%20by%20logs.py-a.JPG "logs")
![Logs](Images/Step4-Logs%20by%20logs.py-b.JPG "logs")
![Logs](Images/Step4-Logs%20by%20logs.py-c.JPG "logs")


<a name="swagger"></a>
*Step 5*:Swagger Documentation

Azure provides swagger json file for deployed models. Heading to the Endpoints section->Details tab find the Swagger URL which is used to download the file and saved it locally in the same folder as swagger.sh and serve.py files. Execute the swagger.sh script which downloads the latest Swagger container and runs it on port 9000. Running the script serve.py starts a python server on port 8000.

**Screenshot showing that swagger runs on localhost showing the HTTP API methods and responses for the model.**

![Swagger](Images/Step5-Swagger%20runs%20on%20localhost.JPG "swagger runs on localhost")
![Swagger](Images-Review/Step5-Swagger-Documentation-b.JPG)
![Swagger](Images-Review/Step5-Swagger-Documentation-c-1.JPG)
![Swagger](Images-Review/Step5-Swagger-Documentation-c-2.JPG)
![Swagger](Images-Review/Step5-Swagger-Documentation-d.JPG)

<a name="consume"></a>
*Step 6*:Consume Model Endpoints and Benchmark the endpoint using Apache Benchmark

a. Consume Model Endpoints- Head to the consume tab in the Endpoints section and then note the REST Endpoint URI and Primary Key and then in the endpoint.py file modify the scoring_uri and key to match them respectively. Now execute the enddpoint.py file and you will see the output from the model in the terminal.

**Consume Model Endpoints**

![endpoint](Images/Step6-Endpoint%20result.JPG "Endpoint result")

b. Benchmarking-Make changes in the benchmark.sh file by replacing the authentication key with the primary key of the model and the REST uri with that of the model. After running the endpoint.py file, a data.json file appears in the folder. Then run the benchmark.sh script.

**Screenshot showing that Apache Benchmark runs against the HTTP API using authentication keys to retrieve performance results.**

![Benchmarking](Images/Step6-Benchmark.sh%20log-a.JPG "Benchmarking")
![Benchmarking](Images/Step6-Benchmark.sh%20log-b.JPG "Benchmarking")
![Benchmarking](Images/Step6-Benchmark.sh%20log-c.JPG "Benchmarking")

Now that we have used Azure to configure a cloud based machine learning production model, deployed and consumed it we will move to the next section where we will use Python SDK to create, publish and consume a Pipeline.

<a name="pipeline"></a>
*Step 7*: Create , Publish and Consume a Pipeline

a. Use the Auto ML Experiment which has run earlier and the previously created compute cluster to create the Pipeline

**Pipeline Created**

![Pipeline](Images/Step7-Pipeline%20Created%20Completed.JPG "Pipeline Created")

**BankMarketing Dataset with AutoML Module**

![Pipeline](Images/Step7-BankMarketing%20Dataset%20with%20AutoML%20Module-Completed.JPG "AutoML Module")

b. After the pipeline_run object is created publish the Pipeline

**Pipeline section shows Pipeline Endpoint**

![Pipeline](Images/Step7-Pipeline-Endpoint.JPG "published pipeline")

**Published Pipeline Overview showing a REST Endpoint and status Active**

![Pipeline](Images/Step7-Published%20Pipeline%20Overview.JPG "Published Pipeline")

In Jupyter Notebook we use RunDetail Widget to show the step runs.

**RunDetail Widgets-step runs**

![RunDetail](Images-Review/Step7-Jupyter-Show-step-runs.JPG "RunDetail Widget")
![RunDetail](Images-Review/Step7-6.JPG "RunDetail Widget")

c. Consume a Pipeline endpoint-The first step was to authenticate and then the published Pipeline was used to retrieve the endpoint using Python SDK.

**Scheduled Run in the ML Studio**

![Pipeline](Images/Step7-5.JPG "Pipeline")

![Pipeline](Images-Review/Step7-3.JPG "Pipelines")

## Screen Recording
[Screencast Link for Project-Operationalizing ML](https://youtu.be/rdz4DlNq-pE "Screencast for Project2-Operationalizing ML")

## Standout Suggestions
1. While creating the Automated ML run I would like to choose validation type instead of using auto. I would also enable featurization for feature selection and make changes in feature type and impute with options for the features. I will examine imbalanced classes which were detected in input and rectify the issue.

2. When creating the compute cluster I would like to experiment with virtual machine sizes so that I can try and find a cheaper option without affecting the production model and endpoint consumption.

3. Use Batch Inference Pipeline to do predictions using parallelism. This increases productivity and optimizes costs.

#### The Udacity Course material and Microsoft Documentation has been used as reference.
