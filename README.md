# Most brutal Weightclass in UFC

## Ask:

* Which weightclass has most KO ?
* Which fighters has most KOs in UFC history ?
* Which fighters has highest striking accuracy ?
* What is most common result for KO in UFC history ?


---
## Prepare

### Source
https://www.kaggle.com/datasets/fatismajli/ufc-data
#### Dataset scrapped from:
http://www.ufcstats.com/statistics/events/completed


#### Tables Explanation
> Ufc_events\
> event_id - Primary key for ufc_events, unique for each event\
> event_name - Name of the event, e.g. UFC 267\
> event_date - Date of the event (YYYY-MM-DD)\
> event_city - City the event was hosted\
> event_state - State the event was hosted (if applicable)\
> event_country - Country the event was hosted\
> event_url - URL used to scrape event data from ufcstats.com

> Ufc_fights\
> fight_id - Primary key for ufc_fights, unique for each fight\
> event_id - Secondary key from ufc_events\
> referee - Referee of the fight\
> f_1 - Fighter 1\
> f_2 - Fighter 2\
> winner - Winner of the fight\
> num_rounds - Number of rounds\
> title_fight - Boolean for whether fight is a title fight or not\
> weight_class - Weight class of the fight\
> gender - Male or female fight\
> result - How did the fight end, e.g. decision, KO\
> result_details - Specific details of how the fight ended, e.g. KO by elbows, split decision\
> finish_round - What round did the fight finish\
> finish_time - What minute and second did the fight finish in that round (m:ss)\
> fight_url - URL used to scrape fight data from ufcstats.com

> Ufc_fight_stats
> fight_stat_id - Primary key for ufc_fight_stats, unique for each fighter of each fight\
> fight_id - Foreign key from ufc_fights\
> fighter_id - Foreign key from ufc_fighters\
> Knockdowns - No. of knockdowns landed \
> total_strikes_att - No. of strikes attempted\
> total_strikes_succ - No. of successful strikes\
> sig_strikes_att - No. of significant strikes attempted\
> sig_strikes_succ - No. of significant strikes successful\
> takedown_att - No. of takedown attempts\
> takedown_succ - No. of successful takedowns\
> submission_att - No. of submission attempts\
> reversals - No. of reversals\
> ctrl_time - Control time \
> fighter_age - Age of the fighter\
> winner - Boolean for whether fighter won or lost

> Ufc_fighters
> fighter_id - Primary key for ufc_fighters, unique for each fighter\
> fighter_f_name - Fighter first name\
> fighter_l_name - Fighter last name\
> fighter_nickname - Fighter nickname\
> fighter_height_cm - Fighter height in cm\
> fighter_weight_lbs - Fighter weight in lbs \
> fighter_reach_cm - Fighter reach in cm\
> fighter_stance - Fighter stance - e.g. southpaw, orthodox\
> fighter_dob - Fighter date of birth\
> fighter_w - No. of wins (at the time of scraping)\
> fighter_l - No. of losses (at the time of scraping)\
> fighter_d - No. of draws (at the time of scraping)\
> fighter_nc_dq - No. of no contests or disqualifications (at the time of scraping)\
> fighter_url - URL used to scrape fighter data from ufcstats.com}

#####Ufc_events - Useless for this analysis.

---
## Process 

### Data cleaning

##### Ufc_fighters
* Save it as ufc_fighters_edited
Created new Sheet for edition and copied data
Freezed top rows
Add filters to check any missing values, or wrong data - Not found
Check for any duplicates
* 19 removed no single fight()
* Create table (Total_ufc_fights) =COUNTIF($B$2:$B$14051,B2)
Double check formats of columns
Saved

##### Ufc_fight_stats
* Save it as ufc_fight_stats_edited
Created new Sheet for edition and copied data
Freezed top rows
Check for any duplicates
Add filters to check any missing values, or wrong data - Not found
Fighter_fight_id – (fighter_id missing 98 rows without Fighter_id and Winner/FigherAge) 196 NULLS+ (14149 Rows) Deleted Fighter_URL, Formated cells to numbers
Removed 19 Fighters (No single fight happened yet) e.g - https://www.ufc.com/athlete/craig-jones 
Double check formats of columns
Saved

##### Ufc_fights
* Save it as ufc_events_edited
Created new Sheet for edition and copied data
Freezed top rows
Check for any duplicates
Add filters to check any missing values, or wrong data - Not found
Fight url column - removed
F_1 and F_2 has blank values but we still might get some valueable informations so we leave them
No winner for 50 fights( Even if fight wanst draw or n/c) leave it as theres still some valuable data
Saved

Merged all tables into 1 using PowerQuery.
