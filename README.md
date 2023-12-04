# SafeComm Digital Security Solutions
# By Bogdan Iavorskii, Savva Krasnokutskii, Spinghar Kochai

# Section 1 - Introduction

We are given a dataset of SMS data, each entry has it's own unique ID, date of sending, text of the SMS itself and finally a label, telling whether it is fraudulent or not. Our aim for the project is, applying all the knowedge we got during the semester, to design a model which would be able to identify the message (whether it is legit or a fraud). The dataset is quite small.

# Section 2 Methods

Preproccesing. The data obviously was needed to be preprocesed. We used pandas library for that. We checked for presense of Null or invalid values. We took a look on the distribution of the dataset and made some analysis of it (See ipynb file for more detalis). After we were done with the preproccesing we started to think on how to approach the data. There were 2 major things to be done, first of all we needed top identify the type propblem we are solving, second of all we needed to somehow deal with the fact that the data given is in the natural language, hence making our job of constructing model somewhat harder and requiring more steps.

A)Identifying the problem.
This was a classical example of classification problem, for which there are many potential methods like KNN, SVM, or even an artificial neural network. But before we choose which classification to use we still needed to solve a very important problem - dealing with natural language. 

B)Semantic analysis.
Now it was time to deal with semantic analysis, first we modified the given strings to get rid or hmlt references, special characters, punctuation and common, but meaningless words. Also we converted everything to lower case, the reason behind this was quite simple. In machine learning there is a big problem with dimentions, when the data feeded in the model is to complex it often worsens the performance and output correctness, because AI wastes time on unimportant stuff. So we did this dimention reduction so that the model with only work with important information, afterwards we vectorised the data, so that our model will have an expected type of input. For that we were using pre build libraries, because writing semantic analysis program from complete scratch would consume way to much time.

C)Choice of models
Here is the list of models we used and why did we choose them:

1)Artificial neural network: We used it, because artificial neural networks are very flexible and can take in very big amounts of data, which we will have, because the output of vectorizer function is massive. Also it is good in finding the important details from large amounts of data, which is helpfull for our case.

2)KNN: Despite KNN is not realy made for that complex data, we still decided to use it, because by studying cases, where model was wrongwe would be able to understand, the reasons behind it's failure, which would allow us to tune the future models better.

3)SVM: Most prominent method. Using this method we would be able to search niot just for linear rel;ationships, greatly expanding out capabilities, compared to KNN. Also it requires much less power then ANN, which is also good. Plus it does not need as much data as ANN, which is good for our dataset, since it is small.

After we were done with that all we needed to do was to plug the data into the given models and see how they perform. Later on we will use confution matrises and ROC curves for evalutation (Just like we did in class).

# Section 3 Experimental Design

I decided to use the validation methods, we were using in class, since they are reliable and tell us just enought information to understand model performance. By that I mean confusion matrix, there are already libraries in python to create it, so it is both usefull and simple to implement. Plus we know how to interpret the data we got easily, which makes them even better of a choice. We are using enitre confusion matrix, instead of just accuracy, because only one metric can sometimes be decieving, as we will see later.

# Section 4 

1)KNN (for visualisation please see ipynb file, there are confusion matrises plotted there)

Accuracy: 0.9576453697056713

Confusion matrix:

[[1183    2]
 [  57  151]]
 
Classification Report:

              precision    recall  f1-score   support

           0       0.95      1.00      0.98      1185
           1       0.99      0.73      0.84       208
    accuracy                           0.96      1393
   macro avg       0.97      0.86      0.91      1393
weighted avg       0.96      0.96      0.95      1393

We have got a pretty decent results. 95% accuracy is a good approximation for such a diffiult task (natural language).
Also confusion matrix is quite balanced. There are more FP than FN, but in general they are more or less balanced.
We can see that the model actualy tries to make a choice, instead of always guessing one particuklar value. The only downside
Is that rather often the fradoulent message is not being identified as such, which is a potential downside of our model.

2)SVM (for visualisation please see ipynb file, there are confusion matrises plotted there)

Accuracy: 0.9777458722182341

Confusion matrix:

[[1185    0]
 [  31  177]]
 
Classification Report:

              precision    recall  f1-score   support
           0       0.97      1.00      0.99      1185
           1       1.00      0.85      0.92       208
    accuracy                           0.98      1393
   macro avg       0.99      0.93      0.95      1393
weighted avg       0.98      0.98      0.98      1393

This is by far the best model we ever made. 97% Accuracy is very impresive, especially for the small train dataset we were given. Another good thing ss that we got no false positive (When running trials there sometimes were some but never >5). Meaning good messages are essentialy never marked as fraud. (Very high recall, thought not always 1, this run is an exception).
So the model will not intercept "good" messages, which is very important for us, since intercepting such message will be quite harmful to the users, even worse than accidently sliding couple of fradoulent ones.

3)Artificial neural network (for visualisation please see ipynb file, there are confusion matrises plotted there)

Accuracy: 0.8657573582196698

Confusion matrix:

[[1206    0]
 [ 187    0]]
 
Classification Report:

              precision    recall  f1-score   support
           0       0.87      1.00      0.93      1206
           1       0.00      0.00      0.00       187
    accuracy                           0.87      1393
   macro avg       0.43      0.50      0.46      1393
weighted avg       0.75      0.87      0.80      1393

Here we can see that since the dataset was unbalanced, the neural netowrk just decided to always label as message
As non fradulent, this strategy yields seemingly decent results, but is not good for us, since we actually want to
Get rid of the fraudulent messages. So we either should use more balance dataset, or resort to some other method. I
Would prefer to go back to SVM, since it's performance is already satisfactory.

# Section 5 Conclusion

From this project we have learned a lot. We understood, that it is possible to approach the same problem, from the multiple sides and that many different methods for the problem solutions might be valid. We also learned that the most complicated way is not nessesary the best one (artificial neural network). We also had some practical experince to apply the given knowedge on the real project. Also we were able to achive great accuracy in teaching the AI to understand the natural language, which was a great suscess. Initialy I never expected, that a result that high would be even possible.

For the future there is still some potential work to do. It would be good idea to try to implement the same code, without any libraries - completely from scratch. I think that it would give us even better understanding of the inner workings of semantic analysis. Also it would be a very good idea to work with a better dataset next time. 6783 Entires is not enought for any meaningfull machine learning project.
