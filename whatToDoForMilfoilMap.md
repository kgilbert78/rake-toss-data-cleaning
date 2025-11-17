# Steps to generate csv with the new year's rake toss data added

__Note: The only python files necessary are `tableB.ipynb` and `combining_tables.ipynb`__

_Preliminary work: activate virtual environment (ve-dataprep) and make sure VS Code finds & is using it for Jupyter. Run the previous years' code._

1. Download spreadsheet of new rake toss data and save it to `input/rakeToss20XX-AB.xlsx` where 20XX is the actual year it's for, and AB (or just B) represents which sheets/tables are present in it.

2. In `tableB.ipynb` find locations of last year's data by searching on "df20XX" whatever last year was.

3. The first one will be something like the code below, to read from the file. Add lines to read from the file, replacing XX with year and checking actual sheet_name. skiprows is for the top line "Table B. Conversion of ..." so make sure that exists in the sheet.

```Python
df20XX = pd.read_excel("input/rakeToss20XX-AB.xlsx", sheet_name="TableB_AbundanceSpecies", skiprows=[0])

for col in df20XX.columns:
    df20XX.rename(columns={col:col.strip().replace(" ","_")},inplace=True)

df20XX.head()
```

4. The next ones will be renaming columns so they match up across years. Duplicate those and reimpliment them for the current year. Open this year's file in excel and do a manual check for any other typos in the column names in this year's data and handle it in a similar manner.
5. The next ones will be `df20XX.to_csv('output/table_B_20XX.csv')` to generate the csv of abundance data for all plants of that year
6. Then search for `milfoil20XX` to filter into csv's for only milfoil data, then the line to generate the csv
7. Then in the last line, where it assigns `df_list = `... 
   1. add this year's df to the python list
   2. change the output file name to include this year's date
8. Run All
9. In `combining_tables.ipynb`, add this year to the list of years in the top line
10. Search for "create table b dataframes" and add this year to that list too
11. search for `table_b_df = pd.concat` and add year there
12. Search for `final_abundance_df.to_csv` and change year in file name
13. Run all & look for `output/Final_Abundance_2008_20xx.xlsx` in the file system, make sure it's correct by opening in excel
14. Find or `output/milfoil/table_B_20xx.csv` in the file system, open it and make sure it looks good. Keep it open for the next step.

## Then open the milfoil-viz repo

The code I want to run here is in `animated_milfoil.ipynb`

Open the file `milfoil_tableB_all_years_to_2024_cleaned.csv` or similar (most up to date), resave with new year in name, and add the rake toss data from the file in the other repo to columns:

1. copy column A & B contents (id & sample point) to the bottom of column A & B of the csv
2. copy column C to column E
3. fill in columns C & D with the latitude and longitude entried from a previous year's corresponding sample points 
4. fill in column F with this year all the way down
5. update file name in first section in `animated_milfoil.ipynb`, run all and play map to check!
