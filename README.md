## League of Legends
# Competitive Matches Analysis

---

## Introduction

In this short website, I would like to explore the competitve matches in League of Legends.

In League of Legends, having gold often helps the player to further have an item advantage over the opponent. So does having more total gold as a teaan at the end of a match make you more likely to win or lose given match? However, it is not only gold that wins the game. There are also skills and strategy to this game. The players' understanding and knowledge of opponent Champions, team strategy, their own champion controlling skills, getting other objectives, etc. all contribute to how a team can win a game.

In an attempt to find whether team gold at is a factor that is related to the game result, we will be exploring a csv file provided by Oracle's Elixir. The dataset we are about to explore contains match data from LCS, LEC, LCK, and more from 2022. This csv file has 149400 rows and 123 columns, however we will be mainly looking 24900 rows that consist of data for teams and the 4 following columns to investigate our question: ‘gameid’, ‘gamelength’, ‘totalgold’ and ‘result’. 
 - 'gameid': unique id for the match
 - 'gamelength': duration of the game in seconds
 - 'totalgold': the total gold that the team collected at the end of the match
 - 'result': indicates 1 for victory and 0 for defeat

---


## Cleaning and EDA

### Data Cleaning

First thing I needed to have was data that only consisted of rows of team. I noticed that the 'position' column has not only tells the position of individual players role in the game but also indicates team states. So I queried so that I only have rows that have 'position' equal to the string 'team'. Then I just pulled those four columns out. I checked for missing values and it seems like there is none.

Here is the head of the cleaned dataframe:

| gameid                |   gamelength |   totalgold | victory   |
|:----------------------|-------------:|------------:|:----------|
| ESPORTSTMNT01_2690210 |         1713 |       47070 | False     |
| ESPORTSTMNT01_2690210 |         1713 |       52617 | True      |
| ESPORTSTMNT01_2690219 |         2114 |       57629 | False     |
| ESPORTSTMNT01_2690219 |         2114 |       71004 | True      |
| 8401-8401_game_1      |         1365 |       45468 | True      |



### Univariate Analysis

The distrubution of total gold enable us to see that most teams ends the game when they have 56.6725k gold. We can also see that there are lot more outlier as the amount of gold get higher (more than 86.301k is considered an outlier). 
<iframe src="assets/univariate2" width=500 height=400 frameBorder=0></iframe>


### Bivariate Analysis

The distrubution of total gold based on whether a team wins or not is shown in this bivariate analysis. We are able to see that the team that got the victory ends of on average with more gold than the team who lost the match.
<iframe src="assets/bivariate" width=500 height=400 frameBorder=0></iframe>


### Interesting Aggregates

Regardless of whether the match is won or less, on average the game length is similar to one another. Here we can see that the total gold is higher once again.

| victory   |   gamelength |   totalgold |
|:----------|:------------:|------------:|
| False     |      1895.91 |     51960.7 |
| True      |      1896.14 |     61939.7 |




## Assessment of Missingness

### NMAR Analysis

If we examine the csv file, I believe that the columns such as doublekills, tripleskills, quadrakills, and pentakills is NMAR. While some people recorded those unoccurred events as zero, I believe that they also recorded nothing (missing value) for when the event did not occur. The total number of doublekills, tripleskills, quadrakills, and pentakills per team (no need for player), can help us get an explaination. This will make it MAR if no occurrence is the reason for missing value.


### Missingness Dependency
Because my cleaned data does not any missing value, I will be picking 'teamname' column for this section of the project.

**Comparing null and non-null 'teamname' distrubution for 'league'**

<iframe src="assets/league by missingness of teamname" width=500 height=400 frameBorder=0></iframe>

Based on this this figure, 'league by missingness of teamname', we can see that there is one league that has team name missing. Let us try to a simulation with 500 repetition by shuffling the 'league' column to make sure determine if it is significant. We will compute the TVD for each shuffle than compare it to the observed TVD.

<iframe src="assets/empirical distrubution of the tvd1" width=500 height=400 frameBorder=0></iframe>

With the observed_tvd of 0.48543650315375036, the p-value is 0.0. So we can reject the null hypothesis, meaning that columns 'teamname' is MAR dependent on column 'league'.


**Comparing null and non-null 'teamname' distrubution for 'result'**

<iframe src="assets/league by missingness of teamname" width=500 height=400 frameBorder=0></iframe>

Unlike the previous column's distrubution against 'teamname' missingness, we can't get any idea of what is happenning just by looking at this graph. However, once again let us do a simulation with 500 repetition. We will be shuffling the 'result' columns, compute the TVDs of each shuffles, then compare it to the observed TVD.

<iframe src="assets/empirical distrubution of the tvd2" width=500 height=400 frameBorder=0></iframe>

The observed_tvd of these two columns is 0.055495292809984886, with the p-value is 0.592. We failed to reject the null, which means that the column 'teamname' does not depend on the column 'result'.


---


## Hypothesis Testing

**null hypothesis:** In competitve league of legend, winning team and losing team have the same distrubution of total gold.

**alternate hypothesis:** In competitve league of legend, winning team has higher total gold at the end of the game than losing team.

We need to figure out whehter the two samples (winning team and losing team) come from the same sample. In order to do so, I will be doing a permutation test with 500 repetition, shuffling the 'totalgold' column then computing the difference of means. Then I will be comparing the observed differences to differences computed from the permutation test. 
<iframe src="assets/empirical distrubution of the mean difference" width=500 height=400 frameBorder=0></iframe>

With the observed difference of about 9978.96 total gold and a p-value of 0.0, we can reject the null hypothesis.

---