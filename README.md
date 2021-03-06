# Slice Tuner: A Selective Data Acquisition Framework for Accurate and Fair Machine Learning Models

## Motivation
As machine learning becomes democratized in the era of Software 2.0, a serious bottleneck is acquiring enough data to ensure accurate and fair models. Recent techniques including crowdsourcing provide cost-effective ways to gather such data. 

However, simply acquiring data as much as possible is not necessarily an effective strategy for optimizing accuracy and fairness. For example, if an online app store has enough training data for certain slices of data (say American customers), but not for others, obtaining more American customer data will only bias the model training. 

## Slice Tuner
We contend that one needs to selectively acquire data and propose Slice Tuner, which acquires possibly-different amounts of data per slice such that the model accuracy and fairness on all slices are optimized. This problem is different than labeling existing data (as in active learning or weak supervision) because the goal is obtaining the right amounts of new data. At its core, Slice Tuner maintains learning curves of slices that estimate the model accuracies given more data and uses convex optimization to find the best data acquisition strategy. 

The key challenges of estimating learning curves are that they may be inaccurate if there is not enough data, and there may be dependencies among slices where acquiring data for one slice influences the learning curves of others. We solve these issues by iteratively and efficiently updating the learning curves as more data is acquired. We evaluate Slice Tuner on real datasets using crowdsourcing for data acquisition and show that Slice Tuner significantly outperforms baselines in terms of model accuracy and fairness, even when the learning curves cannot be reliably estimated. 

## Architecture

<p align="center"><img src=https://user-images.githubusercontent.com/67897374/106998345-b18ea300-67c7-11eb-8b3a-08174df3eebc.jpg></p>

Slice Tuner receives as input a set of slices and their data and estimates the learning curves of the slices by training models on samples of data. Next, Slice Tuner performs the selective data acquisition optimization where it determines how much data should be acquired per slice in order to minimize the loss and unfairness. As data is acquired, the learning curves can be iteratively updated. 
