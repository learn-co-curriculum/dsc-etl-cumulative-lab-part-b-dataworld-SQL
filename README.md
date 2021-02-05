# dsc-etl-cumulative-lab-part-b-dataworld-SQL

# TODOs
- Solution query is in #__Solution__ cell at bottom; move to appropriate place in the repo
- Copy over `Business Understanding` and `Data Understanding` from Part D (Tableau) where the project and data is laid out
- Alter / write additional `Business Understanding` and `Data Understanding` as needed

## Introduction
You've completed the setup portion for `data.world` in Part A of the ETL lab. Now the fun begins! We're going to write a SQL query to pull a specific set of data from two tables and join them.  

You'll get practice using SQL to pull specific data from a larger database, manipulating that data, and joining it to additional data from another table.

The steps of this lab will prepare you for doing the project at the end of the Phase, so you are *highly* encouraged to complete it!

## Objectives
You will be able to write an sql query in `data.world` to extract data from several hosted datasets

Figuring out what variables to use in the query will incorporate the following skills:
- reading documentation of a government-provided dataset


The itself query will incorporate the following skills:
- aliasing
- sub-querying
- transforming variables with arithmetic
- joining

## Your Task:

### Business Understanding

### Data Understanding

### Requirements

#### 1. `American Community Survey` documentation research

Look within the `Health Insurance` and `Poverty` documentation of the American Community Survey for 2011-2015, which you set up in your project at `data.world` in Part A of this lab.  Find specific variables counting people who have health insurance and people below the poverty line for each Zip Code Tabulation Area, or `zcta`.


#### 2. Writing a SQL query

Craft an SQL query using the variables you found above, which will add some of the variables together in specific ways to create data for each `zcta`. 

## 1. `American Community Survey` documentation research
>Look within the `Health Insurance` and `Poverty` documentation of the American Community Survey for 2011-2015, which you set up in your project at `data.world` in Part A of this lab.  Find specific variables counting people who have health insurance and people below the poverty line for each Zip Code Tabulation Area, or `zcta`.

## 2. Write an SQL query

>Craft an SQL query using the variables you found above, which will add some of the variables together in specific ways to create data for each `zcta`. 

## Final Checks

## Summary


```python
#__SOLUTION__

#Final Query in `data.world`


with ins as(
    SELECT  zcta,  
        B27001_001 as health_ins_total,
        B27001_002 as health_ins_total_male,
        B27001_004 + B27001_007 + B27001_010 + B27001_013 + 
            B27001_016 + B27001_019 + B27001_022 + B27001_025 + 
            B27001_028 as male_ins,
        B27001_005 + B27001_008 + B27001_011 + B27001_014 + 
            B27001_017 + B27001_020 + B27001_023 + B27001_026 + 
            B27001_029
            as male_unins,
        B27001_030 as health_ins_total_female,
        B27001_032 + B27001_035 + B27001_038 + B27001_041 + 
            B27001_044 + B27001_047 + B27001_050 + B27001_053 + 
            B27001_056 as female_ins,
        B27001_033 + B27001_036 + B27001_039 + B27001_042 + 
            B27001_045 + B27001_048 + B27001_051 + B27001_054 + 
            B27001_057 as female_unins
    FROM `uscensusbureau`.`acs-2015-5-e-healthinsurance`.`USA_ZCTA`
)
select  ins.zcta,
        ins.male_ins+ins.female_ins+ins.male_unins+ins.female_unins as total_pop,
        ins.male_ins+ins.female_ins as total_ins,
        ins.male_unins+ins.female_unins as total_unins,
        poverty.B17001_003 as native_poverty,
        poverty.B17025_010 as native_non_poverty,
        poverty.B17001_006 as foreign_born_poverty,
        poverty.B17025_013 as foreign_born_non_poverty

FROM ins 

INNER JOIN `uscensusbureau`.`acs-2015-5-e-poverty`.`USA_ZCTA` as poverty
    on poverty.zcta = ins.zcta
```
