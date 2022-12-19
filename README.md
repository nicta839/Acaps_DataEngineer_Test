# Data Engineer test assignment

This repository contains my solution to the Data Engineer test assignment given by ACAPS. The objective of this project is to evaluate Machine Learning (ML) skills with a focus on natural language processing (NLP).

The scenario given is the following:
Imagine you are working in a company that provides services to academic institutions. One of the services the team plans to develop is to classify a corpus of academic papers in real-time. The team wants academic institutions to access the service via website, or mobile application. They can upload an archive of files in .zip or .tar and the files could be of different types -.doc, .docx, .pdf, .html, .txt. The team expects that they will start with a small number of users first (3-4 users uploading files daily), but plan to scale up to 30000 users per day. Assume that the average .zip or .tar archive will have around 20000 papers to classify. You decide that you want to focus on abstracts classification first. The team still has not decided on the product output, i.e., how and in what format results will be provided to the clients.

## Prototyping the model
The first task consists in prototyping a classifier to classify articles falling under the "Computer Science", "Mathematics", "Physics" and "Statistics" categories. The other categories provided are ignored (as per instructions).

The second task consists in including at least two evaluation metrics on the test dataset, one of which is the area under the ROC curve, and the other should be a metric of our choice relevant to this problem. These metrics should showcase the classification of the topic "Statistics".

### Data cleaning and exploration

The first task consisted in removing irrelevant columns and formatting the data such as one-hot-vectors were removed and replaced by class representation (numbers 0-3 representing respectively "Computer Science", "Mathematics", "Physics" and "Statistics" in order).

Two data sets were then produced. One using the full dataset and another that was under-sampled to avoid sample distribution bias. Both these dataset abstract were then normalized and stored in data/processed file.

### Model selection

Several models were attempted. First using different representations for word vectors (count vectors, tfidf vectorization, embeddings) and different classifiers (logistic regression, random forest classifier and BiLSTM). Using cross validation for baseline models and dropout layer for regularization in the case of the BiLSTM, metrics were produced that showed that the best model to use is the Logistic Regression with Tfidf-vectorizer. We used the under-sampled dataset for training as it removes class distribution bias.

### Model evaluation

To evaluate the model, we use precision, recall, accuracy and f1-score to measure the performance of the model both class-wise and overall for the model. We present below the best performing model parameters as well as the ROC AUC as asked in the task for the "Statistics" class in a one-vs-rest way.

|                  | Precision | Recall | f1-score |
|------------------|-----------|--------|----------|
| Computer Science | 0.86      | 0.80   | 0.83     |
| Mathematics      | 0.86      | 0.92   | 0.89     |
| Physics          | 0.98      | 0.95   | 0.96     |
| Statistics       | 0.64      | 0.74   | 0.69     |
|                  |           |        |          |
| Accuracy         |           |        | 0.86     |
| Macro avg.       | 0.83      | 0.85   | 0.84     |
| Weighted avg.    | 0.86      | 0.86   | 0.86     |


![alt text](../reports/figures/ROC_AUC.png)

We also present the confusion matrix for further reference

![alt text](../reports/figures/CM.png)

## Workflow description and considerations

We invite the reader to go to the [report](../reports/description_considerations.pdf) for the second part of the assignment and the answers to those questions.

## Installation and usage

First clone the repository in your directory of choice. Then install the required packages in your environment of choice using:

```bash
pip install -r requirements.txt

```
The code is located under [notebooks](../notebooks/). The notebooks `0.2_Modelling_baselines` and `0.3_BiLSTM_model` are lengthy to compute without the appropriate CPU and GPU resources, respectively. We suggest to run the data cleaning and performance metrics notebooks to check that the code is working.

## License

[MIT](https://choosealicense.com/licenses/mit/)


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
