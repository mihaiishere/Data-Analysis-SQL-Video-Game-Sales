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
| `Game_Sales` | float | The number of sold copies |
| `Year` | int | Year of release |
