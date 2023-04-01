---
layout: post
title:  "Data Exploration - Oscars and Ratings"
author: Kaylee Dial
description: Exploring and visualizing Oscars Data
image: https://github.com/kayleedial/my386blog/raw/main/assets/images/edabanner.png
---

## Overview
Welcome to my third blog about Oscar winning movies. In this blog we'll be exploring and visualizing the dataset I curated in my last blog of Oscar movies and Rotten Tomato scores.

While there is some bias and personal preference when it comes to picking out the best movies, we know that it's not completely subjective. Many people can agree that certain movies are terrible and certain movies are great. Just like how "Surf's Up" (2007) is an objectively better penguin movie than "Happy Feet" (2006), there are some qualities that make a movie better than another.
 
That being said, you would think that Rotten Tomato Critics and the Academy would be aligned on the movies they claim to be the best; if a movie were to get above 90% on Rotten Tomatoes, it's probably safe to assume that movie would get some nominations at the Oscars. 

Well, suprise! That's not really the case. One of the best actress performances I saw last year was from Mia Goth in "Pearl" (2022). It got a 92% on Rotten Tomatoes, yet didn't get a single nomination in the 2023 Oscars Ceremony. 

Look at how scary this face is. You're really not going to give her a nomination, @Academy? Be real. 

![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/pearl.jpg)

## The Data

We'll be exploring the relationships between the variables in the movies dataset I created in the last blog. This combined an Oscar's dataset with ratings scraped from the Rotten Tomatoes website. That blog is linked [here](https://kayleedial.github.io/my386blog/2023/03/16/data-collection.html) if you want to check it out.

The dataset looks something like this:

![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/data_eda.png#center)

- Ceremony: the Oscars ceremony number
- Name: the studio or production company
- film: the movie title
- winner: True or False if the movie won best picture
- Tomato Score: the Rotten Tomato score (0.0-1.0) 
- Year: the year the film came out
- Critic Review: the review from Rotten Tomatoes
- Nomination Count: the count of nominations received in a ceremony 

## Visualizing 

The first thing I wanted to explore was the relationship between Oscar nominations and Rotten Tomato Score. Each point on this scatter plot represents a movie in our dataset (all nominations for best picture). It shows the number of nominations received in any category in one award show on the y-axis. This is plotted against their Rotten Tomato Score out of 100% on the x-axis. Whether or not a movie won the best picture award is indicated by the color.

<center><img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/scatter_all.png" alt="Scatter Plot" width="500"/></center>

It's not surprising that most of the points hover between the 80%-100% mark. I was suprised by the way the orange points (winners of best picture) were dispersed among the blue points. You'd expect best picture winners to be clustered towards the top, but they seem to be pretty evenly distributed throughout the blue points.

This visual shows only the winners, with a few interesting outliers labeled. 

<center><img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/scatter_wins.png" alt="Scatter Plot" width="500"/></center>

- "Coda" won best picture in 2022, yet received an abnormally low number of total nominations. 

- "Out of Africa" won best picture at the 1986 Oscars, yet was given a low Rotten Tomatoes score of 61%.

- "The Greatest Show on Earth" won best picture in 1953, yet got the lowest Rotten Tomatoes score of any winner in this dataset: 49%. 

<p><img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/africa.jpg" alt="Africa", width="250">
<img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/show.jpg" alt="Greatest Show", width="250">
</p>

When I first looked at the points for "Out of Africa" and "The Greatest Show on Earth", I thought that the discrepancy between the Academy and Rotten Tomatoes were due to the age of these movies. It would make sense that movie quality and criteria for good movies has changed over time. 

To test this theory, I created the plot below that shows the average Tomato Score for winners over the years:

<center><img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/score_years.png" alt="Scores over Years" width="500"/></center>

We can see where "The Greatest Show on Earth" and "Out of Africa" are dragging the average down around 1953 and 1986. Besides that, there isn't a very obvious increase of average Tomato Scores happening throughout the years. In fact, one of the most consistently high average score time periods looks to be between 1970-1980. 

This made me interested to see where the highest Rotten Tomato Scores were given over time. This plot shows every Rotten Tomato Score in this dataset given over 97% and the year it was given in. 

<center><img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/top_scores.png" alt="Top Scores" width="500"/></center>

In this dataset, there hasn't been a nomination that had 100% on Rotten Tomatoes since 1971. It makes me wonder if movies aren't as "good" as they used to be, or if the Rotten Tomato criteria has become more strict. Or maybe "the best" according to the Oscars versus Rotten Tomatoes is different from one another. 

This last visual shows a spread of the nominees versus the winners plotted with their Tomatoes score. 

<center><img src="https://github.com/kayleedial/my386blog/raw/main/assets/images/boxes.png" alt="Boxplot" width="500"/></center>

The mean for winners is a little higher for nominees, which is expectyed, but it's interesting that the max Tomato Score for nominees is higher than the max for winners.

## Conclusion

To wrap up, I found that the Rotten Tomatoes critics and the Academy like to have their own opinions on which movies are the best of the best. Though average Rotten Tomatoes scores for best picture winners oscilate, they have remained relatively level over the years. If you have any questions or want to talk about how awesome "Surf's Up" is, feel free to leave a comment. 