# Rake Toss Data Cleaning

My work cleaning data from a series of Excel files to create uniform CSVs that I can work with across the files.

The data is from an aquatic plant survey conducted on Cazenovia Lake annually.

My intention is to use it for data visualization projects and eventually integrate it into a database with data from all the studies conducted on Cazenovia Lake in recent years.

## ERD draft, if I was making a database for the rake toss only

[Mermaid Diagram](https://mermaid.js.org/)

```mermaid
erDiagram
LOCATION ||--O{ SAMPLE: has
SAMPLE ||--|{ SAMPLE_PLANT: has
PLANT ||--|{ SAMPLE_PLANT: has

	LOCATION {
		int id PK
		int point_num
		float latitude
		float longitude
	}

	SAMPLE {
		int id PK
		int loc_id FK
		int year
		int toss_num
		float depth
		char rake_abundance
		%% optional date field if we know the specific day
	}

	SAMPLE_PLANT {
		int id PK
		int sample_id FK
		int plant_id FK
		char rake_abundance
		float percent
	}

	PLANT {
		int id
		varchar scientific_name
		boolean is_native
		boolean is_invasive
		varchar common_name
		varchar img_url
		text description
	}
```
