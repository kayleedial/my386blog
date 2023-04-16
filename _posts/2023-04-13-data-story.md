---
layout: post
title:  "Data Story - the Best of the Best for Rotten Tomatoes versus the Academy"
author: Kaylee Dial
description: A walkthrough of my data story - Oscars and Rotten Tomatoes data
image: https://github.com/kayleedial/my386blog/raw/main/assets/images/dsbanner.png
---

## Introduction

This post will be summarizing the findings on Oscar awards versus Rotten Tomatoes ratings. In my post about [data collection](https://kayleedial.github.io/my386blog/2023/03/16/data-collection.html), I went through the steps to merge an Oscars dataset with information scraped from the Rotten Tomatoes website. The following post on [data exploration and visualization](https://kayleedial.github.io/my386blog/2023/03/30/oscars-eda.html) went over the movies dataset and showed different visuals highlighting the relationship between Oscar nominations and winners versus Rotten Tomato scores.

By visualizing that information, I learned that what the academy believes to be the best of the best (Oscar winners) isn't always what Rotten Tomatoes deems is the best of the best (98-100% on Rotten Tomatoes).

## Data Story

The last movie I saw that really made me feel something is <i>[Puss in Boots: The Last Wish](https://www.rottentomatoes.com/m/puss_in_boots_the_last_wish)</i>. I laughed, I felt joy, and a single tear fell from my eye, which feels crazy for an animated movie about warrior cats in boots. 

![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/pussinboots.png)

Just because I thought the movie was life-changing, that doesn't mean that it's everyone's experience. Rating a film is tricky because everyone has different standards for good. Is the criteria for a good movie to make you laugh, to make you feel good, to make you think, to make you cry? Everyone has their own definition of the best, but when we're looking at two of the most well-known groups of critics, they probably have a more technical and methodical way of rating movies that somewhat standardizes the process. With that in mind, how aligned are these two groups in determining which movies are the best? To answer this, I wanted a plot to show if the highest scoring Rotten Tomato Scores indicated that the film was a best picture winner or not. 

These are the best picture nominees from 2010-2023 with their Tomato Score indicated by the bars, and if they won the best picture indicated by color.

![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/MoviesScores.png)

Are they aligned on their opinions of the best movies? The answer is a definite.. kinda. If they were totally aligned, the orange bars would be taking over the bottom section of the graph. It looks like the most common Tomato score to win best picture from 2010-2023 isn't 100%, or 99%, or 98%, but 94%. Moral of the story, "best" does not mean the best indefinitely, just the best according to a group of people.

## Conclusion

This shows me that no matter how well-known and prestigious the group is, their choice for the best films is going to be a little subjective. I think this will help me be less angry when the academy makes a choice I don't like. 

Thank you for coming on this journey with me through Rotten Tomatoes and Oscars data. If you take anything from this blog post, please just see <i>Puss in Boots: The Last Wish</i> if you haven't already. As always, feel free to leave a comment below if you have anything to add. 

The visual was made using Tableau, and all other code from all previous blogs can be found is [this repository](https://github.com/kayleedial/Blog-3a-data-collection).