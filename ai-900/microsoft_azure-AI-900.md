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
4. Identify a fraudulent credit card payment.

# Computer vision
is a field of computer science that focuses on enabling computers to identify and understand objects and people in **images and videos**. Like other types of AI, computer vision seeks to perform and automate tasks that replicate human capabilities. 
Types of computer vision: 
* face detection (e.g for unblocking phone),
* optical character recognation - recognize text in images etc.
* identify handwritten letters

# Natural language processing (NLP)
is the area of AI that deals with creating software that understands written and spoken language. <br>
NLP enables you to create software that can:
Analyze and interpret text in documents, email messages, and other sources.
Interpret spoken language, and synthesize speech responses.
Automatically translate spoken or written phrases between languages.
Interpret commands and determine appropriate actions.

# Knowledge mining
Knowledge mining is the term used to describe solutions that involve extracting information from large volumes of often unstructured data to create a searchable knowledge store. In azure there is Azure Cognitive Search.

# Machine learning (technique that uses mathematics and statistics to create model that can predict unknown values)
Machine Learning is the foundation for most artificial intelligence solutions. Creating an intelligent solution often begins with the use of machine learning to train predictive models using historic data(dataset) that you have collected.
Azure Machine Learning is a cloud service that you can use to train and manage machine learning models.


Types of machine learning
There are two general approaches to machine learning, **supervised** and **unsupervised** machine learning. In both approaches, you train a model to make predictions.

The supervised machine learning approach requires you to start with a dataset(historical data) with known label values. Two types of supervised machine learning tasks include regression and classification:
* **Regression** (predicting numeric values): used to predict a continuous value; like a price, a sales total, or some other measure.
* **Classification** (predicting categories or classes using historical data with features): used to determine a class label; <br>
an example of a binary class label is whether a patient has diabetes or not; an example of multi-class labels is classifying text as positive, negative, or neutral. <br>
Metric to evaluate classification model is true positive rate. <br>
Example: predict wheather a student will complete an university course.
* **Time series forecasting** (predicting numeric values at a future point in time)


The unsupervised machine learning approach starts with a dataset without known label values. One type of unsupervised machine learning task is clustering.
* **Clustering**: used to determine labels by grouping similar information into label groups; like grouping measurements from birds into species or identify groups of people who have similar purchasing habits or segment customers into different groups to support a marketing department.

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
  
<b>Image classification</b> is the process of applying a label to the images and then service once trained will be able to classify and predict new images e.g cars. Accuracy is the calculated probability of a correct image classification.
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

<b>Analyzing Documents and Photos</b> - read text from the images of receipts, invoices and forms. It also uses OCR.<br>
Azure offers Document Intelligence - automates the process of extracting text from a document. It uses models that can interpret different fields.<br>
There are prebuilt models in Document Inteligence to read text from: Recepts, invoices, ID Documents, Contracts, Health Insureance Cards, US Tax Forms. But you can also create custom models or use general analysis<br>

<b>Analyzing video</b> - Azure AI Video Indexer which extract insights (e.g optical character recognition, labeling, etc.) from videos using video and audio models.
Video Features:
* Face detection - who appeard on the screen, how long he was on video
* OCR
* Content Moderation - e.g adult content
* scene changes
* people tracking - e.g when they appear or disappear on frame
* labeling

Audio features:
* transcription
* emotion detection - if someone is happy, sad etc.
* translation
* automatic language detecion
* keyword and named entity extraction


# Natural Language Processing - text analytics, speech and translation, language understanding.
* Interpret spoken language and synthesize speech e.g Sentiment determination, extract key phrases or summarize meeting
* speech to text or text to speech
* translate - natural language processing can translate spoken or written text between languages. You can talk in english and it will be translated to Polish.
* interpret commands and take proper actions (voice assistance e.g turn on light in kitchen)

Azure services: Azure AI Language Service (has it's own endpoint and key), Azure AI translator service, Azure AI speech. All of them are included into Azure AI Services

Text analytics - best used to examine and evaluate text for content, keywords, and more e.g what it is about. It can be used to determine if a review is in a different language, focused on the predominant language (when you have mixed 2 langauges it can tell which one is dominating). If the language can't be determined, it will return with unknown language and NaN.

Sentiment Analysis - determinate if the text is positive, neutral or negative. Each category is rated from 0 to 1. It also extract keywords from text.

Entity recognition - returns a list of entities in the text and the category they're assigned to. So when we provide text it will categorize e.g Marek is person, 1 p.m is DateTime, Ostrow Wielkopolski is location.

PII (Personally identifiable information) detection - identify, categorize and redact PII (phone numbers, email addresses etc.)

How AI is doing text analytics?
1. Text normalization - removes punctuation and changes words to lower case.
2. Stop word removal - is the process of excluding words e.g it, the, a
3. N-grams are multi-term phrases e.g 'I have'
4. Stemming allows you to cosolidate similar words e.g benefactor, beneficial could be the same token



Speech recognition - taking spoken language and convert it into data or text. The spoken language can be either live audio or an audio file. It can be automated note-taking or creating a transcript from discussion, phone call etc. Speech to text API

Speech synthesis - like Speech recognition but other side - we take text and convert it into speech e.g GPS. Text to speech API.

Text translation - translate text or documens to another language. Azure AI translator is ONLY focused on text-to-text translation, it supports over 90 langauges. Also we cna translate documents to another language, extension doesn't matter e.g pdf, excel, word. You can also create custom translation.

Additional features:
* Automatic language detection,
* dictionaries,
* profanity filters

  Translation of spoken language: Translate directly (speech to speech), automatic translation during a presentation, translate spoken language into text (speech to text)


Language understanding - example is home assistance.
3 concepts of language understanding:
* Utterances - A phrase we say to the AI - turn on the living room lights
* Entities - An item the phrase refers to - turn on the living room `lights`
* Intent - purspose or goal of the phrase - `turn on` the living room lights

Metrics to evaluate model:
* Precision - percentage of correct positive predeictions out of all the positive predictions made
* Recall - percentage of actual positives that your model correctly identified
* F1 score - single metric that combines precision and recall

Asking questions and getting answers - chat bots.
To teach chat bot you need to build knowledge base. You can do it by:
* Azure AI Language can create our knowledge base
* generate Q&A pairs from FAQ documents
* import them from a chit-chat data source
* input the questions and answers manually

# Generative AI - write a receipe, create code in a wide variety of languages, create a function, troubleshooting, creating images. It's different from traditional AI, it's creating something new.
How it works? It uses LLM (Large Language Models e.g GPT, Llama, Bard). Large language model is trained off of data.
![image](https://github.com/user-attachments/assets/03708503-d49f-4b7e-b635-2eee42d24782)
When we write prompt e.g `go to the zoo`, it's translated into tokens 112, 31, 43, 2341.

Copilots - generative AI assistants







Accountability(odpowiedzialność) e.g implementing processess to ensure that decision made by AI systems can be overriden by humans.<br>
Fairness(uczciwość) - AI systems should not reflect biases from the data sets that are used to train the systems.<br>
Feature engineering - Splitting a date into month, day and year fields<br>
Automated machine learning is the process of automating the time consuming, iterative tasks of machine learning model development. It works by running multiple training iterations that are scored and ranked by the metrics you specify.<br>
Labelling is the process of tagging training data with known values.<br>
Form recognizer to extract text, key/value pairs and table data automatically from scanned documents.<br>
Conversational AI - It can be an automated chatbot to answer questions about refunds and exchanges.


Document base on Clint Bonnett videos on Plurarsight.
