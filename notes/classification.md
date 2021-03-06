---
title: Classification
layout: note
---

# Classification

Classification is one of the primary, but not only, uses of machine learning. As with all machine learning operations, the goal is to train a model that, when combined with a corresponding inference algorithm, is able to estimate (infer/predict/guess) something about new, unseen data. For example, we might wish to have a machine that can estimate whether an email is spam or not. A machine learning approach to meet this goal is to train a model with lots of spam and non-spam messages. Once trained, this model can be applied to a new message.

## Issues to consider

There are several issues to consider when building a classifier:

- How do we obtain a sufficient amount of training data?
- What kind of model will we train and what inference algorithm will we use on this model? (Usually the choice of model and inference algorithm go together, as algorithms are usually designed to operate on one specific kind of model.)
- How will we know if our technique is good enough to apply to new, real cases?
- Related to the above point, but not equivalent: How do we act as proper scientists and evaluate our technique in a way that will pass peer review and contribute to the community's knowledge?

## Workflow

The diagram below shows a high-level viewpoint of the workflow of building a classifier. The workflow applies to machine learning problems in general, but our focus here is classification. Each step is described in more detail below the figure.

![Classification workflow](/images/classification-workflow.png)

### Data acquisition

Machine learning usually requires lots of training data. Depending on the procedure used and the difficulty of the classification problem, the number of distinct instances required may vary across several orders of magnitude. Some training algorithms, such as deep learning, proceed very slowly, and require a thousand or more instances. Some classification problems, such as face recognition or speech recognition, depend on very subtle differences among the classes (different faces, different words) and therefore require many instances of every variation in order to train a model on these subtle differences.

Note that the training data should structurally match data that will be encountered in real usage. This ensures the trained model will be able to utilize real data once deploy. The training data should also match the quality of real data, e.g., if real data is expected to be very noisy, the training data should be equally noisy.

Training data may be gathered from realistic scenarios or generated by simulations. Both approaches have advantages and disadvantages:

- Data from the real world will only represent real events, so rare events will likely only appear rarely or not at all. This makes it difficult to train a model to detect these rare events. On the other hand, real data will include mistakes and noise that reflect the real world; sometimes, these errors are not even noticeable by humans without careful analysis, yet the trained model may be able to discover and exploit them.
- Data generated from simulations can cover a wide range of scenarios at any degree of complexity, noise, and rarity. However, simulations often miss subtle variations that appear in real world data, and training with simulated data may produce a model that is only useful for classifying more simulated data but completely fail on realistic data.

### Data labeling

In this class, we will primarily look at *supervised machine learning*, meaning the training procedure exploits "groundtruth" labels on the data in order to train a model. In semi-supervised or unsupervised training, some or none of the data have groundtruth labels, so these labels may not be available to inform the training procedure if the model is learning the right facts.

Should supervised training be used, then all training data must be labeled ahead of time with groundtruth labels. If the data is produced from a simulation, this labeling is straightforward, since the simulator would be able to know what kind of example it has generated (e.g., an example of spam or non-spam). If the data is acquired from the real world, then some person must decide the labels. When humans are involved, we have to wonder if the human is producing correct labels.

### Train/test splitting

Once the data is labeled, it should be split into train/testing subsets. An 80%/20% split seems reasonable (80% for training). The testing set should not be revisited until we are finished training a model on the training set.

The purpose of splitting the data at this point is to ensure we're being scientific about our process. If we allow ourselves to build a model by training with all the data, and then testing the model on that same data, we risk training a model that more-or-less memorized that specific set of data. Such a model is useless in the real world since it learned the training data too specifically and did not learn any *generalizations* about the data. We also will be unable to convincingly argue that our model is useful if we test on the same data the model is trained on. Scientific studies usually have a "control" group for these purposes. The test set is our control group.

Not only should we separate the training and testing data, we should commit to not looking at the test data (perhaps we even leave it unlabeled until we're ready for final validation). We do not want to inadvertently learn some details about the testing data and factor those into our training procedure.

### Feature engineering, algorithm design

Now that the data has been split into training/testing, we can begin to analyze and process the training data, and feed it into a training procedure. First, we often want to manipulate the data into a form more appropriate for our training procedure. This is known as [feature engineering](/notes/feature-engineering.html). For example, many training procedures and their corresponding models cannot handle non-numeric data, so we'll either need to transform nominals (strings) into ordinals (numbers) by giving each distinct string a unique number, or dropping the nominal fields. We may also wish to fill in missing values with the average or min or max for that field, and may drop fields altogether if they are likely not to be useful.

There exist many different training procedures and models for classification. These include [k-nearest neighbor](/notes/k-nn.html), [decision trees](/notes/decision-trees.html), [neural networks](/notes/neural-networks.html), among others. Although each of these algorithms attempt to solve the same kind of problem (classification, namely), each has advantages and disadvantages for specific kinds of uses. These tradeoffs should be understood and the right procedure and model should be chosen for the "right reasons" (appropriateness for the task at hand, vaguely). Given the abundance of machine learning software, such as [Weka](/notes/weka-classification.html), there is often a tendency to just try every algorithm to see what works best on the training data, in terms of training accuracy. However, this approach can be less than ideal, as an algorithm may perform best (in terms of accuracy) on the training set but perform poorly on the test set because, for example, it does not generalize well on the kind of data to which it is applied.

### k-fold cross validation

In order to get an accurate picture of the accuracy of a particular training procedure, we have to be careful to evaluate the procedure on a different set of data than it was trained on. Note that we do not yet look at the test data segregated earlier. At this stage, we are only working with the training data. However, we do not want to train a model on all of the training data and then test on that same data, since the model may very well have "memorized" the training data (and thus will perform really well on when tested on the same data, but perform poorly in the real world or the segregated test data). Thus, we often employ [k-fold cross validation](/notes/classification-evaluation.html). Visit the linked notes for more details.

### Final validation

Assuming we're happy with our training procedure, we're ready to perform a final validation test on the segregated testing data. The model should be trained again, this time on all the training data (not using k-fold cross validation), and tested on the segregated test data. Note that this is the first (and only) time this test data has been used. The results on this final validation will most closely match those experienced in the real world on totally new data. These results are the only results that are appropriate for publication in a scientific venue. If we're not happy with the results, then we have some soul-searching to do (should we abandon the idea? was their something wrong with our workflow?).

