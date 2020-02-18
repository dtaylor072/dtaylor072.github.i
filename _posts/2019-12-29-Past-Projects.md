---
layout: post
title: Past Projects and Site Roadmap
date:   2019-12-29 17:56:00 -0500
icon: /images/profile_image.png
---
<!--more-->

For the first post on this site, I thought it would be a good exercise for me to document a couple of the  projects that I've worked on in the past semester in school. At the end of this post, I will be giving a rough roadmap for what's to come in future posts.

___
## Project 1: [Visualizing TED Talk Topics](https://github.com/esegaul/tedtalkvis)
<div class="img-container">
<img src="/post_assets/2019-12-29/vis_screenshot.png">
</div>
This is a project that I completed with two other group members for our final project in "CS 3891: Data Visualization" at Vanderbilt, also in the Fall of 2019. We first found a Kaggle dataset with details and text transcripts for every TED Talk ever given, and we used the transcripts with **Non-Negative Matrix Factorization** to label each talk with a predicted "topic". We then used D3.js to visualize the topics and explore how talk topics relate to other talk aspects (date and user reaction). Each topic is described by a group of 5 words, which are visible on the x-axis of the parallel coordinates plot below. My portion of the project was the topic modeling and parallel coordinates plot, so I'll describe both of those a bit. For all of the talk transcripts, I use [tf-idf](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) to create a tf-idf matrix $$V$$ of dimension $$ m \times n$$, so there are $$n$$ documents (talks), each indexed by $$m$$ words. tf-idf helps us to weed out stop words and find the words that explain the most variance between talks. This is almost reminiscient of applying PCA to each document. Then, NMF works in the following way: given our TFIDF matrix $$V$$, we can find a decomposition $$V = WH$$, where $$W$$ is an $$m \times 10$$ features matrix and $$H$$ is a $$10 \times n$$ weights matrix (we can choose any number of topics, but 10 seemed to work best for the given set of documents). The [coordinate descent algorithm](https://en.wikipedia.org/wiki/Coordinate_descent) then iterates so as to minimize the error $$ \epsilon = {\Vert V - WH\Vert}_F$$ subject to the constraint that all entries of $$W$$ and $$H$$ must be, you guessed it, non-negative. We can interpret the column vectors of $$W$$ as weights for each tf-idf word for a given topic, and the column vectors of $$H$$ as weights of each topic for a given document. Then, each document is expressed as a linear combination of topic features (columns in $$W$$), where the constants are determined by rows of $$H$$. Conveniently, NMF minimizes the Frobenius norm, so we are implicitly clustering the documents into topic groups in $$10$$-dimensional space. It is [in this way](https://www.cc.gatech.edu/~hpark/papers/GT-CSE-08-01.pdf) that we can think of NMF as closely-realted to K-means  clustering. We then chose to select the 5 words that are the most "characteristic" for each topic (the 5 words with the highest weights in each row of $$W$$) and display those as our learned "topics". In the parallel coordinates plot below, each line represents a talk, and the values along the y-axes are the weights that each talk is assigned for each topic along the x-axis. Hovering allows one to inspect the talk title as well as each of its topic weights. I was surprised with the accuracy of NMF upon inspection, as each of the documents is very long (they're entire lecture transcripts) and contain a lot of useless noise. Combining the topic modeling results interactively with other features such as date and user reaction allows for some interesting analysis, which I highly suggest viewing (instructions in the repo's `README.md`, the link to which is embedded in the heading of this paragraph). This project definitely turned my attention to the world of dimensionality reduction techniques, and I'm hoping to do some exploring of alternate techniques in the future.
<div class="img-container">
<img src="/post_assets/2019-12-29/pcoords.png">
</div>

___

## Project 2: [Predicting Airbnb Prices](https://github.com/dtaylor072/nashville_airbnb)
<div class="img-container">
<img src="/post_assets/2019-12-29/price_map.jpg" style="height:300px">
</div>
This is a machine learning project that I completed for "ECON 3750: Econometrics for Big Data" at Vanderbilt in the Fall of 2019. I found data for every Airbnb listing in Nashville on [InsideAirbnb.com](http://insideairbnb.com/nashville/), and I used that data to build out an XGBoosted Regression model to try and predict the prices of unseen listings. After tuning the hyperparameters of the model, I analyzed the importance of each feature to the model, as measured by the overall information gain provided by each feature. Although this type of project is a well-travelled path in the world of ML, I found this project interesting for several reasons: 1) I was able to apply advanced ML techniques to a phenomenon unfolding in the neighborhood around my school, and 2) I found that the most important feature in the XGBRegressor model was the number of listings that the host has, suggesting that large-scale hosts have a great deal of power in the short-term rental market in Nashville (and this is a [debated topic](https://www.tennessean.com/story/money/2019/05/02/nashville-cracking-down-illegal-short-term-rentals/3629030002/)). It was a nice feeling to finally bring ML to topic that affects my immediate surroundings, rather than just a dummy dataset used for instructional purposes. I was also pleasantly surprised by the performance attained with XGBoosting, as I had never used that model before. Although this project was fairly simple, it was good for me to get more repetitions with regression techniques and feature engineering. A more detailed, formal write-up of my findings can be found [here](https://github.com/dtaylor072/nashville_airbnb/blob/master/final_note.pdf), and the source code for the modeling can be found [here](https://github.com/dtaylor072/nashville_airbnb/blob/master/modeling.ipynb).  

___
## Site Roadmap:
There are several topics that I'm planning to work on and research in the coming months. First, I will be beginning preliminary research for my senior honor's thesis in math, which I'm hoping to carry out in the study of [Optimal Transport Theory](http://www.math.cmu.edu/~mthorpe/OTNotes). It seems to me that the study of OT is a perfect combination of rigorous theory-building with computational applications (in deep learning, specifically image processing). I plan to write several posts on ideas relating to OT as I get myself up to speed on the topic in the coming months. I'm also in the process of completing Facebook's [Intro to Deep Learning with PyTorch](https://www.udacity.com/course/deep-learning-pytorch--ud188) course on Udacity, so I'm hoping to get to work building deep neural networks with PyTorch and documenting them in posts on this site. Besides those two main topics, I have compiled a list of several random topics that I'm hoping to explore both theoretically and in application in coming posts:
- Force-directed Graph Layouts
- Kernel Density Estimation
- Principal Component Analysis
- Manifold Learning
- t-Stochastic Neighborhood Embedding (tSNE)
- Topological Data Analysis (TDA)

