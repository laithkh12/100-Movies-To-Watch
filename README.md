# 🎥 Best Movies Scraper
## 📝 Overview
This Python script scrapes a list of movies from a specified webpage on Empire Online and saves the titles in reverse order to a text file, movies.txt. By leveraging the Wayback Machine, it accesses a cached version of the page to avoid issues due to website updates.
## 📚 Requirements
This script requires the following Python libraries:
- requests
- BeautifulSoup (part of bs4)
To install these packages, run:
```bash
pip install requests beautifulsoup4
```
## 🚀 Usage
1. Set the URL: The script uses a cached URL from the Internet Archive's Wayback Machine:
```python
URL = "https://web.archive.org/web/20200518073855/https://www.empireonline.com/movies/features/best-movies-2/"
```
2. Run the Script: Execute the script to generate a movies.txt file with a list of the movies.
3. Check the Output: The movies.txt file will contain the movies in reverse order, starting from the most recent to the oldest.
## 📖 Code Breakdown
- **Step 1**: Make an HTTP GET request to the provided URL to retrieve the HTML content.
- **Step 2**: Parse the HTML content using BeautifulSoup.
- **Step 3**: Locate all movie titles by finding the <h3> tags with the class "title".
- **Step 4**: Reverse the order of the movie titles and save them to movies.txt.
### Script
```python
import requests
from bs4 import BeautifulSoup

URL = "https://web.archive.org/web/20200518073855/https://www.empireonline.com/movies/features/best-movies-2/"

response = requests.get(URL)
website_html = response.text

soup = BeautifulSoup(website_html, "html.parser")
all_movies = soup.find_all(name="h3", class_="title")
movie_titles = [movie.getText() for movie in all_movies]
movies = movie_titles[::-1]

with open("movies.txt", mode="w") as file:
    for movie in movies:
        file.write(f"{movie}\n")
```
## ❓ FAQ
Why use the Internet Archive's Wayback Machine?
Empire Online's website structure has changed, making the original selector (h3.title) invalid. Using a cached version ensures the script continues to work as intended.
---
