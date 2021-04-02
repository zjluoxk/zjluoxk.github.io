---
layout: post
title:      "Quick Summary of Data Size Impact Model Accuracy"
date:       2021-04-02 04:25:50 +0000
permalink:  quick_summary_of_data_size_impact_model_accuracy
---


In my experience of fitting models and comparing their accuracy. It seems to me it's always the same or similar of how much complexity I added to the model.

For example, here's a simple base model:

*models[1] = Sequential([
        embeddinglayer,
        tf.keras.layers.Bidirectional(LSTM(128, returnsequences=True)),
        tf.keras.layers.Dropout(0.3),
        tf.keras.layers.Bidirectional(LSTM(128)),
        tf.keras.layers.Dropout(0.3),
        tf.keras.layers.Dense(64, activation='relu'),
        tf.keras.layers.Dense(1, activation='sigmoid'),
    ])*
		
		
Here is the more complex one:
tf.keras.backend.clear_session()
*models[4] = Sequential([
        embeddinglayer,
        tf.keras.layers.Bidirectional(LSTM(maxlength, returnsequences=True)),
        tf.keras.layers.Dropout(0.5),
        tf.keras.layers.Bidirectional(LSTM(maxlength, returnsequences=True)),
        tf.keras.layers.Dropout(0.5),
        tf.keras.layers.Bidirectional(LSTM(maxlength, returnsequences=True)),
        tf.keras.layers.Dropout(0.5),
        tf.keras.layers.Bidirectional(LSTM(maxlength)),
        tf.keras.layers.Dropout(0.5),
        tf.keras.layers.Dense(int(maxlength), activation='relu'),
        tf.keras.layers.Dense(int(maxlength/2), activation='relu'),
        tf.keras.layers.Dense(int(maxlength/4), activation='relu'),
        tf.keras.layers.Dense(1, activation='sigmoid'),
    ])*

Their accuracy is 0.67 and 0.70 respectively. 
Their AUC is 0.7469 and 0.7709.
Their time is 4min 1s and 8min 15s.

Despite the twice in computational time, both simple and complex model performance are nearly identical.

Then I set out to search for reason why.

I came across this presentation:
https://web.science.mq.edu.au/~mjohnson/papers/Johnson17Power-talk.pdf

![](https://raw.githubusercontent.com/zjluoxk/Twitter_Emotions/main/images/Capture.PNG)

The above graph may be the reason why all my models are similar! Perhaps I need to work on my amount of data. There is a point of diminishing return as show by the inverse exponential curve above. So I would need to trade between my data collection/training time and model performance.


