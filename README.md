# Using NLP on Crossword and Sudoku Subreddit Content to Interpret Keywords

### Background
The [Puzzle Society](https://www.puzzlesociety.com/about-us) is a community for puzzle fans around the world that provides a wide array of mind challenges for its members to solve. I'm a data scientist who The Puzzle Society has hired to help increase its membership size (please note -- this is a **fictional** scenario).

### Problem Statement
>By modeling on crossword and sudoku subreddit content, the goal is to understand what aspects of those puzzles generate most discussion, so that the Puzzle Society can use that information to better know its audience, improve marketing efforts, and increase membership.

### Methodology
* Using the [PushShift API](https://github.com/pushshift/api), I scraped 2400 total submissions from the crossword and sudoku subreddit pages.
* After cleaning and formatting the submission data, I lemmatized all words and dropped every instance where 'crossword' or 'sudoku' appeared in a post, since the presence of those words are a dead giveaway for telling a model which subreddit a post came from.
* I binarized the subreddit data, giving 'crossword' a value of 1 and 'sudoku' a value of 0.    
* I put the submission data through three models -- Logistic Regression, Support Vector Classifier, and Naive Bayes -- to predict whether a post originated from the crossword or sudoku subreddit.
* Using Logistic Regression, I interpreted the highest and lowest feature coefficients to determine which words played the largest role in determining whether a post originated from the crossword or sudoku subreddit.

##### Datasets Created During Project
* [`cw_posts`](./Data/cw_posts.csv): 1200 posts from the crossword subreddit, including text from each post title and subtext below each title (selftext).
* [`sud_posts`](./Data/sud_posts.csv): 1200 posts from the sudoku subreddit, including text from each post title and subtext below each title (selftext).
* [`titles_and_text`](./Data/titles_and_text.csv): a combination of the cw_posts and sud_posts datasets, cleaned and lemmatized.
* [`titles_and_text_no_cw_or_sud`](./Data/titles_and_text_no_cw_or_sud.csv): the same dataset as titles_and_text, except that all instances of the words 'crossword' and 'sudoku' in the text are removed.

### Conclusion from Analysis

#### Key Takeaways:

* Most of the larger coefficients look more specific to crosswords than to sudoku. New York Times crosswords are the most popular brand of crosswords, so using the 'nyt' in the crossword subreddit is expectedly common. Crosswords have themes, obviously a lot of words, and clues, whereas sudoku does not tend to possess any of those things.  

* Most of the words with small coefficients fit better to what sudoku is all about. Sudoku is analytical and numbers-heavy, so the presence of a word like 'logic' makes sense. 'Cracking' stems from 'cracking the code,' which brings a numerical puzzle like sudoku to mind before a crossword. 'Technique' and 'strategy' are talked about more in sudoku -- crosswords has a few strategies, but crossword success has to do less with a strategy/technique than simply having an advanced vocabulary.

#### Recommendation:
Logistic Regression models should be used in favor of Naive Bayes and Support Vector Classifier when wanting to learn more about crossword and sudoku audiences, since the feature coefficients they produce are interpretable.

The Puzzle Society should post promotions for membership in the sudoku and crossword subreddits, taking care to incorporate the keywords and themes with the highest and lowest correlations found from the Logistic Regression models in order to raise its membership. If The Puzzle Society leverages the same keywords often used by puzzle fans themselves, it should be more likely to attract those fans to join the community.
