# Bad-plots
Some plots are just born bad. Use your dataviz skills to make a deliberately ugly and misleading data visual.

Each dataset has a short script provide so that you can skip the data cleanin' - and get straight into misleadin'

Remember a GOOD plot would include an accurate title, clear, accessible and attractive visuals with annotations that improve the message. They would also source the dataset. 

Now do your worst...

## Covid cases by age

```
library(tidyverse)
library(here)
library(janitor)
library(stringr)

covid <- read_csv(here("data", "covid cases by age.csv"))

covid <- covid %>% 
janitor::clean_names() %>% 
pivot_longer(!date, 
names_to="ages", 
values_to="percentage_cases") %>% 
mutate(date=lubridate::dmy(date), 
percentage_cases=str_remove(percentage_cases, "%"), 
percentage_cases=as.numeric(percentage_cases),
ages = factor(ages, levels=c("age_2_to_school_year_6", 
"school_year_7_to_school_year_11",
"school_year_12_to_age_24",       
"age_25_to_age_34",
"age_35_to_age_49",
"age_50_to_age_69",              
"age_70")))

```

A live roundup of the latest data and trends about the coronavirus (COVID-19) pandemic from the ONS and other sources. This data was taken from September to October 2020

## Plants under threat

The data  `iucn threats.csv` comes from the International Union for Conservation of Nature (IUCN) Red list of Threatened Species (Version 2020-1) (https://www.iucn.org/)

### Tidying script

```
library(tidyverse)
library(here)

iucn <- read_csv(here("data", "iucn threats.csv"))


iucn <- iucn %>% 
drop_na() %>% 
mutate(year_last_seen=factor(year_last_seen, 
levels=c("Before 1900", 
"1900-1919", 
"1920-1939", 
"1940-1959", 
"1960-1979", 
"1980-1999", 
"2000-2020")))

```

### Data Dictionary


|variable         |class     |description                             |
|:----------------|:---------|:---------------------------------------|
|binomial_name    |character | Species name (Genus + species)         |
|country          |character | Country of origin                      |
|continent        |character | Continent of origin                    |
|group            |character | Taxonomic group                        |
|year_last_seen   |character | Period species was last seen           |
|red_list_category|character | IUCN Red List category                 |
|threat_type       |character | Type of threat |
|threatened        |double    | Binary 0 or 1 (not threatened by this), and 1 (threatened) |


## Malarial deaths

`malaria_deaths.csv`

Simple aggregated malaria data from Our World in Data (https://ourworldindata.org/malaria), you can see many different summary-level datasets related to malaria incidence by region, age, or time.


```

library(tidyverse)
library(here)

malaria <- read_csv(here("data", "malaria_deaths.csv"))

malaria <- malaria %>%  
rename("Row"=X1) %>% 
mutate(age_group = factor(age_group,
levels = c("Under 5",
            "5-14",
            "15-49",
            "50-69",
            "70 or older"))

```