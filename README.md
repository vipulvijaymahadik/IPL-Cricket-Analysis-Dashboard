# IPL-Cricket-Analysis-Dashboard
Problem Statement:

The Indian Premier League (IPL) generates massive volumes of data each season, including player statistics, team performances, and match results. However, raw data tables make it difficult to quickly derive insights, compare performances, or spot trends over time.

The problem is: “How can we transform IPL data into a visually interactive dashboard that provides meaningful insights for fans, analysts, and decision-makers?”

This dashboard solves the problem by:
Aggregating IPL data into a structured and interactive Power BI dashboard.
Allowing quick comparison between players, teams, and seasons.
Providing decision-making insights such as best performers, winning factors, and performance trends.

# Dataset:
**Ball-by-Ball Dataset (ipl_ball_by_ball_2008_2022.csv)(Columns)**
1. id
2. innings
3. overs
4. ball_number
5. batter
6. bowler
7. non_striker
8. extra_type
9. batsman_run
10. extras_run
11. total_run
12. non_boundary
13. iswicket_delivery
14. player_out
15. dismisal_kind
16. fielders_involved
17. batting_team

**Matches Dataset (ipl_matches_2008_2022.csv)(Columns)**
1. id
2. city
3. match_date
4. season
5. match_number
6. team1
7. team2
8. venue
9. toss_winner
10. toss_decision
11. superover
12. winning_team
13. won_by
14. margin
15. method
16. player_of_match
17. umpire1
18. umpire2

# steps:

**1.Load data into PowerBI**
Open Power BI - Get Data - Link Folder which contains csv files

**2.Data Transformation**
Calendar Table (Date Dimension for Time Intelligence):
-Dax formula: Calender Table = CALENDAR(MIN('public ipl_matches_2008_2022'[match_date]),MAX('public ipl_matches_2008_2022'[match_date]))
