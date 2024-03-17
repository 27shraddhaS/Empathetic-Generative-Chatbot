# 3M-NLP-Chatbot

* **Project Title**: Topic-Based Empathic Chatbot
* **Description**:  The 3M-NLP Chatbot is an AI-based conversational agent capable of engaging in general talk while also offering factual information on Reddit topics encompassing healthcare, education, environment, politics, and technology. It uses advanced natural language processing techniques, notably Named Entity Recognition, Sentiment Analysis, and we fine-tune the pre-trained models to comprehend user queries and generate appropriate responses.
* **Getting Started**: <br />
!pip install transformers <br />
!pip install tensorflow_text <br />
!pip install sentence_transformers <br />
!pip install profanity-check <br />
!pip install transformers <br />
!pip install better_profanity <br />
!pip install flask_cors <br />
!pip install flask_ngrok <br />
!pip install pyngrok==4.1.1 <br /> <br />
Next step is to get the authtoken from ngrok.<br />
Login to ngrok https://ngrok.com/ and get the authtoken <br />
!ngrok authtoken <authtoken> <br /> <br />
You are set for hosting the flask app using ngrok.

* **Data pre-processing** <br />
To create a well structured data for further processing, we firstly take all the raw dataset.
- Chitchat dataset: https://github.com/BYU-PCCL/chitchat-dataset
- Empathetic dataset: https://github.com/facebookresearch/EmpatheticDialogues
- Reddit dataset: We extract the submissions and comments from reddit using the psaw API. The reddit_data_extraction.ipynb has the code for extracting topic based submissions and respective comments. <br/>

  The BERT_classifier_data_pre.ipynb has the code to preprocess all three datasets into a query-reply format. The Data_combining.ipynb combines the required fields from each dataset and agglomerates it into a single dataset. It has the training of a BERT classifier that determines which type of reply (chitchat vs reddit) is expected from the chatbot. We get the classifier model. <br />
Sentiment_NER_GPT2.ipynb performs some basic data cleaning and contains the code to import the pretrained GPT-2 model, perform NER and Sentiment analysis on the query, refine the query for fine-tuning of the GPT-2 model. The combined dataset is divided into batches of 64, split for getting train and test data and further training the model with custom dataset. We get the fine-tuned GPT-2 model.

* **Flask App** <br />
3M-NLP_flask_app.ipynb is the main file that integrates the three models and runs the flask app. It loads the fine-tuned GPT-2 model, BERT classifier model and has the RoBERTa pipeline for question answering. Once we run the app we get the interface for our chatbot. The entered query follows the pipeline by refining it and passing it to the loaded GPT-2 model. We get the context using cosine similarity function and append the GPT-2 reply to it. The query and context is passed through the RoBERTa pipeline to get the final reply.

* **Run** <br />
After getting all the models trained, the 3M-NLP_flask_app.ipynb file contains the main function that runs the app and passes the user query through the complete pipeline and returns the reply to the user.
  
* **Evaluation** <br />
The code for evaluation methods (BLEU & BERT) can be found in Sentiment_NER_GPT2.ipynb.
  
* **Team Members** <br />
Shraddha Shekhar,
Mayuresh Wagh,
Yash Joshi



