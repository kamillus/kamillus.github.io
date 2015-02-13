---
layout: post
title:  "Machine learning using scikit-learn"
date:   2015-02-13 08:44:30
categories: machine learning, scikit
---
Scikit-learn is a fantastic library to solve problems using machine learning and other, more traditional statistical methods. One of the problems I was working on not too long ago was classifying which user is at the front of the computer. I have developed a small [user classifying](https://github.com/kamillus/text_profile) game utilizing an [SVM](http://en.wikipedia.org/wiki/Support_vector_machine). The game asks a user for a bunch of words to create a profile of the user. In the next part of the game, the user types a bunch of words and the computer tries to recognize who is at the front of the keyboard.

How does the computer learn? The [feature](http://en.wikipedia.org/wiki/Feature_%28machine_learning%29) generation is accomplished when the user is asked for their name, then presented with a series of words from a dictionary and finally asked to type words as they appear. The features that is recorded is the typing speed, number of errors, and corrections made to typed words.

The next part of the program is to run the data through the classifier (which in our case is SVM). The tricky part is to get the right values for gamma. You could experiment with this by using a [test data set](http://en.wikipedia.org/wiki/Test_set) as opposed to your [training set](http://en.wikipedia.org/wiki/Training_set). Once you have this data, the actual classifying is trivial with scikit-learn:


    classifier = svm.SVC(gamma=1)
    (features, targets) = profiles.get_classifier_data()
    
    classifier.fit(features, targets)
    predicted = classifier.predict([[data_point.time, data_point.error_count, data_point.distance]])


How could this be improved? I think the first opportunity for improvement is to recognize data clusters automatically using k-means and possibly utilize [principal component analysis](http://en.wikipedia.org/wiki/Principal_component_analysis). That way, every cluster of data will be automatically assigned without first creating user profiles.

I hope this post elucidates the high level machine learning process for anyone that is interested.

[Full Listing](https://github.com/kamillus/text_profile/blob/master/learn.py)