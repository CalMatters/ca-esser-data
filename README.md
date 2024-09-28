# California ESSER data

California received over $20 billion in federal aid through three rounds of the Elementary and Secondary School Emergency Relief Act (ESSER) from 2020-2024. The state Dept. of Education collects expenditure reports from districts and makes the data available in Excel files. These files provide each district’s amount spent per reporting period and percent spent by category.

The level of detail in these files makes it complicated to quickly see how much each district received and spent in total, as the analysis requires summing across multiple rows and files. Our dataset in `ca_esser.csv` is one CSV aggregating across these files with the total allocated and spent per district for each of the three rounds of aid.

This dataset will be updated when additional ESSER III data becomes available.

This dataset powers the district lookup tool in this story: “Use it or lose it: California schools race to spend the last of their pandemic funds” by Carolyn Jones (published September 30, 2024).

## Data sources

The original files can be found in `/sources`. All were downloaded September 26, 2024. The original source links provide detail on how the funding could be used.

| Funding round | Original spending deadline                                     | Link to original source                   | File name                                     |
| ------------- | -------------------------------------------------------------- | ----------------------------------------- | --------------------------------------------- |
| ESSER I       | September 30, 2022                                             | https://www.cde.ca.gov/fg/cr/caresact.asp | `caresesseri.xlsx`                            |
| ESSER II      | September 30, 2023                                             | https://www.cde.ca.gov/fg/cr/crrsa.asp    | `crrsaesserii.xlsx`                           |
| ESSER III     | September 30, 2024  *Note: Current data is through June 30, 2024* | https://www.cde.ca.gov/fg/cr/arpact.asp   | `arpesseriii3213.xlsx` `arpesseriii3214.xlsx` |

## Methodology

The values in `ca_esser.csv` were calculated with the following methods.

1. Download the most recent quarterly expenditure reports (as seen in the table above).
2. For each local educational agency (LEA), grouped by unique CDS code, sum up the `ExpendedAmount` column across reporting periods.
3. For each LEA, take the most recent `TotalAllocatedAmount` (currently `Summer 2024`).
4. For ESSER III, sum the above for the 3213 and 3214 spreadsheets to get total allocated and spent.


## Data dictionary

These are the columns in `ca_esser.csv`. Each row is a local education agency, either a district or charter school that is not within a district. Values in all expenditure and allocation columns are `NaN` if there was not a value for that funding round.

| Column  | Description                                                                                                                                                                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| cds     | 14-digit County-District-School (CDS) code that is the official, unique identification of a local educational agency within California. See [explanation of codes](https://www.cde.ca.gov/ds/si/ds/). Note: Some values have leading zeros, which are necessary for matching with other datasets. |
| lea     | Name of the local educational agency                                                                                                                                                                                                                          |
| county  | County in which the LEA is located                                                                                                                                                                                                                            |
| i_exp   | Total amount of ESSER I funding the LEA reported expending over all reporting periods                                                                                                                                                                         |
| i_all   | Final ESSER I allocation the LEA is eligible to receive as of the Summer 2024 reporting period                                                                                                                                                                |
| ii_exp  | Total amount of ESSER II funding the LEA reported expending over all reporting periods                                                                                                                                                                        |
| ii_all  | Final ESSER II allocation the LEA is eligible to receive as of the Summer 2024 reporting period                                                                                                                                                               |
| iii_exp | Total amount of ESSER III funding the LEA reported expending over all reporting periods                                                                                                                                                                       |
| iii_all | Final ESSER III allocation the LEA is eligible to receive as of the Summer 2024 reporting period                                                                                                                                                              |
| iii_plan_link | Link to ESSER III expenditure plan if available and confirmed |

## Data Use

If you use this dataset, please mention it was collected and cleaned by CalMatters. If you have any questions about this dataset, feel free to contact erica@calmatters.org.

[CalMatters](https://calmatters.org/) is a nonpartisan, nonprofit journalism venture committed to explaining how California’s state Capitol works and why it matters.
