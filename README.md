# What is the project about?
This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.

# Data Source: Where Our Data Comes From
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).

## Carbon Emission Analysis
### 1. Which products contribute the most to carbon emissions?
**Explain:** Get top 10 products contribute the most to carbon emissions

**SQL:**
`select product_name, sum(carbon_footprint_pcf) as co2_emission
				from product_emissions
				group by product_name
				order by co2_emission desc
				limit 10`

**Result:**
| product_name                                                                                                                       | co2_emission | 
| ---------------------------------------------------------------------------------------------------------------------------------: | -----------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044      | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187      | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608      | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625      | 
| TCDE                                                                                                                               | 198150       | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687       | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000       | 
| Electric Motor                                                                                                                     | 160655       | 
| Audi A6                                                                                                                            | 111282       | 
| Average of all GM vehicles produced and used in the 10 year life-cycle.                                                            | 100621       | 

**Insight:** Wind Turbine is dominated in the list products contribute the most to carbon emissions

### 2. What are the industry groups of these products?
**Explain:** Get top 10 industry groups contribute the most to carbon emissions

**SQL:**
`select industry_groups.industry_group, sum(carbon_footprint_pcf) as co2_emission
from product_emissions
inner join industry_groups		
	on industry_groups.id = product_emissions.industry_group_id
group by industry_groups.industry_group
order by co2_emission desc
limit 10`

**Result:**
| industry_group                                   | co2_emission | 
| -----------------------------------------------: | -----------: | 
| Electrical Equipment and Machinery               | 9801558      | 
| Automobiles & Components                         | 2582264      | 
| Materials                                        | 577595       | 
| Technology Hardware & Equipment                  | 363776       | 
| Capital Goods                                    | 258712       | 
| "Food, Beverage & Tobacco"                       | 111131       | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486        | 
| Chemicals                                        | 62369        | 
| Software & Services                              | 46544        | 
| Media                                            | 23017        | 

**Insight:** "Electrical Equipment and Machinery" and "Automobiles & Components" account for the majority of the contribution to carbon emissions

### 3. What are the industries with the highest contribution to carbon emissions?
**Explain:** Get top 1 industries contribute the most to carbon emissions

**SQL:**
`select industry_groups.industry_group, sum(carbon_footprint_pcf) as co2_emission
from product_emissions
inner join industry_groups		
	on industry_groups.id = product_emissions.industry_group_id
group by industry_groups.industry_group
order by co2_emission desc
limit 1`

**Result:**
| industry_group                     | co2_emission | 
| ---------------------------------: | -----------: | 
| Electrical Equipment and Machinery | 9801558      | 

**Insight:** "Electrical Equipment and Machinery" are the highest contribution to carbon emissions.

### 4. What are the companies with the highest contribution to carbon emissions?
**Explain:** Get top 10 company contribute the most to carbon emissions

**SQL:**
`select companies.company_name, sum(carbon_footprint_pcf) as co2_emission
from product_emissions
inner join companies		
	on companies.id = product_emissions.company_id
group by companies.company_name
order by co2_emission desc
limit 10`

**Result:**
| company_name                            | co2_emission | 
| --------------------------------------: | -----------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 9778464      | 
| Daimler AG                              | 1594300      | 
| Volkswagen AG                           | 655960       | 
| "Mitsubishi Gas Chemical Company, Inc." | 212016       | 
| "Hino Motors, Ltd."                     | 191687       | 
| Arcelor Mittal                          | 167007       | 
| Weg S/A                                 | 160655       | 
| General Motors Company                  | 137007       | 
| "Lexmark International, Inc."           | 132012       | 
| "Daikin Industries, Ltd."               | 105600       | 

**Insight:** "Gamesa Corporación Tecnológica, S.A.",  "Daimler AG" and "Volkswagen AG" are top 3 company contribute the most to carbon emissions

### 5. What are the countries with the highest contribution to carbon emissions?
**Explain:** Get top 10 countries contribute the most to carbon emissions

**SQL:**
`select countries.country_name, sum(carbon_footprint_pcf) as co2_emission
from product_emissions
inner join countries		
	on countries.id = product_emissions.country_id
group by countries.country_name
order by co2_emission desc
limit 10`

**Result:**
| country_name | co2_emission | 
| -----------: | -----------: | 
| Spain        | 9786130      | 
| Germany      | 2251225      | 
| Japan        | 653237       | 
| USA          | 518381       | 
| South Korea  | 186965       | 
| Brazil       | 169337       | 
| Luxembourg   | 167007       | 
| Netherlands  | 70417        | 
| Taiwan       | 62875        | 
| India        | 24574        | 

**Insight:** Spain and Germany are top 2 countries contribute the most to carbon emissions

### 6. What is the trend of carbon footprints (PCFs) over the years?
**Explain:** List carbon emissions in each year

**SQL:**
`select year, sum(carbon_footprint_pcf) as total_co2_emission, round(avg(carbon_footprint_pcf),2) as avg_co2_emission
from product_emissions
group by year
order by year desc`

**Result:**
| year | total_co2_emission | avg_co2_emission | 
| ---: | -----------------: | ---------------: | 
| 2017 | 340271             | 4050.85          | 
| 2016 | 1640182            | 6891.52          | 
| 2015 | 10840415           | 43188.90         | 
| 2014 | 624226             | 2457.58          | 
| 2013 | 503857             | 2399.32          | 

**Insight:** In recent years, there has been a tendency to reduce carbon emissions. The spike in 2015 was due to "Wind Turbine" of "Gamesa Corporación Tecnológica, S.A." company in Spain

**SQL:**
`select product_name, 
	  company_name, 
	  country_name, 
	  industry_group, 
	  year,
	  sum(carbon_footprint_pcf) as co2_emission
from product_emissions as t1
	join companies as t2 on t2.id = t1.company_id
	join countries as t3 on t3.id = t1.country_id
	join industry_groups as t4 on t4.id = t1.industry_group_id
group by product_name, 
	  company_name, 
	  country_name, 
	  industry_group,
	  year
order by co2_emission desc
limit 5`

| product_name                 | company_name                            | country_name | industry_group                     | year | co2_emission | 
| ---------------------------: | --------------------------------------: | -----------: | ---------------------------------: | ---: | -----------: | 
| Wind Turbine G128 5 Megawats | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 2015 | 3718044      | 
| Wind Turbine G132 5 Megawats | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 2015 | 3276187      | 
| Wind Turbine G114 2 Megawats | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 2015 | 1532608      | 
| Wind Turbine G90 2 Megawats  | "Gamesa Corporación Tecnológica, S.A."  | Spain        | Electrical Equipment and Machinery | 2015 | 1251625      | 
| TCDE                         | "Mitsubishi Gas Chemical Company, Inc." | Japan        | Materials                          | 2017 | 198150       | 

### 7. Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?
**Explain:** Get top 10 products contribute the most to carbon emissions

**SQL:**
`select t2.industry_group, 
		sum(case when t1.year = 2013 then t1.carbon_footprint_pcf end) as co2_emission_2013,
		sum(case when t1.year = 2014 then t1.carbon_footprint_pcf end) as co2_emission_2014,
		sum(case when t1.year = 2015 then t1.carbon_footprint_pcf end) as co2_emission_2015,
		sum(case when t1.year = 2016 then t1.carbon_footprint_pcf end) as co2_emission_2016,
		sum(case when t1.year = 2017 then t1.carbon_footprint_pcf end) as co2_emission_2017
from product_emissions as t1
 join industry_groups as t2 on t2.id = t1.industry_group_id
group by t2.industry_group
order by 6 desc,5 desc,4 desc,3 desc,2 desc
limit 10`

**Result:**
| industry_group                     | co2_emission_2013 | co2_emission_2014 | co2_emission_2015 | co2_emission_2016 | co2_emission_2017 | 
| ---------------------------------: | ----------------: | ----------------: | ----------------: | ----------------: | ----------------: | 
| Materials                          | 200513            | 75678             | [NULL]            | 88267             | 213137            | 
| Capital Goods                      | 60190             | 93699             | 3505              | 6369              | 94949             | 
| Technology Hardware & Equipment    | 61100             | 167361            | 106157            | 1566              | 27592             | 
| "Food, Beverage & Tobacco"         | 4995              | 2685              | 0                 | 100289            | 3162              | 
| Commercial & Professional Services | 1157              | 477               | [NULL]            | 2890              | 741               | 
| Software & Services                | 6                 | 146               | 22856             | 22846             | 690               | 
| Automobiles & Components           | 130189            | 230015            | 817227            | 1404833           | [NULL]            | 
| Energy                             | 750               | [NULL]            | [NULL]            | 10024             | [NULL]            | 
| Media                              | 9645              | 9645              | 1919              | 1808              | [NULL]            | 
| Consumer Durables & Apparel        | 2867              | 3280              | [NULL]            | 1162              | [NULL]            | 

**Insight:** Wind Turbine is dominated in the list products contribute the most to carbon emissions
