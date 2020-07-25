### Introduction
[***Reddit***](https://www.reddit.com/) is an American social news aggregation, web content rating, and discussion website. Registered members submit content to the site such as links, text posts, and images, which are then voted up or down by other members.

Thus it contains huge chunks of data whose analysis could yield so much insights especially towards understanding the behaviour of a particular community.

It has subreddits indicating subtopics and each subreddit has moderators and members.

[***Praw***](https://praw.readthedocs.io/en/latest/) is the Python reddit API wrapper.

### Requirements
1. Pandas - A software library written for the Python programming language for data manipulation and analysis.
   Can be installed via ***pip, pipenv*** or ***conda***
    * ` pip install pandas` 
    * ` pipenv install pandas` (in a virtual environment)
    * ` conda install pandas` (in  conda environment)
   
2. Praw - The Python reddit API wrapper. Can be installed as follows:
    * ` pip install praw` 
    * ` pipenv install praw` (in a virtual environment)
   
   
3. Create an app from this [link](https://www.reddit.com/prefs/apps) to get the **cliend_id, client_secret** and **user_agent.**


### Scrapping data from the LiverpoolFC Subreddit.
I love soccer, and a huge fan of Liverpool FC, so what better subreddit to scrap from than that.

The first step is to create an instance of reddit after importing the 2 libraries:

    import praw
    import pandas as pd
    reddit = praw.Reddit(client_id = 'client_id', client_secret ='client_secret', user_agent='user_agent')

Then get the posts from the subreddit and specifiy the number of posts you're interested in:


    posts = reddit.subreddit('LiverpoolFC').hot(limit = 2000)

Various attributes can be pulled from the post object. For instance:

`Post Title, Name, Post URL, No. of Comments, Upvote Ratio (upvotes/downvotes), created at (timestamp), status(locked or not).`

The following line of code pulls these attributes, creates a dataframe then saves the dataframe to a csv file:

    c = ['title', 'name', 'url', 'score', 'locked', 'created', 'num of comment', 'upvote ratio']
    df = pd.DataFrame(([post.title, post.name, post.url, post.score, post.locked, post.created, post.num_comments, post.upvote_ratio]
                        for post in posts), columns = c)
    df.to_csv('liverpool_subreddit.csv')

##### To be continued to cover more features of praw.

