# Human-level Semantic Score Prediction from Dialogue using BERT
## NLP, NLU Deep Learning Final Project

### Introduction
- Sentiment analysis is one of the most famous topic in natural language processing (NLP), used to determine whether data is positive, negative or neutral.
- Sentiment analysis researches are actively conducted using product reviews or movie reviews and so on.
- However, most of them are based on a single sentence.

![previous_studies](https://github.com/kimchaeri/Human-level_Semantic_Score_Prediction_from_Dialogue_using_BERT/assets/74261590/78b9c221-6b31-49d6-bc19-acdb7a612735)

- There are few researches about sentiment analysis based on dialogue.
- Unlike previous researches that analyze sentiment in a sentence, we would like to analyze sentiment between people through sentiment analysis based on dialogue.
- For effective dialogue sentiment analysis, we propose a human-level Semantic Score Prediction(SSP) model which uses **turn embedding** that enables to know which speaker is speaking during conversation.
- In addition to semantic information of the sentence spoken by each speaker, the context of the conversation and the emotional information of each person can be learned to obtain a **relation score** between two people. By looking at the relation score, we can know the
degree of likability.

### Semantic Score Prediction(SSP) model
#### Overview
- In contrast to the basic semantic analysis models, Semantic Score Prediction (SSP) model tries to deal with the semantic analysis tasks as regression problems, not the classification problem.
- From pre-trained BERT, it is fine-tuned with the dialogue from multiple speakers.
- As the model can know which speaker said the input sentence, it can learn the context of the conversation and predict the relationship between the speakers.
 
![overview](https://github.com/kimchaeri/Human-level_Semantic_Score_Prediction_from_Dialogue_using_BERT/assets/74261590/d519d463-192b-456c-a0e7-19ee064b7d71)

#### Word Embeddings
