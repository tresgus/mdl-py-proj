# Profitable App Profiles for the App Store and Google Play

A guided Python project from [Dataquest](https://www.dataquest.io/) that analyzes two app store datasets to find a type of app that is likely to attract many users on **both** the Apple App Store and Google Play.

## Project Goal

The scenario: we work as data analysts for a company that builds **free**, **English-language** mobile apps for Android and iOS. Revenue comes from in-app ads, so the more users an app has, the more it earns. The goal is to give developers a data-backed recommendation for which kind of app to build.

The company's launch strategy shapes the analysis:

1. Build a minimal Android version and publish it on Google Play.
2. If users respond well, develop it further.
3. If it is profitable after 6 months, build an iOS version for the App Store.

That means the recommended app profile has to work in both markets.

## Data

| Dataset | Apps | Collected | Source |
|---|---|---|---|
| Google Play (`data/googleplaystore.csv`) | ~10,800 | August 2018 | [Kaggle](https://www.kaggle.com/datasets/lava18/google-play-store-apps) |
| Apple App Store (`data/AppleStore.csv`) | ~7,200 | July 2017 | [Kaggle](https://www.kaggle.com/datasets/ramamet4/app-store-apple-data-set-10k-apps) |

## Approach

The analysis uses plain Python only (the built-in `csv` module, lists, dictionaries and loops), with no pandas.

### 1. Data cleaning

| Step | Google Play | App Store |
|---|---|---|
| Starting rows | 10,841 | 7,197 |
| Remove a malformed row (row 10,472, columns shifted) | 10,840 | n/a |
| Remove duplicates, keeping the entry with the most reviews | 9,659 | 7,197 (no duplicates) |
| Remove non-English apps (names with more than 3 non-ASCII characters) | 9,614 | 6,183 |
| Keep free apps only | **8,863** | **3,222** |

### 2. Most common genres

Frequency tables of the free English apps show two different markets:

- **App Store:** dominated by entertainment. `Games` makes up **58%** of apps, followed by `Entertainment` (7.9%) and `Photo & Video` (5.0%).
- **Google Play:** more balanced. `Family` (18.9%, mostly children's games) and `Game` (9.7%) lead, followed by practical categories such as `Tools`, `Business`, `Lifestyle`, `Productivity` and `Finance`.

### 3. Most popular genres

Having the most apps in a genre doesn't mean that genre has the most users, so popularity was measured separately:

- **App Store:** average number of user ratings per genre (used as a stand-in for installs, which this dataset doesn't include).
- **Google Play:** average number of installs per category.

Key observations:

- Top genres like `Navigation` and `Social Networking` (iOS) or `Communication` and `Video Players` (Android) are skewed by a few giants such as Google Maps, Waze, Facebook, WhatsApp and YouTube. They would be very hard to compete in.
- **Health & Fitness** sits in the middle of the pack on both platforms (about 23,000 average ratings on iOS and about 4.2 million average installs on Android), with many successful mid-size apps rather than one dominant player.

### 4. Digging into Health & Fitness

- Only two Google Play Health & Fitness apps pass 100 million installs: **Samsung Health** (pre-installed on Samsung phones) and **Period Tracker** (a specialized niche).
- The 1 to 50 million install range is crowded with calorie counters, ab and home workouts, step counters and run trackers.
- **Yoga** is noticeably underserved, with only a handful of yoga-related apps.

## Conclusion

The recommended app profile is a **free daily yoga tracker with game-like features**:

- Tracks daily yoga practice and progress.
- Has a **level-up system**: staying consistent unlocks new poses suited to the user's skill level, from beginner-friendly poses to advanced positions and challenges.
- Has optional **social and community features** (in the spirit of Strava) so users can share progress with friends.

This combines an underserved Health & Fitness niche with the broad appeal of gaming, which is the most common genre on both platforms.

## Repository Contents

```
├── PythonAppAnalysisProject.ipynb   # Full analysis notebook
├── data/
│   ├── AppleStore.csv
│   └── googleplaystore.csv
└── images/
    └── AndroidFamilyApps.png
```

## Running the Notebook

1. Clone the repository.
2. Open `PythonAppAnalysisProject.ipynb` in Jupyter (Anaconda, VS Code or JupyterLab).
3. Run all cells. Only the Python standard library is needed.
