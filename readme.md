# About

This project is about behavioural testing of a trained NLP model by using the **[checklist](https://github.com/marcotcr/checklist)** library from [Beyond Accuracy: Behavioral Testing of NLP Models with CheckList](https://aclanthology.org/2020.acl-main.442/).

## Model and Task
---------------------

A distill-bert based model was trained on the task:-

**Predict which Tweets are about real disasters and which ones are not**

### Example : 
- Tweet about real disaster : `South Japan is experiencing some earthquakes right now!`

- Tweet NOT about a real disaster : `This movie was a complete disaster! I hated it.`

It's not always clear whether a person's words are actually announcing a disaster.

dataset and more about the task - [here](https://www.kaggle.com/competitions/nlp-getting-started)

`training.py` has the training code.

`checklist-experiments.ipynb` contains all the checklist tests done on the model.

## Overview of training

We have a train dataset with list of tweets that are either "disaster tweets" or belong to the negative class.

[BERT](https://arxiv.org/abs/1810.04805) is a transformer based model, serves as a good baseline to get high accuracies on text classification tasks.

[Distill-BERT](https://arxiv.org/abs/1910.01108) is smaller version of BERT, made using the technique of distillation, with only a small compromise in metrics.

I use the distill-bert model and fine-tune it on the given text classificaition task. I use the pooled output from the transformer and attach a dropout and a simple output layer at the end.

This model gives a validation F1-score of 0.92

`After training, we save the trained model and use it in the checklist notebook.`



## Overview of the Checklist process

The main idea of the Checklist library is to create large number of diverse test examples and adversarially test the NLP model. It tests the linguistic capabilities of the model with a variety of test types. The concept is similar to software testing.

A Minimum Functionality test (**MFT**) is a collection of simple examples (and labels) to check a behavior within a capability. MFTs are similar to creating small and focused testing datasets, and are particularly useful for detecting when models use shortcuts to handle complex inputs without actually mastering the capability.

In the experments, I did 2 MFTs to check model's ability to predict positive and negative classes, generated using templates.


An Invariance test (**INV**) is when we apply label-preserving perturbations to inputs and expect the model prediction to remain the same.
Robustness to typos is one kind of invariance test, which is what I did in the experiments.

A Directional Expectation test (**DIR**) is similar, except that the label is expected to change in a certain way.
In the experiments, I add a simpe phrase "a fire then broke out" to the end of each sentence. Now we expect the probability of the positive class to not go down. This is what we test in the DIR test.




