# Spotify Top Artist Predictor

A data science project that predicts who my top Spotify artist will be, using my own Spotify extended streaming history.

## Data

The data comes from my personal Spotify data request (Extended streaming history). It is not included in this repository because it is personal.

Files used:
- `Streaming_History_Audio_2026.json`
- `Streaming_History_Audio_2026_1.json`
- `Streaming_History_Audio_2026_2.json`

`Streaming_History_Video_2026.json` is not used.

Key columns: `ts` (timestamp), `master_metadata_album_artist_name` (artist), `master_metadata_track_name` (track), `ms_played`, `skipped`, `shuffle`, `platform`.

## Approach

1. Load and combine the audio history files into one DataFrame.
2. Clean the data: remove duplicates, drop rows with no artist, and drop very short plays.
3. Aggregate listening time (minutes) per artist per week.
4. Build features from past weeks, such as recent minutes, growth rate, share of total listening and skip rate.
5. Predict each artist's listening time for the next week. The artist with the highest prediction is the predicted top artist.
6. Compare models against a simple baseline ("next top artist = last week's top artist").

## Evaluation

- Time-based train/test split (train on the past, test on the future)
- Top-1 accuracy and top-3 hit rate
- MAE on predicted minutes

## Setup

```bash
pip install -r requirements.txt
```

Put your Spotify JSON files in the project folder, then open the notebook and run the cells in order.

## Project Structure

```
Spotify project/
├── Streaming_History_Audio_*.json   # raw data (not committed)
├── requirements.txt
├── notebook.ipynb                   # analysis and modelling
└── README.md
```

## Status

In progress. Data loading done; feature engineering and modelling next.
