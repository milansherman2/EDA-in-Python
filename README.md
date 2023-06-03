# EDA-in-Python
Are First Basemen Power Hitters?

  <h2>Languages Used</h2>
  
- <b>Python</b>


<h2>Overview</h2>
<p>In my experience following baseball, I have found that first basemen are often the power hitters on the team.  A power hitter can be loosely defined as a player has more extra base hits (versus singles).</p>

I did some research and found that this idea is not unfounded, for a few reasons:
1. First basemen do not require the quickness and agility of a middle infielder as they have less ground to cover
2. First basemen tend to be taller/bigger players in order to have a bigger range in catching throws to first base
3.  First base is an easier defensive position to play (fewer hits come to first basemen and they rarely have to make a throw), so managers can afford to put players at that position who are stronger hitters than fielders. 

However, while I have anecdotal evidence and reasons to believe this is true, what do the data say?

<h2>Data</h2>
<p>I obtained a dataset from Kaggle that includes every at bat by every player in Major League baseball from 1901 through 2021 (https://www.kaggle.com/datasets/darinhawley/mlb-batting-stats-by-game-19012021).  There are over 4.2 million observations in this dataset, where each observation is a player’s hitting statistics for a single game, so data cleaning and aggregation were necessary to get the data needed to answer the question.</p>

I generated the following for each player:
- <b>Player position</b> (categorical with nine levels): the position a player plays in the field
- <b>At bats</b> (numerical): the number of at bats a player had during a game.  An at-bat is defined at a plate appearance that results in a hit or an out.  In particular, it excludes walks.
- <b>Hits</b> (numerical): the number of hits a player had in a game
- <b>Doubles</b> (numerical): the number of doubles a player had in a game
- <b>Triples</b> (numerical): the number of triples a player had in a game
- <b>Home runs</b> (numerical): the number of home runs a player had in a game
- <b>Single</b> (numerical): the number of singles a player had in a game, computed by taking the number of hits and subtracting the number of doubles, triples, and home runs
- <b>Batting average</b> (numerical): the number of hits divide by the number of at-bats
- <b>Slugging percentage</b> (numerical): [singles + 2(doubles) + 3(triples) + 4(home runs)]/at-bats
- <b>Isolated power</b> (numerical): slugging percentage - batting average
- <b>Home run percentage</b> (numerical): home runs/at-bats.  We include home run percentage to normalize home runs relative to the number of at-bats.

After each of these were generated for each player and each game, the data were aggregated by position in order to compare first basemen with other positions.  Pitchers were excluded from the analysis as they are notoriously bad hitters, and they don't even bat in the American League.


<h2>Results</h2>

High Level Takeaways:
- The data supports the hypothesis that first basemen are better power hitters than other field players.  This was substantiated via hypothesis testing on the difference of means between first basemen and non-first base position players (i.e., no pitchers) for the three power hitting metrics identified above.
- Slugging percentage is a better predictor of runs scored than batting average.  This was established through a higher correlation with runs scored and a comparison of linear models.
- There exists a correlation with at-bats and slugging percentage and batting average, so that players with more at-bats generally have higher batting averages and slugging percentages.  The direction of this relationship is unknown, but is likely bidirectional, i.e., players who hit more get better at it, and players who are better hitters will likely get more opportunities to hit.  

<b>Assumptions</b>:
<p>In terms of assumptions, there is an implicit assumption about the value of power hitting.  While we showed that slugging percentage is a more predictive metric than batting average with respect to runs scored, the question about whether first basemen tend to be better power hitters assumes that power hitters are valuable.  Another metric that is highly correlated with runs scored is base-out percentage, which is the ratio of the number bases a player nets to the number of outs that they generate.  
<p>In this analysis, we explored a hypothesis about power hitting and first basemen.  A more open question is which types of players tend to have the best base-out percentage?  A further assumption is about the values of runs scored.  Ultimately, scoring runs is only half of the equation.  No matter how many runs your team scores, you will still lose if your opponent scores more.

A few things that would improve this analysis:
1.	I conducted a hypothesis test on the difference of means between first basemen and other field players (except pitchers) for each of three power hitting metrics: slugging percentage, isolated power, and home run percentage.  These showed that the difference between first basemen and all other field players as a group is statistically significant.  An open question is whether first basemen are better power hitters compared to each type of field player.  For example, right fielders were the second highest in each of the three power hitting metrics behind first basemen.  But when combined with other field positions that are much worse power hitters, we fail to answer the question as to whether first basemen are better power hitters than right fielders.  To answer this question, we would need to conduct an ANOVA, and likely a post hoc analysis.
2.	Given the correlation noted above between at-bats and the hitting metrics used in this analysis, it would be useful to control for number of at bats by replicating the analysis after creating separate groups based on number of at-bats to see if the results hold.  For example, it would be worth splitting this data into players with fewer than 2000 at-bats and those who had more and seeing if the results remain the same for both groups.

