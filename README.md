### Background and Objective

**Background:** 
Reddit is a discussion website with subreddits for different categories. Many popular video games have subreddits where users discuss game updates, share their opinions, and share game content. 

Two popular games are *Call of Duty: Modern Warfare II* (which from here will be abbreviated as "COD MW2") and *Overwatch 2*. COD MW2 was released October 28, 2022 and Overwatch 2 was released on October 4, 2022. Both are first-person shooters which have multiplayer modes and are played on various platforms including PS4, PS5, Xbox One, Xbox X/S, and Windows. Although there are different game modes for each game and the gameplay for each is different, they are both shooters with large and active Reddit communities, with the *COD MW2* subreddit having 806k members and the *Overwatch* subreddit (which contains *Overwatch 2* content) having 4.2 million members. 

**Goal:** 
The goal of this project is to classify reddit posts as *Call of Duty: Modern Warfare II* subreddit or *Overwatch 2* subreddit posts using natural language processing (NLP). Then, we will look at features which have high importance in classification to shed light on these two gaming communities. This will be turned into actionable insights for the advertising departments/ agencies of the two game companies. 

Success will be evaluated as a logistic regression or random forest model that performs better than a baseline classification model

### Process and Model

**Process:**

For classification, the combined title and selftext were used after data was pulled using pushshift api. The data was cleaned by removing unwanted characters (such as punctuation, emoji, line breaks) and unwanted words from the combined title_selftext. The process of removing unwanted words was involved. First, self-references to the games were removed (words such as "overwatch" and "warfare"). This is because we aim to look at the language in the two gaming communities and want to use words used in both communities, not just one or the other. Other words such as weapon names for *COD MW2* and character names for *Overwatch 2* were removed.

After a first round of cleaning, most frequent words were pulled using CountVectorizer and the words were researched for context (using both desktop research and friends as a reference). Many words were removed which were used primarily for one community over the other (these words are detailed in the data_cleaning notebook). This process was repeated several times.

Once the data was cleaned, the title_selftext was lemmatized. Both lemmatized and non-lemmatized title_selftext were evaluated, but the lemmatized version was kept as performance was better.

**Model:**

For modeling, both Logistic Regression and Random Forest were considered as they are industry standard and widely used for their performance. Both were considered with both CountVectorizer and TFIDF, and a gridsearch was used for model parameters and stop words (english or none). 

Baseline: 0.660

The final model was:
* CountVectorizer, no stop words
* done on unigrams
* Lasso penalty, C = 1.3
* Lemmatization on title + self_text
* Training score: 0.918
* Testing score: 0.861

### Results and Recommendations

**Results:**

For results, we have identified words which are important in classification for the two different subreddit communities of *Call of Duty: Modern Warfare II* and *Overwatch 2* (see model_creation notebook). This is important for the following two reasons:

1. Gaming communities which have niche vocabulary terms are signs of a successful game. It means that when a particular term is used, users understand what the word means in the context of the game; they have taken the time to learn new game-specific terms, which often comes after playing the game for multiple hours. It speaks to both the popularity of the game and strength of the community. It likely helps retain users on the game who are familar and comfortable with the terminology as going to another game would mean they would have to adapt their language.

2. On the flip side, having niche vocabulary terms may act to stop new users from picking up the game. They may be intimidated (especially if there are a lot of niche words), especially if the game has live voice channels with teammates (which *Overwatch 2* and *COD MW2* both have)

Words important in *Overwatch 2*: tank, support, rank, comp/ competative, role, heal

Words important in *Call of Duty: Modern Warfare II*: multiplayer, loadout, activision, gun, weapon

In general, words in *Overwatch* subreddit posts are more character/role based and words in *COD MW2* subreddit posts are more weapon-based. We also observe that *Overwatch* has more unique/ niche language in comparison.

**Recommendations:**


In terms of maximizing revenue, *COD MW2* is a pay-to-play game while *Overwatch 2* is free-to-play but has in-game purchases such as character skins (this is actually not strictly true - *COD MW2* offers a free gameplay mode and has in-game weapon skin purchases as well. But for the large part, we can assume *COD MW2* makes the majority of its revenue off the $70 price tag and *Overwatch 2* makes the majority of its revenue off in-game purchases). Therefore, user retention is more important for *Overwatch 2* whereas new users are more important for *COD MW2*. 

For *Overwatch 2*, it may therefore be beneficial to include its niche terms in advertising efforts and tournaments to build a stronger sense of community. This would likely move users to make in-game purchases. For *COD MW2*, it may be beneficial to instead gear its advertising towards new users by explaining or unraveling any niche in-game terms and making the community more accessible. In both cases, next steps should be to frewquently and systematically look at community language (through Reddit, voice chats, and voice channels) and relate it to game revenue. 

The use of language in advertizing is powerful and although *Overwatch 2* and *Call of Duty: Modern Warfare II* are both FPS games, one may benefit from reinforcing its niche vocabulary whereas the other may benefit from keeping general terms and opening up doors to new users instead.

sources:

https://en.wikipedia.org/wiki/Reddit
https://en.wikipedia.org/wiki/Call_of_Duty:_Modern_Warfare_II_(2022_video_game)
https://en.wikipedia.org/wiki/Overwatch_2

(additional sources are added inline to the notebooks)