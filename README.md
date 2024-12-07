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
select * from game_sales 
order by sold_copies desc 
limit 10
```

Output:


And now let's check how many games have missing data for the scores.

Input:
```
select count(name) from game_sales
left join game_scores
using (name)
where critic_score is null and user_score is null
```

Output:

## Critics opinion

Now that we know the most 10 sold games and we have noticed that only a very small portion of data is missing reviews, let's check the top 10 years with the best scores according to critics.

Input:
```
select year, round(avg(critic_score),2) as avg_critic_score from game_sales
join game_scores
using (name)
group by year
order by avg_critic_score desc
limit 10
```
Output:


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


