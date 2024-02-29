# 🌐 Covid-Visualization

## 📚 About Data
Investigating Covid data from January 2020 to February 2024, including total cases, total deaths, and death percentage per country and continent. 

The dataset contains two csv tables called Covid_Deaths and Covid_Vaccinations.

## 💡 Highlights
- Total Covid cases have reached a quarter of a billion as of February 2024.
- Europe has the highest death count at 2 million deaths followed by Asia and North America at around 1.6 million deaths
- Brunei has the highest percentage of the population infected, with 76%. 

## 📂 Data Construction
Created four tables on the SQL server and copied the data to Excel to input them into Tableau.

````sql
SELECT SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) AS total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 AS DeathPercentage
FROM Portfolio_Project.dbo.Covid_Deaths
WHERE continent IS NOT NULL
ORDER BY 1,2
````
Select total cases, deaths, and overall death percentage.

````sql
SELECT location, SUM(cast(new_deaths as int)) AS TotalDeathCount
FROM Portfolio_Project.dbo.Covid_Deaths
WHERE continent  IS NULL
AND location NOT IN ('World', 'European Union', 'International', 'High income', 'Upper middle income', 'Lower middle income', 'Low income')
GROUP BY location
ORDER BY TotalDeathCount DESC
````
Select the Location column while excluding values in the WHERE statement and displaying total deaths. 

````sql
SELECT Location, Population, MAX(total_cases) AS HighestInfectionCount,  Max((total_cases/population))*100 AS PercentPopulationInfected
FROM Portfolio_Project.dbo.Covid_Deaths
GROUP BY Location, Population
ORDER BY PercentPopulationInfected DESC
````
Select all countries and display the population, maximum total cases, and percent population infected. Displays 255 rows

````sql
SELECT Location, Population,date, MAX(total_cases) AS HighestInfectionCount,  Max((total_cases/population))*100 AS PercentPopulationInfected
FROM Portfolio_Project.dbo.Covid_Deaths
GROUP BY Location, Population, date
ORDER BY Location, PercentPopulationInfected DESC
````
Select the same values as the previous query, but add the date. Displays 376,654 rows.

## 📊 Visualization 
Tableau: [Link](https://public.tableau.com/app/profile/justin.mcauliffe/viz/Covid_Project_17091625388030/Dashboard1?publish=yes) 

![Covid-1](https://github.com/justin1721/images/blob/main/Covid_Dashboard_1.png?raw=true)
