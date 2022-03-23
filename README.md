DSIR 1213  
PROJECT 3

PROBLEM STATEMENT
Many people want to become financially independent, but they have misperceptions of what that means.

There is a movement referred to as "FIRE", which is an acronym for Financial Independence, Retire Early.

One common misperception is that you must be EXTREMELY frugal to FIRE!

A way to debunk this misperception is to compare the Fire and Frugal subreddits and evaluate the language used to see how similar it is.

If the language between the two subreddits is extremely similar, then my model won't be able to correctly predict which subreddit a post is from.

DATA COLLECTION
I collected 20,003 posts from the Fire subreddit and 25,004 posts from the Frugal subreddit using the Pushshift API.

DATA CLEANING AND EDA
Although I collected significantly more Frugal posts, I ended up with slightly more Fire posts in my final dataset.  This was because I dropped posts that were not "self posts" by reddit members.  They could have been links to outside websites or ads, just as two examples, but they weren't appropriate for this analysis.  My final dataset consisted of 19,700 Fire posts and 
18,650 Frugal posts.

The data was remarkably clean.  I didn't have missing data except for 2 unimportant pieces of data.

Even though I pulled in a lot of extra variables to learn more about these different subreddits, most did not contain any meaningful information.  I thought it was strange that both subreddits seemed to be hihgly cross posted.  Only 350 Fire posts were not cross posted, and only 4,600 Frugal posts were not cross posted.

PREPROCESSING AND MODELING

I used Natural Language Processing to try to predict if a post came from the Fire or the Frugal subreddit.

My target for my models, the subreddit field, held the name of the subreddit, so I changed it to be a "1" if it was the Fire subreddit and a "0" if it was the Frugal subreddit.

I created a "superfeature" by concatenating the title feature and the subtext feature for each post.  I then used CountVectorization to explode my superfeature into several individual words for consideration in my models. I using stop_words='english' to screen out common words, but didn't apply any other restrictions or do any other dropping/cleaning of the words.

NULL MODEL 
The null model revealed a balanced accuracy score of .5 so it wasn't very strong.  Remember, I had 51% Fire posts and 49% Frugal posts in my analysis dataset, so it predicted everyone would be from the Fire subreddit since there were slightly more Fire posts.

LOGISTIC REGRESSION
I first built a Logistic Regression model.  My target was the subreddit field I created, and my features were exploded from the subreddit post title and post text.  My accuracy score on both my training and testing data was 1!  I was cetrain that I done done something incorrectly, but after conferring with my instructor, I realized that this showed what I was trying to prove, that focusing on frugality and fire are two very different experiences as revealed by the language used on reddit by members fo the different subreddits.

NAIVE BAYES MODEL
I then created a Naive Bayes model.  My target and features were exactly the same as those used for the Logistical Regression model so that I could compare the models "head to head".  My accuracy score on my testing data was 0.997 and was 0.998 on my training data.  So this model was slightly worse than the Logistic Regression model.

EVALUATION AND CONCEPTUAL UNDERSTANDING
Since my models were so good, it wasn't necesary to see if stemming and lemmatization would improve them.

My null model, with a baseline balanced accuracy score of  .5, wasn't any better than flipping a coin to determine which subreddit a post came from!  This is because I had an almost 50/50 split of Fire vs Frugal posts, so it didn't favor one over the other.

I would choose the Logistical Regression model over the Bayes model because its output is much more interpretable than the Bayes model.  The coefficients for the top and bottom 20 words were much more logical for the Logistical Regression model than for the Bayes model.

I evaluated the polarity of the sentiment of the two subreddits, looking at the title and text individually.  My boxplots showed that the Fire subreddit's title sentiment was more neutral compared to that of the Frugal subreddit. The Frugal subreddit title's boxplot range skewed more positive than that of the Fire subreddit titles.  Both subreddits had polarity outliers that ranged from -.75 to 1.  For text, the median polarity was lightly more positive for the Frgual subreddit texts, but the boxplots were very similiar.  One striking difference for the texts is that the outliers for Frugal subreddit texts had much wider swings in polarity than the Frugal subreddit did.

RECOMMENDATIONS
It is possible to accurately determine if a post came from the Fire subreddit versus the Frugal subreddit.

The words used by each subreddit community are distinctly different.  The Fire community is definitely more investing/growth focused, while the Frugal community is more consuming/minimizing focused.

Here are the most important top 20 words to indicate a post is from the Fire subreddit (listed in order of importance):
Dreaming
Big
Life
ETFs
Stocks
Passive
300
FI
Portfolio
Trying
Invest
Plan
401K
Tax
Retire
Vs
Comfortable
Youtubers
Market
Escape

Here are the least important bottom 20 words to indicate a post is from the Fire subreddit...which means they are highly likely to be found on the Frugal subreddit.  These are listed in order of most importance to the Frugal subreddit (and thus least important for the Fire subreddit):
Removed
Frugal
Tips
Food
Cheap
Store
Buy
Going
Internet
Antrepreneur
Tried
Items
Car
Survey
Replacing
Does
Phone
Paper
Don't
Save

NEXT STEPS
Pull comments from each subreddit and see if there is a similar impact on modeling.
Look at the individual impact of only title or only text in the models.
Start over with two different reddits that are related to Personal Finance in hopes of finding a tougher classification problem.
I can now apply this NLP modeling process knowledge to help my District 40 Toastmasters leadership team evaluate the language from the area director club visit reports.
