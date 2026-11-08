# Company News Monitor

A tiny, free RSS watcher that alerts you when your watchlist companies appear in the news — no API keys, no paid news service, no local install.

The whole tool is one Google Colab script: paste two cells, edit the watchlist, run.

## What it does

- Reads a list of free RSS feeds (Google News RSS works out of the box)
- Scans the latest 20 headlines from each feed
- Prints a match whenever a watchlisted company name appears in a headline, with the article link

Typical use cases: monitoring prospects before outreach, tracking competitors, watching suppliers or clients for negative press.

## Quick start

1. Open [Google Colab](https://colab.research.google.com) and create a new notebook.
2. Paste **Cell 1** (install) and **Cell 2** (watchlist + feeds) from the [`company news monitor`](./company%20news%20monitor) script, each into its own cell.
3. Run the cells in order.

No signup, no billing, no keys.

## Configuration

```python
watchlist = ["Acme Industrial", "MedTech Polska", "GrantWorks"]

feeds = [
    "https://news.google.com/rss/search?q=przemysl+polska&hl=pl&gl=PL&ceid=PL:pl",
    "https://news.google.com/rss/search?q=medtech+poland&hl=en",
]
```

- **`watchlist`** — exact company names to look for. Matching is a case-insensitive substring test, so keep names specific enough to avoid false positives.
- **`feeds`** — any RSS/Atom URL. Google News RSS is the easiest general-purpose source; trade press, regulator feeds and company blogs usually expose RSS too.

To build a Google News feed for a phrase, use:

```text
https://news.google.com/rss/search?q=YOUR+QUERY&hl=en
```

Add `&hl=pl&gl=PL&ceid=PL:pl` for Polish-language results.

## Output

Console only, for example:

```text
Checking feed: https://news.google.com/rss/search?q=medtech+poland&hl=en
  MATCH [MedTech Polska]: MedTech Polska opens new plant
    https://example.com/article
```

## Limitations

- Only the first 20 entries of each feed are checked per run.
- Matching is plain substring matching: no stemming, no fuzzy matching, no entity resolution.
- Google News RSS is rate-limited and can return different results by region.
- Nothing is persisted — for history, write matches to a CSV or Google Sheet.
- The script is designed for Colab; converting it to a `.py` file requires replacing the `!pip install` line with a normal `pip` call and removing the Colab-specific bits.
