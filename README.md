# MLB 2020 Stats Web Scraper

This web scraper takes the data from each active player in the 2020 season in any position of the [MLB Web](https://www.mlb.com/stats/2020).<br />
The data collected from the players that could be obtained were the following:<br />
## Columns
|Data|Info|
|-------|:---|
|Player |Player's first and last name|
|Team |Name of the team|
|Games (G) |Games in which player has appeared.|
|At Bats (AB) |Trips to the plate that do not result in a walk, hit by pitch, sacrifice, or reach on interference.|
|Runs (R) |When a baserunner safely reaches home plate and scores.|
|Hits (H) |When a batter reaches base safety on a fair ball unless the batter is deemed by the official scorer to have reached on an error or a fielder's choice.|
|Doubles (2B) |When a batter reaches on a hit and stops at seconds base or only advances farther than second base on an error or a fielder's attempt to put out another baserunner.|
|Triples (3B) |When a batter reaches on a hit and stops at third base or only advances farther than third base on an error or a fielder's attempt to put out another baserunner.|
|Home Runs (HR) |When a batter reaches on a hit, touches all bases, and scores a run without a putout recorded or the benefit of error.|
|Runs Batted In (RBI) |Runs which socre because of the batter's safe hit, sac fly, infield out ot fielder's choice or is forced to score by a bases loaded walk, hit batter, or interference.|
|Walks (BB) |When a batter is awarded first base after four balls have been called by the umpire or the opposing team opts to intentionally award the batter first base.|
|Strikeouts (SO) |When the unpire calls three strikes on the batter.|
|Stolen Bases (SB) |When the runner advances one base unaided by a hit, a putout, an error, a force-out, a fielder's choice, a passed ball, a wild pitch,or a balk.|
|Caught Stealing (CS) |When a runner attemps to steals but is tagged out before safely attaining the next base.|
|Batting Average (AVG) |The rate of hits per at bat. (H/AB)|
|On-Base Percentage (OBP) |The rate at which a batter reached base in his place appearances. (H+BB+HBP)/(AB+BB+HBP+SF)|
|Slugging Percentage (SLG) |The rate od total bases per at bat. (1B+2Bx2+3Bx3+HRx4)/AB|
|On-Base Plus Slugging (OPS) |The sum of on-base percentage and slugging percentage. (OBP+SLG)|

## Cleaning the data
The data was cleaned, correcting the 'PLAYER' column in order to get the name and surname of each player.<br />
```python
df['PLAYER'] = df['PLAYER'].str.rstrip('âââ')
```
Then, from the same column 'PLAYER', the position of each player was obtained.
