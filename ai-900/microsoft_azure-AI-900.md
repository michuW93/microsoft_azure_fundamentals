# What is AI?
Simply put, AI is the creation of software that imitates human behaviors and capabilities. Key workloads include:

* Machine learning - This is often the foundation for an AI system, and is the way we "teach" a computer model to make predictions and draw conclusions from data.
* Anomaly detection - The capability to automatically detect errors or unusual activity in a system.
* Computer vision - The capability of software to interpret the world visually through cameras, video, and images.
* Natural language processing - The capability for a computer to interpret written or spoken language, and respond in kind.
* Knowledge mining - The capability to extract information from large volumes of often unstructured data to create a searchable knowledge store.

![image](https://github.com/michuW93/microsoft_azure_fundamentals/assets/16575035/43e1ca69-3779-440d-9849-9fd4c1430ba8)

# Anomaly detection - anything that deviates from the standard pattern:
1. Sensors in the car collect telemetry, such as engine revolutions, brake temperature, and so on.
2. An anomaly detection model is trained to understand expected fluctuations in the telemetry measurements over time.
3. If a measurement occurs outside of the normal expected range, the model reports an anomaly that can be used to alert the race engineer to call the driver in for a pit stop to fix the issue before it forces retirement from the race.

# Computer vision
is a field of computer science that focuses on enabling computers to identify and understand objects and people in **images and videos**. Like other types of AI, computer vision seeks to perform and automate tasks that replicate human capabilities. Type of computer vision: face detection, optical character recognation etc.

# Natural language processing (NLP)
is the area of AI that deals with creating software that understands written and spoken language. <br>
NLP enables you to create software that can:
Analyze and interpret text in documents, email messages, and other sources.
Interpret spoken language, and synthesize speech responses.
Automatically translate spoken or written phrases between languages.
Interpret commands and determine appropriate actions.

# Knowledge mining
Knowledge mining is the term used to describe solutions that involve extracting information from large volumes of often unstructured data to create a searchable knowledge store. In azure there is Azure Cognitive Search

# Machine learning
Machine Learning is the foundation for most artificial intelligence solutions. Creating an intelligent solution often begins with the use of machine learning to train predictive models using historic data that you have collected.
Azure Machine Learning is a cloud service that you can use to train and manage machine learning models.


Types of machine learning
There are two general approaches to machine learning, **supervised** and **unsupervised** machine learning. In both approaches, you train a model to make predictions.

The supervised machine learning approach requires you to start with a dataset with known label values. Two types of supervised machine learning tasks include regression and classification:
* **Regression** (predicting numeric values): used to predict a continuous value; like a price, a sales total, or some other measure.
* **Classification** (predicting categories or classes): used to determine a class label; an example of a binary class label is whether a patient has diabetes or not; an example of multi-class labels is classifying text as positive, negative, or neutral.
* **Time series forecasting** (predicting numeric values at a future point in time)


The unsupervised machine learning approach starts with a dataset without known label values. One type of unsupervised machine learning task is clustering.
* **Clustering**: used to determine labels by grouping similar information into label groups; like grouping measurements from birds into species.

Machine learning is a technique that uses mathematics and statistics to create a model that can predict unknown values.

Machine learning process:
* Prepare data: Identify the features and label in a dataset. Pre-process, or clean and transform, the data as needed.
* Train model: Split the data into two groups, a training and a validation set. Train a machine learning model using the training data set. Test the machine learning model for performance using the validation data set.
* Evaluate performance: Compare how close the model's predictions are to the known labels.
* Deploy a predictive service: After you train a machine learning model, you can deploy the model as an application on a server or device so that others can use it.

The difference between the predicted and actual value, known as the **residuals**, indicates the amount of error in the model.
