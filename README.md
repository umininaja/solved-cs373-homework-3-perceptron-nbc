Download Link: https://assignmentchef.com/product/solved-cs373-homework-3-perceptron-nbc
<br>
In this homework, you will be working with the ‘Review Polarity’ dataset. You are given movie reviews and the task is to classify them as positive or negative. The entire dataset has 1000 movie reviews, out of which 500 are labeled positive and the other 500 are labeled as negative. The dataset is split into training (train.tsv) and test (test.tsv) sets. Training set consists of 699 instances and the test set has 301 instances. Look into the training set file and try to gauge the nature of the data and the task.

Your submission will be tested on a hidden dataset which is different from given dataset. The hidden set would have similar number of instances and data splits.

<strong>Input: </strong>Movie review consisting of a few sentences of text.

<strong>Label: </strong>Positive (+1)/Negative (−1)

The features you will use for the classification task are bag-of-words. Provided skeleton code has 2 feature extractors already implemented. The first feature extractor extracts binary word presence/absence and the second feature extractor extracts word frequency. You are free to implement and add any features that you believe would help you get a better performance on the task, but you can get full credit without using any extra features. Top-10% submissions according to the performance on the hidden test set will be given extra credit. You might need to use additional features to get extra credit. You are allowed to use libraries such as NLTK or Spacy to extract those features.

<h2>1.1         Skeleton Code</h2>

You are provided a skeleton code with this homework. The code has the following folder structure:

cs373-hw3/ handout.pdf data/ given/ train.tsv test.tsv

src/ init .py main.py classifier.py utils.py config.py naive bayes.py perceptron.py report/ report.pdf

<strong>Do not </strong>modify the given folder structure. You should not need to, but you may, add any extra files of code in cs373-hw3/src/ folder. You should place your report (report.pdf) in the cs373-hw3/report/ folder. You <strong>must not </strong>modify init .py, main.py or classifier.py. They may be replaced while grading. All your coding work for this homework must be done inside cs373-hw3/src/ folder. You are not allowed to use any external libraries for classifier implementations such as scikit-learn etc. Make sure that you understand the given code fully, before you start coding.

Your code will be tested using the command python2.7 main.py from inside the cs373-hw3/src/ folder. Make sure that you test your code on data.cs.purdue.edu before submitting. Output of the TA solution is given below. Your final numbers might differ. The given numbers are just a guideline, meant for sanity checking.

Perceptron Results:

Accuracy: 62.46, Precision: 97.27, Recall: 24.32, F1: 38.91

Averaged Perceptron Results:

Accuracy: 66.45, Precision: 91.21, Recall: 35.13, F1: 50.73

Naive Bayes Results:

Accuracy: 77.74, Precision: 78.72, Recall: 74.99, F1: 76.81

<h1>2           Perceptron</h1>

<h2>2.1         Theory</h2>

<ol>

 <li>(5 points) Perceptron model discussed in class is shown as:</li>

</ol>

(

1       if Σ<em>w<sub>j</sub>x<sub>j </sub>&gt; </em>0

<em>f</em>(<em>x</em>) =

0       if Σ<em>w<sub>j</sub>x<sub>j </sub></em>≤ 0

The <em>bias </em>term is missing in the shown equation. Write the equation with the <em>bias </em>term included. Is perceptron with a <em>bias </em>term more expressive (can represent more classification scenarios) compared to the one without bias? Why or why not?

<strong>P.T.O</strong>

<ol start="2">

 <li>(5 points) Given below are four figures that show the distribution of data points with binary classes. The two colors denote the different classes. For each of these, reason whether the following would give a high(<em>&gt; </em>0<em>.</em>95) classification accuracy.

  <ul>

   <li>a perceptron without bias</li>

   <li>a perceptron with bias</li>

  </ul></li>

 <li>(5 points) What is the update rule for the <em>bias </em>term <em>b </em>of a vanilla perceptron, given the learning rate <em>γ </em>and gold label <em>y</em>, when the classifier label doesn’t match the gold label during training? What is the update rule when the classifier label matches the gold label?</li>

</ol>

<h2>2.2         Implementation</h2>

You need to implement a vanilla perceptron and an averaged perceptron model for this part. Both the models should be implemented with a bias term. This part could be completed by editing only perceptron.py, unless you plan to extract any new features for the task. You need to initialize the parameters ( init () method), learn them from training data (fit() method) and use the learned parameters to classify new instances (predict() method) for each of the models. Take note that init .py, main.py and classifier.py may be replaced while grading. Do not make any modifications to these files. You need to follow the description of the models discussed in the lecture slides <a href="https://piazza.com/class_profile/get_resource/jqlonlli5gd3cb/jsni5ek0m7y5m8">(link)</a>. Report the results obtained on the given test set for both the models in your report. You should submit your code with the hyperparameter settings (config.py) that produce the best performance.

<h1>3           Naive Bayes</h1>

<h2>3.1         Theory</h2>

<ol>

 <li>(5 points) Given a text document <em>d </em>which is a sequence of words <em>w</em><sub>1</sub><em>,w</em><sub>2</sub><em>,…,w<sub>n</sub></em>, we want to compute <em>P</em>(<em>c</em><sup>+</sup>|<em>d</em>) and <em>P</em>(<em>c</em><sup>−</sup>|<em>d</em>). We use Bayes theorem to estimate the probabilities. Compute the equation for <em>P</em>(<em>c</em><sup>+</sup>|<em>d</em>) in terms of <em>P</em>(<em>d</em>|<em>c</em><sup>+</sup>) using Bayes theorem.</li>

</ol>

<strong>P.T.O</strong>

<ol start="2">

 <li>(5 points) To estimate <em>P</em>(<em>d</em>|<em>c</em><sup>+</sup>) using the training data without making any assumptions, we need impractically large amounts of data. Let us say that the size of the vocabulary is <em>V </em>and length of all documents is exactly <em>l </em>(we can ensure this by padding shorter texts with dummy tokens). In a binary classification task, how many parameters do we need to learn, in order to correctly estimate <em>P</em>(<em>d</em>|<em>c</em><sup>+</sup>) for any given document without making independence assumptions?</li>

 <li>(5 points) If we make the unigram assumption, that is, if we assume that occurrence of each word in the document is independent of the other words, then how many parameters do we need to learn to be able to estimate <em>P</em>(<em>d</em>|<em>c</em><sup>+</sup>)?</li>

 <li>(5 points) In a binary text classification task, mention the equations you would use to estimate <em>P</em>(<em>c</em><sup>+</sup>) and <em>P</em>(<em>c</em><sup>−</sup>) from the training data (<em>c</em><sup>+ </sup>and <em>c</em><sup>− </sup>are the two classes for the classification problem).</li>

</ol>

<h2>3.2         Implementation</h2>

You need to implement a Naive Bayes classifier for the given task. This part could be completed by editing only naive bayes.py, unless you plan to extract any new features for the task. You need to initialize the parameters ( init () method), learn them from training data (fit() method) and use the learned parameters to classify new instances (predict() method). Take note that init .py, main.py and classifier.py may be replaced while grading. Do not make any modifications to these files. You need to follow the description of the model discussed in the lecture slides <a href="https://piazza.com/class_profile/get_resource/jqlonlli5gd3cb/jsni5ek0m7y5m8">(link)</a>. Report the results obtained on the given test set in your report. You should submit your code with the hyperparameter settings (config.py) that produce the best performance.

<h1>4           Analysis</h1>

You need to perform additional experiments to answer the following questions. You don’t need to submit your code for this part. You only need to include your plots and discussions in your report. Make sure that the code you submit doesn’t include any changes you don’t want to be included, as that might affect your chances of getting extra credit.

<ol>

 <li>(5 points) Remove the bias term from the Perceptron and Averaged Perceptron and report the performance of the models. Is the performance better or worse than the respective models with a bias term? Discuss in one sentence.</li>

 <li>(5 points) Plot a graph of test accuracy vs number of iterations for Averaged Perceptron for number of iterations = { 1, 2, 5, 10, 20, 50 }. Does Perceptron converge i.e. does the training accuracy become 100? If yes, after how many iterations? If not, why?</li>

 <li>(5 points) Plot graphs of Naive Bayes test accuracy vs vocabulary size, Averaged Perceptron test accuracy vs vocabulary size for vocabulary sizes = {100, 500, 1000, 5000, 10000, 20000}. How does the performance change? Discuss in two sentences.</li>

</ol>

<h1>5           Time Limit</h1>

Your code must terminate with in 2 minutes for all 3 models combined together. If it doesn’t terminate with in 2 minutes, you will be graded for the output your code generates at the end of the 2 minute time limit.

<h1>6           Extra Credit</h1>

Your submission will be evaluated on a hidden dataset of similar nature. The hidden dataset is of similar size and splits. Top-10% (17 in number) of the students in the class would be awarded 10 extra credit points. You are not allowed to use any optimization libraries but you are allowed to use feature extraction software. If in doubt, ask a question on piazza and the instructors would respond. Remember that the extra credit only depends on the results on the hidden dataset. Overfitting the given dataset might prove counter-productive.