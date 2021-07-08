---
layout:             page
title:              Projects
permalink:          /proj/
modified_date:      2021-07-06 13:40:00 -0400
---

* dummy list needed for table of contents
{:toc}

## Research at Dartmouth
<br /><center><img src="/_img/dartmouth_baker_tower.jpg" alt="Baker Library at Dartmouth" width="600"></center> <br />
<!-- ![Baker Library at Dartmouth](/_img/dartmouth_baker_tower.j) -->

From September of 2018 until March of 2021, I researched at Dartmouth as a research assistant and PhD student in the Dartmouth Security and Artificial Intelligence Lab (DSAIL). Due to personal issues which were exarcebated by the pandemic, I decided (after discussion with and with approval from the directors of the CS, PhD, and Masters programs) to transition out of DSAIL and complete the coursework required for a Masters degree in CS.

### Cryptocurrency price prediction through social network analysis
Starting in 2019, I began working on a project centered around analyzing the relationship between fluctuations in the prices of cryptocurrencies and interactions on social media. In particular, we looked at roughly the top 20 cryptocurrencies at the time per [CoinMarketCap](https://coinmarketcap.com/) and several months of posts from [Reddit](https://reddit.com/) and [Twitter](https://twitter.com/) related to these cryptocurrencies. This work was done with funding from and in collaboration with [VeChain](https://www.vechain.org/) - who also hosted a [blockchain technology workshop](https://news.dartmouth.edu/events/event?event=56046), featuring our work as one of the presentations.

In the first iteration of this work, we produced an analysis based on simple statistics from social network activity. The dataset included things such as number of likes, number of posts, post sentiment distribution, etc. for the discussion communities on Reddit and Twitter for each of the cryptocurrencies. The Reddit data was collected by using [PRAW](https://praw.readthedocs.io/en/stable/) as well as [pushshift.io](https://pushshift.io/) to scrape archived Reddit data. The Twitter data had to be ordered directly from Twitter, in a process that took months to complete. In total, we were working with millions of Tweets and Reddit posts/comments.

I processed the data by using [Google Cloud's Natural Language module](https://cloud.google.com/natural-language/docs/analyzing-sentiment) to generate sentiment analysis results for each tweet, post and comment in the dataset. These scores (as well as likes, comments, etc.) were then analyzed as a distribution over different time intervals (i.e. past 4 hours of posts or past 3 days of posts) to be used in prediction. For prediction, we used a [collective classification](https://en.wikipedia.org/wiki/Collective_classification) model based on the correlation between prices of different cryptocurrencies to leverage relationships between coins during prediction. 

I presented this work at [IEEE 2019 International Conference on Blockchain and Cryptocurrency](https://icbc2019.ieee-icbc.org/) in Atlanta, Georgia. It was later published in the [proceedings of the conference](https://www.computer.org/csdl/proceedings/blockchain/2019/1gjS4tubCmI).

In the more recent iteration of this work, we expanded our social network analysis to include novel metrics which we defined. These metrics were designed to capture the significance of specific authors and posts, then use this information in predictions. Also in this iteration we improved the core collective classification algorithm used in the original work. This required me to organize many compute nodes on [the Dartmouth research cluster](https://rc.dartmouth.edu/index.php/discovery-overview/) to run thousands of hours of computations for the iterative novel metrics we defined, as they applied to graphs with many thousands of nodes. It was worth it in the end, though, as it led to significant improvements over our previous analysis and the results are in preparation for submission to a journal.

A description page will be added to this site once I have time to add it. The source code for this project will not be made available unless requested by a potential employer, as this is active work.


### Social network analysis for counter-terrorism
In this project, we investigated a dataset containing known terrorist organizations and individuals, as well as the relationships between them. Treating this as a low-information and highly [unbalanced](https://www.kdnuggets.com/2019/05/fix-unbalanced-dataset.html) social network (i.e. where the information in the dataset only represents a small fraction of the real data with actual incidents of interest being disproportionately rare), we tackled various difficult problems such as predicting changes in relationships in the network and predicting major events.

In the initial analysis, we theorized about novel [multigraph](https://en.wikipedia.org/wiki/Multigraph) influence and [centrality](https://en.wikipedia.org/wiki/Node_influence_metric) metrics which may provide better predictive results. We also considered how these metrics correlated with the rank of an individual within an organization. We finally conducted statistical analyses to ensure predictive information provided by these metrics was statistically significant. Though many of our metrics seemed to contain statistically significant information per our analysis, no combination of these metrics helped improve our predictive results to a level that would be publishable.

More recently, we conducted another set of studies on the data with colleagues from the [Netherlands Defence Academy](https://english.defensie.nl/topics/netherlands-defence-academy/research-and-education). This analysis expanded the prediction problems significantly for this dataset by asking: 
* Do either of the metrics defined in our previous analysis or the new metrics introduced in the final analysis provide predictive value when making predictions about the future structure of the graph rather than a major event? 
* Can we improve performance by making predictions which look further into the future? 
    * Where a prediction is on whether or not an event will happen within 3, 6, 12 months rather than just in the next month.
    * If so, what can we discover about the relationship between prediction performance and the length of the prediction window? 

A description page will be added to this site once I have time to add it. Our results were significantly interesting and could be published someday, but those as well as the source code for this project will not be made available unless requested by a potential employer, as this is active work.


### Physician network analysis for efficient information spreading
This project was a short collaboration with our colleagues [Ronnie Zipkin](https://geiselmed.dartmouth.edu/qbs/rzipkin/) and [Erika Moen](https://moen-lab.com/team) of the eponymous Moen Lab in the [Quantitative Biomedical Sciences program](https://geiselmed.dartmouth.edu/qbs/) at Dartmouth's Geisel School of Medicine. We explored the problem of spreading novel, effective treatment information throughout the United States by viewing physicians as a social network, where links were added between physicians based primarily on publications and location. In particular, we examined the usage of a more effective and cheaper test related to breast cancer and modelled its spread similar to how infectious spread is modeled.

As we were strapped for time already in my lab, I did not have time to join the project fully. That said, I provided consulting on the statistical and mathematical models which could be applied to the data as well as some ideas on tools that could be used to facilitate the calculations (such as [networkx](https://networkx.org/) and [igraph](https://igraph.org/) -- which I have used extensively in other projects).

In the end, though we didn't end up publishing a paper as a result of this short collaboration, it was very interesting to see the applications of [graph theory](https://www.britannica.com/topic/graph-theory) to medicine. The work done by the Moen team (and others at Geisel/TDI) is great, and definitely worth a read. I may expand on this section with a blog post someday.


### General collective classifier
[Collective classification](https://en.wikipedia.org/wiki/Collective_classification) leverages the idea that nodes which are closer to each other in a network should be more similar. In theory, this similarity should mean that nodes which are closer to each other are more likely to share the same label in a prediction problem. Using methods similar to clustering, my advisor theorized that we could create a general collective classifier which would extract a network from a dataset and then run iterative collective classification on the extracted graph. This should create a powerful classifier which may be more effective in certain datasets.

I implemented the idea from scratch in Python and ran my new model on tens of different datasets, comparing to standard parametric models from [scikit-learn](https://scikit-learn.org/stable/) (Naive Bayes, K Nearest Neighbors, Support Vector Machines, Random Forest, etc.) as well as a simple neural network built with [Keras](https://keras.io/) and tuned using [GridSearchCV](https://scikit-learn.org/stable/modules/grid_search.html). Unfortunately, though the generalized collective classification model matched the performance of the simple neural network on quite a few datasets, it was never able to surpass the neural network. As such, the project was scrapped soon after I reported these findings.

A description page will be added to this site once I have time to add it. The source code for this project will not be made available unless requested by a potential employer, as this work was not published.


## Cal Poly capstone projects

<br /><center><img src="/_img/cal_poly_grad.JPG" width="600"></center><br />

In undergrad, I completed both a major in computer science and a cross-disciplinary minor in data science as part of my studies at Cal Poly. For the minor, I had to complete a capstone (after completing 15+ other courses) which was a 6 month long, team-based industry collaboration in a data science project. For the major, I had to complete a senior project with rather open requirements, so I did a collaboration with a local AI start up in San Luis Obispo. 

### Cal Poly data science capstone
From January 2018 through June 2018, I worked in a team of three with [Owais Sarfaraz](https://www.linkedin.com/in/osarf/) and [Aleks Braksator](alexbrax.com) on a collaborative capstone project with [FICO](https://www.fico.com/). In this project, we worked with a dataset consisting of driving videos along with telemetric data for various driving trips. We worked under our Data Science minor advisors [Professor Dennis Sun](https://statistics.calpoly.edu/dennis-sun) and [Professor Alex Dekhtyar](http://users.csc.calpoly.edu/~dekhtyar/) as well as an advisor from FICO, [Steve Lakowske](https://www.linkedin.com/in/stephen-lakowske-96420b8/).

My team developed a driving score based on the safety of a driver. Unfortunately, the only dataset we were able to use at the time was the version which includes no accidents. That is, we had no concretely dangerous events to examine. We had to find a way to identify and measure unsafe driving without examples of unsafe driving.

To do so, we first had to watch the videos and manually note the beginning and ending time of each driving maneuver (turn, brake, etc.) as well as rate the maneuver as either safe or dangerous. With these annotated sets, we were able to use rules-based methods to identify the start and end times of driving maneuvers.

Once we had these chunks of data, which consisted of [time-series telemetry](https://thevirtualforge.com/blog/telematics-data/) and video data over each time segment we identified, we had to learn from them. We decided to use unsupervised learning to understand a bit more about this new annotated dataset we had created. We settled on using clustering methods, and found clear distinction between safe and unsafe driving within each of our different driving maneuver categories.  

A description page will be added to this site and source code will be added to [my Github][githome] once I have time to make these changes.


### Cal Poly senior project
From January 2018 through June 2018, I worked on and completed my senior project for the [Cal Poly SLO Computer Science program](cpslo). I did this project as a collaboration with [Unanimous AI (UAI)](https://unanimous.ai/). UAI provided data collected from their Swarm AI sessions about games from multiple professional sports leagues.

The project focused on the results of a customized betting algorithm utilizing rules-based methods to maximize returns. The bot was successful in its bets, making significant gains on average.

A description page will be added to this site and source code will be added to [my Github][githome] once I have time to make these changes.


## Personal projects
After transitioning from being a PhD student to being a Masters student, I have found a lot more free time to code. So far, I have only been working on this website and a customized LaTex template for my resume, but I am excited to fill this section out more.

### Transitioning resume to LaTex
Back in 2018 or so, I transitioned to using a [LaTex](https://www.latex-project.org/) resume using a theme that I found on [Overleaf](https://overleaf.com/). Using the interactive development environment on their website, the live compiling feature, the template repository, and many visits to the documentation, I was able to produce a very nice looking resume. It looked nice, but it never felt like I really

In June of 2021 I finally decided to significantly rework my own LaTex template based on the original <> template from Overleaf. 

You can find the source code for the current version of my resume on Github:
[websurfin][githome] /
[hire-me](https://github.com/websurfin/hire-me)


### Building this website
In addition to revamping my resume, I started work on this website in late June of 2021.

You can find the source code for the website on Github:
[websurfin][githome] / [websurfin.github.io](https://github.com/websurfin/websurfin.github.io)


[githome]: https://github.com/websurfin/
[cpslo]: https://csc.calpoly.edu/
