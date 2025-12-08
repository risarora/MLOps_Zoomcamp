# Three Ways to deploy a Model

Machine learning models can be deployed using three primary patterns: batch processing, streaming analytics, and web services (real-time online deployment). The choice depends on the specific business needs, latency requirements, and data volume. [1, 2]

## 1. Batch Deployment (Offline Prediction)

Batch deployment is the simplest and most cost-effective method, where the model processes a large dataset all at once at scheduled intervals (e.g., hourly, nightly).

• Characteristics:

    • Latency: High latency is acceptable, as predictions are not needed immediately.
    • Data: Processes large volumes of historical or accumulated data in bulk.
    • Use Cases: Churn prediction, risk analysis, generating monthly reports, or scoring all customers in a database.

• Implementation: Typically runs on job scheduling or orchestration platforms like Apache Airflow or cloud-native solutions, outputting predictions to a database or file system. [2, 3, 4, 5, 6]

## 2. Streaming Deployment (Near-Real Time Prediction)

In streaming deployment, the model continuously processes a stream of incoming data events as they arrive, reacting to them in near-real time.

• Characteristics:

    • Latency: Low to very low latency is required.
    • Data: Handles a continuous flow of data events (e.g., from Kafka or Kinesis streams).
    • Use Cases: IoT sensor analytics, real-time monitoring, and fraud detection in financial transactions.

• Implementation: The model is embedded within a data streaming consumer framework, such as Apache Spark Streaming or Apache Flink, to perform inference on the fly. [2, 5, 7, 8, 9]

## 3. Web Service Deployment (Real-Time Online Prediction)

Web service deployment involves wrapping the model in an API (Application Programming Interface) that listens for requests and returns predictions in real time.

• Characteristics:

    • Latency: Requires low latency (milliseconds) for immediate responses.
    • Data: Typically processes single requests at a time, often integrated with user-facing applications.
    • Use Cases: Recommendation engines, chatbots, ad-serving, and real-time fraud detection where an instant response is necessary.

• Implementation: The model is hosted on a server and exposed as a REST API using frameworks like Flask or FastAPI, often containerized with Docker and orchestrated with Kubernetes for scalability and reliability. [2, 10, 11, 12, 13]

## Summary Comparison

| Feature [5, 14, 15, 16, 17] | Batch Deployment          | Streaming Deployment          | Web Service Deployment      |
| --------------------------- | ------------------------- | ----------------------------- | --------------------------- |
| Prediction Speed            | Offline (scheduled)       | Near-real time                | Real-time (instant)         |
| Data Flow                   | Large datasets in bulk    | Continuous data streams       | Individual API requests     |
| Latency                     | High                      | Low                           | Very Low                    |
| Use Cases                   | Reports, risk modeling    | IoT analytics, monitoring     | Recommendations, chatbots   |
| Core Technologies           | Airflow, Cron, Spark Jobs | Kafka, Flink, Spark Streaming | FastAPI, Flask, Docker, K8s |

Choosing the appropriate deployment strategy ensures the model effectively meets the operational and performance requirements of the specific business application. [2, 18, 19, 20]

[1] https://blog.devops.dev/mlops-project-part-3a-machine-learning-model-deployment-2eafe2ff89a8
[2] https://www.youtube.com/watch?v=wBosclQJvWQ
[3] https://medium.com/@iagomodesto/batch-or-api-deployment-of-machine-learning-models-98369b04294a
[4] https://dagshub.com/blog/model-deployment-types-strategies-and-best-practices/
[5] https://medium.com/swlh/productionizing-machine-learning-models-bb7f018f8122
[6] https://cloud.google.com/discover/what-is-batch-inference
[7] https://fullstackdeeplearning.com/spring2021/lecture-11/
[8] https://medium.com/mlearning-ai/end-to-end-machine-learning-workflow-part-2-e7b6d3fb1d53
[9] https://docs.oracle.com/en/solutions/deploy-ml-at-edge/index.html
[10] https://northflank.com/blog/how-to-deploy-machine-learning-models-step-by-step-guide-to-ml-model-deployment-in-production
[11] https://campus.datacamp.com/courses/developing-machine-learning-models-for-production/ml-in-production-environments?ex=1
[12] https://hazelcast.com/blog/from-batch-machine-learning-to-real-time-machine-learning/
[13] https://edgedelta.com/company/blog/stream-processing-vs-batch-processing
[14] https://shelf.io/blog/machine-learning-deployment/
[15] https://datatalks.club/blog/mlops-10-minutes.html
[16] https://www.linkedin.com/posts/varsha-verma-_data-collection-is-a-cornerstone-of-market-activity-7329918144016211969-xtuS
[17] https://datatalks.club/blog/mlops-zoomcamp.html
[18] https://shalb.com/blog/building-reliable-systems-factors-of-success/
[19] https://embee.co.in/blog/10-crucial-factors-for-optimal-sap-deployment-selection/
[20] https://strandsagents.com/latest/documentation/docs/user-guide/deploy/operating-agents-in-production/
