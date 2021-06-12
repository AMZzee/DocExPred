# DocExPred
Extraction and Contextual Classification of Documents based on confidentiality.

Through this system the Documents are classified as confidential or non-confidential.
It handles large documents as well and is capable of contextual analysis to understand the sentiment/context being expressed within a document to effectively predict its confidentiality.
This project uses BERT at its core and an additional LSTM layer that is appended to the BERT's output layer inorder to overcome BERT's limitation of 512 Tokens. Thereby supporting analysis of documents containing tokens less than or much more than 512 tokens.
It supports multiple document types - doc, docx, html, htm, txt and pdf. 
The data from these documents is extracted using textract and PyPDF.

The dataset used here is: https://www.kaggle.com/cfpb/us-consumer-finance-complaints
(As it contains a lot text records with more than 512 tokens).

## The Control and Data flow pipeline:

The Document data is split into chunks of 200 tokens and passed through BERT to get contextual Embeddings (pooled_output) for each text record (document).
This pooled output from BERT is formed into a dataset of embeddings and labels which is passed onto an additional LSTM layer which merges the chunks and retains BERT's classification.
The above step is basically what forms the connection between the LSTM layer and BERT's output layer.
Finally based on the categorization of the documents from the 10 classes defined within the preprocessed training data, the document's confidentiality is determined. 

Since the BERT model exported is an tf estimator model and the LSTM model is a keras model, both the models are required to be exported inorder to enable deployment of this system.

The exported fine-tuned BERT pre-trained model: https://drive.google.com/file/d/1yLJnjYNjranb5zAXXr_q883trF1aAxZx/view?usp=sharing
The exported LSTM keras model: https://drive.google.com/file/d/1--kvG6PlwLSmD834J0Bw9Fsa7efK8FJk/view?usp=sharing
