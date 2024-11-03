# Problem description

The challenge is centered around developing better methods for prediction of Alzheimer's disease and Alzheimer's disease related dementias (AD/ADRD) as early as possible. Phase 2: **Algorithms and Approaches Social Determinants Track** — is focused on building innovative models for early detection of AD/ADRD using social determinants of health.

Current methods of screening for AD/ADRD are time intensive and difficult to perform. Models that can flag individuals with a high likelihood of cognitive decline early based on social determinants have the potential to catch and treat cognitive decline earlier, and to reduce disparities in care for marginalized groups.

Prizes, with the exception of community code, will be awarded based on a combination of leaderboard score and model report. For details on the timeline and requirements, see the home page. No prizes will be awarded based on leaderboard score alone. All winners will be required to submit their modeling code. DrivenData will rerun the full model training and inference pipeline to confirm all winners' leaderboard scores.

<br>

## Data

The data for this competition comes from a national longitudinal study of adults 50 years and older in Mexico, the Mexican Health and Aging Study (MHAS). The study includes information about demographics, economic circumstances, migration, physical limitations, self-reported health, and lifestyle behaviors.

Overview of the data files provided for this competition:

```bash
├── submission_format.csv
├── test_features.csv
├── train_features.csv
└── train_labels.csv
```
All data files are hosted by the Mexican Health and Aging Study (MHAS), and can be downloaded via the link on the data download page.

<br>

## Feature data

The feature data for this competition includes survey responses from both 2003 and 2012. Some individuals in the dataset responded to the 2003 survey only, some responded to the 2012 survey only, and some responded to both. Missing values are present where the information either was not collected or where the question does not apply.

Data comes from in-person interviews. Individuals for the survey were selected to be a nationally representative sample of Mexicans aged 50 or older.

External data usage: Per the competition rules, external data is not allowed in this competition. However, participants can use pre-trained computer vision models as long as they were (1) available freely and openly in that form at the start of the competition and (2) not trained on any data associated with the ground truth data for this challenge.

Many features are available for both 2003 and 2012. Columns collected in 2003 end with _03, and columns collected in 2012 end with _12. Columns that are year-agnostic do not contain either year.

`train_features.csv` and `test_features.csv` include the following columns:

  + `uid` (str): Unique identifier for the individual. Each row is one individual.
  + `age_03` / `age_12` (str): Binned age group
  + `urban_03` / `urban_12` (str): Locality size. Either 0. <100,000 (rural) or 1. 100,000+ (urban)
  + `married_03` / `married_12` (str): Marital status
  + `n_mar_03` / `n_mar_12` (float): Number of marriages
  + `edu_gru_03` / `edu_gru_12` (str): Binned education level
  + `n_living_child_03` / `n_living_child_12` (str): Binned number of living children
  + `migration_03` / `migration_12` (float, 0 or 1): Has lived or worked in the U.S.
  + `glob_hlth_03` / `glob_hlth_12` (str): Self-reported global health
  + `adl_dress_03` / `adl_dress_12` (float, 0 or 1): Has difficulty getting dressed
  + `adl_walk_03` / `adl_walk_12` (float, 0 or 1): Has difficulty walking from one side of the room to the other
  + `adl_bath_03` / `adl_bath_12` (float, 0 or 1): Has difficulty bathing themselves in a tub or shower
  + `adl_eat_03` / `adl_eat_12` (float, 0 or 1): Has difficulty eating
  + `adl_bed_03` / `adl_bed_12` (float, 0 or 1): Has difficulty getting in and out of bed
  + `adl_toilet_03` / `adl_toilet_12` (float, 0 or 1): Has difficulty using the toilet
  + `n_adl_03` / `n_adl_12` (float): Number of activities of daily living (ADL) limitations (0-5)
  + `iadl_money_03` / `iadl_money_12` (float, 0 or 1): Has difficulty managing money
  + `iadl_meds_03` / `iadl_meds_12` (float, 0 or 1): Has difficulty taking medications
  + `iadl_shop_03` / `iadl_shop_12` (float, 0 or 1): Has difficulty shopping for groceries
  + `iadl_meals_03` / `iadl_meals_12` (float, 0 or 1): Has difficulty preparing a hot meal
  + `n_iadl_03` / `n_iadl_12` (float): Number of instrumental activities of daily living (IADL) limitations (0-4)
  + `depressed_03` / `depressed_12` (float, 0 or 1): Most of the past week, felt depressed
  + `hard_03` / `hard_12` (float, 0 or 1): Most of the past week, felt that everything was an effort
  + `restless_03` / `restless_12` (float, 0 or 1): Most of the past week, felt that their sleep was restless
  + `happy_03` / `happy_12` (float, 0 or 1): Most of the past week, felt happy
  + `lonely_03` / `lonely_12` (float, 0 or 1): Most of the past week, felt lonely
  + `enjoy_03` / `enjoy_12` (float, 0 or 1): Most of the past week, felt that they enjoyed life
  + `sad_03` / `sad_12` (float, 0 or 1): Most of the past week, felt sad
  + `tired_03` / `tired_12` (float, 0 or 1): Most of the past week, felt tired
  + `energetic_03` / `energetic_12` (float, 0 or 1): Most of the past week, felt they had a lot of energy
  + `n_depr_03` / `n_depr_12` (float): Number of CES-D depressive symptoms (0-9)
  + `cesd_depressed_03` / `cesd_depressed_12` (float, 0 or 1): Has 5+ CES-D depressive symptoms
  + `hypertension_03` / `hypertension_12` (float, 0 or 1): Has been diagnosed with hypertension
  + `diabetes_03` / `diabetes_12` (float, 0 or 1): Has been diagnosed with diabetes
  + `resp_ill_03` / `resp_ill_12` (float, 0 or 1): Has been diagnosed with respiratory illness
  + `arthritis_03` / `arthritis_12` (float, 0 or 1): Has been diagnosed with arthritis/rheumatism
  + `hrt_attack_03` / `hrt_attack_12` (float, 0 or 1): Has been told they had a heart attack
  + `stroke_03` / `stroke_12` (float, 0 or 1): Has been told they had a stroke
  + `cancer_03` / `cancer_12` (float, 0 or 1): Has been diagnosed with cancer
  + `n_illnesses_03` / `n_illnesses_12` (float): Number of illnesses (0-7)
  + `bmi_03` / `bmi_12` (str): Binned body mass index
  + `exer_3xwk_03` / `exer_3xwk_12` (float, 0 or 1): Exercises 3+ times per week
  + `alcohol_03` / `alcohol_12` (float, 0 or 1): Currently drinks alcohol
  + `tobacco_03` / `tobacco_12` (float, 0 or 1): Currently smokes tobacco
  + `test_chol_03` / `test_chol_12` (float, 0 or 1): Has had a cholesterol blood test
  + `test_tuber_03` / `test_tuber_12` (float, 0 or 1): Has been tested for tuberculosis
  + `test_diab_03` / `test_diab_12` (float, 0 or 1): Has been tested for diabetes
  + `test_pres_03` / `test_pres_12` (float, 0 or 1): Has been tested for high blood pressure
  + `hosp_03` / `hosp_12` (float, 0 or 1): Has been hospitalized at least one night in the last year
  + `visit_med_03` / `visit_med_12` (float, 0 or 1): Has visited a doctor at least once in the last year
  + `out_proc_03` / `out_proc_12` (float, 0 or 1): Has had at least one outpatient procedure in the last year
  + `visit_dental_03` / `visit_dental_12` (float, 0 or 1): Has visited a dentist at least once in the last year
  + `imss_03` / `imss_12` (float, 0 or 1): Has health coverage with IMSS
  + `issste_03` / `issste_12` (float, 0 or 1): Has health coverage with ISSSTE/ISSSTE Estatal
  + `pem_def_mar_03` / `pem_def_mar_12` (float, 0 or 1): Has health coverage with PEMEX, Defensa, or Marina
  + `insur_private_03` / `insur_private_12` (float, 0 or 1): Has health coverage with private health insurance
  + `insur_other_03` / `insur_other_12` (float, 0 or 1): Has health coverage with other health insurance
  + `seg_pop_12` (float, 0 or 1): Has health coverage with Seguro Popular
  + `insured_03` / `insured_12` (float, 0 or 1): Has health insurance
  + `decis_famil_03` / `decis_famil_12` (str): Weight in family decisions
  + `decis_personal_03` / `decis_personal_12` (str): Weight over personal decisions
  + `employment_03` / `employment_12` (str): Employment status
  + `vax_flu_12` (float, 0 or 1): Has been vaccinated against flu
  + `vax_pneu_12` (float, 0 or 1): Has been vaccinated against pneumonia
  + `care_adult_12` (float, 0 or 1): Uses time to look after a sick or disabled adult
  + `care_child_12` (float, 0 or 1): Uses time to look after children under 12
  + `volunteer_12` (float, 0 or 1): Uses time to volunteer for a non-profit
  + `attends_class_12` (float, 0 or 1): Uses time to attend training course, lecture, or class
  + `attends_club_12` (float, 0 or 1): Uses time to attend sports or social club
  + `reads_12` (float, 0 or 1): Uses time to read books, magazines, newspapers
  + `games_12` (float, 0 or 1): Uses time to do crosswords, jigsaw puzzles, number games
  + `table_games_12` (float, 0 or 1): Uses time to play tabletop games. E.g., cards, dominoes, chess
  + `comms_tel_comp_12` (float, 0 or 1): Uses time to talk on the phone or send message/use the web on a computer
  + `act_mant_12` (float, 0 or 1): Uses time to maintain a house, do repairs, garden, etc.
  + `tv_12` (float, 0 or 1): Uses time to watch television
  + `sewing_12` (float, 0 or 1): Uses time to sew, emboider, knit, make crafts
  + `satis_ideal_12` (str): How much they agree with the statement that their life is close to ideal
  + `satis_excel_12` (str): How much they agree with the statement that life is excellent
  + `satis_fine_12` (str): How much they agree with the statement that they are satisfied with their life
  + `cosas_imp_12` (str): How much they agree with the statement that they have achieved the things in life that are important to them
  + `wouldnt_change_12` (str): How much they agree with the statement that they would change almost nothing about their life
  + `memory_12` (str): Self-reported memory
  + `ragender` (str): Gender
  + `rameduc_m` (str): Mother's education level
  + `rafeduc_m` (str): Father's education level
  + `sgender_03` / `sgender_12` (str): Spouse's gender
  + `rjob_hrswk_03` / `rjob_hrswk_12` (float): Hours per week that they worked at their main job
  + `rjlocc_m_03` / `rjlocc_m_12` (str): Category of their longest occuptation
  + `rjob_end_03` / `rjob_end_12` (float): Year that their last job ended
  + `rjobend_reason_03` / `rjobend_reason_12` (str): Reason that their last job ended
  + `rearnings_03` / `rearnings_12` (float): Earnings from employment
  + `searnings_03` / `searnings_12` (float): Spouse's earnings from employment
  + `hincome_03` / `hincome_12` (float): Household income
  + `hinc_business_03` / `hinc_business_12` (float): Household income from business
  + `hinc_rent_03` / `hinc_rent_12` (float): Household income from rent
  + `hinc_assets_03` / `hinc_assets_12` (float): Household income from financial assets
  + `hinc_cap_03` / `hinc_cap_12` (float): Household capital income
  + `rinc_pension_03` / `rinc_pension_12` (float): Income from pensions
  + `sinc_pension_03` / `sinc_pension_12` (float): Spouse's income from pensions
  + `rrelgimp_03` / `rrelgimp_12` (str): Importance of religion
  + `rrfcntx_m_12` (str): How often they see friends and relatives
  + `rsocact_m_12` (str): How often they have social activities
  + `rrelgwk_12` (str): Participates in weekly religious services
  + `a16a_12` (float, 0 or 1): Year when respondent first left for the U.S., if they ever lived in the U.S.
  + `a21_12` (float): Total years lived or worked in the U.S.
  + `a22_12` (str): Main job type during longest stay in the U.S.
  + `a33b_12` (str): U.S. residency status
  + `a34_12` (str): Speaks English
  + `j11_12` (str): Floor material of residence

<br>

## Labels

The target variable in this competition is a composite score reflecting cognitive function across seven different domains. Composite scores are calculated based on in-depth cognitive assessments that were administered in person as part of the MHAS Cognitive Aging Ancillary Study (Mex-Cog). A higher score is better, and the maximum possible score is 384.

The target data includes scores from two survey years: 2016 and 2021. Some individuals are in 2016 only, some are in 2021 only, and some are in both. train_labels.csv indicates for which years an individual has available scores.

`train_labels.csv` includes the following columns. Each row is a unique combination of uid and year.

  + `uid` (str): Unique identifier for the individual
  + `year` (int): Year the individual received the score
  + `composite_score` (int): Composite score across the seven domains listed below

Labelled training data example

The first few rows in `train_labels.csv` are:

| uid  | year | composite_score |
|------|------|----------------|
| aace | 2021 | 175           |
| aanz | 2021 | 206           |
| aape | 2016 | 161           |
| aape | 2021 | 144           |

In 2021, individual aace got a score of 175. Individuals aace and aanz only have scores for 2021, while individual aape has scores for both 2016 and 2021.

The feature data only includes information through 2012, while cognitive scores are based on surveys conducted in 2016 and 2021. Participants will be predicting composite score 4 and 9 years in the future from the perspective of the feature data.

Composite score is the number of points that an individual received across seven domains:

| Domain                | Example task or question        | Possible score |
| --------------------- | ------------------------------- | -------------- |
| Orientation           | Where are we now?               | 9              |
| Immediate memory      | Word repetition tests           | 95             |
| Delayed memory        | Delayed recall of a short story | 106            |
| Attention             | Ability to count backwards      | 65             |
| Language              | Write a sentence                | 14             |
| Constructional praxis | Physically copy a drawn figure  | 12             |
| Executive function    | Simple math question            | 83             |


Cognitive assessment scores are useful to determine an individual's risk of AD/ADRD and their need for treatment, but are time-intensive and complex to perform. Predicting an individual's likely cognitive ability in the future based on various social determinants of health could save time for clinicians and improve availability of cognitive screening.

<br>

## Submission format

The format for submission is a .csv with the same columns as train_labels.csv:

Required format: `.csv` file with the following columns:
- `uid` (str): Unique identifier for the individual
- `year` (int): Year the individual received the score
- `composite_score` (int): Predicted composite score for the individual in the given year

To create a submission, download submission_format.csv and replace the placeholder value of 0 with your predictions. Not every individual has a score for every year. The uid plus year combinations in submission_format.csv indicate which person-years to generate predictions for.

For example, if the first few rows of your predictions are:

| uid  | year | composite_score |
|------|------|----------------|
| abxu | 2016 | 150           |
| aeol | 2016 | 275           |
| aeol | 2021 | 200           |

That means you are predicting individual abxu will get a score of 150 in 2016, and individual aeol will get a score of 275 in 2016 and 200 in 2021.

<br>

## Performance metric

Leaderboard performance is evaluated using root-mean squared error (RMSE). RMSE is the square root of the mean of squared differences between estimated and observed values. This is an error metric, so a lower value is better. RMSE is implemented in scikit-learn, with the squared parameter set to False.

> Note that final prizes will be awarded based on a combination of leaderboard score and model reports. No prize depends on leaderboard score alone. Winners will be required to submit their modeling code to verify their leaderboard score and adherence to the competition rules.
Competition arenas
