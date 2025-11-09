# MLOps Zoomcamp 1.1 - Introduction

```
Design --> Train --> Operate

```

You've correctly described a classic machine learning workflow:

1.  **The Model:** A trained model that predicts trip duration.
2.  **Deployment:** The model is packaged into a web service/API.
3.  **Use Case:** A customer on a phone app sends a pickup and drop-off location to this API.
4.  **Prediction:** The API uses the model to return a prediction (e.g., "10 minutes").
5.  **MLOps Purpose:** This process is part of the **Operate** stage. MLOps (which you called "envelopes") provides the tools and practices to:
    - Experiment reproducibly.
    - Retrain models with one click.
    - Deploy easily.
    - Monitor model quality to prevent degradation.

This is a perfect real-world example.

---

# MLOps Zoomcamp 1.4 - Course overview

### Expanding on the Key Concepts (The "How" and "Why")

Let's dive a bit deeper into the stages you mentioned, using your ride-hailing scenario.

#### 1\. Experimentation & Reproducibility ("we do not lose our mind")

- **The Problem:** Data scientists try hundreds of models, data processing steps, and parameters (hyperparameters). Without a system, it's impossible to remember which combination produced the best result.
- **How MLOps Helps (e.g., with tools like MLflow, Weights & Biases):**
  - **Tracking:** Every time you run an experiment, the system automatically logs the code version, data version, parameters, and resulting metrics (e.g., Mean Absolute Error of the predicted trip time).
  - **Reproducibility:** You can instantly re-run any past experiment with the exact same conditions. This is crucial for debugging and validating results.

#### 2\. One-Click Retraining & Deployment ("retrain the model easily with just one click")

- **The Problem:** Retraining a model manually is slow, error-prone, and not scalable.
- **How MLOps Helps (e.g., with CI/CD pipelines):**
  - **Automation:** The entire process—fetching new data, preprocessing, training, evaluating, and packaging the model—is codified into a **pipeline**.
  - **Orchestration:** This pipeline can be triggered automatically (e.g., every week) or manually with a single command. It ensures the process is consistent and reliable.
  - **Deployment:** The new model is automatically tested and can be deployed to the API with strategies like blue-green deployment to avoid downtime for your customers.

#### 3\. Monitoring & Preventing Degradation ("how do we make sure the model is performing well")

This is a critical point. Model performance can degrade in production without any changes to the code. This is called **model drift**. There are two main types:

- **Data Drift (Covariate Shift):** The distribution of the _input data_ changes over time.

  - **Example:** Your model was trained on data from the summer. Now it's winter. Trip patterns change (more indoor pickups, weather delays), so the model's 10-minute prediction becomes less accurate because the input data (weather, traffic patterns) looks different.

- **Concept Drift:** The relationship between the input data and the target variable changes.

  - **Example:** A new law is passed increasing speed limits on major highways. The relationship between _distance_ and _trip time_ has now fundamentally changed. A 5-mile trip that used to take 10 minutes might now only take 8. The model hasn't learned this new "concept."

**How MLOps Helps with Monitoring:**

- **Tracking Predictions vs. Actuals:** The system continuously monitors the API. It logs the model's predictions (the "10 minute" estimate) and, crucially, later collects the **actual** trip time.
- **Statistical Monitoring:** It runs statistical tests on the incoming data and the predictions vs. actuals to detect significant drift.
- **Alerting:** If drift or a drop in accuracy is detected, the system alerts the data science team. This is the trigger to investigate and potentially retrain the model with newer data.

### The Big Picture: MLOps as a Set of Practices

You are absolutely right. **MLOps** (Machine Learning Operations) is not a single tool, but a set of practices and cultural principles that combine:

- **Machine Learning**
- **Software Engineering** (DevOps principles like CI/CD)
- **Data Engineering**

Its goal is to **automate, standardize, and scale** the ML lifecycle, making it reliable, efficient, and collaborative—exactly as you described.

---

The notebook, while functional, suffers from typical issues that make it difficult to reproduce, track, and maintain. It represents a "Level 0" (no MLOps) maturity level.

### **Key Issues with the Current Notebook:**

- **Lack of Clarity:** It's unclear which cells are necessary and in what order to execute them.
- **Lost Experiment History:** There's no systematic way to track different model iterations, parameters, and their performance metrics. Relying on memory or manual spreadsheets is error-prone.
- **Risk of Overwriting:** Variables and saved models can be accidentally overwritten, leading to lost work.
- **Poor Reproducibility:** Changing parameters (like dates) requires manual, error-prone edits to the notebook code.
- **Not Modular:** The code is not broken into reusable, parameterized components.

### **MLOps Solutions Proposed (Mapped to Course Modules):**

The course will address these problems with specific tools and practices:

1.  **Module 2: Experiment Tracking (MLflow)**

    - **Tool:** MLflow.
    - **Solution:** Log all experiments, parameters, and metrics automatically to preserve history and compare model performance.

2.  **Module 3: ML Pipelines (Prefect, Kedro)**

    - **Solution:** Break the notebook into a structured, automated pipeline (e.g., data preparation -> feature engineering -> model training).
    - **Benefits:** Enables easy parameterization, reproducibility, and avoids re-running unnecessary steps.

3.  **Module 4: Model Serving**

    - **Solution:** Deploy the trained model as a web service (e.g., a REST API) to make it available for users/clients.

4.  **Module 5: Model Monitoring**

    - **Solution:** Monitor the live model's performance to detect drops in accuracy or data drift and trigger alerts.

5.  **Module 6: Best Practices**

    - **Focus:** Code quality, testing, documentation, and packaging (e.g., using Docker) for both the pipeline and the web service.

6.  **Module 7: Processes**

    - **Focus:** The human and collaborative aspects of MLOps—how teams work together to own the code, understand the problem, and ensure they are building the right solution.

### **The Ultimate Goal: Automation**

The course envisions a mature MLOps system (Level 4) where the entire process is automated:

- Monitoring detects a performance drop.
- This automatically triggers the pipeline to retrain a model on new data.
- The new model is automatically validated and deployed.
- This creates a continuous loop with minimal human intervention.

### **Final Note:**

The speaker clarifies that not every project needs the highest level of maturity. The course will also cover the different maturity levels (0 to 4) and help decide what's appropriate for a given project.

# MLOps Zoomcamp 1.5 - MLOps maturity model

## **The Five Maturity Levels:**

### Level 0: No MLOps (Manual Process)

- **Description:** The starting point. Work is done entirely in sloppy Jupyter notebooks with no automation, tracking, or reproducibility.
- **Use Case:** Perfect for initial proof-of-concept (POC) projects and experimentation where the goal is to simply see if an idea works.

### Level 1: DevOps but No MLOps (Engineering Best Practices)

- **Description:** Applies standard software engineering best practices to ML. This includes automated releases, CI/CD pipelines, unit/integration tests, and monitoring of operational metrics (like requests/sec).
- **Focus:** The system is reliable from an engineering standpoint but is not "ML-aware." It lacks specific features like experiment tracking or a model registry.
- **Use Case:** The essential first step when moving a proven POC model into production.

### Level 2: Automated Training (Emerging MLOps)

- **Description:** Introduces core MLOps capabilities. The training process is automated into a pipeline or script. It includes experiment tracking and a model registry to manage different model versions.
- **Key Shift:** Data scientists and engineers start working closely together.
- **Use Case:** Becomes necessary when an organization has multiple models in production, making it efficient to invest in this infrastructure.

### Level 3: Automated Deployment (Managed ML Platform)

- **Description:** Focuses on making deployment seamless and low-friction, often via an ML platform. May include capabilities for A/B testing to compare model versions.
- **Inclusion:** The speaker argues that **model monitoring** (tracking live performance for drift or degradation) is a key component of this level.
- **Use Case:** For organizations with several mature use cases or a single, critical model that requires close observation.

### Level 4: Full MLOps Automation (Self-Healing System)

- **Description:** The highest level of maturity. The system is a closed loop: monitoring detects a problem (e.g., model drift), which automatically triggers retraining, validation, and deployment of a new model with minimal to no human intervention.
- **Use Case:** Reserved for the most critical and well-understood models. The speaker emphasizes that this requires a high degree of trust in the automated system.

---

### **Key Takeaways and Pragmatic Advice:**

- **Not All Projects Need the Highest Level:** Organizations should be pragmatic. Most models may only need to be at Level 2 or 3. Level 4 is for specific, high-stakes use cases.
- **Start Simple:** It's perfectly acceptable to begin at Level 0 for a POC. The investment in more mature practices should grow as the project proves its value and moves to production.
- **Human Oversight is Often Necessary:** For many models, having a human make the final decision on deployment is safer and more desirable than full automation.
- **Course Goal:** This course will equip students to build systems that reach **Level 2, touching Level 3**, covering automated training, experiment tracking, and model monitoring.

## Machine Learning operations maturity models by Microsoft

https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/mlops-maturity-model#level-1-devops-no-mlops

**The purpose of this maturity model is to help clarify the Machine Learning Operations (MLOps) principles and practices. The maturity model shows the continuous improvement in the creation and operation of a production level machine learning application environment. You can use it as a metric for establishing the progressive requirements needed to measure the maturity of a machine learning production environment and its associated processes.**

## Maturity model

The MLOps maturity model helps clarify the Development Operations (DevOps) principles and practices necessary to run a successful MLOps environment. It's intended to identify gaps in an existing organization's attempt to implement such an environment. It's also a way to show you how to grow your MLOps capability in increments rather than overwhelm you with the requirements of a fully mature environment. Use it as a guide to:

- Estimate the scope of the work for new engagements.
- Establish realistic success criteria.
- Identify deliverables you'll hand over at the conclusion of the engagement.

As with most maturity models, the MLOps maturity model qualitatively assesses people/culture, processes/structures, and objects/technology. As the maturity level increases, the probability increases that incidents or errors will lead to improvements in the quality of the development and production processes.

The MLOps maturity model encompasses five levels of technical capability:

| Level | Description                     | Highlights                                                                                                                                                                                                          | Technology                                                                                                                                                      |
| ----- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | No MLOps                        | - Difficult to manage full machine learning model lifecycle <br>- The teams are disparate and releases are painfu <br>- Most systems exist as "black boxes," little feedback during/post deployment                 | - Manual builds and deployment <br>- Manual testing of model and applicatio <br>- No centralized tracking of model performanc <br>- Training of model is manual |
| 1     | DevOps but no MLOps             | - Releases are less painful than No MLOps, but rely on Data Team for every new model <br>- Still limited feedback on how well a model performs in productio <br>- Difficult to trace/reproduce results              | - Automated build <br>- Automated tests for application code <br>-                                                                                              |
| 2     | Automated Training              | - Training environment is fully managed and traceabl <br>- Easy to reproduce mode <br>- Releases are manual, but low friction                                                                                       | - Automated model trainin <br>- Centralized tracking of model training performanc <br>- Model management                                                        |
| 3     | Automated Model Deployment      | - Releases are low friction and automati <br>- Full traceability from deployment back to original dat <br>- Entire environment managed: train > test > production                                                   | - Integrated A/B testing of model performance for deploymen <br>- Automated tests for all cod <br>- Centralized tracking of model training performance          |
| 4     | Full MLOps Automated Operations | - Full system automated and easily monitored <br>- Production systems are providing information on how to improve and, in some cases, automatically improve with new model <br>- Approaching a zero-downtime system | - Automated model training and testin <br>- Verbose, centralized metrics from deployed model                                                                    |

The tables that follow identify the detailed characteristics for that level of process maturity. The model will continue to evolve.

> [!NOTE]
> A/B is not part of the course
