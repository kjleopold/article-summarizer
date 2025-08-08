# Final Project: Spotify API and LyricGenius Analysis

Complete the tasks in the Python Notebook in this repository.
Make sure to add and push the pkl or text file of your scraped html (this is specified in the notebook)

## Rubric

* (Question 1) Article html stored in separate file that is committed and pushed: 1 pt
* (Question 2) Polarity score printed with an appropriate label: 1 pt
* (Question 2) Number of sentences printed: 1 pt
* (Question 3) Correct (or equivalent in the case of multiple tokens with same frequency) tokens printed: 1 pt
* (Question 4) Correct (or equivalent in the case of multiple lemmas with same frequency) lemmas printed: 1 pt
* (Question 5) Histogram shown with appropriate labelling: 1 pt
* (Question 6) Histogram shown with appropriate labelling: 1 pt
* (Question 7) Cutoff score seems appropriate given histograms: 2 pts (1/score)
* (Question 8) Summary contains a shortened version of the article (less than half the number of sentences): 1 pt
* (Question 8) Summary sentences are in the same order as they appeared in the original article: 1 pt
* (Question 9) Polarity score printed with an appropriate label: 1 pt
* (Question 9) Number of sentences printed: 1 pt
* (Question 10) Summary contains a shortened version of the article (less than half the number of sentences): 1 pt
* (Question 10) Summary sentences are in the same order as they appeared in the original article: 1 pt
* (Question 11) Polarity score printed with an appropriate label: 1 pt
* (Question 11) Number of sentences printed: 1 pt
* (Question 12) Thoughtful answer based on reported polarity scores: 1 pt
* (Question 13) Thoughtful answer based on summaries: 1 pt

## Objective
Access the Spotify API using OAuth authentication to retrieve information from a selected playlist. Extract and format the top 10 tracks from the returned JSON data and print them as a list. Then, use the Genius API with authentication to pull lyrics from one of the top 10 songs and print a snippet of those lyrics. Finally, perform sentiment analysis on the lyrics using both token-based and lemma-based approaches, generate summaries for each, print their polarity scores, and discuss the results.

### Step 1: Fork the base repo and copy to local machine
* Fork [Base Repository](https://github.com/wmnlp-materials/article-summarizer)
* `git clone` [(https://github.com/kjleopold/article-summarizer)](https://github.com/kjleopold/article-summarizer)

### Step 2: Set Up and Activate Virtual Environment
* `python -m venv .venv`
* `.venv/Scripts/activate`
* Select appropriate interpreter
    - Ctrl + Shift + P
    - Python: Select Inerpreter
    - Choose .venv\Scripts\python.exe

### Create .gitignore and Install Packages
* Create .gitignore.
* Create requirements.txt to install packages.
* `pip install -r requirements.txt`

### Open Notebook and Complete Tasks
* Make sure kernel is selected.
* Add a viewable, clickable link to GitHub repo after name in the Markdown Introduction.
* Use Markdown headings to show content by each question number.
* Complete the questions.
  * Create a .env to store OAuth authentication codes for Spotify and Genius API.
  * `SPOTIPY_CLIENT_ID=Add Spotify Client ID`
  `SPOTIPY_CLIENT_SECRET=Add Spotify Client Secret Code`
  `SPOTIPY_REDIRECT_URI=Rediret URI must match exactly`
  `GENIUS_API_TOKEN=Add Genius API Token`
  * Set up .py to pull the access token automatically and store it with a funcion named get_token  
```
import os
from dotenv import load_dotenv
from spotipy.oauth2 import SpotifyOAuth

load_dotenv()

def get_token(scope="user-library-read"):
    sp_oauth = SpotifyOAuth(
        client_id=os.getenv('SPOTIPY_CLIENT_ID'),
        client_secret=os.getenv('SPOTIPY_CLIENT_SECRET'),
        redirect_uri=os.getenv('SPOTIPY_REDIRECT_URI'),
        scope=scope
    )
    token_info = sp_oauth.get_access_token(as_dict=False)
    return token_info
```

  * To the function for the Spotify API from the saved .env
```
from get_spotify_token import get_token

ACCESS_TOKEN = get_token()
```

  * Same for Genius API
```
# Get lyrics for a top 10 song
from dotenv import load_dotenv

# Load environment variables
load_dotenv()
GENIUS_API_TOKEN = os.getenv("GENIUS_API_TOKEN")
if not GENIUS_API_TOKEN:
    raise ValueError("GENIUS_API_TOKEN not found in environment variables")

# Setup Genius
genius = lyricsgenius.Genius(GENIUS_API_TOKEN, timeout=15, retries=3)
genius.skip_non_songs = True
genius.excluded_terms = ["(Remix)", "(Live)"]
genius.remove_section_headers = True
```

### Execute the notebook

### Commit and push to GitHub
* `git add .`
* `git commit -m "Meaningful comment"`
* `git push`
* Verify the notebook appears correctly in GitHub.

### Export to HTML and Finalize Repo
* `!jupyter nbconvert --to html web-scraping.ipynb`
