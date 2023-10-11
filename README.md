# Human-level Semantic Score Prediction from Dialogue using BERT
## NLP, NLU Deep Learning Final Project

### Introduction
- Sentiment analysis is one of the most famous topic in natural language processing (NLP), used to determine whether data is positive, negative or neutral.
- Sentiment analysis researches are actively conducted using product reviews or movie reviews and so on.
- However, most of them are based on a single sentence.

<p align="center"><img src=https://github.com/kimchaeri/Human-level_Semantic_Score_Prediction_from_Dialogue_using_BERT/assets/74261590/78b9c221-6b31-49d6-bc19-acdb7a612735 width="800" height="200"></p>

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
 
<p align="center"><img src=https://github.com/kimchaeri/Human-level_Semantic_Score_Prediction_from_Dialogue_using_BERT/assets/74261590/d519d463-192b-456c-a0e7-19ee064b7d71 width="800" height="250"></p>

#### Word Embeddings
- We use BERT based multilingual cased pre-trained tokenizer consisting of 104 languages with the largest Wikipedia using a masked language modeling(MLM) objective to tokenize the dialogue made in Korean.
- We also used BERT-based word embedding to embed the tokenized words.
- This base embedding consists of word embedding, positional embedding, and tokenize embedding. To make the model recognize the speaker of the sentence, we added **turn embedding** on the base BERT embedding.
- We set the special tokens like CLS and SEP as 0, the first speaker started the conversation as 1, and the second speaker who is going to talk with the first speaker as 2.
<p align="center"><img src=https://github.com/kimchaeri/Human-level_Semantic_Score_Prediction_from_Dialogue_using_BERT/assets/74261590/6b74206b-a8fb-4e88-90bd-b6dd17d4d0b3 width="500" height="300"></p>

#### Model Architecture
- It consists of BERT layer, some fully connected layers, and a scoring matrix.
- We bring the base pre-trained BERT model for our baseline and modify it to have an ability to deal with turn-based knowledge. Then, we fine-tune it with many dialogue data which know the concept of turn and information about semantics between love and breakup.
- From the fine-tuned BERT, we can get the logits of the breakup, daily conversation, and love each.
- These results pass through two fully connected layers so that we can get the yardstick of break-up conversation, daily conversation, and love conversation between two speakers.
- Defined scoring matrix is used to predict the relation score.
- If you want more detailed information about scoring matrix, you can check 'paper' folder.
<p align="center"><img src=https://github.com/kimchaeri/Human-level_Semantic_Score_Prediction_from_Dialogue_using_BERT/assets/74261590/b27ef7eb-2c2d-45af-86b7-4f0d3e0916a0 width="700" height="300"></p>

### Dataset
#### Synthetic dataset
We use chatbot dataset, it is synthetic data and there are 11,876 pairs of questions and answers. It was produced by referring to the stories frequently found in Daum Cafe’s "Better than Love" in some breakup-related questions. In original data, daily conversations are
labeled 0, break-up conversations are labeled 1, and love conversations are labeled 2. We re-labeled the break-up dialogue as -1, the daily dialogue as 0, and the love dialogue as 1.

#### Real-world dataset
We use real-world messenger dataset. Everyone’s corpus is data released by the National Institute of Korean Language. There are 47,421 training examples. This data is not labeled, so we label 5,000 dialogues personally. In addition to the each speaker’s utterance,
this data includes various information such as the speaker’s gender and relationship. Based on this information, we label some data in rule-based.

### Result
- Our SSP model outperforms the baseline in the semantic analysis task with dialogue system.
- Even though our purpose is to predict the relation score, we used argmax to the output to calculate the accuracy because it is hard to label the dialogue data as score.
- But even we see this task as classification problem, the performance outperforms the baseline in most of metrics.

<table align="center">
  <caption>Result</caption>
  <tr>
    <th></th>
    <th>Accuracy</th>
    <th>Precision</th>
    <th>Recall</th>
    <th>F1 Score</th>
    <th>RMSE</th>
  </tr>
  <tr>
    <td>Baseline</td>
    <td>79.38%</td>
    <td><b>57.56%</b></td>
    <td>59.61%</td>
    <td>58.26%</td>
    <td>0.45</td>
  </tr>
  <tr>
    <td>SSP</td>
    <td><b>83.51%</b></td>
    <td>57.52%</td>
    <td><b>67.86%</b></td>
    <td><b>58.99%</b></td>
    <td><b>0.41</b></td>
  </tr>
</table>

