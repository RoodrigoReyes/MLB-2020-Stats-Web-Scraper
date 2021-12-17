# MLB 2020 Stats Web Scraper
![alt text](https://gray-kvly-prod.cdn.arcpublishing.com/resizer/k9dD9Um3nwV3ZeRLo0AoC6dQGfc=/1200x675/smart/filters:quality(85)/cloudfront-us-east-1.images.arcpublishing.com/gray/APSOXLYZTFMPTOMQ6I6O3THNEU.jpg "MLB 2020 Season")
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
The data was cleaned by correcting the 'PLAYER' column to obtain, first, the position of each player.<br />
```python
df['PLAYER'] = df['PLAYER'].str.rstrip('âââ')
```
```python
#Get the positions of the players from the 'PLAYER' column
def unique(sequence):
    seen = set()
    return [x for x in sequence if not (x in seen or seen.add(x))]
posit=[]
for i in df['PLAYER']:
    m = unique(re.findall('[A-Z][^A-Z]*', i))
    if 'X' in m[-1]:
        posit.append('X')
    elif 'C' in m[-1]:
        posit.append('C')
    elif 'P' in m[-1]:
        posit.append('P')
    else:
        m = m[-2][-1]+m[-1][0]
        posit.append(m)
```
To then create the column 'POSITION' with the data extracted previously.<br />
```python
df.loc[:,'POSITION'] = posit
```
We obtain the player's first and last name with the following for loops.
```python
for i in df['PLAYER']:
    i = ''.join(filter(str.isalpha,i))
    
from string import printable
for i in range(len(df)):
    df['PLAYER'][i] = ''.join(filter(str.isalpha, df['PLAYER'][i]))
    m = unique(re.findall('[A-Z][^A-Z]*', df['PLAYER'][i]))
    set(m[2]).difference(printable)

    if set(m[2]).difference(printable):
        m.pop(2)
        df['PLAYER'][i] = str(m[0]+" "+m[2])
    else:
        df['PLAYER'][i] = str(m[0]+" "+m[2])
```
I save the player's data in a file called 'mlb_players_data.xlsx', where later it will be possible to make graphics either in Power BI or Tablue for further analysis.
```python
#Saving the data in a new file in xlsx format. called: 'mlb_players_data.xlsx'
df.to_excel('mlb_players_data.xlsx',index=False)
```
