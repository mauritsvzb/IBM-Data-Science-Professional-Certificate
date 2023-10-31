# Chicago Census, Crime, and School Data Analysis using SQL
## Context
Using a a real world dataset provided by the Chicago Data Portal, assume the role of a data analyst hired by a non-profit organization that strives to improve educational outcomes for children and youth in the City of Chicago. The job is to analyze the census, crime, and school data for a given neighborhood or district, identifying causes that impact the enrollment, safety, health, and environment ratings of schools.

Using SQL queries, anwer a number of questions about the dataset.

In this assignment:
* Download the datasets provided
* Load them into a database
* Write and execute SQL queries to answer the problems provided
* Upload screenshots showing the correct SQL queries and results for peer review.

Datasets
This assignment involves 3 datasets for the city of Chicago obtained from the Chicago Data Portal:

1. [Chicago Socioeconomic Indicators](https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/blob/main/06.%20Databases%20and%20SQL%20for%20Data%20Science%20with%20Python/05.%20Course%20Assignment/ChicagoCensusData.csv)
  * This dataset contains a selection of six socioeconomic indicators of public health significance and a hardship index, by Chicago community area, for the years 2008 – 2012. 

2. [Chicago Public Schools](https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/blob/main/06.%20Databases%20and%20SQL%20for%20Data%20Science%20with%20Python/05.%20Course%20Assignment/ChicagoPublicSchools.csv)
  * This dataset shows all school level performance data used to create CPS School Report Cards for the 2011-2012 school year. 

3. [Chicago Crime Data](https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/blob/main/06.%20Databases%20and%20SQL%20for%20Data%20Science%20with%20Python/05.%20Course%20Assignment/ChicagoCrimeData.csv)
  * This dataset reflects reported incidents of crime (with the exception of murders where data exists for each victim) that occurred in the City of Chicago from 2001 to present, minus the most recent seven days.

## Problems
The full notebook can be found [here]. It follows the assignment instructions outlined above, and answers the following problems. Screenshots to the problems are also shown below.

Problem 1: Find the total number of crimes recorded in the CRIME table.

<img src="https://user-images.githubusercontent.com/13508894/279471346-87a6d12a-c1c2-4cb3-8006-b30bbfd572c8.png" width="600" />

Problem 2: List community areas with per capita income less than 11000.

<img src="https://user-images.githubusercontent.com/13508894/279471503-ad5a96cd-5c5c-45b4-a22a-94ab1615fb51.png" width="600" />

Problem 3: List all case numbers for crimes involving minors?

<img src="https://user-images.githubusercontent.com/13508894/279471654-2ba031b2-b35c-4467-91a8-aaae02f18b60.png" width="600" />

Problem 4: List all kidnapping crimes involving a child?(children are not considered minors for the purposes of crime analysis)

<img src="https://user-images.githubusercontent.com/13508894/279471749-0469bdfd-19d3-43c6-befc-1401f28ea47f.png" width="600" />

Problem 5: What kind of crimes were recorded at schools?

<img src="https://user-images.githubusercontent.com/13508894/279471918-b41542be-aba7-44cf-ae17-fa1ccf11c124.png" width="600" />

Problem 6: List the average safety score for all types of schools.

<img src="https://user-images.githubusercontent.com/13508894/279472075-7111cde2-e5e4-4192-8cb5-d4199509ea6e.png" width="600" />

Problem 7: List 5 community areas with highest % of households below poverty line.

<img src="https://user-images.githubusercontent.com/13508894/279472146-e7563b57-dbdc-47ad-bdd9-7442a9c79d30.png" width="600" />

Problem 8: Which community area(number) is most crime prone?

<img src="https://user-images.githubusercontent.com/13508894/279472269-bac91e59-e2c7-4ab0-aea3-f8ea1c7ecd3b.png" width="600" />

Problem 9: Use a sub-query to find the name of the community area with highest hardship index.

<img src="https://user-images.githubusercontent.com/13508894/279472366-45bd648c-7a24-4f9f-a0ef-191fdead7f18.png" width="600" />

Problem 10: Use a sub-query to determine the Community Area Name with most number of crimes.

<img src="https://user-images.githubusercontent.com/13508894/279472557-7c3154c5-4392-4285-b408-0914f7fe2cf7.png" width="600" />
