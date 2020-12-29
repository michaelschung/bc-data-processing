# Notes on these data sets

## Stock market data

I added two more data sets, named `SPY.csv` and `TLT.csv`. The SPY data came from [here](https://finance.yahoo.com/quote/SPY/history?period1=728265600&period2=1609113600&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true), which showed up when I searched "SPY ETF data over time csv," and the TLT data came from [here](https://finance.yahoo.com/quote/TLT/history?period1=1027987200&period2=1609113600&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true), which showed up when I searched "TLT bond data over time csv." Both of those Google search queries were based on your email where you told me what you needed.

On each of those pages linked above, I set the Time Period to "Max" and the Frequency to "Daily," and then just clicked the Download button. I hope they're what you're looking for!

---

## Chess data

Unfortunately, the link you provided for exploring opening moves on 365chess.com could not be scraped into CSV files. Instead, I did my best to find an extensive data set that might possibly work. I found [this one](https://www.kaggle.com/penchalaiah123/chess-game-dataset) on Kaggle and downloaded it to the file named `lichess-games.csv`. It's not data from professional players, but I hope it can help you do some good analysis anyway!

### Update: added massive chess data set

I found [another data set](https://www.kaggle.com/milesh1/35-million-chess-games), this time containing data from over 3.5 million games (3,561,470 to be exact). As a single file, the data took up more than 2.5GB, which is too large of a file size for Github to allow. Thus, I split up the data into 30 files, each containing 120,000 lines – all of which can be found inside the `chess-data-chunked` folder.

In order to use the data from the 3.5M chess games, each of the 30 files must be merged into a single DataFrame. I've provided a code snippet below that does that for you. Simply paste the snippet into a code cell in Colab, and it'll read and combine all 30 CSV files into a single DataFrame called `chess`. (Note that this cell will take upwards of a minute to run, since it's dealing with such a large amount of data. Be patient with it!)

```python
# Make sure you've already imported pandas as pd!

chess_url = 'https://raw.githubusercontent.com/michaelschung/bc-data-processing/master/datasets/final-projects/sean/chess-data-chunked/chess-data-{}.csv'

all_dfs = []
for i in range(1, 31):
  all_dfs.append(pd.read_csv(chess_url.format(i), index_col=0))
chess = pd.concat(all_dfs)

chess
```

If you choose to use this massive data set, I _highly_ recommend that you develop and test your code using just one of the files with 120K lines. Then, when you're confident that your code works as intended, paste in the code snippet above to use the entire 3.5M lines. This will save you a lot of wait time while you're just trying to refine your code.
