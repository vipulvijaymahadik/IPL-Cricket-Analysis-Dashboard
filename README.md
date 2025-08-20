# IPL-Cricket-Analysis-Dashboard
Problem Statement:

The Indian Premier League (IPL) generates massive volumes of data each season, including player statistics, team performances, and match results. However, raw data tables make it difficult to quickly derive insights, compare performances, or spot trends over time.

The problem is: “How can we transform IPL data into a visually interactive dashboard that provides meaningful insights for fans, analysts, and decision-makers?”

This dashboard solves the problem by:
Aggregating IPL data into a structured and interactive Power BI dashboard.
Allowing quick comparison between players, teams, and seasons.
Providing decision-making insights such as best performers, winning factors, and performance trends.

# Dataset:
1.**Ball-by-Ball Dataset (ipl_ball_by_ball_2008_2022.csv)**

2.**Matches Dataset (ipl_matches_2008_2022.csv)**

# steps:

**1.Load data into PowerBI:**
Open Power BI - Get Data - Link Folder which contains csv files

**2.Data Transformation:**
Calendar Table (Date Dimension for Time Intelligence):
-Dax formula: Calender Table = CALENDAR(MIN('public ipl_matches_2008_2022'[match_date]),MAX('public ipl_matches_2008_2022'[match_date]))

**3.Manage Relationship:**
created a schema relationship between tables.
<img width="1010" height="753" alt="image" src="https://github.com/user-attachments/assets/3bd1b83b-7d05-4b94-93af-d7289c92ef22" />

**4.Create measures:**
1. **Average by bowler** = DIVIDE(
                SUMX(
                    FILTER('public ipl_ball_by_ball_2008_2022','public ipl_ball_by_ball_2008_2022'[extra_type]<>"legbyes" && 'public ipl_ball_by_ball_2008_2022'[extra_type]<>"byes") , 'public ipl_ball_by_ball_2008_2022'[total_run]),SUM('public ipl_ball_by_ball_2008_2022'[iswicket_delivery]))

2. **Batter Runs** = CONCATENATE(SUM('public ipl_ball_by_ball_2008_2022'[batsman_run]),"Runs")

3. **Bowling SR** = COUNT('public ipl_ball_by_ball_2008_2022'[bowler])/SUM('public ipl_ball_by_ball_2008_2022'[iswicket_delivery])

4. **Economy** = DIVIDE(
                SUMX(
                    FILTER('public ipl_ball_by_ball_2008_2022','public ipl_ball_by_ball_2008_2022'[extra_type]<>"legbyes" && 'public ipl_ball_by_ball_2008_2022'[extra_type]<>"byes") , 'public ipl_ball_by_ball_2008_2022'[total_run]),(COUNT('public ipl_ball_by_ball_2008_2022'[overs]))/6)
   
5.**Strike Rate for Batsman** = (SUM('public ipl_ball_by_ball_2008_2022'[batsman_run])/COUNT('public ipl_ball_by_ball_2008_2022'[ball_number]))*100

6.**Matches win on toss decision** = CALCULATE(COUNTROWS('public ipl_matches_2008_2022'), 'public ipl_matches_2008_2022'[toss_winner] = 'public ipl_matches_2008_2022'[winning_team])

7.**Title Winner** = VAR max_date = CALCULATE(MAX('Calender Table'[Date]), ALLSELECTED('public ipl_ball_by_ball_2008_2022'), VALUES('public ipl_matches_2008_2022'))
var Title_winner = CALCULATE(SELECTEDVALUE('public ipl_matches_2008_2022'[winning_team]), 'Calender Table'[Date] = max_date)
return Title_winner

**5.Create Dashboard**
<img width="2767" height="1600" alt="IPL_DASHBOARD-1" src="https://github.com/user-attachments/assets/0b62566b-e5c4-4794-8da9-23d56f6228fa" />

