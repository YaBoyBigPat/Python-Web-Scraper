# Python-Web-Scraper

The main python code is in the NBAData.ipynb

Hello, I'm excited to post projects here!

This is my first python project following the video tutorial from Dataquest, "Web Scraping NBA Stats With Python: Data Project" on YouTube that attempts to scrape player data, clean it, and make it usable for machine learning to see if we can accurately predict players MVP ranking. https://www.youtube.com/watch?v=JGQGd-oa0l4&t=704s

Even though this project was done by following a YouTube tutorial (I did my best to follow along line by line so I could thoroughly learn and understand the project). I ran into my own challenges with this project and had to make changes along the way so it could work for me (which I expand on more down below). This project helped me learn about using python imports, pandas, web scraping techniques, data cleaning, debugging, and machine learning. I also learned a lot about communication through the command terminal. I plan on modifying it more so that it can also be used in Tableau for data analysis, seeing which stat columns work together when trying to improve the model's accuracy.


# Quick Project Overview

- The data came from the website, "https://www.basketball-reference.com/" where I got player statistic data from 1992-2022.
- This data included stats from players like points per game, average minutes played per game, 3-point percentage, etc.
- The goal of this project is to (somewhat) accurately predict player's rankings using the data we've collected over the years.
- For example, in our data Steve Nash is ranked #1 for MVP in 2005, our regression model predicted him to be ranked #46, and our Random Forest model predicted him to be ranked #12. 

# Some problems I ran into and solved:
1. Creating a different "years" list starting at 1992 because starting at 1991 gave a [429] error.
2. Making timers where I start to access the web page "https://www.basketball-reference.com/". That way I don't spam requests to the server and get an [429] error.
3. When cleaning the data some player names are spelled differently and use different charters for example Peja Stojakovi'. His names looked like that in the MVP data, but for the player data his name was, 'Peja Stojaković', so when merging I was getting incorrect information. To fix this I replaced his name in the MVP data with how it's represented in the player data.
4. Figuring out how to accurately run the Random Forest Regressor, playing around with the number of simulations and random states to try and improve accuracy. 

# Project Insights:

- Our error metric was about 81%
- The backtests mean accuracy precision (mean_ap) was, "0.7163491855092012", this is only using the original columns from the data I scraped: "predictors['Age','G','GS','MP','FG','FGA','FG%','3P','3PA','3P%','2P','2PA','2P%','eFG%','FT','FTA','FT%','ORB','DRB','TRB','AST','STL','BLK','TOV','PF','PTS','Year','W','L','W/L%','GB','PS/G','PA/G','SRS']"
- To give the regression model more data and improve its accuracy, we created a lambda function that calculates the mean of these -columns above throughout the years of data we have.
- These new columns are labeled "predictors += ["PTS_R", "AST_R", "BLK_R", "DRB_R", "GB_R", "W_R", "STL_R", "3P_R"]", and these columns are being added to the "predictors" list above.
- This improved our backtest to, mean_ap = 0.7226465820837664.
- Running our Random Forest Regressor without these columns and starting are predictions at 1997 gives us a mean_ap of, "0.7340772475387858". When starting at a recent year our model becomes more accurate, starting at 2019 and adding the predictor columns we created gives us an accuracy of mean_ap = 0.8491117216117215.
- The accuracy for the past years was improved to around 73%, but there are modifications we can make to possibly improve it further. 

