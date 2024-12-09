# What is AI?
Simply put, <b>AI is the creation of software that imitates human behaviors and capabilities</b>. 
Key workloads include:

* Machine learning - This is often the foundation for an AI system, and is the way we "teach" a computer model to make predictions and draw conclusions from data.
* Anomaly detection - The capability to automatically detect errors or unusual activity in a system.
* Computer vision - The capability of software to interpret the world visually through cameras, video, and images.
* Natural language processing - The capability for a computer to interpret written or spoken language, and respond in kind.
* Knowledge mining - The capability to extract information from large volumes of often unstructured data to create a searchable knowledge store.
* generative AI - AI that can create original content such as text, images and code.

![image](https://github.com/michuW93/microsoft_azure_fundamentals/assets/16575035/43e1ca69-3779-440d-9849-9fd4c1430ba8)

Important terminology:
* features - historical data on which model will be trained
* label - what we want to predict

# Anomaly detection - anything that deviates from the standard pattern:
1. Sensors in the car collect telemetry, such as engine revolutions, brake temperature, and so on.
2. An anomaly detection model is trained to understand expected fluctuations in the telemetry measurements over time.
3. If a measurement occurs outside of the normal expected range, the model reports an anomaly that can be used to alert the race engineer to call the driver in for a pit stop to fix the issue before it forces retirement from the race.

# Computer vision
is a field of computer science that focuses on enabling computers to identify and understand objects and people in **images and videos**. Like other types of AI, computer vision seeks to perform and automate tasks that replicate human capabilities. Type of computer vision: face detection (e.g for unblocking phone), optical character recognation - recognize text in images etc.

# Natural language processing (NLP)
is the area of AI that deals with creating software that understands written and spoken language. <br>
NLP enables you to create software that can:
Analyze and interpret text in documents, email messages, and other sources.
Interpret spoken language, and synthesize speech responses.
Automatically translate spoken or written phrases between languages.
Interpret commands and determine appropriate actions.

# Knowledge mining
Knowledge mining is the term used to describe solutions that involve extracting information from large volumes of often unstructured data to create a searchable knowledge store. In azure there is Azure Cognitive Search

# Machine learning (technique that uses mathematics and statistics to create model that can predict unknown values)
Machine Learning is the foundation for most artificial intelligence solutions. Creating an intelligent solution often begins with the use of machine learning to train predictive models using historic data(dataset) that you have collected.
Azure Machine Learning is a cloud service that you can use to train and manage machine learning models.


Types of machine learning
There are two general approaches to machine learning, **supervised** and **unsupervised** machine learning. In both approaches, you train a model to make predictions.

The supervised machine learning approach requires you to start with a dataset(historical data) with known label values. Two types of supervised machine learning tasks include regression and classification:
* **Regression** (predicting numeric values): used to predict a continuous value; like a price, a sales total, or some other measure.
* **Classification** (predicting categories or classes using historical data with features): used to determine a class label; an example of a binary class label is whether a patient has diabetes or not; an example of multi-class labels is classifying text as positive, negative, or neutral.
* **Time series forecasting** (predicting numeric values at a future point in time)


The unsupervised machine learning approach starts with a dataset without known label values. One type of unsupervised machine learning task is clustering.
* **Clustering**: used to determine labels by grouping similar information into label groups; like grouping measurements from birds into species.

Machine learning process:
* Prepare data: Identify the features (values which we know from past) and label(value which we want to predict) in a dataset. Pre-process, or clean (e.g some rows can be empty) and transform, the data as needed. We can even normalize data - convert values to be on the same scale from 0-1.
* Train model: Split the data into two groups, a training and a validation set. Train a machine learning model using the training data set. Test the machine learning model for performance using the validation data set. This will enable us to compare actual values to predicted values.
* Evaluate performance: Compare how close the model's predictions are to the known labels.
* Deploy a predictive service: After you train a machine learning model, you can deploy the model as an application on a server or device so that others can use it.

The difference between the predicted and actual value, known as the **residuals**, indicates the amount of error in the model.

R2 score (from 0 to 1, the higher the better) - R-squared, also known as the coefficient of determination, is a statistical measure used in machine learning to evaluate the quality of a regression model. It measures how well the model fits the data by assessing the proportion of variance in the dependent variable explained by the independent variables

The Root Mean Squared Error (RMSE) is one of the two main performance indicators for a regression model (lower is better). It measures the average difference between values predicted by a model and the actual values. It provides an estimation of how well the model is able to predict the target value (accuracy). A 0 value indicates that the expected and actual values match precisely. Low RMSE values show that the model makes more accurate predictions and fits the data well. Higher levels, on the other hand, imply more significant mistakes and fewer accurate forecasts

# Computer vision (Analyze image and return information about them)

* Image Captions - short pharses or sentences that describe what is in the image. Running image analysis returns description and confidence. Confidence is from rango 0-1, 0 means it's totally inconfident and 1 means that it's confident about it's description.
![image](https://github.com/user-attachments/assets/415d69be-bb84-4768-a3d9-d04fc319a6b1)

* Tagging - return tags for an image with confidence e.g christmas(0.95), winter(0.9), gifts(0.75)
  ![image](https://github.com/user-attachments/assets/c27bbb0e-809f-4532-a8f1-870a94dda83a)

* Object detection - christmas tree (0.95), snowman(0.9). Bounding box is the location of the object on the picture.
* Facial detection - it's not facial recogination! It's just determines if there is a face on the photo.
* Optical character recogination (OCR) - read text from the image.

  Azure services for Computer vision:
  * Azure AI vision - interact using API (application programming interface) endpoint and key
  
<b>Image classification</b> is the process of applying a label to the images and then service once trained will be able to classify and predict new images e.g cars.
Object detection is  labeling the objects in our images and return bound boxes with probability.
Both image classification and object detection can be done on Custom Vision Portal.

<b>Face analyze</b><br>
To analyze face from photos but also from videos we can use Azure AI Face - can be used to detect, analyze and recognize faces.<br>
We can train model by adding some photos of person X and then service would be able to find face of person X on different photos, even when person X would have sunglasses, photos woudl be done from high angle etc. so it's not a problem to find face of person X on group photos. Azure AI Face also can find similar faces and group them together.<br>
Azure AI Face can also easily recognize if person is waering mask.<br>
For face details Azure AI Face is much better than Azure AI Vision. Azure AI Vision can detect face on photo but it's not providing all informations which we can see in Azure AI Service.<br>

<b>Reading text from images</b>
Optical character recognition (OCR) - model that is trained to recoginze text in an image. OCR can be used to read handwritted text or printed documents and it uses Read OCR Engine.

There are two Read OCR Engine Edition:
* images - optimised for non-document images e.g handwriting
* documents - optimized for text-heavy documents

Extracting text from an image. It's broke down to:
* pages
* lines - all words in all lines
* words - separately even if in the same line
