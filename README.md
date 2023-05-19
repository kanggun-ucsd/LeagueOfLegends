# LeagueOfLegends

---

## Introduction

---

In this short website, I would like to explore the competitve matches in League of Legends.

In League of Legends, having gold often helps the player to further have an item advantage over the opponent. However, it is not only gold that wins the game. There are also skills and strategy to this game. The players understanding and knowledge of opponent Champions, team strategy, Champion controlling skills, getting other objectives, etc. all contribute to how a team can win a game.

In an attempt to find whether team gold at then end is a factor that determines the game result, we will be exploring a csv file provided by Oracle's Elixir. The dataset we are about to explore contains match data from LCS, LEC, LCK, and more from 2022. This csv file has 149400 rows and 123 columns, however we will be mainly looking 24900 rows that consist of data for teams and the 4 following columns to investigate our question: ‘gameid’, ‘gamelength’, ‘totalgold’ and ‘results’.

---

## Cleaning and EDA
<iframe src="assets/univariate2" width=700 height=500 frameBorder=0></iframe>
'| gameid                |   gamelength |   totalgold | victory   |\n|:----------------------|-------------:|------------:|:----------|\n| ESPORTSTMNT01_2690210 |         1713 |       47070 | False     |\n| ESPORTSTMNT01_2690210 |         1713 |       52617 | True      |\n| ESPORTSTMNT01_2690219 |         2114 |       57629 | False     |\n| ESPORTSTMNT01_2690219 |         2114 |       71004 | True      |\n| 8401-8401_game_1      |         1365 |       45468 | True      |'



'|   gamelength |   totalgold |\n|-------------:|------------:|\n|      1895.91 |     51960.7 |\n|      1896.14 |     61939.7 |'
---

## Assessment of Missingness

If we examine the csv file, I believe that the columns such as doublekills, tripleskills, quadrakills, and pentakills is NMAR. While some people recorded those unoccurred events as zero, I believe that they also recorded nothing (missing value) for when the event did not occur. The total number of doublekills, tripleskills, quadrakills, and pentakills per team (no need for player), can help us get an explaination. This will make it MAR if no occurrence is the reason for missing value.


---

## Hypothesis Testing

hello