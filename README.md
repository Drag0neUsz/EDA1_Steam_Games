# EDA1 — Steam Games Exploratory Data Analysis

## Short Introduction
A concise exploratory data analysis project in Python focused on the Steam games catalog (~122k entries). The notebook (`EDA0.ipynb`) explores platform coverage, pricing, review signals, release trends, and engagement-related features.

## Setup
1. Clone the repository.
2. (Recommended) Create and activate a virtual environment.
3. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
4. Download `games.csv` from Kaggle and place it in the repository root.
5. Run the notebook:
   ```bash
   jupyter notebook EDA0.ipynb
   ```

## Dataset Info
- **Source:** Kaggle — Steam Games Dataset (fronkongames)
- **File used:** `games.csv` (not committed)
- **Size:** ~122,611 rows
- **Core fields analyzed:** `Name`, `Release date`, `Estimated owners`, `Price`, `Windows`, `Mac`, `Linux`, `Metacritic score`, `Achievements`, `Average playtime forever`
- **Data note:** score value `0` is treated as “not rated” in score-based analyses.

## Analyses with Conclusions
1. **Platform support (Windows/Mac/Linux)**  
   Windows support dominates the catalog by a large margin; Mac and Linux support are much smaller and often co-occur.

2. **Price vs. Metacritic score**  
   No strong relationship was found between higher price and better critic scores. Many highly rated titles are in lower price ranges.

3. **Release volume and average scores over time**  
   The number of releases grows strongly in later years (especially after ~2014). Average scores among rated games show an upward tendency.

4. **Estimated owners vs. average playtime**  
   Ownership and playtime do not show a clear, strong linear relationship overall; high-owner games can have very different engagement patterns.

5. **Achievements vs. playtime**  
   More achievements do not guarantee higher engagement, though longer-played games naturally tend to accumulate more achievements.
