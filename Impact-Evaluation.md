# Impact Evaluation 

## Executive Summary

The aim of this report is to demonstrate the impact that a piece of my work has had on my organisation. It exhibits some of the skills I have developed as a result of my learning on my Data Science apprenticeship. The piece I have selected is the creation of a dashboard which shows customers who have changed their contact details, called ‘Retailer Destination Number Changes’. 

The overall impact this work has had includes improved data quality and traceability for auditing purposes, a more streamlined process which has significantly reduced toil, enhanced insight into our customers’ behaviours, improved trust from consumers and reduced financial and reputational risk. 


## Project Background

The project was a result of a request by the Data Governance (DG) team because a pattern of behaviour had been observed: customers who had yet to pay their bills, or who had been previously had their contract terminated by the organisation, were signing up for our services using false contact details to avoid being rejected. Once they were signed up under these false details, they would then change those details back to their genuine contacts. 

This behaviour posed a financial and reputational risk to the organisation, as we aim to be a highly trusted and responsible organisation, which is only possible if those who sign up for our services are reputable and reliable. Therefore, addressing this issue was an urgent business priority. 

The project aimed to address several business challenges:

### Data Quality:
Initially, the DG team were manually searching through inconsistent and incomplete data, which reduced their capacity to find the offending customers as it was a long and laborious process, which also took time away from their other tasks. 

### Data Accessibility:
Data was siloed in various systems, making it challenging for teams to access and use data effectively.


## Approach

### Data Infrastructure & Tools

#### Data Warehouse Implementation: 
Using DBT (data build tool), I built the structure to house the incoming data in a centralised, cloud-based data warehouse (Google Cloud Platform), providing a single place for storing and accessing data.

#### ETL Pipeline: 
Developed an ETL (extract, transform, load) pipeline to ensure data from disparate sources were cleaned, transformed, and loaded into the data warehouse.

#### Data Governance:
Implemented data governance procedures to maintain data quality and consistency. The information being handled was personal identified information (PII), and so specific access requirements had to be applied and regular meetings with the DG team were arranged to ensure compliance with data governance and the Data Protection Act. 

### Data Engineering

#### Automation: 
Automated the ETL pipeline using Apache Airflow – a software which allows pipelines to be ran automatically – so that the data ingestion and transformations were ran automatically every day.

### Data Visualisation

#### Dashboard Development: 
Created a dashboard in Looker which met the requirements of the DG team and complied with data governance. 

#### Ad-Hoc Analysis: 
The dashboard had filters (e.g., type of customer) so that users could explore and utilise the data themselves to perform ad-hoc analyses. 


## Analysis Performed

### Data Quality
Data profiling was conducted to identify anomalies such as missing values, different sources not matching and de-duplicating. 

### Data Analytics
The dashboard was built in Looker using a SQL-like language called LookML. This involved stating the data relationships in the database. The process started with by creating a 'view' (the code bringing together the data needed from the data warehouse).

![view edited](https://github.com/BP0268119/Portfolio/assets/144491381/689ff23f-48da-445d-be1b-495b50c1b194)

Then the 'explore' is built - only selected data is brought through to be featured on the dashboard. This is where the filters, dimensions and measures are established.

![explore edit](https://github.com/BP0268119/Portfolio/assets/144491381/c3d335fd-0267-46f0-8f88-45f3738d67f9)

### Data Visualisation
The dashboard needed to contain two main figures (key performance indicators, KPIs): the number of the customers who changed their primary phone number and the total number of destination number changes, and this number needed to change depending on the date filter which could be changed to any length of time. 

#### The grey box is present to protect PII.
![dashboard](https://github.com/BP0268119/Portfolio/assets/144491381/14043fd4-1b77-4249-801f-1fdb3bdd598c)

Also, both KPIs can be explored in further detail. The user can alter the filters and measures (data attributes).

![Picture 1](https://github.com/BP0268119/Portfolio/assets/144491381/1375b3c1-1732-41d4-8eb9-0dae965e497d)


## Results, Impact and Value

### Improved Data Quality
Reduced erroneous data has led to improved and more efficient decision-making.

### Automation
Automation of the ETL pipeline reduced manual effort and errors. It has improved the DG team’s efficiency by removing a laborious process, allowing them to complete this task quicker and therefore complete other tasks.

### Dashboard
The GD team are now able to identify, and deal with, accounts of concern. As a result, more fraudulent accounts are being identified sooner, meaning that the business can improve its reputation and security, as well as reducing its financial and reputational risk. 

Also, there is now a singular source of truth, so different teams who may be involved (Finance, Legal, etc.) can refer to the same data. This enables efficient teamwork across different areas of the business, saving several teams from wondering whose data source is correct. 


## Future iterations and improvements
The dashboard could be improved by including more visualisations. It only displays KPIs numerically. It would be more visually appealing and useful if the dashboard included some visualisations to help identify trends quickly and easily. 

Also, create machine learning models to predict customer behaviour based on factors such as amount owed in bills, how often their contact details change, etc. This could help the DG team be even more efficient in identifying and dealing with concerning customers. 
