# Spotify top streams 2023

The Spotify Streaming Insights Dashboard is a sophisticated web application that leverages DAX, Dandeb, and HTML to provide Spotify users with an in-depth analysis of their music listening patterns. The dashboard presents a daily report featuring interactive data visualizations that reflect the user’s streaming activity.

## Key Features:

1. **Personalized User Experience**: A welcoming interface greets users by name and offers a snapshot of their recent listening activity.
2. **Track Analytics**: Utilizes DAX formulas to calculate and display detailed information about tracks, including artist, title, and listening date.
3. **Streaming Statistics**: Interactive bar graphs, powered by Dandeb, show the sum of streams per track, allowing users to visualize their most-listened songs.
4. **Yearly Trends**: Showcases the average number of streams per year with a percentage increase, highlighting user engagement over time.
5. **Energy Meter**: A pie chart, rendered using Dandeb, indicates the ‘Energy’ level of the user’s preferred tracks.
6. **Historical Data Correlation**: A line graph correlates track popularity with release dates, offering insights into the user’s evolving music tastes.

## Technologies Used:

- **DAX (Data Analysis Expressions)**: Utilized for calculating various metrics such as the sum of streams and average stream per year.
- **Dandeb**: Employed to power interactive data visualizations including bar graphs and pie charts.
- **HTML**: Used for structuring and presenting the dashboard interface.

## Objective:

The objective of the Spotify Streaming Insights Dashboard is to empower Spotify users with actionable insights into their streaming habits, enabling them to explore musical trends and gain a deeper appreciation of their personal music journey.

You can view the interactive dashboard [here](https://app.fabric.microsoft.com/view?r=eyJrIjoiZDJhOTRkNjktYmQ1ZC00YmRkLWFlOGMtYzhmMjRkMzIxMDBlIiwidCI6IjkwMzY2M2NiLWY5NGQtNGQzZC05NWY1LTBlNzk5MDNlNjE0ZSJ9).

---

```dax
# DAX Formulas Used

1. **Max Streams**: 
    ```
    Max streams = max('Spotify Dataset'[streams])
    ```

2. **Average Stream per Year**: 
    ```
    Average stream per year = CALCULATE(
           AVERAGE('Spotify Dataset'[streams]),
           ALLEXCEPT('Spotify Dataset','Date'[Year]))
    ```
## Additional Metrics

3. **Track Count**: 
    ```dax
    Track count = COUNT('Spotify Dataset'[track_name])
    ```

4. **Top Song vs Average Value**: 
    ```dax
    Top song vs avg val = DIVIDE([Top song streams] - [Average stream per year],
                                [Top song streams])
    ```

5. **Top Songs vs Average**: 
    ```html
    var x = [Top song vs avg val] 
    return
    if ( x > 0,
    FORMAT(x,"#.0%") & " " & UNICHAR(9650) ,
    FORMAT(x,"#.0%") & " " & UNICHAR(9660))
    ```
## HTML Code for Image Display

```html
var x = 
CALCULATE(MAX('Spotify Dataset'[cover_url]),
    'Spotify Dataset'[streams] = MAX('Spotify Dataset'[streams])
       )
return 
"<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <style>
        .image-container {
            width: 200%; /* Adjust as needed */
            max-width: 500px; /* Adjust as needed */
            height: 0;
            padding-bottom: 40%; /* 16:9 aspect ratio */
            overflow: hidden;
            position: relative;
            border-radius: 16px;
        }

        .image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>
    <div class='image-container'>
        <img src='"&x&"' alt='Image Description'>
    </div>
</body>
</html>

