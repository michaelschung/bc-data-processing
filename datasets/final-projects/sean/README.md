# Notes on these data sets

Unfortunately, the link you provided for exploring opening moves on 365chess.com could not be scraped into CSV files. Instead, I did my best to find an extensive data set that might possibly work. I found [this one](https://www.kaggle.com/penchalaiah123/chess-game-dataset) on Kaggle. It's not data from professional players, but I hope it can help you do some good analysis anyway!

## Update: added massive chess data set

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
