# Similarity-meausre-for-YouTube-Spam-Detection
This is to try and detect bots using a similarity measurement mainly Cosine Similarity and Jaccard Similarity and compare their performances
The project has been done using the R Language in R Studio 

The libraries used are 
1. qdapRegex
2. stringdist

The dataset we are working with is from the UCI Machine Learning Repository [YouTube Spam Collection Data Set](https://archive.ics.uci.edu/ml/datasets/YouTube+Spam+Collection)

First we read all the datasets and combine them into one for ease of use. 

    katy=read.csv("D:/Doucuments/MSc CS MI/Bot Detection/Dataset/YouTube-Spam-Collection-v1/Youtube02-KatyPerry.csv",stringsAsFactors = FALSE)
    lmfao=read.csv("D:/Doucuments/MSc CS MI/Bot Detection/Dataset/YouTube-Spam-Collection-v1/Youtube03-LMFAO.csv",stringsAsFactors = FALSE)
    eminem=read.csv("D:/Doucuments/MSc CS MI/Bot Detection/Dataset/YouTube-Spam-Collection-v1/Youtube04-Eminem.csv",stringsAsFactors = FALSE)
    shakira=read.csv("D:/Doucuments/MSc CS MI/Bot Detection/Dataset/YouTube-Spam-Collection-v1/Youtube05-Shakira.csv",stringsAsFactors = FALSE)
    train=rbind(katy,lmfao,eminem,shakira)
    
Now comes the hard part of cleaning the data. 
Since this is a YouTube comments database there are lots of comments which includes special charcters, links, blank spaces and other unwanted text. To remove them we use gsub and remove all the unwanted characters. 
Some comments only included these unwanted text so after cleaning we are left with no text. So it is important to remember to not consider these empty cleaned texts. 

We now slipt the data in to test case (30) and train case (1606)

It is important to understand how Jaccard and Cosine Similarity work and how we can use this.
We are comparing a test case all the train cases and finding out to which of the train cases is our test case most similar to. 

For example a test case of **Hello make sure to check out my channel** which is clearly a spam comment is more similar in terms of Cosine and Jaccard similarity to **Hello guys, i know its asking a lot but check out this channel, it is really good** rather than **Wow this video is so good** which is obviously and good ham comment. 

We calculate the similarity for ham and spam using both Jaccard and Cosine similarity
     
    spamtempcosine=spamtempcosine+stringdist(test,train[j,4], method ="cosine", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
    spamtempjaccard=spamtempjaccard+stringdist(test,train[j,4], method ="jaccard", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
    hamtempcosine=hamtempcosine+stringdist(test,train[j,4], method ="cosine", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
    hamtempjaccard=hamtempjaccard+stringdist(test,train[j,4], method ="jaccard", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
      
After that we verify whether our observations are true using the  expected outputs fromt the test set. 

All that's left is to see the performance measure (Accuracy, Precision, Recall and F1 Score) and confusion matrix. 
