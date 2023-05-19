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

| gameid                |   gamelength |   totalgold | victory   |
|:----------------------|-------------:|------------:|:----------|
| ESPORTSTMNT01_2690210 |         1713 |       47070 | False     |
| ESPORTSTMNT01_2690210 |         1713 |       52617 | True      |
| ESPORTSTMNT01_2690219 |         2114 |       57629 | False     |
| ESPORTSTMNT01_2690219 |         2114 |       71004 | True      |
| 8401-8401_game_1      |         1365 |       45468 | True      |



### Univariate Analysis
<iframe src="assets/univariate2" width=500 height=400 frameBorder=0></iframe>


### Bivariate Analysis
<iframe src="assets/bivariate" width=500 height=400 frameBorder=0></iframe>


### Interesting Aggregates

|   gamelength |   totalgold |
|:-------------|------------:|
|      1895.91 |     51960.7 |
|      1896.14 |     61939.7 |


| victory   |   gamelength |   totalgold |
|:----------|:------------:|------------:|
| False     |      1895.91 |     51960.7 |
| True      |      1896.14 |     61939.7 |

---


## Assessment of Missingness
If we examine the csv file, I believe that the columns such as doublekills, tripleskills, quadrakills, and pentakills is NMAR. While some people recorded those unoccurred events as zero, I believe that they also recorded nothing (missing value) for when the event did not occur. The total number of doublekills, tripleskills, quadrakills, and pentakills per team (no need for player), can help us get an explaination. This will make it MAR if no occurrence is the reason for missing value.

<iframe src="assets/league by missingness of teamname" width=500 height=400 frameBorder=0></iframe>
<iframe src="assets/empirical distrubution of the tvd1" width=500 height=400 frameBorder=0></iframe>
<iframe src="assets/league by missingness of teamname" width=500 height=400 frameBorder=0></iframe>
<iframe src="assets/empirical distrubution of the tvd2" width=500 height=400 frameBorder=0></iframe>


---


## Hypothesis Testing

**null hypothesis:** In competitve league of legend, winning team and losing team have the same distrubution of total gold.

**alternate hypothesis:** In competitve league of legend, winning team has higher total gold at the end of the game than losing team.

<iframe src="assets/empirical distrubution of the mean difference" width=500 height=400 frameBorder=0></iframe>

---