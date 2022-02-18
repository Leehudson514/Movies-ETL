# Movies-ETL
## Overview
* The client is outsourcing their project to a hackathon case competition which will be to create an algorithm that will determine which low budget movie release will become popular in the future so they could acquire the streaming rights at a low cost. 
* Our Purpose was to extract a large amount of raw data from different sources and provide a clean SQL summary of the data for the competition participants .
## Results
* Two final tables were created as the end results that contained clean "ratings data" and "movie data" that is accessible through SQL.
* The orginal **raw data had 40+ columns** and the final version for participants was **cleaned to 23 useful columns.**
* The final count of rows fpr the ratings table was 26,024,289.
* The final count of rows for the mobies table was 6,052.

![goals](https://github.com/Leehudson514/Movies-ETL/blob/main/Resources/ratings_query.png)

![goals](https://github.com/Leehudson514/Movies-ETL/blob/main/Resources/movies_query.png)

## Summary
* The raw data had too many columns that were not useful to case participants which means it needed to be filtered down to a reasonable size. 
* One example this was done through the following code which goal was to filter out "alternative movie titles":
```
def clean_movie(movie):
    movie = dict(movie) #create a non-destructive copy
    alt_titles = {}
    # combine alternate titles into one list
    for key in ['Also known as','Arabic','Cantonese','Chinese','French',
                'Hangul','Hebrew','Hepburn','Japanese','Literally',
                'Mandarin','McCune-Reischauer','Original title','Polish',
                'Revised Romanization','Romanized','Russian',
                'Simplified','Traditional','Yiddish']:
        if key in movie:
            alt_titles[key] = movie[key]
            movie.pop(key)
    if len(alt_titles) > 0:
        movie['alt_titles'] = alt_titles

    # merge column names
    def change_column_name(old_name, new_name):
        if old_name in movie:
            movie[new_name] = movie.pop(old_name)
    change_column_name('Adaptation by', 'Writer(s)')
    change_column_name('Country of origin', 'Country')
    change_column_name('Directed by', 'Director')
    change_column_name('Distributed by', 'Distributor')
    change_column_name('Edited by', 'Editor(s)')
    change_column_name('Length', 'Running time')
    change_column_name('Original release', 'Release date')
    change_column_name('Music by', 'Composer(s)')
    change_column_name('Produced by', 'Producer(s)')
    change_column_name('Producer', 'Producer(s)')
    change_column_name('Productioncompanies ', 'Production company(s)')
    change_column_name('Productioncompany ', 'Production company(s)')
    change_column_name('Released', 'Release Date')
    change_column_name('Release Date', 'Release date')
    change_column_name('Screen story by', 'Writer(s)')
    change_column_name('Screenplay by', 'Writer(s)')
    change_column_name('Story by', 'Writer(s)')
    change_column_name('Theme music composer', 'Composer(s)')
    change_column_name('Written by', 'Writer(s)')

    return movie
    ```
