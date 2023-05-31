# EDA-in-Python
Are First Basemen Power Hitters?

<h2>Overview</h2>
<p>In my experience following baseball, I have found that first basemen are often the power hitters on the team.  A power hitter can be loosely defined as a player hits the ball farther and who tends to hit more home runs, as well as doubles and triples (versus singles).</p>

I did some research and found that this idea is not unfounded, for a few reasons:
1. First basemen do not require the quickness and agility of a middle infielder as they have less ground to cover
2. First basemen tend to be taller/bigger players in order to have a bigger range in catching throws to first base
3.  First base is an easier defensive position to play, so managers can afford to put players at that position who are stronger hitters than fielders

However, while I have anecdotal evidence and reasons to believe this is true, what do the data say?

<h2>Data</h2>
I obtained a dataset from Kaggle that includes every at bat by every player in Major League baseball from 1901 through 2021
There are over 4.2 million observations in this dataset, where each observation is a player’s hitting statistics for a single game
To compute the metrics noted on the previous slide, I will need the following variables:
Player position (categorical with nine levels): the position a player plays in the field
At bats (numerical): the number of at bats a player had during a game.  An at-bat is defined at a plate appearance that results in a hit or an out.  In particular, it excludes walks.
Hits (numerical): the number of hits a player had in a game
Doubles (numerical): the number of doubles a player had in a game
Triples (numerical): the number of triples a player had in a game
Home runs (numerical): the number of home runs a player had in a game
In addition to these raw metrics, I will need the number singles a player hit in a game, which can be computed by taking the number of hits and subtracting the number of doubles, triples, and home runs
As I am comparing these metrics of first basemen vs. other position players, I will need to aggregate my data by position
The metrics that I am computing (batting average, slugging percentage, isolated power, and home run percentage) are based on at-bats, singles, doubles, triples, and home runs
![image](https://github.com/milansherman2/EDA-in-Python/assets/85588082/e5e376cd-60a6-4dd0-897a-a926ac93044e)


<h2>Results</h2>
<p>The outcome of my exploratory data analysis demonstrated a few things:</p>
1. The data supports the hypothesis that first basemen are better power hitters than other field players.
2. Slugging percentage is a better predictor of runs scored than batting average.
3. There exists a correlation with at-bats and slugging percentage and batting average, so that players with more at-bats generally have higher batting averages and slugging percentages.  The direction of this relationship is unknown, but is likely bidirectional, i.e., players who hit more get better at it, and players who are better hitters will likely get more opportunities to hit.  

As far as other variables is concerned, it would have been interesting to know which side of the plate a player batted from, for a couple of reasons.   
1.	My intuition suggests that there is a higher proportion of left-handed baseball players than the general population.  Historically, players who bat from the left side of the plate hit better against right-handed pitchers than right-handed hitters.  As most pitchers are right-handed, left-handed hitters may be more highly valued.  Having this data would allow us to determine if indeed the proportion of left-handed baseball players is higher than the general population.
2.	There also seems to be a higher proportion of first basemen who are left-handed, with good reason.  A first baseman lines up just to the right of the foul line, meaning that most hits that they would have to field will be to their right.  A left-handed player throws with their left hand and has their glove on their right hand.  So if the ball is hit to their right, a left-handed first basemen is better prepared to prevent a base hit as they can reach farther to their right than a player with their glove on their left hand.  If it is true that first basemen are left-handed more often than other players, it would be interesting to then explore these hitting metrics based on which side of the plate a player hits from.

In terms of assumptions, there is an implicit assumption about the value of power hitting.  While we showed that power hitting is a more predictive metric than batting average with respect to runs scored, the question about whether first basemen tend to be better power hitters somewhat assumes that power hitters are valuable.  Another metric that is highly correlated with runs scored is base-out percentage, which is the ratio of the number bases a player nets to the number of outs that they generate.  In this analysis, we explored a hypothesis about power hitting and first basemen.  A more open question is which types of players tend to have the best base-out percentage?  A further assumption is about the values of runs scored.  Ultimately, scoring runs is only half of the equation.  No matter how many runs your team scores, you will still lose if your opponent scores more.  

A few things that would improve this analysis:
1.	I conducted a hypothesis test on the difference of means between first basemen and other field players (except pitchers) for each of three power hitting metrics, which showed that the difference between first basemen and all other field players as a group is statistically significant.  An open question is whether first basemen are better power hitters compared to each type of field player.  For example, right fielders were the second highest in each of the three power hitting metrics behind first basemen.  But when combined with other field positions that are much worse power hitters, we fail to answer the question as to whether first basemen are better power hitters than right fielders.  To answer this question, we would need to conduct an ANOVA, and likely a post hoc analysis.
2.	Given the correlation noted above between at-bats and the hitting metrics used in this analysis, it would be useful to control for number of at bats by replicating the analysis after creating separate groups based on number of at-bats to see if the results hold.  For example, it would be worth splitting this data into players with fewer than 2000 at-bats and those who had more and seeing if the results remain the same for both groups.

