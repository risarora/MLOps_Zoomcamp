# What we have learnt so far

1. **Experiment tracking**: We run a number of experiments with an objective. We saw how we can use _MLflow Experiment_ to track all of runs in an experiment.
2. **Model tracking**: There are a number of models from all the experimental runs. However, not all of them are selected as production candidates. We saw how we can select good candidates and manage their life cycle in _MLflow Model Registry_.
3. **Pipeline**: We also saw, how we took the code from notebook and created pipeline so as to make the code modular, reproducible, manage dependencies and orchestrate each of the processes with help of _Prefect_ workflow engine.

![](/Week4/img/beforedeploy.png)

# What is next?

Now that the model is registered in _MLflow Model Registry_ and production ready, we need to deploy that so that we can get the prediction result for the given data to realize its value.

# Model Deployment

The kind of deployment depends upon how we want the prediction result. Say, if we can wait for an hour or a day for the prediction result then we do the `offline batch deployment` of the model that runs periodically. On the other hand, if we need to the prediction in real time then it has to be online deployment where the model is always up and running on a compute to serve. Again, when it comes to online deployment, based off the use case, we can deploy the model as a web service or a streaming service.

**Batch Mode:** When we can wait for hours for model to make a prediction and and speed of response is not of prime importance.

**Webservice:** We wrap the model in a web service where the model can be loaded and served to predict in a REST API call. For entire set of data received in an API call, the output from the model is sent in the response in one:one fashion.

**Streaming:** Runs in producer and consumer model where the producer pushes information to event stream and the consumers listen to the stream to get updates. For example, the predicted taxi duration result is published in the event stream and consumers such as subsequent models listen to the event stream to fetch the predicted data to further do further processing.

![](/Week4/img/predwebservice_v1.png)

https://www.youtube.com/watch?v=JMGe4yIoBRA&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=18

- [01 Three ways to deploy a Model](01-Three%20ways%20to%20deploy%20a%20Model.md)
- [02 Batch deployment of model](02-Batch%20deployment%20of%20model.md)
- [03 Deploying model as a web-service](03-Deploying%20model%20as%20a%20web-service.md)
- [04 Deploy model as Streaming service](04-Deploy%20model%20as%20Streaming%20service.md)
