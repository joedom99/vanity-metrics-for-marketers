# Vanity Metrics: You Can't Deposit Likes at the Bank

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/joedom99/vanity-metrics-for-marketers/blob/main/vanity_metrics_for_marketers.ipynb)
[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Made with Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![NumPy](https://img.shields.io/badge/NumPy-arrays-013243?logo=numpy&logoColor=white)](https://numpy.org/)
[![pandas](https://img.shields.io/badge/pandas-data-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-figures-11557C?logo=python&logoColor=white)](https://matplotlib.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/joedom99/vanity-metrics-for-marketers/blob/main/LICENSE)
[![Blog](https://img.shields.io/badge/Blog-Marketing%20Data%20Science-teal)](https://blog.marketingdatascience.ai)

Companion notebook for the article **"Vanity Metrics: You Can't Deposit Likes at the Bank"** on the [Marketing Data Science blog](https://blog.marketingdatascience.ai) by Joe Domaleski.

## What This Is

A vanity metric is a number that reliably goes up and never changes a decision. Everybody agrees they are a problem, and almost every article about them stops at the scolding. This notebook does something more useful: it builds a year of data where a vanity metric and a real metric point in opposite directions, and then shows you how to tell them apart on your own dashboard.

The running example is a small service business over 52 weeks:

- Social followers grow from **2,446 to 4,661**, a **91% gain** with no down weeks
- Over the same year, weekly revenue falls from about **$25K to $12K** and then recovers
- The collapse lasts **14 weeks** and is caused by a broken form and drifting targeting
- The follower chart never registers it. Not a dip, not a flat spot

Correlation with revenue across those 52 weeks: followers **-0.10**, qualified lead rate **+0.88**. Same business, same year, same dashboard. One number would have caught the problem in week 18 and the other one never would have.

All data in this repository is **simulated**. No client data is used anywhere.

## What's Inside

The notebook walks through:

1. **Building the data.** Three layers: a vanity layer where followers only go up, a traffic layer driven mostly by paid spend, and a decision layer where the qualified lead rate can actually fall. The non-monotone dip is the whole experiment.
2. **The setup.** Two charts of the same 52 weeks, one of which noticed that the business lost a quarter of its revenue.
3. **What actually tracked revenue.** Side-by-side scatter plots with correlation coefficients, then the full correlation matrix.
4. **The block structure.** Vanity metrics are not random noise. They correlate with **each other** at +0.54, which is exactly why a dashboard full of them feels like a real measurement system. They just form a system disconnected from revenue.
5. **The three-question test.** An editable cell that screens your own metrics in about ten seconds, no year of history required.
6. **What the model cannot tell you.** Fifty-two observations, no causal identification, and an honest note that followers are not worth zero, they are worth whatever your follower-to-lead rate says they are worth.

All three article figures are saved at 200 DPI when the notebook runs.

## Quick Start

**Option 1: Google Colab (easiest).** Click the "Open in Colab" badge at the top. Everything runs top to bottom with no installs.

**Option 2: Run locally.**

```
git clone https://github.com/joedom99/vanity-metrics-for-marketers.git
cd vanity-metrics-for-marketers
pip install numpy pandas matplotlib jupyter
jupyter notebook vanity_metrics_for_marketers.ipynb
```

Requires Python 3.9+ with NumPy, pandas, and Matplotlib. No other dependencies.

## The Three-Question Test

Part 5 contains the only block you need to edit. Ask three questions about any metric on your dashboard:

1. If this number **doubled** tomorrow, what would I do differently?
2. If it **halved** tomorrow, what would I do differently?
3. Does it move **before or after** money changes hands?

If questions 1 and 2 have the same answer, it is not a metric. It is a mood.

```
my_metrics = [
    # name,                     action_if_doubled,   action_if_halved,          timing
    ("Instagram followers",     "post more",         "post more",               "after"),
    ("Qualified lead rate",     "raise budget",      "audit form + targeting",  "before"),
]
```

Be honest on the first two fields. That is the entire difficulty of this exercise.

## Key Results

| Quantity | Value |
| --- | --- |
| Weeks of simulated data | 52 |
| Follower growth over the year | 2,446 to 4,661 (+91%) |
| Down weeks in the follower count | 0 |
| Revenue, first 8 weeks | ~$25.0K / week |
| Revenue, weeks 20 to 28 | ~$12.6K / week |
| Revenue, last 8 weeks | ~$23.0K / week |
| Length of the revenue collapse | 14 weeks |
| corr(followers, revenue) | **-0.10** |
| corr(impressions, revenue) | **-0.13** |
| corr(sessions, revenue) | **+0.45** |
| corr(qualified lead rate, revenue) | **+0.88** |
| corr(qualified leads, revenue) | **+0.95** |
| corr(followers, impressions) | **+0.54** |
| Qualified lead rate range | 1.3% to 5.2% |

Seeded with `default_rng(42)`. These numbers reproduce exactly.

## Vanity to Decision-Grade Translation

A metric without a threshold is still decoration. The third column is the part most versions of this table leave out.

| Vanity metric | Decision-grade version | Threshold it triggers |
| --- | --- | --- |
| Followers | Follower-to-lead rate | Rate drops 2 weeks running |
| Impressions | Cost per qualified lead | CPQL exceeds gross margin per deal |
| Sessions | Session-to-inquiry rate | Rate below trailing 12-week floor |
| Email list size | Active subscriber rate (90-day) | Active share falls under 30% |
| Total leads | Qualified leads | Qualification rate drops |
| Engagement rate | Reply or booking rate | Zero bookings in a full cycle |

## Related Articles

This notebook supports a series of articles on marketing data science:

- [Marketing Data Science blog](https://blog.marketingdatascience.ai) - the full article archive
- [Essential Marketing Analytics for Small Businesses](https://blog.marketingdatascience.ai/essential-marketing-analytics-for-small-businesses-a-guide-to-what-really-matters-68ed6f5e26a6) - what to track when you are starting from nothing
- [Optimizing Small Business Marketing with Dashboards](https://blog.marketingdatascience.ai/optimizing-small-business-marketing-with-dashboards-a-deep-dive-into-what-we-track-and-why-56ceca040306) - what we actually put on a client dashboard and why
- [When the Numbers Look Wrong: A Marketer's Guide to Anomaly Detection](https://blog.marketingdatascience.ai/when-the-numbers-look-wrong-a-marketers-guide-to-anomaly-detection-3895e22f2fe7) - how the week 18 collapse would have been caught automatically
- [Regression to the Mean: The Statistical Force That Humbles Marketers](https://blog.marketingdatascience.ai/regression-to-the-mean-the-statistical-force-that-humbles-marketers-61382f3e1ceb) - why a metric that falls and recovers invites false credit for the fix
- [Measuring Lift: A Marketer's Guide to Incrementality](https://blog.marketingdatascience.ai/measuring-lift-a-marketers-guide-to-incrementality-ab4f57b21cc6) - the causal answer this notebook deliberately does not attempt
- [When Sales Go Up, How Do You Know Marketing Helped?](https://blog.marketingdatascience.ai/when-sales-go-up-how-do-you-know-marketing-helped-4c7846eb3f56) - the same question from the other direction
- [When Less Means More: The Case for Simplicity in Marketing](https://blog.marketingdatascience.ai/when-less-means-more-the-case-for-simplicity-in-marketing-fb39eafbaad1) - why a shorter dashboard usually beats a longer one

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/joedom99/vanity-metrics-for-marketers/blob/main/LICENSE) file for details.

## Author

**Joe Domaleski** - [Marketing Data Science](https://blog.marketingdatascience.ai) | [Medium](https://medium.com/@marketingdatascience) | [GitHub](https://github.com/joedom99)
