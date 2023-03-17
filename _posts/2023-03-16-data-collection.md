---
layout: post
title:  "Data Collection - Oscars and Ratings"
author: Kaylee Dial
description: This blog post will go through the steps of creating a dataset built from Oscars data used in a previous post and web scraping techniques on the Rotten Tomatoes site. 
image: https://github.com/kayleedial/my386blog/raw/main/assets/images/eeaao_3.jpeg
---

Since my last blog, I've had the pleasure of watching the 95th annual Oscars award show. The biggest winner of the night was undoubtedly <i>Everything Everywhere All At Once</i>, taking home seven Oscars, including best picture. I'm not sure what it was about the mother-daughter dynamics of a Chinese immigrant family and their story told via martial arts across multiple dimensions that made this the clear winner of best picture, but I'm in full support of the academy's choice on this one.

![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/eeaao_2.jpeg)

It does beg the question, what traits does this movie share with other best picture winners? How does it differ from the losers? Was there a way to know that this movie would fair well with the academy? 

It can be tricky to predict something that feels so subjective. After all, this isn't actually about predicting the best movie of the year. It's about predicting what an exclusive group of fancy people in LA thought was the best movie of the year. 

To make things interesting, I wanted to bring in a metric from a group of critics a little less fancy and arguably a little more in touch: Rotten Tomatoes. 
![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/rottom.png)

In my [first blog](https://kayleedial.github.io/my386blog/2023/02/08/tutorial.html) I showed an example of merging datasets using historical academy awards data from kaggle (link it). I'll be using that dataset in conjunction with data gathered via webscraping on the [Rotten Tomatoes Website](https://www.rottentomatoes.com/). 

To ensure that the data was collected ethically and that good webscraping practices were followed, no urls were used that the [robots.txt](https://www.rottentomatoes.com/robots.txt) file disallowed (/search and /user/id/).


The Oscars dataset I started out with looked like:
![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/oscarsdf.png)

I only wanted to consider best picture (or best motion picture) movies, so I filtered all other categories out of the dataset. 

```
bp = oscars[(oscars['category'] == 'best picture') | (oscars['category'] == 'best motion picture')]
```
I used libraries like [requests](https://pypi.org/project/requests/) and [Beautiful Soup](https://tedboy.github.io/bs4_doc/) to help me in the webscraping process. 

Unfortunately, there wasn't a single list or webpage of every oscar nominee for best picture on Rotten Tomatoes. Instead, I had to collect the urls of any webpage of oscars data throughout the years that I could find. Instead of setting one link equal to url, I created a list of all the links. 
```
url_list = ['https://editorial.rottentomatoes.com/guide/oscars-2023-best-picture-nominees/',
            'https://editorial.rottentomatoes.com/guide/2022-best-picture-nominees/', 
            'https://editorial.rottentomatoes.com/guide/2021-best-picture-nominees-ranked-by-tomatometer/',
            'https://editorial.rottentomatoes.com/guide/oscars-2020-best-picture-nominees-ranked-by-tomatometer/',
            'https://editorial.rottentomatoes.com/article/oscars-2019-best-picture-nominees/',
            'https://editorial.rottentomatoes.com/article/all-2018-oscar-best-picture-nominees-by-tomatometer/',
            ... # concatenated
            ]

```

I wanted to collect the movie title, rotten tomato score, year, and the critic review for each movie on each webpage. I created an empty dataframe to hold each of these metrics.

```
toms = pd.DataFrame(columns=['Title', 'Tomato Score', 'Year', 'Critic Review'])
```

This is where the true webscraping happens. These six steps walk through the code below.

1. The code starts by iterating through a list of URLs called url_list. For each URL in the list, it sends a GET request using the requests library and saves the response as a variable.

2. The response object is then passed into the BeautifulSoup constructor. This creates a BeautifulSoup object, which holds the HTML content of the webpage.

3. The code then uses the soup.find_all() method to extract all of the HTML elements that have a <div> tag and a "countdown-item-content" class. This returns a list of all the movies on the webpage.

4. The code then iterates through this list of movies, using the find() method to extract the title, tomato score, year, and critic review for each movie. These values are saved to variables.

5. The code appends this data to a pandas DataFrame.

6. Once all the URLs have been scraped, the code prints out the entire DataFrame.

```
for url in url_list:
    response = requests.get(url)
    soup = BeautifulSoup(response.content, 'html.parser')
    
    movies = soup.find_all('div', {'class': 'countdown-item-content'})
    
    for movie in movies:
        title = movie.find('a').text
        tomato_score = movie.find('span', {'class': 'tMeterScore'}).text
        year = movie.find('span', {'class': 'subtle start-year'}).text
        critic_review = soup.find('div', {'class': 'info critics-consensus'}).text.strip()
        
        toms = toms.append({'Title': title, 'Tomato Score': tomato_score, 'Year': year, 'Critic Review': critic_review}, ignore_index=True)

print(toms)
```

The Rotten Tomatoes dataset we get from this code looks like: 
![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/tomatdf.png)

Some cleaning needed to be done before this information could be merged with the Oscars dataset. First, I dropped duplicates from the dataframe, which took us from 572 rows to 444 rows. 

```
tomats = toms.drop_duplicates()
```

I cleaned up the Year column by taking off the parenthesis and the Critic Review column by removing "Critics Consensus: "
```
tomats['Year'] = tomats['Year'].str.replace('(', '').str.replace(')', '')
tomats['Critic Review'] = tomats['Critic Review'].str.replace('Critics Consensus: ', '')
```

There were were five instances of a different movie with the same movie title found in the Rotten Tomatoes dataset. To handle this, I found the version that exists in the Oscars dataset, and removed the other version from the Rotten Tomatoes dataset. 

Example:
```
tomats[tomats['Title'] == 'Cleopatra']
bp[bp['film'] == 'Cleopatra'] # it's only been a nominee once (1963/56% version)
# remove the other version:
tomats = tomats[~((tomats['Title'] == 'Cleopatra') & (tomats['Tomato Score'] == '82%'))]
```
Once the cleaning was done, I changed Rotten Tomatoes' "Title" column to "film", and merged the two datasets on that column.
```
tomats['film'] = tomats['Title']
tomats = tomats.drop('Title', axis=1)

df_m = pd.merge(bp, tomats, how='inner', on=['film'])
```

The Oscars dataset from Kaggle had not been updated with the results of the 95th Oscars awards, so the 'winner' column had NAs. The final step in preparing this dataset was to fill all these NAs with 'False', then set <i>Everything Everywhere All At Once</i> to 'True'.
```
df_m['winner'] = df_m['winner'].fillna(False)
df_m.loc[df_m['film'] == 'Everything Everywhere All at Once', 'winner'] = True
```
The last five columns of our scraped, cleaned, and merged dataset looks like this:
![Image](https://github.com/kayleedial/my386blog/raw/main/assets/images/finaldf.png)

The full dataset can be found [here](https://github.com/kayleedial/Blog-3a-data-collection/movies.csv)
Conclusion: introduce the next part of the EDA, get them excited

Link the repo