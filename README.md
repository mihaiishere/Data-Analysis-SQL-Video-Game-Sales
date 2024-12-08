# Data-Analysis-SQL-Video-Game-Sales

In this project, we'll explore the sales and scores of video games created between 1977 and 2020. We'll compare a dataset of game sales with critic and user reviews to determine whether or not video games have improved as the gaming market has grown.

The database contains two tables. You can find the complete dataset with on [Kaggle](https://www.kaggle.com/datasets/holmjason2/videogamedata?resource=download)

`game_sales`

| Column | Type | Description |
| --- | --- | --- |
| `ID` | int | PK - distinct record number | 
| `Name` | varchar | Video Game Name |
| `Platform` | varchar | Game Platform |
| `Publisher` | varchar | Game Publisher |
| `Developer` | varchar | Game Developer |
| `Sold_Copies` | float | The number of sold copies |
| `Year` | int | Year of release |


`game_scores`

| Column | Type | Description |
| --- | --- | --- |
| `ID` | int | PK - distinct record number | 
| `Name` | varchar | Video Game Name |
| `Critic_Score` | varchar | The mark given by critics |
| `User_Score` | varchar | The mark given by users |

## Highest and missing scores

Let's look at the highest 10 scores first:

Input:
```
SELECT TOP(10) *
FROM game_sales
ORDER BY Sold_Copies DESC;
```

Output:
| ID	| Name	| Platform	| Publisher	| Developer	| Sold_Copies	| Year |
| ---	| ---	| ---	| ---	| ---	| ---	| --- |
| 1	| Wii Sports	| Wii	| Nintendo	| Nintendo EAD	| 82.9	| 2006 |
| 2	| Super Mario Bros.	| NES	| Nintendo	| Nintendo EAD	| 40.24	| 1985 |
| 3	| Counter-Strike: Global Offensive	| PC	| Valve	| Valve Corporation	| 40	| 2012 |
| 4	| Mario Kart Wii	| Wii	| Nintendo	| Nintendo EAD	| 37.32	| 2008 |
| 5	| PLAYERUNKNOWN'S BATTLEGROUNDS	| PC	| PUBG Corporation	| PUBG Corporation	| 36.6	| 2017 |
| 6	| Minecraft	| PC	| Mojang	| Mojang AB	| 33.15	| 2010 |
| 7	| Wii Sports Resort	| Wii	| Nintendo	| Nintendo EAD	| 33.13	| 2009 |
| 8	| Pokemon Red / Green / Blue Version	| GB	| Nintendo	| Game Freak	| 31.38	| 1998 |
| 9	| New Super Mario Bros.	| DS	| Nintendo	| Nintendo EAD	| 30.8	| 2006 |
| 10 | New Super Mario Bros. Wii	| Wii	| Nintendo	| Nintendo EAD	| 30.3	| 2009 |




And now let's check how many games have missing data for the scores.

Input:
```
SELECT COUNT(game_sales.Name) AS Count
FROM game_sales
LEFT JOIN game_scores ON game_sales.Name = game_scores.Name
WHERE Critic_Score IS NULL AND User_Score IS NULL;
```

Output:

| Count |
| --- |
| 17324 |



## Critics opinion

Now that we know the most 10 sold games and we have noticed that only a very small portion of data is missing reviews, let's check the top 10 years with the best scores according to critics.

Input:
```
SELECT TOP(10) Year, ROUND(AVG(Critic_Score), 2) AS Avg_Critic_Score
FROM game_sales
JOIN game_scores ON game_sales.Name = game_scores.Name
GROUP BY Year
ORDER BY Avg_Critic_Score DESC;
```
Output:
| Year	| Avg_Critic_Score
| ---	| ---
| 1984	| 9.5
| 1992	| 8.68
| 1990	| 8.54
| 1991	| 8.32
| 2020	| 8.26
| 1994	| 8.04
| 2019	| 7.97
| 1985	| 7.84
| 1993	| 7.72
| 2013	| 7.6


Since the average is not the most important point of view when checking the top 10 scores, let's also see how many games were reviewed in that year. We will also look for the top 10 years with atleast 10 titles.

Input:
```
select year, round(avg(critic_score),2) as avg_critic_score, count(name) as num_games from game_sales
join game_scores
using (name)
group by year
having count(name) > 10
order by avg_critic_score desc
limit 10
```

Output:


