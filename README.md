<div align="center">

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

</div>


<!-- PROJECT LOGO -->
<br />
<div align="center">

  <h3 align="center"> YouTube-Spam-Detection</h3>

  <p align="center">
    A simple similarity measurement used to detect the similarity between 
    bots on Youtube from actual people. 
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This project uses simple similarity measurments namely Cosin and Jaccard 
Similarity to find the similarity of accounts to a dataset containing only 
bot accounts. We also try to find our which similarity measurement is better 
for this purpose. 

<p align="right">(<a href="#top">back to top</a>)</p>


### Built With

The project is written in R Language in R Studio. This uses some libraries in R 
for language analysis. 

* [R](https://www.r-project.org/about.html)
* [R Studio](https://www.rstudio.com/products/rstudio/download/)
* [qdapRegex](https://cran.r-project.org/web/packages/qdapRegex/index.html)
* [stringdist](https://cran.r-project.org/web/packages/stringdist/index.html)

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- GETTING STARTED -->
## Getting Started

I used R Studio to write and run the code but are free to use whatever IDE 
of your choice. You will need to install the following libraries and the 
download the bot dataset. 

### Prerequisites

* [qdapRegex](https://cran.r-project.org/web/packages/qdapRegex/index.html)
* [stringdist](https://cran.r-project.org/web/packages/stringdist/index.html)
* [YouTube Spam Collection Data Set](https://archive.ics.uci.edu/ml/datasets/YouTube+Spam+Collection)

<!-- USAGE EXAMPLES -->
## Usage

1. First we read all the datasets and combine them into one for ease of use 

```
katy=read.csv("Youtube02-KatyPerry.csv",stringsAsFactors = FALSE)
lmfao=read.csv("Youtube03-LMFAO.csv",stringsAsFactors = FALSE)
eminem=read.csv("Youtube04-Eminem.csv",stringsAsFactors = FALSE)
shakira=read.csv("/Youtube05-Shakira.csv",stringsAsFactors = FALSE)
train=rbind(katy,lmfao,eminem,shakira)
```

2. We now remove all the special characters used in the YouTube comments using gsub. 
We remove them since they contribute very little to our task and can usually throw us off. During removal of
special characters we also remove emojis and any other non english characters. 


3. We now split the data in to test case (30) and train case (1606)


4. We now compare the test data with all the training data to come to a conclusion on 
how similar the text it to the dataset. 

    For example : **"Hello make sure to check out my channel"** is considered SPAM, will be
similar to a comment saying **"Hello guys, i know its asking a lot but check out this channel, it is really good"**
but not with a comment **"Wow this video is so good"**

5. We calculate the similarity for ham and spam using both Jaccard and Cosine similarity

```
spamtempcosine=spamtempcosine+stringdist(test,train[j,4], method ="cosine", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
spamtempjaccard=spamtempjaccard+stringdist(test,train[j,4], method ="jaccard", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
hamtempcosine=hamtempcosine+stringdist(test,train[j,4], method ="cosine", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
hamtempjaccard=hamtempjaccard+stringdist(test,train[j,4], method ="jaccard", useBytes = FALSE, q = 1, nthread = getOption("sd_num_thread"))
```


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- CONTACT -->
## Contact

Your Name - [Anandha Krishnan H](anandhakrishnanh1998@gmail.com) - anandhakrishnanh1998@gmail.com

Project Link: [https://github.com/anandhakrishnanh/YouTube-Spam-Detection](https://github.com/anandhakrishnanh/YouTube-Spam-Detection)

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/anandhakrishnanh/YouTube-Spam-Detection.svg?style=for-the-badge
[contributors-url]: https://github.com/anandhakrishnanh/YouTube-Spam-Detection/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/anandhakrishnanh/YouTube-Spam-Detection.svg?style=for-the-badge
[forks-url]: https://github.com/anandhakrishnanh/YouTube-Spam-Detection/network/members
[stars-shield]: https://img.shields.io/github/stars/anandhakrishnanh/YouTube-Spam-Detection.svg?style=for-the-badge
[stars-url]: https://github.com/anandhakrishnanh/YouTube-Spam-Detection/stargazers
[issues-shield]: https://img.shields.io/github/issues/anandhakrishnanh/YouTube-Spam-Detection.svg?style=for-the-badge
[issues-url]: https://github.com/anandhakrishnanh/YouTube-Spam-Detection/issues
[license-shield]: https://img.shields.io/github/license/anandhakrishnanh/YouTube-Spam-Detection.svg?style=for-the-badge
[license-url]: https://github.com/anandhakrishnanh/YouTube-Spam-Detection/blob/master/LICENSE.txt
