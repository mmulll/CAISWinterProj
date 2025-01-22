# CAISWinterProj

Maddie Muller

mfmuller@usc.edu

My project used BERT, a deep learning model designed for natural language processing tasks, to classify news articles as fake or real, with implications for digital literacy and misinformation identification.

**Dataset**

I used the dataset “Fake News Detection” from Kaggle, as provided in the instructions for the project. This dataset contained 12,600+ real articles from Reuters and 12,600+ fake articles from various news sources. It included their headline, the body text, the date, and the type of article. For preprocessing, I added both the real and fake articles to a pandas dataframe. I combined the headline and body into one large chunk of text for ease of processing. I removed the word Reuters from the real articles, as well as the city name as the beginning of the article. I removed all the other data points (date, article type, headline, body) from the dataframe and added one data point denoting if the article was fake (0) or real (1). I chose to combine the headline and body because headlines often convey sensationalism, which is important to discern between real and fake articles. However, I wanted to include the body, or at least a portion of it, in case the headline did not fully capture the markers that allow the algorithm to distinguish between real and fake news articles. Because there were so many articles, I only kept half of them; when I tried training the algorithm with all of them, it was clear this would take an unrealistic amount of time.

**Model Development and Training**

I decided to use BERT because of its versatility and high-performance, and because a pre-trained model saved me computational power and allowed me to achieve better results. Specifically, I chose to use the cased version because, during my initial exploration of the data, I found that many of the fake articles had words capitalized in the headline. The capitalization of words can capture sensationalism, which I wanted to include in the input fed into the algorithm. As for hyperparameters, I chose a batch size of 32, 2 epochs, and a learning rate of 2e-5. I chose the batch size of 32 because the BERT authors recommend a batch size of 16 or 32, and I had a lot of data to process so bigger batches seemed more efficient. I chose 2 epochs because the authors also recommend 2 to 4 epochs and, again, I had a lot of data (and each data point is quite large) so I wanted to shorten the training process. I also wanted to avoid overfitting. I chose a learning rate of 2e-5 (one of the options recommended by the BERT authors) to avoid overfitting and drastic updates to the model. In addition, when tokenizing, I limited each body of text to 250 tokens. I began with the maximum of 512, but I found that this took an inordinate amount of time. I hypothesized that a section of the text, especially the intro which would include the hook, wooden encapsulate, the tone and main message of the article.

**Model Evaluation/Results**

I used the Matthew's correlation coefficient to evaluate the success of my model as it works well for binary classification and incorporates false positives, false negatives, true positives, and true negatives into one value. It had also been used in the L4/5 notebook. My MCC score was 1, or 100% accuracy, which is unusual. When I originally got this score, I took a few steps to try to change it, but I continued to get 100% accuracy. First, I ensured the word "Reuters" and the capitalized location was removed from all the real articles so the model could not rely on that. I also used the smallest learning rate and number of epochs within the recommended range to avoid overfitting. However, the 100% score persisted. This could be a result of all the real articles being from Reuters; it is possible the model is evaluating on writing style or some other characteristic apart from real versus fake. Testing the model on non-Reuters real articles may give a more holistic picture of its accuracy, which is discussed further below.

**Discussion**

Overall, I believe the data set, model architecture, training procedures, and metrics were a good fit for this project. Much of it was taken from or inspired by the L4/5 notebooks, which gave the project a good foundation. However, there are some limitations that should be discussed. As for the dataset, all the real articles from the data that were from the Reuters website. Thus, it is possible that the algorithm actually classified Reuters versus non-Reuters articles, not fake versus real articles. To ensure accuracy, it should be tested on legitimate articles from other sources as well. Second, the algorithm achieved 100% accuracy, which is unusual. While I minimized the learning rate and epochs to avoid overfitting, it should be further explored why this is by testing the model on articles from new sources, which could give a more accurate picture of the model's accuracy.

This project could be used for social good by means of identifying and combating misinformation, for example on fact-checking websites or social media platforms. It would be especially relevant and necessary to content surrounding issues where accurate information is key, like presidential elections. Most people obtain information about current events, politics, etc. from online news sources, so vetting them is vital to fostering an informed society. However, there are some important limitations to using a technology like this. First, one would have to ensure that the algorithm is not biased, politically or in some other way. Otherwise, certain voices could be censored even when they are not spreading misinformation. In order to test this, the model’s performance classifying articles from a variety of news sources and global cultures would need to be evaluated. Because all of the real articles were from Reuters, the model could have developed a bias towards the general views or even the writing style of Reuters articles. Second, it's important to consider what misinformation even is and what should be done with misinformation/misinformers. This issue could raise concerns about free speech or what is defined as fact versus opinion. This would need to be considered before implementing this model on any platform.

As next steps, I'd want to evaluate the model on articles from a variety of reputable news sources of different political leanings and from different countries and cultures. This would give a bigger picture of the model's performance on the swaths of articles that exist on the Internet and mitigate possible political or cultural bias. I'd also want to evaluate the model on factual versus fake social media posts to see if its use case could be extended beyond just news. Since none of the articles were padded because they were all longer than the token max, I'd want to test some really short articles that would have padding to see how they would perform. I'd also want to dig into why the model classifies articles as fake or real, as this could increase transparency and help us better understand the model. Finally, I would want to try to use the uncased version of BERT to understand how significant of a role the capitilization of words is playing in the process.

**Credit**
I copy-and-pasted code from the L4/5 notebook and edited it to suit my purposes.
