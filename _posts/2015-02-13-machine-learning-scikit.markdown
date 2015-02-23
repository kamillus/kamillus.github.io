---
layout: post
title:  "Machine learning using scikit-learn"
date:   2015-02-13 08:44:30
categories: machine learning, scikit
---
Scikit-learn is a fantastic library to solve problems using machine learning and other, more traditional statistical methods in the area of Data Science. In this post I'm outlining why machine learning is important, demonstrating a simple machine learning problem and how to solve it.

Why should you care? Data science is becoming more and more relevant with the growth of big data, and more autononomous systems (ex. [recommender systems](http://en.wikipedia.org/wiki/Recommender_system), [pattern recognition](http://en.wikipedia.org/wiki/Pattern_recognition)). Machine learning, specifically, is applicable to many fields including finance (ex. Detecting credit card fraud), medical (ex. Classifying patient cancer), entertainment (ex. Chess playing bot). The number of careers involving machine learning will steadily increase (there is evidence it's already [happening](http://www.indeed.com/jobtrends?q=machine+learning&l=&relative=1)) since the supporting technologies are becoming more prolific (Hadoop, scikit-learn, Mahout etc.). 

One of the problems I was working on not too long ago was classifying which user is at the front of the computer. I have developed a small [user classification](https://github.com/kamillus/text_profile) game utilizing an [SVM](http://en.wikipedia.org/wiki/Support_vector_machine). The game asks a user for a bunch of words to create a profile of the user - the machine is "learning". In the next part of the game, the user types a bunch of words and the computer tries to recognize who is typing at the keyboard by utilizing what it learned.

How does the computer learn? The [feature](http://en.wikipedia.org/wiki/Feature_%28machine_learning%29) generation is accomplished when the user is asked for their name, then presented with a series of words from a dictionary and finally asked to type words as they appear. The features that is recorded is the typing speed, number of errors, and corrections made to typed words.

The next part of the program is to run the data through the classifier (which in our case is SVM). The tricky part is to get the right values for gamma. You could experiment with this by using a [test data set](http://en.wikipedia.org/wiki/Test_set); do not use your [training set](http://en.wikipedia.org/wiki/Training_set). Once you have this data, the actual classifying is trivial with scikit-learn:


    #create the classifiter
    classifier = svm.SVC(gamma=1)
    #get existing features, and their expected results
    (features, targets) = profiles.get_classifier_data()
    classifier.fit(features, targets)
	
    #based on new features and targets feed into the program and guess the new predicted targets
    predicted = classifier.predict([[data_point.time, data_point.error_count, data_point.distance]])


How could this be improved? I think the first opportunity for improvement is to recognize data clusters automatically using k-means and possibly utilize [principal component analysis](http://en.wikipedia.org/wiki/Principal_component_analysis). That way, every cluster of data will be automatically assigned without first creating user profiles.

I hope this post elucidates the high level machine learning process for anyone that is interested. The technologies and ideas used here are just some tools that can be added to your toolbelt. If you'd like to find out more about machine learning, I recommend Andrew Ng's [set of lectures](https://www.youtube.com/view_play_list?p=A89DCFA6ADACE599).

[Full Listing](https://github.com/kamillus/text_profile/blob/master/learn.py)