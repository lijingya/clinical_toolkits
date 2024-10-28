# Info
Good read: https://rconsortium.github.io/rtrs-wg/commontables.html#demographic-tables

# rtable[https://github.com/insightsengineering/rtables?tab=readme-ov-file] 
Developed by Roche.

# tern[https://github.com/insightsengineering/tern?tab=readme-ov-file]
The tern R package contains analysis functions to create tables and graphs used for clinical trial reporting

e.g.
```
library(tern)
table_df <-
  meta %>%
  as.data.frame() %>%
  select(subject_id, pnk_set, site:super_label, diagnosis ) %>%
  mutate_if(sapply(., is.character), as.factor)
table_df <- df_explicit_na(table_df, na_level = "Missing Values")

vars <- c("site", "age", "BMI", "race", "ethnicity", "is_taking_medications",
          "has_taken_vaginal_medications", "is_taking_vaginal_medications", "has_pessary",
          "has_diabetes", "has_hyperlipidemia", "has_hypertension", "is_post_menopausal", "age_of_menarche", "num_pregnancies",
          "num_births","had_pap_smear","pap_smear_result","had_hpv_test","hpv_result","had_previous_endometrial_biopsy","has_aub","aub_duration_months","aub_amt","final_diagnosis","cancer_type","cancer_subtype_1","cancer_subtype_2","figo_grade","super_label","diagnosis"
          )

lyt <- basic_table(title = "x.x: Study Subject Data",
                   subtitles= c("x.x.x: Demographic Characteristics",
                                "Table x.x.x.x: Demographic Characteristics - Full Analysis Set"),
                   prov_footer = "Source: ADSL DDMMYYYY hh:mm; Listing x.xx; SDTM package: DDMMYYYY") |>
  split_cols_by("pnk_set") |>
  add_overall_col("All Patients") |>
  analyze_vars(vars, var_labels = vars)


tbl <- build_table(lyt, table_df)
export_as_docx(tbl, file.path(outputDir, "tableone_pnk_set.docx"))
```