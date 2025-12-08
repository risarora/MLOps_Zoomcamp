# Batch deployment of model

Typical approach for deploying a model in batch model:

- Create a notebook/training script to train a model and save it
- Create a notebook to load the trained model and make prediction on the new data
- Convert the notebook to an inference script
- Clean and parameterize the script
- Schedule the inference script if required

We will use the same taxi duration prediction example here.

**Step 1: Train the model and save the artifacts**

- If the model is not trained yet we got train first. Since as per the homework we need to train the model on FHV datasets, I am training the model from scratch here.

  Connect to EC2 server and create a new virtual environment

  ```bash
  mkdir batch-train
  cd batch-train
  pipenv shell --python=3.9
  pipenv install scikit-learn==1.0.2 flask gunicorn mlflow boto3
  ```

- Train random forest regressor model for the fhv taxi dataset  
  [Jupyter notebook for training model](/Week4/batch-train/fhv-taxi-duration-training.ipynb)

  Take a note of the full path from artifact section in mlflow ui

**Step 2: Notebook for fetching the model and predicting**

- Connect to EC2 server and create a new virtual environment
  ```bash
  mkdir batch-inference
  cd batch-inference
  pipenv shell --python=3.9
  pipenv install scikit-learn==1.0.2 prefect mlflow pandas boto3 pyarrow s3fs
  ```
- Copy the training notebook and change it for prediction, say, score.ipynb.

  [score notebook](/Week4/batch-inference/score.ipynb)

  Once the notebook code successfully runs convert that to python script.

  ```cp
   jupyter nbconvert --to script score.ipynb
  ```

- Clean and parameterize the prediction script score.py  
  [Clean code in score.py](/Week4/batch-inference/score.py)

![](/Week4/img/scorerun.png)

**Step 3: Dockerise the script [Homework]**  
[Pending] This is yet to be completed.
