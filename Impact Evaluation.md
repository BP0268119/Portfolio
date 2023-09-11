# Impact Evaluation 

## Executive Summary

The aim of this report is to demonstrate the impact that a piece of my work has had on my organisation. It exhibits some of the skills I have developed as a result of my learning on my Data Science apprenticeship. The piece I have selected is the creation of a dashboard which shows customers who have changed their contact details, called ‘Retailer Destination Number Changes’. 

The overall impact this work has had includes improved data quality and traceability for auditing purposes, a more streamlined process which has significantly reduced toil, enhanced insight into our customers’ behaviours, improved trust from consumers and reduced financial and reputational risk. 


## Project Background

The project was a result of a request raised by the Data Governance (DG) team because a concerning pattern of behaviour had been observed: customers who had yet to pay their bills, or who had been previously had their contract terminated by the organisation, were signing up for our services using false contact details to avoid being rejected or chased about their unpaid bills. Once they were signed up under these false details, they would then change those details back to their genuine contacts. 

This behaviour posed a financial and reputational risk to the organisation, as we aim to be a highly trusted and responsible organisation, which is only possible if those who sign up for our services are reputable and reliable. Therefore, addressing this issue was an urgent business priority. 

The project aimed to address several business challenges:

### Data Quality:
Initially, the DG team were manually searching through inconsistent and incomplete data, which reduced their capacity to find the offending customers as it was a long and laborious process, which also took time away from their other tasks. 

### Data Accessibility:
Data was siloed in various systems, making it challenging for teams to access and use data effectively.

### Analytics Efficiency:
The lack of streamlined data processes led to inefficiencies in the DG team’s workflows.


## Approach

### Data Infrastructure & Tools

#### Data Warehouse Implementation: 
Using DBT (data build tool), I built the structure (and accompanying) documentation to house the incoming data in a centralised data warehouse using cloud-based infrastructure (Google Cloud Platform), providing a single place for storing and accessing data.

#### ETL Pipeline: 
Developed an ETL (extract, transform, load) pipeline to ensure data from disparate sources (several different tables and internal applications) were cleaned, transformed, and loaded into the data warehouse.

#### Data Governance:
Implemented data governance policies and procedures to maintain data quality and consistency. The information being handled was personal identified information (PII), and so specific access requirements had to be applied and regular meetings with the DG team were arranged to ensure compliance with data governance and the Data Protection Act. 

### Data Engineering

#### Automation: 
Automated the ETL pipeline using Apache Airflow – a software which allows pipelines to be ran automatically – so that the data ingestion and transformations were ran automatically every day.

#### Scalability: 
The infrastructure and pipeline were built in such a way that they will be able to handle different amounts of data each day, and so will be able to scale with a growing data volume.

### Data Visualisation

#### Dashboard Development: 
Created a dashboard in Looker which met the strict requirements of the DG team and complied with data governance. It was designed to be functional and to produce reports.

#### Ad-Hoc Analysis: 
The dashboard had filters available (e.g., type of customer, how many days’ worth of data) so that users could explore and utilise the data themselves to perform ad-hoc analyses. 


## Analysis Performed

### Data Quality
Data profiling was conducted in order to identify any anomalies, such as missing values, different sources not matching (e.g., different contact details for the same customer, or different numbers of changes per day depending on which source was examined) and de-duplicating. 

### Data Analytics
The dashboard was built in Looker using a SQL-like language called LookML. The build involved stating the data relationships in the database, and then which dimensions, aggregates and calculations were to be present in the dashboard. Below are some examples of the building process. The process started with by creating a 'view' (the code bringing together the data needed from the cloud-based data warehouse).

![view edited](https://github.com/BP0268119/Portfolio/assets/144491381/689ff23f-48da-445d-be1b-495b50c1b194)

Then the 'explore' is built - this is the workings behind the dashboard and only selected data is brought through to be interacted with and visualised. This is where the filters, dimensions and measures are dictated.

![explore edit](https://github.com/BP0268119/Portfolio/assets/144491381/c3d335fd-0267-46f0-8f88-45f3738d67f9)

### Data Visualization
The dashboard needed to contain two main figures (key performance indicators, KPIs): the number of the customers (referred to as “retailers”) who changed their primary phone number (referred to as “destination number”) and the total number of destination number changes, and this number needed to change depending on the date filter which could be changed to any length of time (i.e., anywhere from “all time” to the last 24 hours). 

#### The grey box is present to protect PII.
![dashboard](https://github.com/BP0268119/Portfolio/assets/144491381/14043fd4-1b77-4249-801f-1fdb3bdd598c)

As well as this, Looker enables dashboard users to drill down into the data: both KPIs can be explored in further detail. In the example below, the user has the ability to alter the filters and measures (data attributes, in this example, counts). Here, the filters and measures have been selected to the number of destination number changes (red bars) and the number of retailers who changed their destination number (blue bars) can be seen over four weeks. 

![Picture 1](https://github.com/BP0268119/Portfolio/assets/144491381/1375b3c1-1732-41d4-8eb9-0dae965e497d)


